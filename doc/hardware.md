# HARDWARE
## Sommaire:

> 1. **Description du projet**
	 - **Objectifs**
	 - **Composants de la canette**
> 2. **Structure de la canette**
	 - **Structure principale**
	 - **Structure secondaire**
 >3. **Missions principale**
	 - **Structure interne**
	 - **Communication interne**
 >4. **Mission secondaire**
	 - **Structure interne**
	 - **Communication interne**
 >5. **Communications**
	 - **Réception**
	 - **Émission**

## Description du projet:

### Objectifs:

##### Objectifs imposés:
Comme précisé dans les règles du concours, la canette doit d'abord être capable de se poser avec les contraintes suivants :

 - vitesse : entre 5.5m/s et 12m/s
 - masse  : entre 300g et 350g
 
 Les règles indiquent également que la canette doit pouvoir enregistrer la pression et la température, disposer d'un GPS et d'un buzzer pour retrouver sa position rapidement.  
##### Objectifs choisis:
Nous avons choisi la prise de multiples mesures. Nous avons donc décidé de nous fixer les objectifs suivants :

 - Obtenir une vidéo durant la descente en format classique et thermique.
 - Obtenir l'altitude au cours du temps de la canette.
 - Obtenir l'accélération au cours du temps de la canette.
 - Déterminer le degré hygrométrique de l'air (*le taux d'humidité*).
 - Un système de stockage sécurisé des données (*cryptage des données*).
 
Le traitement des données sera quand à lui effectué au sol à l'aide d'outil conçu à cet effet.

### Composants de la canette:

