---
title: "aaaConnect un appareil à l’aide de C sur mbed | Documents Microsoft"
description: "Décrit comment tooconnect un toohello appareil Azure IoT Suite préconfiguré solution d’analyse à distance à l’aide d’une application écrite en C en cours d’exécution sur un appareil mbed."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 9551075e-dcf9-488f-943e-d0eb0e6260be
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: dobett
ROBOTS: NOINDEX
ms.openlocfilehash: dcd1e74635e8dec678a59bff060a73f7cfabd124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-mbed"></a>Se connecter à votre solution préconfigurée (mbed) de surveillance à distance de toohello périphérique

## <a name="scenario-overview"></a>Présentation du scénario
Dans ce scénario, vous créez un périphérique qui envoie hello suivant la surveillance à distance de télémétrie toohello [solution préconfigurée][lnk-what-are-preconfig-solutions]:

* Température externe
* Température interne
* Humidité

Par souci de simplicité, code hello sur l’appareil de hello génère des exemples de valeurs, mais nous encourageons exemple hello tooextend par connexion réelle capteurs tooyour appareil et l’envoi de télémétrie réel.

Hello appareil est également en mesure de toorespond toomethods appelée à partir du tableau de bord de solution hello et souhaitée des valeurs de propriété définies dans le tableau de bord de solution hello.

toocomplete ce didacticiel, vous avez besoin d’un compte Azure actif. Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes. Pour plus d’informations, consultez la rubrique [Version d’évaluation gratuite d’Azure][lnk-free-trial].

## <a name="before-you-start"></a>Avant de commencer
Avant d’écrire du code pour votre appareil, vous devez approvisionner votre solution préconfigurée de surveillance à distance et approvisionner un nouvel appareil personnalisé dans cette solution.

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a>Approvisionner la solution préconfigurée de surveillance à distance
APPAREIL Hello vous créez dans ce didacticiel envoie instance tooan de données de hello [surveillance à distance] [ lnk-remote-monitoring] solution préconfigurée. Si vous n’avez pas déjà configuré hello solution préconfigurée dans votre compte Azure de surveillance à distance, utilisez hello comme suit :

1. Sur hello <https://www.azureiotsuite.com/> , cliquez sur  **+**  toocreate une solution.
2. Cliquez sur **sélectionnez** sur hello **surveillance à distance** panneau toocreate votre solution.
3. Sur hello **créer distant solutions d’analyse** , entrez un **nom de la Solution** de votre choix, sélectionnez hello **région** vous le souhaitez toodeploy à et sélectionnez hello Azure abonnement toowant toouse. Cliquez ensuite sur **Créer la solution**.
4. Attendez que hello processus de configuration est terminée.

> [!WARNING]
> les solutions de Hello préconfiguré utilisent les services Azure facturables. Veillez tooremove hello solution préconfigurée à partir de votre abonnement lorsque vous avez terminé avec lui tooavoid tous les frais inutiles. Vous pouvez supprimer complètement une solution préconfigurée de votre abonnement en visitant hello <https://www.azureiotsuite.com/> page.
> 
> 

Lorsque hello processus pour hello solution de surveillance à distance de configuration est terminée, cliquez sur **lancer** tooopen hello solution tableau de bord dans votre navigateur.

![Tableau de bord de solution][img-dashboard]

### <a name="provision-your-device-in-hello-remote-monitoring-solution"></a>Configurer votre appareil dans la solution de surveillance à distance de hello
> [!NOTE]
> Si vous avez déjà approvisionné un appareil dans votre solution, vous pouvez ignorer cette étape. Vous avez besoin d’informations d’identification de périphérique tooknow hello lorsque vous créez l’application cliente de hello.
> 
> 

Pour une solution toohello préconfiguré tooconnect des appareils, il doit s’identifier tooIoT concentrateur à l’aide des informations d’identification valides. Vous pouvez récupérer les informations d’identification de périphérique hello à partir du tableau de bord de solution hello. Pour inclure des informations d’identification de périphérique hello dans votre application cliente, plus loin dans ce didacticiel.

tooadd une solution d’analyse à distance tooyour périphérique, hello complet suivant les étapes dans le tableau de bord de solution hello :

1. Dans hello coin inférieur gauche du tableau de bord hello, cliquez sur **ajouter un périphérique**.
   
   ![Ajout d’un appareil][1]
2. Bonjour **personnalisé appareil** du panneau, cliquez sur **ajouter un nouveau**.
   
   ![Ajout d’un appareil personnalisé][2]
