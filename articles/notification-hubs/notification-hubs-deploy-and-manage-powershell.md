---
title: "aaaDeploy et gérer des concentrateurs de Notification à l’aide de PowerShell"
description: "Comment tooCreate et gérer de Notification Hubs à l’aide de PowerShell pour l’automatisation"
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 7c58f2c8-0399-42bc-9e1e-a7f073426451
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: powershell
ms.devlang: na
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 8835bdefa0d360354263eab8040259ad08281771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-notification-hubs-using-powershell"></a>Déploiement et gestion des concentrateurs de notification à l'aide de PowerShell
## <a name="overview"></a>Vue d'ensemble
Cet article vous explique comment toouse créer et gérer Azure Notification Hubs à l’aide de PowerShell. Hello suivant des tâches d’automatisation courantes est présenté dans cette rubrique.

* Création d’un concentrateur de notification
* Définition des informations d’identification

Si vous devez également toocreate un nouvel espace de noms de service bus pour vos hubs de notification, consultez [gérer Service Bus avec PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md).

La gestion des concentrateurs de Notifications ne sont pas prise en charge directement par les applets de commande hello inclus avec Azure PowerShell. meilleure approche de Hello à partir de PowerShell est assembly de Microsoft.Azure.NotificationHubs.dll tooreference hello. assembly Hello est distribué avec hello [package NuGet de Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).

## <a name="prerequisites"></a>Composants requis
Avant de commencer cet article, vous devez disposer de hello :

