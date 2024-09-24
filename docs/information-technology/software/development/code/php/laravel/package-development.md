# Laravel package development


## Notes

If any point, something doesn't make sense, or you made some changes in composer.json of your package: do these (in your test laravel project, not the package project) to ensure the slate is clean:
- Clear bootstrap/cache folder content, don't delete the folder
- Delete vendor folder
- Delete composer.lock
- `composer install`
- `composer dump-autoload`
- Re-require your package
- If none of these work: call an exorcist. Trust me, it worked.


## Resc
- https://laravelpackage.com/02-development-environment/
- [!] https://github.com/spatie/package-skeleton-laravel


## Steps

1. `git init` (duh)

2. `composer init`

3. add `.gitignore`
```
/vendor/
/.idea/
composer.lock
**/coverage/
.phpunit.result.cache
/.phpunit.cache/
/clover.xml

```

4. Create basic folder structure
- /src
- /tests

5. Add orchestra. Enables laravel mocking environment. For type-hint and stuff.

6. Integrate into an actual laravel project for local development and testing purposes
   1. `composer create-project laravel/laravel example-app`
   2. `cd example-app`
   3. `composer install`
   4. Add repository target for your package, do this in the laravel project's `composer.json`:
   ```
   "repositories": [
        {
            "type": "path",
            "url": "../path-to-your-package",
            "options": {
                "symlink": true
            }
        }
    ],
   ```
   5. `composer install`
   6. `composer require username/package-name:dev-master` (username/package-name should be identical with `name` key in your package's `composer.json`.
   7. `composer install`

```
composer require --dev "orchestra/testbench"

```
