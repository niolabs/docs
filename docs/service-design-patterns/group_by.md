# Using Signal Groups

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
You can use a [_Join_](https://docs.n.io/service-design-patterns/join.html) block to create a signal where the key is the department name and the value of that key is a list of names in that department.
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

That looks great, but what if you want to have a separate signal for each department, but still have a list of names?

One inefficient option would be to filter the stream based on the department and then put the individual streams into copies of the _Join_ block from before. The following image displays this example.

> **[danger] Inefficient use of _<span class="allow-caps">Join</span>_ block**
>
> This is **not** the advised way to create separate lists of signals by group.
>
> <img class="border display" src="/img/bad-join.png" height="350" />
>

There are several downsides to this approach.

* It is not dynamic based on department. If you add another department, you have to add a new _Filter_ block and replicate the _Join_ again.
* You lose your original list. When the chain started you had a list of all employees, and now you have different lists floating around. You would have to merge the streams back together to get a list of all the employee names.
* It is very tedious and repetitive. You have the same blocks used over and over again.

The [group-by mixin](https://docs.n.io/blocks/block-development/mixins.html) can group the signals into smaller lists first before performing the same action. This is very similar to the SQL [`GROUP BY`](https://www.w3schools.com/sql/sql_groupby.asp) operator. Fortunately, the _Join_ block includes the group-by mixin, so you can eliminate the _Filter_ blocks and rely on only one _Join_ block. Using the group-by mixin, the block will first group the signals by the department attribute under a new key called "group". Then, since you don't need the department name as the key to the list of names anymore, you can hard code the new key to be the string `"names"` instead.

```
{
  "name": "List Names",
  "type": "Join",
  "key": "names",
  "value": "{{ $name }}",
  "group_by": "{{ $department }}"
}
```

You added an attribute to your block configuration identifying the attribute to group by. The output of the block is a list of two signals, one for each department. Again, remember that since you only have one list of inputs, you can only have one list of outputs. Even though there are two signals being emitted, they will be emitted together in the same list.
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
