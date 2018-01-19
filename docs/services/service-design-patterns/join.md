# Restructure and group signals

If you have a list of signals that you want to condense into fewer signals or even one signal, there are a few nio Blocks that will help. The [_Join_ block](https://blocks.n.io/Join) is commonly used.

---

## Paring down lists of signals with the Join block

The _Join_ block goes through every signal in an incoming list and consolidates them into a single signal based on the specified criteria. For example, if you have your signal with the numbers 1 through 5 from the previous example, you can shrink the list of five signals into one signal containing two attributes—one for odds and one for evens.
```
{
  "name": "Split Odds and Evens",
  "type": "Join",
  "key": "{{ $num % 2 }}",
  "value": "{{ $num }}"
}
```

This configuration (based on the configuration of `key`) will create a new signal with two attributes.
```
{
  0: [2, 4],
  1: [1, 3, 5]
}
```

---

## Using group-by

By default, a block operates over an entire list of signals. However, sometimes you need to perform the block's operation multiple times over a subset of the incoming list. For example, you may want to pass around a list of all employees at a company and want to reduce the list down to a signal that contains all of their names.
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
You can use a _Join_ block to create a signal where the key is the department name and the value of that key is a list of names in that department.
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

That looks great, but what if you want to have a separate signal for each department, but still have a list of names. One inefficient option would be to filter the stream based on the department and then put the individual streams into copies of the _Join_ block from before. The following image displays this example.

> **[danger] Inefficient Join**
>
> This is **not** the advised way to create separate lists of signals by group.
>
> <img class="border display" src="/img/bad-join.png" height="350" />
>

There are several downsides to this approach.

* It is not dynamic based on department. If we add another department, we have to add a new _Filter_ block and replicate the _Join_ again.
* You lose your original list. When the chain started you had a list of all employees, and now you have different lists floating around. You would have to merge the streams back together to get a list of all the employee names.
* It is very tedious and repetitive. We have the same blocks used over and over again.

The [group-by mixin](https://github.com/niolabs/nio/tree/master/nio/block/mixins/group_by) can group the signals into smaller lists first before performing the same action. This is very similar to the SQL [`GROUP BY`](https://www.w3schools.com/sql/sql_groupby.asp) operator. Fortunately, the _Join_ block includes the group-by mixin, so you can eliminate the _Filter_ blocks and rely on only one _Join_ block. Using the group-by mixin, the block will first group the signals by the department attribute under a new key called "group". Then, since you don't need the department name as the key to the list of names anymore, you can hard code the new key to be the string `"names"` instead.

```
{
  "name": "List Names",
  "type": "Join",
  "key": "names",
  "value": "{{ $name }}",
  "group_by": "{{ $department }}"
}
```

You added an attribute to your block configuration identifying the attribute to group by. The output of the block is a list of two signals, one for each department. Again, remember that since you only have one list of inputs, you can only have one list of outputs. Even though there are two signals being notified, they will be notified together in the same list.
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

Understanding how group-by works and when to use it can save a lot of headaches and repetition in nio services, allowing you to build very powerful services without many blocks. In general, if you are frequently repeating the same blocks when designing with the nio Platform, there is probably a more efficient way to perform the task.
