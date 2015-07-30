# Javascript Notes

<b>When do you use Wrapping Primitives</b>
If you want to add properties.<br />
Unwrap a primitive by invoking the method valueOf(). All objects have this method. <br />
 >> new Number(123).valueOf() <br />
123 <br />
<b>Note</b> <br />
 >> Boolean(new Boolean(false))  // does not unwrap <br />
true <br />
<br />
- There is no way to overload or customize operators in JavaScript, not even equality. <br />
<br />
<b>Pitfalls</b>
>> NaN === NaN <br />
false <br />
<br />
- lenient equality is different from conversion to boolean <br />
>> 2 == true <br />
false <br />
>> 2 == false <br />
false <br />
>> 1 == true <br />
true <br />
>> 0 == false <br />
true <br />
Similarly for strings <br />
> '' == false <br />
true <br />
> '1' == true <br />
true<br />
> '2' == true <br />
false<br />
<br />
-lenient equality and objects <br />
If you compare an object to a nonobject, it is converted to a primitive, which leads to strange results: <br />
> {} == '[object Object]' <br />
true <br />
> ['123'] == 123 <br />
true <br />
> [] == 0 <br />
true <br />

<h4>Numbers</h4>
Unlike Python all numbers ara floating point numbers
<b>Exponent</b>
An exponent, eX, is an abbreviation for “multiply with 10X”: <br />
> 5e2 <br />
500 <br />
> 5e-2 <br />
0.05 <br />
<br />
Prefer Number() to parseFloat() <br />
the latter first converts to string if not a number and only then tries to parse as a number <br />
thus:<br />
> parseFloat(null)  // same as parseFloat('null') <br />
NaN <br />
> Number(null) <br />
0 <br />

Probably, not desired ouput. <br />
<br />
It also parses until the last legal character: <br />
> parseFloat('123.45#') <br />
123.45 <br />
> Number('123.45#') <br />
NaN <br />
<br />
<b> Ironically: </b><br />
> typeof NaN <br />
'number <br />

<br />
<b>Pitfalls</b>
NaN is the only value that is not equal to itself: <br />
> NaN === NaN <br />
false <br />
<br />

If you want to check whether a value is NaN, you have to use the global function isNaN(): <br />
> isNaN(NaN) <br />
true <br />
> isNaN(33) <br />
false <br />

However, isNaN does not work properly with nonnumbers, because it first converts those to numbers.  <br />
 > isNaN('xyz') <br />
true <br />
<br />

Best to do:<br />
function myIsNaN(value) { <br />
return typeof value === 'number' && isNaN(value); <br />
} <br />
<br />
<b>Infinity:</b>
Strict and lenient equality work fine for Infinity:<br />
> var x = Infinity;<br />
> x === Infinity  <br />
true <br />
<br />
Additionally, the global function <b>isFinite()</b> allows you to check whether a value is an actual number (neither infinite nor NaN):
> isFinite(5) <br />
true <br />
> isFinite(Infinity) <br />
false <br />
> isFinite(NaN) <br />
false <br />
<br />