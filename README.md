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

const char* ssid = "xxxxxxx";
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

### Connexion au serveur MQTT
#### Exemple 1 avec une souscription/publication de messages

Cet exemple illustre l'établissement d'une connexion MQTT à l'aide du terminal Wio avec un
serveur MQTT. Avec cela, vous pouvez utiliser le terminal Wio pour vous abonner et publier des
messages sur le serveur MQTT. Ici utilisé un serveur MQTT gratuit : https://test.mosquitto.org/.

- Téléchargez et installez la bibliothèque Arduino MQTT ici
(https://github.com/knolleary/pubsubclient)

```
#include "rpcWiFi.h"
#include <PubSubClient.h>

// Update these with values suitable for your network.
const char *ssid = "yourNetworkName";
// your network SSID
const char *password = "yourNetworkPassword"; // your network password
const char *ID = "Wio-Terminal-Client"; // Name of our device, must be unique
const char *TOPIC = "WioTerminal"; // Topic to subcribe to
const char *subTopic = "inTopic"; // Topic to subcribe to
const char *server = "test.mosquitto.org"; // Server URL

WiFiClient wifiClient;
PubSubClient client(wifiClient);

void callback(char* topic, byte* payload, unsigned int length) {
      Serial.print("Message arrived [");
      Serial.print(topic);
      Serial.print("] ");
      for (int i=0;i<length;i++) {
              Serial.print((char)payload[i]);
      }
      Serial.println();
}


void reconnect() {
// Loop until we're reconnected
while (!client.connected())
{
Serial.print("Attempting MQTT connection...");
// Attempt to connect
if (client.connect(ID)) {
      Serial.println("connected");
      // Once connected, publish an announcement...
      client.publish(TOPIC, "{\"message\": \"Wio Terminal is connected!\"}");
      Serial.println("Published connection message successfully!");
      // ... and resubscribe
      client.subscribe(subTopic);
      Serial.print("Subcribed to: ");
      Serial.println(subTopic);
}
else {
      Serial.print("failed, rc=");
      Serial.print(client.state());
      Serial.println(" try again in 5 seconds");
      // Wait 5 seconds before retrying
      delay(5000);
}

void setup()
{
      Serial.begin(115200);
      while (!Serial)
      ; // Wait for Serial to be ready
      Serial.print("Attempting to connect to SSID: ");
      Serial.println(ssid);
      WiFi.begin(ssid, password);
      // attempt to connect to Wifi network:
      while (WiFi.status() != WL_CONNECTED)
      {
            Serial.print(".");
            WiFi.begin(ssid, password);
            // wait 1 second for re-trying
            delay(1000);
      }
      Serial.print("Connected to ");
      Serial.println(ssid);
      delay(500);
}
client.setServer(server, 1883);
client.setCallback(callback);

void loop()
{
      if (!client.connected()) {
      reconnect();
      }
      client.loop();
}

```
Cet exemple illustre l'établissement d'une connexion MQTT à l'aide du terminal Wio. Ici utilisé un
serveur MQTTs gratuit : https://test.mosquitto.org/ et envoyant des données d'accélérateur à un
sujet.

##### Exemple 2 avec un transfert de données
Cet exemple illustre l'établissement d'une connexion MQTT à l'aide du terminal Wio. Ici utilisé un
serveur MQTTs gratuit : https://test.mosquitto.org/ et envoyant des données d'accélérateur à un
sujet.

- Téléchargez et installez la bibliothèque Arduino MQTT
(https://github.com/knolleary/pubsubclient)

- Installez la bibliothèque Accelerator pour Wio Terminal en suivant ce wiki (
https://wiki.seeedstudio.com/Wio-Terminal-IMU-Overview/)

- Le terminal Wio publiera l'accélérateur sur le sujet WioTerminal/IMU et souscrira aux
messages du sujet inTopic.

```
#include "rpcWiFi.h"
#include <PubSubClient.h>
#include <WiFiClientSecure.h>
#include"LIS3DHTR.h"
//const char *ssid = "yourNetworkName"; // your network SSID
//const char *password = "yourNetworkPassword"; // your network password
const char *ssid = "xxxxxx"; // your network SSID
const char *password = "wwwwww"; // your network password
const char *ID = "Wio-Terminal-Client"; // Name of our device, must be unique
const char *TOPIC = "WioTerminal/IMU"; // Topic to subcribe to
const char *subTopic = "inTopic"; // Topic to subcribe to
const char *server = "test.mosquitto.org"; // Server URL
const char *test_root_ca =
"-----BEGIN CERTIFICATE-----\n"
"MIIEAzCCAuugAwIBAgIUBY1hlCGvdj4NhBXkZ/uLUZNILAwwDQYJKoZIhvcNAQEL\n"
"BQAwgZAxCzAJBgNVBAYTAkdCMRcwFQYDVQQIDA5Vbml0ZWQgS2luZ2RvbTEOMAwG\n"
"A1UEBwwFRGVyYnkxEjAQBgNVBAoMCU1vc3F1aXR0bzELMAkGA1UECwwCQ0ExFjAU\n"
"BgNVBAMMDW1vc3F1aXR0by5vcmcxHzAdBgkqhkiG9w0BCQEWEHJvZ2VyQGF0Y2hv\n"
"by5vcmcwHhcNMjAwNjA5MTEwNjM5WhcNMzAwNjA3MTEwNjM5WjCBkDELMAkGA1UE\n"
"BhMCR0IxFzAVBgNVBAgMDlVuaXRlZCBLaW5nZG9tMQ4wDAYDVQQHDAVEZXJieTES\n"
"MBAGA1UECgwJTW9zcXVpdHRvMQswCQYDVQQLDAJDQTEWMBQGA1UEAwwNbW9zcXVp\n"
"dHRvLm9yZzEfMB0GCSqGSIb3DQEJARYQcm9nZXJAYXRjaG9vLm9yZzCCASIwDQYJ\n"
"KoZIhvcNAQEBBQADggEPADCCAQoCggEBAME0HKmIzfTOwkKLT3THHe+ObdizamPg\n"
"UZmD64Tf3zJdNeYGYn4CEXbyP6fy3tWc8S2boW6dzrH8SdFf9uo320GJA9B7U1FW\n"
"Te3xda/Lm3JFfaHjkWw7jBwcauQZjpGINHapHRlpiCZsquAthOgxW9SgDgYlGzEA\n"
"s06pkEFiMw+qDfLo/sxFKB6vQlFekMeCymjLCbNwPJyqyhFmPWwio/PDMruBTzPH\n"
"3cioBnrJWKXc3OjXdLGFJOfj7pP0j/dr2LH72eSvv3PQQFl90CZPFhrCUcRHSSxo\n"
"E6yjGOdnz7f6PveLIB574kQORwt8ePn0yidrTC1ictikED3nHYhMUOUCAwEAAaNT\n"
"MFEwHQYDVR0OBBYEFPVV6xBUFPiGKDyo5V3+Hbh4N9YSMB8GA1UdIwQYMBaAFPVV\n"
"6xBUFPiGKDyo5V3+Hbh4N9YSMA8GA1UdEwEB/wQFMAMBAf8wDQYJKoZIhvcNAQEL\n"
"BQADggEBAGa9kS21N70ThM6/Hj9D7mbVxKLBjVWe2TPsGfbl3rEDfZ+OKRZ2j6AC\n"
"6r7jb4TZO3dzF2p6dgbrlU71Y/4K0TdzIjRj3cQ3KSm41JvUQ0hZ/c04iGDg/xWf\n"
"+pp58nfPAYwuerruPNWmlStWAXf0UTqRtg4hQDWBuUFDJTuWuuBvEXudz74eh/wK\n"
"sMwfu1HFvjy5Z0iMDU8PUDepjVolOCue9ashlS4EB5IECdSR2TItnAIiIwimx839\n"
"LdUdRudafMu5T5Xma182OC0/u/xRlEm+tvKGGmfFcN0piqVl8OrSPBgIlb+1IKJE\n"
"m/XriWr/Cq4h/JfB7NTsezVslgkBaoU=\n"
"-----END CERTIFICATE-----\n";
long lastMsg = 0;
LIS3DHTR<TwoWire> lis;
WiFiClientSecure wifiClient;
PubSubClient client(wifiClient);
void callback(char *topic, byte *payload, unsigned int length)
{
Serial.print("Message arrived [");
Serial.print(topic);
Serial.print("] ");
for (int i = 0; i < length; i++)
{
Serial.print((char)payload[i]);
}
Serial.println();
}
void reconnect()
{
// Loop until we're reconnected
while (!client.connected())
{
Serial.print("Attempting MQTT connection...");
// Attempt to connect
if (client.connect(ID))
{
Serial.println("connected");
// Once connected, publish an announcement...
client.publish(TOPIC, "{\"message\": \"Wio Terminal is connected!\"}");
Serial.println("Published connection message successfully!");
// ... and resubscribe
client.subscribe(subTopic);
Serial.print("Subcribed to: ");
Serial.println(subTopic);
}
else
{
Serial.print("failed, rc=");
Serial.print(client.state());
Serial.println(" try again in 5 seconds");
// Wait 5 seconds before retrying
delay(5000);
}
}
}
void setup()
{
//Initialize serial and wait for port to open:
Serial.begin(115200);
while (!Serial)
; // Wait for Serial to be ready
delay(1000);
lis.begin(Wire1);
if (!lis) {
Serial.println("ERROR");
while(1);
}
lis.setOutputDataRate(LIS3DHTR_DATARATE_25HZ); //Data output rate
lis.setFullScaleRange(LIS3DHTR_RANGE_2G); //Scale range set to 2g
Serial.print("Attempting to connect to SSID: ");
Serial.println(ssid);
WiFi.begin(ssid, password);
// attempt to connect to Wifi network:
while (WiFi.status() != WL_CONNECTED)
{
Serial.print(".");
WiFi.begin(ssid, password);
// wait 1 second for re-trying
delay(1000);
}
Serial.print("Connected to ");
Serial.println(ssid);
wifiClient.setCACert(test_root_ca);
client.setServer(server, 8883);
client.setCallback(callback);
}
void loop()
{
if (!client.connected())
{
reconnect();
}
float x_values, y_values, z_values;
// Sending Data
long now = millis();
if (now - lastMsg > 5000) {
lastMsg = now;
x_values = lis.getAccelerationX();
y_values = lis.getAccelerationY();
z_values = lis.getAccelerationZ();
String data="{\"x-axis\": "+String(x_values)+","+"\"y-axis\": "+String(y_values)
+","+"\"z-axis\": "+String(z_values)+"}";
if (!client.publish(TOPIC, data.c_str())) {
Serial.println("Message failed to send.");
}
Serial.printf("Message Send [%s] ", TOPIC);
Serial.println(data);
}
client.loop();
}

```

###### Exemple 3 avec un client UDP

Le protocole UDP fonctionne différemment de TCP/IP. TCP est un protocole orienté flux,
garantissant que toutes les données sont transmises dans le bon ordre, UDP est un protocole orienté
message. UDP ne nécessite pas de connexion de longue durée, donc la configuration d’un socket
UDP est un peu plus simple. D’ailleurs, les messages UDP doivent tenir dans un seul paquet (pour
IPv4, cela signifie qu’ils ne peuvent contenir que 65507 octets car le paquet de 65535 octets
comprend également des informations d’en-tête) et la livraison n’est pas garantie comme c’est le
cas avec TCP.

Cet exemple se connecte à un réseau Wi-Fi et envoie des paquets UDP à un serveur UDP qui
s'exécute sur votre PC.

Remarque : Assurez-vous que votre PC et votre Wio Terminal sont sur le même réseau !

**Code serveur Python UDP**

- Enregistrez le code suivant sous udp_server.py.


  ```
# This python script listens on UDP port 3333
# for messages from the Wio Terminal board and prints them

import socket
import sys
try :
s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
s.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
except socket.error, msg :
print 'Failed to create socket. Error Code : ' + str(msg[0]) + ' Message '
+ msg[1]
sys.exit()
try:
s.bind(('', 3333))
except socket.error , msg:
print 'Bind failed. Error: ' + str(msg[0]) + ': ' + msg[1]
sys.exit()
print 'Server listening'
while 1:
d = s.recvfrom(1024)
data = d[0]
f not data:
break
print data.strip()
s.close()

  ```

  - Lancez le script python : python udp_server.py.

**Code Arduino**

- Remplacez networkName et networkPswd par vos paramètres Wi-Fi.

- Remplacez udpAddress par l'adresse IP de votre PC et assurez-vous que votre PC qui
exécute le serveur UDP est sur le même réseau que le Wio Terminal.

- Téléchargez le code sur le terminal Wio.

**Description de la fonction millis() :** La fonction millis() ne prend aucun paramètre et renvoie une
valeur qui représente le nombre de millisecondes écoulées depuis la mise en tension de l’Arduino.
La valeur est de type long non-signé (unsigned long, 4-bytes ou 32-bits). La valeur maximale
qu’elle peut prendre est de 4,294,967,295 soit 49 jours.

**Utilisation de la fonction millis() de l’IDE Arduino :** Pour pallier aux problèmes générés par
l’utilisation de la fonction delay(), une solution possible est d’utiliser la fonction millis(). Dès la
première utilisation de l’Arduino, la fonction delay() est utilisée afin de gérer les instructions en
fonction du temps. Le problème majeur de la fonction delay() est qu’elle bloque l’exécution de la
suite du code. Ceci devient très limitant lorsqu’on travaille avec plusieurs composants (gestions de
plusieurs LEDs ou capteurs). Nous allons voir dans ce tutoriel comment utiliser la fonction millis()
pour remplacer la fonction delay(). Il existe aussi la fonction micros() qui fonctionne sur le même
principe mais renvoie des microsecondes.

```
#include <rpcWiFi.h>
#include <WiFiUdp.h>
// WiFi network name and password:
const char * networkName = "your-ssid";
const char * networkPswd = "your-password";
//IP address to send UDP data to:
// either use the ip address of the server or
// a network broadcast address
const char * udpAddress = "192.168.0.255";
const int udpPort = 3333;
//Are we currently connected?
boolean connected = false;
//The udp library class
WiFiUDP udp;
void setup(){
// Initilize hardware serial:
Serial.begin(115200);
}
//Connect to the WiFi network
connectToWiFi(networkName, networkPswd);
void loop(){
//only send data when connected
if(connected){
//Send a packet
udp.beginPacket(udpAddress,udpPort);
udp.printf("Seconds since boot: %lu", millis()/1000);
udp.endPacket();
}
//Wait for 1 second
delay(1000);
}
void connectToWiFi(const char * ssid, const char * pwd){
Serial.println("Connecting to WiFi network: " + String(ssid));
// delete old config
WiFi.disconnect(true);
//register event handler
WiFi.onEvent(WiFiEvent);
//Initiate connection
WiFi.begin(ssid, pwd);
}
Serial.println("Waiting for WIFI connection...");
//wifi event handler
void WiFiEvent(WiFiEvent_t event){
switch(event) {
case SYSTEM_EVENT_STA_GOT_IP:
//When connected set
Serial.print("WiFi connected! IP address: ");
Serial.println(WiFi.localIP());
//initializes the UDP state
//This initializes the transfer buffer
udp.begin(WiFi.localIP(),udpPort);
connected = true;
break;
case SYSTEM_EVENT_STA_DISCONNECTED:
Serial.println("WiFi lost connection");
connected = false;
break;
default: break;
}
}
```
