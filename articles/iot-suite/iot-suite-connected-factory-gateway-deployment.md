---
title: "aaaDeploy votre Azure IoT Suite connecté passerelle de fabrique | Documents Microsoft"
description: "Comment toodeploy une passerelle sur Windows ou Linux toohello de connectivité tooenable connectées fabrique de solution préconfigurée."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: dobett
ms.openlocfilehash: 72436dec60eda0de20143f362fe740b0c4412f36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-gateway-on-windows-or-linux-for-hello-connected-factory-preconfigured-solution"></a>Déployer une passerelle sur Windows ou Linux pour la solution de fabrique préconfiguré hello connecté

Hello logiciels requis toodeploy une passerelle pour hello connecté fabrique préconfiguré solution comporte deux composants :

* Hello *OPC Proxy* établit une connexion de tooIoT Hub. Hello *OPC Proxy* puis attend des messages de contrôle et commande de hello intégré OPC navigateur qui s’exécute dans le portail de solution hello fabrique connecté.
* Hello *OPC Publisher* se connecte tooexisting par OPC UA serveurs locaux et transfère les messages de télémétrie à partir de ces tooIoT Hub.

Les deux composants sont open source et disponibles en tant que sources sur GitHub et en tant que conteneurs Docker :

| GitHub | DockerHub |
| ------ | --------- |
| [Éditeur d’OPC][lnk-publisher-github] | [Éditeur d’OPC][lnk-publisher-docker] |
| [Proxy OPC][lnk-proxy-github] | [Proxy OPC][lnk-proxy-docker] |

Aucune adresse IP ou trous dans le pare-feu passerelle hello publique ne sont requis pour un composant. Hello OPC Proxy et serveur de publication OPC utilisent uniquement les ports sortants 443, 5671 et 8883.

