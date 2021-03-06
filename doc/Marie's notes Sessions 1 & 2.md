#Notes Session 1: intro à Ruby

MRI est un interpreteur ruby. Irb est un interpréteur de Ruby aussi.

Il y a plusieurs implémentations de Ruby. Les plus gros changements de versions sont les versions 1.8.7, 1.9.3 et 2.1.etc. 

Rbenv permet d'installer différentes versions de Ruby (pour pouvoir tester les programmes sur différentes versions). On peut également utiliser Rvm au lieu de Rbenv.

Commande pour installer ruby avec Rbenv: Rbenv install version 2.1.2 

Le gestionnaire de library est: rails
→ Bundler gère les librairies (aussi appelées bibliothèques).

Un bundler = un gem. Toutes les librairies sont des gem (des sortes de plugins). Il faut passer par bundler pour installer les gems.

Commande pour installer Bundler:
sudo gem install bundler 
rbenv install et numéro de version à installer (si un pb de SSL survient, faire : sudo apt-get install libssl-dev)
rbenv global mettre le même numéro de version
rbenv rehash

Pour installer un gem:
bundle install nom du gem

bundle exec → cerveau de gemfile


#Notes Session 2 du 29 juin 2014:

Bundler →  appelle: Ruby Gems → qui installe des gems 

Notes pour Linux: Pour copier, il suffit de sélectionner. Pour coller: cliquer avec la mollette. 

Les méthodes

Nil => “vide”. Exemple: nil.nil?
				Le point signifie: “est-ce que c'est” ? 
				Ici: est-ce que nil est vide?
 

toto → Récupère une valeur
toto= → Défini une valeur
toto? → Méthode test (retourne soit TRUE soit FALSE)
toto! → Méthode qui va modifier l'état de l'objet (à utiliser avec précaution)

Un objet → Ensemble de variables et de méthodes. Dans le cadre d'un objet, une méthode avec un “!” modifie l'objet.

Par exemple:

L'objet “Animal” a 4 pattes. 
On a une méthode qui s'appelle “Accident!”. On l'appelle. Dans cette méthode, il est défini qu'il faut enlever une patte. Une fois la méthode appelée, l'objet “Animal” va retourner 3 pattes, et non plus 4. Il a été modifié.


Exemples méthodes :

> toto  = 1
=> 1
> toto.nil?
=> false

Pour changer une lettre (mais sans sauvegarder le changement):
> toto= "hello"
=> "hello"
> toto.gsub('o','a')
=> "hella"
> toto
=> "hello"


> toto.gsub!('o','a')
=> "hella"
> toto
=> "hella"

Equivaut à :

> toto = "hello"
=> "hello"
> toto = toto.gsub('o','a')
=> "hella"
> toto
=> "hella"


Les lignes de commandes UNIX

Quand j'ouvre mon terminal, je suis à la racine de mon répertoire personnel. Si je tape ls, j'obtiens la liste de mes documents: en bleu s'affichent les répertoires, et en blanc les fichiers.

Une commande a un corps (ex.: “ls”), puis des paramètres.

Man
Permet d'accèder au manuel de n'importe quelle commande. Pour en sortir, taper “q”. Ce manuel permet de voir les paramètres possibles pour chaque commande.

Ls
Affiche le contenu du fichier.

