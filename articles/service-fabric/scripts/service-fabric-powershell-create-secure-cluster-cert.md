---
title: "aaaAzure exemple de Script PowerShell - créer un cluster Service Fabric | Documents Microsoft"
description: "Exemple de script Azure PowerShell - Créer un cluster Service Fabric"
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0f9c8bc5-3789-4eb3-8deb-ae6e2200795a
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 12fdc201bd51688cb850cd456b1e00442b79c22d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster"></a>Créer un cluster Service Fabric

Cet exemple de script crée un cluster Service Fabric à cinq nœuds sécurisé avec un certificat X.509.  commande Hello crée un certificat auto-signé et il télécharge tooa nouveau coffre de clés. Hello certificat est également copié tooa les répertoire local.  Ensemble hello *-OS* version de hello paramètre toochoose de Windows ou Linux qui s’exécute sur les nœuds de cluster hello.  Personnaliser les paramètres de hello en fonction des besoins.

Si nécessaire, installez hello Azure PowerShell en utilisant une instruction de hello trouvé dans hello [guide Azure PowerShell](/powershell/azure/overview) , puis exécutez `Login-AzureRmAccount` toocreate une connexion avec Azure. 

## <a name="sample-script"></a>Exemple de script

[!code-powershell[main](../../../powershell_scripts/service-fabric/create-secure-cluster/create-secure-cluster.ps1 "Create a Service Fabric cluster")]

## <a name="clean-up-deployment"></a>Nettoyer le déploiement 

Après exécution de l’exemple de script hello, hello commande suivante peut être groupe de ressources utilisé tooremove hello, cluster et toutes les ressources.

```powershell
$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="script-explanation"></a>Explication du script

Ce script utilise hello suivant les commandes. Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.

| Commande | Remarques |
|---|---|
| [New-AzureRmServiceFabricCluster](/powershell/module/azurerm.servicefabric/New-AzureRmServiceFabricCluster) | Crée un cluster Service Fabric. |

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur le module Azure PowerShell de hello, consultez [documentation Azure PowerShell](/powershell/azure/overview).

Vous trouverez des exemples supplémentaires de Azure Powershell pour Azure Service Fabric Bonjour [exemples Azure PowerShell](../service-fabric-powershell-samples.md).
