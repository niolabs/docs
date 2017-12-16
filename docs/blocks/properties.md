# Block Properties

Block properties are the configuration fields of a block.

In the System Designer, when you double-click a block, the configuration panel displays the block's properties. The configuration panel for a _Modifier_ block is shown below. It displays four properties: **Exclude Existing Fields**, **Fields**, **Log Level**, and **Version**.

<img src="/img/modifier-block-config.png" width="300" />

The input fields are block properties that can be edited, updated, and saved to create a configured block.

The property configuration of the block makes it unique. A **block type name**—_Filter_, _Modifier_, _Counter Interval Simulator_—defines the block type and the configurable fields. (In the System Designer, this name is abbreviated in a vertical bar on the left side of the block.) The unique **block name**, which you define when dragging a new instance of the block type onto the canvas of the System Designer, saves a specific configuration of the block and defines how the block acts on signals. All blocks with the same **block name** share a configuration. For example, if you change the configuration of your "isWatering" _Filter_ block, the configuration of every "isWatering" block will be be updated to match. The unique **block name** is the link to a block's property configuration. For this reason, it is good to give your blocks descriptive names that reflect their configured properties.

## Property Types

In the example above, Exclude Existing Fields is a checkbox, Fields is a list of input pairs, Log Level is a drop-down menu, and Version is a series of three numbers separated by periods (0.1.0).

The different types of inputs in the configuration panel represent different [property types](../block-development/development.md#property-types).

In the above example, Exclude Existing Fields is a "BoolProperty" that can be true or false and is represented by a checkbox. Log Level is a "SelectProperty" that enumerates available options and is represented by a drop-down menu. Fields is a "ListProperty" and is represented by a list of items that can be defined by the user with `+ Fields` to add items and `x` to remove items. In this example, there are three key-value pairs defined in the list. Each item in a list can also have a type, in this case, a dictionary defined by a "PropertyHolder" property made up of two properties represented by the Attribute Name and Attribute Value input areas. And finally, Version is a special "VersionProperty" that takes three integers separated by periods.

Some properties (the base Property property) can take any type of input while others require specific types of input. The IntProperty can only take integers while the SelectProperty requires a selection from a specific list. If your property input is filled with the incorrect type of content, your block will not configure and your service will not run.

In the _Modifier_ block shown above, the `ShowAlertLevel` block is configured so that it will enrich the signal with three new fields, one each for danger, caution, and success. The structure of the fields added to the signal would look similar to the following. (For illustration purposes, the expressions in curly braces have not been evaluated.)

```python
[
  {
    "attribute_name": "danger_label",
    "attribute_value": {{ $alert_value }}
  },
  {
    "attribute_name": "caution_label",
    "attribute_value": {{ $warning_value }}
  },
  {
    "attribute_name": "success_label",
    "attribute_value": {{ $ok_value }}
  },
]
```

## Expressions

Expressions are used to dynamically define properties. Many property types can accept expressions. Expressions are found inside the double curly braces. In the _Dynamic Fields_ block configuration shown above, you can see example expressions in the Attribute Value inputs. Learn more about how to create expressions in [nio Expressions](/blocks/expressions.md).

## Environment Variables

Another syntax that nio uses in property configuration is the double-square-bracket notation for an [environment variable](/services/service-design-patterns/environment-variables.md).

`[[YOUR_ENV_VAR]]`

Environment variables are used when you want your instance to function in different environments or you do not want to expose an access token or other secret.

Your environment variable can be used alone, or you can embed it, with the double-square-bracket notation, inside of strings and expressions.

To embed you environment variable inside of single brackets, you need to include a space between the single bracket and the double brackets of the environment variable

```[ [[MY_ACCESS_TOKEN]] ]```