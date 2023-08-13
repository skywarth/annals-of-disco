# Laravel package development


## Notes

If any point, something doesn't make sense, or you made some changes in composer.json of your package: do these to ensure the slate is clean:
- Clear bootstrap/cache folder content, don't delete the folder
- Delete vendor folder
- Delete composer.lock
- `composer install`
- `composer dump-autoload`
- Re-require your package
- If none of these work: call an exorcist. Trust me, it worked.


## Resc
https://laravelpackage.com/02-development-environment/


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

5. Add your package development folder into an actual laravel project for basic testing capabilities.
```
"repositories": [
        {
            "type": "path",
            "url": "../path-to-your-package"
        }
    ]
```
6. Add orchestra. Enables laravel mocking environment. For type-hint and stuff.
```
composer require --dev "orchestra/testbench"

```
