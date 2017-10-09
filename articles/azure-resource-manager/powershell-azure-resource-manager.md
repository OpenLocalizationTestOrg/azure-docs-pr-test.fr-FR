---
title: aaaManage Azure solutions avec PowerShell | Documents Microsoft
description: Utiliser Azure PowerShell et le Gestionnaire de ressources toomanage vos ressources.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: b33b7303-3330-4af8-8329-c80ac7e9bc7f
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: powershell
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: 47a91af8d7eb59585bcfd43571ce76b90a0d7971
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-resources-with-azure-powershell-and-resource-manager"></a>Gérer les ressources avec Azure PowerShell et Resource Manager
> [!div class="op_single_selector"]
> * [Portail](resource-group-portal.md)
> * [Interface de ligne de commande Azure](xplat-cli-azure-resource-manager.md)
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [API REST](resource-manager-rest-api.md)
>
>

Dans cet article, vous apprendrez comment toomanage vos solutions avec Azure PowerShell et le Gestionnaire de ressources Azure. Si vous n’êtes pas familiarisé avec Resource Manager, consultez la page [Vue d’ensemble de Resource Manager](resource-group-overview.md). Cette rubrique se concentre sur les tâches de gestion. Vous allez :

1. Créer un groupe de ressources
2. Ajouter un groupe de ressources toohello
3. Ajouter une ressource de toohello de balise
4. Interroger les ressources selon des noms ou des valeurs de balise
5. Appliquer et supprimer un verrou sur une ressource de hello
6. Supprimer un groupe de ressources

Cet article ne montre pas comment toodeploy un abonnement de tooyour de modèle de gestionnaire de ressources. Pour plus d’informations, voir [Déployer des ressources à l’aide de modèles Resource Manager et d’Azure PowerShell](resource-group-template-deploy.md).

## <a name="get-started-with-azure-powershell"></a>Prise en main de Microsoft Azure PowerShell

Si vous n’avez pas installé Azure PowerShell, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).

Si vous avez installé Azure PowerShell Bonjour cours mais que vous n'avez pas mis à jour récemment, envisagez d’installer la version la plus récente hello. Vous pouvez mettre à jour la version hello via hello même méthode que vous avez utilisé tooinstall il. Par exemple, si vous avez utilisé hello Web Platform Installer, relancer et recherchez une mise à jour.

utilisation de votre version de module de ressources Azure, de hello toocheck hello suivant l’applet de commande :

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

Cette rubrique a été mise à jour pour la version 3.3.0. Si vous avez une version antérieure, votre expérience peut ne pas correspond hello décrite dans cette rubrique. Pour plus d’informations sur les applets de commande hello dans cette version, consultez [AzureRM.Resources Module](/powershell/module/azurerm.resources).

## <a name="log-in-tooyour-azure-account"></a>Ouvrez une session dans tooyour compte Azure
Avant d’utiliser votre solution, vous devez vous connecter tooyour compte.

toolog dans tooyour compte Azure, utilisez hello **AzureRmAccount de connexion** applet de commande.

```powershell
Login-AzureRmAccount
```

applet de commande Hello vous demande des informations d’identification de connexion hello pour votre compte Azure. Une fois connecté, il télécharge les paramètres de votre compte afin qu’ils soient disponible tooAzure PowerShell.

applet de commande Hello retourne des informations sur votre toouse d’abonnement de compte et hello pour les tâches de hello.

```powershell
Environment           : AzureCloud
Account               : example@contoso.com
TenantId              : {guid}
SubscriptionId        : {guid}
SubscriptionName      : Example Subscription One
CurrentStorageAccount :

```

Si vous avez plusieurs abonnements, vous pouvez basculer tooa autre abonnement. Tout d’abord, nous allons voir tous les abonnements hello pour votre compte.

```powershell
Get-AzureRmSubscription
```

Les abonnements activés et désactivés sont retournés.

```powershell
SubscriptionName : Example Subscription One
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Two
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Three
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Disabled
```

tooswitch tooa autre abonnement, fournissez le nom d’abonnement de hello avec hello **Set-AzureRmContext** applet de commande.

```powershell
Set-AzureRmContext -SubscriptionName "Example Subscription Two"
```

## <a name="create-a-resource-group"></a>Créer un groupe de ressources
Avant de déployer n’importe quel abonnement tooyour de ressources, vous devez créer un groupe de ressources qui contient des ressources hello.

