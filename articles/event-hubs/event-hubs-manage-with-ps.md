---
title: "ressources d’Azure Event Hubs aaaUse PowerShell toomanage | Documents Microsoft"
description: "Utilisez PowerShell module toocreate et gérer les Hubs d’événements"
services: event-hubs
documentationcenter: .NET
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: d79cb307c2b4a031d059ce6ca67117ffc0b4600b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomanage-event-hubs-resources"></a>Utiliser les ressources de concentrateurs d’événements toomanage PowerShell

Microsoft Azure PowerShell est un environnement de script que vous pouvez utiliser toocontrol et automatiser le déploiement de hello et la gestion des services Azure. Cet article décrit comment toouse hello [module PowerShell de gestionnaire de ressources de concentrateurs événement](/powershell/module/azurerm.eventhub) tooprovision et de gérer les entités de concentrateurs d’événements (espaces de noms, les concentrateurs d’événements individuels et les groupes de consommateurs) à l’aide d’une console Azure PowerShell locale ou script.

Vous pouvez également gérer les ressources Event Hubs avec des modèles Azure Resource Manager. Pour plus d’informations, voir l’article hello [créer un espace de noms de concentrateurs d’événements avec le groupe d’événements concentrateur et le consommateur à l’aide d’un modèle Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub.md).

## <a name="prerequisites"></a>Composants requis

Avant de commencer, vous devez suivant de hello :

* Un abonnement Azure. Pour plus d’informations sur la façon de se procurer un abonnement, consultez les [options d’achat][purchase options], les [offres spéciales membres][member offers] ou découvrez comment créer un [compte gratuit][free account].
* Un ordinateur sur lequel est installé Azure PowerShell. Pour obtenir des instructions, consultez la page [Bien démarrer avec les applets de commande Azure PowerShell](/powershell/azure/get-started-azureps).
* Une compréhension générale de scripts PowerShell, les packages NuGet et hello .NET Framework.

## <a name="get-started"></a>Prise en main

première étape de Hello est toolog de PowerShell toouse dans tooyour compte Azure et d’abonnement Windows Azure. Suivez les instructions de hello dans [prise en main des applets de commande Azure PowerShell](/powershell/azure/get-started-azureps) toolog dans tooyour compte Azure, puis récupérer et accéder aux ressources hello dans votre abonnement Azure.

## <a name="provision-an-event-hubs-namespace"></a>Approvisionner un espace de noms Event Hubs

Lorsque vous travaillez avec des espaces de noms de concentrateurs d’événements, vous pouvez utiliser hello [Get-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace), [New-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace), [Remove-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace) , et [Set-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace) applets de commande.

Cet exemple crée quelques variables locales dans le script de hello ; `$Namespace` et `$Location`.

* `$Namespace`est le nom hello d’espace de noms de concentrateurs d’événements hello avec lequel nous souhaitons toowork.
* `$Location`identifie le centre de données hello dans lequel nous configurera hello espace de noms.
* `$CurrentNamespace`stocke l’espace de noms hello référence nous récupérer (ou créer).

Dans un script réel, les variables `$Namespace` et `$Location` peuvent être transmises en tant que paramètres.

Cette partie du script de hello hello suivant :

1. Tentatives tooretrieve concentrateurs d’événements d’un espace de noms avec hello spécifié de nom.
2. Si l’espace de noms hello est trouvé, il signale ce qui a été trouvé.
3. Si l’espace de noms hello n’est trouvé, il crée l’espace de noms hello, puis récupère hello nouvellement créé espace de noms.

    ```powershell
    # Query toosee if hello namespace currently exists
    $CurrentNamespace = Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
   
    # Check if hello namespace already exists or needs toobe created
    if ($CurrentNamespace)
    {
        Write-Host "hello namespace $Namespace already exists in hello $Location region:"
        # Report what was found
        Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "hello $Namespace namespace does not exist."
        Write-Host "Creating hello $Namespace namespace in hello $Location region..."
        New-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
        Write-Host "hello $Namespace namespace in Resource Group $ResGrpName in hello $Location region has been successfully created."
    }
    ```

## <a name="create-an-event-hub"></a>Création d'un concentrateur d'événements

toocreate un concentrateur d’événements, effectuer une vérification de l’espace de noms à l’aide du script de hello dans la section précédente de hello. Ensuite, utilisez hello [New-AzureRmEventHub](/powershell/module/azurerm.eventhub/new-azurermeventhub) concentrateur d’événements d’applet de commande toocreate hello :

```powershell
# Check if event hub already exists
$CurrentEH = Get-AzureRMEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName

if($CurrentEH)
{
    Write-Host "hello event hub $EventHubName already exists in hello $Location region:"
    # Report what was found
    Get-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
}
else
{
    Write-Host "hello $EventHubName event hub does not exist."
    Write-Host "Creating hello $EventHubName event hub in hello $Location region..."
    New-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -Location $Location -MessageRetentionInDays 3
    $CurrentEH = Get-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
    Write-Host "hello $EventHubName event hub in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

### <a name="create-a-consumer-group"></a>Créer un groupe de consommateurs

toocreate un groupe de consommateurs dans un concentrateur d’événements, vérification hello espace de noms et les événements concentrateur à l’aide de scripts de hello dans la section précédente de hello. Ensuite, utilisez hello [New-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) groupe de consommateurs toocreate hello applet de commande dans le concentrateur d’événements hello. Par exemple :

```powershell
# Check if consumer group already exists
$CurrentCG = Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -ErrorAction Ignore

if($CurrentCG)
{
    Write-Host "hello consumer group $ConsumerGroupName in event hub $EventHubName already exists in hello $Location region:"
    # Report what was found
    Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
}
else
{
    Write-Host "hello $ConsumerGroupName consumer group does not exist."
    Write-Host "Creating hello $ConsumerGroupName consumer group in hello $Location region..."
    New-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
    $CurrentCG = Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
    Write-Host "hello $ConsumerGroupName consumer group in event hub $EventHubName in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

#### <a name="set-user-metadata"></a>Définir les métadonnées utilisateur

Après l’exécution de scripts de hello Bonjour sections précédentes, vous pouvez utiliser hello [Set-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) propriétés de hello tooupdate applet de commande d’un groupe de consommateurs, comme dans hello l’exemple suivant :

```powershell
# Set some user metadata on hello CG
Write-Host "Setting hello UserMetadata field too'Testing'"
Set-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -UserMetadata "Testing"
# Show result
Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
```

## <a name="remove-event-hub"></a>Supprimer un concentrateur d’événements

concentrateurs d’événements hello tooremove vous avez créé, vous pouvez utiliser hello `Remove-*` applets de commande, comme dans hello l’exemple suivant :

```powershell
# Clean up
Remove-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
Remove-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
Remove-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
```

## <a name="next-steps"></a>Étapes suivantes

- Consultez la documentation du module hello complète événement concentrateurs Resource Manager PowerShell [ici](/powershell/module/azurerm.eventhub). Cette page liste toutes les applets de commande disponibles.
- Pour plus d’informations sur l’utilisation de modèles Azure Resource Manager, voir l’article hello [créer un espace de noms de concentrateurs d’événements avec le groupe d’événements concentrateur et le consommateur à l’aide d’un modèle Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub.md).
- Informations sur les [bibliothèques de gestion .NET Event Hubs](event-hubs-management-libraries.md).

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
