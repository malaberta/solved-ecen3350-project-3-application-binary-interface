Download Link: https://assignmentchef.com/product/solved-ecen3350-project-3-application-binary-interface
<br>
In this project, you will use the Nios II application binary interface to make function calls in assembly and C.

Objectives:

<ul>

 <li>Learn the importance of calling conventions / ABIs in assembly</li>

 <li>Use callee and caller saved registers and the stack</li>

 <li>Understand buffer overflows and their consequences</li>

</ul>

<h1>Part 1. Application Binary Interface</h1>

In this part, you’ll write <em>three </em>ABI-compliant functions in Nios II assembly.

<h2>Part 1.1 Calling Convention</h2>

In Nios II assembly, write an ABI-compliant function that takes 2 arguments, and returns the sum of them. You should use signed arithmatic, and your function should have the type signature: int sum_two(int a, int b)

(Note: this is just the function prototype; you’ll write your function entirely in assembly).

<h2>Part 1.2 Saving Registers</h2>

We’ve defined a new mathmatical operation, ◦, and written an ABI-complaint function that implements it. The operation is binary: it takes two inputs, and produces one output. We won’t tell you what the operation is (it’s a mystery!), but we can say that ◦ is a commutative and associative operation. This means that <em>a</em>◦<em>b </em>= <em>b</em>◦<em>a</em>, and that (<em>a</em>◦<em>b</em>)◦<em>c </em>= <em>a</em>◦(<em>b</em>◦<em>c</em>). Our function is named op_two, and takes two 32-bit inputs <em>a </em>and <em>b</em>, and returns a single 32-bit value <em>a</em>◦<em>b</em>.

Your task is to implement an ABI-compliant op_three function in Nios II assembly, that inputs <em>three </em>32-bit inputs, <em>a</em>, <em>b</em>, and <em>c</em>, and returns <em>a</em>◦<em>b</em>◦<em>c</em>.

The type signature of the given function is int op_two(int a, int b), and your function’s type signature should be int op_three(int a, int b, int c).

Note that you don’t know what operation ◦ is, so you’ll have to rely on calling op_two to perform that for you! Your function should work for any operation we implement in op_two. At the very least, you should test it with your above sum_two function as the op_two function, but we encourage you to try it with other commutative/associative functions, such as multiplication, minimum integer, bitwise xor, etc.

Make sure you don’t leave a <strong>op_two </strong>function in your submission! We’ll define one, and use it to test your program.

<h2>Part 1.3 Recursvie functions</h2>

In Nios II assembly, write an ABI-compliant <em>recursive </em>function that calculates the Fibonacci sequence for a given input index number. The Fibonacci sequence is defined as the sum of the previous two numbers in the sequence, with the first two numbers being 0 and 1 (i.e. fibonacci(n) = fibonacci(n-1) + fibonacci(n-2), with fibonacci(0) = 0 and fibonacci(1) = 1).

Thus, for example, if given index 0, your function should return 0. Input index 1 should return 1, and input index 7 should return 13.

Your function’s type signature should look like int fibonacci(int n).

What to submit           A single file, part1.s, that includes all three functions you wrote in Part 1.1, Part 1.2, and Part 1.3 combined. Your file should <em>not </em>define a _start label (and it also should not define an op_two function).

Your file could look something like this:

.text .global sum_two sum_two:

# implement Part 1.1 here

.global op_three op_three:

# implement Part 1.2 here

.global fibonacci fibonacci:

# implement Part 1.3 here

You may want to test your program (we recommend you do!!). You can do this by adding part1.s to your project, and defining your _start function (along with other test functions, e.g. op_two) in another file (e.g. main.s) that is also added to your project. Then, only turn in the part1.s file.

<h1>Part 2. Buffer Overflows</h1>

In this section, you’ll provide different data to two programs we’ve written to determine your grade.

<h2>Part 2.1</h2>

In the first part, we’ve written a simple program in C that reads your name over the JTAG UART port, and then assigns a grade, writing the result back over the UART terminal.

Download the C file at <a href="https://ecen3350.rocks/static/proj3-part2-1.c">https://ecen3350.rocks/static/proj3-part2-1.c</a>

An equivalent assembly file can be found at <a href="https://ecen3350.rocks/static/proj3-part2-1.s">https://ecen3350.rocks/static/proj3-part2-1. </a><a href="https://ecen3350.rocks/static/proj3-part2-1.s">s</a> and can be loaded into the CPUlator: <a href="https://cpulator.01xz.net/?sys=nios-de10-lite&amp;maxmem=67108864">https://cpulator.01xz.net/?sys=nios-de10-lite&amp; </a><a href="https://cpulator.01xz.net/?sys=nios-de10-lite&amp;maxmem=67108864">maxmem=67108864</a><a href="https://cpulator.01xz.net/?sys=nios-de10-lite&amp;maxmem=67108864">.</a>

You’ll note that the code appears to assign an F- for everyone. Your job is to provide a specific name that will make your grade an A+ instead. It doesn’t matter what’s printed in the name field, but it should print Your grade is: A+. You’ll provide your input name in a text file for this part (part2.txt), on its own line, following the submission template below.

Please note: we will grade your assignment with compiler optimizations turned <em>off </em>(in your project’s Program Settings, “Additional compiler flags” should not have -O1 in it).

<h2>Part 2.2</h2>

In the second part, we’ve learned better than to store grades on the stack.

Instead, we have a hardcoded assembly program that assigns the grades, and the name is provided with its length as a global variable STUDENT_NAME.

Download the assembly file at <a href="https://ecen3350.rocks/static/proj3-part2-2.s">https://ecen3350.rocks/static/proj3-part2-2.s</a>

Your task is to change the values of STUDENT_NAME and STUDENT_NAME_LEN to improve your grade. Hint: there is a print_good_grade function in the program, but nothing calls it. How can you make sure that code gets used?

You may <em>NOT </em>change the value of any other data or code in the program, besides STUDENT_NAME and STUDENT_NAME_LEN.

You may use the CPUlator or your DE-10 for this part.

What to submit           A single plaintext file part2.txt that has your answers to Part 2.1 and Part 2.2 with the following template:

Part 2.1:

&lt;YOUR NAME HERE&gt;

Part 2.2:

STUDENT_NAME_LEN:       .word       &lt;YOUR VALUE HERE&gt;

STUDENT_NAME:                  .ascii “&lt;YOUR VALUE HERE&gt;”