ls -l
Long-listing format (donne plus d'infos).

.
Correspond au répertoire courant

ex.: ls Desktop → affiche le contenu du desktop.

Pwd
Donne le chemin du répertoire en partant de / (home). 

.. /
Pour naviguer

mkdir
Créé un répertoire

chmod
Permet de changer les droits

touch suivi du nom du fichier à créer
Permet de créer un fichier. Permet également de mettre à jour le timestamp sans venir modifier le contenu du fichier (chaque fichier a une date de création et de modification).

cd..
Permet de remonter d'un niveau.

Mv
“move”. Permet de déplacer et de renommer.
ex.:  mv 	mon-fichier 	dev/
	       |        		 |
 	  fichier à bouger  	destination								

On peut spécifier le chemin absolu ou relatif.
ex.:  mv dev/          fichier2       .
          |                |          |
  Dossier où je		fichier à	  répertoire courant
déplace mon fichier	déplacer	  (là où je me situe)

Pour renommer:
mv mon_fichier fichier2

rm
Permet de supprimer un fichier ou un répertoire.
Rm fichier
rm dir mon_rep ou rm -r mon_rep (si les répertoires sont vides)

Si le répertoire n'est pas vide est refuse d'être supprimé car il contient des fichiers:
rm -rf mon_rep (“f” pour “force”).

Man rm donne les options de suppression.

Echo “du texte”
Affiche du texte dans mon terminal. Il s'affiche sur la sortie standard (appellée stdout).

Le > redirige. Permet d'afficher le contenu de l'echo dans un autre endroit.
ex.: echo “du texte” > mon_fichier
→ “du texte” va s'afficher dans le fichier nomm” “mon_fichier”.

Cat
“Concatenate”. Permet d'afficher le contenu de mon fichier. Cela permet d'éviter que trop de texte défile si c'est un gros fichier. 

Less examples.desktop → affiche le contenu jusqu'à la fin de ma fenêtre uniquement. Dès que “less” est utilisé, on peut effectuer des recherches.

ex.: /size
	/n (“next”)
→ man less
 /size

Créer un lien symbolique (raccourci):
ln -s 
source vers destination.

Ln -s mon_fichier lien_mon_fichier
ls
lien_mon_fichier mon_fichier
      |		     |
couleur bleue du lien  fichier

Comme c'est un lien, ce sera le même fichier avec le même contenu. Cela permet de faire pointer vers la base de données dans un cas d'utilisation d'un outil de versioning qui requêt que la BDD soit placée dans un endroit obligatoirement, alors qu'on souhaite utiliser une autre localisation qui soit plus cohérente pour nous). Cela aide aussi en cas de nouvelles versions.

Head
N'affiche que les 10 premières lignes d'un fichier. Si on veut voir + que les 19 premières lignes: head -n15 → affiche les 15 premières lignes.

Tail
Même chose, mais avec les dernières lignes. Tail -f → rafraîchi régulièrement mon fichier. C'est utile pour surveiller les fichiers de log.

>>
Rajoute dans mon fichier (apend).

Grep
Permet de rechercher du texte dans un fichier.

ex.: grep “tex” dev/mon_fichier → affiche tous les “tex” qui se trouvent dans le fichier. Permet de rechercher dans une arborescence de fichiers.

Grep -r “tex” dev/      (sensible à la casse)
      -r = recursive

Explore tous les fichiers dans la dossier.
Grep -ri → insensible à la casse (indifférent aux majuscules et minuscules)

zgrep → va chercher dans des fichiers compressés
sed → permet de rechercher et remplacer du texte dans un fichier. A une syntaxe particulière:

ex.: sed 's/text/té/g' dev/mon_fichier
	→ Quand tu trouve “text”, remplace-le par “té”.

Sed -i → modifie directement le fichier.

Archivage: tar

Transforme un répertoire en un seul fichier. Prend l'arborescence du dossier pour le transformer en un seul fichier, et le compresse. Tar permet aussi de choisir un algorithme de compression. Pour installer un programme, j'aurai un fichier en .tar.gz par exemple. Ce qui signifie que tar est compressé en gzip.

Tar c
Permet de créer une archive 

tar cvf archive.tar dev/
→ met en un seul fichier ce qu'il y a dans mon dossier.
(créer)

tar tvf archive.tar
(lister)

tar xvf .. / archive.tar
(extraire) permet de décompresser.

Du
“disk usage” Pour voir la taille
du -sh dev (“dev” = nom du répertoire dont on veut voir la taille)
df -h  → Permet de connaître l'utilisation des disques.

Compression avec TAR

tar cvfz archive.tar.gz dev/
       z = gzip: c'est + rapide mais compresse -
il y a j = bzip: compresse + mais – rapide

Faire une boucle en ligne de commande:

for I in 1 2 3 4 5; do echo toto >> fichier1; done
→ permet d'écrire 5 fois toto dans le fichier nommé “fichier1”.

Cp
Permet de copier.




EXO d'entraînement:

Créer un répertoire avec deux fichiers dedans: le premier s'appelle “fichier1” et contient le texte suivant: “toto”, 5 fois.
Copier le fichier1 en fichier2. Remplacer toto par tata.
Créer une archive de ce répertoire “archive.tar.gz”
Renommer archive.tar.gz en archive.tgz
