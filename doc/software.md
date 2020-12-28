# SOFTWARE:

## Sommaire:

> 1. Description du projet
>    * Objectifs du projets
>    * Langages et technologies utilisés
>    * Objectifs du projet
>    * Langages et technologies utilisés
> 2. Structure du projet
>    * Structure Frontend
>    * Structure Backend
> 3. Interfaces
>    * Ux design
>    * Fonctionnement
> 4. Backend
>    * Traitement des données
>    * Utilisation de l'intelligence artificielle
> 5. Résultats
>    * Exemples de graphiques
>    * Description des graphiques

## Description du projet:

### Objectifs du projet:

Nous avons décidé de choisir la prise de multiples données comme mission secondaire pour notre satellite. De ce fait, il apparait comme besoin la création d'outils pour les analyser. Ces outils seront utilisés au travers d'une application desktop (*pour ordinateur*). L'objectif de cette application est de mettre à disposition des outils de traitement de vidéos, d'images pour l'utilisateur. L'application peut ainsi créer des graphiques, utiliser des technologies comme de l'intelligence artificielle pour traiter et améliorer les images pendant la diffusion de vidéo, etc...
En bref, il s'agit ici de créer une application regroupant de multiples outils qui analysent et traitent les données prises par le satellite.

### Langages et technologies utilisées:

Pour ce projet, nous avons décidé d'utiliser comme langage de programmation le langage **python**. En effet, ce langage présente beaucoup d'avantages pour notre projet. D'abord, les composants hardwares sont des composants de la gamme Raberrypi, une technologie utilisant le langage python pour être programmée. De plus, python présente un large éventail de librairies. Il s'avère également que le langage python est le langage le plus utilisé dans le Big Data, Data Sciences et Intelligence Artificielle (*Python est principalement utilisé dans l'analyse de données en masse*).
Nous allons donc utiliser plusieurs librairies et technologies pour créer nos outils (*voir tableau*):

##### Librairies:


| Noms: | Secteurs: | Objectifs: |
| - | - | - |
| tkinter | Frontend | Créer une inetrace pour l'utilisateur. |
| json | Frontend et Backend | Enregistrer et accéder aux données stockées par l'application: les thèmes, les langues, les options etc... |
| matplotlib | Backend | Créer des graphiques de tous types |

## Structure du projet:

### Structure Frontend:

La partie Frontend (*Apparence*) du script est organisé avec une infrastructure M.V.C. (*Models Views Controllers*):

> /Interface<br/>
> |--/Models<br/>
> |--/Views<br/>
> |--/Controllers<br/>
> |--root.py<br/>

Le fichier ***root*** initialise la fenêtre principale de l'application, le fichier ***/Controllers*** contient les fichiers qui communiqueront à l’application les informations stockées (langues, thèmes, paramètres, etc...), le fichier ***/Models*** contient les fichiers qui retournent des éléments graphiques préconçus (*cela permet de mieux compartimenter le projet et d'accélérer la création des fenêtres*), et le fichier ***/Views*** contient les autres fenêtres de l'application.
Cette structure est très utilisée dans la création graphiques dans de multiples domaines comme le mobile, le desktop, etc...

### Structure Backend:

En cours de réflexion et de rédaction.

## Interfaces:

### Ux design:

Pour le Ux design (*User eXperience: conception de la fenêtre adaptée aux utilisateurs ciblés*), nous avons utilisé le logiciel *adobeXD*. L’objectif est d'intégrer un maximum de fonctions dans une même page sans pour autant surchargé et perdre l’utilisateur. Nous avons donc opter pour la structure suivante :
![enter image description here](https://cdn.discordapp.com/attachments/777134083045326861/793121690115768340/unknown.png)
Ici, les outils seront placés sur le bord de gauche de l'application et le rendu sera dans le grand espace libre.

### Fonctionnement:

L'application permet à l'utilisateur de sélectionner la donnée qui l'intéresse et de lui appliquer plusieurs outils de traitement. Par exemple, l'utilisateur peut appliquer un outil de détourage des mouvements sur une vidéo. Le rendu est sur la fenêtre de l'application, mais il peut également être externalisé afin d'être mis en plein écran ou de pouvoir en projeter plusieurs.

## Backend:

En cours de réflexion et de rédaction.

## Résultats:

En cours de réflexion et de rédaction.
