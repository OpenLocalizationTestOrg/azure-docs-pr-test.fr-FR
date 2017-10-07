---
title: "aaaAzure IoT Suite connecté fabrique FAQ | Documents Microsoft"
description: "Questions fréquentes sur l’usine connectée IoT Suite"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: 4ae9beb0daf1b0578850cd652eaca7635b0d039d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-iot-suite-connected-factory-preconfigured-solution"></a>Questions fréquentes sur la solution préconfigurée d’usine connectée IoT Suite

Voir aussi, hello général [FAQ](iot-suite-faq.md) pour IoT Suite.

### <a name="where-can-i-find-hello-source-code-for-hello-preconfigured-solution"></a>Où puis-je trouver code source de hello pour les solutions hello préconfiguré ?

code source de Hello est stocké dans hello suivant le dépôt GitHub :

* [Solution préconfigurée d’usine connectée](https://github.com/Azure/azure-iot-connected-factory)

### <a name="what-is-opc-ua"></a>Qu’est-ce que l’UA OPC ?

OPC UA (Unified Architecture) est un standard d’interopérabilité indépendant de la plateforme et orienté services, qui date de 2008. OPC UA est utilisé par différents systèmes et dispositifs industriels tels que les PC industriels, les automates programmables industriels et les capteurs. OPC UA intègre des fonctionnalités de hello de spécifications OPC classique de hello dans une infrastructure extensible avec la sécurité intégrée. Il est une norme est pilotée par hello OPC Foundation. Hello [OPC Foundation](http://opcfoundation.org/) est une organisation à but non lucratif avec plus de 440 membres. Hello organisation de hello vise toouse OPC spécifications toofacilitate hétérogène, multi-plateforme, sécurisée et fiable l’interopérabilité via :

* Infrastructure
* Spécifications
* Technology
* Processus

### <a name="why-did-microsoft-choose-opc-ua-for-hello-connected-factory-preconfigured-solution"></a>Pourquoi Microsoft choisi QU'UA OPC pour hello connecté solution de fabrique préconfiguré ?

Microsoft a choisi l’UA OPC, car il s’agit d’une norme ouverte, non propriétaire, ne dépendant pas d’une plateforme, reconnue par le secteur et éprouvée. Elle est exigée pour les solutions d’architecture de référence Industrie 4.0 (RAMI4.0) assurant l’interopérabilité entre un large ensemble de processus de fabrication et les équipements. Microsoft voit la demande à partir de notre toobuild Industrie 4.0 aux clients des solutions. Prise en charge des OPC UA permet inférieur barrière hello pour les clients tooachieve leurs objectifs et fournit le bénéfice immédiat valeur toothem.

### <a name="how-do-i-add-a-public-ip-address-toohello-simulation-vm"></a>Comment ajouter une simulation de toohello adresse IP publique machine virtuelle ?

Deux options tooadd hello l’adresse IP est :

* Utiliser un script PowerShell hello `Simulation/Factory/Add-SimulationPublicIp.ps1` Bonjour [référentiel](https://github.com/Azure/azure-iot-connected-factory). Passez le nom de votre déploiement en tant que paramètre. Pour un déploiement local, utilisez `<your username>ConnFactoryLocal`. script de Hello imprime hello adresseIP de hello machine virtuelle.

* Bonjour portail Azure, recherchez le groupe de ressources hello de votre déploiement. À l’exception d’un déploiement local, groupe de ressources hello a nom hello spécifié en tant que solution ou le nom du déploiement. Pour un déploiement local à l’aide du script de compilation hello, nom hello hello du groupe de ressources est `<your username>ConnFactoryLocal`. Ajoutez maintenant un nouveau **adresse IP publique** toohello groupe de ressources.

> [!NOTE]
> Dans les deux cas, assurez-vous d’installer correctifs les plus récents hello en suivant les instructions de hello de hello [site Web d’Ubuntu](https://wiki.ubuntu.com/Security/Upgrades). Gardez à l’installation hello toodate pour tant que votre machine virtuelle est accessible via une adresse IP publique.

### <a name="how-do-i-remove-hello-public-ip-address-toohello-simulation-vm"></a>Comment supprimer les hello publique IP adresse toohello simulation de machine virtuelle ?

Deux options tooremove hello l’adresse IP est :

* Utiliser un script PowerShell hello Simulation/Factory/Remove-SimulationPublicIp.ps1 Hello [référentiel](https://github.com/Azure/azure-iot-connected-factory). Passez le nom de votre déploiement en tant que paramètre. Pour un déploiement local, utilisez `<your username>ConnFactoryLocal`. script de Hello imprime hello adresseIP de hello machine virtuelle.

* Bonjour portail Azure, recherchez le groupe de ressources hello de votre déploiement. À l’exception d’un déploiement local, groupe de ressources hello a nom hello spécifié en tant que solution ou le nom du déploiement. Pour un déploiement local à l’aide du script de compilation hello, nom hello hello du groupe de ressources est `<your username>ConnFactoryLocal`. Supprimer hello **adresse IP publique** ressource du groupe de ressources hello.

### <a name="how-do-i-sign-in-toohello-simulation-vm"></a>Comment se connecter lors de la simulation de toohello machine virtuelle ?

Signature lors de la simulation de toohello machine virtuelle est uniquement prise en charge si vous avez déployé votre solution à l’aide du script PowerShell de hello `build.ps1` Bonjour [référentiel](https://github.com/Azure/azure-iot-connected-factory).

Si vous avez déployé la solution hello www.azureiotsuite.com, vous n’aurez toohello machine virtuelle. Vous ne pouvez pas connecter, car hello le mot de passe est généré de façon aléatoire et vous ne pouvez pas le réinitialiser.

1. Ajouter un toohello d’adresse IP publique machine virtuelle. Consultez [comment ajouter une simulation de toohello adresse IP publique machine virtuelle ?](#how-do-i-remove-the-public-ip-address-to-the-simulation-vm)
1. Créer un tooyour de session SSH machine virtuelle à l’aide d’adresse IP hello hello machine virtuelle.
1. toouse du nom d’utilisateur Hello est : `docker`.
1. toouse de mot de passe Hello dépend de la version de hello que vous avez utilisé toodeploy :
    * Pour les solutions déployées à l’aide du script de build.ps1 hello avant 1 juin 2017, mot de passe hello est : `Passw0rd`.
    * Pour les solutions déployées à l’aide du script de build.ps1 hello après 1 juin 2017, vous pouvez trouver le mot de passe hello Bonjour `<name of your deployment>.config.user` fichier. mot de passe Hello est stocké dans hello **VmAdminPassword** paramètre. Hello mot de passe est généré de manière aléatoire au moment du déploiement, sauf si vous spécifiez à l’aide de hello `build.ps1` paramètre de script`-VmAdminPassword`

### <a name="how-do-i-stop-and-start-all-docker-processes-in-hello-simulation-vm"></a>Comment arrêter et démarrer tous les processus docker lors de la simulation de hello machine virtuelle ?

1. Connectez-vous à la simulation toohello machine virtuelle. Consultez [comment se connecter lors de la simulation de toohello machine virtuelle ?](#how-do-i-sign-in-to-the-simulation-vm)
1. toocheck les conteneurs sont actifs, exécutez : `docker ps`.
1. l’exécution de tous les conteneurs de simulation, toostop : `./stopsimulation`.
1. toostart tous les conteneurs de simulation :
    * Exporter une variable d’environnement avec le nom de hello **IOTHUB_CONNECTIONSTRING**. Utilisez la valeur hello hello **IotHubOwnerConnectionString** paramètre Bonjour `<name of your deployment>.config.user` fichier. Par exemple :

        ```
        export IOTHUB_CONNECTIONSTRING="HostName={yourdeployment}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={your key}"
        ```

    * Exécutez `./startsimulation`.

### <a name="how-do-i-update-hello-simulation-in-hello-vm"></a>Comment mettre à jour la simulation hello Bonjour machine virtuelle ?

Si vous avez apporté des modifications toohello simulation, vous pouvez utiliser le script PowerShell de hello `build.ps1` Bonjour [référentiel](https://github.com/Azure/azure-iot-connected-factory) à l’aide de hello `updatedimulation` commande. Ce script génère tous les composants de simulation hello, la simulation hello Bonjour machine virtuelle est arrêtée, télécharge, installe et démarre.

### <a name="how-do-i-find-out-hello-connection-string-of-hello-iot-hub-used-by-my-solution"></a>Comment savoir la chaîne de connexion hello de hello IoT hub utilisé par ma solution ?

Si vous avez déployé votre solution avec hello `build.ps1` script Bonjour [référentiel](https://github.com/Azure/azure-iot-connected-factory), chaîne de connexion hello est la valeur hello **IotHubOwnerConnectionString** Bonjour `<name of your deployment>.config.user` fichier.

Vous trouverez également la chaîne de connexion hello à l’aide de hello portail Azure. Bonjour ressource IoT Hub dans le groupe de ressources hello de votre déploiement, recherchez les paramètres de chaîne de connexion hello.

### <a name="which-iot-hub-devices-does-hello-connected-factory-simulation-use"></a>Les appareils IoT Hub hello utilisation de simulation de fabrique connectés ?

Hello simulation self inscrit hello suivants des appareils :

* proxy.beijing.corp.contoso
* proxy.capetown.corp.contoso
* proxy.mumbai.corp.contoso
* proxy.munich0.corp.contoso
* proxy.rio.corp.contoso
* proxy.seattle.corp.contoso
* publisher.beijing.corp.contoso
* publisher.capetown.corp.contoso
* publisher.mumbai.corp.contoso
* publisher.munich0.corp.contoso
* publisher.rio.corp.contoso
* publisher.seattle.corp.contoso

À l’aide de hello [DeviceExplorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) ou [iothub-explorer](https://github.com/azure/iothub-explorer) outil, vous pouvez vérifier quels appareils sont inscrits avec hello IoT hub à l’aide de votre solution. toouse ces outils, vous devez chaîne de connexion hello pour le hub IoT de hello dans votre déploiement.

### <a name="how-can-i-get-log-data-from-hello-simulation-components"></a>Comment puis-je obtenir des données du journal à partir des composants de simulation hello ?

Tous les composants dans la simulation hello enregistrer des informations dans les fichiers toolog. Ces fichiers sont accessibles dans hello machine virtuelle dans le dossier de hello `home/docker/Logs`. journaux de hello tooretrieve, vous pouvez utiliser de script PowerShell hello `Simulation/Factory/Get-SimulationLogs.ps1` Bonjour [référentiel](https://github.com/Azure/azure-iot-connected-factory).

Ce script doit toosign dans toohello machine virtuelle. Vous devrez peut-être les informations d’identification tooprovide pour la connexion d’hello. Consultez [comment se connecter lors de la simulation de toohello VM ?](#how-do-i-sign-in-to-the-simulation-vm) informations d’identification de toofind hello.

script de Hello ajoute/supprime un toohello d’adresse IP publique machine virtuelle, si elle n’en a pas encore et le supprime. script de Hello place tous les fichiers journaux dans une archive et télécharge la station de travail développement hello archive tooyour.

Vous pouvez également connecter toohello machine virtuelle via SSH et inspecter des fichiers de journal hello lors de l’exécution.

### <a name="how-can-i-check-if-hello-simulation-is-sending-data-toohello-cloud"></a>Comment puis-je vérifier si la simulation hello envoie des données dans le cloud toohello ?

Avec hello [DeviceExplorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) ou hello [iothub-explorer](https://github.com/azure/iothub-explorer) outil, vous pouvez inspecter les données hello envoyées tooIoT Hub à partir de certains appareils. toouse ces outils, vous devez chaîne de connexion tooknow hello pour le hub IoT de hello dans votre déploiement. Consultez [comment faire pour rechercher des chaîne de connexion hello de hello IoT hub utilisé par ma solution ?](#how-do-i-find-out-the-connection-string-of-the-iot-hub-used-by-my-solution)

Inspecter les données hello envoyées par un des appareils de serveur de publication hello :

* publisher.beijing.corp.contoso
* publisher.capetown.corp.contoso
* publisher.mumbai.corp.contoso
* publisher.munich0.corp.contoso
* publisher.rio.corp.contoso
* publisher.seattle.corp.contoso

Si vous ne voyez aucuns envoyées tooIoT concentrateur de données, il est un problème avec la simulation de hello. Vous devez analyser les journaux hello de composants de simulation hello dans un premier temps d’analyse. Consultez [comment puis-je obtenir des données de journal à partir de hello composants de simulation ?](#how-can-i-get-log-data-from-the-simulation-components) Ensuite, essayez toostop et démarrer la simulation hello et si encore aucune donnée n’est envoyée, la simulation hello jour complètement. Consultez [comment mettre à jour la simulation hello Bonjour machine virtuelle ?](#how-do-i-update-the-simulation-in-the-vm)

### <a name="next-steps"></a>Étapes suivantes

Vous pouvez également découvrir hello autres et les fonctionnalités des solutions de IoT Suite préconfiguré hello :

* [Présentation de la solution préconfigurée de maintenance prédictive](iot-suite-predictive-overview.md)
* [Présentation de la solution préconfigurée d’usine connectée](iot-suite-connected-factory-overview.md)
* [IoT hello d’arrière-plan la sécurité](securing-iot-ground-up.md)
