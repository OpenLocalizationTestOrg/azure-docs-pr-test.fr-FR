---
title: "Résoudre les problèmes liés à la passerelle de réseau virtuel et aux connexions Azure - PowerShell | Microsoft Docs"
description: "Cette page explique comment utiliser Azure Network Watcher pour résoudre les problèmes liés à l’applet de commande PowerShell"
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
ms.openlocfilehash: 0bdffbac18d1d236b7674feed4dbc784e50e0ea8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a><span data-ttu-id="45377-103">Résoudre les problèmes liés à la passerelle de réseau virtuel et aux connexions par le biais de PowerShell d’Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="45377-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="45377-104">Portail</span><span class="sxs-lookup"><span data-stu-id="45377-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="45377-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="45377-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="45377-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="45377-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="45377-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="45377-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="45377-108">API REST</span><span class="sxs-lookup"><span data-stu-id="45377-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="45377-109">Le service Network Watcher offre de nombreuses fonctionnalités en lien avec la bonne compréhension de vos ressources réseau dans Azure.</span><span class="sxs-lookup"><span data-stu-id="45377-109">Network Watcher provides many capabilities as it relates to understanding your network resources in Azure.</span></span> <span data-ttu-id="45377-110">Il permet notamment de résoudre les problèmes liés aux ressources.</span><span class="sxs-lookup"><span data-stu-id="45377-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="45377-111">Vous pouvez appeler la solution de résolution des problèmes de ressources par le biais du portail, de PowerShell, de l’interface de ligne de commande ou de l’API REST.</span><span class="sxs-lookup"><span data-stu-id="45377-111">Resource troubleshooting can be called through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="45377-112">Lorsque cette fonctionnalité est appelée, Network Watcher inspecte l’intégrité d’une passerelle de réseau virtuel ou d’une connexion et renvoie ses résultats.</span><span class="sxs-lookup"><span data-stu-id="45377-112">When called, Network Watcher inspects the health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="45377-113">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="45377-113">Before you begin</span></span>

<span data-ttu-id="45377-114">Ce scénario suppose que vous ayez déjà suivi la procédure décrite dans [Créer une instance d’Azure Network Watcher](network-watcher-create.md) pour créer un Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="45377-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

