Par Thomas SAZERAT
# Les Bases de la Mémoire en C : Pile, Tas, Variables et Pointeurs

## 1. Les Variables

Une variable est un conteneur qui stocke une information en mémoire. Elle peut être décrite comme un **quadruple** composé de :

| Élément             | Description                                                              | Exemple (en C)         |
| ------------------- | ------------------------------------------------------------------------ | ---------------------- |
| **Type**            | Définit le genre de données stockées (entier, texte, etc.).              | `int`, `float`, `char` |
| **Nom**             | L’identifiant que vous donnez pour accéder à la variable.                | `a`, `age`, `resultat` |
| **Valeur**          | La donnée actuelle stockée (peut changer si ce n’est pas une constante). | `0`, `3.14`, `'A'`     |
| **Adresse mémoire** | L’emplacement physique dans la RAM (sous forme d’un nombre hexadécimal). | `0x7ffd42a1b3ac`       |

### Analogie
Imaginez la RAM comme une rue avec des maisons :
- Chaque maison a une **adresse unique** (ex: `0x1000`).
- Chaque maison contient une **valeur** (ex: `0`, `42`).
- Le **nom de la variable** (`a`) est comme une étiquette sur la boîte aux lettres.

### Exemple en C

```c
int a = 0; // Type: int, Nom: a, Valeur: 0, Adresse: 0x7ffd42a1b3ac
```

---

## 2. La Pile (Stack)

### Définition
La pile est une zone mémoire **gérée automatiquement** par le programme. Elle est liée à l’exécution des fonctions.

### Fonctionnement
- **Allocation automatique** : Les variables locales sont placées sur la pile.
- **Libération automatique** : À la fin de la fonction, les variables sont supprimées.
- **Stackframe**: Chaque fonction à un espace dans la pile

### Analogie
Une pile d’assiettes :
- On empile les assiettes (variables) les unes sur les autres.
- On ne peut retirer que la dernière ajoutée (principe **LIFO** : *Last In, First Out*).

### Avantages et Limites
- **Avantages** : Rapide et simple à utiliser.
- **Limites** : Taille limitée (risque de *stack overflow*).

### Exemple
```c
void maFonction() {
    int a = 0; // Allouée sur la pile
    int b = 1; // Allouée sur la pile, au-dessus de 'a'
    // À la fin de la fonction, 'a' et 'b' sont automatiquement libérées
}
```

---

## 3. Le Tas (Heap)

### Définition
Le tas est une zone mémoire **gérée manuellement** par le programmeur.

### Fonctionnement
- **Allocation** : Utilisation de `malloc` pour réserver de la mémoire.
- **Libération** : Utilisation de `free` pour libérer la mémoire.

### Analogie
Un tas de vêtements :
- On ajoute ou retire des vêtements (blocs de mémoire) **dans n’importe quel ordre**.

### Exemple
```c
int *ptr = malloc(sizeof(int)); // Alloue un entier sur le tas
if (ptr == NULL) {
    exit(1); // Échec de l'allocation
}
*ptr = 42; // Utilisation de la mémoire allouée
free(ptr); // Libération obligatoire
```

### Risques
- **Fuite mémoire** : Oublier d’appeler `free`.
- **Déréférencement invalide** : Utiliser un pointeur après `free`.

---

## 4. Les Pointeurs

### Définition
Un pointeur est une variable qui stocke **l’adresse mémoire d’une autre variable**.

### Syntaxe
- **Déclaration** : `int *ptr;`
- **Initialisation** : `int *ptr = &a;`

### Opérateurs Clés
| Opérateur | Rôle                               | Exemple         |
| --------- | ---------------------------------- | --------------- |
| `&`       | Récupère l’adresse d’une variable. | `ptr = &a;`     |
| `*`       | Accède à la valeur pointée.        | `int b = *ptr;` |

### Schéma Mental
```
+--------+       +--------+
|  ptr   | ----> |   a    |
+--------+       +--------+
|0x7ffd..|       |   42   |
+--------+       +--------+
```

### Exemple Complet
```c
int main() {
    int a = 42;
    int *ptr = &a;  // ptr pointe vers 'a'
    
    printf("Valeur de a: %d", a);       // Affiche 42
    printf("Adresse de a: %p", ptr);    // Affiche l'adresse
    printf("Valeur pointée: %d", *ptr); // Affiche 42
    
    *ptr = 10;  // Modifie 'a' via le pointeur
    printf("Nouvelle valeur de a: %d", a);  // Affiche 10
    return 0;
}
```

### Lien avec le Tas
Les pointeurs sont souvent utilisés pour manipuler des données allouées dynamiquement sur le tas.

---

## Résumé
| Concept      | Gestion     | Utilisation Typique                      |
| ------------ | ----------- | ---------------------------------------- |
| **Variable** | Automatique | Stockage de données simples.             |
| **Pile**     | Automatique | Variables locales et appels de fonction. |
| **Tas**      | Manuelle    | Données dynamiques et volumineuses.      |
| **Pointeur** | Manuelle    | Référencer des adresses mémoire.         |
