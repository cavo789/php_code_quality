# PHPStan

> [PhpStan](https://phpstan.org/user-guide/getting-started)
>
> [Larastan](https://github.com/nunomaduro/larastan)
>
> Tuto sur grafikart.fr [PHPStan](https://grafikart.fr/tutoriels/laravel-ide-helper-2040#t416) and [Larastan](https://grafikart.fr/tutoriels/laravel-ide-helper-2040#t599)

## How to install

```bash
composer require --dev phpstan/phpstan
```

Also run this command for a Laravel project:

```bash
composer require nunomaduro/larastan:^2.0 --dev
```

For a Laravel project, also refers to [phpstan / larastan integration](#phpstan_mixins)


And add the following block at the top of your `phpstan.neon` file:

```neon
includes:
    - ./vendor/nunomaduro/larastan/extension.neon
```

## How to run

```bash
./vendor/bin/phpstan analyse
```

## Some errors

### Method ... with generic class Illuminate\Database\Eloquent\Builder does not specify its types: TModelClass

This problem is linked to how Laravel works. We need to edit the model (like `App\Models\Post`) and we need to defined the `Builder` parameter or return type.

For instance the declaration below is too generic: 

```php
public function scopePublished(Builder $builder): Builder
```

For phpstan / larastan we need to precise the type of the Builder like below i.e. declare that our builder concerns posts and will return a post.

```php
/**
 * @oaram Builder<Post> $builder
 * @return Builder<Post>
 */ 
public function scopePublished(Builder $builder): Builder
```
