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

