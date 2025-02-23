---
layout: default
language: 'uk-ua'
version: '4.0'
title: 'Phalcon\Security'
---

- [Phalcon\Security](#security)
- [Phalcon\Security\Exception](#security-exception)
- [Phalcon\Security\JWT\Builder](#security-jwt-builder)
- [Phalcon\Security\JWT\Exceptions\UnsupportedAlgorithmException](#security-jwt-exceptions-unsupportedalgorithmexception)
- [Phalcon\Security\JWT\Exceptions\ValidatorException](#security-jwt-exceptions-validatorexception)
- [Phalcon\Security\JWT\Signer\AbstractSigner](#security-jwt-signer-abstractsigner)
- [Phalcon\Security\JWT\Signer\Hmac](#security-jwt-signer-hmac)
- [Phalcon\Security\JWT\Signer\None](#security-jwt-signer-none)
- [Phalcon\Security\JWT\Signer\SignerInterface](#security-jwt-signer-signerinterface)
- [Phalcon\Security\JWT\Token\AbstractItem](#security-jwt-token-abstractitem)
- [Phalcon\Security\JWT\Token\Enum](#security-jwt-token-enum)
- [Phalcon\Security\JWT\Token\Item](#security-jwt-token-item)
- [Phalcon\Security\JWT\Token\Parser](#security-jwt-token-parser)
- [Phalcon\Security\JWT\Token\Signature](#security-jwt-token-signature)
- [Phalcon\Security\JWT\Token\Token](#security-jwt-token-token)
- [Phalcon\Security\JWT\Validator](#security-jwt-validator)
- [Phalcon\Security\Random](#security-random)

<h1 id="security">Class Phalcon\Security</h1>

[Source on GitHub](https://github.com/phalcon/cphalcon/blob/v{{ pageVersion }}.0/phalcon/Security.zep)

| Namespace | Phalcon | | Uses | Phalcon\Di\DiInterface, Phalcon\Di\AbstractInjectionAware, Phalcon\Http\RequestInterface, Phalcon\Security\Random, Phalcon\Security\Exception, Phalcon\Session\ManagerInterface | | Extends | AbstractInjectionAware |

This component provides a set of functions to improve the security in Phalcon applications

```php
$login    = $this->request->getPost("login");
$password = $this->request->getPost("password");

$user = Users::findFirstByLogin($login);

if ($user) {
    if ($this->security->checkHash($password, $user->password)) {
        // The password is valid
    }
}
```

## Constants

```php
const CRYPT_BLOWFISH = 4;
const CRYPT_BLOWFISH_A = 5;
const CRYPT_BLOWFISH_X = 6;
const CRYPT_BLOWFISH_Y = 7;
const CRYPT_DEFAULT = 0;
const CRYPT_EXT_DES = 2;
const CRYPT_MD5 = 3;
const CRYPT_SHA256 = 8;
const CRYPT_SHA512 = 9;
const CRYPT_STD_DES = 1;
```

## Властивості

```php
/**
 * @var int|null
 */
protected defaultHash;

/**
 * @var int
 */
protected numberBytes = 16;

/**
 * @var Random
 */
protected random;

/**
 * @var string}null
 */
protected requestToken;

/**
 * @var string|null
 */
protected token;

/**
 * @var string|null
 */
protected tokenKey;

/**
 * @var string
 */
protected tokenKeySessionId = $PHALCON/CSRF/KEY$;

/**
 * @var string
 */
protected tokenValueSessionId = $PHALCON/CSRF$;

/**
 * @var int
 */
protected workFactor = 10;

/**
 * @var SessionInterface|null
 */
private localSession;

/**
 * @var RequestInterface|null
 */
private localRequest;

```

## Методи

```php
public function __construct( SessionInterface $session = null, RequestInterface $request = null );
```

Phalcon\Security constructor

```php
public function checkHash( string $password, string $passwordHash, int $maxPassLength = int ): bool;
```

Checks a plain text password and its hash version to check if the password matches

```php
public function checkToken( mixed $tokenKey = null, mixed $tokenValue = null, bool $destroyIfValid = bool ): bool;
```

Check if the CSRF token sent in the request is the same that the current in session

```php
public function computeHmac( string $data, string $key, string $algo, bool $raw = bool ): string;
```

Computes a HMAC

```php
public function destroyToken(): Security;
```

Removes the value of the CSRF token and key from session

```php
public function getDefaultHash(): int | null;
```

Returns the default hash

```php
public function getRandom(): Random;
```

Returns a secure random number generator instance

```php
public function getRandomBytes(): int;
```

Returns a number of bytes to be generated by the openssl pseudo random generator

```php
public function getRequestToken(): string | null;
```

Returns the value of the CSRF token for the current request.

```php
public function getSaltBytes( int $numberBytes = int ): string;
```

Generate a >22-length pseudo random string to be used as salt for passwords

```php
public function getSessionToken(): string | null;
```

Returns the value of the CSRF token in session

```php
public function getToken(): string;
```

Generates a pseudo random token value to be used as input's value in a CSRF check

```php
public function getTokenKey(): string;
```

Generates a pseudo random token key to be used as input's name in a CSRF check

```php
public function getWorkFactor(): int
```

```php
public function hash( string $password, int $workFactor = int ): string;
```

Creates a password hash using bcrypt with a pseudo random salt

```php
public function isLegacyHash( string $passwordHash ): bool;
```

Checks if a password hash is a valid bcrypt's hash

```php
public function setDefaultHash( int $defaultHash ): Security;
```

Sets the default hash

```php
public function setRandomBytes( int $randomBytes ): Security;
```

Sets a number of bytes to be generated by the openssl pseudo random generator

```php
public function setWorkFactor( int $workFactor ): Security;
```

Sets the work factor

<h1 id="security-exception">Class Phalcon\Security\Exception</h1>

[Source on GitHub](https://github.com/phalcon/cphalcon/blob/v{{ pageVersion }}.0/phalcon/Security/Exception.zep)

| Namespace | Phalcon\Security | | Extends | \Phalcon\Exception |

Phalcon\Security\Exception

Exceptions thrown in Phalcon\Security will use this class

<h1 id="security-jwt-builder">Class Phalcon\Security\JWT\Builder</h1>

[Source on GitHub](https://github.com/phalcon/cphalcon/blob/v{{ pageVersion }}.0/phalcon/Security/JWT/Builder.zep)

![](/assets/images/version-4.1.svg)

| Namespace | Phalcon\Security\JWT | | Uses | Phalcon\Collection, Phalcon\Collection\CollectionInterface, Phalcon\Helper\Base64, Phalcon\Helper\Json, Phalcon\Security\JWT\Exceptions\ValidatorException, Phalcon\Security\JWT\Signer\SignerInterface, Phalcon\Security\JWT\Token\Enum, Phalcon\Security\JWT\Token\Item, Phalcon\Security\JWT\Token\Signature, Phalcon\Security\JWT\Token\Token |

Class Builder

@property CollectionInterface $claims @property CollectionInterface $jose @property string $passphrase @property SignerInterface $signer

@link https://tools.ietf.org/html/rfc7519

## Властивості

```php
/**
 * @var CollectionInterface
 */
private claims;

/**
 * @var CollectionInterface
 */
private jose;

/**
 * @var string
 */
private passphrase;

/**
 * @var SignerInterface
 */
private signer;

```

## Методи

```php
public function __construct( SignerInterface $signer );
```

Builder constructor.

```php
public function getAudience();
```

```php
public function getClaims(): array;
```

```php
public function getContentType(): string | null;
```

```php
public function getExpirationTime(): int | null;
```

```php
public function getHeaders(): array;
```

```php
public function getId(): string | null;
```

```php
public function getIssuedAt(): int | null;
```

```php
public function getIssuer(): string | null;
```

```php
public function getNotBefore(): int | null;
```

```php
public function getPassphrase(): string;
```

```php
public function getSubject(): string | null;
```

```php
public function getToken(): Token;
```

```php
public function init(): Builder;
```

```php
public function setAudience( mixed $audience ): Builder;
```

The "aud" (audience) claim identifies the recipients that the JWT is intended for. Each principal intended to process the JWT MUST identify itself with a value in the audience claim. If the principal processing the claim does not identify itself with a value in the "aud" claim when this claim is present, then the JWT MUST be rejected. In the general case, the "aud" value is an array of case- sensitive strings, each containing a StringOrURI value. In the special case when the JWT has one audience, the "aud" value MAY be a single case-sensitive string containing a StringOrURI value. The interpretation of audience values is generally application specific. Use of this claim is OPTIONAL.

```php
public function setContentType( string $contentType ): Builder;
```

Sets the content type header 'cty'

```php
public function setExpirationTime( int $timestamp ): Builder;
```

The "exp" (expiration time) claim identifies the expiration time on or after which the JWT MUST NOT be accepted for processing. The processing of the "exp" claim requires that the current date/time MUST be before the expiration date/time listed in the "exp" claim. Implementers MAY provide for some small leeway, usually no more than a few minutes, to account for clock skew. Its value MUST be a number containing a NumericDate value. Use of this claim is OPTIONAL.

```php
public function setId( string $id ): Builder;
```

The "jti" (JWT ID) claim provides a unique identifier for the JWT. The identifier value MUST be assigned in a manner that ensures that there is a negligible probability that the same value will be accidentally assigned to a different data object; if the application uses multiple issuers, collisions MUST be prevented among values produced by different issuers as well. The "jti" claim can be used to prevent the JWT from being replayed. The "jti" value is a case- sensitive string. Use of this claim is OPTIONAL.

```php
public function setIssuedAt( int $timestamp ): Builder;
```

The "iat" (issued at) claim identifies the time at which the JWT was issued. This claim can be used to determine the age of the JWT. Its value MUST be a number containing a NumericDate value. Use of this claim is OPTIONAL.

```php
public function setIssuer( string $issuer ): Builder;
```

The "iss" (issuer) claim identifies the principal that issued the JWT. The processing of this claim is generally application specific. The "iss" value is a case-sensitive string containing a StringOrURI value. Use of this claim is OPTIONAL.

```php
public function setNotBefore( int $timestamp ): Builder;
```

The "nbf" (not before) claim identifies the time before which the JWT MUST NOT be accepted for processing. The processing of the "nbf" claim requires that the current date/time MUST be after or equal to the not-before date/time listed in the "nbf" claim. Implementers MAY provide for some small leeway, usually no more than a few minutes, to account for clock skew. Its value MUST be a number containing a NumericDate value. Use of this claim is OPTIONAL.

```php
public function setPassphrase( string $passphrase ): Builder;
```

```php
public function setSubject( string $subject ): Builder;
```

The "sub" (subject) claim identifies the principal that is the subject of the JWT. The claims in a JWT are normally statements about the subject. The subject value MUST either be scoped to be locally unique in the context of the issuer or be globally unique. The processing of this claim is generally application specific. The "sub" value is a case-sensitive string containing a StringOrURI value. Use of this claim is OPTIONAL.

<h1 id="security-jwt-exceptions-unsupportedalgorithmexception">Class Phalcon\Security\JWT\Exceptions\UnsupportedAlgorithmException</h1>

[Source on GitHub](https://github.com/phalcon/cphalcon/blob/v{{ pageVersion }}.0/phalcon/Security/JWT/Exceptions/UnsupportedAlgorithmException.zep)

![](/assets/images/version-4.1.svg)

| Namespace | Phalcon\Security\JWT\Exceptions | | Uses | Exception, Throwable | | Extends | Exception | | Implements | Throwable |

This file is part of the Phalcon Framework.

(c) Phalcon Team [&#116;&#x65;&#97;&#109;&#x40;&#112;&#104;&#x61;&#108;c&#x6f;&#110;&#x2e;&#x69;&#111;](&#x6d;&#97;&#x69;&#x6c;&#116;&#x6f;&#58;&#116;&#x65;&#97;&#109;&#x40;&#112;&#104;&#x61;&#108;c&#x6f;&#110;&#x2e;&#x69;&#111;)

For the full copyright and license information, please view the LICENSE.txt file that was distributed with this source code.

<h1 id="security-jwt-exceptions-validatorexception">Class Phalcon\Security\JWT\Exceptions\ValidatorException</h1>

[Source on GitHub](https://github.com/phalcon/cphalcon/blob/v{{ pageVersion }}.0/phalcon/Security/JWT/Exceptions/ValidatorException.zep)

![](/assets/images/version-4.1.svg)

| Namespace | Phalcon\Security\JWT\Exceptions | | Uses | Exception, Throwable | | Extends | Exception | | Implements | Throwable |

This file is part of the Phalcon Framework.

(c) Phalcon Team [&#116;&#x65;&#97;&#109;&#x40;&#112;&#104;&#x61;&#108;c&#x6f;&#110;&#x2e;&#x69;&#111;](&#x6d;&#97;&#x69;&#x6c;&#116;&#x6f;&#58;&#116;&#x65;&#97;&#109;&#x40;&#112;&#104;&#x61;&#108;c&#x6f;&#110;&#x2e;&#x69;&#111;)

For the full copyright and license information, please view the LICENSE.txt file that was distributed with this source code.

<h1 id="security-jwt-signer-abstractsigner">Abstract Class Phalcon\Security\JWT\Signer\AbstractSigner</h1>

[Source on GitHub](https://github.com/phalcon/cphalcon/blob/v{{ pageVersion }}.0/phalcon/Security/JWT/Signer/AbstractSigner.zep)

![](/assets/images/version-4.1.svg)

| Namespace | Phalcon\Security\JWT\Signer | | Implements | SignerInterface |

Class AbstractSigner

@property string $algo

## Властивості

```php
/**
 * @var string
 */
protected algorithm;

```

## Методи

```php
public function getAlgorithm(): string
```

<h1 id="security-jwt-signer-hmac">Class Phalcon\Security\JWT\Signer\Hmac</h1>

[Source on GitHub](https://github.com/phalcon/cphalcon/blob/v{{ pageVersion }}.0/phalcon/Security/JWT/Signer/Hmac.zep)

![](/assets/images/version-4.1.svg)

| Namespace | Phalcon\Security\JWT\Signer | | Uses | Phalcon\Security\JWT\Exceptions\UnsupportedAlgorithmException | | Extends | AbstractSigner |

Class Hmac

## Методи

```php
public function __construct( string $algo = string );
```

Hmac constructor.

```php
public function getAlgHeader(): string;
```

Return the value that is used for the "alg" header

```php
public function sign( string $payload, string $passphrase ): string;
```

Sign a payload using the passphrase

```php
public function verify( string $source, string $payload, string $passphrase ): bool;
```

Verify a passed source with a payload and passphrase

<h1 id="security-jwt-signer-none">Class Phalcon\Security\JWT\Signer\None</h1>

[Source on GitHub](https://github.com/phalcon/cphalcon/blob/v{{ pageVersion }}.0/phalcon/Security/JWT/Signer/None.zep)

![](/assets/images/version-4.1.svg)

| Namespace | Phalcon\Security\JWT\Signer | | Implements | SignerInterface |

Class None

## Методи

```php
public function getAlgHeader(): string;
```

Return the value that is used for the "alg" header

```php
public function getAlgorithm(): string;
```

Return the algorithm used

```php
public function sign( string $payload, string $passphrase ): string;
```

Sign a payload using the passphrase

```php
public function verify( string $source, string $payload, string $passphrase ): bool;
```

Verify a passed source with a payload and passphrase

<h1 id="security-jwt-signer-signerinterface">Interface Phalcon\Security\JWT\Signer\SignerInterface</h1>

[Source on GitHub](https://github.com/phalcon/cphalcon/blob/v{{ pageVersion }}.0/phalcon/Security/JWT/Signer/SignerInterface.zep)

![](/assets/images/version-4.1.svg)

| Namespace | Phalcon\Security\JWT\Signer |

This file is part of the Phalcon Framework.

(c) Phalcon Team [&#116;&#x65;&#97;&#109;&#x40;&#112;&#104;&#x61;&#108;c&#x6f;&#110;&#x2e;&#x69;&#111;](&#x6d;&#97;&#x69;&#x6c;&#116;&#x6f;&#58;&#116;&#x65;&#97;&#109;&#x40;&#112;&#104;&#x61;&#108;c&#x6f;&#110;&#x2e;&#x69;&#111;)

For the full copyright and license information, please view the LICENSE.txt file that was distributed with this source code.

## Методи

```php
public function getAlgHeader(): string;
```

Return the value that is used for the "alg" header

```php
public function getAlgorithm(): string;
```

Return the algorithm used

```php
public function sign( string $payload, string $passphrase ): string;
```

Sign a payload using the passphrase

```php
public function verify( string $source, string $payload, string $passphrase ): bool;
```

Verify a passed source with a payload and passphrase

<h1 id="security-jwt-token-abstractitem">Abstract Class Phalcon\Security\JWT\Token\AbstractItem</h1>

[Source on GitHub](https://github.com/phalcon/cphalcon/blob/v{{ pageVersion }}.0/phalcon/Security/JWT/Token/AbstractItem.zep)

| Namespace | Phalcon\Security\JWT\Token |

Class AbstractItem

@property array $data

## Властивості

```php
/**
 * @var array
 */
protected data;

```

## Методи

```php
public function getEncoded(): string;
```

<h1 id="security-jwt-token-enum">Class Phalcon\Security\JWT\Token\Enum</h1>

[Source on GitHub](https://github.com/phalcon/cphalcon/blob/v{{ pageVersion }}.0/phalcon/Security/JWT/Token/Enum.zep)

![](/assets/images/version-4.1.svg)

| Namespace | Phalcon\Security\JWT\Token |

Class Enum

@link https://tools.ietf.org/html/rfc7519

## Constants

```php
const ALGO            = 'alg';
const AUDIENCE        = 'aud';
const CONTENT_TYPE    = 'cty';
const EXPIRATION_TIME = 'exp';
const ID              = 'jti';
const ISSUED_AT       = 'iat';
const ISSUER          = 'iss';
const NOT_BEFORE      = 'nbf';
const SUBJECT         = 'sub';
const TYPE            = 'typ';
```

<h1 id="security-jwt-token-item">Class Phalcon\Security\JWT\Token\Item</h1>

[Source on GitHub](https://github.com/phalcon/cphalcon/blob/v{{ pageVersion }}.0/phalcon/Security/JWT/Token/Item.zep)

![](/assets/images/version-4.1.svg)

| Namespace | Phalcon\Security\JWT\Token | | Extends | AbstractItem |

Class Item

## Методи

```php
public function __construct( array $payload, string $encoded );
```

Item constructor.

```php
public function get( string $name, mixed $defaultValue = null ): mixed | null;
```

```php
public function getPayload(): array;
```

```php
public function has( string $name ): bool;
```

<h1 id="security-jwt-token-parser">Class Phalcon\Security\JWT\Token\Parser</h1>

[Source on GitHub](https://github.com/phalcon/cphalcon/blob/v{{ pageVersion }}.0/phalcon/Security/JWT/Token/Parser.zep)

![](/assets/images/version-4.1.svg)

| Namespace | Phalcon\Security\JWT\Token | | Uses | InvalidArgumentException, Phalcon\Helper\Arr, Phalcon\Helper\Base64, Phalcon\Helper\Json |

Class Parser

## Методи

```php
public function parse( string $token ): Token;
```

Parse a token and return it

<h1 id="security-jwt-token-signature">Class Phalcon\Security\JWT\Token\Signature</h1>

[Source on GitHub](https://github.com/phalcon/cphalcon/blob/v{{ pageVersion }}.0/phalcon/Security/JWT/Token/Signature.zep)

![](/assets/images/version-4.1.svg)

| Namespace | Phalcon\Security\JWT\Token | | Extends | AbstractItem |

Class Item

## Методи

```php
public function __construct( string $hash = string, string $encoded = string );
```

Signature constructor.

```php
public function getHash(): string;
```

<h1 id="security-jwt-token-token">Class Phalcon\Security\JWT\Token\Token</h1>

[Source on GitHub](https://github.com/phalcon/cphalcon/blob/v{{ pageVersion }}.0/phalcon/Security/JWT/Token/Token.zep)

![](/assets/images/version-4.1.svg)

| Namespace | Phalcon\Security\JWT\Token |

Class Token

@property Item $claims @property Item $headers @property Signature $signature

@link https://tools.ietf.org/html/rfc7519

## Властивості

```php
/**
 * @var Item
 */
private claims;

/**
 * @var Item
 */
private headers;

/**
 * @var Signature
 */
private signature;

```

## Методи

```php
public function __construct( Item $headers, Item $claims, Signature $signature );
```

Token constructor.

```php
public function getClaims(): Item
```

```php
public function getHeaders(): Item
```

```php
public function getPayload(): string;
```

```php
public function getSignature(): Signature
```

```php
public function getToken(): string;
```

<h1 id="security-jwt-validator">Class Phalcon\Security\JWT\Validator</h1>

[Source on GitHub](https://github.com/phalcon/cphalcon/blob/v{{ pageVersion }}.0/phalcon/Security/JWT/Validator.zep)

![](/assets/images/version-4.1.svg)

| Namespace | Phalcon\Security\JWT | | Uses | Phalcon\Security\JWT\Exceptions\ValidatorException, Phalcon\Security\JWT\Signer\SignerInterface, Phalcon\Security\JWT\Token\Enum, Phalcon\Security\JWT\Token\Token |

Class Validator

@property int $timeShift @property Token $token

## Властивості

```php
/**
 * @var int
 */
private timeShift = 0;

/**
 * @var Token
 */
private token;

```

## Методи

```php
public function __construct( Token $token, int $timeShift = int );
```

Validator constructor.

```php
public function setToken( Token $token ): Validator;
```

```php
public function validateAudience( string $audience ): Validator;
```

```php
public function validateExpiration( int $timestamp ): Validator;
```

```php
public function validateId( string $id ): Validator;
```

```php
public function validateIssuedAt( int $timestamp ): Validator;
```

```php
public function validateIssuer( string $issuer ): Validator;
```

```php
public function validateNotBefore( int $timestamp ): Validator;
```

```php
public function validateSignature( SignerInterface $signer, string $passphrase ): Validator;
```

<h1 id="security-random">Class Phalcon\Security\Random</h1>

[Source on GitHub](https://github.com/phalcon/cphalcon/blob/v{{ pageVersion }}.0/phalcon/Security/Random.zep)

| Namespace | Phalcon\Security |

Phalcon\Security\Random

Secure random number generator class.

Provides secure random number generator which is suitable for generating session key in HTTP cookies, etc.

`Phalcon\Security\Random` could be mainly useful for:

- Key generation (e.g. generation of complicated keys)
- Generating random passwords for new user accounts
- Encryption systems

```php
$random = new \Phalcon\Security\Random();

// Random binary string
$bytes = $random->bytes();

// Random hex string
echo $random->hex(10); // a29f470508d5ccb8e289
echo $random->hex(10); // 533c2f08d5eee750e64a
echo $random->hex(11); // f362ef96cb9ffef150c9cd
echo $random->hex(12); // 95469d667475125208be45c4
echo $random->hex(13); // 05475e8af4a34f8f743ab48761

// Random base62 string
echo $random->base62(); // z0RkwHfh8ErDM1xw

// Random base64 string
echo $random->base64(12); // XfIN81jGGuKkcE1E
echo $random->base64(12); // 3rcq39QzGK9fUqh8
echo $random->base64();   // DRcfbngL/iOo9hGGvy1TcQ==
echo $random->base64(16); // SvdhPcIHDZFad838Bb0Swg==

// Random URL-safe base64 string
echo $random->base64Safe();           // PcV6jGbJ6vfVw7hfKIFDGA
echo $random->base64Safe();           // GD8JojhzSTrqX7Q8J6uug
echo $random->base64Safe(8);          // mGyy0evy3ok
echo $random->base64Safe(null, true); // DRrAgOFkS4rvRiVHFefcQ==

// Random UUID
echo $random->uuid(); // db082997-2572-4e2c-a046-5eefe97b1235
echo $random->uuid(); // da2aa0e2-b4d0-4e3c-99f5-f5ef62c57fe2
echo $random->uuid(); // 75e6b628-c562-4117-bb76-61c4153455a9
echo $random->uuid(); // dc446df1-0848-4d05-b501-4af3c220c13d

// Random number between 0 and $len
echo $random->number(256); // 84
echo $random->number(256); // 79
echo $random->number(100); // 29
echo $random->number(300); // 40

// Random base58 string
echo $random->base58();   // 4kUgL2pdQMSCQtjE
echo $random->base58();   // Umjxqf7ZPwh765yR
echo $random->base58(24); // qoXcgmw4A9dys26HaNEdCRj9
echo $random->base58(7);  // 774SJD3vgP
```

This class partially borrows SecureRandom library from Ruby

@link http://ruby-doc.org/stdlib-2.2.2/libdoc/securerandom/rdoc/SecureRandom.html

## Методи

```php
public function base58( int $len = null ): string;
```

Generates a random base58 string

If $len is not specified, 16 is assumed. It may be larger in future. The result may contain alphanumeric characters except 0, O, I and l.

It is similar to `Phalcon\Security\Random::base64()` but has been modified to avoid both non-alphanumeric characters and letters which might look ambiguous when printed.

```php
$random = new \Phalcon\Security\Random();

echo $random->base58(); // 4kUgL2pdQMSCQtjE
```

@see \Phalcon\Security\Random:base64 @link https://en.wikipedia.org/wiki/Base58 @throws Exception If secure random number generator is not available or unexpected partial read

```php
public function base62( int $len = null ): string;
```

Generates a random base62 string

If $len is not specified, 16 is assumed. It may be larger in future.

It is similar to `Phalcon\Security\Random::base58()` but has been modified to provide the largest value that can safely be used in URLs without needing to take extra characters into consideration because it is [A-Za-z0-9].

```php
$random = new \Phalcon\Security\Random();

echo $random->base62(); // z0RkwHfh8ErDM1xw
```

@see \Phalcon\Security\Random:base58 @throws Exception If secure random number generator is not available or unexpected partial read

```php
public function base64( int $len = null ): string;
```

Generates a random base64 string

If $len is not specified, 16 is assumed. It may be larger in future. The length of the result string is usually greater of $len. Size formula: 4($len / 3) rounded up to a multiple of 4.

```php
$random = new \Phalcon\Security\Random();

echo $random->base64(12); // 3rcq39QzGK9fUqh8
```

@throws Exception If secure random number generator is not available or unexpected partial read

```php
public function base64Safe( int $len = null, bool $padding = bool ): string;
```

Generates a random URL-safe base64 string

If $len is not specified, 16 is assumed. It may be larger in future. The length of the result string is usually greater of $len.

By default, padding is not generated because "=" may be used as a URL delimiter. The result may contain A-Z, a-z, 0-9, "-" and "_". "=" is also used if $padding is true. See RFC 3548 for the definition of URL-safe base64.

```php
$random = new \Phalcon\Security\Random();

echo $random->base64Safe(); // GD8JojhzSTrqX7Q8J6uug
```

@link https://www.ietf.org/rfc/rfc3548.txt @throws Exception If secure random number generator is not available or unexpected partial read

```php
public function bytes( int $len = int ): string;
```

Generates a random binary string

The `Random::bytes` method returns a string and accepts as input an int representing the length in bytes to be returned.

If $len is not specified, 16 is assumed. It may be larger in future. The result may contain any byte: "x00" - "xFF".

```php
$random = new \Phalcon\Security\Random();

$bytes = $random->bytes();
var_dump(bin2hex($bytes));
// Possible output: string(32) "00f6c04b144b41fad6a59111c126e1ee"
```

@throws Exception If secure random number generator is not available or unexpected partial read

```php
public function hex( int $len = null ): string;
```

Generates a random hex string

If $len is not specified, 16 is assumed. It may be larger in future. The length of the result string is usually greater of $len.

```php
$random = new \Phalcon\Security\Random();

echo $random->hex(10); // a29f470508d5ccb8e289
```

@throws Exception If secure random number generator is not available or unexpected partial read

```php
public function number( int $len ): int;
```

Generates a random number between 0 and $len

Returns an integer: 0 <= result <= $len.

```php
$random = new \Phalcon\Security\Random();

echo $random->number(16); // 8
```

@throws Exception If secure random number generator is not available, unexpected partial read or $len <= 0

```php
public function uuid(): string;
```

Generates a v4 random UUID (Universally Unique IDentifier)

The version 4 UUID is purely random (except the version). It doesn't contain meaningful information such as MAC address, time, etc. See RFC 4122 for details of UUID.

This algorithm sets the version number (4 bits) as well as two reserved bits. All other bits (the remaining 122 bits) are set using a random or pseudorandom data source. Version 4 UUIDs have the form xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx where x is any hexadecimal digit and y is one of 8, 9, A, or B (e.g., f47ac10b-58cc-4372-a567-0e02b2c3d479).

```php
$random = new \Phalcon\Security\Random();

echo $random->uuid(); // 1378c906-64bb-4f81-a8d6-4ae1bfcdec22
```

@link https://www.ietf.org/rfc/rfc4122.txt @throws Exception If secure random number generator is not available or unexpected partial read

```php
protected function base( string $alphabet, int $base, mixed $n = null ): string;
```

Generates a random string based on the number ($base) of characters ($alphabet).

If $n is not specified, 16 is assumed. It may be larger in future.

@throws Exception If secure random number generator is not available or unexpected partial read
