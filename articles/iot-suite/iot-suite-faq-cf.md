---
title: "Questions fréquentes (FAQ) sur l’usine connectée Azure IoT Suite | Microsoft Docs"
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
ms.date: 09/15/2017
ms.author: corywink
ms.openlocfilehash: babd39d5e2f290d9e3f7fc3a232937c6ccfc85c6
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="frequently-asked-questions-for-iot-suite-connected-factory-preconfigured-solution"></a>Questions fréquentes sur la solution préconfigurée d’usine connectée IoT Suite

Voir aussi les [questions fréquentes (FAQ)](iot-suite-faq.md) d’ordre général sur IoT Suite.

### <a name="where-can-i-find-the-source-code-for-the-preconfigured-solution"></a>Où trouver le code source de la solution préconfigurée ?

Le code source est stocké dans le dépôt GitHub suivant :

* [Solution préconfigurée d’usine connectée](https://github.com/Azure/azure-iot-connected-factory)

### <a name="what-is-opc-ua"></a>Qu’est-ce que l’UA OPC ?

OPC UA (Unified Architecture) est un standard d’interopérabilité indépendant de la plateforme et orienté services, qui date de 2008. OPC UA est utilisé par différents systèmes et dispositifs industriels tels que les PC industriels, les automates programmables industriels et les capteurs. OPC UA intègre les fonctionnalités des spécifications OPC Classic dans un seul et même framework extensible avec un dispositif de sécurité intégré. La fondation OPC Foundation est à l’origine de cette norme. [OPC Foundation](http://opcfoundation.org/) est une organisation à but non lucratif qui compte plus de 440 membres. L’objectif de cette organisation est d’utiliser les spécifications OPC de façon à favoriser une interopérabilité fiable et sécurisée entre les fabricants et les plateformes par les moyens suivants :

* Infrastructure
* Spécifications
* Technology
* Processus

### <a name="why-did-microsoft-choose-opc-ua-for-the-connected-factory-preconfigured-solution"></a>Pourquoi le choix de Microsoft s’est-il porté sur l’UA OPC en matière de solution préconfigurée d’usine connectée ?

Microsoft a choisi l’UA OPC, car il s’agit d’une norme ouverte, non propriétaire, ne dépendant pas d’une plateforme, reconnue par le secteur et éprouvée. Elle est exigée pour les solutions d’architecture de référence Industrie 4.0 (RAMI4.0) assurant l’interopérabilité entre un large ensemble de processus de fabrication et les équipements. Microsoft constate une demande de la part des clients pour créer des solutions Industrie 4.0. La prise en charge de l’UA OPC permet de supprimer la barrière empêchant les clients d’atteindre leurs objectifs et leur apporte une valeur commerciale instantanée.

### <a name="how-do-i-add-a-public-ip-address-to-the-simulation-vm"></a>Comment ajouter une adresse IP publique à la machine virtuelle de simulation ?

Vous pouvez ajouter l’adresse IP de deux manières :

* Utilisez le script PowerShell `Simulation/Factory/Add-SimulationPublicIp.ps1` dans le [dépôt](https://github.com/Azure/azure-iot-connected-factory). Passez le nom de votre déploiement en tant que paramètre. Pour un déploiement local, utilisez `<your username>ConnFactoryLocal`. Le script imprime l’adresse IP de la machine virtuelle.

* Dans le portail Azure, recherchez le groupe de ressources de votre déploiement. À moins qu’il s’agisse d’un déploiement local, le groupe de ressources porte le nom que vous avez spécifié comme nom de solution ou de déploiement. Pour un déploiement local utilisant le script build, le nom du groupe de ressources est `<your username>ConnFactoryLocal`. À présent, ajoutez une nouvelle ressource **Adresse IP publique** au groupe de ressources.

> [!NOTE]
> Dans les deux cas, veillez à installer les derniers correctifs en suivant les instructions sur le [site web Ubuntu](https://wiki.ubuntu.com/Security/Upgrades). Tenez à jour l’installation aussi longtemps que votre machine virtuelle est accessible via une adresse IP publique.

### <a name="how-do-i-remove-the-public-ip-address-to-the-simulation-vm"></a>Comment supprimer l’adresse IP publique de la machine virtuelle de simulation ?

Vous pouvez supprimer l’adresse IP de deux manières :

* Utilisez le script PowerShell Simulation/Factory/Remove-SimulationPublicIp.ps1 du [dépôt](https://github.com/Azure/azure-iot-connected-factory). Passez le nom de votre déploiement en tant que paramètre. Pour un déploiement local, utilisez `<your username>ConnFactoryLocal`. Le script imprime l’adresse IP de la machine virtuelle.

* Dans le portail Azure, recherchez le groupe de ressources de votre déploiement. À moins qu’il s’agisse d’un déploiement local, le groupe de ressources porte le nom que vous avez spécifié comme nom de solution ou de déploiement. Pour un déploiement local utilisant le script build, le nom du groupe de ressources est `<your username>ConnFactoryLocal`. À présent, supprimez la ressource **Adresse IP publique** du groupe de ressources.

### <a name="how-do-i-sign-in-to-the-simulation-vm"></a>Comment se connecter à la machine virtuelle de simulation ?

La connexion à la machine virtuelle de simulation n’est prise en charge que si vous avez déployé votre solution à l’aide du script PowerShell `build.ps1` du [dépôt](https://github.com/Azure/azure-iot-connected-factory).

Si vous avez déployé la solution à partir de www.azureiotsuite.com, vous ne pouvez pas vous connecter à la machine virtuelle. En effet, le mot de passe est généré de façon aléatoire, donc vous ne pouvez pas le réinitialiser.

1. Ajoutez une adresse IP publique à la machine virtuelle. Consultez [Comment ajouter une adresse IP publique à la machine virtuelle de simulation ?](#how-do-i-remove-the-public-ip-address-to-the-simulation-vm).
1. Créez une session SSH sur votre machine virtuelle en utilisant l’adresse IP de la machine virtuelle.
1. Le nom d’utilisateur à utiliser est `docker`.
1. Le mot de passe à utiliser dépend de la version que vous avez utilisée pour le déploiement :
    * Pour les solutions déployées à l’aide du script build.ps1 avant le 1er juin 2017, le mot de passe est `Passw0rd`.
    * Pour les solutions déployées à l’aide du script build.ps1 après le 1er juin 2017, le mot de passe est `<name of your deployment>.config.user`. Le mot de passe est stocké dans le paramètre **VmAdminPassword**. Le mot de passe est généré de façon aléatoire au moment du déploiement, sauf si vous le spécifiez à l’aide du paramètre `-VmAdminPassword` du script `build.ps1`.

### <a name="how-do-i-stop-and-start-all-docker-processes-in-the-simulation-vm"></a>Comment arrêter et démarrer tous les processus Docker dans la machine virtuelle de simulation ?

1. Connectez-vous à la machine virtuelle de simulation. Consultez [Comment se connecter à la machine virtuelle de simulation ?](#how-do-i-sign-in-to-the-simulation-vm).
1. Pour identifier les conteneurs actifs, exécutez `docker ps`.
1. Pour arrêter tous les conteneurs de simulation, exécutez `./stopsimulation`.
1. Pour démarrer tous les conteneurs de simulation :
    * Exportez une variable shell sous le nom **IOTHUB_CONNECTIONSTRING**. Utilisez la valeur du paramètre **IotHubOwnerConnectionString** du fichier `<name of your deployment>.config.user`. Par exemple :

        ```
        export IOTHUB_CONNECTIONSTRING="HostName={yourdeployment}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={your key}"
        ```

    * Exécutez `./startsimulation`.

### <a name="how-do-i-update-the-simulation-in-the-vm"></a>Comment mettre à jour la simulation dans la machine virtuelle ?

Si vous avez apporté des modifications à la simulation, vous pouvez utiliser le script PowerShell `build.ps1` du [dépôt](https://github.com/Azure/azure-iot-connected-factory) en utilisant la commande `updatedimulation`. Ce script génère tous les composants de simulation, arrête la simulation dans la machine virtuelle, puis les charge, les installe et les démarre.

### <a name="how-do-i-find-out-the-connection-string-of-the-iot-hub-used-by-my-solution"></a>Comment identifier la chaîne de connexion du hub IoT utilisé par ma solution ?

Si vous avez déployé votre solution avec le script `build.ps1` du [dépôt](https://github.com/Azure/azure-iot-connected-factory), la chaîne de connexion est la valeur de **IotHubOwnerConnectionString** du fichier `<name of your deployment>.config.user`.

Vous pouvez aussi trouver la chaîne de connexion dans le portail Azure. Dans la ressource IoT Hub du groupe de ressources de votre déploiement, recherchez les paramètres de chaîne de connexion.

### <a name="which-iot-hub-devices-does-the-connected-factory-simulation-use"></a>Quels appareils IoT Hub la simulation d’usine connectée utilise ?

La simulation inscrit elle-même les appareils suivants :

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

À l’aide de l’outil [DeviceExplorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) ou [iothub-explorer](https://github.com/azure/iothub-explorer), vous pouvez identifier les appareils inscrits auprès du hub IoT utilisé par votre solution. Pour utiliser ces outils, vous avez besoin de la chaîne de connexion du hub IoT de votre déploiement.

### <a name="how-can-i-get-log-data-from-the-simulation-components"></a>Comment obtenir les données de journal des composants de simulation ?

Tous les composants de la simulation enregistrent des informations dans des fichiers journaux. Ces fichiers se trouvent dans la machine virtuelle dans le dossier `home/docker/Logs`. Pour récupérer les journaux, vous pouvez utiliser le script PowerShell `Simulation/Factory/Get-SimulationLogs.ps1` du [dépôt](https://github.com/Azure/azure-iot-connected-factory).

Ce script doit se connecter à la machine virtuelle. Vous serez peut-être amené à fournir des informations d’identification pour vous connecter. Pour savoir comment trouver les informations d’identification, consultez [Comment se connecter à la machine virtuelle de simulation ?](#how-do-i-sign-in-to-the-simulation-vm).

Le script ajoute une adresse IP publique à la machine virtuelle, si elle n’en dispose pas déjà d’une, puis la supprime. Le script place tous les fichiers journaux dans une archive et télécharge celle-ci sur votre station de travail de développement.

Vous pouvez aussi vous connecter à la machine virtuelle via SSH et inspecter les fichiers journaux au moment de l’exécution.

### <a name="how-can-i-check-if-the-simulation-is-sending-data-to-the-cloud"></a>Comment vérifier si la simulation envoie des données vers le cloud ?

Avec l’outil [DeviceExplorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) ou [iothub-explorer](https://github.com/azure/iothub-explorer), vous pouvez inspecter les données envoyées à IoT Hub à partir de certains appareils. Pour utiliser ces outils, vous devez connaître la chaîne de connexion du hub IoT de votre déploiement. Consultez [Comment identifier la chaîne de connexion du hub IoT utilisé par ma solution ?](#how-do-i-find-out-the-connection-string-of-the-iot-hub-used-by-my-solution).

Inspecter les données envoyées par l’un des appareils serveur de publication :

* publisher.beijing.corp.contoso
* publisher.capetown.corp.contoso
* publisher.mumbai.corp.contoso
* publisher.munich0.corp.contoso
* publisher.rio.corp.contoso
* publisher.seattle.corp.contoso

Si vous constatez qu’aucune donnée n’a été envoyée à IoT Hub, c’est qu’il y a un problème au niveau de la simulation. La première étape d’analyse que vous devez effectuer consiste à analyser les fichiers journaux des composants de simulation. Consultez [Comment obtenir les données de journal des composants de simulation ?](#how-can-i-get-log-data-from-the-simulation-components). Ensuite, essayez d’arrêter et de démarrer la simulation et si aucune donnée n’est toujours envoyée, mettez entièrement à jour la simulation. Consultez [Comment mettre à jour la simulation dans la machine virtuelle ?](#how-do-i-update-the-simulation-in-the-vm).

### <a name="next-steps"></a>Étapes suivantes

Vous pouvez également explorer certaines des autres fonctionnalités et capacités des solutions préconfigurées IoT Suite :

* [Présentation de la solution préconfigurée de maintenance prédictive](iot-suite-predictive-overview.md)
* [Présentation de la solution préconfigurée d’usine connectée](iot-suite-connected-factory-overview.md)
* [Sécurisation de l’Internet des objets de bout en bout](securing-iot-ground-up.md)