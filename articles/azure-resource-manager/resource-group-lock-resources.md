---
title: modifications de tooprevent de ressources Azure aaaLock | Documents Microsoft
description: "Empêchez les utilisateurs de mettre à jour ou de supprimer des ressources Azure critiques en appliquant un verrou à tous les utilisateurs et rôles."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 53c57e8f-741c-4026-80e0-f4c02638c98b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: tomfitz
ms.openlocfilehash: 1f0d8911b2b129069bd2f01a9a4ec0a3cf700118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="lock-resources-tooprevent-unexpected-changes"></a>Verrouiller les ressources tooprevent modifications inattendues 
En tant qu’administrateur, vous devrez peut-être toolock un abonnement, groupe de ressources ou ressource tooprevent autres utilisateurs de votre organisation d’accidentellement supprimer ou modifier des ressources critiques. Vous pouvez définir au niveau du verrou hello trop**CanNotDelete** ou **ReadOnly**. 

* **CanNotDelete** signifie que les utilisateurs autorisés peuvent toujours lire et modifier une ressource, mais ils ne peuvent pas supprimer la ressource de hello. 
* **En lecture seule** signifie que les utilisateurs autorisés peuvent lire une ressource, mais ils ne peuvent pas supprimer ou mettre à jour la ressource de hello. Appliquer ce verrou est similaire toorestricting tout autorisé toohello aux utilisateurs des autorisations accordées par hello **lecteur** rôle. 

## <a name="how-locks-are-applied"></a>Application des verrous

Lorsque vous appliquez un verrou sur une portée parent, toutes les ressources dans cette étendue héritent hello même verrou. Même les ressources que vous ajouterez ultérieurement héritent de verrou de hello parent de hello. verrou de Hello plus restrictif dans l’héritage hello est prioritaire.

Contrairement au contrôle d’accès basé sur un rôle, vous utilisez Gestion des verrous tooapply une restriction sur tous les utilisateurs et les rôles. toolearn sur la définition des autorisations pour les utilisateurs et les rôles, consultez [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).

Verrous de gestionnaire de ressources s’appliquent uniquement aux toooperations qui se produisent dans le plan de gestion de hello, qui se compose d’opérations envoyées trop`https://management.azure.com`. les verrous Hello ne limitent pas la façon dont les ressources effectuent leurs propres fonctions. Les modifications des ressources sont limitées, mais pas les opérations sur les ressources. Par exemple, un verrou en lecture seule sur une base de données SQL vous empêche de supprimer ou modifier la base de données hello, mais il ne vous empêche pas de création, mise à jour ou supprimer des données dans la base de données hello. Les transactions de données sont autorisées, car ces opérations ne sont pas envoyées trop`https://management.azure.com`.

Application **ReadOnly** peut entraîner des résultats de toounexpected, car certaines opérations semblent lire opérations nécessitent réellement des actions supplémentaires. Par exemple, placer un **ReadOnly** verrou sur un compte de stockage empêche tous les utilisateurs d’afficher la liste des clés de hello. liste Hello opération clés est gérée via une demande POST car hello retourné clés sont disponibles pour les opérations d’écriture. Pour un autre exemple, placer un **ReadOnly** verrou sur une ressource de Service de l’application empêche l’Explorateur de serveurs Visual Studio à partir de l’affichage des fichiers pour la ressource de hello, car cette interaction nécessite un accès en écriture.

## <a name="who-can-create-or-delete-locks-in-your-organization"></a>Personnes autorisées à créer ou supprimer des verrous dans votre organisation
toocreate ou supprimer les verrous de gestion, vous devez avoir accès trop`Microsoft.Authorization/*` ou `Microsoft.Authorization/locks/*` actions. Hello rôles intégrés uniquement **propriétaire** et **administrateur de l’accès utilisateur** sont accordées à ces actions.

