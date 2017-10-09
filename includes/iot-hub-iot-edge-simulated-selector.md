> [!div class="op_single_selector"]
> * [Linux](../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md)
> * [Windows](../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md)

Cette procédure pas à pas de hello [Cloud d’appareil simulé télécharger l’exemple] vous montre comment toouse [Azure IoT bord] [ lnk-sdk] toosend appareil-à-cloud télémétrie tooIoT concentrateur de simulé appareils.

Cette procédure pas à pas inclut les étapes suivantes :

* **Architecture**: architecture informations hello [Cloud d’appareil simulé télécharger l’exemple].
* **Générez et exécutez**: toobuild de hello étapes requis et exemple hello d’exécution.

## <a name="architecture"></a>Architecture

Hello [Cloud d’appareil simulé télécharger l’exemple] montre comment toocreate une passerelle qui envoie les données de télémétrie des simulée IoT hub tooan de périphériques. Un périphérique n’est peut-être pas en mesure de tooconnect directement tooIoT Hub, car les périphériques hello :

* L’appareil n’utilise pas un protocole de communication compris par IoT Hub
* N’est pas assez intelligente tooremember hello identité attribuée tooit par IoT Hub.

Une passerelle IoT peut résoudre ces problèmes Bonjour suivant façons :

* passerelle de Hello comprend protocole hello utilisée par des appareils hello, reçoit les données de télémétrie appareil-à-cloud à partir de l’appareil de hello et transmet ces tooIoT messages concentrateur à l’aide d’un protocole compris par IoT hub de hello.

* passerelle de Hello mappe toodevices d’identités IoT Hub et agit comme un proxy lorsqu’un appareil envoie des messages tooIoT Hub.

Hello suivant schéma montre hello les principaux composants de l’exemple hello, y compris hello les modules IoT bord :

![][1]

les modules Hello ne passent pas de messages directement tooeach autres. les modules Hello publier des messages tooan interne service broker remet toohello de messages hello autres modules à l’aide d’un mécanisme d’abonnement. Pour plus d’informations, voir [Get started with Azure IoT Edge (Prise en main d’Azure IoT Edge)][lnk-gw-getstarted].

### <a name="protocol-ingestion-module"></a>Module d'ingestion de protocole

Ce module est hello point de départ pour recevoir des données à partir de périphériques, via la passerelle de hello et dans le cloud de hello. Dans l’exemple hello, hello module :

1. Crée les données de la température simulée. Si vous utilisez des périphériques physiques, module de hello lit les données à partir de ces périphériques physiques.
1. Crée un message.
1. Place les données de température hello simulé dans le contenu du message hello.
1. Ajoute une propriété avec un message factice de toohello d’adresse MAC.
1. Rend le module de hello message toohello disponible suivant dans la chaîne de hello.

module Hello appelé **ingestion de protocole X** Bonjour diagramme précédent est appelé **appareil simulé** dans le code source de hello.

### <a name="mac-lt-gt-iot-hub-id-module"></a>MAC &lt;-&gt; IoT Hub ID module

Ce module analyse les messages dotés d’une propriété d’adresse Mac. Dans l’exemple hello, module de réception du protocole hello ajoute la propriété d’adresse MAC hello. Si le module de hello détecte une telle propriété, il ajoute une autre propriété avec un message de clé toohello appareil IoT Hub. module de Hello rend ensuite le module de hello message toohello disponible suivant dans la chaîne de hello.

développement de Hello définit un mappage entre les adresses MAC et appareils de hello simulée IoT Hub identités tooassociate avec les identités des appareils IoT Hub. développeur de Hello ajoute manuellement le mappage de hello dans le cadre de la configuration du module hello.

> [!NOTE]
> Cet exemple utilise une adresse MAC comme identificateur unique de l'appareil et la met en corrélation avec une identité d'appareil IoT Hub. Toutefois, vous pouvez écrire votre propre module qui utilise un autre identificateur unique. Par exemple, vos appareils peuvent avoir des numéros de série uniques ou les données de télémétrie hello peuvent inclure un nom de périphérique intégré unique.

### <a name="iot-hub-communication-module"></a>Module de communication IoT Hub

Ce module prend les messages avec un IoT Hub propriété de clé de périphérique qui a été affectée par le module précédent de hello. module de Hello envoie un message de type hello tooIoT contenu concentrateur à l’aide de hello le protocole HTTP. HTTP est un des hello trois protocoles compris par IoT Hub.

Au lieu d’ouvrir une connexion pour chaque appareil simulé, ce module ouvre une connexion HTTP à partir de la toohello IoT hub hello passerelle. module de Hello multiplexage puis des connexions à partir de tous les appareils hello simulée sur cette connexion. Cette approche permet un tooconnect passerelle unique plus grand nombre d’appareils.

## <a name="before-you-get-started"></a>Avant de commencer

Avant de commencer, vous devez :

* [Créez un hub IoT] [ lnk-create-hub] dans votre abonnement Azure, vous devez fournir hello nom de votre concentrateur de toocomplete cette procédure pas à pas. Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.
* Ajouter deux périphériques tooyour IoT hub et prenez note de leur ID et les clés de l’appareil. Vous pouvez utiliser hello [Explorateur de périphérique] [ lnk-device-explorer] ou [iothub-explorer] [ lnk-iothub-explorer] outil tooadd votre concentrateur de IoT toohello périphériques vous avez créé dans hello précédente étape et récupérer leurs clés.

![][2]

<!-- Images -->
[1]: media/iot-hub-iot-edge-simulated-selector/image1.png
[2]: media/iot-hub-iot-edge-simulated-selector/image2.png

<!-- Links -->
[Cloud d’appareil simulé télécharger l’exemple]: https://github.com/Azure/iot-edge/blob/master/samples/simulated_device_cloud_upload/README.md
[lnk-sdk]: https://github.com/Azure/iot-edge
[lnk-gw-getstarted]: ../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md
[lnk-create-hub]: ../articles/iot-hub/iot-hub-create-through-portal.md