* Un abonnement Azure. Azure est une plateforme disponible par abonnement. Pour plus d'informations sur l'obtention d'un abonnement, consultez les pages [Modes d’achat d’Azure], [Offres spéciales membres] ou [Version d'évaluation gratuite].
* Un ordinateur sur lequel est installé Azure PowerShell. Pour obtenir des instructions, consultez la rubrique [Installation et configuration d'Azure PowerShell].
* Une compréhension générale de scripts PowerShell, les packages NuGet et hello .NET Framework.

## <a name="including-a-reference-toohello-net-assembly-for-service-bus"></a>Y compris un assembly référence toohello .NET Service Bus
La gestion des concentrateurs de Notification Azure ne sont pas encore incluses avec hello applets de commande PowerShell dans Azure PowerShell. concentrateurs de notification tooprovision, vous pouvez utiliser hello .NET client fourni dans hello [package NuGet de Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).

Tout d’abord, assurez-vous que votre script peut localiser hello **Microsoft.Azure.NotificationHubs.dll** assembly, qui est installé en tant que package NuGet dans un projet Visual Studio. Dans l’ordre les toobe flexible, script de hello procède comme suit :

1. Détermine le chemin d’accès hello à laquelle il a été appelé.
2. Parcourt hello chemin d’accès jusqu'à ce qu’il trouve un dossier nommé `packages`. Ce dossier est créé lorsque vous installez les packages NuGet pour les projets Visual Studio.
3. De manière récursive les recherches hello `packages` dossier pour un assembly nommé **Microsoft.Azure.NotificationHubs.dll**.
4. Références hello assembly afin que les types de hello sont disponibles pour une utilisation ultérieure.

Voici comment ces étapes sont implémentées dans un script PowerShell :

``` powershell

try
{
    # WARNING: Make sure tooreference hello latest version of Microsoft.Azure.NotificationHubs.dll
    Write-Output "Adding hello [Microsoft.Azure.NotificationHubs.dll] assembly toohello script..."
    $scriptPath = Split-Path (Get-Variable MyInvocation -Scope 0).Value.MyCommand.Path
    $packagesFolder = (Split-Path $scriptPath -Parent) + "\packages"
    $assembly = Get-ChildItem $packagesFolder -Include "Microsoft.Azure.NotificationHubs.dll" -Recurse
    Add-Type -Path $assembly.FullName

    Write-Output "hello [Microsoft.Azure.NotificationHubs.dll] assembly has been successfully added toohello script."
}

catch [System.Exception]
{
    Write-Error("Could not add hello Microsoft.Azure.NotificationHubs.dll assembly toohello script. Make sure you build hello solution before running hello provisioning script.")
}
```

## <a name="create-hello-namespacemanager-class"></a>Créer la classe NamespaceManager de hello
tooprovision concentrateurs de Notification, créez une instance de hello [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) classe à partir de hello SDK. 

Vous pouvez utiliser hello [Get-AzureSBAuthorizationRule] applet de commande incluses avec Azure PowerShell tooretrieve une règle d’autorisation qui a utilisé tooprovide une chaîne de connexion. Nous allons stocker une référence toohello `NamespaceManager` instance Bonjour `$NamespaceManager` variable. Nous allons utiliser `$NamespaceManager` tooprovision un concentrateur de notification.

``` powershell
$sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
# Create hello NamespaceManager object toocreate hello hub
Write-Output "Creating a NamespaceManager object for hello [$Namespace] namespace..."
$NamespaceManager=[Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
Write-Output "NamespaceManager object for hello [$Namespace] namespace has been successfully created."
```


## <a name="provisioning-a-new-notification-hub"></a>Configuration d’un nouveau concentrateur de notification
tooprovision un hub de notification, utilisez hello [API .NET pour les concentrateurs de Notification].

Dans cette partie du script de hello configurer quatre variables locales. 

1. `$Namespace`: Définissez ce toohello nom de l’espace de noms hello où vous souhaitez toocreate un concentrateur de notification.
2. `$Path`: Définissez ce nom toohello de chemin d’accès du nouveau concentrateur de notification hello.  Par exemple, « MonConcentrateur ».    
3. `$WnsPackageSid`: Définissez ce SID du package toohello vous application Windows à partir de hello [centre de développement Windows](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).
4. `$WnsSecretkey`: Définissez cette clé secrète toohello vous application Windows à partir de hello [centre de développement Windows](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).

Ces variables sont l’espace de noms utilisé tooconnect tooyour et créer un nouveau toohandle de Hub de Notification configuré des notifications de Services de Notification de Windows (WNS) avec les informations d’identification WNS pour une application Windows. Pour plus d’informations sur l’obtention de hello SID et package, consultez clé secrète hello [mise en route avec Notification Hubs](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) didacticiel. 

* extrait de code de script Hello utilise hello `NamespaceManager` si hello Hub de Notification est identifiée par l’objet toocheck toosee `$Path` existe.
* Si elle n’existe pas, hello script crée un `NotificationHubDescription` avec WNS informations d’identification et passer ce toohello `NamespaceManager` classe `CreateNotificationHub` (méthode).

``` powershell

$Namespace = "<Enter your namespace>"
$Path  = "<Enter a name for your notification hub>"
$WnsPackageSid = "<your package sid>"
$WnsSecretkey = "<enter your secret key>"

$WnsCredential = New-Object -TypeName Microsoft.Azure.NotificationHubs.WnsCredential -ArgumentList $WnsPackageSid,$WnsSecretkey

# Query hello namespace
$CurrentNamespace = Get-AzureSBNamespace -Name $Namespace

# Check if hello namespace already exists
if ($CurrentNamespace)
{
    Write-Output "hello namespace [$Namespace] in hello [$($CurrentNamespace.Region)] region was found."

    # Create hello NamespaceManager object used toocreate a new notification hub
    $sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
    Write-Output "Creating a NamespaceManager object for hello [$Namespace] namespace..."
    $NamespaceManager = [Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
    Write-Output "NamespaceManager object for hello [$Namespace] namespace has been successfully created."

    # Check toosee if hello Notification Hub already exists
    if ($NamespaceManager.NotificationHubExists($Path))
    {
        Write-Output "hello [$Path] notification hub already exists in hello [$Namespace] namespace."  
    }
    else
    {
        Write-Output "Creating hello [$Path] notification hub in hello [$Namespace] namespace."
        $NHDescription = New-Object -TypeName Microsoft.Azure.NotificationHubs.NotificationHubDescription -ArgumentList $Path;
        $NHDescription.WnsCredential = $WnsCredential;
        $NamespaceManager.CreateNotificationHub($NHDescription);
        Write-Output "hello [$Path] notification hub was created in hello [$Namespace] namespace."
    }
}
else
{
    Write-Host "hello [$Namespace] namespace does not exist."
}
```




## <a name="additional-resources"></a>Ressources supplémentaires
* [Gestion de Service Bus avec PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md)
* [Comment toocreate Service Bus files d’attente, rubriques et abonnements à l’aide d’un script PowerShell](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [Comment toocreate un Service Bus Namespace et qu’un concentrateur d’événements à l’aide d’un script PowerShell](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)

Vous pouvez également télécharger des scripts prêts à l’emploi :

* [Scripts PowerShell pour Service Bus](https://code.msdn.microsoft.com/windowsazure/Service-Bus-PowerShell-a46b7059)

[Modes d’achat d’Azure]: http://azure.microsoft.com/pricing/purchase-options/
[Offres spéciales membres]: http://azure.microsoft.com/pricing/member-offers/
[Version d'évaluation gratuite]: http://azure.microsoft.com/pricing/free-trial/
[Installation et configuration d'Azure PowerShell]: /powershell/azureps-cmdlets-docs
[API .NET pour les concentrateurs de Notification]: https://msdn.microsoft.com/library/azure/mt414893.aspx
[Get-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495122.aspx
[New-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495165.aspx
[Get-AzureSBAuthorizationRule]: https://msdn.microsoft.com/library/azure/dn495113.aspx