Hello étapes décrites dans cet article vous montrent comment toodeploy une passerelle à l’aide de Docker soit [Windows](#windows-deployment) ou [Linux](#linux-deployment). passerelle de Hello permet la solution de connectivité toohello connecté fabrique préconfiguré.

> [!NOTE]
> logiciel de la passerelle Hello qui s’exécute dans le conteneur Docker de hello est [Azure IoT Edge].

## <a name="windows-deployment"></a>Déploiement sous Windows

> [!NOTE]
> Si vous ne possédez pas encore de passerelle, Microsoft vous recommande d’acheter une passerelle disponible dans le commerce auprès de l’un de nos partenaires. Visitez hello [catalogue de périphérique Azure IoT] pour obtenir la liste de périphériques de la passerelle compatibles avec hello connecté solution de fabrique. Suivez les instructions de hello qui accompagnent hello des tooset de périphérique de passerelle de hello. Vous pouvez également utiliser hello suivant toomanually instructions définir l’une de vos passerelles existants.

### <a name="install-docker"></a>Installation de Docker

Installez [Docker pour Windows] sur votre passerelle basée sur Windows. Pendant l’installation de Windows Docker, sélectionnez un lecteur sur votre tooshare d’ordinateur hôte avec Docker. Hello ci-dessous illustre d’écran lecteur hello D sur votre système Windows de partage :

![Installation de Docker][img-install-docker]

Puis créez un dossier appelé **docker** à racine hello hello le lecteur partagé.
Vous pouvez également effectuer cette étape après l’installation de docker à partir de hello **paramètres** menu.

### <a name="configure-hello-gateway"></a>Configurer la passerelle de hello

1. Vous devez hello **iothubowner** chaîne de connexion de votre Azure IoT Suite connecté fabrique toocomplete hello passerelle un déploiement. Bonjour [portail Azure], accédez tooyour IoT Hub du groupe de ressources hello créé lorsque vous avez déployé la solution de fabrique hello connecté. Cliquez sur **les stratégies d’accès partagé** tooaccess hello **iothubowner** chaîne de connexion :

    ![Recherche hello chaîne de connexion IoT Hub][img-hub-connection]

    Hello de copie **chaîne de connexion--clé primaire** valeur.

1. Configurer la passerelle de hello pour votre IoT Hub en exécutant des modules de passerelle hello deux **une fois** à partir d’une invite de commandes avec :

    `docker run -it --rm -h <ApplicationName> -v //D/docker:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/CertificateStores -v //D/docker:/root/.dotnet/corefx/cryptography/x509stores microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName> "<IoTHubOwnerConnectionString>"`

    `docker run -it --rm -v //D/docker:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -i -c "<IoTHubOwnerConnectionString>" -D /mapped/cs.db`

    * **&lt;ApplicationName&gt;**  est hello nom toogive tooyour OPC UA Publisher au format de hello **publisher.&lt; votre nom de domaine complet&gt;**. Par exemple, si votre réseau de la fabrique est appelée **myfactorynetwork.com**, hello **ApplicationName** valeur est **publisher.myfactorynetwork.com**.
    * **&lt;IoTHubOwnerConnectionString&gt;**  est hello **iothubowner** chaîne de connexion que vous avez copié à l’étape précédente de hello. Cette chaîne de connexion est utilisée uniquement dans cette étape, vous n’en avez pas besoin de hello comme suit :

    Vous utilisez hello mappé D:\\dossier docker (hello `-v` argument) toopersist ultérieure hello deux certificats X.509 qui utilisent des modules de passerelle hello.

### <a name="run-hello-gateway"></a>Exécuter hello passerelle

1. Redémarrez la passerelle hello hello suivant les commandes à l’aide de :

    `docker run -it --rm -h <ApplicationName> --expose 62222 -p 62222:62222 -v //D/docker:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/Logs -v //D/docker:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/CertificateStores -v //D/docker:/shared -v //D/docker:/root/.dotnet/corefx/cryptography/x509stores -e _GW_PNFP="/shared/publishednodes.JSON" microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName>`

    `docker run -it --rm -v //D/docker:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -D /mapped/cs.db`

1. Pour des raisons de sécurité, des certificats X.509 hello deux persistant Bonjour D:\\dossier docker contiennent la clé privée de hello. Limiter l’accès toothis dossier toohello informations d’identification (généralement **administrateurs**) vous utilisez le conteneur de Docker toorun hello. Avec le bouton hello D:\\dossier docker, choisissez **propriétés**, puis **sécurité**, puis **modifier**. Donnez aux **Administrateurs** le contrôle total, et supprimez tous les autres utilisateurs :

    ![Partage de tooDocker autorisations GRANT][img-docker-share]

1. Vérifiez la connectivité du réseau. À partir d’une invite de commandes, entrez la commande hello `ping publisher.<your fully qualified domain name>` tooping votre passerelle. Si la destination hello est inaccessible, ajouter l’adresse IP de hello et le nom de votre fichier d’hôtes toohello gateway sur votre passerelle. fichier d’hôtes Hello se trouve dans hello **Windows\\System32\\pilotes\\etc.** dossier.

1. Ensuite, essayez de serveur de publication de toohello tooconnect à l’aide d’un client OPC UA local en cours d’exécution sur la passerelle hello. Hello OPC UA point de terminaison URL `opc.tcp://publisher.<your fully qualified domain name>:62222`. Si vous n’avez pas de client OPC UA, vous pouvez télécharger un [client OPC UA open source].

1. Lorsque vous avez terminé ces tests en locales, accédez à toohello **connecter votre propre serveur d’agent utilisateur OPC** page du portail de solution hello fabrique connecté. Entrez l’URL de point de terminaison de serveur de publication hello (`tcp://publisher.<your fully qualified domain name>:62222`) et cliquez sur **connexion**. Vous obtenez un avertissement de certificat ; cliquez sur **Continuer.** Ensuite vous obtenez une erreur que hello hello UA Web Client n’approuve pas serveur de publication. tooresolve cette erreur, le hello de copie **UA Web Client** certificat à partir de hello **D:\\docker\\a rejeté les certificats\\certificats** dossier toohello **D:\\docker\\UA Applications\\certificats** dossier sur la passerelle hello. Vous n’avez pas besoin de toorestart de passerelle de hello. Répétez cette étape. Vous pouvez maintenant vous connecter toohello passerelle de cloud de hello, et vous êtes prêt tooadd solution de toohello OPC UA serveurs.

### <a name="add-your-opc-ua-servers"></a>Ajouter vos serveurs OPC UA

1. Parcourir toohello **connecter votre propre serveur d’agent utilisateur OPC** page du portail de solution hello fabrique connecté. Suivez hello mêmes étapes que dans hello précédant la section tooestablish approbation entre hello du portail de la fabrique connecté et hello du serveur de OPC UA. Cette étape établit une approbation mutuelle des certificats hello de hello connecté portail de la fabrique et hello server de OPC UA et crée une connexion.

1. Parcourir l’arborescence de nœuds OPC UA de votre serveur OPC UA de hello, cliquez sur les nœuds OPC hello et sélectionnez **publier**. Pour la publication toowork de cette façon, hello server de OPC UA et serveur de publication hello doit se trouver sur hello même réseau. En d’autres termes, si hello complet nom de domaine du serveur de publication hello est **publisher.mydomain.com** ensuite le nom de domaine complet de hello Hello OPC UA serveur doit être, par exemple, **myopcuaserver.mydomain.com**. Si votre programme d’installation est différente, vous pouvez ajouter manuellement des nœuds toohello publishesnodes.json fichier dans hello **D:\\docker** dossier. Hello publishesnodes.json fichier est généré automatiquement sur hello tout d’abord réussie d’un nœud OPC de publication.

1. Télémétrie circulent maintenant à partir de la passerelle hello. Vous pouvez afficher les données de télémétrie hello Bonjour **Factory Locations** affichage du portail de fabrique connecté hello sous **nouvelle fabrique**.

## <a name="linux-deployment"></a>Déploiement sous Linux

> [!NOTE]
> Si vous ne possédez pas encore de passerelle, Microsoft vous recommande d’acheter une passerelle disponible dans le commerce auprès de l’un de nos partenaires. Visitez hello [catalogue de périphérique Azure IoT] pour obtenir la liste de périphériques de la passerelle compatibles avec hello connecté solution de fabrique. Suivez les instructions de hello qui accompagnent hello des tooset de périphérique de passerelle de hello. Vous pouvez également utiliser hello suivant toomanually instructions définir l’une de vos passerelles existants.

[Installez Docker] sur votre passerelle Linux.

### <a name="configure-hello-gateway"></a>Configurer la passerelle de hello

1. Vous devez hello **iothubowner** chaîne de connexion de votre Azure IoT Suite connecté fabrique toocomplete hello passerelle un déploiement. Bonjour [portail Azure], accédez tooyour IoT Hub du groupe de ressources hello créé lorsque vous avez déployé la solution de fabrique hello connecté. Cliquez sur **les stratégies d’accès partagé** tooaccess hello **iothubowner** chaîne de connexion :

    ![Recherche hello chaîne de connexion IoT Hub][img-hub-connection]

    Hello de copie **chaîne de connexion--clé primaire** valeur.

1. Configurer la passerelle de hello pour votre IoT Hub en exécutant des modules de passerelle hello deux **une fois** à partir d’un interpréteur de commandes avec :

    `sudo docker run -it --rm -h <ApplicationName> -v /shared:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/ -v /shared:/root/.dotnet/corefx/cryptography/x509stores microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName> "<IoTHubOwnerConnectionString>"`

    `sudo docker run --rm -it -v /shared:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -i -c "<IoTHubOwnerConnectionString>" -D /mapped/cs.db`

    * **&lt;ApplicationName&gt;**  hello désigne hello OPC UA application hello passerelle crée dans le format de hello **publisher.&lt; votre nom de domaine complet&gt;**. Par exemple, **publisher.microsoft.com**.
    * **&lt;IoTHubOwnerConnectionString&gt;**  est hello **iothubowner** chaîne de connexion que vous avez copié à l’étape précédente de hello. Cette chaîne de connexion est utilisée uniquement dans cette étape, vous n’en avez pas besoin de hello comme suit :

    Vous utilisez hello **/ shared** dossier (hello `-v` argument) toopersist ultérieure hello deux certificats X.509 qui utilisent des modules de passerelle hello.

### <a name="run-hello-gateway"></a>Exécuter hello passerelle

1. Redémarrez la passerelle hello hello suivant les commandes à l’aide de :

    `sudo docker run -it -h <ApplicationName> --expose 62222 -p 62222:62222 –-rm -v /shared:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/Logs -v /shared:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/CertificateStores -v /shared:/shared -v /shared:/root/.dotnet/corefx/cryptography/x509stores -e _GW_PNFP="/shared/publishednodes.JSON" microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName>`

    `sudo docker run -it -v /shared:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -D /mapped/cs.db`

1. Pour des raisons de sécurité, des certificats X.509 hello deux persistant Bonjour **/ shared** dossier contient la clé privée de hello. Limite l’accès toothis dossier toohello informations d’identification vous utilisez toorun hello conteneur Docker. autorisations hello tooset **racine** uniquement, utilisez hello `chmod` d’interpréteur de commandes sur le dossier de hello.

1. Vérifiez la connectivité du réseau. À partir d’un interpréteur de commandes, entrez la commande hello `ping publisher.<your fully qualified domain name>` tooping votre passerelle. Si la destination hello est inaccessible, ajouter l’adresse IP de hello et le nom de votre fichier d’hôtes tooyour gateway sur votre passerelle. fichier d’hôtes Hello se trouve dans hello **etc.** dossier.

1. Ensuite, essayez de serveur de publication de toohello tooconnect à l’aide d’un client OPC UA local en cours d’exécution sur la passerelle hello. Hello OPC UA point de terminaison URL `opc.tcp://publisher.<your fully qualified domain name>:62222`. Si vous n’avez pas de client OPC UA, vous pouvez télécharger un [client OPC UA open source].

1. Lorsque vous avez terminé ces tests en locales, accédez à toohello **connecter votre propre serveur d’agent utilisateur OPC** page du portail de solution hello fabrique connecté. Entrez l’URL de point de terminaison de serveur de publication hello (`tcp://publisher.<your fully qualified domain name>:62222`) et cliquez sur **connexion**. Vous obtenez un avertissement de certificat ; cliquez sur **Continuer.** Ensuite vous obtenez une erreur que hello hello UA Web Client n’approuve pas serveur de publication. tooresolve cette erreur, le hello de copie **UA Web Client** certificat à partir de hello **partagés/rejeté certificats/certificats** dossier toohello **/shared/UA Applications/certificats** dossier sur la passerelle hello. Vous n’avez pas besoin de toorestart de passerelle de hello. Répétez cette étape. Vous pouvez maintenant vous connecter toohello passerelle de cloud de hello, et vous êtes prêt tooadd solution de toohello OPC UA serveurs.

### <a name="add-your-opc-ua-servers"></a>Ajouter vos serveurs OPC UA

1. Parcourir toohello **connecter votre propre serveur d’agent utilisateur OPC** page du portail de solution hello fabrique connecté. Suivez hello mêmes étapes que dans hello précédant la section tooestablish approbation entre hello du portail de la fabrique connecté et hello du serveur de OPC UA. Cette étape établit une approbation mutuelle des certificats hello de hello connecté portail de la fabrique et hello server de OPC UA et crée une connexion.

1. Parcourir l’arborescence de nœuds OPC UA de votre serveur OPC UA de hello, cliquez sur les nœuds OPC hello et sélectionnez **publier**. Pour la publication toowork de cette façon, hello server de OPC UA et serveur de publication hello doit se trouver sur hello même réseau. En d’autres termes, si hello complet nom de domaine du serveur de publication hello est **publisher.mydomain.com** ensuite le nom de domaine complet de hello Hello OPC UA serveur doit être, par exemple, **myopcuaserver.mydomain.com**. Si votre programme d’installation est différente, vous pouvez ajouter manuellement des nœuds toohello publishesnodes.json fichier dans hello **/ shared** dossier. Hello publishesnodes.json est automatiquement générée sur hello tout d’abord réussie d’un nœud OPC de publication.

1. Télémétrie circulent maintenant à partir de la passerelle hello. Vous pouvez afficher les données de télémétrie hello Bonjour **Factory Locations** affichage du portail de fabrique connecté hello sous **nouvelle fabrique**.

## <a name="next-steps"></a>Étapes suivantes

solution préconfigurée de toolearn plus sur l’architecture de hello de fabrique de hello connecté, consultez [fabrique connecté préconfiguré procédure pas à pas de solution][lnk-walkthrough].

[img-install-docker]: ./media/iot-suite-connected-factory-gateway-deployment/image1.png
[img-hub-connection]: ./media/iot-suite-connected-factory-gateway-deployment/image2.png
[img-docker-share]: ./media/iot-suite-connected-factory-gateway-deployment/image3.png

[Docker pour Windows]: https://www.docker.com/docker-windows
[catalogue de périphérique Azure IoT]: https://catalog.azureiotsuite.com/?q=opc
[portail Azure]: http://portal.azure.com/
[client OPC UA open source]: https://github.com/OPCFoundation/UA-.NETStandardLibrary/tree/master/SampleApplications/Samples/Client.Net4
[Installez Docker]: https://www.docker.com/community-edition#/download
[lnk-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[Azure IoT Edge]: https://github.com/Azure/iot-edge

[lnk-publisher-github]: https://github.com/Azure/iot-edge-opc-publisher
[lnk-publisher-docker]: https://hub.docker.com/r/microsoft/iot-gateway-opc-ua
[lnk-proxy-github]: https://github.com/Azure/iot-edge-opc-proxy
[lnk-proxy-docker]: https://hub.docker.com/r/microsoft/iot-gateway-opc-ua-proxy