toocreate un groupe de ressources, utilisez hello **New-AzureRmResourceGroup** applet de commande. commande Hello utilise hello **nom** toospecify de paramètre un nom pour le groupe de ressources hello et hello **emplacement** paramètre toospecify son emplacement.

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location "South Central US"
```

sortie de Hello est Bonjour suivant le format :

```powershell
ResourceGroupName : TestRG1
Location          : southcentralus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/{guid}/resourceGroups/TestRG1
```

Si vous avez besoin de groupe de ressources tooretrieve hello plus tard, utilisez hello suivant l’applet de commande :

```powershell
Get-AzureRmResourceGroup -ResourceGroupName TestRG1
```

tooget tous hello des groupes de ressources dans votre abonnement, ne spécifiez pas un nom :

```powershell
Get-AzureRmResourceGroup
```

## <a name="add-resources-tooa-resource-group"></a>Ajouter le groupe de ressources tooa de ressources
tooadd un groupe de ressources toohello, vous pouvez utiliser hello **New-AzureRmResource** applet de commande ou une applet de commande est de type toohello spécifique de ressource que vous créez (comme **New-AzureRmStorageAccount**). Il peut s’avérer plus facile toouse une applet de commande qui est le type de ressource tooa spécifique, car il inclut des paramètres pour les propriétés hello qui sont nécessaires pour la ressource hello. toouse **New-AzureRmResource**, vous devez connaître tous les tooset de propriétés hello sans être invité à les entrer.

Toutefois, l’ajout d’une ressource via les applets de commande peut entraîner futures toute confusion, car la ressource hello n’existe pas dans un modèle de gestionnaire de ressources. Microsoft vous recommande de définir l’infrastructure hello pour votre solution Windows Azure dans un modèle de gestionnaire de ressources. Les modèles permettent de tooreliably et à plusieurs reprises de déployer votre solution. Dans le cadre de cette rubrique, vous créez un compte de stockage avec une applet de commande PowerShell et générerez plus tard un modèle à partir de votre groupe de ressources.

Hello suivant l’applet de commande crée un compte de stockage. Au lieu d’utiliser le nom hello hello illustré, fournissez un nom unique pour le compte de stockage hello. nom de Hello doit être comprise entre 3 et 24 caractères et utiliser uniquement des chiffres et des lettres minuscules. Si vous utilisez le nom hello hello illustré, vous recevez une erreur, car ce nom est déjà en cours d’utilisation.

```powershell
New-AzureRmStorageAccount -ResourceGroupName TestRG1 -AccountName mystoragename -Type "Standard_LRS" -Location "South Central US"
```

Si vous devez tooretrieve cette ressource ultérieurement, utilisez hello suivant l’applet de commande :

```powershell
Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1
```

## <a name="add-a-tag"></a>Ajouter une balise

Balises permettent tooorganize vos ressources en fonction des propriétés de toodifferent. Par exemple, peut avoir plusieurs ressources dans différents groupes de ressources qui appartiennent toohello même service. Vous pouvez appliquer une toomark de ressources de toothose balise et la valeur service en tant qu’appartenant toohello même catégorie. Vous pouvez également indiquer si une ressource est utilisée dans un environnement de production ou de test. Dans cette rubrique, vous appliquez des balises tooonly une ressource, mais dans votre environnement n’est plus probablement sens tooapply balises tooall vos ressources.

Hello suivant l’applet de commande applique le compte de stockage de deux balises tooyour :

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
 ```

Les balises sont mises à jour en tant qu’objet unique. tout d’abord, tooadd une ressource tooa balise qui contient déjà des balises, extraire les balises existantes hello. Ajouter hello nouvelle balise toohello objet qui contient les balises existantes hello et appliquer toutes les ressources de toohello balises hello.

```powershell
$tags = (Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
```

## <a name="search-for-resources"></a>Rechercher des ressources

Hello d’utilisation **recherche-AzureRmResource** ressources tooretrieve d’applet de commande pour les conditions de recherche différente.

* tooget une ressource par son nom, fournissez hello **ResourceNameContains** paramètre :

  ```powershell
  Find-AzureRmResource -ResourceNameContains mystoragename
  ```

* tooget toutes les ressources hello dans un groupe de ressources, fournir hello **ResourceGroupNameContains** paramètre :

  ```powershell
  Find-AzureRmResource -ResourceGroupNameContains TestRG1
  ```

* tooget toutes les ressources hello avec un nom de balise et la valeur fournir hello **TagName** et **TagValue** paramètres :

  ```powershell
  Find-AzureRmResource -TagName Dept -TagValue IT
  ```

* ressources de hello tooall avec un type particulier, fournissent des hello **ResourceType** paramètre :

  ```powershell
  Find-AzureRmResource -ResourceType Microsoft.Storage/storageAccounts
  ```

