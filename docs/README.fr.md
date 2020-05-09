
# ITI 1521 - Lab 00 - Édition, compilation et exécution

## Objectifs d'apprentissage

* **Rappeler** les exigences du cours par rapport à la soumission des devoirs.
* **Découvrir** les divers outils liés au développement de programmes Java.
* **Éditer, compiler** et **exécuter** un programme Java.
* **Exécution de tests junit**
* **Soumission de la solution** dans BrightSpace.

### Soumission

Veuillez lire les [instructions junit](JUNIT.md) pour obtenir
de l'aide avec l'exécution des tests pour ce laboratoire.

Ce laboratoire n'est pas marqué, mais vous donnera de l'expérience
avec un soumission à BrightSpace. Votre _solution_ devrait
implémentez `sayHello()` pour retourner `"Hello World"`.

Si vous choisissez de pratiquer les soumissions, veuillez lire
attentivement les [Directives de soumission](SUBMISSION.fr.md).
Les erreurs de soumission affecteront vos futures notes.

## 1. Revue des directives pour l’écriture de programmes Java

Prenez quelques minutes afin de revoir les règles concernant
l'écriture de programmes Java. Consultez ces règles pour tous
vos travaux pratiques. Jusqu'à 10% de la note des devoirs
dépend du respect de ces règles et de la clarté du code.

