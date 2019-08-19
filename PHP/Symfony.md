# Symfony

## Requirements & Install

* php > 7.1
* install composer
* install [Symfony](https://symfony.com/download)
  * If you are building a traditional web application: `symfony new --full my_project`
  * If you are building a microservice, console application or API: `symfony new my_project`
* without install and make project with composer
  * traditional web application: `composer create-project symfony/website-skeleton my_project_name`
  * microservice, console application or API: `composer create-project symfony/skeleton my_project_name`
* Running: `symfony server:start`
* Installing Packages: `composer require logger`
* Checking Security Vulnerabilities: `symfony check:security`
* Demo application: `symfony new --demo my_project_name`
