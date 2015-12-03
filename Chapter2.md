# 第二章 程序结构

> And my heart glows bright red under my filmy, translucent skin and they have to administer 10cc of JavaScript to get me to come back. (I respond well to toxins in the blood.) Man, that stuff will kick the peaches right out your gills!  —— _why, Why's (Poignant) Guide to Ruby

在第二章，我们将开始一些能够被称为“编程”的事情了。为了写出更有意义的程序，我们也将会继续学习JavaScript知识，当然并不局限于之前提到的名词和语句片段。

## 表达式和语句

在第一章，我们创建了一些值，然后把操作符应用到这些值上，最后获得了一些新值。对于JavaScript程序而言，像第一章那样产生值只是其很基础、很小的一部分。

A fragment of code that produces a value is called an expression. Every value that is  en literally (such as 22 or "psychoanalysis") is an expression. An expression between parentheses is also an expression, as is a binary operator applied to two expressions or a unary operator applied to one.

产生值的代码段被称作表达式。而一望而知的值（字面值常量）（比如：22、"psychoanalysis"）也是表达式。被圆括号括住的表达式@@，同样也是表达式。

This shows part of the beauty of a language-based interface. Expressions can nest in a way very similar to the way subsentences in human languages are nested—a subsentence can contain its own subsentences, and so on. This allows us to combine expressions to express arbitrarily complex computations.

上面对于表达式的定义展现了@@。表达式

If an expression corresponds to a sentence fragment, a JavaScript statement corresponds to a full sentence in a human language. A program is simply a list of statements.

如果把JavaScript的表达式比作人类的句子片段，那么JavaScript的语句就相当于完整的语句。程序仅仅就是语句的列表而已。如下例所示，就是一个程序：

```js
1;
!false;
```
It is a useless program, though. An expression can be content to just produce a value, which can then be used by the enclosing expression. A statement stands on its own and amounts to something only if it affects the world. It could display something on the screen—that counts as changing the world—or it could change the internal state of the machine in a way that will affect the statements that come after it. These changes are called side effects. The statements in the previous example just produce the values 1 and true and then immediately throw them away. This leaves no impression on the world at all. When executing the program, nothing observable happens.

但是这个程序没有什么卵用。表达式可以产生一个值，用作封闭表达式。
 
有时候，JavaScript允许你在语句的结尾省略分号。而在其他情况下，语句的结尾必须加上分号，否则下一行代码将会成为其一部分。而分号什么时候可以被安全省略的规则有点复杂且容易出错。在本书中，每一个语句都会以分号结尾。至少在你深入了解省略分号的各种坑之前，我建议你在你的程序中也这样做。

## Variables

程序怎样保持内部的状态？它怎样存储信息呢？结合之前所学，我们已经了解了怎样从旧值中产生新值。而这样做以后，旧值不会被改变，产生新值会被立即使用或者将重新消逝。那该怎么办呢？JavaScript提供了`变量`（variable）来捕获和保留住值。

```js
var caught = 5 * 5;
```
And that gives us our second kind of statement. The special word (keyword) var indicates that this sentence is going to define a variable. It is followed by the name of the variable and, if we want to immediately give it a value, by an = operator and an expression.

上面的代码为我们展现了语句的第二种形式。这个语句中单词(关键字)`var`被用来定义变量。`var`后面跟着的`caught`是这个变量的名字，如果我们想在创建变量的时候立即给它一个值，就可以使用`=`赋值操作符和表达式来达到目的。

The previous statement creates a variable called caught and uses it to grab hold of the number that is produced by multiplying 5 by 5.

简而言之，

After a variable has been defined, its name can be used as an expression. The value of such an expression is the value the variable currently holds. Here’s an example:

在变量被定义以后，

```js
var ten = 10;
console.log(ten * ten);
// → 100

```

Variable names can be any word that isn’t a reserved word (such as var). They may not include spaces. Digits can also be part of variable names—catch22 is a valid name, for example—but the name must not start with a digit. A variable name cannot include punctuation, except for the characters $ and _.

