# Rector

> [https://github.com/rectorphp/rector](https://github.com/rectorphp/rector)
>
> [Tuto sur grafikart.fr](https://grafikart.fr/tutoriels/rector-php-refactor-1977)

## How to install

```bash
composer require rector/rector --dev
```

## How to use

Once:

```bash
vendor/bin/rector init
```

then

```bash
vendor/bin/rector process . --dry-run
```

(with or without the `--dry-run` flag).

## Write own rules

A nice introduction can be retrieved here (in French): [https://youtu.be/JKN-Ui0FcHQ?t=346](https://youtu.be/JKN-Ui0FcHQ?t=346)

The example will be to inverted arguments i.e.

```php
$this->myService->myMethod('Hello', 'World');
```

should becomes

```php
$this->myService->myMethod('World', 'Hello');
```

The example illustrate how to reach the `myMethod` method call and how to make sure to correctly target `myMethod` (and not f.i. `myMethod2`) and also `myService->myMethod` (and not f.i. `mySecondService->myMethod`) i.e. to check the parent of our method.
