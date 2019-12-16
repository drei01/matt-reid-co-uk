---
layout: post
title: Extending @Value classes with Lombok
---

I've been using Value objects a lot recently. Especially as I've been [working with DDD](https://www.matt-reid.co.uk/2019/07/24/domain-driven-design-in-reality.html). Lombok provides a [convenient annotation](https://projectlombok.org/features/Value) to avoid writing lots of boilerplate code for Value object classes. The annotation will make the class `final`, add a constructor that takes all the arguments and make each field `private` and `final`.

Consider a model where we have two value objects, Animal and Human.

```java
@Value
class Animal {
	Date birthday;
}

@Value
class Human extends Animal{
	String name;
}
```

If we use `@Value` on both classes, we'll get a compilation error `cannot extend final class`.


## Solution

```java
@AllArgsConstructor
@Getter
class Animal {
	private final Date birthday;
}

@Value
@EqualsAndHashCode(callSuper = true)
class Human extends Animal{
	String name;

	public Human(Date birthday, String name) {
		super(birthday);
		this.name = name;
	}
}
```

Use `@AllArgsConstructor` and `private final` to mimic the behaviour of `@Value`. If you use Intellij, it will autocomplete the constructor for you so you don't have to type it by hand. If you add/remove a field, just delete the constructor and generate it again.
