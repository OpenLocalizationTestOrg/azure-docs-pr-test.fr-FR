---
title: "aaaIoT DevKit toocloud - tooAzure de se connecter AZ3166 de kit de développement IoT IoT Hub | Documents Microsoft"
description: "Découvrez comment toosetup et connectez-vous tooAzure AZ3166 du Kit de développement IoT IoT Hub pour qu’il plateforme de cloud computing Azure toosend données toohello dans ce didacticiel."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: xshi
ms.openlocfilehash: fd36abaed1fd9f73028b84312bca9e900fb9c004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-iot-devkit-az3166-tooazure-iot-hub-in-hello-cloud"></a>Se connecter AZ3166 du Kit de développement IoT tooAzure IoT Hub dans le cloud de hello

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

Hello [MXChip IoT DevKit](https://microsoft.github.io/azure-iot-developer-kit/) peuvent être utilisé toodevelop et prototype solutions Internet of Things (IoT) en exploitant les services Microsoft Azure. Il comprend une carte compatible avec Arduino et équipée d’un large éventail de périphériques et de capteurs, un package de carte open source et un [catalogue de projets](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/) grandissant.

## <a name="what-you-do"></a>Procédure
Se connecter [DevKit](https://microsoft.github.io/azure-iot-developer-kit/) tooan Azure IoT hub que vous créez, données de température et humidité hello collecter à partir des capteurs et envoyez le concentrateur de tooIoT données hello.

Vous n’avez pas encore de DevKit ? Cliquez [ici](https://aka.ms/iot-devkit-purchase) pour en obtenir un.

## <a name="what-you-learn"></a>Contenu

* Comment tooconnect IoT DevKit tooWireless accès point et préparer votre environnement de développement.
* Comment toocreate un IoT hub et inscrire un appareil pour le Kit de développement MXChip IoT.
* Comment les données de capteur toocollect par un exemple d’application en cours d’exécution sur le Kit de développement MXChip IoT.
* Comment toosend hello tooyour IoT hub capteur données.

## <a name="what-you-need"></a>Ce dont vous avez besoin

* Une carte MXChip IoT DevKit avec câble micro USB. [Cliquez ici pour l’obtenir](https://aka.ms/iot-devkit-purchase).
* Un ordinateur sous Windows 10 ou macOS 10.10 ou une version ultérieure.
* Un abonnement Azure actif
  * Activez un [compte d’évaluation Microsoft Azure gratuit pendant 30 jours](https://azureinfo.microsoft.com/us-freetrial.html).

## <a name="prepare-your-hardware"></a>Préparation du matériel

Raccorder hello matériel tooyour ordinateur.

### <a name="hardware-you-need"></a>Matériel nécessaire

* Carte DevKit
* Câble micro USB

![bien-démarrer-matériel](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/hardware.jpg)

### <a name="connect-devkit-tooyour-computer"></a>Kit de développement tooyour ordinateur connecté

1. Connexion USB fin tooyour PC
2. Se connecter Micro USB fin toohello Kit de développement
3. toopower suivant de LED Hello verte confirme la connexion

![bien-démarrer-connexion](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect.jpg)

## <a name="configure-wifi"></a>Configurer le WiFi

Les projets IoT dépendent de la connectivité à Internet. Utilisez hello suivant les instructions tooconfigure hello DevKit tooconnect tooWiFi.

### <a name="enter-ap-mode"></a>Activer le mode « point d’accès »

Maintenez le bouton B, puis push et relâchez le bouton Réinitialiser de hello, puis le bouton de mise en production B. Votre Kit de développement passe en Mode de point d’accès de configuration Wi-Fi. écran Hello affiche hello Service définir Identifier(SSID) Hello Kit de développement ainsi que d’adresse IP du portail configuration hello :

![bien-démarrer-point-d-accès-wifi](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ap.jpg)

### <a name="connect-toodevkit-ap"></a>Se connecter tooDevKit l’Asie-Pacifique

À présent, utiliser un autre Wi-Fi activée périphériques (PC ou un téléphone mobile) tooconnect toohello SSID DevKit (mis en surbrillance dans la capture d’écran hello ci-dessus), laissez le mot de passe hello vide.

![bien-démarrer-ssid](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect-ssid.png)

### <a name="configure-wifi-for-devkit"></a>Configurer le WiFi pour DevKit

Adresse IP de hello ouverte à l’écran du Kit de développement hello sur votre PC ou d’un navigateur de téléphone mobile, sélectionnez hello Wi-Fi réseau tooconnect du Kit de développement hello à, puis tapez le mot de passe hello. Cliquez sur **Connect** toocomplete :

![bien-démarrer-portail-wifi](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-portal.png)

Une fois la connexion de hello réussit, hello Kit de développement redémarrera dans quelques secondes. Si a réussi, vous verrez hello Wi-Fi nom et adresse IP sur l’écran hello :

![bien-démarrer-ip-wifi](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ip.jpg)

> [!NOTE] 
adresse IP de Hello dans photo de hello ne correspondent ne peut-être pas hello réel affecté et IP affichées sur l’écran du Kit de développement hello. Ce comportement est normal de Wi-Fi qui utilise DHCP toodynamically affecter des adresses IP.

Après la configuration Wi-Fi, vos informations d’identification sont rendues persistantes sur l’appareil hello pour cette connexion, même si déconnecté. Par exemple, si vous configuré hello Kit de développement pour Wi-Fi à votre domicile et a ensuite pris office de toohello hello Kit de développement, vous devez tooreconfigure PA mode (commençant à l’étape **passer en Mode de l’Asie-Pacifique**) tooconnect hello DevKit tooyour office Wi-Fi. 

## <a name="start-using-devkit"></a>Commencer à utiliser DevKit

application par défaut de Hello en cours d’exécution sur le Kit de développement vérifie hello dernière version du microprogramme de hello et afficher des données de diagnostic de capteur pour vous.

### <a name="upgrade-toohello-latest-firmware"></a>Mettre à niveau le microprogramme toohello

Vous êtes invité à l’écran hello que deux hello version du microprogramme actuel et la plus récente s’il existe une mise à niveau si nécessaire. Suivez [mise à niveau du microprogramme](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/) guide tooupgrade il.

![bien-démarrer-microprogramme](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/firmware.jpg)

> [!NOTE] 
Il s’agit d’un effort à usage unique, une fois que vous démarrez le développement sur le Kit de développement de hello et télécharger votre application, vous devez le dernier microprogramme de hello sont fournis avec votre application.

### <a name="test-various-sensors"></a>Tester divers capteurs

Appuyez sur les capteurs tootest bouton B, continuer en appuyant sur et en libérant hello B bouton toocycle via chaque capteur.

![bien-démarrer-capteurs](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/sensors.jpg)

## <a name="prepare-development-environment"></a>Préparer l’environnement de développement

À présent, il tooset temps d’environnement de développement hello : outils et les packages pour toobuild IoT applications surprenantes. Vous pouvez choisir la version Windows ou macOS selon le système d’exploitation de tooyour.


### <a name="windows"></a>Windows

Nous vous invitons à vous toouse hello installation package tooprepare hello environnement de développement. Si vous rencontrez des problèmes, vous pouvez suivre hello [étapes manuelles](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/) tooget il fait.

#### <a name="download-latest-package"></a>Télécharger la dernière version du package

Hello `.zip` fichier que vous téléchargez contient tous les outils nécessaires et les packages requis pour le développement du Kit de développement.

> [!div class="button"]
[Télécharger](https://azureboard.azureedge.net/prod/installpackage/devkit_install_1.0.2.zip)


> [!NOTE] 
> Hello `.zip` fichier contient des éléments suivants de hello outils et les packages. Si vous avez déjà des composants installés, le script de hello détectera et les ignorer.
> * Node.js et fils : exécution de script de configuration hello et les tâches automatisées
> * [Fichier MSI de Azure CLI 2.0](https://docs.microsoft.com//cli/azure/install-azure-cli#windows) -expérience en ligne de commande d’inter-plateformes de gestion de ressources Azure hello MSI contient les Python et pip dépendante.
> * [Visual Studio Code](https://code.visualstudio.com/) : éditeur de code léger pour le développement DevKit
> * [Extension Visual Studio Code pour Arduino](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino) : permet le développement Arduino dans VS Code
> * [Arduino IDE](https://www.arduino.cc/en/Main/Software): extension hello pour Arduino s’appuie sur cet outil
> * Package de la carte du Kit de développement : Outil de chaînes, les bibliothèques et les projets pour hello Kit de développement
> * Utilitaire ST-Link : pilotes et utilitaires essentiels

#### <a name="run-installation-script"></a>Exécuter le script d’installation

Dans l’Explorateur de fichiers Windows, localisez hello `.zip` et extrayez-le, recherchez `install.cmd`, avec le bouton droit et sélectionnez **« Exécuter en tant qu’administrateur »** toostart.

![bien-démarrer-exécution-administrateur](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/run-admin.png)

Pendant l’installation, vous verrez progression hello de chaque outil ou d’un package.

![bien-démarrer-installation](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/install.png)

#### <a name="confirm-tooinstall-drivers"></a>Vérifiez les pilotes tooinstall

Hello VS Code pour l’extension de Arduino s’appuie sur hello Arduino IDE. S’il s’agit hello première fois que vous installez hello Arduino IDE, vous serez tooinstall demandées les pilotes appropriés :

![bien-démarrer-pilote](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/driver.png)

Il doit prendre l’installation de toofinish environ 10 minutes en fonction de votre vitesse d’Internet. Une fois l’installation de hello est terminée, vous devez voir les raccourcis de Code Visual Studio et Arduino IDE sur votre bureau.

> [!NOTE] 
Au lancement de VS Code, il peut arriver qu’une erreur s’affiche, indiquant que l’IDE Arduino ou un package de carte associé est introuvable. toosolve il, fermez Visual Studio Code, lancer Arduino IDE qu’une seule fois et VS Code doivent localiser les chemin d’accès Arduino IDE correctement.


### <a name="macos-preview"></a>macOS (préversion)

Suivez ces environnement de développement tooprepare étapes macOS.

#### <a name="install-azure-cli-20"></a>Installer Azure CLI 2.0

Suivez hello [guide officiel](https://docs.microsoft.com//cli/azure/install-azure-cli) tooinstall Azure CLI 2.0 :

Installez Azure CLI 2.0 avec une commande `curl` :

```bash
curl -L https://aka.ms/InstallAzureCli | bash
```

Et redémarrez votre interface de commande pour effet de tootake de modifications :

```bash
exec -l $SHELL
```

#### <a name="install-arduino-ide"></a>Installer l’IDE Arduino

Hello Arduino de Code Visual Studio extension s’appuie sur hello Arduino IDE. Téléchargez et installez hello [Arduino IDE pour macOS](https://www.arduino.cc/en/Main/Software).

#### <a name="install-visual-studio-code"></a>Installation de Visual Studio Code

Téléchargez et installez [Visual Studio Code pour macOS](https://code.visualstudio.com/). Il s’agit de hello principal outil de développement pour la création d’applications DevKit IoT.

####  <a name="download-latest-package"></a>Télécharger la dernière version du package

1. Installez Node.js. Vous pouvez utiliser le Gestionnaire de package macOS populaires [Homebrew](https://brew.sh/) ou [intégrées dans le programme d’installation](https://nodejs.org/en/download/) tooinstall il.

2. Téléchargez le fichier `.zip` contenant les scripts de tâches requis pour le développement DevKit dans VS Code.

   > [!div class="button"]
   [Télécharger](https://azureboard.azureedge.net/installpackage/devkit_tasks_1.0.2.zip)

   Recherchez hello `.zip` et extrayez-le. Puis lancez **Terminal** application et exécution hello suivant tooconfigure de commandes :

   Déplacez les extraits tooyour macOS utilisateur dossier :
   ```bash
   mv [.zip extracted folder]/azure-board-cli ~/. ; cd ~/azure-board-cli
   ```
  
   Installez les packages `npm` :
   ```
   npm install
   ```

#### <a name="install-vs-code-extension-for-arduino"></a>Installer l’extension VS Code pour Arduino

Code Visual Studio permet aux extensions de Marketplace tooinstall directement dans l’outil de hello, cliquez simplement sur icône des extensions dans le volet de menu de gauche hello hello, puis recherchez `Arduino` tooinstall :

![installation-extensions](media/iot-hub-arduino-devkit-az3166-get-started/installation-extensions-mac.png)

#### <a name="install-devkit-board-package"></a>Installer le package de carte DevKit

Vous aurez besoin à l’aide de hello Gestionnaire de tableau dans Visual Studio Code le Kit de développement tableau tooadd hello.

1. Utilisez `Cmd+Shift+P` palette et le type de commande tooinvoke **Arduino** puis recherchez et sélectionnez **Arduino : Gestionnaire de tableau**.

2. Cliquez sur **'URL supplémentaires'** en bas de hello à droite.
   ![installation-url-supplémentaires](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)

3. Bonjour `settings.json` , ajoutez une ligne au bas de hello de `USER SETTINGS` volet et l’enregistrer.
   ```json
   "arduino.additionalUrls": "https://raw.githubusercontent.com/VSChina/azureiotdevkit_tools/master/package_azureboard_index.json"
   ```
   ![installation-paramètres-json](media/iot-hub-arduino-devkit-az3166-get-started/installation-settings-json-mac.png)

4. Maintenant Bonjour Gestionnaire de tableau de rechercher « az3166 » et installer la version la plus récente hello.
   ![installation-az3166](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)

Vous avez maintenant tous les outils nécessaires de hello et les packages installés pour macOS.


## <a name="open-project-folder"></a>Ouvrir un dossier de projet

### <a name="launch-vs-code"></a>Lancer VS Code

Assurez-vous que votre DevKit n’est pas connecté. Lancez VS Code tout d’abord, puis connectez hello DevKit tooyour ordinateur. VS Code le détecte automatiquement et ouvre une page d’introduction :

![mini-solution-vscode](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-vscode.png)

> [!NOTE] 
Au lancement de VS Code, il peut arriver qu’une erreur s’affiche, indiquant que l’IDE Arduino ou un package de carte associé est introuvable. toosolve il, fermez Visual Studio Code, relancez Arduino IDE qu’une seule fois et VS Code doivent localiser les chemin d’accès Arduino IDE correctement.

### <a name="open-arduino-examples-folder"></a>Ouvrir le dossier des exemples Arduino

Basculer trop**'Exemples Arduino'** onglet, accédez trop`Examples for MXCHIP AZ3166 > AzureIoT` , puis cliquez sur `GetStarted`.

![mini-solution-exemples](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-examples.png)

Si vous vous trouvez le volet de hello tooclose, tooreload il, utilisez `Ctrl+Shift+P` (macOS : `Cmd+Shift+P`) la palette et le type de commande tooinvoke **Arduino** toofind et sélectionnez **Arduino : exemples**.

## <a name="provision-azure-services"></a>Approvisionner les services Azure

Dans la fenêtre de solution hello, exécuter la tâche `Ctrl+P` (macOS : `Cmd+P`) en tapant la configuration cloud de la tâche :

Bonjour VS Code Terminal Server, qu'une ligne de commande interactive vous guide dans la configuration hello requis des services Azure :

![mini-solution-approvisionnement-cloud](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/cloud-provision.png)

## <a name="build-and-upload-arduino-sketch"></a>Générer et charger un croquis Arduino

### <a name="install-required-library"></a>Installer la bibliothèque requise

1. Appuyez sur `F1` ou `Ctrl+Shift+P` (macOS : `Cmd+Shift+P`) la palette et le type de commande tooinvoke **Arduino** puis recherchez et sélectionnez **Arduino : le Gestionnaire de bibliothèque**.

2. Recherchez la bibliothèque `ArduinoJson` et cliquez sur **Installer**.

### <a name="build-and-upload-hello-device-code"></a>Générer et télécharger le code de périphérique hello

Utilisez `Ctrl+P` (macOS : `Cmd+P`) toorun 'appareil tâche-téléchargement'. Hello Terminal Server vous invite à vous tooenter en mode de configuration. toodo, maintenez enfoncée la touche bouton A, puis hello par émission de données et de mise en production de bouton Réinitialiser. écran Hello affiche « Configuration ». Il s’agit de chaîne de connexion de hello tooset récupère à partir de l’étape de « cloud-configuration de tâche ».

Ensuite, il démarre vérification et téléchargement esquisse de Arduino hello :

![mini-solution-chargement-appareil](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/device-upload.png)

Kit de développement de Hello redémarre et démarrer l’exécution du code de hello.

## <a name="test-hello-project"></a>Projet de test hello

Dans le Code de Visual Studio, cliquez sur icône plug hello sur la barre tooopen hello série moniteur d’état hello.

exemple d’application Hello est en cours d’exécution avec succès lorsque vous consultez hello suivant des résultats :

* Hello moniteurs série hello mêmes informations en tant que contenu hello dans hello capture d’écran ci-dessous.
* Hello LED sur le Kit de développement MXChip IoT clignote.

![Sortie finale dans VS Code](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/result-serial-output.png)

## <a name="problems-and-feedback"></a>Problèmes et commentaires

Vous pouvez trouver [FAQ](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) si vous rencontrez des problèmes ou contacter toous à partir de canaux hello ci-dessous.

## <a name="next-steps"></a>Étapes suivantes

Vous êtes connecté avec succès un tooyour du Kit de développement MXChip IoT IoT Hub et envoyé hello capturé tooyour IoT hub capteur données.

toocontinue mise en route avec IoT Hub et tooexplore autres scénarios IoT, consultez :

- [Gérer la messagerie de périphérique cloud avec iothub-explorer](https://docs.microsoft.com/azure/iot-hub/iot-hub-explorer-cloud-device-messaging)
- [Enregistrer les messages IoT Hub tooAzure le stockage de données](https://docs.microsoft.com//azure/iot-hub/iot-hub-store-data-in-azure-table-storage)
- [Utiliser des données de capteur en temps réel toovisualize Power BI à partir d’Azure IoT Hub](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-power-bi)
- [Utiliser des données de capteur en temps réel toovisualize Azure Web Apps dans Azure IoT Hub](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-web-apps)
- [Prévisions météorologiques à l’aide des données de capteur hello à partir de votre hub IoT dans Azure Machine Learning](https://docs.microsoft.com/azure/iot-hub/iot-hub-weather-forecast-machine-learning)
- [Gestion des appareils avec iothub-explorer](https://docs.microsoft.com/azure/iot-hub/iot-hub-device-management-iothub-explorer)
- [Surveillance à distance et notifications avec Logic Apps](https://docs.microsoft.com/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps)