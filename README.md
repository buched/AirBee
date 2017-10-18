﻿# AirBee V1.0 en cours

<img src="Picture/montagev1.png" width="500"/>

L'idée est de transmettre toutes les données suivantes :
- température dans la ruche -- fait
- humidité dans la ruche -- fait
- masse de la ruche -- fait
- nombre d'abeilles entrées -- en cours
- nombre d'abeille sortie -- en cours
- tension de la batterie -- fait
Via un système 100% autonome en énergie et communication
	
## Coté alimentation : 
- Une lipo 5Ah <http://www.cdiscount.com/telephonie/batteries-telephone/easyacc-batterie-externe-5000mah-ultra-slim-charge/f-14487-eas0700686513077.html> (33€)
- Panneau solaire 3W <https://www.digikey.fr/product-detail/fr/seeed-technology-co-ltd/313070001/1597-1414-ND/5488054> (12USD)
- lipoRider <https://www.seeedstudio.com/Lipo-Rider-v1.3-p-2403.html> (9.5USD)

3 fils partent du module d'alim vers la carte (vcc,gnd,Tbat)

<img src="Picture/alim.jpg" width="500"/>
<img src="Picture/alim3D.jpg" width="500"/>

## Coté intelligence :
- Carte ucontrolleur Arduino nano <https://fr.aliexpress.com/item/Freeshipping-Nano-3-0-controller-compatible-for-arduino-nano-CH340-USB-driver-NO-CABLE/32242060255.html?spm=a2g0s.9042311.0.0.Ohpjts>(2€)

## Coté communication :
- Kit Carte Breakout Sigfox BRKWS01 + Antenne +fdp TTC + un an abonnement <https://yadom.fr/carte-breakout-sfm10r1.html> (26€)
ou que le module <https://yadom.fr/reseaux-iot/sigfox/pack-10-modules-wisol-sfm10r1-pour-le-reseau-sigfox.html> (4€)

## Coté Capteur :
- pour avoir l'heure RTC  <https://www.adafruit.com/product/3296> (7.5USD) -- pas indispensable
- Compteur I/O abeilles : projet BeeCounter2 <http://www.instructables.com/id/Honey-Bee-Counter-II/> (25USD)
- Capteur température humidité SHT11 <https://www.adafruit.com/product/246> (35USD) (2€ sur Aliexpress)
- Capteur poids X4 + Load Cell Amplifier - HX711 <https://fr.aliexpress.com/item/FREE-SHIPPING-20pcs-lot-Experiments-body-scale-wholesale-human-scale-load-cell-sensor-resistance-strain-50kg/32271599811.html> et <https://fr.aliexpress.com/item/1PCS-HX711-Weighing-Sensor-Dual-Channel-24-Bit-Precision-A-D-Module-Pressure-Sensor-for-Arduino/32653087154.html?spm=a2g0s.9042311.0.0.zTDiLJ> (5€)
  
Prix total low cost : 15€ !?

vue d'ensemble au 08/10/2017 :

<img src="Picture/plateau.jpg" width="500"/>
<img src="Picture/electronique.jpg" width="500"/>
<img src="Picture/ensemble2.jpg" width="500"/>

## Fonctionnement
L'Arduino centralise les données est les envoie au backend sigfox. On a droit à 140 messages de 12 Octets par jour, ca passe juste sans optimisation.

Payload : 
	
	ID::uint:8 Temp::int:16:little-endian Hum::uint:16:little-endian Poids::uint:16:little-endian IN::uint:16:little-endian OUT::uint:16:little-endian Vbat::uint:8

Sigfox renvoie les données via des CallBacks vers serveur perso (php-->json) ou backend web (Carrots et ConnectView), je suis aussi en train de regarder DjangoREST pour voir la meilleure solution.
Le but est d'avoir un dashboard pour suivre l'évolution des paramètres, sans tout redévelopper.

Il reste du travail sur l'intégration de toute l'electronique sur un plateau de ruche indépendant, sans pertuber son fonctionnement.


# Perspectives
Supprimer le RTC au profit d'un compteur ?
Passer directement à la puce sigfox SFM10R1 à 34€ les 10 et pas la carte à 26€ l'unité
Dessiner une carte electronique dediée. --> en cours <https://circuitmaker.com/Projects/Details/jeremy-seyssaud/AirBee>
Peut etre créer un reseau Xbee local sur 5 ruches pour un seul module Sigfox.
Rajouter une station météo?