3. Choisissez **Me laisser définir mon propre ID d'appareil**. Entrez un ID de périphérique tel **mydevice**, cliquez sur **vérifier l’ID** tooverify ce nom n’est pas déjà en cours d’utilisation, puis cliquez sur **créer** appareil de hello tooprovision.
   
   ![Ajouter ID d’appareil][3]
4. Rendre un périphérique de hello de note les informations d’identification (ID de périphérique, nom d’hôte du Hub IoT et clé de périphérique). Votre application cliente doit ces toohello tooconnect de valeurs solution de surveillance à distance. Cliquez ensuite sur **Terminé**.
   
    ![Afficher les informations d’identification d’un appareil][4]
5. Sélectionnez votre appareil dans la liste des appareils hello dans le tableau de bord de solution hello. Ensuite, dans hello **détails de l’appareil** du panneau, cliquez sur **activer le périphérique**. Hello de votre appareil est maintenant **en cours d’exécution**. solution de surveillance à distance Hello peut maintenant recevoir les données de télémétrie à partir de votre appareil et d’appeler des méthodes sur l’appareil de hello.

[img-dashboard]: ./media/iot-suite-connecting-devices-mbed/dashboard.png
[1]: ./media/iot-suite-connecting-devices-mbed/suite0.png
[2]: ./media/iot-suite-connecting-devices-mbed/suite1.png
[3]: ./media/iot-suite-connecting-devices-mbed/suite2.png
[4]: ./media/iot-suite-connecting-devices-mbed/suite3.png

