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
# <a name="deploy-and-manage-notification-hubs-using-powershell"></a><span data-ttu-id="f17ad-103">Déploiement et gestion des concentrateurs de notification à l'aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="f17ad-103">Deploy and Manage Notification Hubs using PowerShell</span></span>
## <a name="overview"></a><span data-ttu-id="f17ad-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="f17ad-104">Overview</span></span>
<span data-ttu-id="f17ad-105">Cet article vous explique comment toouse créer et gérer Azure Notification Hubs à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f17ad-105">This article shows you how toouse Create and Manage Azure Notification Hubs using PowerShell.</span></span> <span data-ttu-id="f17ad-106">Hello suivant des tâches d’automatisation courantes est présenté dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="f17ad-106">hello following common automation tasks are shown in this topic.</span></span>

* <span data-ttu-id="f17ad-107">Création d’un concentrateur de notification</span><span class="sxs-lookup"><span data-stu-id="f17ad-107">Create a Notification Hub</span></span>
* <span data-ttu-id="f17ad-108">Définition des informations d’identification</span><span class="sxs-lookup"><span data-stu-id="f17ad-108">Set Credentials</span></span>

<span data-ttu-id="f17ad-109">Si vous devez également toocreate un nouvel espace de noms de service bus pour vos hubs de notification, consultez [gérer Service Bus avec PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md).</span><span class="sxs-lookup"><span data-stu-id="f17ad-109">If you also need toocreate a new service bus namespace for your notification hubs, see [Manage Service Bus with PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md).</span></span>

<span data-ttu-id="f17ad-110">La gestion des concentrateurs de Notifications ne sont pas prise en charge directement par les applets de commande hello inclus avec Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f17ad-110">Managing Notifications Hubs is not supported directly by hello cmdlets included with Azure PowerShell.</span></span> <span data-ttu-id="f17ad-111">meilleure approche de Hello à partir de PowerShell est assembly de Microsoft.Azure.NotificationHubs.dll tooreference hello.</span><span class="sxs-lookup"><span data-stu-id="f17ad-111">hello best approach from PowerShell is tooreference hello Microsoft.Azure.NotificationHubs.dll assembly.</span></span> <span data-ttu-id="f17ad-112">assembly Hello est distribué avec hello [package NuGet de Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="f17ad-112">hello assembly is distributed with hello [Microsoft Azure Notification Hubs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f17ad-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f17ad-113">Prerequisites</span></span>
<span data-ttu-id="f17ad-114">Avant de commencer cet article, vous devez disposer de hello :</span><span class="sxs-lookup"><span data-stu-id="f17ad-114">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="f17ad-115">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="f17ad-115">An Azure subscription.</span></span> <span data-ttu-id="f17ad-116">Azure est une plateforme disponible par abonnement.</span><span class="sxs-lookup"><span data-stu-id="f17ad-116">Azure is a subscription-based platform.</span></span> <span data-ttu-id="f17ad-117">Pour plus d'informations sur l'obtention d'un abonnement, consultez les pages [Modes d’achat d’Azure], [Offres spéciales membres] ou [Version d'évaluation gratuite].</span><span class="sxs-lookup"><span data-stu-id="f17ad-117">For more information about obtaining a subscription, see [Purchase Options], [Member Offers], or [Free Trial].</span></span>
* <span data-ttu-id="f17ad-118">Un ordinateur sur lequel est installé Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f17ad-118">A computer with Azure PowerShell.</span></span> <span data-ttu-id="f17ad-119">Pour obtenir des instructions, consultez la rubrique [Installation et configuration d'Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="f17ad-119">For instructions, see [Install and configure Azure PowerShell].</span></span>
* <span data-ttu-id="f17ad-120">Une compréhension générale de scripts PowerShell, les packages NuGet et hello .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="f17ad-120">A general understanding of PowerShell scripts, NuGet packages, and hello .NET Framework.</span></span>

## <a name="including-a-reference-toohello-net-assembly-for-service-bus"></a><span data-ttu-id="f17ad-121">Y compris un assembly référence toohello .NET Service Bus</span><span class="sxs-lookup"><span data-stu-id="f17ad-121">Including a reference toohello .NET assembly for Service Bus</span></span>
<span data-ttu-id="f17ad-122">La gestion des concentrateurs de Notification Azure ne sont pas encore incluses avec hello applets de commande PowerShell dans Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f17ad-122">Managing Azure Notification Hubs is not yet included with hello PowerShell cmdlets in Azure PowerShell.</span></span> <span data-ttu-id="f17ad-123">concentrateurs de notification tooprovision, vous pouvez utiliser hello .NET client fourni dans hello [package NuGet de Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="f17ad-123">tooprovision notification hubs, you can use hello .NET client provided in hello [Microsoft Azure Notification Hubs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="f17ad-124">Tout d’abord, assurez-vous que votre script peut localiser hello **Microsoft.Azure.NotificationHubs.dll** assembly, qui est installé en tant que package NuGet dans un projet Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f17ad-124">First, make sure your script can locate hello **Microsoft.Azure.NotificationHubs.dll** assembly, which is installed as a NuGet package in a Visual Studio project.</span></span> <span data-ttu-id="f17ad-125">Dans l’ordre les toobe flexible, script de hello procède comme suit :</span><span class="sxs-lookup"><span data-stu-id="f17ad-125">In order toobe flexible, hello script performs these steps:</span></span>

