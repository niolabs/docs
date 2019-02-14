# nio Block Standard Library

Different nio binaries support different blocks. The main nio binary is written in Python 3 and uses Python-based blocks. However, other alternative binaries are available for enterprise customers and support different blocks.

There is, however, a set of blocks that is guaranteed to exist within every nio binary. These blocks tend to be used for manipulating signal streams and integrating with <a href="/pubkeeper">Pubkeeper</a> communications. The standard library blocks all follow the same block specifications as well, allowing you to design your nio services using these blocks without concern for which binary they will run on.

Here are the current blocks included in the nio Block Standard Library:

 * **Communication**
   * <a href="https://blocks.n.io/Publisher">Publisher</a>
   * <a href="https://blocks.n.io/Subscriber">Subscriber</a>
 * **Signal Modifiers**
   * <a href="https://blocks.n.io/Modifier">Modifier</a>
   * <a href="https://blocks.n.io/ConditionalModifier">ConditionalModifier</a>
   * <a href="https://blocks.n.io/AttributeSelector">AttributeSelector</a>
   * <a href="https://blocks.n.io/Join">Join</a>
   * <a href="https://blocks.n.io/Replicator">Replicator</a>
 * **Stateful Blocks**
   * <a href="https://blocks.n.io/StateChange">StateChange</a>
   * <a href="https://blocks.n.io/AppendState">AppendState</a>
   * <a href="https://blocks.n.io/Switch">Switch</a>
 * **Signal Flow**
   * <a href="https://blocks.n.io/Filter">Filter</a>
   * <a href="https://blocks.n.io/Debounce">Debounce</a>
   * <a href="https://blocks.n.io/SignalTimeout">SignalTimeout</a>
   * <a href="https://blocks.n.io/MergeStreams">MergeStreams</a>
 * **Miscellaneous**
   * <a href="https://blocks.n.io/Logger">Logger</a>
   * <a href="https://blocks.n.io/CounterIntervalSimulator">CounterIntervalSimulator</a>
   * <a href="https://blocks.n.io/IdentityIntervalSimulator">IdentityIntervalSimulator</a>
