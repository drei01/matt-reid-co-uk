# Extending @Value classes with Lombok

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

Error `cannot extend final class`.


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

Use `@AllArgsConstructor` and `private final` to mimic the behaviour of `@Value`. Intellij will autocomplete the constructor for you so you don't have to type it by hand. If you add/remove a field, just delete the constructor and generate it again.