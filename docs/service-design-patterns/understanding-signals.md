# Understanding Signals

Signals are the pieces of information that are passed from block to block throughout your system. They are the fundamental message type that {{ book.product }} understands. Structurally, signals are key-value objects. Here is an example of a signal:

```
{
  "name": "John Doe",
  "age": 34
}
```

That signal has two attributes, a `name` and an `age`.

## Lists of Signals

Signals are passed from block to block. You define your systems by designing how signals should move from block to block throughout the system. However, what is actually happening under the hood is that **lists** of signals are being passed between blocks. If a block notifies only one signal, then the next block will receive a list of signals that contains that signal.

Lists of signals are an important concept to understand. Blocks will typically operate independently on an entire list of incoming signals. This means that blocks act on the entire list of incoming signals rather than the individual signals themselves. When a block only receives one list of signals as input, you can safely assume that you will only get one list of signals as output.

For example, let's imagine a [filter block](https://github.com/nio-blocks/filter) that filters out a stream of odd numbers:

```
{
  "name": "Only Odds",
  "type": "Filter",
  "condition": "{{ $num % 2 == 1}}"
}
```

If we called `process_signals` on that block with a list of the following signals:

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

In other words, the block will only call `notify_signals` once for the incoming list, even though three signals would be notified. It would **not** call `notify_signals` three times--once for each signal out.

## Paring Down Lists of Signals

If you have a list of signals but want to condense it into fewer signals or even one signal. There are a few blocks that will help you do that. The [hash table block](https://github.com/nio-blocks/hash_table.git) is commonly used ones.  

The `HashTable` block goes through every signal in an incoming list and consolidates them into a single signal based on the specified criteria. For example, if we have our signals with the numbers 1 through 5 from the previous example, we can shrink the list of five signals into one signal containing two attributes--one for odds and one for evens. The following block configuration would do that:

```
{
  "name": "Split Odds and Evens",
  "type": "HashTable",
  "key": "{{ $num % 2 }}",
  "value": "{{ $num }}"
}
```

More explanation of the `HashTable` block's behavior can be found on the [GitHub README](https://github.com/nio-blocks/hash_table.git), but this configuration will create a new signal that has two attributes \(based on the configuration of `key`\). The resulting output signal would look like this:

```
{
  0: [2, 4],
  1: [1, 3, 5]
}
```

## Group By

In a normal condition a block would operate over an entire list of signals. However, sometimes it is useful to perform the block's operation multiple times over a subset of the incoming list. For example, we may be passing around a list of all employees at a company and we want to reduce the list down to a signal that contains all of their names. Here is an example data set:

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

We could use a `HashTable` block to create a signal where the key was the department name and the value of that key was a list of names in the department like so:

```
{
  "name": "List Names",
  "type": "HashTable",
  "key": "{{ $department }}",
  "value": "{{ $name }}"
}
```

This block config would result in a single output signal:

```
{
  "sales": ["Jim Halpert", "Stanley Hudson"],
  "accounting": ["Angela Martin"]
}
```

That looks great, but what if we wanted to have a separate signal for each department, but still have a list of names. One inefficient option would be to filter the stream based on the department, and then put the individual streams into copies of the `HashTable` block from before. The following image displays this example. Note that this **not** the advised way to do this:

![Bad HashTable](/img/bad-hash-table.png)

There are several downsides to this approach.

1. It is not dynamic based on department. If we add another department, we have to add a new `Filter` block and replicate the `HashTable` again.
2. We lose our original list. When the chain started we had a list of all employees, now we have different lists floating around. We would have to merge the streams back together to get a list of all employee names again.
3. It is very tedious and repetitive. We have the same blocks used over and over again.

But we have a solution! Enter the [Group By mixin](https://github.com/nioinnovation/nio/tree/master/nio/block/mixins/group_by). To group the signals into smaller lists first before performing the same action, this mixin can be added. This is very similar to how SQL's [`GROUP BY`](https://www.w3schools.com/sql/sql_groupby.asp) operator works. Fortunately, the `HashTable` block uses the Group By mixin, so we can drop all of those pesky `Filter` blocks and rely on only one `HashTable` block. The block will group the hash table functionality by the department of the employee. And since we don't need the department name as the signal attribute key anymore, we can hard code that to be a string `"names"` instead. The block's config looks like this:

```
{
  "name": "List Names",
  "type": "HashTable",
  "key": "names",
  "value": "{{ $name }}",
  "group_by": "{{ $department }}"
}
```

Notice we've just added an attribute to our block config indentifying the value to group by. The output of the block will be a list of two signals, one for each department. Again, remember that since we had only one list of inputs, we can only have one list of outputs. Even though there are two signals being notified, they will be notified together in the same list. The block's output looks like this:

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

Understanding how Group By works and when to use it can save a lot of headaches and repetition in {{ book.product }} services. It can also allow you to build very powerful services without many blocks. In general, if you are frequently repeating the same blocks when designing in {{ book.product }}, there is probably a more efficient way of performing the task.
