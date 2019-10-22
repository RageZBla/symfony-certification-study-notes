---
title: Symfony Architecture
permalink: /symfony-architecture
---

# Symfony Architecture

## Deprecations

[link](https://symfony.com/doc/4.0/contributing/code/conventions.html#deprecations)

When deprecating a whole class the `trigger_error()` call should be placed between the namespace and the use declarations

```php
namespace Symfony\Component\ExpressionLanguage\ParserCache;

@trigger_error('The '.__NAMESPACE__.'\ArrayParserCache class is deprecated since version 3.2 and will be removed in 4.0. Use the Symfony\Component\Cache\Adapter\ArrayAdapter class instead.', E_USER_DEPRECATED);

use Symfony\Component\ExpressionLanguage\ParsedExpression;

/**
 * @author Adrien Brault <adrien.brault@gmail.com>
 *
 * @deprecated ArrayParserCache class is deprecated since version 3.2 and will be removed in 4.0. Use the Symfony\Component\Cache\Adapter\ArrayAdapter class instead.
 */
class ArrayParserCache implements ParserCacheInterface

```

## Our Backward Compatibility Promise

**![careful][careful] [Symfony use Semantic Versioning](https://semver.org/)**


In short, Semantic Versioning means that only major releases (such as 2.0, 3.0 etc.) are allowed to break backward compatibility. Minor releases (such as 2.5, 2.6 etc.) may introduce new features, but must do so without breaking the existing API of that release branch (2.x in the previous example).

**![careful][careful] All interfaces shipped with Symfony can be used in type hints. You can also call any of the methods that they declare.**

## The Release Process

Symfony manages its releases through a _time-based model_ and follows the [Semantic Versioning](https://semver.org/) strategy:

*   A new Symfony minor version (e.g. 2.8, 3.2, 4.1) comes out every _six months_: one in _May_ and one in _November_;
*   A new Symfony major version (e.g., 3.0, 4.0) comes out every _two years_ and it's released at the same time of the last minor version of the previous major version.

Each Symfony version is maintained for a fixed period of time, depending on the type of the release. This maintenance is divided into:

*   _Bug fixes and security fixes_: During this period, all issues can be fixed. The end of this period is referenced as being the _end of maintenance_ of a release.
*   _Security fixes only_: During this period, only security related issues can be fixed. The end of this period is referenced as being the _end of life_ of a release.

[careful]: https://img.icons8.com/office/16/000000/warning-shield.png