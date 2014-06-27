NIO Expression Properties
=========================

Given the event driven nature of most NIO applications, it can be difficult or impossible to completely describe the contents of Block properties statically. For this reason, we provide a simple syntax for accessing Signal attributes at run-time. If the value of a Block property should reflect some value that may vary from Signal to Signal, simply declare that property an ExpressionProperty and grab its value inside Block.process_signals.

Here's an example:

	class MyBlock(Block):
		expr = ExpressionProperty(default=None)
		
		def process_signals(self, signals):
			for s in signals:
				value = self.expr(s)
				# Do some stuff with the value
				
It's that simple. If the Signal under inspection is missing an attribute you ask for in the expression, the default value (provided at property initialization) is used in its place. Any other errors in the expression will raise exceptions whose handling is the responsibility of the Block developer. 

* **

NIO Scripting Syntax
====================

There are effectively two cases to consider when configuring an expression property:

* **Immediate Value** - A single python expression is evaluated and the result is returned without modification/stringification.

* **String Interpolation** - Snippets of Python code are evaluated and interpolated based on their position in an enclosing string.

###String Interpolation
String interpolation in expression properties works similarly to string interpolation in other dynamic languages. Snippets of code are delimited as such:
	
	...{{ <code goes here> }}...
	
and the result of evaluation is inserted directly into the surrounding string, replacing the code snipped and enclosing braces. The code inside the braces can be pure python, if you like, as in:

	"{{1 + 5}} dogs went to the park" -> "6 dogs went to the park"
	
Or you can use our special syntax for accessing signal properties:

	# given a signal s s.t. s.v1 == 6
    "{{$v1}} dogs went to the park" -> "6 dogs went to the park"
    
Naturally, you can combine the two approaches, as in:

	"My favorite Integer is {{$v1 if isinstance($v1, int) else 'not an Integer...'}}"
	
If you'd like to include a '$' character in a string literal inside a code snippet, just escape it with a '\'. Similarly, escaping the '}}' or '{{' with a '\' causes them to be treated as strings rather than as delimiters. For example:

	"Code snippets are delimited by \{{ and \}}" -> "Code snippets are delimited by {{ and }}"


###Immediate Value

If you'd prefer that the result of your expression evaluation not be stringified, you can populate an expression field with a single snippet enclosed in double-curlies:

	# given a signal s s.t. s.v1 == 1, s.v2 == 'two', s.v3 == [3]
	"{{[$v1, $v2, $v3]}}" -> [1, 'two', [3]]

* **

Here are some more examples that we find particularly illustrative:

	"{{1 + 5}} dogs went to the {{'p' + 'ark'}}" -> "6 dogs went to the park"
	
	# given a signal s s.t. s.v1 == {'who': 'Baron Samedi'}
	"{{$v1['who']}} and the Jets" -> "Baron Samedi and the Jets"
	
	# given a signal s s.t. s.v1 raises AttributeError, s.v2 == 'Cogito'
	# and a default value of None
	"{{$v1 or $v2}} ergo sum" -> "Cogito ergo sum"
	
	# given a signal s s.t. s.get_val() == 'foobar'
	"Opened it with a {{$get_val()}}" -> "Opened it with a foobar"




