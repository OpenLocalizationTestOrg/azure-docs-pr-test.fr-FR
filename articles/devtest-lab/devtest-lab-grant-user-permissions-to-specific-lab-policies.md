---
title: "stratégies de laboratoire aaaGrant utilisateur autorisations toospecific | Documents Microsoft"
description: "Découvrez comment les stratégies toogrant utilisateur autorisations toospecific lab dans DevTest Labs en fonction des besoins de chaque utilisateur"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 5ca829f0-eb69-40a1-ae26-03a629db1d7e
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: 35647ab837243188f06566cdf365b67fe33a3865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="grant-user-permissions-toospecific-lab-policies"></a>Accorder des autorisations utilisateur toospecific des stratégies de laboratoire
## <a name="overview"></a>Vue d'ensemble
Cet article explique comment toouse stratégie de PowerShell toogrant utilisateurs autorisations tooa lab particulier. De cette façon, les autorisations peuvent être appliquées selon les besoins de chaque utilisateur. Par exemple, vous pourriez toogrant un paramètre de stratégie utilisateur particulier hello hello capacité toochange machine virtuelle, mais pas hello coût des stratégies.

## <a name="policies-as-resources"></a>Stratégies en tant que ressources
Comme indiqué dans hello [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md) article, RBAC permet la gestion accès affiné des ressources Azure. À l’aide de RBAC, vous pouvez séparer les droits au sein de votre équipe DevOps et accorder uniquement hello quantité toousers d’accès dont ils ont besoin tooperform leur travail.

Dans DevTest Labs, une stratégie est un type de ressource qui permet l’action de RBAC hello **Microsoft.DevTestLab/labs/policySets/policies/**. Chaque stratégie lab est une ressource de type de ressource de stratégie de hello et peut être affecté comme un rôle RBAC tooan étendue.

Par exemple, dans l’ordre toogrant les utilisateurs en lecture/écriture autorisation toohello **autorisé des tailles de machine virtuelle** stratégie, vous devez créer un rôle personnalisé qui fonctionne avec hello **Microsoft.DevTestLab/labs/policySets/policies/** * action et puis affecter hello utilisateurs appropriés toothis personnalisé rôle dans la portée de hello de **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.

toolearn savoir plus sur les rôles personnalisés dans RBAC, consultez hello [rôles de personnaliser le contrôle d’accès](../active-directory/role-based-access-control-custom-roles.md).

## <a name="creating-a-lab-custom-role-using-powershell"></a>Création d’un rôle personnalisé de laboratoire en utilisant PowerShell
Tooget commande a démarré, vous devez hello tooread suivant l’article, qui explique comment tooinstall et configurer les applets de commande PowerShell Azure hello : [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).

Une fois que vous avez configuré hello applets de commande PowerShell de Azure, vous pouvez effectuer hello tâches suivantes :

* Liste de toutes les opérations de hello/actions pour un fournisseur de ressources
* Répertorier les actions d’un rôle particulier :
* Créer un rôle personnalisé

Hello PowerShell script suivant illustre des exemples de tooperform ces tâches :

    ‘List all hello operations/actions for a resource provider.
    Get-AzureRmProviderOperation -OperationSearchString "Microsoft.DevTestLab/*"

    ‘List actions in a particular role.
    (Get-AzureRmRoleDefinition "DevTest Labs User").Actions

    ‘Create custom role.
    $policyRoleDef = (Get-AzureRmRoleDefinition "DevTest Labs User")
    $policyRoleDef.Id = $null
    $policyRoleDef.Name = "Policy Contributor"
    $policyRoleDef.IsCustom = $true
    $policyRoleDef.AssignableScopes.Clear()
    $policyRoleDef.AssignableScopes.Add("/subscriptions/<SubscriptionID> ")
    $policyRoleDef.Actions.Add("Microsoft.DevTestLab/labs/policySets/policies/*")
    $policyRoleDef = (New-AzureRmRoleDefinition -Role $policyRoleDef)

## <a name="assigning-permissions-tooa-user-for-a-specific-policy-using-custom-roles"></a>Affectation d’autorisations tooa utilisateur pour une stratégie spécifique à l’aide de rôles personnalisés
Une fois que vous avez défini vos rôles personnalisés, vous pouvez les affecter toousers. Dans l’ordre tooassign un utilisateur tooa de rôle personnalisé, vous devez d’abord obtenir hello **ObjectId** représentant cet utilisateur. toodo qui, utilisez hello **Get-AzureRmADUser** applet de commande.

Dans l’exemple suivant de hello, hello **ObjectId** Hello *SomeUser* utilisateur est 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3.

    PS C:\>Get-AzureRmADUser -SearchString "SomeUser"

    DisplayName                    Type                           ObjectId
    -----------                    ----                           --------
    someuser@hotmail.com                                          05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3

Une fois que vous avez hello **ObjectId** pour l’utilisateur de hello et un nom de rôle personnalisé, vous pouvez l’affecter rôle toohello avec hello **New-AzureRmRoleAssignment** applet de commande :

    PS C:\>New-AzureRmRoleAssignment -ObjectId 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 -RoleDefinitionName "Policy Contributor" -Scope /subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroupName>/providers/Microsoft.DevTestLab/labs/<LabName>/policySets/policies/AllowedVmSizesInLab

Dans l’exemple précédent de hello, hello **AllowedVmSizesInLab** stratégie est utilisée. Vous pouvez utiliser un des hello les stratégies suivantes :

* MaxVmsAllowedPerUser
* MaxVmsAllowedPerLab
* AllowedVmSizesInLab
* LabVmsShutdown

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Étapes suivantes
Une fois vous avez accordé des stratégies de laboratoire autorisations toospecific utilisateur, Voici certains tooconsider étapes suivant :

* [Laboratoire tooa de sécuriser l’accès](devtest-lab-add-devtest-user.md).
* [Définir des stratégies de laboratoire](devtest-lab-set-lab-policy.md).
* [Créer un modèle de laboratoire](devtest-lab-create-template.md).
* [Créer des artefacts personnalisés pour vos machines virtuelles](devtest-lab-artifact-author.md).
* [Ajouter une machine virtuelle avec lab de tooa artefacts](devtest-lab-add-vm-with-artifacts.md).

