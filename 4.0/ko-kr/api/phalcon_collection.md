---
layout: default
language: 'ko-kr'
version: '4.0'
title: 'Phalcon\Collection'
---

- [Phalcon\Collection](#collection)
- [Phalcon\Collection\CollectionInterface](#collection-collectioninterface)
- [Phalcon\Collection\Exception](#collection-exception)
- [Phalcon\Collection\ReadOnly](#collection-readonly)

<h1 id="collection">Class Phalcon\Collection</h1>

[Source on GitHub](https://github.com/phalcon/cphalcon/blob/v{{ pageVersion }}.0/phalcon/Collection.zep)

| Namespace | Phalcon | | Uses | ArrayAccess, ArrayIterator, Countable, IteratorAggregate, JsonSerializable, Phalcon\Collection\CollectionInterface, Phalcon\Helper\Json, Serializable, Traversable | | Implements | ArrayAccess, CollectionInterface, Countable, IteratorAggregate, JsonSerializable, Serializable |

`Phalcon\Collection` is a supercharged object oriented array. It implements:

- [ArrayAccess](https://www.php.net/manual/en/class.arrayaccess.php)
- [Countable](https://www.php.net/manual/en/class.countable.php)
- [IteratorAggregate](https://www.php.net/manual/en/class.iteratoraggregate.php)
- [JsonSerializable](https://www.php.net/manual/en/class.jsonserializable.php)
- [Serializable](https://www.php.net/manual/en/class.serializable.php)

It can be used in any part of the application that needs collection of data Such implementations are for instance accessing globals `$_GET`, `$_POST` etc.

## Properties

```php
/**
 * @var array
 */
protected data;

/**
 * @var bool
 */
protected insensitive = true;

/**
 * @var array
 */
protected lowerKeys;

```

## Methods

```php
public function __construct( array $data = [], bool $insensitive = bool );
```

Collection constructor.

```php
public function __get( string $element ): mixed;
```

Magic getter to get an element from the collection

```php
public function __isset( string $element ): bool;
```

Magic isset to check whether an element exists or not

```php
public function __set( string $element, mixed $value ): void;
```

Magic setter to assign values to an element

```php
public function __unset( string $element ): void;
```

Magic unset to remove an element from the collection

```php
public function clear(): void;
```

Clears the internal collection

```php
public function count(): int;
```

Count elements of an object. See [count](https://php.net/manual/en/countable.count.php)

```php
public function get( string $element, mixed $defaultValue = null, string $cast = null ): mixed;
```

Get the element from the collection

```php
public function getIterator(): Traversable;
```

Returns the iterator of the class

```php
public function getKeys( bool $insensitive = bool ): array;
```

```php
public function getValues(): array;
```

```php
public function has( string $element ): bool;
```

Determines whether an element is present in the collection.

```php
public function init( array $data = [] ): void;
```

Initialize internal array

```php
public function jsonSerialize(): array;
```

Specify data which should be serialized to JSON See [jsonSerialize](https://php.net/manual/en/jsonserializable.jsonserialize.php)

```php
public function offsetExists( mixed $element ): bool;
```

Whether a offset exists See [offsetExists](https://php.net/manual/en/arrayaccess.offsetexists.php)

```php
public function offsetGet( mixed $element );
```

Offset to retrieve See [offsetGet](https://php.net/manual/en/arrayaccess.offsetget.php)

```php
public function offsetSet( mixed $element, mixed $value ): void;
```

Offset to set See [offsetSet](https://php.net/manual/en/arrayaccess.offsetset.php)

```php
public function offsetUnset( mixed $element ): void;
```

Offset to unset See [offsetUnset](https://php.net/manual/en/arrayaccess.offsetunset.php)

```php
public function remove( string $element ): void;
```

Delete the element from the collection

```php
public function serialize(): string;
```

String representation of object See [serialize](https://php.net/manual/en/serializable.serialize.php)

```php
public function set( string $element, mixed $value ): void;
```

Set an element in the collection

```php
public function toArray(): array;
```

Returns the object in an array format

```php
public function toJson( int $options = int ): string;
```

Returns the object in a JSON format

The default string uses the following options for json_encode

`JSON_HEX_TAG`, `JSON_HEX_APOS`, `JSON_HEX_AMP`, `JSON_HEX_QUOT`, `JSON_UNESCAPED_SLASHES`

See [rfc4627](https://www.ietf.org/rfc/rfc4627.txt)

```php
public function unserialize( mixed $serialized ): void;
```

Constructs the object See [unserialize](https://php.net/manual/en/serializable.unserialize.php)

```php
protected function setData( string $element, mixed $value ): void;
```

Internal method to set data

<h1 id="collection-collectioninterface">Interface Phalcon\Collection\CollectionInterface</h1>

[Source on GitHub](https://github.com/phalcon/cphalcon/blob/v{{ pageVersion }}.0/phalcon/Collection/CollectionInterface.zep)

| Namespace | Phalcon\Collection |

Phalcon\Collection\CollectionInterface

Interface for Phalcon\Collection class

## Methods

```php
public function __get( string $element ): mixed;
```

```php
public function __isset( string $element ): bool;
```

```php
public function __set( string $element, mixed $value ): void;
```

```php
public function __unset( string $element ): void;
```

```php
public function clear(): void;
```

```php
public function get( string $element, mixed $defaultValue = null, string $cast = null ): mixed;
```

```php
public function getKeys( bool $insensitive = bool ): array;
```

```php
public function getValues(): array;
```

```php
public function has( string $element ): bool;
```

```php
public function init( array $data = [] ): void;
```

```php
public function remove( string $element ): void;
```

```php
public function set( string $element, mixed $value ): void;
```

```php
public function toArray(): array;
```

```php
public function toJson( int $options = int ): string;
```

<h1 id="collection-exception">Class Phalcon\Collection\Exception</h1>

[Source on GitHub](https://github.com/phalcon/cphalcon/blob/v{{ pageVersion }}.0/phalcon/Collection/Exception.zep)

| Namespace | Phalcon\Collection | | Uses | Throwable | | Extends | \Phalcon\Exception | | Implements | Throwable |

Exceptions for the Collection object

<h1 id="collection-readonly">Class Phalcon\Collection\ReadOnly</h1>

[Source on GitHub](https://github.com/phalcon/cphalcon/blob/v{{ pageVersion }}.0/phalcon/Collection/ReadOnly.zep)

| Namespace | Phalcon\Collection | | Uses | Phalcon\Collection | | Extends | Collection |

Phalcon\Collection\ReadOnly is a read only Collection object

## Methods

```php
public function remove( string $element ): void;
```

Delete the element from the collection

```php
public function set( string $element, mixed $value ): void;
```

Set an element in the collection