变量名字可以是除了保留字（比如`var`）以外的任何单词。但是不能含有空格。数字也可以是变量名字的一部分，比如`catch22`，就是一个有效的变量名。但是变量名不能以数字开头。变量的名字不能包含除了`$`和`_`以外的标点符号。

When a variable points at a value, that does not mean it is tied to that value forever. The = operator can be used at any time on existing variables to disconnect them from their current value and have them point to a new one.

当一个变量指向一个值的时候，并不意味着它就永远联系在一起。通过=可以在任何时候让已经赋值变量切断与旧值的联系，同时将其指向新值。

```js
var mood = "light";
console.log(mood);
// → light
mood = "dark";
console.log(mood);
// → dark
```

You should imagine variables as tentacles, rather than boxes. They do not contain values; they grasp them—two variables can refer to the same value. A program can access only the values that it still has a hold on. When you need to remember something, you grow a tentacle to hold on to it or you reattach one of your existing tentacles to it.

你应该想象把变量看做触手，而不是盒子。它们不会容纳任何值，而只会抓住值，也就是说，两个变量可以同时指向同一个值。程序只能够使用它保存的值。当你需要存储信息的时候，你重新长出一个触手去抓住它或者用你已经存在的触手去接纳它。

Let’s look at an example. To remember the number of dollars that Luigi still owes you, you create a variable. And then when he pays back $35, you give this variable a new value.

我们来看一个例子。为了记住Luigi借给你钱的数目，你创建了一个变量。当你偿还$35的时候，你赋予了这个变量的一个新值。

```js
var luigisDebt = 140;
luigisDebt = luigisDebt - 35;
console.log(luigisDebt);
// → 105
```

When you define a variable without giving it a value, the tentacle has nothing to grasp, so it ends in thin air. If you ask for the value of an empty variable, you’ll get the value undefined.

当你只定义变量，而没有给它赋值的时候，这个新生长出来的触手不会抓住任何东西，只能无奈的在空中飘扬。如果你想请求这个空值变量，你会得到的值为`undefined`。

A single var statement may define multiple variables. The definitions must be separated by commas.

通过一个var语句可以定义多个变量。而这些定义必须用逗号隔开。

```js
var one = 1, two = 2;
console.log(one + two);
// → 3
```
## 关键字和保留字

Words with a special meaning, such as var, are keywords, and they may not be used as variable names. There are also a number of words that are “reserved for use” in future versions of JavaScript. These are also officially not allowed to be used as variable names, though some JavaScript environments do allow them. The full list of keywords and reserved words is rather long.

像`var`这类具有特殊意义的单词被称为“关键字”，关键字不能被用作的变量的名字。有一些单词是为了将来JavaScript版本更替而保留的，这些单词被称为“保留字”。同关键字一样，官方不允许保留字被用作变量的名字，虽然有些JavaScript环境确实可以使用它们。关键字和保留字的列表有些小长，如下所示：

```js
break case catch class const continue debugger
default delete do else enum export extends false
finally for function if implements import in
instanceof interface let new null package private
protected public return static super switch this
throw true try typeof var void while with yield
```

不需要去记上面这些单词。只要记住如果变量定义出现错误时，可能与误用关键字和保留字有关，就可以了。

## The environment

The collection of variables and their values that exist at a given time is called the environment. When a program starts up, this environment is not empty. It always contains variables that are part of the language standard, and most of the time, it has variables that provide ways to interact with the surrounding system. For example, in a browser, there are variables and functions to inspect and influence the currently loaded website and to read mouse and keyboard input.

在某一给定的时间内，变量和变量值的集合被称为环境。当程序开始运行时，环境不是空的。环境总是包含着一些语言标准内置的变量。在很多时候，这些变量提供了与环境交互的方法。例如，在浏览器中，有一些变量和函数可以监视和影响已加载的页面，还能读取鼠标和键盘输入的信息。

## 函数

A lot of the values provided in the default environment have the type function. A function is a piece of program wrapped in a value. Such values can be applied in order to run the wrapped program. For example, in a browser environment, the variable alert holds a function that shows a little dialog box with a message. It is used like this:

例如，在浏览器环境当中，alert可以用系统对话框向用户显示消息。

![revolunet logo]( "revolunet logo")

