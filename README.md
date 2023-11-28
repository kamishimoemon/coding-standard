# Coding Standard

**Example**

```
<?php

declare(strict_types=1);

namespace Vendor\Package;

use Vendor\Package\{ClassA as A, ClassB, ClassC as C};
use Vendor\Package\SomeNamespace\ClassD as D;

use function Vendor\Package\{functionA, functionB, functionC};

use const Vendor\Package\{ConstantA, ConstantB, ConstantC};

class Foo extends Bar implements FooInterface
{
    public function sampleFunction (int $a, int $b = null): array
    {
        if ($a === $b) {
            bar();
        }
        elseif ($a > $b) {
            $foo->bar($arg1);
        }
        else {
            BazClass::bar($arg2, $arg3);
        }
    }

    public static final function bar ()
    {
        // method body
    }
}

enum Beep: int
{
    case Foo = 1;
    case Bar = 2;

    public function isOdd (): bool
    {
        return $this->value() % 2;
    }
}
```
## 1. Overview

- Files **MUST** use only ```<?php``` and ```<?=``` tags.
- Files **MUST** use only UTF-8 without BOM for PHP code.
- All PHP files **MUST** use the Unix LF (linefeed) line ending only.
- All PHP files **MUST** end with a non-blank line, terminated with a single LF.
- Files **SHOULD** either declare symbols (classes, functions, constants, etc.) or cause side-effects (e.g. generate output, change .ini settings, etc.) but **SHOULD NOT** do both.
- Namespaces and classes **MUST** follow the [PSR-4](https://www.php-fig.org/psr/psr-4/) autoloading standard.
- Class names **MUST** be declared in ```PascalCase```.
- Class constants **MUST** be declared in all upper case with underscore separators.
- Method names **MUST** be declared in ```camelCase```.

## 2. Files

### 2.1 Lines

There **MUST NOT** be trailing whitespace at the end of lines.
Blank lines **MAY** be added to improve readability and to indicate related blocks of code except where explicitly forbidden.
There **MUST NOT** be more than one statement per line.

### 2.2 Indentation

Code **MUST** use a tab for each indent level, and **MUST NOT** use spaces for indenting.

### 2.3 Keywords and Types

All PHP reserved [keywords](http://php.net/manual/en/reserved.keywords.php) and [types](http://php.net/manual/en/reserved.other-reserved-words.php) **MUST** be in lower case.
Any new types and keywords added to future PHP versions **MUST** be in lower case.
Short form of type keywords **MUST** be used i.e. ```bool``` instead of ```boolean```, ```int``` instead of ```integer``` etc.

### 2.4 Trailing commas

Numerous PHP constructs allow a sequence of values to be separated by a comma, and the final item may have an optional comma. Examples include array key/value pairs, function arguments, closure ```use``` statements, ```match()``` statement branches, etc.
If that list is contained on a single line, then the last item **MUST NOT** have a trailing comma.
If the list is split across multiple lines, then the last item **MUST** have a trailing comma.
The following are examples of correct comma placement:
```
function beep(string $a, string $b, string $c)
{
    // ...
}

function beep(
    string $a,
    string $b,
    string $c,
) {
    // ...
}

$arr = ['a' => 'A', 'b' => 'B', 'c' => 'C'];

$arr = [
    'a' => 'A',
    'b' => 'B',
    'c' => 'C',
];

$result = match ($a) {
    'foo' => 'Foo',
    'bar' => 'Bar',
    default => 'Baz',
};
```

### 2.5 PHP Tags

PHP code **MUST** use the long ```<?php ?>``` tags or the short-echo ```<?= ?>``` tags; it **MUST NOT** use the other tag variations.
The closing ```?>``` tag **MUST** be omitted from files containing only PHP.

### 2.6 Character Encoding

PHP code MUST use only UTF-8 without BOM.

### 2.7 Side Effects

A file **SHOULD** declare new symbols (classes, functions, constants, etc.) and cause no other side effects, or it **SHOULD** execute logic with side effects, but **SHOULD NOT** do both.
"Side effects" include but are not limited to: generating output, explicit use of ```require``` or ```include```, connecting to external services, modifying ini settings, emitting errors or exceptions, modifying global or static variables, reading from or writing to a file, and so on.

## 3. Declare Statements, Namespace, and Import Statements

The header of a PHP file **MAY** consist of a number of different blocks. If present, each of the blocks below **MUST** be separated by a single blank line, and **MUST NOT** contain a blank line. Each block **MUST** be in the order listed below, although blocks that are not relevant may be omitted.

- Opening ```<?php``` tag.
- File-level docblock.
- One or more declare statements.
- The namespace declaration of the file.
- One or more class-based ```use``` import statements.
- One or more function-based ```use``` import statements.
- One or more constant-based ```use``` import statements.
- The remainder of the code in the file.

When a file contains a mix of HTML and PHP, any of the above sections may still be used. If so, they **MUST** be present at the top of the file, even if the remainder of the code consists of a closing PHP tag and then a mixture of HTML and PHP.

When the opening ```<?php``` tag is on the first line of the file, it **MUST** be on its own line with no other statements unless it is a file containing markup outside of PHP opening and closing tags.

Import statements **MUST** be fully qualified.

Declare statements **MUST** be exactly ```declare(strict_types=1);```.

## 4. Classes, Properties, and Methods

The term "class" refers to all classes, interfaces, traits, and enums.

When instantiating a new class, parentheses MUST always be present even when there are no arguments passed to the constructor. For example:
```
new Foo();
```

If class contains no additional declarations (such as an exception that exists only to extend another exception with a new type), then the body of the class **SHOULD** be abbreviated as ```{}``` and placed on the same line as the previous symbol, separated by a space. For example:
```
class MyException extends \RuntimeException {}
```

### 4.1 Extends and Implements

The ```extends``` and ```implements``` keywords **MUST** be declared on the same line as the class name.

The opening brace for the class **MUST** go on its own line, and **MUST NOT** be preceded or followed by a blank line.

The closing brace for the class **MUST** go on its own line, immediately following the last line of the class body, and **MUST NOT** be preceded by a blank line.

Lists of ```implements``` and, in the case of interfaces, ```extends``` **MAY** be split across multiple lines, where each subsequent line is indented once. When doing so, the first item in the list **MUST** be on the next line, and there **MUST** be only one interface per line. For example:
```
class ClassName extends ParentClass implements
    \ArrayAccess,
    \Countable,
    \Serializable
{
    // constants, properties, methods
}
```

### 4.2 Using traits

The ```use``` keyword used inside the classes to implement traits **MUST** be declared on the next line after the opening brace.

Each individual trait that is imported into a class **MUST** be included one-per-line and each inclusion **MUST** have its own ```use``` import statement.

When the class has nothing after the ```use``` import statement, the class closing brace **MUST** be on the next line after the ```use``` import statement. Otherwise, it **MUST** have a blank line after the ```use``` import statement.

When using the ```insteadof``` and ```as``` operators they **MUST** be used as follows taking note of indentation, spacing, and new lines.
```
class Talker
{
    use A;
    use B {
        A::smallTalk insteadof B;
    }
    use C {
        B::bigTalk insteadof C;
        C::mediumTalk as FooBar;
    }
}
```

### 4.3 Properties and Constants

Visibility and type **MUST** be declared on all properties and constants.

### 4.4 Methods and Functions

Visibility **MUST** be declared on all methods.

Method and function names **MUST** be declared with one space after the method name. The opening brace **MUST** go on its own line, and the closing brace **MUST** go on the next line following the body. There **MUST NOT** be a space after the opening parenthesis, and there **MUST NOT** be a space before the closing parenthesis.

If a function or method contains no statements or comments (such as an empty no-op implementation or when using constructor property promotion), then the body **SHOULD** be abbreviated as ```{}``` and placed on the same line as the previous symbol, separated by a space. For example:
```
class Point
{
    public function __construct (private int $x, private int $y) {}
}
```
```
class Point
{
    public function __construct(
      public readonly int $x,
      public readonly int $y,
    ) {}
}
```

### 4.5 Method and Function Parameters

In the argument list, there **MUST NOT** be a space before each comma, and there **MUST** be one space after each comma.

Argument lists **MAY** be split across multiple lines, where each subsequent line is indented once. When doing so, the first item in the list **MUST** be on the next line, and there **MUST** be only one argument per line. When the argument list is split across multiple lines, the closing parenthesis and opening brace **MUST** be placed together on their own line with one space between them. For example:
```
class ClassName
{
    public function aVeryLongMethodName(
        ClassTypeHint $arg1,
        &$arg2,
        array $arg3 = [],
    ) {
        // method body
    }
}
```

When you have a return type declaration present, there **MUST** be one space after the colon followed by the type declaration. The colon and declaration **MUST** be on the same line as the argument list closing parenthesis with no spaces between the two characters.
```
class ReturnTypeVariations
{
    public function functionName (int $arg1, $arg2): string
    {
        return 'foo';
    }
}
```
```
class ReturnTypeVariations
{
    public function anotherFunction(
        string $foo,
        string $bar,
        int $baz,
    ): string {
        return 'foo';
    }
}
```

In nullable type declarations, there **MUST NOT** be a space between the question mark and the type.
```
class ReturnTypeVariations
{
    public function functionName (?string $arg1, ?int &$arg2): ?string
    {
        return 'foo';
    }
}
```

When using the reference operator ```&``` before an argument, there **MUST NOT** be a space after it.

There **MUST NOT** be a space between the variadic three dot operator and the argument name.

When combining both the reference operator and the variadic three dot operator, there **MUST NOT** be any space between the two of them.

### 4.6 Modifier Keywords

Classes, properties, and methods have numerous keyword modifiers that alter how the engine and language handles them. When present, they **MUST** be in the following order:

- Visibility modifier: public, protected, or private
- Scope modifier: static
- Inheritance modifier: abstract or final
- Mutation modifier: readonly
- Type declaration
- Name

All keywords **MUST** be on a single line, and **MUST** be separated by a single space.

### 4.7 Method and Function Calls

When making a method or function call, there **MUST NOT** be a space between the method or function name and the opening parenthesis, there **MUST NOT** be a space after the opening parenthesis, and there **MUST NOT** be a space before the closing parenthesis. In the argument list, there **MUST NOT** be a space before each comma, and there **MUST** be one space after each comma.

Method chaining **MAY** be put on separate lines, where each subsequent line is indented once. When doing so, the first method **MUST** be on the next line. The final semicolon **MUST** be in a line of its own without indentation. For example:
```
$someInstance
    ->create()
    ->prepare()
    ->run()
;
```

## 5. Control Structures

The general style rules for control structures are as follows:

- There **MUST** be one space after the control structure keyword
- There **MUST NOT** be a space after the opening parenthesis
- There **MUST NOT** be a space before the closing parenthesis
- There **MUST** be one space between the closing parenthesis and the opening brace
- The structure body **MUST** be indented once
- The body **MUST** be on the next line after the opening brace
- The closing brace **MUST** be on the next line after the body

The body of each structure **MUST** be enclosed by braces. This standardizes how the structures look and reduces the likelihood of introducing errors as new lines get added to the body.

### 5.1 ```if```, ```elseif```, ```else```

An ```if``` structure looks like the following. Note the placement of parentheses, spaces, and braces; and that ```else``` and ```elseif``` are on the next line of the closing brace from the earlier body.
```
if ($expr1) {
    // if body
}
else if ($expr2) {
    // elseif body
}
else {
    // else body;
}
```

The keyword ```else if``` **SHOULD** be used instead of ```elseif```.

### 5.2 ```switch```, ```case```, ```match```

A ```switch``` structure looks like the following. Note the placement of parentheses, spaces, and braces. The ```case``` statement **MUST** be indented once from ```switch```, and the ```break``` keyword (or other terminating keywords) **MUST** be indented at the same level as the ```case``` keyword. There **MUST** be a comment such as ```// no break``` when fall-through is intentional in a non-empty case body.
```
switch ($expr) {
    case 0:
        echo 'First case, with a break';
    break;
    case 1:
        echo 'Second case, which falls through';
        // no break
    case 2:
    case 3:
    case 4:
        echo 'Third case, return instead of break';
    return;
    default:
        echo 'Default case';
    break;
}
```

Similarly, a ```match``` expression looks like the following. Note the placement of parentheses, spaces, and braces.
```
$returnValue = match ($expr) {
    0 => 'First case',
    1, 2, 3 => multipleCases(),
    default => 'Default case',
};
```

### 5.3 ```while```, ```dowhile```

A ```while``` statement looks like the following. Note the placement of parentheses, spaces, and braces.
```
while ($expr)
{
    // structure body
}
```

Similarly, a ```do while``` statement looks like the following. Note the placement of parentheses, spaces, and braces.
```
do {
    // structure body;
} while ($expr);
```

### 5.4 ```for```

A ```for``` statement looks like the following. Note the placement of parentheses, spaces, and braces.
```
for ($i = 0; $i < 10; $i++)
{
    // for body
}
```

### 5.5 ```foreach```

A ```foreach``` statement looks like the following. Note the placement of parentheses, spaces, and braces.
```
foreach ($iterable as $value)
{
    // foreach body
}
```
```
foreach ($iterable as $key => $value)
{
    // foreach body
}
```

### 5.6 ```try```, ```catch```, ```finally```

A ```try-catch-finally``` block looks like the following. Note the placement of parentheses, spaces, and braces.
```
try
{
    // try body
}
catch (FirstThrowableType $e)
{
    // catch body
}
catch (OtherThrowableType | AnotherThrowableType $e)
{
    // catch body
}
finally
{
    // finally body
}
```

## 6. Operators

### 6.1 Unary operators

The increment/decrement operators **MUST NOT** have any space between the operator and operand:
```
$i++;
++$j;
```

Type casting operators **MUST NOT** have any space within the parentheses and **MUST NOT** be separated from the variable they are operating on:
```
$intValue = (int)$input;
```

### 6.2 Binary operators

All binary [arithmetic](http://php.net/manual/en/language.operators.arithmetic.php), [comparison](http://php.net/manual/en/language.operators.comparison.php), [assignment](http://php.net/manual/en/language.operators.assignment.php), [bitwise](http://php.net/manual/en/language.operators.bitwise.php), [logical](http://php.net/manual/en/language.operators.logical.php), [string](http://php.net/manual/en/language.operators.string.php), and [type](http://php.net/manual/en/language.operators.type.php) operators **MUST** be preceded and followed by one space:
```
if ($a === $b)
{
    $foo = $bar ?? $a ?? $b;
}
elseif ($a > $b)
{
    $foo = $a + $b * $c;
}
```

### 6.3 Ternary operators

The conditional operator, also known simply as the ternary operator, **MUST** be preceded and followed by one space around both the ```?``` and ```:``` characters:
```
$variable = $foo ? 'foo' : 'bar';
```

When the middle operand of the conditional operator is omitted, the operator **MUST** follow the same style rules as other binary comparison operators:
```
$variable = $foo ?: 'bar';
```

## 7. Closures

Closures, also known as anonymous functions, **MUST** be declared with a space after the ```function``` keyword, and a space before and after the ```use``` keyword.

The opening brace **MUST** go on the same line, and the closing brace **MUST** go on the next line following the body.

There **MUST NOT** be a space after the opening parenthesis of the argument list or variable list, and there **MUST NOT** be a space before the closing parenthesis of the argument list or variable list.

In the argument list and variable list, there **MUST NOT** be a space before each comma, and there **MUST** be one space after each comma.

If a return type is present, it **MUST** follow the same rules as with normal functions and methods; if the ```use``` keyword is present, the colon **MUST** follow the ```use``` list closing parentheses with no spaces between the two characters.

```
$closureWithArgs = function ($arg1, $arg2) {
    // body
};

$closureWithArgsAndVars = function ($arg1, $arg2) use ($var1, $var2) {
    // body
};

$closureWithArgsVarsAndReturn = function ($arg1, $arg2) use ($var1, $var2): bool {
    // body
};
```

Note that the formatting rules also apply when the closure is used directly in a function or method call as an argument.
```
$foo->bar(
    $arg1,
    function ($arg2) use ($var1) {
        // body
    },
    $arg3,
);
```

### 7.1 Short Closures

Short closures, also known as arrow functions, **MUST** follow the same guidelines and principles as long closures above, with the following additions.

The ```fn``` keyword **MUST NOT** be succeeded by a space.

The ```=>``` symbol **MUST** be preceded and succeeded by a space.

The semicolon at the end of the expression **MUST NOT** be preceded by a space.

```
$func = fn(int $x, int $y): int => $x + $y;
$result = $collection->reduce(fn(int $x, int $y): int => $x + $y, 0);
```

## 8. Anonymous Classes

Anonymous Classes **MUST** follow the same guidelines and principles as closures in the above section.

```
$instance = new class {};
```

The opening brace **MAY** be on the same line as the ```class``` keyword.

If the anonymous class has no arguments, the ```()``` after ```class``` **MUST** be omitted.

```
// No arguments
$instance = new class extends \Foo implements \HandleableInterface {
    // Class content
};

// Constructor arguments
$instance = new class($a) extends \Foo implements \ArrayAccess {
    public function __construct (public int $a)
    {
    }
    // Class content
};
```

## 9. Enumerations

Enumerations (enums) **MUST** follow the same guidelines as classes, except where otherwise noted below.

Methods in enums **MUST** follow the same guidelines as methods in classes. Non-public methods MUST use ```private``` instead of ```protected```, as enums do not support inheritance.

When using a backed enum, there **MUST NOT** be a space between the enum name and colon, and there **MUST** be exactly one space between the colon and the backing type. This is consistent with the style for return types.

Constants in Enumerations **MUST** use UPPER_CASE capitalization.

```
enum Suit: string
{
    case HEARTS = 'H';
    case DIAMONDS = 'D';
    case SPADES = 'S';
    case CLUBS = 'C';

    const WILD = self::SPADES;
}
```

## 10. Heredoc and Nowdoc

A nowdoc **SHOULD** be used wherever possible. Heredoc **MAY** be used when a nowdoc does not satisfy requirements.

Declared heredocs or nowdocs **MUST** begin on the same line as the context the declaration is being used in. Subsequent lines in the heredoc or nowdoc **MUST** be at the same indentation then the scope they are declared in.

```
$allowedHeredoc = <<<COMPLIANT
This
is
a
compliant
heredoc
COMPLIANT;
```
```
$allowedNowdoc = <<<'COMPLIANT'
This
is
a
compliant
nowdoc
COMPLIANT;

var_dump(
    'foo',
    <<<'COMPLIANT'
    This
    is
    a
    compliant
    parameter
    COMPLIANT,
    'bar',
);
```

---

## 3. Namespace and Class Names

Namespaces and classes **MUST** follow an [PSR-4](https://www.php-fig.org/psr/psr-4/) autoloading standard.

This means each class is in a file by itself, and is in a namespace of at least one level: a top-level vendor name.

Class names MUST be declared in ```PascalCase```.

## 4. Class Constants, Properties, and Methods

The term "class" refers to all classes, interfaces, and traits.

### 4.1 Constants

Class constants **MUST** be declared in all upper case with underscore separators.
For example:

```
<?php
namespace Vendor\Model;

class Foo
{
    const VERSION = '1.0';
    const DATE_APPROVED = '2012-06-01';
}
```

### 4.2 Properties

This guide intentionally avoids any recommendation regarding the use of ```$PascalCase```, ```$camelCase```, or ```$under_score``` property names.

Whatever naming convention is used **SHOULD** be applied consistently within a reasonable scope. That scope may be vendor-level, package-level, class-level, or method-level.

### 4.3 Methods

Method names MUST be declared in ```camelCase()```.
