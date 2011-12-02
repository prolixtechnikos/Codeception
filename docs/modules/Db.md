# Db

Works with SQL dabatase (MySQL tested).

The most important function of this module is cleaning database before each test.
That is the cause this module was added into global configuration file: codeception.yml.
To have your database properly cleaned, you should configure it to access database.

In order to have your database populated with data you need an raw SQL dump.
Just put it in /tests/_data dir (by default) and specify path to it in config.
Next time after database is cleared all your data will be restored from dump.
Don't forget to include CREATE TABLE statements into it.

** Config **
* dsn *required* - PDO DSN
* user *required* - user to access database
* password *required* - password
* dump - path to database dump.

Also provides actions to perform checks in database.


## Actions


### seeInDatabase


Checks if a row with given column values exists.
Provide table name and column values.

Example:

``` php
<?php
$I->seeInDatabase('users', array('name' => 'Davert', 'email' => 'davert * mail.com'));

```
Will generate:

``` sql
SELECT COUNT(*) FROM `users` WHERE `name` = 'Davert AND `email` = 'davert * mail.com'
```
Fails if no such user found.

 * param $table
 * param array $criteria

### dontSeeInDatabase


Effect is opposite to ->seeInDatabase

Checks if there is no record with such column values in database.
Provide table name and column values.

Example:

``` php
<?php
$I->seeInDatabase('users', array('name' => 'Davert', 'email' => 'davert * mail.com'));

```
Will generate:

``` sql
SELECT COUNT(*) FROM `users` WHERE `name` = 'Davert AND `email` = 'davert * mail.com'
```
Fails if such user was found.

 * param $table
 * param array $criteria