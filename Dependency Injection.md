---
title: Dependency Injection
permalink: /dependency-injection
---

# Dependency Injection

## Overview

`autoconfigure`: when set to true, symfony would automatically add tags to service definitions when the class extends predefined class or implement interfaces (i.e. `EventSubscriberInterface`, `TwigExtensionInterface`)

**![careful][careful] `autowire` and `autoconfigure` settings are only applied on the current file**

In parameters values `@` and `%` needs to be escaped by doubling the character. 

**In XML you don't need to escape `@` in parameters value**

**![careful][careful] Parameters can be set only before container is compiled, you can not set value at runtime**

Using PHP constant for parameter value:

```yaml
foo: !php/const MyClass::FOO
```

in XML:

```xml
<parameter key="foo" type="constant">GLOBAL</parameter>
```

**![careful][careful] Parameters in XML are not trimmed do not do this**

```xml
<parameter key="foo" type="string">
    foo
</parameter>
```

You should write it like this:


```xml
<parameter key="foo" type="string">foo</parameter>
```

`null`, `true` and `false` are converted when using XML configuration. In Yaml the format support this values natively.

## Tags

If you want the `autoconfigure` feature to add a tag on your custom interface.

```php
$container->registerForAutoconfiguration(CustomInterface::class)
    ->addTag('app.custom_tag');
```

**![careful][careful] When using tag arguments need to double loop in the compiler pass because a service can have multiple time the same tag with different arguments.**

## Factory 

you can define a service with a factory method using the new syntax

```yaml
App\Email\Foo:
  factory: 'App\Email\FooFactory:method'
```

old syntax

```yaml
App\Email\Foo:
  factory: ['App\Email\FooFactory', method]
```

## Compiler pass

How to add a custom pass in the `kernel` class add `build` method 

```php
public function build(ContainerInterface $container)
{
    $container->addCompilerPass(new CustomPass());
}
```

You can make the kernel implement the `CompilerPassInterface`. This interface define a `process` method that allow to manipulate the container.

## Autowiring

It is possible to use the autowiring on any method by adding the `required` PHP doc annotation to the method.

```php
/**
 * @required
 **/
 public function iAmAutoWired(FooInterface $foo)
 {
 
 }
 ```
 
 All controllers methods are automatically autowired. This is a convenience to improved developer experience DX.
 
 
[careful]: https://img.icons8.com/office/16/000000/warning-shield.png

**![careful][careful]Public bundles must not use autowiring and define theirs services manually**

**![careful][careful]Autowiring has no performances penalities on production and a small overhead on development**