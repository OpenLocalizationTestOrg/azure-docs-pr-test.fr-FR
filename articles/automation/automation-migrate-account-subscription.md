---
title: aaaMigrate compte Automation et ressources | Documents Microsoft
description: "Cet article décrit comment toomove une automatisation de compte dans Azure Automation et les ressources associées à partir d’un seul abonnement tooanother."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9c2db4a2-f324-48dc-8ce7-3343bf7230d5
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/21/2016
ms.author: magoedte
ms.openlocfilehash: 201c9091cd2d78d7ea407c1e5fb27f366bb4fa8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-automation-account-and-resources"></a>Migration d’un compte et de ressources Automation
Pour les comptes Automation et les ressources associées (c'est-à-dire actifs, runbooks, modules, etc.) que vous avez créé dans hello portail Azure et souhaitez toomigrate à partir d’une ressource de groupe tooanother ou à partir d’un seul abonnement tooanother, vous pouvez faire cela facilement avec Hello [déplacer des ressources](../azure-resource-manager/resource-group-move-resources.md) fonctionnalité disponible dans hello portail Azure. Toutefois, avant de procéder à cette action, vous devez tout d’abord examiner suivant de hello [liste de vérification avant le déplacement de ressources](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) et en outre, hello liste ci-dessous tooAutomation spécifique.   

1. groupe de ressource d’abonnement de destination Hello doit être dans la même région que la source de hello.  Cela signifie que les comptes Automation ne peuvent pas être déplacés entre des régions.
2. Lors du déplacement des ressources (par exemple, les procédures opérationnelles, travaux, etc.), les groupes de source de hello et hello cible sont verrouillées pendant l’opération de hello hello. Écriture et suppression des opérations sont bloquées sur les groupes de hello jusqu'à ce que le déplacement de hello se termine.  
3. Les runbooks et les variables qui font référence à un ID de ressource ou d’un abonnement à partir de l’abonnement existant de hello devez toobe mis à jour après que la migration est terminée.   

> [!NOTE]
> Cette fonctionnalité ne prend pas en charge les ressources Automation classiques.
>
>

## <a name="toomove-hello-automation-account-using-hello-portal"></a>toomove hello compte Automation à l’aide du portail de hello
1. À partir de votre compte Automation, cliquez sur **déplacer** haut hello du Panneau de hello.<br> ![option Déplacer](media/automation-migrate-account-subscription/automation-menu-move.png)<br>
2. Sur hello **déplacer des ressources** panneau, notez qu’il présente tooboth connexes des ressources de votre compte Automation et vos groupes de ressources.  Sélectionnez hello **abonnement** et **groupe de ressources** à partir des listes déroulantes de hello ou sélectionnez hello option **créer un groupe de ressources** et entrez un nouveau nom de groupe de ressources dans champ Hello fourni.  
3. Passez en revue et sélectionnez hello case à cocher tooacknowledge vous *comprendre les outils et scripts sera nécessaire toobe mis à jour toouse nouveaux ID de ressource après le déplacement de ressources* puis cliquez sur **OK**.<br> ![panneau Déplacer des ressources](media/automation-migrate-account-subscription/automation-move-resources-blade.png)<br>   

Cette action prendra plusieurs minutes toocomplete.  Le panneau **Notifications**affiche l’état de chaque action effectuée : validation, migration, puis confirmation que l’opération est terminée.     

## <a name="toomove-hello-automation-account-using-powershell"></a>toomove hello compte Automation à l’aide de PowerShell
toomove existant abonnement, utilisez hello ou groupe de ressources Automation ressources tooanother **Get-AzureRmResource** compte Automation spécifique d’applet de commande tooget hello, puis **Move-AzureRmResource** déplacement de l’applet de commande tooperform hello.

Hello premier exemple montre comment toomove une automatisation compte tooa nouveau groupe de ressources.

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup"
   ```

Après avoir exécuté hello, exemple de code ci-dessus, vous serez invité à tooverify vous voulez que tooperform cette action.  Une fois que vous cliquez sur **Oui** et autoriser hello tooproceed de script, vous ne recevrez pas de notifications pendant qu’il effectue la migration hello.  

toomove tooa nouvel abonnement, incluez une valeur pour hello *DestinationSubscriptionId* paramètre.

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup" -DestinationSubscriptionId "SubscriptionId"
   ```

Comme avec l’exemple précédent de hello, vous serez invité à tooconfirm hello move.  

## <a name="next-steps"></a>Étapes suivantes
* Pour plus d’informations sur le groupe de ressources toonew ressources mobile ou d’un abonnement, consultez [déplacer le groupe de ressources toonew ressources ou d’un abonnement](../azure-resource-manager/resource-group-move-resources.md)
* Pour plus d’informations sur le contrôle d’accès basée sur les rôles dans Azure Automation, consultez trop[contrôle d’accès basé sur un rôle dans Azure Automation](automation-role-based-access-control.md).
* toolearn sur les applets de commande PowerShell pour gérer votre abonnement, consultez [à l’aide de Azure PowerShell avec le Gestionnaire de ressources](../azure-resource-manager/powershell-azure-resource-manager.md)
* toolearn sur les fonctionnalités du portail de gestion de votre abonnement, consultez [à l’aide des ressources de toomanage portail Azure hello](../azure-resource-manager/resource-group-portal.md).
