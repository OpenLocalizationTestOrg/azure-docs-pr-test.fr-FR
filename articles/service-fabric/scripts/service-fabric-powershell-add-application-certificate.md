---
title: aaaAzure exemple de Script PowerShell - ajouter application cert tooa cluster | Documents Microsoft
description: Script Azure PowerShell exemple - ajouter un cluster de Service Fabric application certificat tooa.
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
ms.openlocfilehash: aba62598e2e4775012f89b5070bef5e61aec64f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-an-application-certificate-tooa-service-fabric-cluster"></a>Ajouter un cluster de Service Fabric application certificat tooa

Cet exemple de script crée un certificat auto-signé dans le coffre de clés Azure spécifié hello et l’installe tooall des nœuds de cluster du Service Fabric hello. certificat de Hello télécharge également le dossier local de tooa. nom Hello du certificat de hello téléchargé est hello identique au nom du certificat hello dans le coffre de clés hello hello. Personnaliser les paramètres de hello en fonction des besoins.

Si nécessaire, installez hello Azure PowerShell en utilisant une instruction de hello trouvé dans hello [guide Azure PowerShell](/powershell/azure/overview) , puis exécutez `Login-AzureRmAccount` toocreate une connexion avec Azure. 

## <a name="sample-script"></a>Exemple de script

[!code-powershell[main](../../../powershell_scripts/service-fabric/add-application-certificate/add-new-application-certificate.ps1 "Add an application certificate tooa cluster")]

## <a name="script-explanation"></a>Explication du script

Ce script utilise hello suivant de commandes : chaque commande dans la table de hello lie la documentation spécifique de toocommand.

| Commande | Remarques |
|---|---|
| [Add-AzureRmServiceFabricApplicationCertificate](/powershell/module/azurerm.servicefabric/Add-AzureRmServiceFabricApplicationCertificate) | Ajouter qu'une nouvelle application certificat toohello machine virtuelle identiques qui composent le cluster de hello.  |

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur le module Azure PowerShell de hello, consultez [documentation Azure PowerShell](/powershell/azure/overview).

Vous trouverez des exemples supplémentaires de Azure Powershell pour Azure Service Fabric Bonjour [exemples Azure PowerShell](../service-fabric-powershell-samples.md).
