---
title: "aaaTroubleshoot passerelle de réseau virtuel Azure et des connexions - PowerShell | Documents Microsoft"
description: "Cette page explique comment résoudre des toouse hello Observateur de réseau Azure les applet de commande PowerShell"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: f6f0a813-38b6-4a1f-8cfc-1dfdf979f595
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: b7dbe6e44e0fa1ea0481223a84098d7a57c068a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a><span data-ttu-id="f803a-103">Résoudre les problèmes liés à la passerelle de réseau virtuel et aux connexions par le biais de PowerShell d’Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="f803a-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="f803a-104">Portail</span><span class="sxs-lookup"><span data-stu-id="f803a-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="f803a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f803a-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="f803a-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="f803a-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="f803a-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f803a-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="f803a-108">API REST</span><span class="sxs-lookup"><span data-stu-id="f803a-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="f803a-109">Observateur réseau fournit de nombreuses fonctionnalités en matière de toounderstanding vos ressources réseau dans Azure.</span><span class="sxs-lookup"><span data-stu-id="f803a-109">Network Watcher provides many capabilities as it relates toounderstanding your network resources in Azure.</span></span> <span data-ttu-id="f803a-110">Il permet notamment de résoudre les problèmes liés aux ressources.</span><span class="sxs-lookup"><span data-stu-id="f803a-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="f803a-111">Résolution des problèmes de ressource peuvent être appelée via le portail de hello, PowerShell, CLI ou API REST.</span><span class="sxs-lookup"><span data-stu-id="f803a-111">Resource troubleshooting can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="f803a-112">Lorsqu’elle est appelée, Observateur réseau inspecte le contrôle d’intégrité hello d’une passerelle de réseau virtuel ou d’une connexion et retourne les résultats obtenus.</span><span class="sxs-lookup"><span data-stu-id="f803a-112">When called, Network Watcher inspects hello health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f803a-113">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="f803a-113">Before you begin</span></span>

<span data-ttu-id="f803a-114">Ce scénario suppose que vous avez déjà suivi les étapes hello dans [créer un observateur réseau](network-watcher-create.md) toocreate un observateur réseau.</span><span class="sxs-lookup"><span data-stu-id="f803a-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

