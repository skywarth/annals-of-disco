### Composer

#### `composer install`

- If `composer.lock` is present it'll install dependencies from there
- If `composer.lock` is NOT present:
  - install dependencies by `composer.json`
  - create composer.lock
  
#### `composer update`
- Reads `composer.json`
- Remove not used but installed
- Check the availability of the latest versions of your required packages
- Install the latest versions of your packages
- Update `composer.lock` to store the installed packages version
