# Signal Structure

Signals are the pieces of information that are passed from block to block throughout your system. They are the fundamental message types that nio understands. Structurally, signals are objects made up of key-value pairs. The following signal has two key-value pairs:
```
{
  "name": "John Doe",
  "age": 34
}
```

In this signal, the key "name" has a value of "John Doe" and the key "age" has a value of 34. The keys are also often called "attributes." Each key or attribute has its corresponding value.

## Lists of Signals

Signals are passed from block to block and drive the system. You define your systems by designing how signals should move from block to block. However, what is actually happening is that **lists** of signals are being passed between blocks. If a block notifies only one signal, then the next block will receive a list of signals that contains that single signal.

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

In other words, the block will only call the block method `notify_signals` once for the incoming list, even though three signals would be emitted. It would not call `notify_signals` three times, one time for each signal out.
