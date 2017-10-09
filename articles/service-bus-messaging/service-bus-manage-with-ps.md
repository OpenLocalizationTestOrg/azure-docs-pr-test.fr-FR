---
title: "ressources d’Azure Service Bus aaaUse PowerShell toomanage | Documents Microsoft"
description: "Utilisez PowerShell module toocreate et gérer les ressources de Service Bus"
services: service-bus-messaging
documentationcenter: .NET
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/06/2017
ms.author: sethm
ms.openlocfilehash: 737044def913c5798e7e05fc4f1aeece76c8f4dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomanage-service-bus-resources"></a>Utiliser les ressources de Service Bus PowerShell toomanage

Microsoft Azure PowerShell est un environnement de script que vous pouvez utiliser toocontrol et automatiser le déploiement de hello et la gestion des services Azure. Cet article décrit comment toouse hello [module PowerShell de gestionnaire de ressources du Service Bus](/powershell/module/azurerm.servicebus) tooprovision et gérer des entités Service Bus (espaces de noms, les files d’attente, rubriques et abonnements) à l’aide d’une console Azure PowerShell locale ou script.

Vous pouvez également gérer les entités Service Bus à l’aide de modèles Azure Resource Manager. Pour plus d’informations, voir l’article hello [ressources créez Service Bus à l’aide de modèles Azure Resource Manager](service-bus-resource-manager-overview.md).

## <a name="prerequisites"></a>Composants requis

Avant de commencer, vous devez suivant de hello :

* Un abonnement Azure. Pour plus d’informations sur la façon de se procurer un abonnement, consultez les [options d’achat][purchase options], les [offres spéciales membres][member offers] ou découvrez comment créer un [compte gratuit][free account].
* Un ordinateur sur lequel est installé Azure PowerShell. Pour obtenir des instructions, consultez la page [Bien démarrer avec les applets de commande Azure PowerShell](/powershell/azure/get-started-azureps).
* Une compréhension générale de scripts PowerShell, les packages NuGet et hello .NET Framework.

## <a name="get-started"></a>Prise en main

première étape de Hello est toolog de PowerShell toouse dans tooyour compte Azure et d’abonnement Windows Azure. Suivez les instructions de hello dans [prise en main des applets de commande Azure PowerShell](/powershell/azure/get-started-azureps) toolog dans tooyour compte Azure et de récupérer et accès aux ressources de hello dans votre abonnement Azure.

## <a name="provision-a-service-bus-namespace"></a>Approvisionner un espace de noms Service Bus

