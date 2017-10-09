---
title: aaaAzure Service Fabric Docker composer Preview
description: "Azure Service Fabric accepte toomake de format Docker Compose il plus faciles conteneurs existants tooorchestrate à l’aide de l’infrastructure de Service. Cette prise en charge est actuellement en mode préliminaire."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: a60d1321fd6ef07b241a98c5ab2b8dfe5d441b53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="docker-compose-application-support-in-azure-service-fabric-preview"></a>Prise en charge de l’application Docker Compose dans Azure Service Fabric (préversion)

Docker utilise hello [docker-compose.yml](https://docs.docker.com/compose) fichier permettant de définir le conteneur de plusieurs applications. toomake il facile pour les clients familiarisés avec les applications existantes conteneur Docker tooorchestrate sur Azure Service Fabric, nous avons inclus prise en charge de la version préliminaire de Docker Compose en mode natif dans hello plate-forme. Service Fabric peut accepter des fichiers `docker-compose.yml` version 3 ou ultérieure. 

Étant donné que cette prise en charge est disponible en préversion, seul un sous-ensemble des directives de Compose est reconnu. Par exemple, les mises à niveau d’application ne sont pas prises en charge. Toutefois, vous pouvez toujours supprimer et déployer des applications au lieu de les mettre à niveau.

toouse cela prévisualiser, créez votre cluster avec la version 5.7 ou version ultérieure du runtime de Service Fabric hello via le portail Azure, ainsi que de hello correspondant du Kit de développement logiciel de hello. 

> [!NOTE]
> Cette fonctionnalité est disponible en préversion et n’est pas prise en charge dans les environnements de production.

## <a name="deploy-a-docker-compose-file-on-service-fabric"></a>Déployer un fichier Docker Compose sur Service Fabric

Hello commandes suivantes créent une application Service Fabric (nommé `fabric:/TestContainerApp` Bonjour précédent exemple), que vous pouvez surveiller et gérer comme toute autre application de Service Fabric. Vous pouvez utiliser le nom de l’application spécifiée hello pour les requêtes d’intégrité.

### <a name="use-powershell"></a>Utiliser PowerShell

Créez une application de composer de l’infrastructure de Service à partir d’un fichier compose.yml de docker en exécutant hello commande dans PowerShell suivante :

```powershell
New-ServiceFabricComposeApplication -ApplicationName fabric:/TestContainerApp -Compose docker-compose.yml [-RegistryUserName <>] [-RegistryPassword <>] [-PasswordEncrypted]
```

`RegistryUserName`et `RegistryPassword` font référence toohello conteneur Registre username et password. Une fois que vous avez terminé d’application hello, vous pouvez vérifier son état à l’aide de hello de commande suivante :

```powershell
Get-ServiceFabricComposeApplicationStatus -ApplicationName fabric:/TestContainerApp -GetAllPages
```

toodelete hello application composition via PowerShell, utilisez les hello de commande suivante :

```powershell
Remove-ServiceFabricComposeApplication  -ApplicationName fabric:/TestContainerApp
```

### <a name="use-azure-service-fabric-cli-sfctl"></a>Utiliser l’interface CLI Azure Service Fabric (sfctl)

Vous pouvez également utiliser hello Service Fabric CLI commande suivante :

```azurecli
sfctl compose create --application-id fabric:/TestContainerApp --compose-file docker-compose.yml [ [ --repo-user --repo-pass --encrypted ] | [ --repo-user ] ] [ --timeout ]
```

Une fois que vous avez créé l’application hello, vous pouvez vérifier son état à l’aide de hello de commande suivante :

```azurecli
sfctl compose status --application-id TestContainerApp [ --timeout ]
```

toodelete hello application du nouveau message, utilisez hello de commande suivante :

```azurecli
sfctl compose remove  --application-id TestContainerApp [ --timeout ]
```

## <a name="supported-compose-directives"></a>Directives Compose prises en charge

Cette version préliminaire prend en charge un sous-ensemble des options de configuration hello depuis le format de version 3 message hello, y compris hello suivant primitives :

* Services > Déploiement > Réplicas
* Services > Déploiement > Placement > Contraintes
* Services > Déploiement > Ressources > Limites
    * -cpu-shares
    * -memory
    * -memory-swap
* Services > Commandes
* Services > Environnement
* Services > Ports
* Services > Image
* Services > Isolation (uniquement pour Windows)
* Services > Journalisation > Pilote
* Services > Journalisation > Pilote > Options
* Volume & déploiement > Volume

Configurez cluster hello pour mettre en œuvre des limites de ressources, comme décrit dans [gouvernance des ressources de Service Fabric](service-fabric-resource-governance.md). Aucune des autres directives Docker Compose n’est prise en charge pour cette préversion.

## <a name="servicednsname-computation"></a>Calcul de ServiceDnsName

Si le nom du service hello que vous spécifiez dans un fichier de message est un nom de domaine complet (autrement dit, elle contient un point [.]), le nom DNS hello enregistré par le Service Fabric est `<ServiceName>` (y compris le point de hello). Si ce n’est pas le cas, chaque segment de chemin d’accès dans le nom de l’application hello devient un nom de domaine dans le nom DNS du service hello, avec le premier segment de chemin d’accès hello devient l’étiquette du domaine de premier niveau hello.

Par exemple, si hello spécifié le nom de l’application est `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` serait hello nom DNS enregistré.

## <a name="differences-between-compose-instance-definition-and-service-fabric-application-model-type-definition"></a>Différences entre le Compose (définition d’instance) et le modèle d’application Service Fabric (définition de type)

Un fichier docker-compose.yml décrit un ensemble déployable de conteneurs, y compris leurs propriétés et leurs configurations.
Par exemple, fichier de hello peut contenir des variables d’environnement et les ports. Vous pouvez également spécifier des paramètres de déploiement, tels que les contraintes de placement, les limites des ressources et les noms DNS dans le fichier de docker-compose.yml hello.

Hello [modèle d’application Service Fabric](service-fabric-application-model.md) utilise des types de service et les types d’applications, où vous pouvez avoir plusieurs instances d’application du même type de hello. Par exemple, vous pouvez avoir une seule instance d’application par client. Ce modèle basé sur le type prend en charge plusieurs versions de hello même type d’application qui est inscrit avec le runtime de hello.

Par exemple, client A peut disposer d’une application instanciée avec type 1.0 de AppTypeA et client B peut disposer d’une autre application instanciée avec hello même type et la version. Vous définissez des types d’application hello dans les manifestes d’application hello et que vous spécifiez les paramètres du nom et le déploiement d’application hello lorsque vous créez l’application hello.

Bien que ce modèle offre une grande souplesse, nous avons également l’intention toosupport un modèle de déploiement plus simple, basé sur une instance où les types sont implicites à partir du fichier de manifeste hello. Dans ce modèle, chaque application obtient son propre manifeste indépendant. Nous proposons cela en version préliminaire, en ajoutant la prise en charge du format docker-compose.yml, qui est un format de déploiement basé sur les instances.

## <a name="next-steps"></a>Étapes suivantes

* Sur hello [modèle d’application Service Fabric](service-fabric-application-model.md)
* [Prise en main de l’interface de ligne de commande Service Fabric](service-fabric-cli.md)