<span data-ttu-id="f803a-115">Vous trouverez la liste des types de passerelles pris en charge sur la page [Types de passerelles pris en charge](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="f803a-115">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="f803a-116">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="f803a-116">Overview</span></span>

<span data-ttu-id="f803a-117">Résolution des problèmes de ressource permet de hello résoudre les problèmes qui surviennent avec les connexions et les passerelles de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f803a-117">Resource troubleshooting provides hello ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="f803a-118">Lorsqu’une demande est faite tooresource résolution des problèmes, les journaux sont en cours interrogées et inspecté.</span><span class="sxs-lookup"><span data-stu-id="f803a-118">When a request is made tooresource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="f803a-119">Lors de l’inspection est terminée, les résultats de hello sont retournés.</span><span class="sxs-lookup"><span data-stu-id="f803a-119">When inspection is complete, hello results are returned.</span></span> <span data-ttu-id="f803a-120">Demandes de résolution des problèmes sont à long terme des ressources des demandes, ce qui peut prendre plusieurs minutes tooreturn un résultat.</span><span class="sxs-lookup"><span data-stu-id="f803a-120">Resource troubleshooting requests are long running requests, which could take multiple minutes tooreturn a result.</span></span> <span data-ttu-id="f803a-121">journaux de Hello à partir de la résolution des problèmes sont stockés dans un conteneur sur un compte de stockage spécifié.</span><span class="sxs-lookup"><span data-stu-id="f803a-121">hello logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="f803a-122">Récupérer Network Watcher</span><span class="sxs-lookup"><span data-stu-id="f803a-122">Retrieve Network Watcher</span></span>

<span data-ttu-id="f803a-123">première étape de Hello est instance de l’Observateur réseau tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="f803a-123">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="f803a-124">Hello `$networkWatcher` variable est passée toohello `Start-AzureRmNetworkWatcherResourceTroubleshooting` applet de commande à l’étape 4.</span><span class="sxs-lookup"><span data-stu-id="f803a-124">hello `$networkWatcher` variable is passed toohello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet in step 4.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="f803a-125">Récupérer une connexion de passerelle de réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="f803a-125">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="f803a-126">Dans cet exemple, la résolution des problèmes liés aux ressources s’effectue sur une connexion.</span><span class="sxs-lookup"><span data-stu-id="f803a-126">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="f803a-127">Vous pouvez également la transférer à une passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f803a-127">You can also pass it a Virtual Network Gateway.</span></span>

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "2to3" -ResourceGroupName "testrg"
```

## <a name="create-a-storage-account"></a><span data-ttu-id="f803a-128">Créez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="f803a-128">Create a storage account</span></span>

<span data-ttu-id="f803a-129">Résolution des problèmes de ressource retourne des données concernant la santé de ressource de hello hello, il enregistre également les journaux tooa stockage compte toobe révisé.</span><span class="sxs-lookup"><span data-stu-id="f803a-129">Resource troubleshooting returns data about hello health of hello resource, it also saves logs tooa storage account toobe reviewed.</span></span> <span data-ttu-id="f803a-130">À cette étape, nous créons un compte de stockage. Si vous disposez déjà d’un compte de stockage existant, vous pouvez l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="f803a-130">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

```powershell
$sa = New-AzureRmStorageAccount -Name "contosoexamplesa" -SKU "Standard_LRS" -ResourceGroupName "testrg" -Location "WestCentralUS"
Set-AzureRmCurrentStorageAccount -ResourceGroupName $sa.ResourceGroupName -Name $sa.StorageAccountName
$sc = New-AzureStorageContainer -Name logs
```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="f803a-131">Procéder à la résolution des problèmes liés aux ressources Network Watcher</span><span class="sxs-lookup"><span data-stu-id="f803a-131">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="f803a-132">Résolution de ressources avec hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="f803a-132">You troubleshoot resources with hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet.</span></span> <span data-ttu-id="f803a-133">Nous passons hello applet de commande hello Observateur réseau objet, hello Id de connexion de hello ou passerelle de réseau virtuel, id de compte de stockage hello et résultats de hello toostore hello chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="f803a-133">We pass hello cmdlet hello Network Watcher object, hello Id of hello Connection or Virtual Network Gateway, hello storage account id, and hello path toostore hello results.</span></span>

> [!NOTE]
> <span data-ttu-id="f803a-134">Hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` applet de commande est longue et peut prendre quelques minutes toocomplete.</span><span class="sxs-lookup"><span data-stu-id="f803a-134">hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet is long running and may take a few minutes toocomplete.</span></span>

```powershell
Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath "$($sa.PrimaryEndpoints.Blob)$($sc.name)"
```

<span data-ttu-id="f803a-135">Une fois que vous exécutez applet de commande hello, Observateur réseau passe en revue hello tooverify hello contrôle d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="f803a-135">Once you run hello cmdlet, Network Watcher reviews hello resource tooverify hello health.</span></span> <span data-ttu-id="f803a-136">Il retourne les résultats hello toohello shell et stocke les journaux des résultats de hello hello compte de stockage spécifié.</span><span class="sxs-lookup"><span data-stu-id="f803a-136">It returns hello results toohello shell and stores logs of hello results in hello storage account specified.</span></span>

## <a name="understanding-hello-results"></a><span data-ttu-id="f803a-137">Présentation des résultats de hello</span><span class="sxs-lookup"><span data-stu-id="f803a-137">Understanding hello results</span></span>

<span data-ttu-id="f803a-138">texte d’action Hello fournit des indications générales sur la façon dont tooresolve hello problème.</span><span class="sxs-lookup"><span data-stu-id="f803a-138">hello action text provides general guidance on how tooresolve hello issue.</span></span> <span data-ttu-id="f803a-139">Si le problème de hello peut entreprendre une action, un lien est fourni avec des instructions supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="f803a-139">If an action can be taken for hello issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="f803a-140">Dans le cas de hello où il n’existe pas d’instructions supplémentaires, réponse de hello fournit hello url tooopen un cas de prise en charge.</span><span class="sxs-lookup"><span data-stu-id="f803a-140">In hello case where there is no additional guidance, hello response provides hello url tooopen a support case.</span></span>  <span data-ttu-id="f803a-141">Pour plus d’informations sur les propriétés de hello de réponse de hello et ce qui est inclus, visitez [vue d’ensemble de la résolution de l’Observateur réseau](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="f803a-141">For more information about hello properties of hello response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="f803a-142">Pour obtenir des instructions sur le téléchargement de fichiers à partir des comptes de stockage azure, consultez trop[prise en main le stockage Blob Azure à l’aide de .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="f803a-142">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="f803a-143">L’explorateur de stockage peut aussi être utilisé.</span><span class="sxs-lookup"><span data-stu-id="f803a-143">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="f803a-144">Plus d’informations sur l’Explorateur de stockage trouverez ici hello lien : [Explorateur de stockage](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="f803a-144">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="f803a-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f803a-145">Next steps</span></span>

<span data-ttu-id="f803a-146">Si les paramètres ont été modifiés qu’arrêter la connectivité VPN, consultez [gérer les groupes de sécurité réseau](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack vers le bas hello sécurité et groupe de règles de sécurité réseau qui peuvent être en question.</span><span class="sxs-lookup"><span data-stu-id="f803a-146">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that may be in question.</span></span>
