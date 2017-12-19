# nio Expressions

nio leverages Python syntax inside blocks to operate on signals. To perform block operations using Python, simply place your desired expression between two sets of curly brackets `{{ }}` inside a block configuration field. In addition to Python, block configurations can also accept environment variables by using two sets of double brackets `[[ ]]`, as well as string values without any brackets. For more information on environment variables, please see our documentation here: [https://docs.n.io/service-design-patterns/environment-variables.html](https://docs.n.io/service-design-patterns/environment-variables.html)

```
{{ <code goes here> }}
```

## Signal Property Syntax `$`

Signals in nio are passed as key value pairs `{“key1”: value1, “key2”: value2}`. Use the `$` syntax to access signal properties.

```
# given a signal {"dogs": 6}
"{{$dogs}} dogs went to the park"
-> "6 dogs went to the park"
```

## Raw Signal

You can access the raw signal itself, rather than just the attributes, with a lone `$`. As long as the character following the `$` is not a [valid Python identifier](https://docs.python.org/3/reference/lexical_analysis.html#identifiers), the `$` will evaluate to the incoming signal.

## nio Expression Examples

### Rename a Signal

With an incoming signal of `{“sim”: 1}`, we can rename it inside a modifier block:

![rename a signal](/img/expressions/rename.png)

This will create a new signal attribute called "new" with the same value as `sim`.
The new output signal will be `{"new": 1, "sim": 1}`.  

To remove `{“sim”: 1}` from the output, check the **Exclude existing fields?** block property.

### Math Operations

With an incoming signal of `{“sim”: 1}` we can perform math inside a modifier block:

![math](/img/expressions/plus-one.png)

This operation creates a new attribute `plus_one` that will be equal to `sim + 1`.
The new output signal will be `{"plus_one": 2, "sim": 1}`.

### Create Attributes

Anything typed directly into a field is stored as a string, for example:

![string](/img/expressions/string.png)

This will create the following signal:  `{"string": "this is a string"}`.

### Conditionals:
Expressions can perform logic.

With a signal stream `{“sim”:1}, {“sim”: 0}`:

![logic](/img/expressions/logic.png)

Will result in the following signal output:
```
{"sim": 1, "zero": false}
{"sim": 0, "zero": true}
```

### Negation:
Negation (!=) can also be used.
With a signal stream `{“sim”:1}, {“sim”: 0}`:

![negation](/img/expressions/negation.png)

Will result in the following signal output:
```
{"sim": 1, "zero": false}
{"sim": 0, "zero": true}
```

### Timestamp (default libraries):
nio expressions allow you to import the following Python libraries by default:
- datetime
- json
- math
- random
- re

Datetime, used to apply a timestamp to data:

![timestamp](/img/expressions/timestamp.png)

Will output:
`{"timestamp": "2017-12-13 23:52:09.661182"}`

### Library Imports:

Additional Python libraries can be imported within blocks for more advanced or specific operations.

```
{{ __import__('module_name').method_name() }}
{{ __import__('numpy').amax([2, 1, 4]) }}
```

In addition to the default library imports, additional python libraries can be imported within blocks for more advanced or specific operations.
{{ __import__('module_name').method_name() }}
{{ __import__('numpy').amax([2, 1, 4]) }}



Bracket notation can be used.

```
# given a signal s where s.v1 == {'who': 'Baron Samedi'}
"{{$v1['who']}} and the Jets"
-> "Baron Samedi and the Jets"
```

Methods on signals can be called.
```
# given a signal s where s.get_val() == 'foobar'
"Opened it with a {{$get_val()}}"
-> "Opened it with a foobar"
```
```
# given a signal s where s has the attribute v1 but not v2
"{{hasattr($, 'v1') and hasattr($, 'v2')}}"
-> False
```

Check that a signal attribute exists.
```
# given a signal s where s.v1 raises AttributeError, s.v2 == 'Cogito' and a default value of None
"{{ ($v2 + ' ') if (hasattr($, 'v1') or hasattr($, 'v2')) else ''}}ergo sum"
-> "Cogito ergo sum"
"{{ ($v2 + ' ') if (hasattr($, 'v1') and hasattr($, 'v2')) else '' }}ergo sum"
-> "ergo sum"
```

Default libraries can be used in expressions.
```
# math operations are allowed by default (as are regex, datetime, random, and json)
"{{ math.sin(math.radians(90)) }}"
-> 1.0
```

Syntax error
```
"If you don't close the brackets {{1 + 5"
-> "If you don't close the brackets {{1 + 5"
```

Raw signal with method
```
# given a signal s == { v1: 23, v2: "zabow!", v3: "sad trombone…"}
{{ $.to_dict() }}
-> {v1: 23, v2: "zabow!", v3: "sad trombone…"}
```

## Incorporating Libraries

The following libraries are imported by default and can be used in expressions:
  - datetime
  - json
  - math
  - random
  - re

You can import other libraries from your Python installation.

```
{{ __import__('module_name').method_name() }}
{{ __import__('numpy').amax([2, 1, 4]) }}
```
## Escape Characters

To include a $ character in a string literal inside a piece of code, use the backslash (`\`) character to escape it. Similarly, escaping the `}}` or `{{` with a `\` causes the braces to be treated as strings rather than as delimiters.

```
"Code snippets are delimited by \{{ and \}}"
-> "Code snippets are delimited by {{ and }}"
```

## Conditionals

Conditional expressions can be formatted in Python in one line.

```
# given a signal s == { v1: 23, v2: "zabow!", v3: "sad trombone…"}

"When there are {{$v1}} things, we say {{$v2 if $v1 == 23 else $v3}}"
-> "When there are 23 things, we say zabow!"
"When there are {{$v1}} things, we say {{$v2 if $v1 == 42 else $v3}}"
-> "When there are 23 things, we say sad trombone…"
```

Once the code is evaluated, the value will be replaced by the curly braces and its contents.

```
"{{1 + 5}} dogs went to the park"
-> "6 dogs went to the park"
"{{1 + 5}} dogs went to the {{'p'+'ark'}}"
-> "6 dogs went to the park"
```
Inner dictionaries need spaces before and after the curly braces.
```
'{{ {"a": 1} }}' -> {"a": 1}
```