```js
alert("Good morning!");
```

Executing a function is called invoking, calling, or applying it. You can call a function by putting parentheses after an expression that produces a function value. Usually you’ll directly use the name of the variable that holds the function. The values between the parentheses are given to the program inside the function. In the example, the alert function uses the string that we give it as the text to show in the dialog box. Values given to functions are called arguments. The alert function needs only one of them, but other functions might need a different number or different types of arguments.

调用、

## console.log方法

The alert function can be useful as an output device when experimenting, but clicking away all those little windows will get on your nerves. In past examples, we’ve used console.log to output values. Most JavaScript systems (including all modern web browsers and Node.js) provide a console.log function that writes out its arguments to some text output device. In browsers, the output lands in the JavaScript console. This part of the browser interface is hidden by default, but most browsers open it when you press F12 or, on Mac, when you press Command-Option-I. If that does not work, search through the menus for an item named “web console” or “developer tools”.
                                                                                                                                                                                  
alert方法

When running the examples, or your own code, on the pages of this book, console.log output will be shown after the example, instead of in the browser’s JavaScript console.



```js
var x = 30;
console.log("the value of x is", x);
// → the value of x is 30
```

Though variable names cannot contain period characters, console.log clearly has one. This is because console.log isn’t a simple variable. It is actually an expression that retrieves the log property from the value held by the console variable. We will find out exactly what this means in Chapter 4.

## 返回值

Showing a dialog box or writing text to the screen is a side effect. A lot of functions are useful because of the side effects they produce. Functions may also produce values, and in that case, they don’t need to have a side effect to be useful. For example, the function Math.max takes any number of number values and gives back the greatest.

显示一个对话框或者在屏幕上写出一行文字是副作用。大量的函数之所以有用，是因为它们产生的副作用。函数也可以产生值。当它产生值的时候，就不需要副作用的效果了。例如，Math.max函数返回一组数字中最大的一个。

```js
console.log(Math.max(2, 4));
// → 4
```

When a function produces a value, it is said to return that value. Anything that produces a value is an expression in JavaScript, which means function calls can be used within larger expressions. Here a call to Math.min, which is the opposite of Math.max, is used as an input to the plus operator:

当函数产生一个值，也就是说它返回了该值。因为在JavaScript中，任何可以产生值的东西都被成为表达式，所以函数可以被用在表达式中求值，进而组成更广义的表达式。如下例所示，其中Math.min函数的作用与Math.max函数相反，它返回一组数中最小的哪一个。

```js
console.log(Math.min(2, 4) + 100);
// → 102
```

The next chapter explains how to write your own functions.

下一章将会解释如何编写属于你自己的函数。

## 提示与确认

在浏览器环境中，除了alert()之外，还可以用prompt()与confirm()调用系统对话框向用户显示消息。使用
confirm()来询问用户是或否(OK/Cancel)的问题。当用户点击OK按钮，confirm()会返回布尔值`true`；当用户点击Cancel按钮时，confirm()将会返回布尔值`false`。

```js
confirm("Shall we, then?");
```

prompt()函数被用来询问“开放”的问题。第一个参数是要询问的问题，第二个参数是默认问题。在弹出的系统对话框中，可以输入文字。而这些文字会被prompt()函数以字符串的形式返回。

```js
prompt("Tell me everything you know.", "...");
```

在现今的Web编程环境下，prompt()与confirm()很少被使用，因为系统对话框的外观不能被修改，但是我们在做一些小玩意或者实验的时候，还是很有用的。

## 流控制

在你的程序中，通常会有很多语句，而这些语句会从上到下一次顺序执行。如下面的程序所示，有两个语句。第一个语句向用户请求一个数字。第二个语句显示了用户输入的数字的平方。

```js
var theNumber = Number(prompt("Pick a number", ""));
alert("Your number is the square root of " +
      theNumber * theNumber);
```

The function Number converts a value to a number. We need that conversion because the result of prompt is a string value, and we want a number. There are similar functions called String and Boolean that convert values to those types.

Number()函数将值转换为数值。之所以需要这层转换，是因为prompt方法返回的值是字符串，而我们计算的是数值的平方。布尔值和字符串都有相应的函数来把值转换为对应的类型。