1. <span data-ttu-id="f17ad-126">Détermine le chemin d’accès hello à laquelle il a été appelé.</span><span class="sxs-lookup"><span data-stu-id="f17ad-126">Determines hello path at which it was invoked.</span></span>
2. <span data-ttu-id="f17ad-127">Parcourt hello chemin d’accès jusqu'à ce qu’il trouve un dossier nommé `packages`.</span><span class="sxs-lookup"><span data-stu-id="f17ad-127">Traverses hello path until it finds a folder named `packages`.</span></span> <span data-ttu-id="f17ad-128">Ce dossier est créé lorsque vous installez les packages NuGet pour les projets Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f17ad-128">This folder is created when you install NuGet packages for Visual Studio projects.</span></span>
3. <span data-ttu-id="f17ad-129">De manière récursive les recherches hello `packages` dossier pour un assembly nommé **Microsoft.Azure.NotificationHubs.dll**.</span><span class="sxs-lookup"><span data-stu-id="f17ad-129">Recursively searches hello `packages` folder for an assembly named **Microsoft.Azure.NotificationHubs.dll**.</span></span>
4. <span data-ttu-id="f17ad-130">Références hello assembly afin que les types de hello sont disponibles pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="f17ad-130">References hello assembly so that hello types are available for later use.</span></span>

<span data-ttu-id="f17ad-131">Voici comment ces étapes sont implémentées dans un script PowerShell :</span><span class="sxs-lookup"><span data-stu-id="f17ad-131">Here's how these steps are implemented in a PowerShell script:</span></span>

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

## <a name="create-hello-namespacemanager-class"></a><span data-ttu-id="f17ad-132">Créer la classe NamespaceManager de hello</span><span class="sxs-lookup"><span data-stu-id="f17ad-132">Create hello NamespaceManager class</span></span>
<span data-ttu-id="f17ad-133">tooprovision concentrateurs de Notification, créez une instance de hello [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) classe à partir de hello SDK.</span><span class="sxs-lookup"><span data-stu-id="f17ad-133">tooprovision Notification Hubs, create an instance of hello [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) class from hello SDK.</span></span> 

<span data-ttu-id="f17ad-134">Vous pouvez utiliser hello [Get-AzureSBAuthorizationRule] applet de commande incluses avec Azure PowerShell tooretrieve une règle d’autorisation qui a utilisé tooprovide une chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="f17ad-134">You can use hello [Get-AzureSBAuthorizationRule] cmdlet included with Azure PowerShell tooretrieve an authorization rule that's used tooprovide a connection string.</span></span> <span data-ttu-id="f17ad-135">Nous allons stocker une référence toohello `NamespaceManager` instance Bonjour `$NamespaceManager` variable.</span><span class="sxs-lookup"><span data-stu-id="f17ad-135">We'll store a reference toohello `NamespaceManager` instance in hello `$NamespaceManager` variable.</span></span> <span data-ttu-id="f17ad-136">Nous allons utiliser `$NamespaceManager` tooprovision un concentrateur de notification.</span><span class="sxs-lookup"><span data-stu-id="f17ad-136">We will use `$NamespaceManager` tooprovision a notification hub.</span></span>

``` powershell
$sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
# Create hello NamespaceManager object toocreate hello hub
Write-Output "Creating a NamespaceManager object for hello [$Namespace] namespace..."
$NamespaceManager=[Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
Write-Output "NamespaceManager object for hello [$Namespace] namespace has been successfully created."
```


## <a name="provisioning-a-new-notification-hub"></a><span data-ttu-id="f17ad-137">Configuration d’un nouveau concentrateur de notification</span><span class="sxs-lookup"><span data-stu-id="f17ad-137">Provisioning a new Notification Hub</span></span>
<span data-ttu-id="f17ad-138">tooprovision un hub de notification, utilisez hello [API .NET pour les concentrateurs de Notification].</span><span class="sxs-lookup"><span data-stu-id="f17ad-138">tooprovision a new notification hub, use hello [.NET API for Notification Hubs].</span></span>

<span data-ttu-id="f17ad-139">Dans cette partie du script de hello configurer quatre variables locales.</span><span class="sxs-lookup"><span data-stu-id="f17ad-139">In this part of hello script you set up four local variables.</span></span> 

