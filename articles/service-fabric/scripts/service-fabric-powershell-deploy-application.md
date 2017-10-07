---
title: "aaaAzure exemple de Script PowerShell - déploiement d’application tooa cluster | Documents Microsoft"
description: "Script Azure PowerShell exemple - déploiement d’un cluster de Service Fabric application tooa."
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
ms.openlocfilehash: b417c9908c72f016e930c43ff2d13e0cc5451f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-service-fabric-cluster"></a>Déployer un cluster de Service Fabric application tooa

Cet exemple de script copie d’un magasin d’image application package tooa cluster enregistre le type de l’application hello dans un cluster de hello et crée une instance d’application à partir du type d’application hello.  Si tous les services par défaut ont été définies dans le manifeste de l’application hello hello cible du type d’application, ces services sont créés pour l’instant. Personnaliser les paramètres de hello en fonction des besoins. 

Si nécessaire, installez le module PowerShell de l’infrastructure de Service de hello avec hello [Service Fabric SDK](../service-fabric-get-started.md). 

## <a name="sample-script"></a>Exemple de script

[!code-powershell[main](../../../powershell_scripts/service-fabric/deploy-application/deploy-application.ps1 "Deploy an application tooa cluster")]

## <a name="clean-up-deployment"></a>Nettoyer le déploiement 

Une fois l’exemple de script hello a été exécuté, hello script dans [supprimer une application](service-fabric-powershell-remove-application.md) peut être l’instance de l’application hello tooremove utilisé, annuler l’inscription du type de l’application hello et supprimer le package d’application hello à partir du magasin d’images hello.

## <a name="script-explanation"></a>Explication du script

Ce script utilise hello suivant les commandes. Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.

| Commande | Remarques |
|---|---|
| [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | Copier un magasin d’image application package toohello cluster.  |
|[Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps)| Inscrit un type d’application et la version sur le cluster de hello. |
|[New-ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps)| Crée une application à partir d’un type d’application inscrit. |

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur le module PowerShell de l’infrastructure de Service de hello, consultez [documentation Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).

Vous trouverez des exemples supplémentaires de Powershell pour Azure Service Fabric Bonjour [exemples Azure PowerShell](../service-fabric-powershell-samples.md).