<span data-ttu-id="45377-115">Vous trouverez la liste des types de passerelles pris en charge sur la page [Types de passerelles pris en charge](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="45377-115">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="45377-116">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="45377-116">Overview</span></span>

<span data-ttu-id="45377-117">La résolution des problèmes liés aux ressources offre la possibilité de résoudre les problèmes qui surviennent avec les passerelles de réseau virtuel et les connexions.</span><span class="sxs-lookup"><span data-stu-id="45377-117">Resource troubleshooting provides the ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="45377-118">Lorsqu’une demande de résolution des problèmes liés aux ressources est faite, les journaux sont interrogés et inspectés.</span><span class="sxs-lookup"><span data-stu-id="45377-118">When a request is made to resource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="45377-119">Lorsque l’inspection est terminée, les résultats sont renvoyés.</span><span class="sxs-lookup"><span data-stu-id="45377-119">When inspection is complete, the results are returned.</span></span> <span data-ttu-id="45377-120">Les demandes de résolution des problèmes liés aux ressources sont longues : vous devrez peut-être patienter plusieurs minutes avant d’obtenir un résultat.</span><span class="sxs-lookup"><span data-stu-id="45377-120">Resource troubleshooting requests are long running requests, which could take multiple minutes to return a result.</span></span> <span data-ttu-id="45377-121">Les journaux de dépannage sont stockés dans un conteneur sur un compte de stockage spécifié.</span><span class="sxs-lookup"><span data-stu-id="45377-121">The logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="45377-122">Récupérer Network Watcher</span><span class="sxs-lookup"><span data-stu-id="45377-122">Retrieve Network Watcher</span></span>

<span data-ttu-id="45377-123">La première étape consiste à récupérer l’instance Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="45377-123">The first step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="45377-124">La variable `$networkWatcher` est transmise à l’applet de commande `Start-AzureRmNetworkWatcherResourceTroubleshooting` lors de l’étape 4.</span><span class="sxs-lookup"><span data-stu-id="45377-124">The `$networkWatcher` variable is passed to the `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet in step 4.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="45377-125">Récupérer une connexion de passerelle de réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="45377-125">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="45377-126">Dans cet exemple, la résolution des problèmes liés aux ressources s’effectue sur une connexion.</span><span class="sxs-lookup"><span data-stu-id="45377-126">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="45377-127">Vous pouvez également la transférer à une passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="45377-127">You can also pass it a Virtual Network Gateway.</span></span>

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "2to3" -ResourceGroupName "testrg"
```

## <a name="create-a-storage-account"></a><span data-ttu-id="45377-128">Créez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="45377-128">Create a storage account</span></span>

<span data-ttu-id="45377-129">La résolution des problèmes liés aux ressources renvoie des données concernant l’intégrité de la ressource, et elle enregistre les journaux dans un compte de stockage qui fera l’objet d’une révision.</span><span class="sxs-lookup"><span data-stu-id="45377-129">Resource troubleshooting returns data about the health of the resource, it also saves logs to a storage account to be reviewed.</span></span> <span data-ttu-id="45377-130">À cette étape, nous créons un compte de stockage. Si vous disposez déjà d’un compte de stockage existant, vous pouvez l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="45377-130">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

```powershell
$sa = New-AzureRmStorageAccount -Name "contosoexamplesa" -SKU "Standard_LRS" -ResourceGroupName "testrg" -Location "WestCentralUS"
Set-AzureRmCurrentStorageAccount -ResourceGroupName $sa.ResourceGroupName -Name $sa.StorageAccountName
$sc = New-AzureStorageContainer -Name logs
```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="45377-131">Procéder à la résolution des problèmes liés aux ressources Network Watcher</span><span class="sxs-lookup"><span data-stu-id="45377-131">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="45377-132">Résolvez les problèmes liés aux ressources avec l’applet de commande `Start-AzureRmNetworkWatcherResourceTroubleshooting`.</span><span class="sxs-lookup"><span data-stu-id="45377-132">You troubleshoot resources with the `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet.</span></span> <span data-ttu-id="45377-133">Nous transmettons à l’applet de commande l’objet Network Watcher, l’ID de la connexion ou la passerelle de réseau virtuel, l’ID de compte de stockage et le chemin d’accès pour stocker les résultats.</span><span class="sxs-lookup"><span data-stu-id="45377-133">We pass the cmdlet the Network Watcher object, the Id of the Connection or Virtual Network Gateway, the storage account id, and the path to store the results.</span></span>

> [!NOTE]
> <span data-ttu-id="45377-134">L’exécution de l’applet de commande `Start-AzureRmNetworkWatcherResourceTroubleshooting` est longue et peut prendre quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="45377-134">The `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet is long running and may take a few minutes to complete.</span></span>

```powershell
Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath "$($sa.PrimaryEndpoints.Blob)$($sc.name)"
```

<span data-ttu-id="45377-135">Une fois l’applet de commande exécutée, Network Watcher passe en revue la ressource pour vérifier son intégrité.</span><span class="sxs-lookup"><span data-stu-id="45377-135">Once you run the cmdlet, Network Watcher reviews the resource to verify the health.</span></span> <span data-ttu-id="45377-136">Les résultats sont renvoyés à l’interpréteur de commandes, et les journaux des résultats sont stockés dans le compte de stockage spécifié.</span><span class="sxs-lookup"><span data-stu-id="45377-136">It returns the results to the shell and stores logs of the results in the storage account specified.</span></span>

## <a name="understanding-the-results"></a><span data-ttu-id="45377-137">Compréhension des résultats</span><span class="sxs-lookup"><span data-stu-id="45377-137">Understanding the results</span></span>

<span data-ttu-id="45377-138">Le texte d’action fournit des indications générales sur la façon de résoudre le problème.</span><span class="sxs-lookup"><span data-stu-id="45377-138">The action text provides general guidance on how to resolve the issue.</span></span> <span data-ttu-id="45377-139">Si une action peut être entreprise pour résoudre le problème, un lien est fourni avec des indications supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="45377-139">If an action can be taken for the issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="45377-140">En l’absence d’indications supplémentaires, la réponse fournit l’URL permettant d’ouvrir un dossier de support.</span><span class="sxs-lookup"><span data-stu-id="45377-140">In the case where there is no additional guidance, the response provides the url to open a support case.</span></span>  <span data-ttu-id="45377-141">Pour plus d’informations sur les propriétés de la réponse et sur ce qu’elle contient, consultez [Network Watcher Troubleshoot overview (Vue d’ensemble de la résolution des problèmes Network Watcher)](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="45377-141">For more information about the properties of the response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="45377-142">Pour obtenir des instructions de téléchargement des fichiers à partir des comptes de stockage Azure, consultez [Prise en main du stockage d’objets blob Azure à l’aide de .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="45377-142">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="45377-143">L’explorateur de stockage peut aussi être utilisé.</span><span class="sxs-lookup"><span data-stu-id="45377-143">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="45377-144">Pour en savoir plus sur l’explorateur de stockage, cliquez sur le lien suivant : [Explorateur de stockage](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="45377-144">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="45377-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="45377-145">Next steps</span></span>

<span data-ttu-id="45377-146">Si les paramètres ont été modifiés et arrêtent la connectivité VPN, consultez la page [Gérer les groupes de sécurité réseau à partir du portail](../virtual-network/virtual-network-manage-nsg-arm-portal.md) afin d’effectuer le suivi du groupe de sécurité réseau et des règles de sécurité pouvant être concernés.</span><span class="sxs-lookup"><span data-stu-id="45377-146">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that may be in question.</span></span>
