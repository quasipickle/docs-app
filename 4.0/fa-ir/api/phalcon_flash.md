---
layout: default
language: 'fa-ir'
version: '4.0'
title: 'Phalcon\Flash'
---

* [Phalcon\Flash\AbstractFlash](#flash-abstractflash)
* [Phalcon\Flash\Direct](#flash-direct)
* [Phalcon\Flash\Exception](#flash-exception)
* [Phalcon\Flash\FlashInterface](#flash-flashinterface)
* [Phalcon\Flash\Session](#flash-session)

<h1 id="flash-abstractflash">Abstract Class Phalcon\Flash\AbstractFlash</h1>

[Source on GitHub](https://github.com/phalcon/cphalcon/blob/v{{ pageVersion }}.0/phalcon/Flash/AbstractFlash.zep)

| Namespace | Phalcon\Flash | | Uses | Phalcon\Di, Phalcon\Di\DiInterface, Phalcon\Di\AbstractInjectionAware, Phalcon\Escaper\EscaperInterface, Phalcon\Session\ManagerInterface | | Extends | AbstractInjectionAware | | Implements | FlashInterface |

Shows HTML notifications related to different circumstances. Classes can be stylized using CSS

```php
$flash->success("The record was successfully deleted");
$flash->error("Cannot open the file");
```

## Properties

```php
/**
 * @var bool
 */
protected autoescape = true;

/**
 * @var bool
 */
protected automaticHtml = true;

/**
 * @var array
 */
protected cssClasses;

/**
 * @var string
 */
protected customTemplate = ;

/**
 * @var EscaperInterface | null
 */
protected escaperService;

/**
 * @var bool
 */
protected implicitFlush = true;

/**
 * @var array
 */
protected messages;

/**
 * @var SessionInterface | null
 */
protected sessionService;

```

## Methods

```php
public function __construct( EscaperInterface $escaper = null, SessionInterface $session = null );
```

Phalcon\Flash constructor

```php
public function clear(): void;
```

Clears accumulated messages when implicit flush is disabled

```php
public function error( string $message ): string | null;
```

Shows a HTML error message

```php
$flash->error("This is an error");
```

```php
public function getAutoescape(): bool
```

```php
public function getCssClasses(): array
```

```php
public function getCustomTemplate(): string
```

```php
public function getEscaperService(): EscaperInterface;
```

Returns the Escaper Service

```php
public function notice( string $message ): string | null;
```

Shows a HTML notice/information message

```php
$flash->notice("This is an information");
```

```php
public function outputMessage( string $type, mixed $message );
```

Outputs a message formatting it with HTML

```php
$flash->outputMessage("error", $message);
```

```php
public function setAutoescape( bool $autoescape ): FlashInterface;
```

Set the autoescape mode in generated HTML

```php
public function setAutomaticHtml( bool $automaticHtml ): FlashInterface;
```

Set if the output must be implicitly formatted with HTML

```php
public function setCssClasses( array $cssClasses ): FlashInterface;
```

Set an array with CSS classes to format the messages

```php
public function setCustomTemplate( string $customTemplate ): FlashInterface;
```

Set an custom template for showing the messages

```php
public function setEscaperService( EscaperInterface $escaperService ): FlashInterface;
```

Sets the Escaper Service

```php
public function setImplicitFlush( bool $implicitFlush ): FlashInterface;
```

Set whether the output must be implicitly flushed to the output or returned as string

```php
public function success( string $message ): string | null;
```

Shows a HTML success message

```php
$flash->success("The process was finished successfully");
```

```php
public function warning( string $message ): string | null;
```

Shows a HTML warning message

```php
$flash->warning("Hey, this is important");
```

<h1 id="flash-direct">Class Phalcon\Flash\Direct</h1>

[Source on GitHub](https://github.com/phalcon/cphalcon/blob/v{{ pageVersion }}.0/phalcon/Flash/Direct.zep)

| Namespace | Phalcon\Flash | | Extends | AbstractFlash |

This is an implementation of the Phalcon\Flash\FlashInterface that immediately outputs any message passed to it.

## Methods

```php
public function message( string $type, mixed $message ): string | null;
```

Outputs a message

```php
public function output( bool $remove = bool ): void;
```

Prints the messages accumulated in the flasher

<h1 id="flash-exception">Class Phalcon\Flash\Exception</h1>

[Source on GitHub](https://github.com/phalcon/cphalcon/blob/v{{ pageVersion }}.0/phalcon/Flash/Exception.zep)

| Namespace | Phalcon\Flash | | Extends | \Phalcon\Exception |

Exceptions thrown in Phalcon\Flash classes will use this class

<h1 id="flash-flashinterface">Interface Phalcon\Flash\FlashInterface</h1>

[Source on GitHub](https://github.com/phalcon/cphalcon/blob/v{{ pageVersion }}.0/phalcon/Flash/FlashInterface.zep)

| Namespace | Phalcon\Flash |

Phalcon\Flash\FlashInterface

Interface for Phalcon\Flash classes

## Methods

```php
public function error( string $message ): string | null;
```

Shows a HTML error message

```php
public function message( string $type, string $message ): string | null;
```

Outputs a message

```php
public function notice( string $message ): string | null;
```

Shows a HTML notice/information message

```php
public function success( string $message ): string | null;
```

Shows a HTML success message

```php
public function warning( string $message ): string | null;
```

Shows a HTML warning message

<h1 id="flash-session">Class Phalcon\Flash\Session</h1>

[Source on GitHub](https://github.com/phalcon/cphalcon/blob/v{{ pageVersion }}.0/phalcon/Flash/Session.zep)

| Namespace | Phalcon\Flash | | Uses | Phalcon\Di\DiInterface, Phalcon\Session\ManagerInterface | | Extends | AbstractFlash |

This is an implementation of the Phalcon\Flash\FlashInterface that temporarily stores the messages in session, then messages can be printed in the next request.

## Methods

```php
public function clear(): void;
```

Clear messages in the session messenger

```php
public function getMessages( mixed $type = null, bool $remove = bool ): array;
```

Returns the messages in the session flasher

```php
public function getSessionService(): ManagerInterface;
```

Returns the Session Service

```php
public function has( mixed $type = null ): bool;
```

Checks whether there are messages

```php
public function message( string $type, string $message ): string | null;
```

Adds a message to the session flasher

```php
public function output( bool $remove = bool ): void;
```

Prints the messages in the session flasher

```php
protected function getSessionMessages( bool $remove, mixed $type = null ): array;
```

Returns the messages stored in session

```php
protected function setSessionMessages( array $messages ): array;
```

Stores the messages in session
