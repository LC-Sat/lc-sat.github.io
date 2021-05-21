# LC-SAT : Application de traitement de données

Retour à l'[acceuil](https://lc-sat.github.io/doc/index).

Cette application est reliée directement à l'application embarquée dans la canette.
Développeur application de bord: **Aristide URLI**. *[Github](https://github.com/aripot007)*
Développeur application bureau: **Thomas HODSON**. *[Github](https://github.com/Tsumifa)*
Langage utilisé: **Python**. *Version 3.9*
Editeur utilisé: **Sublime Text**  . *Le  télécharger [ici](https://www.sublimetext.com/).*
Logiciel pour les diagrammes: LucidChart. *Le télécharger [ici](https://www.lucidchart.com)*.

Modules: 
> os,
> tkinter,
> opencv (cv2),
> numpy,
> matplotlib,
> json,
> pickle,
> folium,
> webbrowser,
> pyAesCrypt,
> shutil,
> zipfile

## Objectifs :

Les objectifs de cette application sont:

- Décrypter les données enregistrées par la canette au cours de sa chute.
- Traduire les données brutes en données compréhensibles.
- Fournir des outils d'analyses de ses données pour en tirer des conclusions scientifiques.

## Réalisation:
La réalisation de cette application s'est effectuée en plusieurs étapes:

- D'abord, la définition du cahier des charges.

Après de nombreuses réunions, pour définir le projet de la canette, nous avons lister les besoins. Puis, avec Aristide, nous nous sommes accorder sur les modules et les formats d'enregistrement des données. Voici un résumé des besoins et solutions techniques:
|Besoin| Solution envisagée |
|--|--|
| Crypter et décrypter les données. | `pyAescrypt`, `pickle` |
| Solution au stockage limitée. |`zipfile`, `shutil`|
| Utilisation simple pour tout le monde.| `tkinter`|
|Traitement des données.|`numpy`, `opencv`, `folium`, `webbrowser`, `matplotlib`|
|Application paramétrable.|`json`|

- Ensuite, vient la phase de design:

Application de design utilisée: **Adobe Xd**. *La téléchargée [ici](https://www.adobe.com/fr/products/xd.html).*
Durant cette phase, l'idée est de dessiner les différentes fenêtres de l'application, les liens qui les relient. Cette phase permet de s'assurer de n'avoir pas oublier de fenêtres, et de faciliter le développement de l'application.
Exemple d'une des fenêtres imaginée lors de la phase de design:

![Design de la première fenêtre](https://media.discordapp.net/attachments/777134083045326861/822490375556956230/unknown.png?width=1505&height=903)
- Puis vient la phase de développement:

## Structuration du projet:

Voici la structuration du projet:

    LC-Sat Data Treatment/
    |
    | -- bin/
    |	| -- __init__.py
    |
    | -- files/
    |	| -- data/
    |	|	| -- cam.mp4.aes
    |	|	| -- data.bin.aes
    |	| 
    |	| -- cam.mp4
    |	| -- data.bin
    |	| -- output.avi
    |	| -- planisphere.html
    |	| -- schematic.html
    |	| -- terrain.html
    |	| -- thermal.avi
    |
    | -- res/
    |	| -- config/
    |	|	| -- app_config.json
    |	|	| -- data_config.json
    |	|	| -- paths.json
    |	|	| -- settings.json
    |	|	| -- thermal_camera_config.json
    |	|
    |	| -- i18n/
    |	|	| -- cz.json
    |	|	| -- en-us.json
    |	|	| -- fr.json
    |	|
    |	| -- img/
    |	|	| -- logo.ico
    |	|	| -- logo.png
    |	|
    |	| -- themes/
    |	|	| -- bright.json
    |	|	| -- dark.json
    |
    | -- src/
    |	| -- controllers/
    |	|	| -- languages.py
    |	|	| -- load_consts.py
    |	|	| -- paths.py
    |	|	| -- settings.py
    |	|	| -- themes.py
    |	|
    |	| -- models/
    |	|	| -- buttons.py
    |	|	| -- inputs.py
    |	|	| -- labels.py
    |	|	| -- menus.py
    |	|
    |	| -- script/
    |	|	| -- crypt.py
    |	|	| -- graphs.py
    |	|	| -- maps.py
    |	|	| -- read_data.py
    |	|	| -- video.py
    |	|
    |	| -- views/
    |	|	| -- load_data.py
    |	|	| -- main_view.py
    |	|
    |	| -- root.py
    |
    | -- main.py
    | -- READ_ME.md
    | -- requirements.txt
    

L'application utilise une infrastructure MVC (pour Models, Views et Controllers). Cette infrastructure permet d'accélérer le développement frontend (*lié au visuel*) car les composants graphiques sont issus de modèles (moules d'un objet : boutons, textes, etc...). 
Exemple de modèles:  
```python
# Class de liaison entre les différents bouttons

class Buttons:


	def __init__(self):

		self.browse_folder_button = Browse_Folder_Button()
		self.valid_button = Valid_Button()
		self.normal_button = Normal_Button()


	def __str__(self):

		return "Class Bouttons"


# Bouttons de recherche de fichier

class Browse_Folder_Button:


	def __str__(self):

		return "Class Browse Bouttons"


	def create_widget(self, parent, text):

		button = tk.Button(parent, text=text, width=25, font=('Arial', 20, 'bold'))
		return button


# boutton valider

class Valid_Button:


	def __str__(self):

		return "Class Valid Bouttons"


	def create_widget(self, parent, text):

		button = tk.Button(
			parent,
			text=text,
			background="#1e8449",
			foreground="#F0F8FF",
			font=('Arial', 20, 'bold'),
			width=25
			)
		return button


# boutton normal

class Normal_Button:


	def __str__(self):

		return "Class Normal Button"


	def create_widget(self, parent, text):
		
		button = tk.Button(parent, text=text, font=('Arial', 15), width=20)
		return button
```

L'utilisation de l'infrastructure MVC permet de séparer la logique de l'affichage au travers des fichiers type `Views`. Chaque fichier contient l'appel des composants graphiques d'une fenêtre.
Par exemple, voici le fichier de la page de chargement de données :

```python
class Load_Data_Window:


	def __init__(self, controllers, models):
		
		self.controllers = controllers
		self.models = models
	

	def __str__(self):

		return "Load Data Window class"


	# Gère l'affichage du chemin du dossier sélectionné
	def folder_path(self):

		self.filename = filedialog.askopenfilename(defaultextension='.gz', initialdir ="Téléchargements")
		self.path_label.configure(text=self.filename)


	# créer les composants
	def create_widget(self, parent):
		
		# titre
		self.title = self.models.labels.label_title.create_widget(parent,
			self.controllers.language_controller.get_text("loadData"),
			self.controllers.theme_controller.get_theme("backgroundColor"),
			self.controllers.theme_controller.get_theme("color")
			)
		self.title.pack()

		# Frame du formulaire
		 
		self.form_frame = tk.Frame(parent,
			bg=self.controllers.theme_controller.get_theme("backgroundColor"),
			borderwidth=5,
			highlightbackground=self.controllers.theme_controller.get_theme("color"),
			highlightcolor=self.controllers.theme_controller.get_theme("color"),
			highlightthickness=5,
			)
		self.form_frame.pack()

		# indicateur d'enter de clef de décryptage
		self.key_input_indicator = self.models.labels.label_classic.create_widget(self.form_frame,
		 	self.controllers.language_controller.get_text("keyInput"),
			self.controllers.theme_controller.get_theme("backgroundColor"),
			self.controllers.theme_controller.get_theme("color")
			)
		self.key_input_indicator.configure(padding=35)
		self.key_input_indicator.pack()

		# Champs de saisie de la clef de décryptage
		self.key_input = self.models.inputs.entry.create_widget(self.form_frame)
		self.key_input.pack()

		# indicateur d'enter de clef de décryptage
		self.folder_path_indicator = self.models.labels.label_classic.create_widget(self.form_frame,
			self.controllers.language_controller.get_text("folderInput"),
			self.controllers.theme_controller.get_theme("backgroundColor"),
			self.controllers.theme_controller.get_theme("color")
			)
		self.folder_path_indicator.configure(padding=35)
		self.folder_path_indicator.pack()

		# boutton de selection de fichier
		self.browse_folder = self.models.buttons.browse_folder_button.create_widget(
			self.form_frame,
			self.controllers.language_controller.get_text("browse")
			)
		self.browse_folder.configure(command=self.folder_path)
		self.browse_folder.pack()

		# Chemin du fichier choisi
		self.path_label = self.models.labels.subtitle_label.create_widget(self.form_frame,
			'',
			self.controllers.theme_controller.get_theme("backgroundColor"),
			self.controllers.theme_controller.get_theme("color")
			)
		self.path_label.pack()
``` 

Les `controllers` permettent de communiquer les données stockées dans les fichiers de configurations, transmettre les textes dans la langue sélectionnée, de transmettre les caractéristiques du style choisit.
Exemple du controller des paramètres:
```python
class Settings:

	def __init__(self, file_path):

		self.file_path = file_path

		with open(self.file_path, 'r') as f:
			self.data = json.load(f)
			f.close()


	def __str__(self):

		return "Settings Controller"


	def get_setting(self, setting_name):
		
		return self.data[setting_name]

	
	def update_setting(self, setting_name, new_value):
		
		self.data[setting_name] = new_value

		with open(self.file_path, 'w') as f:
			json.dump(self.data, f, indent=4)
			f.close()
```
## Paramétrage de l'application:

### Langues:

L'application dispose de plusieurs langages (actuellement  anglais, français et tchèque). On peut ajouter manuellement des langages. Il suffit de copier un fichier de langue existant, le renommer avec le nom de la langue, changer le contenu dans la langue en question et placer le fichier dans le dossier `i18n`.
Fichier sur la langue française:
```json
{
	"title": "LC-SAT Traitement de donnees",
	"loadData": "Charger Des Donnees : ",
	"keyInput": "Entrer la clef de decryptage :",
	"folderInput": "Choisir un fichier :",
	"browse": "Rechercher",
	"decrypt": "Decrypter",
	"treatmentTools": "Outils de Traitement de Données",
	"graphs": "Graphs",
	"video": "Video",
	"gps": "GPS",
	"map": "Cartes",
	"planisphere": "Planisphere",
	"schematic": "Schematique",
	"satellite": "Satellite",
	"classicVideo": "Video Classique",
	"thermialVideo": "Video Thermique",
	"showNormalVideo": "Voir la video",
	"renderTrackingVideo": "Detourage",
	"renderMotionFiltering": "Filtrage des Mouvements",
	"normalGraph": "Graphique classique",
	"multipleGraph": "Graphiques multiples",
	"fullGraph": "Graphique complet",
	"time": "Temps (s)",
	"overTime": "en fonction du temps",
	"temperature": "Temperature",
	"pression": "Pression",
	"altitude": "Altitude",
	"acceleration": "Acceleration",
	"speed": "Vitesse",
	"quality": "Qualite du signal",
	"humidity": "Humidite",
	"show": "Dessiner"
}
```

### Thèmes:

Comme pour les langues, l'application dispose de plusieurs thèmes. Pour en ajouter un, il suffit de procéder de la manière que pour les langues. L'application dispose de deux thèmes. Vous pouvez ajouter les thèmes dans le dossier `themes`.
Le fichier sur le thème sombre:
```json
{
	"backgroundColor": "#212121",
	"color": "#F0F8FF"
}
```
### Configuration de la fenêtre:

Le fichier `app_config.json` contient les paramètres de la fenêtre :
```json
{
	"WIN_SIZE": "1366x768"
}
```

### Configuration des données:

Vous pouvez changez les paramètres d'enregistrement des données dans le fichier `data_config.json`:
```json
{
	"temperature": {
		"fps": 10,
		"name": "Temperature",
		"unit": "Celsius"
	},
	"pression": {
		"fps": 10,
		"name": "Pression",
		"unit": "hPa"
	},
	"altitude": {
		"fps": 10,
		"name": "Altitude",
		"unit": "m"
	},
	"accelerometre": {
		"fps": 10,
		"name": "Acceleration",
		"unit": "m/s²"
	},
	"satellite": {
		"fps": 10,
		"name": "Satellite",
		"unit": ""
	},
	"quality": {
		"fps": 10,
		"name": "Quality",
		"unit": ""
	},
	"speed": {
		"fps": 10,
		"name": "Speed",
		"unit": "m.s"
	},
	"humidity": {
		"fps": 10,
		"name": "humidity",
		"unit": "%"
	}
}
```

Le fichier de configuration de la caméra thermique est un fichier à part. Il s'agit du fichier `thermal_camera_config.json`. Vous pouvez modifier les configurations de la caméra thermique dans ce fichier:
```json
{
	"FPS": 10,
	"RESOLUTION": [8, 8],
	"FINAL_RESOLUTION": [440, 440],
	"MIN_TEMP": -10,
	"MAX_TEMP": 50,
	"MIN_COLOR": [0, 0, 255],
	"MOY_COLOR": [0, 255, 0],
	"MAX_COLOR": [255, 0, 0]
}
```
### Paramètres :
Pour sélectionner les paramètres de l'application, il suffit de modifier manuellement les valeurs dans le fichier `settings.json`:
```json
{
    "language": "fr",
    "theme": "dark",
    "data_type": [
    	"data.bin",
    	"cam.mp4"
    ]
}
```

## Flexibilité de l'application :

L'application s'adapte quel que soit son emplacement de stockage. Le module `os` permet de trouver l'adresse du dossier racine. Le fichier `paths.json` stocke les destinations depuis le fichier racine:
```json
{
	"DATA_PATH": "/res/config/",
	"SETTINGS_PATH": "/res/config/settings.json",
	"CONST_PATH": "/res/config/app_const.json",
	"THERMAL_CONFIG_PATH": "/res/config/thermal_camera_config.json",
	"DATA_CONFIG_PATH": "/res/config/data_config.json",
	"LANG_PATH": "/res/i18n/",
	"IMG_PATH": "/res/img/",
	"THEME_PATH": "/res/themes/",
	"FILES_DATA": "/files/"
}
```  
## Décryptage et lecture des données :

### Décryptage :

Voici l'organigramme du programme de décryptage:

![Programme décrytptage](https://media.discordapp.net/attachments/777134083045326861/837996710437191690/Read_data.png?width=1006&height=590)

Nous avons opter pour un stockage compressé afin de réduire le poids des données en transite.
Voici le script de décryptage :
```python
class Decrypt:


	def __str__(self):

		return "Decrypt class"


	# Décrypt le fichier
	def decrypt(self, folder_path, destination, data_type, password):

		print("chemin fichier :{0}\nchemin destination: {1}\ntype_donnée: {2}\nmdp: {3}".format(folder_path, destination, data_type, password))

		filename, file_extension = os.path.splitext(folder_path)
		# Décompresse le fichier
		if file_extension == '.gz':
			
			shutil.unpack_archive(folder_path, destination)

		# Transfert les fichiers si le dossier est déjà décompressé
		else:

			for filename in os.listdir(folder_path):
				shutil.copyfile(filename, destination)

		# Décrypte chaque fichier:
		# 	- key est le nom initial
		# 	- value est le nom final
		for key, value in data_type.items():

			pyAesCrypt.decryptFile(key, value, password, 16 * 1024)
```

### Lecture des données :

Une fois les données décryptées et décompressées, le dossier `/files` contient 2 fichiers: `cam.mp4` et `data.bin`.
Le fichier `cam.mp4` contient la vidéo standard enregistrée par la canette. Le fichier `data.bin` contient l'ensemble des données enregistrées par la canette. Voici un script que vous pouvez utiliser ce script pour voir les données enregistrées:
```python
import pickle

data = pickle.load(open("data.bin", "rb"))
print(data.keys())
```
résultat:
|Nom|  Données|
|--|--|
| press | Pression |
| temp | Température |
| alt | Altitude |
| ax | Accélération axe X |
| ay | Accélération axe Y |
| az | Accélération axe Z |
| lat | Latitude |
| lon | Longitude |
| sat | Nombre de satellites en communication avec le GPS |
| qual | Qualité de la réception du GPS |
| speed | Vitesse estimée de la canette par le satellite |
| hum | Humidité |
| therm | Caméra thermique |

 Les données sont chargées dans des `array numpy "float64"`:
```python
class Data_Reader:

	def __init__(self, folder_path):

		self.folder_path = folder_path


	def __str__(self):

		return "Data Reader"


	def read_data(self):

		# Reconvertit les données et les enregistres dans des arrays numpy en "float64"
		data = pickle.load(open(self.folder_path + "data.bin", "rb"))

		self.pression = np.array(data["press"], dtype="float64")
		self.temperature = np.array(data["temp"], dtype="float64")
		self.altitude = np.array(data["alt"], dtype="float64")
		self.x_acceleration = np.array(data["ax"], dtype="float64")
		self.y_acceleration = np.array(data["ay"], dtype="float64")
		self.z_acceleration = np.array(data["az"], dtype="float64")
		self.latitude = np.array(data["lat"], dtype="float64")
		self.longitude = np.array(data["lon"], dtype="float64")
		self.satellite = np.array(data["sat"], dtype="float64")
		self.quality = np.array(data["qual"], dtype="float64")
		self.speed = np.array(data["speed"], dtype="float64")
		# self.humidity = np.array(data["hum"])
		self.thermique = np.array(data["therm"], dtype="float64")


	def return_all_data(self):

		return [self.pression, self.temperature, self.altitude, self.x_acceleration,self.y_acceleration, self.z_acceleration, self.satellite, self.quality, self.speed]
```

La caméra thermique requière cependant plus d'opérations pour rendre les données compréhensibles et exploitables. La caméra thermique enregistre toutes les 0.1 secondes un tableau de 8x8 pixels, où chaque pixels se voient attribuer une valeur.Le script suivant traduit ces valeurs en couleurs et la liste de tableau en une vidéo. La vidéo étant de 8x8 pixels, le script l'agrandit. Le script:
```python
class Thermal_Video:


	def __str__(self):

		return "Thermal Video Maker Class"


	def __init__(self, config_path, store_path):

		# Charge les consantes depuis le fichier de configuration
		with open(config_path, "r") as file:

			config = json.load(file)

			file.close()


		self.MIN_TEMP = [config["MIN_TEMP"], config["MIN_COLOR"]]
		self.MAX_TEMP = [config["MAX_TEMP"], config["MAX_COLOR"]]
		self.MOY_TEMP = [(self.MIN_TEMP[0] + self.MAX_TEMP[0]) / 2, config["MOY_COLOR"]]

		self.WIDTH = config["RESOLUTION"][0]
		self.HEIGHT = config["RESOLUTION"][1]

		self.FPS = config["FPS"]

		self.store_path = store_path

		self.FINAL_RESOLUTION = [config["FINAL_RESOLUTION"][0], config["FINAL_RESOLUTION"][1]]

	def convert_to_color(self, value):

		# Détermination du ratio à appliquer pour changer la couleur
		# 0 <= couleur <= 255
		# Renvoi la couleur RGB du pixel

		if value < MOY_TEMP[0]:

			ratio = (self.MOY_TEMP[0] + self.MIN_TEMP[0] + value) / 300
			return [
				round((self.MOY_TEMP[1][0] + self.MIN_TEMP[1][0]) * ratio),
				round((self.MOY_TEMP[1][1] + self.MIN_TEMP[1][1]) * ratio),
				round((self.MOY_TEMP[1][2] + self.MIN_TEMP[1][2]) * ratio)
			]

		elif value > MOY_TEMP[0]:

			ratio = (self.MOY_TEMP[0] + self.MIN_TEMP[0] + value) / 300
			return [	
				round((self.MOY_TEMP[1][0] + self.MAX_TEMP[1][0]) * ratio),
				round((self.MOY_TEMP[1][0] + self.MAX_TEMP[1][0]) * ratio),
				round((self.MOY_TEMP[1][0] + self.MAX_TEMP[1][0]) * ratio)
			]

		else:

			return self.MOY_TEMP[1]


	def resize_thermal_video(self):

		cap = cv.VideoCapture(self.store_path + 'thermal.avi')
		fourcc = cv.VideoWriter_fourcc(*'XVID')
		out = cv.VideoWriter('output.avi', fourcc, 5, (self.FINAL_RESOLUTION[0], self.FINAL_RESOLUTION[1]))

		while True:

		    ret, frame = cap.read()

		    if ret == True:

		        b = cv.resize(frame, (440, 440), fx=0, fy=0, interpolation = cv.INTER_CUBIC)
		        out.write(b)

		    else:

		        break

		cap.release()
		out.release()
		cv.destroyAllWindows()


	def create_thermal_video(self, data):

		# Transforme la valeur de temperature des pixels en une valeur RGB
		# Ecrit cette valeur dans  

		fourcc = VideoWriter_fourcc(*'MP42')	
		video = VideoWriter(self.store_path +'thermal.avi', fourcc, float(self.FPS), (self.WIDTH, self.HEIGHT))

		for frame in data["therm"]:

			colored_image = []

			for row in frame:

				colored_row = []

				for pixel in row:

					colored_image.append(self.convert_to_color(pixel))

				colored_image.append(colored_row)

			image = np.uint8(colored_image)

			video.write(image)

		video.realease()

		self.resize_thermal_video()
```

---

## Analyses des données :

### Cartes:

Pour analyser les données du GPS, j'utilise les modules `folium` et `webbrowser`. Le module  `folium` permet de créer des cartes et de placer des marqueurs. Le module `webbrowser` permet d'ouvrir la carte sur le navigateur dès sa création. Voici le script de création des cartes :
```python
class Map:


	def __init__(self):

		self.planisphere_map = Planisphere_Map()
		self.schematic_map = Schematic_Map()
		self.terrain_map = Terrain_Map()


	def __str__(self):

		return "Class Map"



class Planisphere_Map:


	def __str__(self):

		return "Marker Map class"


	def render_map(self, latitude, longitude, store_path):

		self.map = folium.Map(location=[latitude[0], longitude[0]], zoom_start=13)

		for i in range(len(latitude)):

			try:

				folium.Marker(
				    location=[latitude[i], longitude[i]],
				    icon=folium.Icon(color="red", icon="info-sign"),
				).add_to(self.map)

				print("Marker {0} :\tlat = {1}\tlon = {2}".format(i, latitude[i], longitude[i]))

			except IndexError:

				break


		# affiche la carte dans le navigateur
		self.map.save(store_path + "planisphere.html")
		self.url = store_path + "planisphere.html"
		webbrowser.open(self.url, new=2)



class Schematic_Map:


	def __str__(self):

		return "Class Schematic Map"


	def render_map(self, latitude, longitude, store_path):

		self.map = folium.Map(location=[latitude[0], longitude[0]], zoom_start=13, tiles="Stamen Toner")

		for i in range(len(latitude)):

			try:

				folium.Marker(
				    location=[latitude[i], longitude[i]],
				    icon=folium.Icon(color="red", icon="info-sign"),
				).add_to(self.map)

				print("Marker {0} :\tlat = {1}\tlon = {2}".format(i, latitude[i], longitude[i]))

			except IndexError:

				break


		# affiche la carte dans le navigateur
		self.map.save(store_path + "schematic.html")
		self.url = store_path + "schematic.html"
		webbrowser.open(self.url, new=2)



class Terrain_Map:


	def __str__(self):

		return "Class Terrain Map"


	def render_map(self, latitude, longitude, store_path):

		self.map = folium.Map(location=[latitude[0], longitude[0]], zoom_start=13, tiles="Stamen Terrain")

		for i in range(len(latitude)):

			try:

				folium.Marker(
				    location=[latitude[i], longitude[i]],
				    icon=folium.Icon(color="red", icon="info-sign"),
				).add_to(self.map)

				print("Marker {0} :\tlat = {1}\tlon = {2}".format(i, latitude[i], longitude[i]))

			except IndexError:

				break


		# affiche la carte dans le navigateur
		self.map.save(store_path + "terrain.html")
		self.url = store_path + "terrain.html"
		webbrowser.open(self.url, new=2)
```

### Vidéos:

Le module `opencv` est un module de traitement d'image. Il permet d'afficher une vidéo, de créer une vidéo et d'analyser une vidéo. La vidéo thermique est téléchargée en format brute. Voici le diagramme de création de la vidéo thermique:

![Diagramme de création de la vidéo thermique](https://media.discordapp.net/attachments/777134083045326861/839503042382790676/Creation_video_thermique.png?width=800&height=590)


Voici le script utilisé pour traiter les vidéos:
```python
class Video:

	def __init__(self):

		self.classic_video = Render_Video()	
		self.motion_filtering = Video_Motion_Filtering()
		self.motion_detection = Motion_Detection()


# Affiche la vidéo sans changements
class Render_Video:

	def render(self, video_path):

		cap = cv.VideoCapture(video_path)

		# Read until video is completed
		while(cap.isOpened()):
		    
		    # Capture frame-by-frame
		    ret, frame = cap.read()
		    
		    if ret == True:

		        # Display the resulting frame
		        cv.imshow('Frame', frame)

		    # Press Q on keyboard to  exit
		    if cv.waitKey(25) & 0xFF == ord('q'):
		        break

		# When everything done, release the video capture object
		cap.release()

		# Closes all the frames
		cv.destroyAllWindows()


# Filtrage des formes en mouvements sur la vidéo
class Video_Motion_Filtering:

	def render(self, video_path):

		# variables
		substractor_min = 20
		substractor_max = 50

		# charge la video et les composants nécéssaires pour le filtrage des mouvements 
		video = cv.VideoCapture(video_path)
		substractor = cv.createBackgroundSubtractorMOG2(20, 50)

		# Recherche si la vidéo est toujours en cours:
		# 	- si oui, applique le détourage tant que la touche 'x' n'est pas pressée
		# 	- si non, relance la vidéo

		while True:

			return_value, frame = video.read()

			if return_value:

				mask = substractor.apply(frame)
				cv.imshow('Mask', mask)

				# changement des variables
				key = cv.waitKey(30)&0xFF
				
				if key == ord('x'):
					break

				if key == ord('p'):

					substractor_max = min(100, substractor_max + 5)

				if key == ord("m"):

					substractor_min = max(5, substractor_min - 5)

			else:
				
				video = cv.VideoCapture(video_path)



		video.release()
		cv.destroyAllWindows()


# Detourage des formes en mouvements
class Motion_Detection:

	def render(self, video_path):

		# Chargement de la video
		capture = cv.VideoCapture(video_path)

		# Valeurs d'analyse
		kernel_blur = 1
		seuil = 15
		surface = 1000

		# Video sans changement des variables d'analyse
		ret, origin = capture.read()

		origin = cv.cvtColor(origin, cv.COLOR_BGR2GRAY)
		origin = cv.GaussianBlur(origin, (kernel_blur, kernel_blur), 0)

		kernel_dilate = np.ones((5, 5), np.uint8)

		while True:

			# Video avec changement des variables d'analyse
			ret, frame = capture.read()

			gray = cv.cvtColor(frame, cv.COLOR_BGR2GRAY)
			gray = cv.GaussianBlur(gray, (kernel_blur, kernel_blur), 0)
			cv.imshow("frame", gray)

			# Comparaison des deux flux videos
			mask = cv.absdiff(origin, gray)
			mask = cv.threshold(mask, seuil, 255, cv.THRESH_BINARY)[1]
			mask = cv.dilate(mask, kernel_dilate, iterations=3)

			# Ajout des contours des objets en mouvement
			contours, nada = cv.findContours(mask, cv.RETR_EXTERNAL, cv.CHAIN_APPROX_SIMPLE)
			frame_contour = frame.copy()

			for c in contours:

				cv.drawContours(frame_contour, [c], 0, (0, 255, 0), 5)

				if cv.contourArea(c)< surface:

					continue

				x, y, w, h = cv.boundingRect(c)
				cv.rectangle(frame, (x, y), (x+w, y+h), (0, 0, 255), 2)

			origin = gray

			# Ajout des textes
			cv.putText(frame, "[o|1]seuil: {:d} [p|m]blur: {:d} [i|k]surface: {:d}".format(seuil, kernel_blur, surface), (10, 30), cv.FONT_HERSHEY_PLAIN, 1, (0, 255, 255), 2)
			# Affichage du resultat
			
			cv.imshow("frame", frame)

			# Changement des variables
			key = cv.waitKey(30)&0xFF

			if key == ord('x'):

				break
			
			try:

				if key == ord('p'):

					kernel_blur = min(43, kernel_blur + 2)

				if key == ord('m'):

					kernel_blur = max(1, kernel_blur - 2)
				
				if key == ord('s'):

					surface += 100

				if key == ord('r'):

					surface -= 100

				if key == ord('o'):

					seuil = min(255, seuil + 1)

				if key == ord('l'):

					seuil = max(1, seuil - 1)

			except Exception:

				pass

		capture.release()
		cv.destroyAllWindows()
```
### Graphiques :
Pour rendre les données compréhensibles, j'utilise le module `matplotlib` afin de créer des graphiques traduisant l'évolution des données au cours du temps. La gestion des graphiques est basée sur un modèle 'flex' puisqu'il suffit d'appeler  la fonction en plaçant les données que l'on veut traiter en paramètre. Voici le script:

```python
class Graph:


	def __str__(self):

		return "Graph class"


	def __init__(self, data_config_path):

		self.data_config_path = data_config_path
		self.normal_graph = Normal_Graph(self.data_config_path)
		self.multiple_graph = Multiple_Graph(self.data_config_path)
		self.full_graph = Full_Graph(self.data_config_path)


# Trace l'evolution d'une seule mesure

class Normal_Graph:


	def __init__(self, data_config_path):

		with open(data_config_path, "r") as file:
			
			self.data_config = json.load(file)
			file.close()


	def __str__(self):

		return "Normal class Graph"


	def create_grah(self, data, data_name, language_controller):

		# valeur x et y du graph
		x = [0]
		y = []
		
		# frequence de l'enregistrement
		x_step = 1 / self.data_config[data_name]["fps"]

		for _ in range(len(data) - 1):

			x.append(x_step)
			x_step += x_step

		X = np.array(x)
		Y = np.array(data, dtype="float64")

		# configuration des graphiques
		
		plt.plot(X, Y, 'r-+')
		plt.xlabel(language_controller.get_text("time"))
		plt.ylabel(self.data_config[data_name]["name"] + ' (' + self.data_config[data_name]["unit"] + ")")

		plt.title(self.data_config[data_name]["name"] + ' ' + language_controller.get_text("overTime"))
		plt.show()



# Trace l'evolution d'un ensemble de mesures de meme type

class Multiple_Graph:


	def __init__(self, data_config_path):

		with open(data_config_path, "r") as file:
			
			self.data_config = json.load(file)
			file.close()


	def __str__(self):

		return "Multiple Graph Class"


	def create_graph(self, data, data_names, data_type):

		# Creation des 'sous' graphiques
		fig, axs = plt.subplots(len(data))
		fig.suptitle(self.data_config[data_type]["name"] + " en fonction du temps.")

		for i, unit in enumerate(data):

			x = []
			x_step = 1 / self.data_config[data_type]["fps"]


			for _ in range(len(unit)):

				x.append(x_step)
				x_step += x_step

			X = np.array(x)
			Y = np.array(unit, dtype="float64")

			axs[i].plot(X, Y, '-o', label=data_names[i])
			axs[i].legend(data_names[i])

		plt.show()


# Trace toutes les mesures

class Full_Graph:


	def __init__(self, data_config_path):

		with open(data_config_path, "r") as file:
			
			self.data_config = json.load(file)
			file.close()


	def __str__(self):

		return "Full Graph Class"


	def create_graph(self, datas, data_names):


		fig, ax = plt.subplots()

		# FPS
		x_step  = 1 / 10

		lines = []

		for i, data in enumerate(datas):

			x = []

			for _ in range(len(data)):

				x.append(x_step)
				x_step += x_step

			X = np.array(x)
			Y = np.array(data, dtype="float64")

			print(len(X))
			print(len(Y))
			i, = ax.plot(X, Y, label=data_names[i])
			lines.append(i)

		rax = plt.axes([0.05, 0.4, 0.1, 0.15])
		labels = [str(line.get_label()) for line in lines]
		visibility = [line.get_visible() for line in lines]
		check = CheckButtons(rax, labels, visibility)


		def change_visivility(label):

		    index = labels.index(label)
		    lines[index].set_visible(not lines[index].get_visible())
		    plt.draw()


		check.on_clicked(change_visivility)

		plt.show()
```

## Ce que je compte ajouter :

L'application fonctionne correctement et ne requière pas de mise à jour particulière. Je souhaite donc orienter les améliorations sur le UX (l'expérience d'utilisation).
- D'abord je voudrais mettre un système de customisation des graphiques, des cartes et des vidéos (choisir les couleurs, les polices, etc...). 
- Ensuite j'aimerais ajouter la reconnaissance d'objet de `OpenCv` sur la caméra classique, également mettre un mode d'affichage des données directement sur la caméra.
- Enfin, je souhaite retravailler l'apparence de l'application, ajouter plus de langues, ajouter plus de thèmes et mettre un menu pour modifier les paramètres.

## Le programme complet :

![diagramme complet](https://cdn.discordapp.com/attachments/777134083045326861/839513898046586880/Programme_complet.png)

---
> Écrit avec [StackEdit](https://stackedit.io/).

