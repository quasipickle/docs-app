---
layout: default
language: 'fr-fr'
version: '4.0'
title: 'Phalcon\Container'
---

* [Phalcon\Container](#container)

<h1 id="container">Class Phalcon\Container</h1>

[Source sur GitHub](https://github.com/phalcon/cphalcon/blob/v{{ pageVersion }}.0/phalcon/Container.zep)

| Namespace | Phalcon | | Uses | Psr\Container\ContainerInterface, Phalcon\Di\DiInterface | | Implements | ContainerInterface |

PSR-11 Wrapper for `Phalcon\Di`

## Properties

```php
/**
 * @var DiInterface
 */
protected container;

```

## Méthodes

```php
public function __construct( DiInterface $container );
```

Phalcon\Container constructor

```php
public function get( mixed $name ): mixed;
```

Return the service

```php
public function has( mixed $name ): bool;
```

Whether a service exists or not in the container
