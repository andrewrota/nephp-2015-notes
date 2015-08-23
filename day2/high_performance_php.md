**High Performance PHP** by [Anthony Ferrara](https://twitter.com/ircmaxell)

Scale !== Speed

AOT Compiler: ahead of time compiler

Tracking JIT Compiler: generates machine call each time you call a function

Local JIT Compiler: combination of JIT and AOT.  Generates machine code when you make a function call.  HHVM.

But How does it do it? AOT/Local JIT: Code --> parser --> IR --> Operations --> IR --> code generator --> target code

    function blah($num) {
        if($num) {
            return $num + 1;
        }
    }
    
    // Tokenize (array of tokens)
    
    T_FUNCTION
    T_STRING
    T_VARIABLE
    T_IF
    T_VARIABLE
    T_RETURN
    T_VARIABLE
    T_LNUMBER
    T_RETURN
    T_LNUMBER
    
    // convert to an AST
    
    Return
        Add
            Variable
            Number 1
            

    // AST maps 100% to the source code

PHP Parser can build ASTs

Graph

Static Single Assignment (SSA) - when it comes to an analysis, changing variables makes things difficult.  So with SSA we say we're only ever going to write to a variable once.

**Four main optimizations**

Peephole Optimziation: traverses the graph and looks at every single operation by itself and determines if it can do something with it.  x = 1 + 2 --> x = 3.  Easy to build.  Small amount sof performance gains.  Limit of what PHP has.

Local Optimizations: Look at just the block of code guarenteed to run together, and sees whether that can be collapsed.  More time to execute, more difficult, but more gains.  (HHVM has this).

Global Optimizations: No JIT compiler goes this.  Function inlining.  Hard to build, but high performance gains.  Really slow.  GCC does this.

Loop Optimizations: Do things like loop invarient code motion.  Say you have assignment inside a loop.  The compiler will pull it outside the loop if it doesn't depend on the loop.

**Make code faster**

- Avoid dynamic types
- Avoid conditional declarations
- Avoid `eval` at all costs

"The more dynamic you write your code...the slower it's going to run, the harder it's going to be to analyze, and the bigger problems you're going to have."