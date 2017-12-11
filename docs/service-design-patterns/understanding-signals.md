# Understanding Signals

Signals are the pieces of information that are passed from block to block throughout your system. They are the fundamental messages type that nio understands. Structurally, signals are key-value objects.
```
{
  "name": "John Doe",
  "age": 34
}
```

That signal has two attributes, a `name` and an `age`.

## Lists of Signals

Signals are passed from block to block. You define your systems by designing how signals should move from block to block throughout the system. However, what is actually happening is that **lists** of signals are being passed between blocks. If a block notifies only one signal, then the next block will receive a list of signals that contains that signal.

Lists of signals are an important concept to understand. Blocks will typically operate independently on an entire list of incoming signals. This means that blocks act on the entire list of incoming signals rather than the individual signals themselves. When a block only receives one list of signals as input, you can safely assume that you will only get one list of signals as output.

For example, let's imagine a [filter block](https://blocks.n.io/Filter) that filters out a stream of odd numbers:

```
{
  "name": "Only Odds",
  "type": "Filter",
  "condition": "{{ $num % 2 == 1}}"
}
```

We can call `process_signals` on that block with a list of the following signals:
```
[
  { "num": 1 },
  { "num": 2 },
  { "num": 3 },
  { "num": 4 },
  { "num": 5 }
]
```

then the block would output the following list:

```
[
  { "num": 1 },
  { "num": 3 },
  { "num": 5 }
]
```

In other words, the block will only call `notify_signals` once for the incoming list, even though three signals would be notified. It would not call `notify_signals` three times--once for each signal out.

## Paring Down Lists of Signals

If you have a list of signals that you want to condense into fewer signals or even one signal, there are a few blocks that will help. The [join block](https://blocks.n.io/Join) is commonly used.  

The `Join` block goes through every signal in an incoming list and consolidates them into a single signal based on the specified criteria. For example, if your have your with the numbers 1 through 5 from the previous example, you can shrink the list of five signals into one signal containing two attributes--one for odds and one for evens.
```
{
  "name": "Split Odds and Evens",
  "type": "Join",
  "key": "{{ $num % 2 }}",
  "value": "{{ $num }}"
}
```

This configuration (based on the configuration of `key`\ will create a new signal with  two attributes.
```
{
  0: [2, 4],
  1: [1, 3, 5]
}
```

## Group By

By default, a block operates over an entire list of signals. However, sometimes you need to perform the block's operation multiple times over a subset of the incoming list. For example, you may want to pass around a list of all employees at a company and  want to reduce the list down to a signal that contains all of their names.
```
[
  {
    "name": "Jim Halpert",
    "department": "sales"
  },
  {
    "name": "Angela Martin",
    "department": "accounting"
  },
  {
    "name": "Stanley Hudson",
    "department": "sales"
  }
]
```
You can use a `Join` block to create a signal where the key is the department name and the value of that key is a list of names in the department.
```
{
  "name": "List Names",
  "type": "Join",
  "key": "{{ $department }}",
  "value": "{{ $name }}"
}
```

The block configuration results in a single output signal.
```
{
  "sales": ["Jim Halpert", "Stanley Hudson"],
  "accounting": ["Angela Martin"]
}
```

That looks great, but what if you want to have a separate signal for each department, but still have a list of names. One inefficient option would be to filter the stream based on the department, and then put the individual streams into copies of the `Join` block from before. The following image displays this example. Note that this is **not** the advised way to do this.

![Bad HashTable](/img/bad-hash-table.png)

There are several downsides to this approach.

* It is not dynamic based on department. If we add another department, we have to add a new `Filter` block and replicate the `HashTable` again.
* You lose your original list. When the chain started you had a list of all employees, and now you have different lists floating around. You would have to merge the streams back together to get a list of all the employee names.
* It is very tedious and repetitive. We have the same blocks used over and over again.

The [Group By mixin](https://github.com/niolabs/nio/tree/master/nio/block/mixins/group_by) groups the signals into smaller lists first before performing the same action. This is very similar to the SQL [`GROUP BY`](https://www.w3schools.com/sql/sql_groupby.asp) operator. Fortunately, the `HashTable` block uses the Group By mixin, so you can eliminate the `Filter` blocks and rely on only one `HashTable` block. The block will group the hash table functionality by the department of the employee. Since you don't need the department name as the signal attribute key anymore, you can hard code that to be a string `"names"` instead.

```
{
  "name": "List Names",
  "type": "HashTable",
  "key": "names",
  "value": "{{ $name }}",
  "group_by": "{{ $department }}"
}
```

You added an attribute to your block configuration indentifying the value to group by. The output of the block is a list of two signals, one for each department. Again, remember that since you only have one list of inputs, you can only have one list of outputs. Even though there are two signals being notified, they will be notified together in the same list.
```
[
  {
    "group": "accounting",
    "names": ["Angela Martin"]
  },
  {
    "group": "sales",
    "names": ["Jim Halpert", "Stanley Hudson"]
  }
]
```

Understanding how Group By works and when to use it can save a lot of headaches and repetition in nio services allowing you to build very powerful services without many blocks. In general, if you are frequently repeating the same blocks when designing in nio, there is probably a more efficient way to perform the task.
