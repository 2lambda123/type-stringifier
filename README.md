# Typhoon Type Stringifier

## Installation

```
composer require typhoon/type-stringifier
```

## Usage

```php
use Typhoon\types;
use Typhoon\TypeStringifier;

$type = types::unsealedShape([
    'a' => types::nonEmptyString,
    'b' => types::optionalKey(types::union(types::int, types::float)),
    'c' => types::object(Traversable::class, types::numericString, types::false),
    'd' => types::callable(
        parameters: [
            types::classConstant(PDO::class, '*'),
            types::defaultParam(types::classTemplate('TSend', Generator::class)),
            types::variadicParam(types::scalar),
        ],
        returnType: types::void,
    ),
]);
// string(141) "array{a: non-empty-string, b?: int|float, c: Traversable<numeric-string, false>, d: callable(PDO::*, TSend:Generator=, scalar...): void, ...}"
var_dump(TypeStringifier::stringify($type));
```
