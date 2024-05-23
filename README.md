## Tutoriel  mise en route : Wio Terminal (RTL8720DN) Wi-Fi

### Aperçu
Mise à jour le dernier micrologiciel pour le Wireless Core Realtek RTL8720 sur Wio Terminal, ainsi
que l'installation de toutes les bibliothèques dépendantes pour Wio Terminal afin d'activer la
connectivité sans fil.
Note :
Nous déplaçons le logiciel Wi-Fi vers la nouvelle structure eRPC qui est plus stable et peut
fonctionner avec le Bluetooth en même temps ! Veuillez suivre la procédure de mise à jour vers le
micrologiciel Wi-Fi eRPC et les bibliothèques associées !

### Mettre à jour le micrologiciel du noyau sans fil
Tout d'abord, nous devons mettre à jour le micrologiciel du noyau sans fil Realtek RTL8720 sur le
terminal Wio. Ceci est essentiel et doit être mis à jour avec le dernier micrologiciel avant de passer
aux exemples.

**Étape 1 - Configuration Arduino**
Pour pouvoir mettre à jour le micrologiciel sur le RTL8720, nous devons activer la connexion série
de SAMD51 à RTL8720. Ceci est fait par un simple programme Arduino.

**Méthode uf2**
Pour plus de commodité, nous proposons des méthodes uf2 de téléchargement du micrologiciel du
terminal Wio. Téléchargez simplement les fichiers uf2 ci-dessous.
Téléchargez les fichiers rtl8720_update_v2.uf2 uf2. (http://files.seeedstudio.com/wiki/Wio-Terminal/res/rtl8720_update_v2.uf2)



 <img alt="WIOT rtl" src="https://github.com/madou-sow/Tutoriel-mise-en-route-Wio-Terminal-Wi-Fi/blob/main/images/rtl8720.png" width=50% height=50%  title="WIOT rtl"/>


Entrer dans le mode bootloader en faisant glisser l'interrupteur d'alimentation deux fois rapidement.
Pour plus de référence, veuillez également consulter ici.

 <img alt="WIOT rtl" src="https://github.com/madou-sow/Tutoriel-mise-en-route-Wio-Terminal-Wi-Fi/blob/main/images/glisser2.png" width=50% height=50%  title="WIOT rtl"/>


Un lecteur externe nommé Arduino devrait apparaître sur votre PC. Faites glisser les fichiers
rtl8720_update_v2.uf2 téléchargés dans le lecteur Arduino et cela réinitialisera le terminal Wio et
chargera le croquis !


 <img alt="WIOT rtl" src="https://github.com/madou-sow/Tutoriel-mise-en-route-Wio-Terminal-Wi-Fi/blob/main/images/misajwio.jpg" width=50% height=50%  title="WIOT rtl"/>

**Étape 2 - Téléchargez le dernier micrologiciel**
Remarque : il s'agit du dernier micrologiciel de structure eRPC pour RTL8720
Téléchargez le dernier micrologiciel RTL8720 (https://github.com/Seeed-Studio/seeed-ambd-firmware/releases)
- 20210519-seeed-ambd-firmware-rpc-v2.1.3.zip
- 20210519-seeed-ambd-firmware-rpc-v2.1.3_JP.zip

**Méthodes CLI**
Maintenant, vous pouvez flasher le micrologiciel RTL8720 sur le terminal Wio en utilisant les
méthodes CLI.
Téléchargez les outils CLI comme suit à l'aide de Terminal :
```
$ cd ~
$ git clone https://github.com/LynnL4/ambd_flash_tool
```
**Exemple d'utilisation de l'interface de ligne de commande**

Pour LinuxOS, veuillez utiliser le script ambd_flash_tool.py.
Ouvrez le terminal et accédez à l'emplacement du fichier. Exécutez python3 ambd_flash_tool.py à
l'emplacement et vous devriez voir l'utilisation de l'aide :

**Remarque :** Assurez-vous que Python 3 est installé sur votre ordinateur, et le script téléchargera
automatiquement toutes les bibliothèques dépendantes.

Dans certains cas, vous pouvez n'avoir que Python 3 sur votre PC, puis remplacez python3
ambd_flash_tool.py par python ambd_flash_tool.py.
Pour effacer le firmware initial à l'intérieur du RTL8720, exécutez :
Il prend en charge la fonction de port de détection automatique !

```
mamadou@dugny:/tempo/wiot-wireless-firmware/ambd_flash_tool$ ls -l
total 11516
-rw-r--r-- 1 mamadou users 19 Jan 6 15:12 README.md
-rw-r--r-- 1 mamadou users 10863916 Jan 6 15:12 ambd_flash_tool.exe
-rwxr-xr-x 1 mamadou users 9859 Jan 6 15:12 ambd_flash_tool.py
drwxr-xr-x 2 mamadou users 4096 Jan 6 15:12 firmware
-rw-r--r-- 1 mamadou users 4688 Jan 6 15:12 imgtool_flashloader_amebad.bin
-rw-r--r-- 1 mamadou users 4412 Jan 6 15:13 km0_boot_all.bin
-rw-r--r-- 1 mamadou users 876544 Jan 6 15:13 km0_km4_image2.bin
-rw-r--r-- 1 mamadou users 4068 Jan 6 15:13 km4_boot_all.bin
-rw-r--r-- 1 mamadou users 25 Jan 6 15:12 requirements.txt
drwxr-xr-x 5 mamadou users 4096 Jan 6 15:12 tool

$ python3 ambd_flash_tool.py erase

Remarque : Le processus d'effacement initial peut prendre un certain temps. Soyez patient et ne fermez pas les fenêtres.
```

<img alt="WIOT rtl" src="https://github.com/madou-sow/Tutoriel-mise-en-route-Wio-Terminal-Wi-Fi/blob/main/images/erase1.png" width=70% height=70%  title="WIOT rtl"/>

 <img alt="WIOT rtl" src="https://github.com/madou-sow/Tutoriel-mise-en-route-Wio-Terminal-Wi-Fi/blob/main/images/erase2.png" width=70% height=70%  title="WIOT rtl"/>

Pour flasher le nouveau firmware téléchargé dans le RTL8720, exécutez :
```
$ python3 ambd_flash_tool.py flash -d [RTL8720-firmware-path]
```
 Remplacez [RTL8720-firmware-path] par le chemin que vous avez téléchargé le RTL8720 ci-
dessus.
Cet emplacement doit contenir **km0_boot_all.bin, km0_km4_image2.bin et km4_boot_all.bin**
ces 3 fichiers.

```
mamadou@dugny:/tempo/wiot-wireless-firmware$ ls -1
20210519-seeed-ambd-firmware-rpc-v2.1.3.zip
ambd_flash_tool
bin
install.sh
rtl8720_update_v2.uf2
seeed-ambd-firmware-2.1.3.zip
mamadou@dugny:/tempo/wiot-wireless-firmware$
mamadou@dugny:/tempo/wiot-wireless-firmware/ambd_flash_tool$ ls -l
drwxr-xr-x 2 mamadou users 4096 Jan 20 10:48 20210519-seeed-ambd-firmware-rpc-v2.1.3
-rw-r--r-- 1 mamadou users19 Jan 6 15:12 README.md
-rw-r--r-- 1 mamadou users 10863916 Jan 6 15:12 ambd_flash_tool.exe
-rwxr-xr-x 1 mamadou users 9859 Jan 6 15:12 ambd_flash_tool.py
drwxr-xr-x 2 mamadou users 4096 Jan 6 15:12 firmware
-rw-r--r-- 1 mamadou users 4688 Jan 6 15:12 imgtool_flashloader_amebad.bin
-rw-r--r-- 1 mamadou users 4412 Jan 23 14:01 km0_boot_all.bin
-rw-r--r-- 1 mamadou users 876544 Jan 23 14:01 km0_km4_image2.bin
-rw-r--r-- 1 mamadou users 4068 Jan 23 14:01 km4_boot_all.bin
-rw-r--r-- 1 mamadou users 25 Jan 6 15:12 requirements.txt
drwxr-xr-x 6 mamadou users 4096 Jan 20 11:22 seeed-ambd-firmware-2.1.3
drwxr-xr-x 5 mamadou users 4096 Jan 6 15:12 tool

mamadou@dugny:/tempo/wiot-wireless-firmware/ambd_flash_tool$ python3 ambd_flash_tool.py flash -d 20210519-seeed-ambd-firmware-rpc-v2.1.3

```
Si tout se passe bien, vous devriez voir tous un message réussi. Vous avez maintenant flashé le
nouveau firmware RTL8720 dans le noyau RTL8720 !

### Installation des bibliothèques (eRPC)
Il existe peu de bibliothèques Arduino nécessaires à la connectivité sans fil. S'ensuit l'installation
toutes les bibliothèques nécessaires :

1. Installez Seeed_Arduino_rpcWiFi
   
Visitez les référentiels Seeed_Arduino_rpcWiFi et téléchargez l'intégralité du référentiel sur
votre disque local.
Maintenant, la bibliothèque Seeed_Arduino_rpcWiFi peut être installée sur l'IDE Arduino.
Ouvrez l'IDE Arduino, et cliquez sur sketch -> Include Library -> Add .ZIP Library, et choisissez le
fichier Seeed_Arduino_rpcWiFi que vous venez de télécharger.

2. Installez Seeed_Arduino_rpcUnified
   
Visitez les référentiels Seeed_Arduino_rpcUnified et téléchargez l'intégralité du référentiel sur
votre lecteur local.
Désormais, la bibliothèque Seeed-Arduino-FreeRTOS peut être installée sur l'IDE Arduino.
Ouvrez l'IDE Arduino, et cliquez sur sketch -> Include Library -> Add .ZIP Library, et choisissez le
fichier Seeed_Arduino_rpcUnified que vous venez de télécharger.

3. Installez Seeed_Arduino_FreeRTOS
Visitez les référentiels Seeed_Arduino_FreeRTOS et téléchargez l'intégralité du référentiel sur
votre lecteur local.
Désormais, la bibliothèque Seeed-Arduino-FreeRTOS peut être installée sur l'IDE Arduino.
Ouvrez l'IDE Arduino et cliquez sur sketch -> Include Library -> Add .ZIP Library, et choisissez le
fichier Seeed_Arduino_FreeRTOS que vous venez de télécharger.

### Wio Terminal RTL8720DN Wi-Fi Manuel d'utilisation
#### Connectivité Wi-Fi
Ce wiki explique comment configurer la connectivité Wi-Fi sur le terminal Wio à l'aide du noyau
Realtek RTL8720.

**Note :**
Assurez-vous d'avoir suivi l'aperçu du réseau, mis à jour le dernier micrologiciel sur RTL8720 et
téléchargé les bibliothèques Arduino dépendantes.

**Attention :**
Les exemples suivants ont été mis à jour pour fonctionner avec le micrologiciel de structure de
structure eRPC, veuillez mettre à jour la structure eRPC. Remplacez simplement AtWifi.h par
rpcWiFi.h.

#### Configuration en mode Station (STA)

- Inclure la librairie rpcWifi.h dans Arduino.
- Configure as STA mode :
  
```
WiFi.mode(WIFI_STA);
```
  
**Numérisation d'un exemple de code de réseau Wi-Fi**

Cet exemple se configurera en mode Wi-Fi STA, scannera et imprimera tous les réseaux disponibles
sur le Serial.

```
#include "rpcWiFi.h"
void setup() {
Serial.begin(115200);
while(!Serial); // Wait for Serial to be ready
delay(1000);
// Set WiFi to station mode and disconnect from an AP if it was previously
connected
WiFi.mode(WIFI_STA);
WiFi.disconnect();
delay(100);
}
Serial.println("Setup done");
void loop() {
Serial.println("scan start");
// WiFi.scanNetworks will return the number of networks found
int n = WiFi.scanNetworks();
Serial.println("scan done");
if (n == 0) {
Serial.println("no networks found");
} else {
Serial.print(n);
Serial.println(" networks found");
for (int i = 0; i < n; ++i) {
// Print SSID and RSSI for each network found
Serial.print(i + 1);
Serial.print(": ");
Serial.print(WiFi.SSID(i));
Serial.print(" (");
Serial.print(WiFi.RSSI(i));
Serial.print(")");
Serial.println((WiFi.encryptionType(i) == WIFI_AUTH_OPEN) ? " " :
"*");
delay(10);
}
}
Serial.println("");
}
// Wait a bit before scanning again
delay(5000);
```

**Connexion au réseau spécifié : Exemple de code**

Cet exemple se connecte à un réseau Wi-Fi spécifié. Modifiez le ssid et le mot de passe de votre
réseau Wi-Fi.

```
#include "rpcWiFi.h"
const char* ssid = "HONOR5MAMADOU";
const char* password = "yourNetworkPassword";
void setup() {
Serial.begin(115200);
while(!Serial); // Wait for Serial to be ready
// Set WiFi to station mode and disconnect from an AP if it was previously
connected
WiFi.mode(WIFI_STA);
WiFi.disconnect();
Serial.println("Connecting to WiFi..");
WiFi.begin(ssid, password);
while (WiFi.status() != WL_CONNECTED) {
delay(500);
Serial.println("Connecting to WiFi..");
WiFi.begin(ssid, password);
}
Serial.println("Connected to the WiFi network");
Serial.print("IP Address: ");
Serial.println (WiFi.localIP()); // prints out the device's IP address
}
void loop() {
}

```
