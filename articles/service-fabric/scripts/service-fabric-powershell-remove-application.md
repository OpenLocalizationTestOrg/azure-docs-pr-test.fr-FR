---
title: "aaaAzure exemple de Script PowerShell - supprimer une application à partir d’un cluster | Documents Microsoft"
description: "Exemple de script Azure PowerShell - Supprimer une application d’un cluster Service Fabric"
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
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 3fe2082c2fbeffbff1622f206021d4d907197d19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a>Supprimer une application d’un cluster Service Fabric

Cet exemple de script supprime une instance en cours d’exécution de l’application Service Fabric, annule l’inscription d’un type d’application et la version du cluster de hello et supprime le package d’application hello à partir du magasin d’images hello cluster.  Instance de l’application hello suppression supprime également hello toutes les instances de service associés à cette application en cours d’exécution. Personnaliser les paramètres de hello en fonction des besoins. 

Si nécessaire, installez le module PowerShell de l’infrastructure de Service de hello avec hello [Service Fabric SDK](../service-fabric-get-started.md). 

## <a name="sample-script"></a>Exemple de script

[!code-powershell[main](../../../powershell_scripts/service-fabric/remove-application/remove-application.ps1 "Remove an application from a cluster")]

## <a name="script-explanation"></a>Explication du script

Ce script utilise hello suivant les commandes. Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.

| Commande | Remarques |
|---|---|
| [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) | Supprime une instance d’application en cours d’exécution de l’infrastructure de Service de cluster de hello.  |
| [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | Annule l’inscription d’un type d’application Service Fabric et une version à partir du cluster de hello. |
| [Remove-ServiceFabricApplicationPackage](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) | Supprime un package d’application Service Fabric de magasin d’images hello.|

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur le module PowerShell de l’infrastructure de Service de hello, consultez [documentation Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).

Vous trouverez des exemples supplémentaires de Powershell pour Azure Service Fabric Bonjour [exemples Azure PowerShell](../service-fabric-powershell-samples.md).
