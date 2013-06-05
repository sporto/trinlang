Tri Language
============

A spec for a language that I would like to build.

- Simple
- Uses prototype chains
- Hackable
- Optional static typing
- Inspired by JavaScript, Ruby, IO and Go
- Implicit returns

Variables
---------

	a := 3
	
Object literals
----------

	    adder := {
	        x := 1
	        sum := ->(y) {
            	this.x + y
	        }
	    }
	
Functions are objects
--------------------

	a := ->(x) { x*x }
	
Objects use prototype chains
-------

	Shape := Object.clone()

    Shape.area := ->(a, b) {
        a * b
    }
    
    Square := Shape.clone()
	
Function shortcut in object literals
----------

		person := {
			greet() {
				...
			}
		}

	This creates a property ‘greet’ with an anonymous function assigned
	
Clone
-----------
Creates an new object with the prototype assigned to source object

	circle := Shape.clone()

New
-----------
Same as clone, but calls init on the clone object and passes the arguments to init
    
	Circle := {
		init(x) -> {
			this.radio = x
		}
	}
    
	circle := Circle.new(3)

Create object with properties
----------

	    Rectangle := Shape.clone({
	        x := 4
	        y := 5
	    })
		
Global methods
-------------

There are global methods that cannot be overriden, they all global have a $ prefix
e.g.

	Triangle := $clone(Shape, {})

But by default prototypes are already overloaded

	Triangle := Shape.clone({})
    

Function definitions
-------------------

All function are anonymous, they cannot be named

Function with no args
	->{}

Function with args
	->(arg){ ... }
	
Default parameters
----------------

	->(a:=1, b:=3){
		...
	}
	
Multiple return values
--------------------

	f := ->{
		1, 3
	}
	
	x, y := f()

Arrays
-------
	
	nums := [1,2,3]
	
First element is index 1 e.g. nums[1] == 1

Hashes, maps, tables, dictionaries
--------------------

Hashes and objects are the same thing, just like JavaScript

	hash := { a:=1, b:=3 }
	
	or
	
	hash := {
		a:=1
		b:=2
	}
	
	hash[a] #1
	
Ranges
-------

	range := (1..4)
	
	range.first # 1
	range.last # 4

Sets
----

	

Mixins
---------

This copies the properties into the object. Existing copies are overriden.

	$mixin(circle, {})

	or

    circle.mixin({b := 3})

Proto
------

The proto property points to the prototype of an object

	circle = Shape.clone()
	circle.proto == Shape # true

The proto of an object can be changed
-------

    circle.proto = Vehicle
	
Use proto to call the prototype object
--------------------------------------

    Shape := Object.clone()
    Shape.area := ->()
		100
    end
    
    circle := Shape.new()
    circle.area := ->()
        this.proto.area() 
    end
	
This
------

Points to the current object. Pretty much like JavaScript.

	machine := {
		start() {
			this.state = 'on'
		}
	}
	
Closures
----------

	make_adder := -> (x) {
		-> (y) {
			y * x
		}
	}
	

Variable shadowing
--------------

    ->() {
        x := 1
        
        internal := ->() {
            x := 2
        }
        
        internal()
        
        #x is 1
    }
    
Optional static typing
-------------------

    ->(a: string) {
		...
	}

Strongly typed
------------

    "a" + 3     
    //throws an error

Interfaces for static typing
--------------------

	Cat := {
		age,
		legs
	}

	->(cat: Cat)
		…	
	end

With throw if passed an object that doesn’t conform with the interface.
This is a duck type (only checks the properties)
    
Introspection - Type property
------

	circle.kind_of?(Shape) # true
	
Explicit return if needed

	-> (){
		if (a==1) ret 1
		3
	}
	
Variable interpolation
----------------------

	user := 'John'
	"Grettings #{user}"
	
Chains
-------

	car.start()
	..accelerate()
	..brake()
	
Modules
-------

	Modules always exports only one value
	
	foo := require('foo')

Comments
-------

	# One line comment
	
	#*
	Block comment
	*#