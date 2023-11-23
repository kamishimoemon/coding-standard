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
