# Signals

Signals are the packets of information that are passed from block to block throughout your nio system. They are the fundamental message types that the nio Platform understands.

Structurally, signals are made of key-value pairs. The following signal has two key-value pairs:
```
{
  "name": "John Doe",
  "age": 34
}
```

In this signal, the key "name" has a value of "John Doe" and the key "age" has a value of 34. Each key has a corresponding value separated by a colon. The key-value pair together is called an "attribute" of a signal.

A signal is denoted by curly braces with its inner attributes separated by commas.

---

## Lists of signals

In nio, signals are passed from block to block as lists. You define your services by designing how lists of signals move from block to block. Signals always travel between blocks as part of a list, even if there is only one signal in that list. Blocks will typically operate on an entire list of incoming signals as one event.

For example, let's imagine a [_Filter_](https://blocks.n.io/Filter) block that we have set up to filter out a stream of odd numbers:

<img class="shadow left" src="/img/signals/filter-block-config.png" width="275"/>

<br>

If the block receives the following incoming list of five signals:

```
[
  { "num": 1 },
  { "num": 2 },
  { "num": 3 },
  { "num": 4 },
  { "num": 5 }
]
```

the block will output the following list from the **true** terminal:

```
[
  { "num": 1 },
  { "num": 3 },
  { "num": 5 }
]
```

and the following list from the **false** terminal:

```
[
  { "num": 2 },
  { "num": 4 }
]
```

In other words, the _Filter_ block will process one list of five incoming signals and each output terminal will emit one list of outgoing signals.

> **[info] Tip**
>
> A helpful way to view lists of signals is to use the _Counter_ block. The _Counter_ block will output the length of each list of signals.
>

---
## See also

* Glossary—[Signal](/glossary/README.md#signal)
