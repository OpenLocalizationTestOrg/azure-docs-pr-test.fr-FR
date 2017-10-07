---
title: aaaAzure Package autonome de Service Fabric pour Windows Server | Documents Microsoft
description: "Description et le contenu du package d’Azure Service Fabric autonomes hello pour Windows Server."
services: service-fabric
documentationcenter: .net
author: maburlik
manager: timlt
editor: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/10/2017
ms.author: chackdan;maburlik
ms.openlocfilehash: e4c6cb9128d659144e559fcad06bb78c9969dd60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="contents-of-service-fabric-standalone-package-for-windows-server"></a>Contenu du package autonome Service Fabric pour Windows Server
Bonjour [téléchargé](http://go.microsoft.com/fwlink/?LinkId=730690) package de Service Fabric autonomes, vous trouverez hello fichiers suivants :

| **Nom de fichier** | **Brève description** |
| --- | --- |
| CreateServiceFabricCluster.ps1 |Un script PowerShell qui crée le cluster hello à l’aide des paramètres de hello dans le fichier ClusterConfig.json. |
| RemoveServiceFabricCluster.ps1 |Un script PowerShell qui supprime d’un cluster à l’aide des paramètres de hello dans le fichier ClusterConfig.json. |
| AddNode.ps1 |Un script PowerShell pour l’ajout d’un tooan de nœud existant déployé cluster sur l’ordinateur en cours de hello. |
| RemoveNode.ps1 |Un script PowerShell pour la suppression d’un nœud existant déployé un cluster à partir de la machine en cours hello. |
| CleanFabric.ps1 |Un script PowerShell pour le nettoyage d’une installation de l’infrastructure de Service hors tension de l’ordinateur actuel de hello autonome. Les installations MSI précédentes doivent être supprimées à l’aide de leur propre programme de désinstallation associé. |
| TestConfiguration.ps1 |Un script PowerShell pour l’analyse d’infrastructure hello comme spécifié dans hello Cluster.json. |
| DownloadServiceFabricRuntimePackage.ps1 |Un script PowerShell utilisé pour télécharger le dernier package de runtime hello hors bande, pour les scénarios où hello déploiement d’ordinateur n’est pas connecté toohello internet. |
| DeploymentComponentsAutoextractor.exe |Archive contenant les composants du déploiement auto-extractible utilisé par hello scripts du package autonome. |
| EULA_ENU.txt |termes du contrat de licence Hello pourquoi l’utilisation de package de Windows Server autonome de Microsoft Azure Service Fabric. Vous pouvez [télécharger une copie du CLUF de hello](http://go.microsoft.com/fwlink/?LinkID=733084) maintenant. |
| Readme.txt |Un lien de toohello notes de publication et des instructions d’installation de base. Il s’agit d’un sous-ensemble d’instructions hello dans ce document. |
| ThirdPartyNotice.rtf |Avis d’un logiciel tiers qui se trouve dans le package de hello. |
| Tools\Microsoft.Azure.ServiceFabric.WindowsServer.SupportPackage.zip |StandaloneLogCollector.exe qui est exécuté sur la trace de toocollect et le téléchargement à la demande ouvre une tooMicrosoft à des fins de prise en charge. |
| Tools\ServiceFabricUpdateService.zip |Un outil utilisé la mise à niveau du code tooenable automatique pour les clusters qui n’ont pas accès à internet. Pour plus d’informations, cliquez [ici](service-fabric-cluster-upgrade-windows-server.md)|

**Modèles** 
| **Nom de fichier** | **Brève description** |
| --- | --- |
| ClusterConfig.Unsecure.DevCluster.json |Un cluster configuration exemple de fichier qui contient les paramètres de hello pour une non sécurisé, trois nœuds, seul ordinateur (ou un ordinateur virtuel) cluster de développement, y compris les informations de hello pour chaque nœud de cluster de hello. |
| ClusterConfig.Unsecure.MultiMachine.json |Un cluster configuration exemple de fichier qui contient les paramètres pour un cluster non sécurisé, avec plusieurs ordinateurs (ou ordinateur virtuel), y compris les informations de hello pour chaque ordinateur dans le cluster de hello hello. |
| ClusterConfig.Windows.DevCluster.json |Un cluster configuration exemple de fichier qui contient tous les cluster de développement de paramètres pour un seul ordinateur sécurisé et trois nœuds, (ou un ordinateur virtuel) hello, y compris les informations de hello pour chaque nœud qui se trouve dans un cluster de hello. cluster de Hello est sécurisé à l’aide de [des identités Windows](https://msdn.microsoft.com/library/ff649396.aspx). |
| ClusterConfig.Windows.MultiMachine.json |Un cluster configuration exemple de fichier qui contient tous les paramètres de hello pour un cluster sécurisé, avec plusieurs ordinateurs (ou ordinateur virtuel), à l’aide de la sécurité de Windows, y compris les informations de hello pour chaque ordinateur qui se trouve dans le cluster sécurisée de hello. cluster de Hello est sécurisé à l’aide de [des identités Windows](https://msdn.microsoft.com/library/ff649396.aspx). |
| ClusterConfig.x509.DevCluster.json |Un cluster configuration exemple de fichier qui contient tous les paramètres de hello pour un sécurisée, trois nœuds, seul ordinateur (ou un ordinateur virtuel) cluster de développement, y compris les informations de hello pour chaque nœud de cluster de hello. Hello cluster est sécurisé à l’aide de x509 certificats. |
| ClusterConfig.x509.MultiMachine.json |Un fichier d’exemple de configuration cluster qui contient tous les paramètres de hello pour hello sécurisée cluster avec plusieurs ordinateurs (ou ordinateur virtuel), y compris les informations de hello pour chaque nœud de cluster sécurisée de hello. Hello cluster est sécurisé à l’aide de x509 certificats. |
| ClusterConfig.gMSA.Windows.MultiMachine.json |Un fichier d’exemple de configuration cluster qui contient tous les paramètres de hello pour hello sécurisée cluster avec plusieurs ordinateurs (ou ordinateur virtuel), y compris les informations de hello pour chaque nœud de cluster sécurisée de hello. Hello cluster est sécurisé à l’aide de [groupe comptes de Service administrés](https://technet.microsoft.com/en-us/library/jj128431(v=ws.11).aspx). |

## <a name="cluster-configuration-samples"></a>Exemples de configuration du cluster
Vous trouverez les versions les plus récentes des modèles de configuration de cluster à la page GitHub de hello : [exemples de Configuration de Cluster autonome](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).

## <a name="independent-runtime-package"></a>Package de runtime indépendant
package de runtime plus récent Hello est automatiquement téléchargé lors du déploiement de cluster à partir de [lien Télécharger - Runtime du Service de l’ensemble fibre optique - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).

## <a name="related"></a>Rubriques connexes
* [Créer un cluster Azure Service Fabric autonome](service-fabric-cluster-creation-for-windows-server.md)
* [Scénarios de sécurité d’un cluster Service Fabric](service-fabric-windows-cluster-windows-security.md)
