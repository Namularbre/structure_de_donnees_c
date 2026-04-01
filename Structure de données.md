Par Thomas SAZERAT

# Les structures en C, c'est quoi ?
Une structure est un type composite qui regroupe plusieurs variables sous un même nom.

En C, la syntaxe d'une variable ressemble à ça :

```c
typedef struct {
	int age;
	char* name;
} Person;

// Exemple d'utilisation
int main() {
	Person bob = {"Bob", 24};
	Person alice = {"Alice", 18};
	
	printf("%s %d\n", bob.name, bob.age);
	printf("%s %d\n", alice.name, alice.age);
	
	return 0;
}
```

Décortiquons un peu ces instructions.
`typedef` sert à définir un type à la manière d'un alias. Cela permet de dire que la structure `MyStruct` est un type à C.

Sans `typedef`, le code serais moins lisible :
```c
struct Person {
	char name[100];
	int age;
};

int main() {
	// on doit répéter struct à chaque fois qu'on définit une variable Person !
	struct Person bob = {"Bob", 24};
	struct Person alice = {"Alice", 18};

	printf("%s %d\n", bob.name, bob.age);
	printf("%s %d\n", alice.name, alice.age);

	return 0;
}
```

Les instructions `struct {[...]};` définissent le contenue de la structure en regroupant les variables que vous placerez entre les deux crochets. *Notez qu'il y a un `;` à la fin de la définition d'une structure !*

Pour finir, `Person` est le nom de la structure, ce qui permet de savoir ce qu'elle représente. Ici, on a donc une personne avec un nom et un âge.
# Exercice 1
## Enoncé
Le BDE vous demande de faire une application qui permettra d'afficher les **Sandwich** à la cafétaria. Un **Sandwich** à plusieurs **Ingrédients** qui sont définis par un **nom** et un **prix** (je rappel qu'un prix est un réel). Pour finir, un **Sandwich** à un nom et le prix d'une baguette est 1.00€.

 Voici la liste des ingrédients, je ne vous demande pas de les lires depuis un fichier, on se contentera de tout coder en dur pour le moment.
 ```mermaid
 flowchart
	 A([Salade,0.20€])
	 B([Tomate,0.50€])
	 C([Poulet,1.20€])
	 D([Jambon,1.50€])
	 E([Mayonnaise,0.10€])
 ```
 Idem, pour la liste des sandwichs :

| Jambon Crudité | Poulet & friends |
| -------------- | ---------------- |
| Salade         | Poulet           |
| Tomate         | Mayonnaise       |
| Jambon         | Salade           |

 On vous demande donc :
 - De faire la structure qui représente un ingrédient
 - De faire la structure qui représente un sandwich

# Manipuler une structure
Maintenant que vous savez déclarer une structure, il est temps de voir comment on les manipules.
## Accès au champ
Contrairement à Java, C# ou Rust, l'accès aux champs d'une structure ne se fait pas via un point `myStruct.myField` mais via une flèche `myStruct->myField`.

Il n'y a pas d'encapsulation (=`private, protected, public` en Java) en C, vous pouvez donc accéder directement aux valeurs.

## Simuler de l'orienté objet avec des fonctions
En C il n'y a pas de programmation objet. Les structures ne sont pas à proprement parler des classes, comme en C++, Java ou C#. Or, l'orienté objet permet d'avoir un code souvent plus lisible, plus simple et sans redondance. Nous allons voir comment on peut simuler cela en C.

Les structures n'ont pas de méthode, mais on peut écrire des fonctions qui prennent des structures en paramètre :

```c
#include <stdbool.h> // c n'a pas de booléen par défaut, il faut importer cette lib

typedef struct {
	char* name;
	int age;
} Person;

bool isAdult(Person *person) {
	return person->age > 17;
}

int main() {
	Person bob = {"bob", 24};

	printf("%v", isAdult(bob));

	return 0;
}
```
C'est l'équivalent exacte de ce code en Java :
```java
public class Person {
	private String name;
	private int age;
	
	public Person(String name, int age) {
		this.name = name;
		this.age = age;
	}
	
	public boolean isAdult() {
		return this.age > 17;
	}
}

public static void main(String[] args) {
	Person bob = new Person("Bob", 24);
	
	System.out.println(bob.isAdult());
}
```
On ne le vois pas, mais Java ajoute automatiquement `this` dans les paramètres de chaque méthode, qui est l'équivalent du `Person *person` dans la fonction en C.



