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
