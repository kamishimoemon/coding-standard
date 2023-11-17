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
