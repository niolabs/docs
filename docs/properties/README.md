# Block Properties

Block properties are the configuration fields of a block.

In the System Designer, when you double-click a block, the configuration panel  displays the block's properties. Below is the configuration panel for a Dynamic Fields block containing three properties: Fields, Log Level, and Version

<img src="/img/DF-block-config.png" width="300" />

Block properties are input fields that can be edited and updated and saved with the block configuration.

The property configuration of the block makes it unique. A **block type name**—_Filter_, _Dynamic Fields_, _Counter Interval Simulator_—defines the block type and the configurable fields. Each block types has an abbreviation such as _DF_ for _Dynamic Fields_. The unique **block name**, defined when created, saves configuration of the specific block and defines how the block acts on signals. All blocks with the same **block name** share a configuration. If you change the configuration of your "isWatering" Filter block, the configuration of every "isWatering" block will be be updated to match. The unique **block name** is the link to its configuration. For this reason, it is good to give your blocks unique names that reflect their configuration.

## Property Types

In the example above, Log Level is a drop-down menu and Version is a series of three numbers separated by periods (0.1.0), and Fields is a list of input pairs. The length of the Fields list can be defined by the user with `+ Fields` to add items and `x` to remove items. In this example, there are three pairs defined in the list.

The different inputs in the configuration panel reflect different property types. Some properties can take any type of input while others can only take integers or select from specific options (e.g., the Log Level drop-down menu is a select type). If your property input is filled with the incorrect type of content, your block will not configure and your service will not run.

Block properties can include the following types:
  - **boolean**: One of two mutually exclusive options. Usually a check box.
  - **string**
  - **integer**
  - **float**
  - **file**
  - **list**: List properties hold a list of object types which contain properties themselves or can be {{ book.product }} types such as IntType.
  - **dictionary**: Object types contain properties themselves.
  - **select**: Select properties enumerate a list of options. For example, Log Level—found in the base block and therefore a property of all blocks—is an example of a select property type where the level can be selected from the following options: CRITICAL, ERROR, WARNING, INFO, DEBUG, NOTSET.
  - **timedelta**: A duration property expressing the difference between two date, time, or datetime instances.
  - **version**: A version property permits saving version information with the `(major.minor.build)` format. All blocks contain this property type since it is inherited from the base block.
  - **property**: A property that can assume any type.

In the Dynamic Fields block shown above, each element of the Fields list is a dictionary defined by a property holder with two properties: Attribute Name and Attribute Value. In this particular block named `ShowAlertLevel`, the structure of the fields added to the signal would look something as follows. For illustration purposes, the expressions in curly braces have not been evaluated.

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

Expressions are used to dynamically define properties. Many property types can accept expressions. Expressions are found inside the double curly braces. In the Dynamic Fields block configuration shown above, you can see example expressions in the Attribute Value inputs. Learn more about how to create expressions in [{{ book.product }} expressions](./expressions.html).

## Environment Variables

Another syntax that {{ book.product }} uses is the double-square-bracket notation to indicate an environment variable.

`[[YOUR_ENV_VAR]]`

Environment variables are used when you want your instance to function in different environments or you do not want to expose an access token or other secret.

Your environment variable can be used alone, or you can embed it, with the double-square-bracket notation, inside of strings and expressions.

To embed you environment variable inside of single brackets, you need to include a space between the single bracket and the double brackets of the environment variable:

```[ [[MY_ACCESS_TOKEN]] ]```