Nous avons choisi d'utiliser des composants de la même gamme afin de faciliter la communication entre eux et réduire le temps de développement des outils de communications et d'analyse. La canette présente tout de même une longue liste de composants :
|Nom|Fonction|Masse (mg)|Volume (mm³)|Marque|Prix (€)|Lien
|--|--|--|--|--|--|--
|Ordinateur de bord|Communication et enregistrement des données|12(g)|14471.6|Raspberry pi|28.55|[Site](https://www.raspberrypi.org/products/compute-module-4/?variant=raspberry-pi-cm4001000)
|Caméra thermique|Prise de vidéo thermique|2.9|3947,4|Adafruit|60|[Site](https://www.amazon.fr/Adafruit-3538-Module-cam%C3%A9ra-thermique/dp/B07GR9ZS9C)
|Caméra standard| Prise de vidéo|3|5400|Raspberry pi|28.99|[Site](https://www.amazon.fr/LABISTS-Raspberry-Officielle-Compatible-Rasbperry/dp/B07VW6XJZQ/ref=sr_1_6?adgrpid=55659850545&dchild=1&gclid=CjwKCAiAxKv_BRBdEiwAyd40N8Ced9-pS5eyqRI4U76AgIqBW67ATFqevL-83qr4JGpVGo7ETZhUQhoClwwQAvD_BwE&hvadid=275569255832&hvdev=c&hvlocphy=9055110&hvnetw=g&hvqmt=e&hvrand=1048945815819096544&hvtargid=kwd-311202848547&hydadcr=27714_1756367&keywords=cam%C3%A9ra%20raspberry%20pi&qid=1609266141&sr=8-6&tag=googhydr0a8-21)
|Pression + Température + Altitude|Détermine l'altitude, la pression et la température.| ?|338|AZDelivery|8|[Site](https://www.amazon.fr/AZDelivery-%E2%AD%90%E2%AD%90%E2%AD%90%E2%AD%90%E2%AD%90-GY-68-BMP180-barom%C3%A9trique/dp/B07D8S617X/ref=sr_1_11?__mk_fr_FR=%C3%85M%C3%85%C5%BD%C3%95%C3%91&dchild=1&keywords=capteur%2bpression%2bet%2btemp%C3%A9rature%2braspberry%2bpi&qid=1608477494&sr=8-11&th=1)
|GPS|Déterminer la position du satellite|22|8482.5|AZDelivery|22|[Site](https://www.amazon.fr/AZDelivery-NEO-6M-Module-GPS-Parent/dp/B01N38EMBF?th=1)
|Accéléromètre|Détermine l'accélération de la canette au cours du temps|2|960|Paradisetronic|8.49|[Site](https://www.amazon.fr/MPU-6050-Acc%C3%A9l%C3%A9rom%C3%A8tre-Gyroscope-d%C3%A9clatement-Raspberry/dp/B01F11WXN4/ref=sr_1_6?dchild=1&keywords=raspberry%20pi%20accelerometre&qid=1608479678&sr=8-6)
|Humidité|Détermine l'humidité de l'air|20|3360|Stemedu|14|[Site](https://www.amazon.fr/capteur-temp%C3%A9rature-num%C3%A9rique-Arduino-Raspberry/dp/B07L83FFV8/ref=sr_1_6?__mk_fr_FR=%C3%85M%C3%85%C5%BD%C3%95%C3%91&dchild=1&keywords=DHT22&qid=1608480572&sr=8-6)
|Batterie|Stockage d'énergie|?|17000|SODIAL|6.90|[Site](https://www.amazon.fr/SODIAL-Batterie-Rechargeable-Navigation-Enregistreur/dp/B07L6MG9J7)
|Chargeur|Recharger la batterie sans la retirer de la canette|2|576|Lorenlil|0.29|[Site](https://fr.aliexpress.com/item/32802292731.html?src=google&albch=shopping&acnt=248-630-5778&isdl=y&slnk=&plac=&mtctp=&albbt=Gploogle_7_shopping&aff_atform=google&aff_short_key=UneMJZVf&gclsrc=aw.ds&&albagn=888888&&ds_e_adid=477782989824&ds_e_matchtype=&ds_e_device=c&ds_e_network=u&ds_e_product_group_id=800756788306&ds_e_product_id=fr32802292731&ds_e_product_merchant_id=106324435&ds_e_product_country=FR&ds_e_product_language=fr&ds_e_product_channel=online&ds_e_product_store_id=&ds_url_v=2&ds_dest_url=https://fr.aliexpress.com/item/32802292731.html?&albcp=11565796786&albag=115683794594&gclid=CjwKCAiAxKv_BRBdEiwAyd40N1__zmK_2D55InbT1PQuLO-w4S_eCLzZRBNjbDWNUdCDYd9U2vrY-xoCJ9wQAvD_BwE)
|Buzzer|Émettre des sons pour retrouver la canette plus rapidement|10|1000|Bobury|2.83|[Site](https://www.amazon.fr/Bobury-%C3%A9lectronique-magn%C3%A9tique-continu-%C3%A9lectromagn%C3%A9tique/dp/B07F6CZ28F/ref=sr_1_18?__mk_fr_FR=%C3%85M%C3%85%C5%BD%C3%95%C3%91&crid=3417U7ZZ92U2V&dchild=1&keywords=buzzer%2belectronique&qid=1608481875&sprefix=buzzer%2belectr,aps,179&sr=8-18&th=1)
|Lecteur carte SD|Stocker les informations et les programmes|Ø|Ø|GCT|0.91|[Site](https://www.digikey.fr/en/supplier-centers/gct)
||Total :|98.9(g)|55535.5||180.96

L'ensemble des composants (sauf batterie et chargeur) sont compatibles avec la technologie Raspberry pi.

## Structure de la canette :

### Structure principale :

La structure principale de la canette est constituée des composants suivants:

 - Batterie
 - Ordinateur de bord
 - Chargeur
 - Parachute

Nous avons donc opter pour une disposition interne permettant de libérer un maximum d'espace pour les composants secondaires (*capteurs...*):
***En cours de réflexion : insérer image plane interne de la canette***

### Structure secondaire :

La structure secondaire de la canette est constituée des composants suivants:

 - Caméra thermique
 - Caméra thermique
 - Capteur pression, température et altimètre
 - GPS
 - Accéléromètre
 - Capteur humidité
 - Buzzer

***En cours de réflexion : insérer image plane interne de la canette***

## Mission principale :

### Structure interne :

La mission principale est composée des modules suivants:
- Parachute
- Capteur pression, température et altimètre
- GPS
- Buzzer
- Ordinateur de bord

La mission principale consiste en deux étapes:
1. D'abord le satellite doit enregistrer la pression et la température au cours de sa descente (*cela permet de déterminer son altitude*).
2. Le satellite doit pouvoir se poser sans dégâts et dans des contraintes prédéfinies (*Voir Objectifs*).

Nous devons donc ici relier la première partie de la mission afin que la seconde puisse être réalisée.

### Communication interne :

***Insérer image ici***

## Mission secondaire:

### Structure interne :

La mission secondaire est composée des modules suivants:
- Ordinateur de bord
- Caméra standart
- Caméra thermique
- 
