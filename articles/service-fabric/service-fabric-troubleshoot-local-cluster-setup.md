---
title: aaaTroubleshoot votre configuration du cluster Service Fabric locale | Documents Microsoft
description: "Cet article aborde un ensemble de suggestions relatives à la résolution des problèmes de votre cluster de développement local"
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: 97f4feaa-bba0-47af-8fdd-07f811fe2202
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: ce36f62a4bc69d2cd5b6c3df4abda6ca88fa84f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-your-local-development-cluster-setup"></a>Résoudre les problèmes d'installation de votre cluster de développement local
Si vous rencontrez un problème lors de l’interaction avec votre cluster de développement local Azure Service Fabric, passez en revue hello suivant des suggestions pour les solutions possibles.

## <a name="cluster-setup-failures"></a>Échecs de configuration du cluster
### <a name="cannot-clean-up-service-fabric-logs"></a>Impossible de nettoyer les journaux de Service Fabric
#### <a name="problem"></a>Problème
Lorsque vous exécutez le script de DevClusterSetup hello, vous voyez ce type d’erreur :

    Cannot clean up C:\SfDevCluster\Log fully as references are likely being held tooitems in it. Please remove those and run this script again.
    At line:1 char:1 + .\DevClusterSetup.ps1
    + ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : NotSpecified: (:) [Write-Error], WriteErrorException
    + FullyQualifiedErrorId : Microsoft.PowerShell.Commands.WriteErrorException,DevClusterSetup.ps1


#### <a name="solution"></a>Solution
Fermez hello fenêtre actuelle de PowerShell et ouvrir une nouvelle fenêtre PowerShell en tant qu’administrateur. Vous devez maintenant être en mesure de toosuccessfully exécuter le script de hello.

## <a name="cluster-connection-failures"></a>Échecs de connexion au cluster
### <a name="service-fabric-powershell-cmdlets-are-not-recognized-in-azure-powershell"></a>Applets de commande PowerShell de Service Fabric non reconnues dans Azure PowerShell
#### <a name="problem"></a>Problème
Si vous essayez toorun des hello applets de commande PowerShell de l’infrastructure de Service, tel que `Connect-ServiceFabricCluster` dans une fenêtre Azure PowerShell, il échoue, indiquant que cette applet de commande hello n’est pas reconnu. Hello fait que Azure PowerShell utilise hello 32 bits de Windows PowerShell (même sur les versions de système d’exploitation 64 bits), alors que hello applets de commande Service Fabric fonctionnent uniquement dans les environnements 64 bits.

#### <a name="solution"></a>Solution
Exécutez toujours les applets de commande Service Fabric directement à partir de Windows PowerShell.

> [!NOTE]
> version la plus récente d’Azure PowerShell Hello ne crée pas un raccourci spécial, donc cela ne devrait plus apparaître.
> 
> 

### <a name="type-initialization-exception"></a>Exception durant l’initialisation de type
#### <a name="problem"></a>Problème
Lorsque vous vous connectez le cluster toohello dans PowerShell, vous voyez l’erreur hello TypeInitializationException pour System.Fabric.Common.AppTrace.

#### <a name="solution"></a>Solution
Votre variable PATH n’a pas été correctement définie durant l’installation. Déconnectez-vous de Windows, puis reconnectez-vous. Le chemin d’accès est alors actualisé.

### <a name="cluster-connection-fails-with-object-is-closed"></a>La connexion au cluster est mise en échec avec une indication de fermeture de l’objet
#### <a name="problem"></a>Problème
Un appel tooConnect-ServiceFabricCluster échoue avec une erreur comme suit :

    Connect-ServiceFabricCluster : hello object is closed.
    At line:1 char:1
    + Connect-ServiceFabricCluster
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : InvalidOperation: (:) [Connect-ServiceFabricCluster], FabricObjectClosedException
    + FullyQualifiedErrorId : CreateClusterConnectionErrorId,Microsoft.ServiceFabric.Powershell.ConnectCluster

#### <a name="solution"></a>Solution
Fermez hello fenêtre actuelle de PowerShell et ouvrir une nouvelle fenêtre PowerShell en tant qu’administrateur. Vous devez maintenant être en mesure de se connecter de toosuccessfully.

### <a name="fabric-connection-denied-exception"></a>Exception Connexion Fabric refusée
#### <a name="problem"></a>Problème
Pendant le débogage à partir de Visual Studio, vous obtenez une erreur FabricConnectionDeniedException.

#### <a name="solution"></a>Solution
Cette erreur se produit généralement lorsque vous essayez de toostart un processus hôte de service manuellement, au lieu de laisser toostart de runtime Service Fabric hello pour vous.

Assurez-vous de ne pas disposer de projets de service définis en tant que projets de démarrage dans votre solution. Seuls les projets d’application Service Fabric doivent être définis en tant que projets de démarrage.

> [!TIP]
> Si, après l’installation, votre cluster local commence toobehave anormalement, vous pouvez réinitialiser à l’aide d’application de barre d’état système hello cluster local manager. Cette supprime hello cluster existant et configurer un nouveau. Notez que toutes les applications déployées et les données associées sont supprimées.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
* [Comprendre votre cluster et résoudre les problèmes à l’aide des rapports d’intégrité système](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [Visualiser votre cluster à l’aide de l’outil Service Fabric Explorer](service-fabric-visualizing-your-cluster.md)

