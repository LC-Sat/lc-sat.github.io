# Application desktop CanSat

La création du CanSat lui même est un enjeux de taille. Cependant, l'enregistrement une fois terminé, les données ne sont pas explicites : 
| Exemple de données de test pour le GPS |  |
|--|--|
| 0010 1101 1001

Il est donc nécessaire de concevoir un logiciel capable de traduire ce format brut de données (binaire) en modèles graphiques et numériques plus adaptés à l'Homme.

## 1. Phase de conception


#### 1.1. Définition des besoins

Notre CanSat enregistre de multiples données pendant son fonctionnement (voir tableau 1).  De plus, l'objectif secondaire,  que nous avons définie pour notre CanSat, est de pouvoir traduire l'évolution des données au cours du fonctionnement du CanSat.
| Liste des données enregistrées : (Tableau 1) |  |
|--|--|
| Pression, Température, Altitude
|--|--
| Latitude, Longitude, Vitesse estimée, Nombre de satellites en liaison, qualité de la réception
|--|--|
| Vidéo standard, Vidéo thermique
|--|--|

Dans la continuité de notre raisonnement quand aux objectifs de notre projet, nous avons décidé de mettre en place un système de sécurité informatique. Celui-ci consiste à crypter les fichiers dans lesquels sont enregistrées les données. 
L'application doit être capable de :
- Décrypter les données.
- Traduire les données brutes en données compréhensibles 

#### 2.1. Définition du cahier des charges

Les objectifs de l'application étant fixé, la réflexion quand aux solutions techniques a commencé. D'abord, cette application  est en correspondance avec l'application à bord du CanSat. Le cahier des charges nous a permis de coordonner le développement des deux applications.
D'abord, nous avons déterminé le format d'enregistrement des données, afin que l'analyse de celles-ci puissent être effectuée sans grande difficultés. Nous avons opté pour un enregistrement en format binaire? Chaque données sont enregistrées dans un dictionnaire (format de données dans lequel une liste d'éléments, auxquels sont associés individuellement une clé, est enregistrée)  composé d'`array numpy`(module python permettant l'optimisation de la compilation. Ici nous l'utilisons dans la gestion des  de données). Ce format d'enregistrement est essentiel étant donnée la quantité faramineuse de données à traiter.
Ensuite, nous avons choisi le module `pyAesCrypt` comme module de cryptage et de décrypatge.

#### faire tableau cahier des charges

## 2. Phase de design

#### 1.1. Création du UX (User eXperience)

La conception des maquettes de l'application a d'abord débuté avec les plans de l'interface. Pour se faire, nous avons utilisé le logiciel Adobe xD   qui permet de créer et de simuler des maquettes rapidement. L'application sera composée de trois grandes interfaces :

- D'abord  
 3. Phase de développement
 4. Phase de tests
 5. Crédits
