# Go document 1

Date:2016-03-09

Tag:golang doc

## Go tour 1
* By convention ,the package name is the same as the last element of the import path.For instance ,the `"math/rand"` package comprises files that begin with the statement `package rand`

* A `return` statement without arguments returns the named return values.This is known as a "naked" return.`Naked` return statemetns should be used `only in short functions` ,as with the example shown here.They can harm readability in longer functions.
* Outside a function ,every statement begins with a keyword(`var`,`func` and so on) and so the `:=` construct is not avaiable
* The `int`,`uint` and `uintptr` types are usually 32 bits wide on 32-bit systems and 64bits wide on 64-bit systems.
* Variables declared without an explicit initial value are given their zero value.The zero value is:
  * 0 for numeric types,
  * false the boolean type,and
  * ""(the empty string) for strings.

* Unlike in c ,in Go assignment between items of different type requires an explicit conversion.
* Constants
  * constants are decleared like variables but with the `const` keyword
  * constants can be character,string,boolean,or numeric values.
  * constants cannot be declared using the `:=` syntax.
  * Numeric constants are high-precision values.An untyped numeric constant takes the type needed bye its context. [see this example](https://tour.golang.org/basics/16)
* Variables declared inside an `if` short statement are also available inside any of the `else` blocks
* in the `Switch` a case body breaks automatically,unless it ends with a `fallthrough` statement
* Switch cases evaluate cases from top to bottom ,stopping when a case succeeds.
* The defered call's arguments are evaluated immediately,but the function call is not executed until the surrounding function returns
  * A defered function's arguments are evaluated when the defer statement is evaluated
  * Defered function calls are executed in Last In First Out order after the surrounding function returns.
  * Defered functions may read and assign to the returning function's named return values.
  * The convention in the GO libraries is that even when a package uses panic internally,its external API still presents explicit error return values.

* maps must be created with `make` before use;the nil map is empty and cannot be assigned to.
* You can only declare a method with a receiver whose type is defined in the same package as the method.You cannot declare a method with a receiver whose type is defined in another package(which includes the build-in types such as `int`)
* Methods with pointer receivers can modify the value to which the receiver points.Since methods often need to modify their receiver,pointer receivers are more common than value receivers.
* There are two reasons to use a pointer receiver:
  * the method can modify the value that its receiver points to
  * avoid copying the value on method call.This can be more efficient if the receiver is a large struct. 
 
 `In general,all methods on a given type shuold either value of pointer receivers,but not a mixture of both.
* if the concrete value inside the interface itself is nil,the method will be called with a nil receiver.In some languages this would trigger a null pointer exception,but in GO it is common to wr4ite meothds that gracefully handle being called with a nil receiver.`Not that an interface value that holds a nil concrete value is itself non-nil` `
  
* A nil interface vaule holds neighter value nor concrete type.Calling a method on a nil interface is a run-time error because there is no type inside the interface tuple to indicate which concrete method to call
* A `type assertion` provide access to an interface value's underlying concrete value:`t:=i.(T)`
   
 ### buildin
* `iota` is a predeclared indentifier representing the untyped integer ordinal number of the current const specification in a (usually parenthesized) const declaration.It is zero-indexed
* `nil` is a predeclared identifier representing the zero value of a pointer ,channel,func ,interface,map,or slice type.
* The `Delete` built-in function deletes the element with the specified key(m[key]) from the map.If m is nil or there is no such element,delete is a no-op
* The `append` function appends the elemetns x to the end of the slice s,and grows the slice if a greater capacity is needed

### go slices useage and internals

Go's arrays are values.An array variable denotes the entire array;`it is NOT a pointer to the first array element`.This means that when you assign or pass around an array value you will make a copy of its contens.(To avoid the copy you could pass a pointer to the array,but then that's a pointer to an array ,not an array) .One way to think about arrays is as a sort of struct but with indexed rather that named fields:a fixed-size composite value.
