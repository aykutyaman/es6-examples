Accessing a `let`-declared variable earlier than its `let ..` declaration/initialization
causes an error. Temporal Dead Zone error
```
{
  // console.log(z);  // Reference Error
  console.log(m);     // undefined

  let z;
  var m;
}
```

let creates variable declaration for each loop which is block level declaration.
```
var funcs = [];
for (var i = 0; i < 5; i++) {
  console.log(i);
  funcs.push( function(){
    console.log( i, 'here' );
  } );
}
funcs[0]();
```

Block-scoped functions
```
{
  foo();        // works
  function foo() {
    // ...
  }
}
foo();
```

`...` instead of spreading out a value out, can gathers a set of values toghether
into an array.
```
function bar(x, y, ...z) { // gather the rest of the arguments (if any) into an array called z." 
  console.log(x, y, z);
}
bar(1, 2, 3, 4, 5);          // 1, 2, [3, 4, 5]
```


A reference to an identifier in a default value expression first matches the formal parameters'
scope before looking to an outer scope.
```
var w = 1, z = 2;

function foo( x = w + 1, y = x + 1, z = z + 1 ) {
	console.log( x, y, z );
}

foo();	                     // Reference error (for z)
```

*Object Property Assignment Pattern*
```
function bar() {
	return {
		x: 4,
		y: 5,
		z: 6
	};
}
var { x: bam, y: baz, z: bap } = bar();
```
`x: bam` means the `x` property is the source value and `bam` is the target variable to assign to

You can map an object to an array, such as:
```
var o1 = { a: 1, b: 2, c: 3 },
    a2 = [];
({a: a2[0], b: a2[1], c: a2[2]} = o1)

console.log(a2);                    //  [1, 2, 3]
```
or the other way around:
```
var a1 = [1, 2, 3],
    o2 = {};
[o2.a, o2.b, o2.c] = a1;

console.log(o2.a, o2.b, o2.c);     // 1, 2, 3
```

you can even solve the traditional "swap two variables" task without a temporary variable:
```
var x = 10, y = 20;

[y, x] = [x, y];

console.log(x, y);                 // 20, 10
```

## Repeated Assignments
Source property listed multiple times
```
var {a: X, a: Y} = {a: 1};
X;        // 1
Y;        // 1
```

You can both destructure a sub-object/array property and also capture the sub-object/array's value itself
```
var {a: {x: X, x: Y}, a} = {a: {x: 1}

X;    // 1
Y;    // 1
a;    // {x: 1}

( { a: X, a: Y, a: [ Z ] } = { a: [ 1 ] } );

X.push( 2 );
Y[0] = 10;

X;	// [10,2]
Y;	// [10,2]
Z;	// 1
```

you can chain destructuring assignment expressions together
```
var o = { a: 1, b: 2, c: 3 },
        p = [4, 5, 6],
	a, b, c, x, y, z;
( {a} = {b, c} = o );
[x, y] = [z] = p;

console.log( a, b, c );  // 1, 2, 3
console.log( x, y, z );  // 4, 5, 4
```