Lorsque vous travaillez avec des espaces de noms Service Bus, vous pouvez utiliser hello [Get-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [New-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace), et [Set-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) applets de commande.

Cet exemple crée quelques variables locales dans le script de hello ; `$Namespace` et `$Location`.

* `$Namespace`est le nom hello d’espace de noms Service Bus hello avec lequel nous souhaitons toowork.
* `$Location`identifie le centre de données hello dans lequel nous configurera hello espace de noms.
* `$CurrentNamespace`stocke l’espace de noms hello référence nous récupérer (ou créer).

Dans un script réel, les variables `$Namespace` et `$Location` peuvent être transmises en tant que paramètres.

Cette partie du script de hello hello suivant :

1. Nom spécifié par les tentatives tooretrieve un espace de noms Service Bus avec hello.
2. Si l’espace de noms hello est trouvé, il signale ce qui a été trouvé.
3. Si l’espace de noms hello n’est trouvé, il crée l’espace de noms hello, puis récupère hello nouvellement créé espace de noms.
   
    ``` powershell
    # Query toosee if hello namespace currently exists
    $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
   
    # Check if hello namespace already exists or needs toobe created
    if ($CurrentNamespace)
    {
        Write-Host "hello namespace $Namespace already exists in hello $Location region:"
        # Report what was found
        Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "hello $Namespace namespace does not exist."
        Write-Host "Creating hello $Namespace namespace in hello $Location region..."
        New-AzureRmServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
        Write-Host "hello $Namespace namespace in Resource Group $ResGrpName in hello $Location region has been successfully created."
                
    }
    ```

### <a name="create-a-namespace-authorization-rule"></a>Créer une règle d’autorisation d’espace de noms

Hello suivant montre comment les règles d’autorisation de toomanage espace de noms à l’aide de hello [New-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [Set-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule), et [applets de commande Remove-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule).

```powershell
# Query toosee if rule exists
$CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

# Check if hello rule already exists or needs toobe created
if ($CurrentRule)
{
    Write-Host "hello $AuthRule rule already exists for hello namespace $Namespace."
}
else
{
    Write-Host "hello $AuthRule rule does not exist."
    Write-Host "Creating hello $AuthRule rule for hello $Namespace namespace..."
    New-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule -Rights @("Listen","Send")
    $CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
    Write-Host "hello $AuthRule rule for hello $Namespace namespace has been successfully created."

    Write-Host "Setting rights on hello namespace"
    $authRuleObj = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

    Write-Host "Remove Send rights"
    $authRuleObj.Rights.Remove("Send")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj

    Write-Host "Add Send and Manage rights toohello namespace"
    $authRuleObj.Rights.Add("Send")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj
    $authRuleObj.Rights.Add("Manage")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj

    Write-Host "Show value of primary key"
    $CurrentKey = Get-AzureRmServiceBusNamespaceKey -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
        
    Write-Host "Remove this authorization rule"
    Remove-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
}
```

## <a name="create-a-queue"></a>Création d’une file d’attente

toocreate une file d’attente ou rubrique, effectuer une vérification de l’espace de noms à l’aide du script de hello dans la section précédente de hello. Ensuite, créez la file d’attente de hello :

```powershell
# Check if queue already exists
$CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName

if($CurrentQ)
{
    Write-Host "hello queue $QueueName already exists in hello $Location region:"
}
else
{
    Write-Host "hello $QueueName queue does not exist."
    Write-Host "Creating hello $QueueName queue in hello $Location region..."
    New-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -EnablePartitioning $True
    $CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName
    Write-Host "hello $QueueName queue in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

### <a name="modify-queue-properties"></a>Modifier les propriétés de la file d’attente

Après avoir exécuté le script de hello Bonjour précédant la section, vous pouvez utiliser hello [Set-AzureRmServiceBusQueue](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) propriétés de hello tooupdate applet de commande d’une file d’attente, comme dans hello l’exemple suivant :

```powershell
$CurrentQ.DeadLetteringOnMessageExpiration = $True
$CurrentQ.MaxDeliveryCount = 7
$CurrentQ.MaxSizeInMegabytes = 2048
$CurrentQ.EnableExpress = $True

Set-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -QueueObj $CurrentQ
```

## <a name="provisioning-other-service-bus-entities"></a>Approvisionne d'autres entités Service Bus

Vous pouvez utiliser hello [module PowerShell de Service Bus](/powershell/module/azurerm.servicebus) tooprovision autres entités, telles que des rubriques et abonnements. Ces applets de commande sont syntaxiquement similaire cmdlets de création de file d’attente toohello illustrée dans la section précédente de hello.

## <a name="next-steps"></a>Étapes suivantes

- Consultez la documentation de module Gestionnaire de ressources du Service Bus PowerShell complète hello [ici](/powershell/module/azurerm.servicebus). Cette page liste toutes les applets de commande disponibles.
- Pour plus d’informations sur l’utilisation de modèles Azure Resource Manager, voir l’article hello [ressources créez Service Bus à l’aide de modèles Azure Resource Manager](service-bus-resource-manager-overview.md).
- Informations sur les [bibliothèques de gestion Service Bus .NET](service-bus-management-libraries.md).

Voici quelques-unes des autres toomanage des entités Service Bus, comme décrit dans ces billets de blog :

* [Comment toocreate Service Bus files d’attente, rubriques et abonnements à l’aide d’un script PowerShell](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [Comment toocreate un Service Bus Namespace et qu’un concentrateur d’événements à l’aide d’un script PowerShell](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)
* [Scripts PowerShell pour Service Bus](https://code.msdn.microsoft.com/Service-Bus-PowerShell-a46b7059)

<!--Anchors-->

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
