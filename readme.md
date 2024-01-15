# Maitrise du versionning

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
