Par Thomas SAZERAT
# Définition
Comme vu dans [[La gestion de la mémoire en C]], il existe deux catégories de variable.
Les variable qui contiennent directement une valeur : 
```c
int age = 24; // Cette variable contient directement la valeur 24
```
Et les pointeurs : 
```c
int* agePtr = &age; // Pointe vers la variable age, qui contient la valeur 24
```

Nous allons voir dans ce chapitre la notion de passage par valeur et par référence, qui exploite les variables classiques et les pointeurs. Vous verrez qu'une fois comprise ces notions vous servirons non seulement en C, mais aussi en Java, C# et tout autre langage de plus haut niveau.

# Passage par valeur/copie
Pour illustrer le passage par valeur et référence, je vais utiliser une fonction simple, la fonction carré :
```c
int square(int number) {
	return number * number;
}
```

On vas ensuite utiliser cette fonction dans ce programme :

```c
int main() {
	int myNumber = 2;
	
	int result = square(myNumber);
	
	printf("%d*%d=%d\n", myNumber, myNumber, result);

	return 0;
}
```

## Exercice
Dessinez la pile de l'exemple de code. Que constatez vous au niveau de la variable `myNumber` ?
Si vous recopiez et compiler le code (oubliez pas `stdio.h`) qu'est-ce qui est affiché dans la console ? Pourquoi ?
# Passage par référence
Pour ce passage, je dois changer un peu la fonction ``square``:
```c
void square(int* number) {
	*number *= *number; // l'opérateur *= fait la multiplication est l'attribution en même temps
}
```
La fonction ne retourne plus rien. Elle utilise un pointeur en paramètre qui contient le nombre à mettre au carré qui sera donc modifié puisque l'on modifie la valeur derrière le pointeur.

Ensuite, on l'utilise comme suit, mais j'ai volontairement laisser un bug :
```c
int main() {
	int myNumber = 2;
	
	square(&myNumber);
	
	printf("%d*%d=%d\n", myNumber, myNumber, myNumber);

	return 0;
}
```
## Exercice
Dessinez la pile de l'exemple de code. Voyez-vous d'où vient le bug ?

---
# Quand choisir un passage par copie ? Par référence ?
L'avantage du passage par valeur est qu'il est simple. Cependant, il fait **une copie** de la variable, il est donc gourmant en mémoire RAM !
Le passage par référence lui est plus complexe, mais **ne fait pas de copie** de valeur en mémoire.

On utilise donc souvent le passage par copie pour les types simple (``int, char, float``, etc.), tandis que l'on utilise souvent le passage par référence pour les types complexes, comme les structures par exemple.

Maintenant que vous savez ça, repensez à Java. Quand je modifie un entier, comme dans cette exemple :

```java
public static int square(int number) {
	return number * number;
}

public static void main(String[] args) {
	int myNumber = 0;
	
	int result = square(myNumber);
	
	System.out.println(result);
}
```
Ici, le nombre ``myNumber`` n'est pas modifier, car Java (et les autres langages plus haut niveau) copie automatiquement les types simples.
Cependant, si on avait un objet, il serait modifié :
```java
public class Number {
    private int value;

    public Number(int value) {
        this.value = value;
    }

    public int getValue() {
        return value;
    }

    public void setValue(int value) {
        this.value = value;
    }
}

public class Main {
    public static void square(Number number) {
        number.setValue(number.getValue() * number.getValue());
    }

    public static void main(String[] args) {
        Number myNumber = new Number(2);
        System.out.println("Avant : " + myNumber.getValue()); // Affiche 2
        square(myNumber);
        System.out.println("Après : " + myNumber.getValue()); // Affiche 4
    }
}
```