Here is the rather trivial schematic representation of straight control flow:

用一个简单的示意图来表示顺序语句

## 条件执行

Executing statements in straight-line order isn’t the only option we have. An alternative is conditional execution, where we choose between two different routes based on a Boolean value, like this:

语句按照直线执行（顺序执行）不是我们唯一的选择。还有一种条件执行，可以根据布尔值，来执行不同的路径。如下图所示：

Conditional execution is written with the if keyword in JavaScript. In the simple case, we just want some code to be executed if, and only if, a certain condition holds. For example, in the previous program, we might want to show the square of the input only if the input is actually a number.

在JavaScript中，条件语句是由关键字if编写的。在简单的情况下，有且只有很简单的条件，一个if语句需要执行。如下面的例子所示，如果我们输入的不是数字，那么将不会有任何提示（alert）任何信息。

```js
var theNumber = Number(prompt("Pick a number", ""));
if (!isNaN(theNumber))
  alert("Your number is the square root of " +
        theNumber * theNumber);
```


The keyword if executes or skips a statement depending on the value of a Boolean expression. The deciding expression is written after the keyword, between parentheses, followed by the statement to execute.

if语句括号内的表达式的布尔值，决定了是否执行if语句。

The isNaN function is a standard JavaScript function that returns true only if the argument it is given is NaN. The Number function happens to return NaN when you give it a string that doesn’t represent a valid number. Thus, the condition translates to “unless theNumber is not-a-number, do this”.

JavaScript语言规范提供了isNaN()函数，这个函数可以帮助我们确定给定的参数是否“不是数值”。对于Number()函数来说，如果给定的参数是字符串且该字符串表示的不是数字，它就会返回NaN。所以，上面的代码就可以翻译为“除非theNumber不是数字，否则就执行”

You often won’t just have code that executes when a condition holds true, but also code that handles the other case. This alternate path is represented by the second arrow in the diagram. The else keyword can be used, together with if, to create two separate, alternative execution paths.

关键字else可以与if混用，用来表示可选择执行。

```js
var theNumber = Number(prompt("Pick a number", ""));
if (!isNaN(theNumber))
  alert("Your number is the square root of " +
        theNumber * theNumber);
else
  alert("Hey. Why didn't you give me a number?");
```

If we have more than two paths to choose from, multiple if/else pairs can be “chained” together. Here’s an example:

如果有多个路径选择，那么多个if/else可以成链式组合。如下面的例子所示：

```js
var num = Number(prompt("Pick a number", "0"));

if (num < 10)
  alert("Small");
else if (num < 100)
  alert("Medium");
else
  alert("Large");
```

The program will first check whether num is less than 10. If it is, it chooses that branch, shows "Small", and is done. If it isn’t, it takes the else branch, which itself contains a second if. If the second condition (< 100) holds, that means the number is between 10 and 100, and "Medium" is shown. If it doesn’t, the second, and last, else branch is chosen.

这个程序首先会检查num是不是小于10。如果小于10，就会执行提示“Small”的语句。如果小于100，就会执行提示“Medium”的语句。如果前两个条件都不满足，那就会执行提示“Large”的语句。

The flow chart for this program looks something like this:

程序的执行逻辑大概如下图所示：

## while and do loops

Consider a program that prints all even numbers from 0 to 12. One way to write this is as follows:

思考一下，如何使得让一个程序输出0到12之间的偶数。其中一个方法如下所示：

```js
console.log(0);
console.log(2);
console.log(4);
console.log(6);
console.log(8);
console.log(10);
console.log(12);
```

That works, but the idea of writing a program is to make something less work, not more. If we needed all even numbers less than 1,000, the previous would be unworkable. What we need is a way to repeat some code. This form of control flow is called a loop:

确实是一种方法，但是不够优雅的同时还没办法拓展。如果我们求0到1000之间的偶数，上面的这种方法显然就能使用了。我们需要一个可以重复执行代码的方法。

下面图片展示的控制流称为：循环。

Looping control flow allows us to go back to some point in the program where we were before and repeat it with our current program state. If we combine this with a variable that counts, we can do something like this:

循环控制流允许我们在保存当前程序执行的状态的情况下，返回程序之前执行的某个点来重复执行某个片段。如果我们用一个变量来记录循环的次数，那我们就可以优雅的解决本节开头提到的那个问题了。

```js
var number = 0;
while (number <= 12) {
  console.log(number);
  number = number + 2;
}
// → 0
// → 2
//   … etcetera
```

A statement starting with the keyword while creates a loop. The word while is followed by an expression in parentheses and then a statement, much like if. The loop executes that statement as long as the expression produces a value that is true when converted to Boolean type.

关键字while开头的语句创建了循环。其后面的语句和if语句类似。当括号内的表达式产生的值，可以被转换为`true`，那么{}内的语句就可以被执行。

In this loop, we want to both print the current number and add two to our variable. Whenever we need to execute multiple statements inside a loop, we wrap them in curly braces ({ and }). Braces do for statements what parentheses do for expressions: they group them together, making them count as a single statement. A sequence of statements wrapped in braces is called a block.

在上面的例子中，我们在输出变量number当前值的同时，也为其增加了2。在任何时候，如果我们想在循环内执行多个语句，都需要用大括号将他们括起来。大括号对于多个语句的作用就和括号对于其内的表达式的作用一样，都是将它们包含的东西聚合起来，让他们以为自己就是一个单一的语句。被大括号括起来的一列语句被称为“块”。

Many JavaScript programmers wrap every single loop or if body in braces. They do this both for the sake of consistency and to avoid having to add or remove braces when changing the number of statements in the body later. In this book, I will write most single-statement bodies without braces, since I value brevity. You are free to go with whichever style you prefer.

许多JavaScript程序员为了程序风格一致性和便于修改，不论while/if语句内包含多少条语句，都会用大括号将这些语句括起来。因为我崇尚简洁，所以在这本书中，如果while/if语句中只包含一条语句，那么我就省略掉大括号。当然，你可以随意选择自己的代码风格。


The variable number demonstrates the way a variable can track the progress of a program. Every time the loop repeats, number is incremented by 2. Then, at the beginning of every repetition, it is compared with the number 12 to decide whether the program has done all the work it intended to do.

变量number展示了，如果通过变量来控制程序的执行。每次循环的时候，number都会增加2。然而在每次循环之前，都会对比number与12的大小，以此来决定是否继续执行循环。

As an example that actually does something useful, we can now write a program that calculates and shows the value of 2^10 (2 to the 10th power). We use two variables: one to keep track of our result and one to count how often we have multiplied this result by 2. The loop tests whether the second variable has reached 10 yet and then updates both variables.

通过上面例子展示的方法，现在我们可以计算2的10次方了。我们用两个变量，一个来记录我们的结果，另一个来记录乘2的次数。这个循环判断第二个变量是否10，进而通过循环来改变两个变量的值。

```js
var result = 1;
var counter = 0;
while (counter < 10) {
  result = result * 2;
  counter = counter + 1;
}
console.log(result);
// → 1024
```

The counter could also start at 1 and check for <= 10, but, for reasons that will become apparent in Chapter 4, it is a good idea to get used to counting from 0.

变量counter也可以从1开始，然后检查是否小于等于10来达到同样的目的。但是，因为通过第四章的学习才会明白从1开始的原因，所以现在最好习惯从0开始。

The do loop is a control structure similar to the while loop. It differs only on one point: a do loop always executes its body at least once, and it starts testing whether it should stop only after that first execution. To reflect this, the test appears after the body of the loop:

do循环和while循环非常相似，唯一不同点在于：do循环首先执行其循环体，再根据判断条件来决定是否进行下一次循环。也就是说，do循环至少会执行其循环体一次。如下例所示：

```js
do {
  var yourName = prompt("Who are you?");
} while (!yourName);
console.log(yourName);
```

This program will force you to enter a name. It will ask again and again until it gets something that is not an empty string. Applying the ! operator will convert a value to Boolean type before negating it, and all strings except "" convert to true. This means the loop continues going round until you provide a name that is not the empty string.