1. <span data-ttu-id="f17ad-140">`$Namespace`: Définissez ce toohello nom de l’espace de noms hello où vous souhaitez toocreate un concentrateur de notification.</span><span class="sxs-lookup"><span data-stu-id="f17ad-140">`$Namespace` : Set this toohello name of hello namespace where you want toocreate a notification hub.</span></span>
2. <span data-ttu-id="f17ad-141">`$Path`: Définissez ce nom toohello de chemin d’accès du nouveau concentrateur de notification hello.</span><span class="sxs-lookup"><span data-stu-id="f17ad-141">`$Path` : Set this path toohello name of hello new notification hub.</span></span>  <span data-ttu-id="f17ad-142">Par exemple, « MonConcentrateur ».</span><span class="sxs-lookup"><span data-stu-id="f17ad-142">For example, "MyHub".</span></span>    
3. <span data-ttu-id="f17ad-143">`$WnsPackageSid`: Définissez ce SID du package toohello vous application Windows à partir de hello [centre de développement Windows](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="f17ad-143">`$WnsPackageSid` : Set this toohello package SID for you Windows App from hello [Windows Dev Center](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span></span>
4. <span data-ttu-id="f17ad-144">`$WnsSecretkey`: Définissez cette clé secrète toohello vous application Windows à partir de hello [centre de développement Windows](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="f17ad-144">`$WnsSecretkey`: Set this toohello secret key for you Windows App from hello [Windows Dev Center](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span></span>

<span data-ttu-id="f17ad-145">Ces variables sont l’espace de noms utilisé tooconnect tooyour et créer un nouveau toohandle de Hub de Notification configuré des notifications de Services de Notification de Windows (WNS) avec les informations d’identification WNS pour une application Windows.</span><span class="sxs-lookup"><span data-stu-id="f17ad-145">These variables are used tooconnect tooyour namespace and create a new Notification Hub configured toohandle Windows Notification Services (WNS) notifications with WNS credentials for a Windows App.</span></span> <span data-ttu-id="f17ad-146">Pour plus d’informations sur l’obtention de hello SID et package, consultez clé secrète hello [mise en route avec Notification Hubs](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="f17ad-146">For information on obtaining hello package SID and secret key see, hello [Getting Started with Notification Hubs](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span></span> 

* <span data-ttu-id="f17ad-147">extrait de code de script Hello utilise hello `NamespaceManager` si hello Hub de Notification est identifiée par l’objet toocheck toosee `$Path` existe.</span><span class="sxs-lookup"><span data-stu-id="f17ad-147">hello script snippet uses hello `NamespaceManager` object toocheck toosee if hello Notification Hub identified by `$Path` exists.</span></span>
* <span data-ttu-id="f17ad-148">Si elle n’existe pas, hello script crée un `NotificationHubDescription` avec WNS informations d’identification et passer ce toohello `NamespaceManager` classe `CreateNotificationHub` (méthode).</span><span class="sxs-lookup"><span data-stu-id="f17ad-148">If it does not exist, hello script will create an `NotificationHubDescription` with WNS credentials and pass that toohello `NamespaceManager` class `CreateNotificationHub` method.</span></span>

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




## <a name="additional-resources"></a><span data-ttu-id="f17ad-149">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="f17ad-149">Additional Resources</span></span>
* [<span data-ttu-id="f17ad-150">Gestion de Service Bus avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="f17ad-150">Manage Service Bus with PowerShell</span></span>](../service-bus-messaging/service-bus-powershell-how-to-provision.md)
* [<span data-ttu-id="f17ad-151">Comment toocreate Service Bus files d’attente, rubriques et abonnements à l’aide d’un script PowerShell</span><span class="sxs-lookup"><span data-stu-id="f17ad-151">How toocreate Service Bus queues, topics and subscriptions using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [<span data-ttu-id="f17ad-152">Comment toocreate un Service Bus Namespace et qu’un concentrateur d’événements à l’aide d’un script PowerShell</span><span class="sxs-lookup"><span data-stu-id="f17ad-152">How toocreate a Service Bus Namespace and an Event Hub using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)

<span data-ttu-id="f17ad-153">Vous pouvez également télécharger des scripts prêts à l’emploi :</span><span class="sxs-lookup"><span data-stu-id="f17ad-153">Some ready-made scripts are also available for download:</span></span>

* [<span data-ttu-id="f17ad-154">Scripts PowerShell pour Service Bus</span><span class="sxs-lookup"><span data-stu-id="f17ad-154">Service Bus PowerShell Scripts</span></span>](https://code.msdn.microsoft.com/windowsazure/Service-Bus-PowerShell-a46b7059)

[Modes d’achat d’Azure]: http://azure.microsoft.com/pricing/purchase-options/
[Offres spéciales membres]: http://azure.microsoft.com/pricing/member-offers/
[Version d'évaluation gratuite]: http://azure.microsoft.com/pricing/free-trial/
[Installation et configuration d'Azure PowerShell]: /powershell/azureps-cmdlets-docs
[API .NET pour les concentrateurs de Notification]: https://msdn.microsoft.com/library/azure/mt414893.aspx
[Get-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495122.aspx
[New-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495165.aspx
[Get-AzureSBAuthorizationRule]: https://msdn.microsoft.com/library/azure/dn495113.aspx

