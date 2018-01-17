# Communication between instances

Instance-to-instance communication in the nio Platform uses standard [publish-subscribe patterns](/services/service-design-patterns/pub-sub.md) and is brokered by [Pubkeeper](/pubkeeper/README.md).

Instances, for the most part, run on separate computers. The beauty of nio pub-sub functionality is that users don’t need to think in those terms within a nio system—simply publish and subscribe as if the instances were one-in-the-same. The lines between the distinct hardware in a system fade into the background.

For most users, [Pubkeeper](/pubkeeper/README.md) is a silent communications enabler. Advanced users may dive deeper into functionality and configuration for their systems.
