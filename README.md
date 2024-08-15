# Easy php.ini

A quick way to prepare your `php.ini` on Windows! ;-)

## Download

PowerShell:

```shell
iwr -outf setup-ini.php https://raw.githubusercontent.com/Piagrammist/easy-php-ini/main/setup-ini.php
```

Batch (Win 10+):

```shell
curl -o setup-ini.php https://raw.githubusercontent.com/Piagrammist/easy-php-ini/main/setup-ini.php
```

> [!TIP]
> For Windows 8.1 and below, you can manually download [curl.exe](https://curl.se/windows/).

## Usage

Simply execute the script using the target php binary:

```shell
C:\php\php.exe setup-ini.php
```

This will automatically find the right ini file, edit and write it to `php.ini` at the php bin directory.

## Config

### Basic

Calling the `setup()` method alone will only uncomment the `ext` entry in `php.ini`:

```php
<?php

(new EasyIni)->setup();
```

### Extensions

Use the `setExtensions()` and/or `addExtension()` methods to add the desired extensions:

```php
<?php

$ini = new EasyIni;
$ini->setExtensions('curl', 'mbstring')
    ->addExtension('zip');
$ini->setExtensions('ftp'); // will override previous ones
$ini->setup();
```

> [!NOTE]
> Zend extensions are not currently supported!

### Environment

Switch between `development` and `production` modes: (Default: `dev`)

```php
<?php

$ini = new EasyIni;
$ini->development();
$ini->production(); // overrides the previous
/*
 * allowed params for `env()`:
 *   d,  dev, development
 *   p, prod, production
 */
$ini->env('dev');
$ini->development(false) // switches to `production` mode
    ->setup();
```

If no `php.ini` already exists, `php.ini-{development,production}` will be used as the template depending on the env value.

### Full example

```php
<?php

(new EasyIni)
    ->production()
    ->setExtensions(
        'curl',
        'mbstring',
        'mysqli',
        'pdo_mysql',
        'pdo_sqlite',
        'sqlite3',
    )
    ->setup();
```
