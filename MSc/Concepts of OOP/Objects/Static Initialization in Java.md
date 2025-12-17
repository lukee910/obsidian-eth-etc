```Java
public Other {
	static int number = 0;
	static {
		// Happens while Super is running
	}
}

public Super {
	static {
		// Happens first
		// Other initializer triggered here, lazily:
		Other.number++;
	}
}

public Sub extends Super {
	static {
		// Happens last
	}
}
```

- Super classes are initialized first
- Unrelated classes are initialized lazily
	- When first accessed