[lnk-what-are-preconfig-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

## <a name="build-and-run-hello-c-sample-solution"></a>Générer et exécuter l’exemple de solution hello C

Hello instructions suivantes décrivent les étapes de hello pour se connecter une [compatible mbed Freescale FRDM-K64F] [ lnk-mbed-home] toohello du périphérique distant solutions d’analyse.

### <a name="connect-hello-mbed-device-tooyour-network-and-desktop-machine"></a>Connexion réseau de tooyour hello mbed périphérique et ordinateur de bureau

1. Connecter hello mbed périphérique tooyour réseau à l’aide d’un câble Ethernet. Cette étape est nécessaire, car l’application d’exemple hello requiert un accès internet.

1. Consultez [prise en main de mbed] [ lnk-mbed-getstarted] tooconnect votre PC de bureau tooyour mbed appareil.

1. Si votre ordinateur de bureau exécutant Windows, consultez [Configuration PC] [ lnk-mbed-pcconnect] dispositif de mbed tooyour accès tooconfigure port série.

### <a name="create-an-mbed-project-and-import-hello-sample-code"></a>Créer un projet de mbed et importer les exemples de code hello

Suivez ces tooadd étapes certains exemple de projet mbed de tooan code. Vous importez le projet de démarrage d’analyse à distance hello et modifiez hello toouse de projet hello protocole MQTT au lieu de hello protocole AMQP. Actuellement, vous devez toouse hello MQTT protocole toouse hello appareil fonctionnalités de gestion d’IoT Hub.

1. Dans votre navigateur web, accédez à toohello mbed.org [site de développement](https://developer.mbed.org/). Si vous n’avez pas encore inscrit, vous consultez un toocreate option un compte (il est disponible). Autrement, connectez-vous avec les informations d’identification de votre compte. Puis cliquez sur **compilateur** dans hello coin supérieur droit de la page de hello. Cette action entraîne un toohello *espace de travail* interface.

1. Assurez-vous que la plateforme matérielle de hello vous utilisez s’affiche dans le coin supérieur droit hello de fenêtre hello ou cliquez sur icône hello dans hello à droite tooselect votre plateforme matérielle.

1. Cliquez sur **importation** sur le menu principal de hello. Puis cliquez sur **cliquez ici tooimport à partir de l’URL**.
   
    ![Espace de travail de démarrage importation toombed][6]

1. Dans la fenêtre contextuelle de hello, entrez le lien de hello pour hello exemple code https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/ puis cliquez sur **importation**.
   
    ![Importer l’espace de travail exemple code toombed][7]

1. Dans la fenêtre de compilateur hello mbed, vous pouvez voir que l’importation de ce projet importe également les différentes bibliothèques. Certaines sont fournies et gérées par l’équipe de Azure IoT hello ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), tandis que d’autres sont des bibliothèques tierces disponibles dans le catalogue de bibliothèques mbed hello.
   
    ![Afficher le projet mbed][8]

1. Bonjour **espace de travail de programme**, avec le bouton hello **iothub\_amqp\_transport** bibliothèque, cliquez sur **supprimer**, puis cliquez sur **OK** tooconfirm.

1. Bonjour **espace de travail de programme**, avec le bouton hello **azure\_amqp\_c** bibliothèque, cliquez sur **supprimer**, puis cliquez sur **OK**  tooconfirm.

1. Avec le bouton hello **remote_monitoring** projet Bonjour **espace de travail de programme**, sélectionnez **bibliothèque d’importation**, puis sélectionnez **From URL**.
   
    ![Démarrer l’espace de travail bibliothèque importation toombed][6]

1. Dans la fenêtre contextuelle de hello, entrez le lien de hello pour hello MQTT transport bibliothèque https://developer.mbed.org/users/AzureIoTClient/code/iothub\_mqtt\_transport / puis cliquez sur **importation**.
   
    ![Importer l’espace de travail bibliothèque toombed][12]

1. Répétition hello étape tooadd hello MQTT bibliothèque précédente à partir de https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c /.

1. Votre espace de travail se présente désormais comme hello ci-après :

    ![Afficher l’espace de travail mbed][13]

1. Hello ouvrir à distance\_monitoring\remote_monitoring.c fichier et qui n’existe hello remplacer `#include` instructions avec hello suivant de code :

    ```c
    #include "iothubtransportmqtt.h"
    #include "schemalib.h"
    #include "iothub_client.h"
    #include "serializer_devicetwin.h"
    #include "schemaserializer.h"
    #include "azure_c_shared_utility/threadapi.h"
    #include "azure_c_shared_utility/platform.h"
    #include "parson.h"

    #ifdef MBED_BUILD_TIMESTAMP
    #include "certs.h"
    #endif // MBED_BUILD_TIMESTAMP
    ```
1. Supprimer tous les hello code Bonjour à distance restant\_monitoring\remote\_monitoring.c fichier.

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a>Générer et exécuter l’exemple hello

Ajouter hello tooinvoke de code **distant\_analyse\_exécuter** fonction puis générer et exécuter l’application d’appareil hello.

1. Ajouter un **principal** fonction avec le code suivant à fin hello Hello distant\_hello de tooinvoke fichier monitoring.c **distant\_analyse\_exécuter** (fonction) :
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. Cliquez sur **compiler** programme de hello toobuild. Vous pouvez sans risque ignorer les avertissements, mais si la génération de hello génère des erreurs, corrigez-les avant de continuer.

1. Si la génération de hello est réussie, le site Web du compilateur hello mbed génère un fichier .bin nom hello de votre projet et le télécharge tooyour les ordinateur local. Copier hello .bin fichier toohello l’appareil. L’enregistrement d’unité de toohello de fichier .bin hello provoque hello appareil toorestart et exécuter le programme hello contenue dans le fichier .bin de hello. Vous pouvez redémarrer manuellement les programme hello à tout moment en appuyant sur bouton Rétablir de hello sur l’appareil de mbed hello.

1. Connecter l’appareil toohello utilise une application client SSH tel que PuTTY. Vous pouvez déterminer le port série de hello que votre appareil utilise en vérifiant le Gestionnaire de périphériques Windows.
   
    ![][11]

1. Dans PuTTY, cliquez sur hello **série** type de connexion. Appareil de Hello se connecte généralement à 9 600 bauds, entrez 9600 Bonjour **vitesse** boîte. Cliquez ensuite sur **Ouvrir**.

1. programme de Hello commence à s’exécuter. Vous avez peut-être tooreset (appuyez sur CTRL + ATTN ou réinitialisation du tableau de presse hello) de carte mère hello si hello programme ne démarre pas automatiquement lorsque vous vous connectez.
   
    ![][10]

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[6]: ./media/iot-suite-connecting-devices-mbed/mbed1.png
[7]: ./media/iot-suite-connecting-devices-mbed/mbed2a.png
[8]: ./media/iot-suite-connecting-devices-mbed/mbed3a.png
[10]: ./media/iot-suite-connecting-devices-mbed/putty.png
[11]: ./media/iot-suite-connecting-devices-mbed/mbed6.png
[12]: ./media/iot-suite-connecting-devices-mbed/mbed7.png
[13]: ./media/iot-suite-connecting-devices-mbed/mbed8.png

[lnk-mbed-home]: https://developer.mbed.org/platforms/FRDM-K64F/
[lnk-mbed-getstarted]: https://developer.mbed.org/platforms/FRDM-K64F/#getting-started-with-mbed
[lnk-mbed-pcconnect]: https://developer.mbed.org/platforms/FRDM-K64F/#pc-configuration
