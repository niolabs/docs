# Multiple systems

Users of the nio Platform may build and manage multiple nio systems within the nio System Designer. Sizing and division of systems should be driven by the use case.

Generally speaking, if nio instances do not interact, directly or indirectly, then they should be in different systems. This allows best practices for user access/permissions, communications with Pubkeeper, ongoing management, etc.

As an example, a multi-factory manufacturing organization may create separate systems for each physical location as their operations do not overlap or interact. They may also create a system that unifies data stores from each of the factories for organization-wide visibility.
