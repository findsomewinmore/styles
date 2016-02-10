# PHP Style Guide
The Findsome & Winmore PHP Style Guide.

Our PHP Style Guide follows the standards specified in the [PSR-1](http://www.php-fig.org/psr/psr-1), [PSR-2](http://www.php-fig.org/psr/psr-2), and [PSR-4](http://www.php-fig.org/psr/psr-4) recommendations proposed by the PHP Framework Interop Group. So, what follows is really what we consider best practices for some common caveats of PHP development not already covered by those recommendations.

## Example using various rules from the PSR recommendations
```php
<?php
declare(strict_types=1);

namespace Vendor\Package;

use Vendor\Package\{ClassA as A, ClassB, ClassC as C};
use Vendor\Package\Namespace\ClassD as D;

use function Vendor\Package\{functionA, functionB, functionC};
use const Vendor\Package\{ConstantA, ConstantB, ConstantC};

class Foo extends Bar implements FooInterface
{
    use FirstTrait;
    use SecondTrait;

    public function sampleFunction(int $a, int $b = null): array
    {
        if ($a === $b) {
            bar();
        } elseif ($a > $b) {
            $foo->bar($arg1);
        } else {
            BazClass::bar($arg2, $arg3);
        }

        foreach ($iterable as $key => $value) {
            // foreach body
        }
    }

    final public static function bar()
    {
        try {
            for ($i = 0; $i < 10; $i++) {
                echo $i;
            }
        } catch (FirstThrowableType $e) {
            exit($e->message());
        } catch (OtherThrowableType $e) {
            exit($e->otherMessage());
        } finally {
            return true;
        }

        do {
            while ($expr2) {
                $expr2 = false;
            }

            $expr = false;
        } while ($expr);
    }
}
```

## Mixing PHP with HTML
In an ideal world, this would never happen as a templating engine would be used instead. But, we do not live in an ideal world. So whenever this is necessary in our unideal world, we like to use [the alternative syntax for control structures](http://php.net/manual/en/control-structures.alternative-syntax.php).

If statements:
```php
<section>
  <?php if ($condition === 1): ?>
    <p>Condition is 1!</p>
  <?php elseif ($condition === 3): ?>
    <p>Condition is 3!</p>
  <?php else: ?>
    <p>Nothing at all, nothing at all, nothing at all.</p>
  <?php endif; ?>
</section>
```

Switches:
```php
<section>
  <?php switch ($value):
    case 1: ?>
      <p>Value is 1.</p>

      <?php break; ?>
    <?php case 2: ?>
      <p>Condition is 2.</p>

      <?php break; ?>
    <?php default: ?>
      <p>Default case.</p>
  <?php endswitch; ?>
</section>
```
For switch statements using the alternative syntax, it's important to note that there cannot be any output between a switch statement and its first case (unless you love syntax errors). Hence, case 1 not having any closing or opening PHP tags before it.

While loops (there is no alternative syntax for do-while loops):
```php
<section>
  <?php while ($condition): ?>
    <p>Condition is <?= $condition; ?> until otherwise!</p>
  <?php endwhile; ?>
</section>
```

For and foreach loops:
```php
<section>
  <ul>
    <?php for ($i = 0; $i < $count; $i++): ?>
      <li><?= $i; ?></li>
    <?php endfor; ?>
  </ul>

  <ul>
    <?php foreach ($collection as $key => $value): ?>
      <li><strong><?= $key; ?>:</strong> <?= $value; ?></li>
    <?php endfor; ?>
  </ul>
</section>
```

Echoing variables (believe it or not it is OK to use the shorthand syntax for echoing):
```php
<h1><?= $var; ?></h1>
```
