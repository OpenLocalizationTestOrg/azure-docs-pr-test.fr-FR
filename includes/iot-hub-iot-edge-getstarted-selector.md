> [!div class="op_single_selector"]
> * [Linux](../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md)
> * [Windows](../articles/iot-hub/iot-hub-windows-iot-edge-get-started.md)
> 
> 

Cet article fournit une description détaillée de hello [exemple de code Hello World] [ lnk-helloworld-sample] composants fondamentaux de hello tooillustrate Hello [Azure IoT bord] [ lnk-iot-edge] architecture. Hello utilise hello Azure IoT bord toobuild une passerelle simple qui se connecte à un fichier de tooa de message « hello world » toutes les cinq secondes.

Cette procédure pas à pas inclut les étapes suivantes :

* **Hello exemple d’architecture World**: décrit comment [concepts d’architecture Azure IoT bord] [ lnk-edge-concepts] appliquer l’exemple Hello World de toohello et comment les composants de hello ensemble.
* **Comment toobuild hello exemple**: hello, exemple hello étapes toobuild requis.
* **Comment toorun hello exemple**: hello, exemple hello étapes toorun requis. 
* **Exemple de résultat**: un exemple Hello tooexpect de sortie lorsque vous exécutez l’exemple hello.
* **Extraits de code**: une collection de tooshow d’extraits de code comment hello Hello World (exemple) implémente les composants de passerelle de IoT bord clés.


## <a name="hello-world-sample-architecture"></a>Exemple d'architecture Hello World
exemple Hello Hello World illustre les concepts de hello décrites dans la section précédente de hello. exemple Hello Hello World implémente une passerelle IoT dispose d’un pipeline composé de deux modules de IoT bord :

* Hello *Bonjour* module crée un message toutes les cinq secondes et le passe module du journal toohello.
* Hello *journal* module écrit les messages hello réception tooa fichier.

![Architecture de l’exemple Hello World conçu avec Azure IoT Edge][4]

Comme décrit dans la section précédente de hello, hello World Hello module ne passe pas directement toohello journal module messages toutes les cinq secondes. Au lieu de cela, elle publie le message broker toohello toutes les cinq secondes.

module d’enregistreur d’événements Hello reçoit un message de type hello à partir du service broker de hello et agit sur, écriture du contenu hello du fichier de tooa message hello.

module d’enregistreur d’événements Hello utilise uniquement les messages de service broker de hello, il publie jamais service Broker pour les nouveaux messages toohello.

![Comment hello broker route les messages entre les modules dans Azure IoT Edge][5]

Hello figure ci-dessus illustre hello architecture de hello Hello World (exemple) et les chemins d’accès relatifs hello fichiers toohello sources qui implémentent différentes parties de l’exemple hello Bonjour [référentiel][lnk-iot-edge]. Explorer le code de hello vous-même, ou utiliser des extraits de code hello ci-dessous comme guide.

<!-- Images -->
[4]: media/iot-hub-iot-edge-getstarted-selector/high_level_architecture.png
[5]: media/iot-hub-iot-edge-getstarted-selector/detailed_architecture.png

<!-- Links -->
[lnk-helloworld-sample]: https://github.com/Azure/iot-edge/tree/master/samples/hello_world
[lnk-iot-edge]: https://github.com/Azure/iot-edge
[lnk-edge-concepts]: ../articles/iot-hub/iot-hub-iot-edge-overview.md