# rappel sur les pointeurs
Dans l'exemple qui suit les variables du programme main ne sont pas modifiés dans ce scop:

``` C

short calcul(short a, short b)
{

    a *= 10;
    b += 1;

    return a+b;

}

int main()
{
    short a = 1, b = 3;

    short c = calcul(a,b);

    printf("a: %d", a); // affichera 1
    printf("b: %d", b); // affichera 3
}
``` 
Cependant, si on utilise les pointeurs on peut facilement modifier les valeurs a et b du programme main:

- * déférencement, valeur
- & référencement, adresse mémoire

``` C
// pointeur des valeurs *a et *b (récupération des valeurs de a et b)
short calcul(short *a, short *b)
{

    *a *= 10;
    *b += 1;

    return *a + *b;

}

int main()
{
    short a = 1, b = 3;

    short c = calcul(&a,&b); // on passe les adresses des valeurs a et b

    printf("a: %d", a); // affichera 10
    printf("b: %d", b); // affichera 4
}
``` 

# Tableau

- définition d'un tableau

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
	int tab[2], i;

    tab[0] = 1;
    tab[1] = 2;
    int tab2[4] = {11,22,33,44};

    printf("%d\n", tab); // address pointer
    printf("%d\n", *tab); // value
    printf("%d\n", *(tab+1)); // second value

    for(i=0;i<2;i++)
    {
        printf("tab: %d\n", *(tab+i)); // move pointer one pos
        printf("tab: %d\n", tab[i]);
        printf("tab2: %d\n", *(tab2+i));
    }

}

```

- définir une fonction pour afficher des données d'un tableau

Il faut passer un pointeur ou un tableau voir les deux définitions valides d'une telle fonction ci-dessous:

```c
void show(int *tab, int max)
{
    int i;

    for(i=0;i<max;i++)
    {
        printf("tab: %d\n", tab[i]);
        //printf("tab: %d\n", *(tab+i)); // equivalent
    }

}

void show2(int tab[], int max)
{
    int i;

    for(i=0;i<max;i++)
    {
        printf("tab: %d\n", tab[i]);
        //printf("tab: %d\n", *(tab+i)); // equivalent
    } 

}

```

# chaînes de caractères

- une chaîne de caractères se termine impérativement par un \0, donc "hello" s'enregistrera h,e,l,l,o,\0

si le caractère de fin de ligne est oublié, c'est source de bug en C. Il a l'avantage de déterminer la fin d'une chaîne, pratique pour le parcours d'une chaîne de caractères.

``` c
char str[6];
str[0]='h';
str[1]='e';
str[2]='l';
str[3]='l';
str[4]='o';
str[5]='\0';
```

- ci-dessous deux manières de parcourir la chaîne str

``` c
void main()
{
	int i;
	char str[] ="Hello";

	for(i=0;i<6;i++)
	{
	    printf("%c", *(str+i));

	}

	printf("%s", str);

}

```
- création d'une fonction qui compte le nombre de caractères dans une chaîne.
On passe un pointeur et une const ce qui permet de s'assurer que la chaîne ne sera pas modifier par la fonction elle-même.

```
int string_length(const char* str)
{
    int i = 0, cpt = 0;

    while(*(str+i) != '\0'){
        i++;
    }

    return i;

}

// application

char *str="arduino";
// equivalent def tab
// char str[] = "arduino"; // C add \0 automatic

printf("%d", string_length(str)); // 7

```

## particularité des chaînes de caractères
La déclaration suivante définie une chaîne de caractères en lecture seule

``` C
char * foo;

// impossible de faire cela, déclenche une erreur de segmentation
foo[0] = 'b';

```
Pour éviter ce genre de problème, il faut définir les chaînes de caractères en constante, dans ce cas c'est à la compilation que ça plante et donc c'est plus facile à corriger.
``` C
const char * foo;

// ça plante à la compilation
foo[0] = 'b';

```