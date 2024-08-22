+++
title = 'Mon Deuxième Article'
date = 2024-07-22T10:47:26+02:00
categories = ["Sport", "Politique"]
tags = ["Football", "Législatives"]
+++

## Instructions et installations

**Source du tutoriel** : [ici](https://www.youtube.com/watch?v=zrmeOu8DYyw)

[Hugo](https://gohugo.io/) est un **générateur de sites statiques**. Vous allez pouvoir construire rapidement, et simplement, un site web rapide, sécurisé, et sans coût d’hébergement. Les sites statiques permettent de déployer très simplement des pages HTML en partant de **fichiers en** [**Markdown**](https://fr.wikipedia.org/wiki/Markdown). Comprendre et maîtriser les générateurs de sites statiques, c’est aller à l’essentiel : se concentrer sur les contenus que l’on affiche en ligne, prendre en main une interface qui ne se transforme en « usine à gaz » et qui est moins sensible aux problèmes de sécurité (par exemple, les lourdeurs et failles d’un WordPress).

Pour installer Hugo, nous passons par [**Chocolatey**](https://chocolatey.org/install) sur Windows. Dans votre invite de commande, tapez : 


```
choco install hugo-extended
```


Assurez-vous également d’installer « **Go** » en suivant les instructions : [ici](https://go.dev/dl/)

Dans ce tutoriel nous travaillons avec [Visual Studio Code](https://code.visualstudio.com/), notamment pour faciliter le déploiement des fichiers sur Github.

***
## Création du site et ajout d'un thème

Vous pouvez dorénavant **travailler avec Hugo sur votre machine** pour créer votre premier site web.

-        Créez un dossier sur votre bureau (« MyBlog ») puis cliquez sur la barre de chemin d'accès aux fichiers, supprimez tout puis tapez « cmd ». Cela ouvre l'invite de commande qui va pouvoir travailler dans le bon répertoire de fichiers. Vous pouvez également ouvrir le dossier dans Visual Studio Code puis accéder au terminal ;

-        On tape cette commande pour créer le site : 


```
hugo new site MyBlog2 --format yaml
```


-        Une deuxième commande pour **travailler dans le bon répertoire** que vous venez de créer : 


```
cd MyBlog2
```


-        **On initialise le dépôt git** (important pour plus tard) : 


```
git init
```


-        Nous allons **importer un des nombreux** [**thèmes d’Hugo**](https://themes.gohugo.io/), en l’occurrence [PaperMod](https://github.com/adityatelange/hugo-PaperMod). Il faut toujours consulter la page GitHub du thème que vous souhaitez installer, et notamment la documentation. Les méthodes d’installation se ressemblent mais il y a souvent des particularités à bien comprendre (et à bien paramétrer). Plusieurs commandes à entrer successivement dans votre CMD pour installer le thème et le mettre à jour :


```
git submodule add --depth=1 https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod

git submodule update --init –recursive

git submodule update --remote --merge
```


-        Vous constatez que vous avez dorénavant les fichiers du thème dans le dossier MyBlog\MyBlog2\themes. Ouvrez le fichier « hugo.yaml » à la racine du dossier avec votre éditeur (par exemple, Visual Studio Code) et ajoutez cette ligne à la suite : 


```
theme: "PaperMod"
```


-        Nous allons maintenant **lancer un serveur virtuel** pour visualiser notre site web, tapez :


```
hugo server
```


-        Si tout fonctionne bien, en ouvrant [http://localhost:1313/](http://localhost:1313/), vous pouvez visualiser votre site (vide) dans votre navigateur. Vous pouvez ensuite arrêter le serveur en tapant Ctrl+c dans l’invite de commande.

## Paramétrage et création d'articles

Vous avez un site et un thème, sur votre machine, que vous aurez le loisir de déployer en ligne par la suite. Nous allons voir maintenant **comment créer et gérer les contenus** de vos articles :

-        Nous allons **créer un fichier en Markdown** (.md) qui sera stocké dans le dossier « content » et le sous-dossier « posts » : 


```
hugo new content content/posts/mon-premier-article.md
```


-        Ouvrez le fichier avec votre éditeur et constatez que vous avez **des métadonnées dans votre en-tête _front matter_ TOML**. Vous avez le titre de l’article, la date de publication, le statut du brouillon (_true_). Retenez qu’il y a une **gestion des brouillons avec Hugo**. Si vous déployez votre site (hugo server) et que votre article est un brouillon, il ne sera pas visible. Pour l’afficher, vous devez ajouter « draft=false » ou effacer la ligne. Vous pouvez ajouter des contenus pour votre article après la deuxième ligne « _+++ »._ Par exemple, pour travailler rapidement, plusieurs paragraphes [Lorem Ipsum](https://fr.lipsum.com/).

-        Déployez le serveur (hugo server) et constatez que votre article s’affiche bien ([http://localhost:1313/](http://localhost:1313/)). N’oubliez pas de l’arrêter ensuite, comme déjà indiqué plus haut (Ctrl+C).

-        Nous allons ajouter également quelques pages à notre site : une page pour les catégories d'articles, une page pour accéder aux articles en passant par les mots-clés, une page pour les archives des articles. Accédez à votre fichier de configuration à la racine (hugo.yaml) et indiquez ceci pour construire le menu :


```
menu:

      main:

        - name: Catégories

          url: categories

          weight: 10

        - name: Mots-clés

          url: tags

          weight: 20

        - name: Archives

          url: archives

          weight: 30
```

          

Dans cet exemple, « weight » permet de hiérarchiser le menu.

-        Ensuite, les pages s’affichent sur vote site mais elles sont vides. D’emblée pour les catégories et les tags, cela se configure dans le _front matter_ des articles que vous postez. Voici ce que vous pouvez indiquer par exemple :


```
categories = ["Sport", "Politique"]
tags = ["Football", "Législatives"]
```


Vous constatez que les mots-clés apparaissent en bas de vos articles. Idem vous pouvez dorénavant naviguer dans vos articles en passant par les pages « Catégories » et « Mots-clés ».

-        Nous allons maintenant construire la page d’archives : dans Visual Studio Code, créez un fichier « archives.md » sous le dossier « content ». Dans ce fichier, copiez et collez ces informations :


```
---

title: "Archives"

layout: "archives"

url: "/archives/"

summary: archives

---
```


La page n’est plus vide dans votre site et elle affiche automatiquement les archives de vos articles.

-        Nous ajoutons également une fonctionnalité de « Recherche » sur le site pour encore une fois faciliter son usage. Retournez sur le fichier de configuration (hugo. yaml) puis indiquez ceci :


```
outputs:

 home:

   - HTML

   - RSS

   - JSON # necessary for search
```


Dans Visual Studio Code, créez un fichier « search.md » sous le dossier « content » puis utilisez ces informations :


```
---

title: "Rechercher" # in any language you want

layout: "search" # necessary for search

# url: "/archive"

# description: "Description for Search"

summary: "search"

placeholder: "Votre recherche..."

---
```


Enfin, ajoutez la page au menu de votre site web dans le fichier « hugo.yaml » (cf. indications plus haut) :


```
- name: Rechercher

  url: search

  weight: 10
```


La page « Rechercher » est bien visible et fonctionnelle sur votre site web.

-        Pour changer la langue par défaut du site, dans « hugo.yaml », ajoutez :


```
defaultContentLanguage: fr
```


-        Nous allons modifier certains paramètres : ajout d'une estimation du temps de lecture des articles, du nombre de mots, d'un bouton « précédent » et « suivant », d'un fil d'Ariane, de boutons de partage sur certains réseaux sociaux. Pour ce faire, il faut encore une fois modifier « hugo.yaml » et ajouter ceci :


```
-        params:

  ShowReadingTime: true

  ShowShareButtons: true

  ShowPostNavLinks: true

  ShowBreadCrumbs: true

  ShowWordCount: true
```


Actualisez votre site et constatez les changements.

-        Profitez-en pour changer le nom de votre site web dans le fichier « hugo.yaml » :

## GitHub Pages


Vous avez un site Hugo, un thème, un article. Nous allons voir ensuite comment utiliser [**GitHub Pages**](https://pages.github.com/) et les [**GitHub Actions**](https://docs.github.com/fr/actions) pour déployer et héberger votre site en ligne sans payer quoi que ce soit.

-        Connectez-vous sur GitHub et créez un répertoire en lui donnant un nom, en le laissant « Public » et en n’ajoutant ni README ni « .gitignore », ni « license ».

-        GitHub vous propose plusieurs manières de procéder, copiez les commandes après « _…or push an existing repository from the command line_ ». Vous allez les taper dans le terminal, dans Visual Studio Code, successivement :


```
git remote add origin https:[le lien de votre dépôt]

git branch -M main
```


-        Vous pouvez ensuite réaliser dans Visual Studio Code le _git push_ pour transférer vos fichiers vers le dépôt en ligne sur GitHub.

-        Ouvrez ensuite, en ligne, les paramètres de votre dépôt puis cliquez sur « Pages » dans la colonne de gauche. Sous « _Build and deployment_ » puis « _Source_ », sélectionnez « GitHub Actions ».

-        Retournez sur Visual Studio Code et créez, à la racine, un dossier « .github » puis un sous-dossier « workflows » puis, enfin, un fichier « hugo.yaml ».

-        Dans ce fichier, vous allez c/c les contenus que vous pouvez trouver [ici en ligne](https://gist.github.com/thisismikekelly/1a24ad2c8c923127dc3cb29edca13746). Ce fichier va permettre de créer une GitHub Actions qui nous permettra de déployer tout le nécessaire pour construire en ligne notre site Hugo en utilisant les services de GitHub Pages.

-        Retournez sur votre dépôt en ligne et cliquez sur « Actions » dans la barre du haut. Dans la colonne de gauche, un bouton « _Deploy Hugo site to Pages_ » doit être visible. SI c’est le cas, cliquez-dessus puis sur « Run workflow » à deux reprises. Après quelques secondes, la tâche s’ajoute, se construit, se finalise (statut vert).

-        Cliquez sur « Code » et, normalement, vous voyez un « _github-pages_ » visible dans la colonne de droite sous « _Deployments_ ». Cliquez pour afficher l’URL de votre site désormais visible en ligne et à jour.

***

Construction d’une page pour les archives, construction d’une page pour les catégories, construction d’une page pour les tags, modification du tuto en partant du principe que l’on travaille dans Visual Studio Code depuis le début, plusieurs scénarios pour déployer (avec Github Page et Actions, avec Netlify, avec Cursor et Github Page), fonctionnement du front matter dans le détail et notamment l’usage de cover et des images dans assets, mise en page et écriture des articles avec Markdown.