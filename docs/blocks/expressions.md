# nio expressions

The nio Platform leverages Python syntax inside blocks to operate on signals. To perform block operations using Python, simply place your desired expression between two sets of curly brackets `{{ }}` inside a block configuration field. In addition to Python, block configurations can also accept environment variables by using two sets of double brackets `[[ ]]`, as well as string values without any brackets. For more information on environment variables, please see our documentation here: <https://docs.n.io/instances/environment-variables.html>.

```
{{ <code goes here> }}
```

---

## Signal property syntax

Signals in nio are passed as key value pairs `{“key1”: value1, “key2”: value2}`. Use the `$` syntax to access signal properties.

```
# given a signal {"dogs": 6}
"{{$dogs}} dogs went to the park"
-> "6 dogs went to the park"
```

---

## Raw signal

You can access the raw signal itself, rather than just the attributes, with a lone `$`. As long as the character following the `$` is not a [valid Python identifier](https://docs.python.org/3/reference/lexical_analysis.html#identifiers), the `$` will evaluate to the incoming signal.

---

## nio expression examples

### Rename a signal

<img class="right border" src="/img/expressions/rename.png" width="250"/>

With an incoming signal of `{“sim”: 1}`, we can rename it inside a _Modifier_ block.

This will create a new signal attribute called "new" with the same value as `sim`.

The new output signal will be `{"new": 1, "sim": 1}`.

To remove `{“sim”: 1}` from the output, check the **Exclude existing fields?** block property.

### Math operations

<img class="right border" src="/img/expressions/plus-one.png" width="250"/>

With an incoming signal of `{“sim”: 1}` we can perform math inside a _Modifier_ block.

This operation creates a new attribute **plus_one** that will be equal to `sim + 1`.

The new output signal will be `{"plus_one": 2, "sim": 1}`.

### Create attributes

<img class="right border" src="/img/expressions/string-input.png" width="250"/>

Anything typed directly into a field is stored in the signal as a string:  `{"string": "this is a string"}`.

### Conditionals

<img class="right border" src="/img/expressions/logic.png" width="250"/>

Expressions can perform logic.

The signal stream `{“sim”: 1}, {“sim”: 0}` will result in the following signal output:

```
{"sim": 1, "zero": false}
{"sim": 0, "zero": true}
```

### Negation

<img class="right border" src="/img/expressions/negation.png" width="250"/>

Negation (!=) can also be used.

The signal stream `{“sim”: 1}, {“sim”: 0}` will result in the following signal output:

```
{"sim": 1, "zero": false}
{"sim": 0, "zero": true}
```

### Timestamp (default libraries)

<img class="right border" src="/img/expressions/timestamp.png" width="250"/>

nio expressions allow you to import the following Python libraries by default:

- datetime
- json
- math
- random
- re

`datetime`, used to apply a timestamp to data as shown will output:

```
{"timestamp": "2017-12-13 23:52:09.661182"}
```

### Library imports

Additional Python libraries can be imported within blocks for more advanced or specific operations.

```
{{ __import__('module_name').method_name() }}
```
For example, to import the `amax` method from numpy:
```
{{ __import__('numpy').amax([2, 1, 4]) }}
```