* [java.sun.com/docs/codeconv/html/CodeConvTOC.doc.html](http://java.sun.com/docs/codeconv/html/CodeConvTOC.doc.html).
* [www.site.uottawa.ca/~turcotte/teaching/iti-1521/assignments/directives.html](http://www.site.uottawa.ca/%7Eturcotte/teaching/iti-1521/assignments/directives.html)

## 2. Installation de « Java Development Kit »

Si vous utilisez un ordinateur personnel et que vous n’avez
pas encore le JDK, vous allez devoir l’installer.

### Microsft Windows

Pour vérifier si le JDK est présent, ouvrez une fenêtre de
la ligne de commande (recherchez « Command Prompt » ou « cmd »
dans votre « menu démarrer ») et insérez la ligne suivante :

```bash
for %i in (javac.exe) do @echo %~$PATH:i
```

Si vous avez déjà installé le JDK cela devrait vous retourner
le chemin de dossier menant au fichier javac.exe, similaire a
ceci :

```bash
for %i in (javac.exe) do @echo %~$PATH:i
C:\Program Files\Java\jdk1.8.0_111\bin\javac.exe
```
Si vous n'obtenez pas le résultat voulu, allez sur le site d'[Oracle](https://www.oracle.com/technetwork/java/javase/downloads/index.html), sélectionnez le « Java SE Development Kit » le plus récent pour votre système d’exploitation et installez-le. **Notez la destination de l’installation.** Une fois terminé, naviguez jusqu’au fichier d’installation, puis dans le dossier bin. Copier le chemin des dossiers (similaire a « C:\Program Files\Java\jdk1.13.0_111\bin »).

Il faut maintenant ajouter une variable locale.

1.  Dans le « start menu », recherchez « Computer » ou « this PC », appuyez sur le bouton de droite et choisissez « Properties ».
2.  Sélectionnez « Advance system settings ».
3.  Sélectionnez « Environment Variables... ».
4.  Cliquez sur « New... ».
5.  Sur la ligne « Variable name », entrez « PATH ». Sur la ligne « Variable value », insérez le chemin de dossier que vous avez copié plus tôt.
6.  Cliquez sur « OK ».
7.  Vérifiez à nouveau si votre JDK est bien installé par la méthode de la ligne de commande décrite précédemment.

![Étapes d'ajout des variables d'environnement sous windows 10](assets/Lab00_environment_variables.png)
**Figure 1 :** Étapes d'ajout des variables d'environnement sous windows 10.

La vidéo ci-dessous résume le processus décrit dans cette section.

<iframe width="560" height="315" src="https://www.youtube.com/embed/ylpgVCoUK4k" allowfullscreen=""></iframe>

#### Résolution de problèmes communs

##### J’ai déjà une variable PATH, que faire?

C’est normal que vous ayez déjà une variable PATH, cliquez sur
« edit » et ajoutez le chemin du dossier à la fin de la variable.
Assurez-vous que ce soit séparé du reste de la variable par un
point-virgule (;)

##### Je reçois le message « ECHO is on » plutôt que le chemin vers le JDK

La commande « echo » retourne par défaut « ECHO is on », donc cela
indique probablement que vous n’avez pas le JDK d’installé ou que
la variable locale n’a pas bien été créée.

**Trucs généraux :**

* Assurez-vous que le chemin de dossier dans la variable PATH mène au JDK et non au JRE
* Assurez-vous d’avoir une seule version du JDK
* Assurez-vous de commencer une nouvelle instance de la ligne de commande après avoir installé le JDK et la variable locale
* Assurez-vous que la variable locale PATH ne contient qu’une seule référence au JDK

##### Ressources

* [JDK Installation for Microsoft Windows](https://docs.oracle.com/en/java/javase/13/install/installation-jdk-microsoft-windows-platforms.html)

### Mac OS

Pour vérifier si le JDK est présent, ouvrez le terminal
(Applications -> Utilities) et insérez la ligne suivante :

```bash
which javac
```

Si le JDK est installé proprement vous devriez voir un chemin
similaire à ceci :

```bash
/usr/bin/javac
```

Si vous n'obtenez pas le résultat voulu, allez sur le site de
[Oracle](https://www.oracle.com/java/technologies/javase-downloads.html),
sélectionnez le « Java SE Development Kit » le plus récent pour
votre système d’exploitation et installez-le.

Vérifiez à nouveau si votre JDK est bien installé par la
méthode du terminal décrite précédemment.

###### Ressources

* [JDK 13 Installation for OS X](https://docs.oracle.com/en/java/javase/13/install/installation-jdk-macos.html)

## 3. Éditeur de code source

Vous devez faire la distinction entre les concepts suivants :
compilateur, éditeur de code source et machine virtuelle
(Java Virtual Machine — JVM). Les environnements de développement
tels qu'Eclipse et Netbeans regroupent ces éléments à l'aide
d'une interface commune (IDE – «Integrated Development Environment»).
Ceci facilite le développement de programmes informatiques,
mais masque les frontières entre ces concepts.

Un éditeur de code source (éditeur de programme) est un éditeur
de texte conçu expressément pour éditer le code source des
programmes — voir **Figure 2**. Ces logiciels ont généralement
les caractéristiques suivantes :

*   Mise en évidence («highlighting») de la syntaxe du langage. Spécifiquement, les éléments du langage tels que les mots réservés (clés), les paramètres et les chaînes de caractères sont affichés à l'aide de polices et de couleurs distinctes. Ceci facilite la lecture du code et son débogage. Par exemple, si l'on oublie le délimiteur de droite d'une chaîne de caractères, tout le texte qui suit sera affiché de la même couleur que la chaîne (essayez-le).
*   Indentation du code source. L'éditeur de code source comprend un ensemble de règles afin de formater le texte. Ceci facilite la lecture du code et son débogage. Par exemple, l'on omet les parenthèses englobant les énoncés de la clause else, seul le premier énoncé sera indenté vers la droite.
*   Correspondance des accolades (,(),[]). Lorsqu'on positionne le curseur sur une accolade, l'éditeur met en évidence l'accolade correspondante, ce qui encore une fois facile la lecture du code.
*   Auto-complétion des mots clés du langage.

![Édition d’un programme de tri par sélection à l’aide de l’éditeur de code source Notepad++ sous Windows.](assets/Lab00_img1_selection_sort-notepad.png)
**Figure 2 :** Édition d’un programme de tri par sélection à l’aide de l’éditeur de code source Notepad++ sous Windows.

Voici quelques éditeurs de code source populaires.

*   Atom (Mac OS, Windows, Linux, [atom.io](https://atom.io))
*   Sublime Text (Mac OS, Windows, Linux, [http://www.sublimetext.com](http://www.sublimetext.com))
*   Notepad++ (Windows, [http://notepad-plus-plus.org](http://notepad-plus-plus.org))
*   TextWrangler (Mac OS, [http://www.barebones.com/products/textwrangler/](http://www.barebones.com/products/textwrangler/))
*   TextMate (Mac OS, [http://macromates.com](http://macromates.com))
*   Emacs (Mac Os, Windows, Unix/Linux, [https://www.gnu.org/software/emacs/](https://www.gnu.org/software/emacs/))

Utilisez votre éditeur de code source favori afin de créer un simple
programme « Hello World » (Notepad++ est recommandé).
Un programme « Hello World » possède une méthode principale et
celle-ci affiche la chaîne de caractères « Hello World ! ».
Vous nommerez cette classe **HelloWorld**. Copier le code
source de suivant dans votre éditeur de code source et sauvegarder
le contenu dans un fichier sous le nom **HelloWorld.java**.
Enregistrer le fichier dans un dossier nommer « Lab00 » sur
votre bureau (desktop).

```java
1 public class HelloWorld {
2   public static void main(String[] args) {
3     System.out.println("Hello World!");
4   }
5 }
```

Explication du code ligne par ligne:

1.  Déclaration de la classe avec le nom « HelloWorld » en utilisant le mot clé **class**. Le mot clé **public** indique qu’il n’y a pas de restriction sur l’accès de la classe.
2.  Déclaration de la méthode principale **main**. Cette méthode est spéciale: elle est le point de départ de l’application. En paramètre, c’est-à-dire entre parenthèses, la méthode reçoit un tableau de **String** qui est nommé « args » par convention. La méthode **main** doit toujours avoir cette signature.
3.  Utilisation de la classe **System** de la libraire java. La classe System contient la variable « out » qui représente là où seront écrites les sorties du programme. Nous utilisons la méthode println qui permet d’imprimer sur une nouvelle ligne tout **String** qu’elle reçoit en paramètre, soit « Hello World! » dans l'exemple ci-haut.
4.  Fermeture de la méthode **main**.
5.  Fermeture de la classe **HelloWorld**.

## Question 1: Hello World avec les tests

Ré-implémentez HelloWorld en appelant une méthode appelée `sayHello()`
comme indiqué ci-dessous:

```java
public class HelloWorld {

  public String sayHello() {
    // your code here
  }

  public static void main(String[] args) {
    System.out.println(sayHello());
  }
}
```

Veuillez lire les [instructions junit](JUNIT.md) pour obtenir
de l'aide avec l'exécution des tests pour ce laboratoire.


#### 4. Compilation et exécution à partir d'un «shell» de commandes

Ouvrer une fenêtre de commande (command prompt)
(ou le terminal pour Mac). Utiliser la commande **dir** pour
afficher les fichiers et dossiers contenus dans le dossier courant.
Utiliser **cd** pour changer de dossier. Voici un exemple de la
procédure, les commandes sont précéder du signe **>**

```bash
 Directory of C:\Users\Admin

01/02/2017  10:31 PM    >DIR>          .
01/02/2017  10:31 PM    >DIR>          ..
01/04/2017  10:42 AM    >DIR>          Desktop
01/01/2017  08:04 PM    >DIR>          Documents
01/04/2017  09:56 AM    >DIR>          Downloads
               0 File(s)              0 bytes
              3 Dir(s)  361,593,483,264 bytes free

C:\Users\Admin>cd desktop

C:\Users\Admin\Desktop>dir
 Directory of C:\Users\Admin\Desktop

01/04/2017  10:42 AM    >DIR>          .
01/04/2017  10:42 AM    >DIR>          ..
01/04/2017  10:42 AM    >DIR>          Lab00
               0 File(s)         0 bytes
               1 Dir(s)  361,593,556,992 bytes free

C:\Users\Admin\Desktop>cd Lab00

C:\Users\Admin\Desktop\Lab00>dir

 Directory of C:\Users\Admin\Desktop\Lab00

01/04/2017  10:53 AM    >DIR>          .
01/04/2017  10:53 AM    >DIR>          ..
01/04/2017  10:53 AM                 124 HelloWorld.java
               1 File(s)              124 bytes
               2 Dir(s)  361,592,205,312 bytes free
```

Pour les utilisateurs de macOS qui ne sont pas familiers avec les
commandes du Shell, consultez ce tutoriel. Vous devrez évidemment
adapter les commandes ci-dessus pour l'environnement macOS (OS X).

*   [Le Terminal dans OS X](https://openclassrooms.com/courses/domptez-votre-mac-avec-mac-os-x-mavericks/le-terminal-dans-os-x)

Assurez-vous que le répertoire courant soit celui qui contient le fichier **HelloWorld.java**.

Compilez le programme **HelloWorld.java**

```bash
> javac HelloWorld.java
```

Le symbole « > » ne fait pas partie de la commande, c'est
l'incitatif (prompt). S'il y a des erreurs, corrigez-les,
et compilez de nouveau. Lorsque vous aurez réussi à compiler
le programme, vous verrez apparaître dans le répertoire
le fichier **HelloWorld.class**. Le fichier **.class** contient
la représentation en code-octet (byte-code) de votre programme.
Ce sont des instructions semblables à celles de l'assembleur de
l'ordinateur TC 1101 présenté en classe.

Le code-octet est exécuté par un interprète qu'on nomme
**Java Virtual Machine** (JVM). Afin d'exécuter ce programme,
tapez ce qui suit dans la fenêtre de commandes (assurez-vous
que le répertoire courant contient le fichier **HelloWorld.class**).

```java
> java HelloWorld
Hello World!
```

Le résultat de l'énoncé println apparaît sur la sortie (à l'écran). Ici, **java**, c'est la machine Java virtuelle (JVM). La JVM lit le code-octet de votre programme, une instruction à la fois, et exécute les actions nécessaires.

La vidéo ci-dessous résume le processus décrit dans cette section. Assurez-vous de bien comprendre chacune des étapes puisque vous en aurez besoin tout au long de la session.

<iframe width="560" height="315" src="https://www.youtube.com/embed/a9LBSF3IW9s"></iframe>

**Video 1 :** Compilation et exécution d’un programme à partir de la ligne de commande.

<iframe width="560" height="315" src="https://www.youtube.com/embed/xzXYUYFWAU0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen=""></iframe>

**Video 2 :** Compilation et exécution d’un programme à partir de la ligne de commande dans les laboratoires de l'Université.

Afin de bien maîtriser les étapes de compilation et d'exécution, faites volontairement des erreurs dans votre code, essayez de le compiler (avec **javac HelloWorld.java**) et voyez-en le résultat. Nous vous suggérons notamment d'essayer de :

*   Supprimer le point-virgule après le System.out.println("Hello World!")
*   Modifier le nom de la classe sans changer le nom du fichier.
*   Supprimer une des accolades '}' de fermeture.
*   Supprimer une des accolades '{' d'ouverture.
*   Supprimer un des " de l'argument de la méthode println.
*   Imprimer votre âge. ;)

Vous remarquerez rapidement qu'un simple oubli peut causer une multitude d'erreurs. Il est ainsi fortement suggéré de compiler son code régulièrement afin d'éviter que les erreurs s'additionnent et deviennent difficiles à déboguer!

## Ressources

*   [https://openclassrooms.com/courses/apprenez-a-programmer-en-java](https://openclassrooms.com/courses/apprenez-a-programmer-en-java)
*   [Le Terminal dans OS X](https://openclassrooms.com/courses/domptez-votre-mac-avec-mac-os-x-mavericks/le-terminal-dans-os-x)
*   [_Java Platform, Standard Edition Installation Guide_](https://docs.oracle.com/en/java/javase/13/install/index.html)
