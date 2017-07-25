# {{ book.product }} Expressions

An expression is an element of code that needs be evaluated to return a result. You can use {{ book.product }} expressions to dynamically define the value of a property when the signal enters a block. 

{{ book.product }} expressions are modeled on string interpolation in other dynamic languages. The snippets of code between the double curly braces are evaluated. For example:

```
{{ <code goes here> }}
```

The content between the curly braces is evaluated as Python code. Once the code is evaluated, the value will be replace the curly braces and its contents.

For example:

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

## Signal Property Syntax `$`

Use the `$` syntax to access signal properties:

```
# given a signal s where s.v1 == 6
"{{$v1}} dogs went to the park"
-> "6 dogs went to the park"
```

You can also combine the two approaches. For example:

```
"My favorite Integer is {{$v1 if isinstance($v1, int) else 'not an Integer…'}}"

# given a signal s where s.v1 == 6
-> "My favorite Integer is 6"

# given a signal s where s.v1 == 'A'
-> "My favorite Integer is not an Integer…"
```

## Raw Signal

You can access the raw signal itself, rather than just the attributes, with a lone `$`. As long as the character following the `$` is not a valid Python identifier, the `$` will evaluate to the incoming signal.

## Escape Characters

To include a`$` character in a string literal inside a code snippet, use an escape with a `\`. Similarly, escaping the `}}` or `{{` with a `\` causes the braces to be treated as strings rather than as delimiters. For example:

```
"Code snippets are delimited by \{{ and \}}"
-> "Code snippets are delimited by {{ and }}"
```

## Conditionals

Conditional expressions can be formatted in Python in one line as follows:

```
# given a signal s == { v1: 23, v2: "zabow!", v3: "sad trombone…"}

"When there are {{$v1}} things, we say {{$v2 if $v1 == 23 else $v3}}"
-> "When there are 23 things, we say zabow!"
"When there are {{$v1}} things, we say {{$v2 if $v1 == 42 else $v3}}"
-> "When there are 23 things, we say sad trombone…"
```

## Incorporating Libraries

The following libraries are imported by default and can be used in expressions:
  - datetime
  - json
  - math
  - random
  - re

You can import other libraries from your Python installation with the following syntax:

```
{{ __import__('module_name').method_name() }}
{{ __import__('numpy').amax([2, 1, 4]) }}
```

## Examples

Bracket notation:

```
# given a signal s where s.v1 == {'who': 'Baron Samedi'}
"{{$v1['who']}} and the Jets"
-> "Baron Samedi and the Jets"
```

Methods on signals can be called:
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

Check signal attribute exists:
```
# given a signal s where s.v1 raises AttributeError, s.v2 == 'Cogito' and a default value of None
"{{ ($v2 + ' ') if (hasattr($, 'v1') or hasattr($, 'v2')) else ''}}ergo sum"
-> "Cogito ergo sum"
"{{ ($v2 + ' ') if (hasattr($, 'v1') and hasattr($, 'v2')) else '' }}ergo sum"
-> "ergo sum"
```


Default libraries can be used in expressions:
```
# math operations are allowed by default (as are regex, datetime, random, and json)
"{{ math.sin(math.radians(90)) }}"
-> 1.0
```

Syntax error:
```
"If you don't close the brackets {{1 + 5"
-> "If you don't close the brackets {{1 + 5"
```

Raw signal with method:
```
# given a signal s == { v1: 23, v2: "zabow!", v3: "sad trombone…"}
{{ $.to_dict() }}
-> {v1: 23, v2: "zabow!", v3: "sad trombone…"}
```
