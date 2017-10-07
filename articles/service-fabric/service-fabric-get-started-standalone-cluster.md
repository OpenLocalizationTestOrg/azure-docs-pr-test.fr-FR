---
title: "aaaSet d’un cluster de Azure Service Fabric autonomes | Documents Microsoft"
description: "Créer un cluster autonome de développement avec trois nœuds sont en cours d’exécution sur hello même ordinateur. Après avoir terminé cette installation, vous serez prêt toocreate un cluster de plusieurs ordinateur."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/06/2017
ms.author: dekapur
ms.openlocfilehash: e4d0ea9fc3b8475160bd8ed19fd3716463791cc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-standalone-cluster"></a>Créer votre premier cluster Service Fabric autonome
Vous pouvez créer un cluster autonome de l’infrastructure de Service sur des machines virtuelles ou des ordinateurs exécutant Windows Server 2012 R2 ou Windows Server 2016, localement ou dans le cloud de hello. Ce démarrage rapide vous aide à toocreate un cluster autonome de développement dans quelques minutes seulement.  Une fois que vous avez terminé, vous disposez d’un cluster à trois nœuds s’exécutant sur un seul ordinateur sur lequel vous pouvez déployer des applications.

## <a name="before-you-begin"></a>Avant de commencer
L’infrastructure de service fournit une configuration de clusters de package toocreate Service Fabric autonomes.  [Télécharger le package d’installation hello](http://go.microsoft.com/fwlink/?LinkId=730690).  Décompressez hello dossier d’installation package tooa sur l’ordinateur de hello ou un ordinateur virtuel sur lequel vous configurez cluster de développement hello.  contenu Hello du package d’installation de hello est décrites en détail [ici](service-fabric-cluster-standalone-package-contents.md).

l’administrateur de cluster Hello déploiement et la configuration de cluster de hello doit avoir des privilèges d’administrateur sur l’ordinateur de hello. Vous ne pouvez pas installer Service Fabric sur un contrôleur de domaine.

## <a name="validate-hello-environment"></a>Validation de l’environnement de hello
Hello *TestConfiguration.ps1* script dans le package de hello autonome est utilisé comme un toovalidate d’analyseur meilleures pratiques si un cluster peut être déployé sur un environnement donné. [Préparation au déploiement](service-fabric-cluster-standalone-deployment-preparation.md) listes hello conditions préalables et les spécifications de l’environnement. Exécutez hello script tooverify si vous pouvez créer le cluster de développement hello :

```powershell
.\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json
```
## <a name="create-hello-cluster"></a>Créer le cluster de hello
Plusieurs fichiers de configuration de cluster d’exemple sont installés avec le package d’installation hello. *ClusterConfig.Unsecure.DevCluster.json* est la configuration de cluster la plus simple de hello : un cluster non sécurisé, trois nœuds en cours d’exécution sur un seul ordinateur.  Les autres fichiers de configuration décrivent des clusters uniques ou de plusieurs ordinateurs, sécurisés à l’aide de certificats X.509 ou de la sécurité Windows.  Superflus toomodify un des paramètres de configuration par défaut hello pour ce didacticiel, mais recherchez dans le fichier de configuration hello et vous familiariser avec les paramètres hello.  Hello **nœuds** section décrit les trois nœuds de cluster de hello de hello : nom, adresse IP, [type de nœud, domaine d’erreur et un domaine de mise à niveau](service-fabric-cluster-manifest.md#nodes-on-the-cluster).  Hello **propriétés** section définit hello [sécurité, niveau de fiabilité, collecte des diagnostics et types de nœuds](service-fabric-cluster-manifest.md#cluster-properties) pour le cluster de hello.

Ce cluster n’est pas sécurisé.  N’importe qui peut se connecter anonymement et effectuer des opérations de gestion. Les clusters de production doivent donc toujours être sécurisés à l’aide de certificats X.509 ou via la sécurité Windows.  La sécurité est configurée uniquement au moment de la création de cluster et n’est pas possible tooenable sécurité après que hello cluster est créé.  Lecture [sécuriser un cluster](service-fabric-cluster-security.md) toolearn plus sur la sécurité du cluster Service Fabric.  

cluster de développement de trois nœuds hello toocreate, exécutez hello *CreateServiceFabricCluster.ps1* script à partir d’une session PowerShell d’administrateur :

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

package de runtime Service Fabric Hello est automatiquement téléchargé et installé au moment de la création du cluster.

## <a name="connect-toohello-cluster"></a>Se connecter toohello cluster
Votre cluster de développement à trois nœuds est maintenant en cours d’exécution. Hello module ServiceFabric PowerShell est installé avec le runtime de hello.  Vous pouvez vérifier ce cluster hello est en cours d’exécution à partir de hello même ordinateur ou à partir d’un ordinateur distant avec le runtime du Service Fabric hello.  Hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) applet de commande établit un cluster de toohello de connexion.   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint localhost:19000
```
Consultez [cluster sécurisée de se connecter tooa](service-fabric-connect-to-secure-cluster.md) pour obtenir des exemples de connexion tooa cluster. Après la connexion toohello cluster, utilisez hello [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) toodisplay de l’applet de commande une liste de nœuds dans les informations de cluster et d’état hello pour chaque nœud. **HealthState** doit être à l’état *OK* pour chaque nœud.

```powershell
PS C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- -------- --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     vm2      localhost       NodeType2 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm1      localhost       NodeType1 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm0      localhost       NodeType0 5.6.220.9494 0                     Up 00:02:43   00:00:00              OK
```

## <a name="visualize-hello-cluster-using-service-fabric-explorer"></a>Visualiser le cluster hello à l’aide de l’Explorateur de Service Fabric
[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) est un bon outil pour visualiser votre cluster et gérer les applications.  Service Fabric Explorer est un service qui s’exécute dans un cluster de hello, laquelle vous accédez à l’aide d’un navigateur en parcourant trop[http://localhost:19080/Explorer](http://localhost:19080/Explorer). 

tableau de bord Hello cluster fournit une vue d’ensemble de votre cluster, y compris un résumé de l’application et d’intégrité de nœud. affichage du nœud Hello montre la disposition physique de hello du cluster de hello. Vous pouvez identifier les applications ayant déployé du code sur un nœud donné.

![Service Fabric Explorer][service-fabric-explorer]

## <a name="remove-hello-cluster"></a>Supprimer le cluster de hello
tooremove un cluster, exécutez hello *RemoveServiceFabricCluster.ps1* script PowerShell à partir de dossier du package hello et passe hello chemin d’accès toohello fichier de configuration JSON. Vous pouvez éventuellement spécifier un emplacement pour le journal de hello de suppression de hello.

```powershell
# Removes Service Fabric cluster nodes from each computer in hello configuration file.
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -Force
```

tooremove le runtime Service Fabric hello à partir de l’ordinateur hello, exécutez hello suite du script PowerShell à partir du dossier du package hello.

```powershell
# Removes Service Fabric from hello current computer.
.\CleanFabric.ps1
```

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez configuré un cluster autonome de développement, essayez hello suivant des articles :
* [Configurez un cluster de plusieurs ordinateurs autonome](service-fabric-cluster-creation-for-windows-server.md) et activez la sécurité.
* [Déployer des applications à l’aide de PowerShell](service-fabric-deploy-remove-applications.md)

[service-fabric-explorer]: ./media/service-fabric-get-started-standalone-cluster/sfx.png
