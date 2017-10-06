---
title: "aaaCreate un serveur Azure Analysis Services à l’aide de PowerShell | Documents Microsoft"
description: "Découvrez comment toocreate un Azure Analysis Services server à l’aide de PowerShell"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 08/01/2017
ms.author: owend
ms.custom: mvc
ms.openlocfilehash: 269b78983410f773d47c4cea34d6d353b19f9e91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-by-using-powershell"></a>Créer un serveur Azure Analysis Services à l’aide de PowerShell

Ce démarrage rapide décrit à l’aide de PowerShell à partir de toocreate de ligne de commande hello un serveur Azure Analysis Services dans un [groupe de ressources Azure](../azure-resource-manager/resource-group-overview.md) dans votre abonnement Azure.

Cette tâche requiert le module Azure PowerShell version 4.0 ou ultérieure. version de hello toofind, exécutez ` Get-Module -ListAvailable AzureRM`. tooinstall ou mise à niveau, consultez [installez Azure PowerShell module](/powershell/azure/install-azurerm-ps). 

> [!NOTE]
> La création d’un serveur peut donner lieu à un nouveau service facturable. toolearn, voir [Analysis Services tarification](https://azure.microsoft.com/pricing/details/analysis-services/).

## <a name="prerequisites"></a>Composants requis
toocomplete ce démarrage rapide, vous devez :

* **Abonnement Azure**: visitez [d’évaluation gratuite Azure](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate un compte.
* **Azure Active Directory** : votre abonnement doit être associé à un client Azure Active Directory et vous devez disposer d’un compte dans ce répertoire. toolearn, voir [d’authentification et les autorisations utilisateur](analysis-services-manage-users.md).

## <a name="import-azurermanalysisservices-module"></a>Importer le module de AzureRm.AnalysisServices
toocreate un serveur dans votre abonnement, vous utilisez hello [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices) module de composant. Charger le module AzureRm.AnalysisServices hello dans votre session PowerShell.

```powershell
Import-Module AzureRM.AnalysisServices
```

## <a name="sign-in-tooazure"></a>Connectez-vous à tooAzure

Se connecter à l’aide de hello tooyour abonnement Azure [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) commande. Suivez hello à l’écran.

```powershell
Add-AzureRmAccount
```

## <a name="create-a-resource-group"></a>Créer un groupe de ressources
 
Un [groupe de ressources Azure](../azure-resource-manager/resource-group-overview.md) est un conteneur logique dans lequel les ressources Azure sont déployées et gérées en tant que groupe. Lorsque vous créez votre serveur, vous devez spécifier un groupe de ressources dans votre abonnement. Si vous n’avez pas déjà un groupe de ressources, vous pouvez créer un autre à l’aide de hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) commande. Hello exemple suivant crée un groupe de ressources nommé `myResourceGroup` dans la région ouest des États-Unis hello.

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
```

## <a name="create-a-server"></a>Créer un serveur

Créer un nouveau serveur à l’aide de hello [New-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) commande. Hello exemple suivant crée un serveur nommé myServer dans myResourceGroup, dans la région ouest des États-Unis hello, au niveau de hello D1 et spécifie philipc@adventureworks.com en tant qu’un administrateur de serveur.

```powershell
New-AzureRmAnalysisServicesServer -ResourceGroupName "myResourceGroup" -Name "myServer" -Location West US -Sku D1 -Administrator "philipc@adventure-works.com"
```

## <a name="clean-up-resources"></a>Supprimer des ressources

Vous pouvez supprimer le serveur de hello à partir de votre abonnement à l’aide de hello [Remove-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) commande. Si vous continuez avec d’autres démarrages rapides et didacticiels de cette collection, ne supprimez pas votre serveur. Hello exemple suivant supprime du serveur hello créé à l’étape précédente de hello.


```powershell
Remove-AzureRmAnalysisServicesServer -Name "myServer" -ResourceGroupName "myResourceGroup"
```

## <a name="next-steps"></a>Étapes suivantes
[Gérer Azure Analysis Services avec PowerShell](analysis-services-powershell.md)   
[Déployer un modèle à partir de SSDT](analysis-services-deploy.md)   
[Créer un modèle dans le portail Azure](analysis-services-create-model-portal.md)