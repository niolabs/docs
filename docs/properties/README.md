# Block Properties

Block properties are the configuration fields of a block.

In the System Designer, when you double click a block, the configuration panel appears and displays the block's properties. Below is the configuration panel for a Dynamic Fields block containing the following properties: Fields, Log Level, and Version:

<img src="/img/DF-block-config.png" width="300" />

Block properties are input fields that can be edited by the user. Once edited, the block configuration can be updated or saved.

Together, a block's property configuration is what makes a block unique. A block **type name**—_Filter_, _Dynamic Fields_, _Counter Interval Simulator_, etc.—defines the **type** of the block and the fields that are available for configuration. The unique **block name**, defined when a new block is created, is what saves the configuration of a specific block and defines how that block will act on each signal. All blocks with the same **block name** share a configuration. If you change the configuration of your "isWatering" Filter block and save it, the configuration of every "isWatering" block will be be updated to match. The unique **block name** is the link to its configuration. For this reason, it is good to give your blocks unique names that reflect something about their configuration.

## Property Types

In the example above, Log Level is a drop-down menu and Version is a series of three numbers separated by dots (0.1.0), Fields is a list of input pairs. The length of the Fields list can be defined by the user with the `+ Fields` to add items and the `x` to remove items. In this example, there are three pairs defined in the list.

The different inputs in the configuration panel reflect different property types. Some properties can take any type of input while others can only take integers or select from specific options (e.g., the Log Level drop down menu is a select type). If your property input is filled with the incorrect type of content, your block will not configure and your service will not run.

Block properties can include the following types:
  - **boolean**: One of two mutually exclusive options. Usually a checkbox.
  - **string**
  - **integer**
  - **float**
  - **file**
  - **list**: List properties hold a list of object types which can contain properties themselves or can be {{ book.product }} types like IntType, etc.
  - **dictionary**: Object types contain properties themselves.
  - **select**: Select properties enumerate a list of options. For example, Log Level—found in the base block and therefore a property of all blocks—is an example of a select property type where the level can be selected from the following options: "CRITICAL, ERROR, WARNING, INFO, DEBUG, NOTSET".
  - **timedelta**: A duration property expressing the difference between two date, time, or datetime instances.
  - **version**: A version property permits saving version information with the `(major.minor.build)` format. All blocks contain this property type since it is inherited from the base block.
  - **property**: A property that can assume any type.

In the Dynamic Fields block shown above, each element of the Fields list is a dictionary defined by a property holder with two properties: "Attribute Name" and "Attribute Value". In this particular block named "ShowAlertLevel", the structure of the fields added to the signal would look something like this (for illustration purposes, the expressions in curly braces have not been evaluated, read more about expressions below):

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

Expressions are used to dynamically define properties. Many property types can accept expressions. Expressions are found inside the double curly braces. In the Dynamic Fields block configuration shown above, you can see some example expressions in the "Attribute Value" inputs. Learn more about how to create expressions in [{{ book.product }} expressions](./expressions.html).

## Environment Variables

A final syntax that {{ book.product }} uses, in addition to the above types and expressions, is the double-square-bracket notation to indicate an environment variable.

`[[YOUR_ENV_VAR]]`

Environment variables are used when you want your instance to function in different environments and/or you do not want to expose an access token or other secret.

Your environment variable can be used alone, or you can embed it, with its double-square-bracket notation, inside of strings and expressions.

If you want to embed you environment variable inside of single brackets, you will need to include a space between the single bracket and the double brackets of the environment variable:

```[ [[MY_ACCESS_TOKEN]] ]```
