# How to use Laravel IDE Helper to help the editor to better understand Laravel

> [Tuto sur grafikart.fr](https://grafikart.fr/tutoriels/laravel-ide-helper-2040#t83)

Using [https://github.com/barryvdh/laravel-ide-helper](https://github.com/barryvdh/laravel-ide-helper) will help our editor (like vscode) to better understand Laravel and his magic method or attributes in models.

## How to install

```bash
composer require --dev barryvdh/laravel-ide-helper
```

Then edit the Laravel `AppServiceProvider` (`app/Providers/AppServiceProvider.php`) to only register the helper when running locally

```php
public function register()
{
    // ...
    if ($this->app->isLocal()) {
        $this->app->register(\Barryvdh\LaravelIdeHelper\IdeHelperServiceProvider::class);
    }
    // ...
}
```

## How to use

From now, it's possible to run:

```bash
php artisan ide-helper:generate
```

That first command will generate the `_ide_helper.php` file. That file will be used by the editor to better understand Laravel facades.

For the second command, prefer to use the `--write-mixin` argument to avoid PHP errors saying a class is already defined since Laravel IDE helper will recreate all models in his `_ide_model.php` file. Using a mixin will add an additional Docblock in all existing models.

```bash
php artisan ide-helper:models -F helpers/_ide_model.php --write-mixin
```

Note: `-F` allow to specify the name of the output file.

## phpstan / larastan integration {#phpstan_mixins}

When the codebase is analyzed using phpstan, the error `PHPDoc tag @mixin contains unknown class` can occurs. This is the case when a model has been updated using `php artisan ide-helper:models --write-mixin` and, thus, a mixin has been added to the model. The referenced mixin class should be accessible to phpstan.

In that scenario, we just need to make sure the `_ide_model.php` file is well loaded by phpstan. This is done by adding the next block at the top of the `phpstan.neon` file:

```neon
scanDirectories:
  - ./helpers
```
