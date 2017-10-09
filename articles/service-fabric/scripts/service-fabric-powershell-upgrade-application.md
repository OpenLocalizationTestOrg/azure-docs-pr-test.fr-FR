---
title: "aaaAzure exemple de Script PowerShell - mise à niveau une application de Service Fabric | Documents Microsoft"
description: "Exemple de script Azure PowerShell - Mettre à niveau une application Service Fabric."
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 4f4777607bd6b35a76029e09ddb441006565d4cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-service-fabric-application"></a>Mettre à niveau une application Service Fabric

Cet exemple de script met à niveau une infrastructure de Service en cours d’exécution de tooversion d’instance application version 1.3.0. script de Hello copie hello nouveau package toohello cluster image Boutique d’applications, inscrit le type de l’application hello, démarre une mise à niveau analysée et vérifie en permanence l’état de mise à niveau hello jusqu'à ce que la mise à niveau hello se termine ou est restaurée. Personnaliser les paramètres de hello en fonction des besoins. 

Si nécessaire, installez le module PowerShell de l’infrastructure de Service de hello avec hello [Service Fabric SDK](../service-fabric-get-started.md). 

## <a name="sample-script"></a>Exemple de script

[!code-powershell[main](../../../powershell_scripts/service-fabric/upgrade-application/upgrade-application.ps1 "Upgrade an application")]

## <a name="script-explanation"></a>Explication du script

Ce script utilise hello suivant les commandes. Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.

| Commande | Remarques |
|---|---|
| [Get-ServiceFabricApplication](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps) | Obtient toutes les applications hello dans le cluster Service Fabric de hello ou une application spécifique.  |
| [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) | Obtient l’état hello d’une mise à niveau des applications de Service Fabric. |
| [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) | Obtient les types d’applications de Service Fabric hello inscrits sur le cluster Service Fabric de hello. |
| [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | Annule l’enregistrement d’un type d’application Service Fabric.  |
| [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | Copie une image de toohello du package d’application de Service Fabric magasin.  |
| [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) | Enregistre un type d’application Service Fabric. |
| [Start-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) | Met à niveau une version de type de Service Fabric application toohello application spécifiée. |


## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur le module PowerShell de l’infrastructure de Service de hello, consultez [documentation Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).

Vous trouverez des exemples supplémentaires de Powershell pour Azure Service Fabric Bonjour [exemples Azure PowerShell](../service-fabric-powershell-samples.md).