## <a name="portal"></a>Portail
[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="template"></a>Modèle
Hello suivant montre un modèle qui crée un verrou sur un compte de stockage. compte de stockage Hello sur le tooapply le verrou de hello est fourni en tant que paramètre. nom du verrou de hello Hello est créé en concaténant le nom de ressource hello avec **/Microsoft.Authorization/** et hello nom du verrou de hello, dans ce cas **myLock**.

type Hello fourni est type de ressource toohello spécifique. Pour le stockage, la valeur hello type too"Microsoft.Storage/storageaccounts/providers/locks ».

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "lockedResource": {
          "type": "string"
        }
      },
      "resources": [
        {
          "name": "[concat(parameters('lockedResource'), '/Microsoft.Authorization/myLock')]",
          "type": "Microsoft.Storage/storageAccounts/providers/locks",
          "apiVersion": "2015-01-01",
          "properties": {
            "level": "CannotDelete"
          }
        }
      ]
    }

## <a name="powershell"></a>PowerShell
Verrou vous déployés ressources avec Azure PowerShell à l’aide de hello [New-AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock) commande.

toolock une ressource, fournissez hello nom hello, son type de ressource et son nom de groupe de ressources.

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockSite `
  -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

toolock un groupe de ressources, fournir un nom hello hello du groupe de ressources.

```powershell
New-AzureRmResourceLock -LockName LockGroup -LockLevel CanNotDelete `
  -ResourceGroupName exampleresourcegroup
```

informations de tooget sur un verrou, utilisez [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock). tooget tous les verrous hello dans votre abonnement, utilisez :

```powershell
Get-AzureRmResourceLock
```

tooget tous les verrous d’une ressource, utilisez :

```powershell
Get-AzureRmResourceLock -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

tooget tous les verrous d’un groupe de ressources, utilisez :

```powershell
Get-AzureRmResourceLock -ResourceGroupName exampleresourcegroup
```

Azure PowerShell fournit des autres commandes pour les verrous de travail, tels que [Set-AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) tooupdate un verrou, et [Remove-AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) toodelete un verrou.

## <a name="azure-cli"></a>Interface de ligne de commande Azure

Verrou vous déployés ressources avec CLI d’Azure à l’aide de hello [créer de verrou de az](/cli/azure/lock#create) commande.

toolock une ressource, fournissez hello nom hello, son type de ressource et son nom de groupe de ressources.

```azurecli
az lock create --name LockSite --lock-type CanNotDelete \
  --resource-group exampleresourcegroup --resource-name examplesite \
  --resource-type Microsoft.Web/sites
```

toolock un groupe de ressources, fournir un nom hello hello du groupe de ressources.

```azurecli
az lock create --name LockGroup --lock-type CanNotDelete \
  --resource-group exampleresourcegroup
```

informations de tooget sur un verrou, utilisez [liste des verrous az](/cli/azure/lock#list). tooget tous les verrous hello dans votre abonnement, utilisez :

```azurecli
az lock list
```

tooget tous les verrous d’une ressource, utilisez :

```azurecli
az lock list --resource-group exampleresourcegroup --resource-name examplesite \
  --namespace Microsoft.Web --resource-type sites --parent ""
```

tooget tous les verrous d’un groupe de ressources, utilisez :

```azurecli
az lock list --resource-group exampleresourcegroup
```

CLI Azure fournit des autres commandes pour les verrous de travail, tels que [mise à jour du verrou az](/cli/azure/lock#update) tooupdate un verrou, et [supprimer de verrou de az](/cli/azure/lock#delete) toodelete un verrou.

## <a name="rest-api"></a>API REST
Vous pouvez verrouiller les ressources déployées par hello [API REST pour les verrous de gestion](https://docs.microsoft.com/rest/api/resources/managementlocks). Hello API REST vous toocreate et supprimer les verrous et récupérer des informations sur les verrous existants.

toocreate un verrou, exécutez :

    PUT https://management.azure.com/{scope}/providers/Microsoft.Authorization/locks/{lock-name}?api-version={api-version}

étendue de Hello peut être un abonnement, le groupe de ressources ou la ressource. Hello-nom du verrou est tout ce que vous voulez verrouiller de hello toocall. Pour la version de l’API, utilisez **2015-01-01**.

Dans la demande de hello, inclure un objet JSON qui spécifie les propriétés hello pour les verrous hello.

    {
      "properties": {
        "level": "CanNotDelete",
        "notes": "Optional text notes."
      }
    } 

## <a name="next-steps"></a>Étapes suivantes
* Pour plus d’informations sur l’utilisation de verrous sur des ressources, consultez [Lock Down Your Azure Resources](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)
* toolearn sur l’organisation logique de vos ressources, consultez [à l’aide des balises tooorganize vos ressources](resource-group-using-tags.md)
* toochange groupe de ressources auquel une ressource se trouve dans, consultez [déplacer le groupe ressource toonew ressources](resource-group-move-resources.md)
* Vous pouvez appliquer des restrictions et des conventions sur votre abonnement avec des stratégies personnalisées. Pour plus d’informations, consultez [ressources toomanage de stratégie d’utilisation et de contrôler l’accès](resource-manager-policy.md).
* Pour obtenir des conseils comment les entreprises peuvent utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise - gouvernance de l’abonnement normative](resource-manager-subscription-governance.md).

