# Prise de note du 15 janvier 2024

## Maitrise du versionning

## Subversion 
SVN = Système de contrôle de version centralisée
Checkout = actions permerttant de récupérer le code 
Commit = opérations local(sans utiliser internet) permettant d'envoyer des modifications du code. 

## Git 

Git = Système de contrôle de version distribué 

# Git en détails 
## Git se charge de gerer de l'intégrité des données. 
Le mecanisme utilise par Git est appelé un empreinte SHA-1. Une chaine de caractères composées de 40 caractères hexadecimaux qui resemble à cela : 

```sh
24b5622b59b59b59b29b54b84bdfdsqdfqds9dsqf8qf29qsf
```
### Git a trois états principaux dans lesquels peuvent se trouver vos fichiers : 

-modifié : permet de modifier les fichiers d'un répertoire
-Indexé : etat intermediaire qui permet de préparer une sauvegarde avec Git. 
-Validé : Aucun changement n'a été detecté 

# La première utilisation de Git 

Git possède un outil appelé Git config qui permet de configurer les paramètres de Git sur votre système. Ces paramètres peuvent être stockés dans trois endroits différents. Le plus important à retenir est celui-ci : 

Fichier config dans le repertoire de Git d'un dépot en cours d'utilisation(c'est à dire .git/config) : Spécifique au seul dépot. Chaque niveau surcharge les valeurs du niveau précédent, donc les valeurs dans .git/config ecrasent celle de /etc/gitconfig.

Pour en savoir plus entrez la commande : 
```sh
git config --list --show-origin
```
Cette commande permet d'afficher tous les  paramètres de configuration Git.

## Configurer votre identité

```sh
git config --global user.name "Balthazar"  
git config --global user.email "mon@email.com"
```
Ces commandes permettent de modifier son nom et le mail de son compte Git.

- Commande de base pour l'utilisation de VIM(editeur de texte).
```sh
i	Passer dans le mode insertion
:q	Quitter
:q!	Quitter sans enregistrer
:w	Enregistrer le fichier
:wq	Enregistrer et quitter
```
## Votre editeur de texte
```sh
git config --global core.editor emacs
```
Cette commande permet de modifier l'éditeur de texte que l'on souhaite utiliser. Sur windows vous êtes obligé de spécifier le chemin complet de l'editeur de texte.

## Le nom de branche par défaut 

```sh
git config --global init.defaultBranch main
```
## Obtenir de l'aide
```sh
git help <commande>
```

## Généreration d'une clé SSH et l'ajouter à l'agent SSH

Ouvrir Git bash.
Entrez cette commande qui permet de générer une clé.
```sh
 ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```
Dans une nouvelle fenêtre PowerShell élevée par l'administrateur , assurez-vous que l'agent ssh est en cours d'exécution. Vous pouvez le démarrer manuellement :
```sh
Get-Service -Name ssh-agent | Set-Service -StartupType Manual
Start-Service ssh-agent
```
Dans une fenêtre de terminal sans autorisations élevées, ajoutez votre clé privée SSH à l'agent ssh. 

```sh
ssh-add c:\Users\YOU\.ssh\id_ed25519
```

git push origin est une commande git qui pousse une ou plusieurs branches locales vers un référentiel distant.
```sh
git push -u origin main
```

### ignore des fichiers 

Pour ignorer des fichiers il suffit de créer un fichier .gitignore et d'y ajouter les fichiers et les dossiers a ignorer.
Le fichier .gitignore agit de façon récursive sur les sous-dossiers.

### Valider des modifications 

```sh
git commit -m 'Message'
```
### Effacer des fichiers 
Pour eliminer un fichier il faut utiliser les commandes suivantes : 
```sh
rm <fichier>
git status 
git rm <fichier>
```
### Creation de tags (ou etiquettes)
En plus d'identifier les commits par des identifiants uniques, Git vous permet aussi d'étiqueter un certain état de l'historique(commit) comme etant important. Cela peut etre utile pour marquer des versions de votre code source. 

```sh
git tag -a v1.0 -m "Version 1.0"    
```

##### Desindexer des elements deja commits

TODO: A completer


# Prise de note du 16 janvier 2024 

## Les branches 

Pour créer une branche il suffit d'utiliser la commande suivante : 
```sh
git branch <NomDeLaBranche>
```

Git branche créer une nouvelle branche mais ne vous fait pas basculer vers cette dernière. 

Pour basculer sur une autre branche on utilise la commande suivante : 

```sh
git checkout <NomDeLaBranche>
```
**Note :** HEAD est considéré comme un pointeur sur le dernier commit de notre branche courante. 

### Fusionner des branches 

Imaginons que nous avons une branche intitulé 'iss53' et 'iss54'.

On va commmencer à travailler sur 'iss53' et effectuer un premier commit: 

```sh
git commit -m "commit 3"
```

Ensuite on rebascule sur la branche master afin d'effectuer un hotfix: 

```sh
git checkout master 
```


```sh
git branch hotfix 
git commit -m "commit -4"
```
Nous sommes satisfait du hotfix et nous allons le valider : 

```sh
git checkout master
git merge hotfix
```
Ici nous avons intégré la branche hotfix à la branche master

La branche hotfix n'a maintenant plus lieu d'être et nous allons la supprimer 

```sh
git branch -d hotfix
```

On va maintenant retoruner sur iss53 et continuer à travailler dessus

```sh
git checkout iss53
```
On effectue un nouveau commit afin de valider notre travaill 

```sh
git commit -m "commit 5"
```

On retourne ensuite sur master et effectuons un merger avec iss53

```sh
git checkout master 
git merge iss53
```
La stratégie de merge est alors différente de celle utilisée précédemment : Merge commit 

Au lieu d'avancer la branche master, Git crée un nouveau commit qui contient les différences entre les deux branches. 

On peut maintenant supprimer la branche iss53:

```sh
git branch -d iss53
```
### Résoudre les conflits 

Un conflit a lieu lorsque deux branches différentes ont modifiées la même partie du même fichier, ou si un fichier à été supprimer dans une branche alors qu'il a été modifié dans une autre. 

Physiquement, un conflit est réprésenté par des caractères spéciaux qui apparaissent dans le fichier. 

Après résolution du conflit il suffit de commit.

# Prise de note du 17 janvier 2024
## (suite résolution de conflit)

Vous avez un outil qui permet de résoudre les conflits avec git : 

```sh
git mergepool
```

Pour afficher toutes les branches : 
```sh
git branch -a
git branch --all
```

Nous allons parler de la commande git fetch : Cette commande permet de synchroniser votre travaux, elle va recherche le serveur qui héberge et va récupérer les modifications qui on étét effectuées sur le serveur distant. 

```sh

```
## Pousser des modifications 

```sh
git push <distant> <branche>
git push origin master
git push -u origin master
```

Pour récupérer les modifications effectuées sur le serveur distant à propos de nouvelles branches ou de branches existantes : 
```sh 
git fetch <distant>
```
Pour récupérer des modifications et les fusionner avec vos branches locales : 
```sh
git pull <distant> <branche>
```
La regle d'or lorsque l'on débute avec Git :
commit -> pull -> push

Lorsque vous récupérez des branches distantes avec la commande fetch, vous ne créer pas automatiquement une branche local qui suit la branche distante. Vous devez créer une branche locale et la lier à la branche distante. 

```sh
git checkout -b <nom-de-branche> <distant>/<nom-de-branche>
branch <nom-de-branche> set up to track remote branch <nom-de-branche> from <distant>.ah
```

On a un raccourci pour cette commande : 

```sh
git checkout --track <distant>/<nom-de-branche>
```
Il y a meme encore plus court, si la branche locale n'existe pas encore :

```sh
git checkout <nom-de-branche>
```
```sh
git branch -vv 
```
Analysons la commande suivante :
```sh
git push origin --delete une-branche
```
## Rebaser votre travail 

**HISTORIQUE LINEAIRE**

Avec git il y a deux manières d'intégrer les modifications d'une branche dans une autre :
- La fusion (merge)
- Le rebasage (rebase)

Fusion:
Lorsque l'on merge on se place dans la branche où on veut faire la modification.

Avec le rebase on aurait entré les commandes suivantes : 

```sh
git checkout experiment
git rebase master 
```
Attention :La commande rebase supprime une partie des commits. 

Quand on rebase on possède un historique divergent qui se transforme en historique linéaire. 

La commande qui correspond au rebase cité en cours :

```sh
git rebase --onto master server client
```
Essaye d'extraire la branche client de la brancher server et de la rebaser sur la branche master. 

```sh
git checkout master
git merge client
```
On peut aussi rebaser la brancher server sur la branche master :

 ```sh
 git rebase master server 
 ```

 Vous pouvez ensuite merge server dans master : 

 ```sh
 git checkout master
 git merge server
 ```
### Important
Rebase or not Rebase ? 

La seule règle à respecter avec la commande rebase : ne jamais rebase des modifications qui ont été publiées sur un serveur distant(push).

Questions exams : 
Que se passe t'il si on rebase des commits qui ont déjà été push ? 

 Si vous poussez des commits quelque part, que d’autres les tirent et se basent dessus pour travailler, et qu’après coup, vous réécrivez ces commits à l’aide de git rebase et les poussez à nouveau, vos collaborateurs devront re-fusionner leur travail et les choses peuvent rapidement devenir très désordonnées quand vous essaierez de tirer leur travail dans votre dépôt.