## <a name="lock-a-resource"></a>Verrouiller une ressource

Lorsque vous devez toomake vraiment une ressource critique n’est pas accidentellement supprimée ou modifiée, appliquer une ressource de toohello de verrou. Vous pouvez spécifier le niveau **CanNotDelete** ou **ReadOnly**.

toocreate ou supprimer les verrous de gestion, vous devez avoir accès trop`Microsoft.Authorization/*` ou `Microsoft.Authorization/locks/*` actions. Rôles intégrés hello uniquement propriétaire et administrateur de l’accès utilisateur sont accordées à ces actions.

tooapply un verrou, utilisez hello suivant l’applet de commande :

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

Hello ressource verrouillée Bonjour précédent exemple ne peut pas être supprimé tant que hello verrou soit supprimé. tooremove un verrou, utilisez :

```powershell
Remove-AzureRmResourceLock -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

Pour plus d’informations sur la définition des verrous, consultez [Verrouiller des ressources avec Azure Resource Manager](resource-group-lock-resources.md).

## <a name="remove-resources-or-resource-group"></a>Supprimer des ressources ou un groupe de ressources
Vous pouvez supprimer une ressource ou un groupe de ressources. Lorsque vous supprimez un groupe de ressources, vous supprimez également toutes les ressources de hello dans ce groupe de ressources.

* toodelete une ressource du groupe de ressources hello, utilisez hello **Remove-AzureRmResource** applet de commande. Cette applet de commande supprime la ressource de hello, mais ne supprime pas le groupe de ressources hello.

  ```powershell
  Remove-AzureRmResource -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
  ```

* toodelete un groupe de ressources et toutes ses ressources, utilisez hello **Remove-AzureRmResourceGroup** applet de commande.

  ```powershell
  Remove-AzureRmResourceGroup -Name TestRG1
  ```

Pour les deux applets de commande, vous êtes invité tooconfirm que vous souhaitez tooremove hello ressource ou un groupe de ressources. Si les opération hello supprime correctement hello ressource ou un groupe de ressources, elle retourne **True**.

## <a name="run-resource-manager-scripts-with-azure-automation"></a>Exécuter des scripts Resource Manager avec Azure Automation

Cette rubrique vous montre comment les opérations de base tooperform sur vos ressources Azure PowerShell. Pour les scénarios de gestion plus avancées, vous généralement souhaitez toocreate un script et réutilisez ce script en fonction des besoins, ou selon une planification. [Azure Automation](../automation/automation-intro.md) offre un moyen pour vous des scripts de tooautomate fréquemment utilisé pour gérer vos solutions Azure.

Hello rubriques suivantes vous montrent comment toouse Azure Automation, Gestionnaire de ressources et PowerShell tooeffectively effectuent des tâches de gestion :

- Pour plus d’informations sur la création d’un runbook, consultez [Mon premier Runbook PowerShell](../automation/automation-first-runbook-textual-powershell.md).
- Pour plus d’informations sur l’utilisation des galeries de scripts, consultez [Galeries de runbooks et de modules pour Azure Automation](../automation/automation-runbook-gallery.md).
- Pour les procédures opérationnelles démarrer et arrêter les machines virtuelles, consultez [scénario d’Azure Automation : au format JSON d’à l’aide de balises toocreate une planification pour le démarrage de la machine virtuelle Azure et d’arrêt](../automation/automation-scenario-start-stop-vm-wjson-tags.md).
- Pour les runbooks qui démarrent et arrêtent des machines virtuelles durant les heures creuses, consultez [Solution Start/Stop VMs during off-hours (Démarrer/arrêter des machines virtuelles durant les heures creuses) dans Automation](../automation/automation-solution-vm-management.md).

## <a name="next-steps"></a>Étapes suivantes
* toolearn sur la création de modèles du Gestionnaire de ressources, consultez [de création de modèles de gestionnaire de ressources Azure](resource-group-authoring-templates.md).
* toolearn sur le déploiement de modèles, consultez [déployer une application avec le modèle de gestionnaire de ressources Azure](resource-group-template-deploy.md).
* Vous pouvez déplacer existant ressources tooa nouveau groupe de ressources. Pour obtenir des exemples, consultez [tooNew de déplacement de ressources groupe de ressources ou d’un abonnement](resource-group-move-resources.md).
* Pour obtenir des conseils comment les entreprises peuvent utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise - gouvernance de l’abonnement normative](resource-manager-subscription-governance.md).

