JS表达式 | 运算符和表达式
Atom

 Expression
 Statement
 Structure
 Program/Module

Member:
	a.b, a[b], foo `string` ,super.b,super['b'], new.target, new Foo()

New:
	new Foo

	Example:
		new a()()
		new new a()

Reference：
	Object, Key, delete, assign;

Call:函数调用
	foo(), super(), foo()['b'], foo().b, foo() `abc`
	Example 
		new a()['b'];

Left Handside & Right Handside
	Example:
		a.b = c, a + b = c (错误);
	
	 所有的expression如果不属于Left Handside 就一定Right Handside;
	 Left Handsie : 能不能放到等号的左边

Update:
	a++, a--, --a, ++a;

Unary:(单目运算)
	delete a.b, void foo(), typeof a, +a, -a, ~a, !a, await a;

Exponental:(右结合)
	**;

	Example：
	3**2**3 等效于 3**(2**3)

Multiplicative:
	*, /, %;

Additive:

- , -;

Shift:
	<<, >>, >>>;

Relationship:
	<, >, <=, >=, instanceof, in;

Equality:
	==, !=, ===, !==;

Bitwise:
	&, ^, |;

Logical:
 &&, ||;

Conditional:
	condition ? expression1 : expression2
语句｜运行时
声明
    前五个作用范围只认function body 没有前后关系，永远会被当作出现在函数第一行，var比较特殊，声明作用在函数头部，但是赋值是在之后发生的。
    function declaration 函数声明 function
    generator declaration (function *)
    asyncFucntion declaration ()
    AsyncGenerator declaration
    VariableStatement var变量声明被归类到语句里
    下面两个当声明之前去使用会报错，有作用域死区
    Class declaration
    Lexical declaration (const和let)
预处理
    在运行之前，js引擎会先预先处理
    会提前找到Var ，把变量声明到函数作用域级别
    所有声明都有预处理机制，const也会，区别是const会在声明之前抛错
    var a = 2;void function () {a = 1;return;var a}();console.log(a);//2
    var a = 2;void function () {a = 1;return;const a}();console.log(a);//抛错，但是把函数用try抱住，还是会打印出2
    上面两个执行结果都说明，函数中第一行a=1都不会改变外面的a因为不管是var 还是const ,都会被预处理，区别是const会在声明之前抛错
JS结构化 | JS函数调用
宏任务和微任务会影响代码执行的次序；
同一个微任务中有不同的函数调用影响代码的执行；

栈式（stack）环境；执行上下文；Excution Context Stack;
栈的顶层是正在执行的执行上下文：Running Excution Context;

Excution Context:
	code evalution state
	Function
	Script or Module
	Generator
	Realm : 保存所有的内置对象
	LexicalEnvironment：保存变量
	VariableEnvironment：var声明变量的环境

	LexicalEnvironment:保存的内容
		this, new.target, super, 变量
	
	VariableEnvironment:历史遗留的包袱，仅仅用于处理var声明；

