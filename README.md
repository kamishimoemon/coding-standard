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
- Files **SHOULD** either declare symbols (classes, functions, constants, etc.) or cause side-effects (e.g. generate output, change .ini settings, etc.) but **SHOULD NOT** do both.
- Namespaces and classes **MUST** follow the [PSR-4](https://www.php-fig.org/psr/psr-4/) autoloading standard.
- Class names **MUST** be declared in ```PascalCase```.
- Class constants **MUST** be declared in all upper case with underscore separators.
- Method names **MUST** be declared in ```camelCase```.

## 2. Files

### 2.1 PHP Tags

PHP code **MUST** use the long ```<?php ?>``` tags or the short-echo ```<?= ?>``` tags; it **MUST NOT** use the other tag variations.

### 2.2 Character Encoding

PHP code MUST use only UTF-8 without BOM.

### 2.3 Side Effects

A file **SHOULD** declare new symbols (classes, functions, constants, etc.) and cause no other side effects, or it **SHOULD** execute logic with side effects, but **SHOULD NOT** do both.
"Side effects" include but are not limited to: generating output, explicit use of ```require``` or ```include```, connecting to external services, modifying ini settings, emitting errors or exceptions, modifying global or static variables, reading from or writing to a file, and so on.

## 3. Namespace and Class Names

Namespaces and classes **MUST** follow an [PSR-4](https://www.php-fig.org/psr/psr-4/) autoloading standard.

This means each class is in a file by itself, and is in a namespace of at least one level: a top-level vendor name.

Class names MUST be declared in ```PascalCase```.