这个程序会一次又一次的强迫你输入一个名字，直到得到一个不是的空字符串的东东。因为操作符!会将值的布尔值取反，所以除了空字符串，其余字符串都会被转换成为true。也就是说，循环会一直持续到你提供一个非空字符串。

## 代码缩进

你可能注意到我在编写代码的时候，语句之前会添加一些空格。对于JavaScript来说，这不是必须的。就算没有这些空格，计算机也会将代码执行的很顺利。事实上，语句的换行也是可选择的。如果你愿意，你可以写一行很长的代码。但缩进可以让代码结构清晰明了。在复杂的程序中，代码块与代码块之间相互嵌套，如果没有良好的缩进，那么代码就会变得难以阅读。如果代码可以有合适的缩进，那么整个程序看起来就像一块又一块的代码堆砌起来的。我喜欢在每个代码块开始之前用两个空格与之前的代码块岔开。但是众口难调，有些人喜欢用四个空格，也有些人喜欢使用制表符（Tab）。

## for 循环

Many loops follow the pattern seen in the previous while examples. First, a “counter” variable is created to track the progress of the loop. Then comes a while loop, whose test expression usually checks whether the counter has reached some boundary yet. At the end of the loop body, the counter is updated to track progress.

许多循环都具有相同的模式结构。首先，一个“计数器”去跟踪记录循环的进程。然后，紧跟着循环边界的判定

Because this pattern is so common, JavaScript and similar languages provide a slightly shorter and more comprehensive form, the for loop.

因为这种循环形式很普遍，所以包括JavaScript在内的很多编程语言都提供了一种更加简洁紧凑的循环语法，for循环。

```js
for (var number = 0; number <= 12; number = number + 2)
  console.log(number);
// → 0
// → 2
//   … etcetera
```

The parentheses after a for keyword must contain two semicolons. The part before the first semicolon initializes the loop, usually by defining a variable. The second part is the expression that checks whether the loop must continue. The final part updates the state of the loop after every iteration. In most cases, this is shorter and clearer than a while construct.

关键字for后面的括号内必须包含两个分号。第一个分号之前的部分会初始化循环，通常是定义一个变量。两个分号之间的部分通常是检查循环

Here is the code that computes 210, using for instead of while:

```js
var result = 1;
for (var counter = 0; counter < 10; counter = counter + 1)
  result = result * 2;
console.log(result);
// → 1024
```

Note that even though no block is opened with a {, the statement in the loop is still indented two spaces to make it clear that it “belongs” to the line before it.

## Breaking Out of a Loop

Having the loop’s condition produce false is not the only way a loop can finish. There is a special statement called break that has the effect of immediately jumping out of the enclosing loop.

This program illustrates the break statement. It finds the first number that is both greater than or equal to 20 and divisible by 7.

```js
for (var current = 20; ; current++) {
  if (current % 7 == 0)
    break;
}
console.log(current);
// → 21
```

Using the remainder (%) operator is an easy way to test whether a number is divisible by another number. If it is, the remainder of their division is zero.

The for construct in the example does not have a part that checks for the end of the loop. This means that the loop will never stop unless the break statement inside is executed.

If you were to leave out that break statement or accidentally write a condition that always produces true, your program would get stuck in an infinite loop. A program stuck in an infinite loop will never finish running, which is usually a bad thing.

If you create an infinite loop in one of the examples on these pages, you’ll usually be asked whether you want to stop the script after a few seconds. If that fails, you will have to close the tab that you’re working in, or on some browsers close your whole browser, in order to recover.

The continue keyword is similar to break, in that it influences the progress of a loop. When continue is encountered in a loop body, control jumps out of the body and continues with the loop’s next iteration.

## Updating variables succinctly

Especially when looping, a program often needs to “update” a variable to hold a value based on that variable’s previous value.

```js
counter = counter + 1;
```

JavaScript provides a shortcut for this:

```js
counter += 1;
```

Similar shortcuts work for many other operators, such as result *= 2 to double result or counter -= 1 to count downward.

This allows us to shorten our counting example a little more.


http://eloquentjavascript.net/02_program_structure.html

http://eloquentjavascript.net/

