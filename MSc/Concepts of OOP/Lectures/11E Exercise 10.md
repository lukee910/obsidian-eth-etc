## Task 1
### A
Task: Add the casts the compiler has to add because of type erasure.

Things noted in `[]` are compiler casts after type erasure:
```Java
class Animal {}
class Mammal extends Animal {}
class Tiger extends Mammal {}

class Ship<T extends Animal> {
	public T content;
}

class Cage<T extends Mammal> {
	public T content;
	
	void takeFromShip(Ship<T> other) {
		this.content = [Mammal]other.content; // other.content could be animal, disallow that.
		other.content = null;
	}
}

class Zoo<T extends Mammal> {
	void swapTigers(Ship<T> mammalShip, Cage<Tiger> tigerCage) {
		Tiger tiger = [Tiger]tigerCage.content; // We don't know about the type of tigerCage at runtime, have to cast it to that
		Cage<Tiger> tmpCage = new Cage<Tiger>();
		tmpCage.takeFromShip((Ship<Tiger>) mammalShip);
		mammalShip.content = (T) tiger;
		tigerCage.content = tmpCage.content;
	}
}
```
### B
Task: Do these methods work?
1. No, because there's no generic array type
2. No, because:
	1. `Cage<Animal>` is not valid
	2. `Cage<T>` is not a runtime type
## Task 2
### A
Task: For each snippet, could the subclass method be allowed to override the superclass method in a type-safe language?

Snippets:
1. No, [[Subtyping Generics]] -> invariant
2. No, contravariant arguments
3. Yes, understands strictly more messages
4. Yes, understands all B
5. No, can narrow down with T
6. Yes, can understand any type, is good
7. No, can instantiate it to be `Sub<T>` and then it won't understand the string message
8. No, the sub methods has to have both lists be of the same type
### B
Task: Code snippet for bad examples A.2, A.3, A.6, A.7.
- A.2: `Super s = new Sub(); s.foo(new X<B>);`
- A.7: `Super s = new Sub<Integer>(); s.foo("Migros");`
	- Note: This is considered an overload by Java, this will run and call the `Super` method.
	- Note `Sub<String>` for the same and it will still use the `Super` method, since the `Sub` method isn't really an override of the `Super` method
## Task 3
### A
Note: Need to make it crash with `current` being the desired user. Do this via:
```Java
register(dummyUser);
dummyUser.name = null;

try {
	login(dummyUser); // provoke crash on name equals check
} catch (LoginException e) {
	login(e.problemUser);
}
```

Other solution: Create a new user with the same name as an existing one, wrong login, get the problem user (which is the existing one) and continue as before.
### B
Task: Can you fix it by only modifying:
- `User`
	- Make a copy of user and set password to "" on exception
- `LoginException`
	- Make `problemUser` private
- `registerUser`
	- Make a copy of user, do not leak alias
- `for` loop in `login` method
	- Proper: swap `nameEqual` and `current = registered` line
	- Hacky: Remove `current` from `throw new LoginException`
## Task 4
```c++
spouse->spouse->money = 100;
```
## Task 6
### A
Output: `1 2`
Because everything's a reference.
### B
Output: `1 1`
Because there's no pointers or references manually applied.
### C
Output: `1 2`
Pointers to `A` are copied, but `A` is referenced so it actually applies there.
### D
Output: `1 <SEGFAULT>`
Unique pointer is copied, deallocated.
