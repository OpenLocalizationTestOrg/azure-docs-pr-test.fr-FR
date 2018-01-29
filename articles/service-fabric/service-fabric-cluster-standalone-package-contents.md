---
title: Package autonome Azure Service Fabric pour Windows Server | Microsoft Docs
description: Description et contenu du package autonome Azure Service Fabric pour Windows Server.
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
ms.openlocfilehash: 6a6bacedde04419449a061554d5ce9ad37259a2f
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="contents-of-service-fabric-standalone-package-for-windows-server"></a>Contenu du package autonome Service Fabric pour Windows Server
Dans le package autonome Service Fabric [téléchargé](http://go.microsoft.com/fwlink/?LinkId=730690), vous trouverez les fichiers suivants :

| **Nom de fichier** | **Brève description** |
| --- | --- |
| CreateServiceFabricCluster.ps1 |Un script PowerShell qui crée le cluster à l’aide des paramètres figurant dans ClusterConfig.json. |
| RemoveServiceFabricCluster.ps1 |Un script PowerShell qui supprime un cluster à l’aide des paramètres figurant ClusterConfig.json. |
| AddNode.ps1 |Un script PowerShell pour l’ajout d’un nœud à un cluster déployé existant sur l’ordinateur actuel. |
| RemoveNode.ps1 |Un script PowerShell pour la suppression d’un nœud d’un cluster déployé existant de l’ordinateur actuel. |
| CleanFabric.ps1 |Un script PowerShell pour supprimer une installation autonome Service Fabric de l’ordinateur actuel. Les installations MSI précédentes doivent être supprimées à l’aide de leur propre programme de désinstallation associé. |
| TestConfiguration.ps1 |Un script PowerShell pour l’analyse de l’infrastructure comme spécifié dans Cluster.json. |
| DownloadServiceFabricRuntimePackage.ps1 |Un script PowerShell utilisé pour télécharger le dernier package de runtime hors bande, pour les scénarios où l’ordinateur de déploiement n’est pas connecté à internet. |
| DeploymentComponentsAutoextractor.exe |Archive auto-extractible qui contient les composants de déploiement utilisés par les scripts du package autonome. |
| EULA_ENU.txt |Les termes du contrat de licence pour l’utilisation du package Windows Server autonome Microsoft Azure Service Fabric. Vous pouvez [télécharger une copie du CLUF](http://go.microsoft.com/fwlink/?LinkID=733084) maintenant. |
| Readme.txt |Un lien vers les notes de publication et des instructions d’installation de base. Il s’agit d’une partie des instructions figurant dans ce document. |
| ThirdPartyNotice.rtf |Informations sur le logiciel tiers du package. |
| Tools\Microsoft.Azure.ServiceFabric.WindowsServer.SupportPackage.zip |StandaloneLogCollector.exe, qui est exécuté à la demande pour collecter et envoyer les journaux de suivi à Microsoft à des fins de support. |
| Tools\ServiceFabricUpdateService.zip |Un outil utilisé pour activer la mise à niveau automatique pour les clusters qui n’ont pas accès à Internet. Pour plus d’informations, cliquez [ici](service-fabric-cluster-upgrade-windows-server.md)|

**Modèles** 
| **Nom de fichier** | **Brève description** |
| --- | --- |
| ClusterConfig.Unsecure.DevCluster.json |Un exemple de fichier de configuration de cluster qui contient les paramètres pour un cluster de développement avec ordinateur unique (ou machine virtuelle) à trois nœuds non sécurisé, notamment les informations de chaque nœud du cluster. |
| ClusterConfig.Unsecure.MultiMachine.json |Un exemple de fichier de configuration de cluster qui contient les paramètres pour un cluster avec plusieurs ordinateurs (ou machines virtuelles) non sécurisé, notamment les informations de chaque ordinateur du cluster. |
| ClusterConfig.Windows.DevCluster.json |Un exemple de fichier de configuration de cluster qui contient tous les paramètres pour un cluster de développement avec ordinateur unique (ou machine virtuelle) à trois nœuds sécurisé, notamment les informations de chaque nœud se trouvant dans le cluster. Le cluster est sécurisé à l’aide [d’identités Windows](https://msdn.microsoft.com/library/ff649396.aspx). |
| ClusterConfig.Windows.MultiMachine.json |Un exemple de fichier de configuration de cluster qui contient tous les paramètres pour un cluster avec plusieurs ordinateurs (ou machines virtuelles) sécurisé, utilisant la sécurité Windows, notamment les informations de chaque ordinateur du cluster sécurisé. Le cluster est sécurisé à l’aide [d’identités Windows](https://msdn.microsoft.com/library/ff649396.aspx). |
| ClusterConfig.x509.DevCluster.json |Un exemple de fichier de configuration de cluster qui contient les paramètres pour un cluster de développement avec ordinateur unique (ou machine virtuelle) à trois nœuds sécurisé, notamment les informations de chaque nœud du cluster. Le cluster est sécurisé à l’aide de certificats x509. |
| ClusterConfig.x509.MultiMachine.json |Un exemple de fichier de configuration de cluster qui contient tous les paramètres pour le cluster à plusieurs ordinateurs (ou machines virtuelles) sécurisé, notamment les informations de chaque nœud du cluster sécurisé. Le cluster est sécurisé à l’aide de certificats x509. |
| ClusterConfig.gMSA.Windows.MultiMachine.json |Un exemple de fichier de configuration de cluster qui contient tous les paramètres pour le cluster à plusieurs ordinateurs (ou machines virtuelles) sécurisé, notamment les informations de chaque nœud du cluster sécurisé. Le cluster est sécurisé à l’aide de [comptes de service gérés de groupe](https://technet.microsoft.com/en-us/library/jj128431(v=ws.11).aspx). |

## <a name="cluster-configuration-samples"></a>Exemples de configuration du cluster
Vous trouverez les dernières versions des modèles de configuration du cluster sur la page GitHub : [Exemples de configuration de cluster autonome](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).

## <a name="independent-runtime-package"></a>Package de runtime indépendant
Le package de runtime le plus récent est téléchargé automatiquement lors du déploiement du cluster, à partir du [lien de téléchargement du runtime Service Fabric de Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).

## <a name="related"></a>Rubriques connexes
* [Créer un cluster Azure Service Fabric autonome](service-fabric-cluster-creation-for-windows-server.md)
* [Scénarios de sécurité d’un cluster Service Fabric](service-fabric-windows-cluster-windows-security.md)
