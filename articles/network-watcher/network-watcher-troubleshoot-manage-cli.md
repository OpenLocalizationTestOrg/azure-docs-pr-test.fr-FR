---
title: "Résoudre des problèmes liés à la passerelle de réseau virtuel et aux connexions Azure - Azure CLI 2.0 | Microsoft Docs"
description: "Cette page explique comment utiliser Azure Network Watcher pour résoudre des problèmes liés à Azure CLI 2.0"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2838bc61-b182-4da8-8533-27db8fdbd177
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: e1d56317b10fa738a3d7089f6c4f357159fe2c2b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-azure-cli-20"></a><span data-ttu-id="52d64-103">Résoudre des problèmes liés à la passerelle de réseau virtuel et aux connexions à l’aide de l’Azure CLI 2.0 d’Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="52d64-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="52d64-104">Portail</span><span class="sxs-lookup"><span data-stu-id="52d64-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="52d64-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="52d64-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="52d64-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="52d64-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="52d64-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="52d64-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="52d64-108">API REST</span><span class="sxs-lookup"><span data-stu-id="52d64-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="52d64-109">Le service Network Watcher offre de nombreuses fonctionnalités en lien avec la bonne compréhension de vos ressources réseau dans Azure.</span><span class="sxs-lookup"><span data-stu-id="52d64-109">Network Watcher provides many capabilities as it relates to understanding your network resources in Azure.</span></span> <span data-ttu-id="52d64-110">Il permet notamment de résoudre les problèmes liés aux ressources.</span><span class="sxs-lookup"><span data-stu-id="52d64-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="52d64-111">Vous pouvez appeler la solution de résolution des problèmes de ressources par le biais du portail, de PowerShell, de l’interface de ligne de commande ou de l’API REST.</span><span class="sxs-lookup"><span data-stu-id="52d64-111">Resource troubleshooting can be called through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="52d64-112">Lorsque cette fonctionnalité est appelée, Network Watcher inspecte l’intégrité d’une passerelle de réseau virtuel ou d’une connexion et renvoie ses résultats.</span><span class="sxs-lookup"><span data-stu-id="52d64-112">When called, Network Watcher inspects the health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="52d64-113">Dans cet article, notre CLI nouvelle génération, Azure CLI 2.0, est utilisée pour le modèle de déploiement de gestion des ressources. Celle-ci est disponible pour Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="52d64-113">This article uses our next generation CLI for the resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="52d64-114">Pour exécuter la procédure indiquée dans cet article, vous devez [installer l’interface de ligne de commande Azure pour Mac, Linux et Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="52d64-114">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="52d64-115">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="52d64-115">Before you begin</span></span>

<span data-ttu-id="52d64-116">Ce scénario suppose que vous ayez déjà suivi la procédure décrite dans [Créer une instance d’Azure Network Watcher](network-watcher-create.md) pour créer un Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="52d64-116">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

<span data-ttu-id="52d64-117">Vous trouverez la liste des types de passerelles pris en charge sur la page [Types de passerelles pris en charge](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="52d64-117">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="52d64-118">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="52d64-118">Overview</span></span>

<span data-ttu-id="52d64-119">La résolution des problèmes liés aux ressources offre la possibilité de résoudre les problèmes qui surviennent avec les passerelles de réseau virtuel et les connexions.</span><span class="sxs-lookup"><span data-stu-id="52d64-119">Resource troubleshooting provides the ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="52d64-120">Lorsqu’une demande de résolution des problèmes liés aux ressources est faite, les journaux sont interrogés et inspectés.</span><span class="sxs-lookup"><span data-stu-id="52d64-120">When a request is made to resource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="52d64-121">Lorsque l’inspection est terminée, les résultats sont renvoyés.</span><span class="sxs-lookup"><span data-stu-id="52d64-121">When inspection is complete, the results are returned.</span></span> <span data-ttu-id="52d64-122">Les demandes de résolution des problèmes liés aux ressources sont longues : vous devrez peut-être patienter plusieurs minutes avant d’obtenir un résultat.</span><span class="sxs-lookup"><span data-stu-id="52d64-122">Resource troubleshooting requests are long running requests, which could take multiple minutes to return a result.</span></span> <span data-ttu-id="52d64-123">Les journaux de dépannage sont stockés dans un conteneur sur un compte de stockage spécifié.</span><span class="sxs-lookup"><span data-stu-id="52d64-123">The logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="52d64-124">Récupérer une connexion de passerelle de réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="52d64-124">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="52d64-125">Dans cet exemple, la résolution des problèmes liés aux ressources s’effectue sur une connexion.</span><span class="sxs-lookup"><span data-stu-id="52d64-125">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="52d64-126">Vous pouvez également la transférer à une passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="52d64-126">You can also pass it a Virtual Network Gateway.</span></span> <span data-ttu-id="52d64-127">L’applet de commande suivante répertorie les connexions vpn dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="52d64-127">The following cmdlet lists the vpn-connections in a resource group.</span></span>

```azurecli
az network vpn-connection list --resource-group resourceGroupName
```

<span data-ttu-id="52d64-128">Une fois que vous connaissez le nom de la connexion, vous pouvez exécuter cette commande pour obtenir son ID de ressource :</span><span class="sxs-lookup"><span data-stu-id="52d64-128">Once you have the name of the connection, you can run this command to get its resource Id:</span></span>

```azurecli
az network vpn-connection show --resource-group resourceGroupName --ids vpnConnectionIds
```

## <a name="create-a-storage-account"></a><span data-ttu-id="52d64-129">Créez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="52d64-129">Create a storage account</span></span>

<span data-ttu-id="52d64-130">La résolution des problèmes liés aux ressources renvoie des données concernant l’intégrité de la ressource, et elle enregistre les journaux dans un compte de stockage qui fera l’objet d’une révision.</span><span class="sxs-lookup"><span data-stu-id="52d64-130">Resource troubleshooting returns data about the health of the resource, it also saves logs to a storage account to be reviewed.</span></span> <span data-ttu-id="52d64-131">À cette étape, nous créons un compte de stockage. Si vous disposez déjà d’un compte de stockage existant, vous pouvez l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="52d64-131">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

1. <span data-ttu-id="52d64-132">Créer le compte de stockage</span><span class="sxs-lookup"><span data-stu-id="52d64-132">Create the storage account</span></span>

    ```azurecli
    az storage account create --name storageAccountName --location westcentralus --resource-group resourceGroupName --sku Standard_LRS
    ```

1. <span data-ttu-id="52d64-133">Obtenir les clés du compte de stockage</span><span class="sxs-lookup"><span data-stu-id="52d64-133">Get the storage account keys</span></span>

    ```azurecli
    az storage account keys list --resource-group resourcegroupName --account-name storageAccountName
    ```

1. <span data-ttu-id="52d64-134">Créer le conteneur</span><span class="sxs-lookup"><span data-stu-id="52d64-134">Create the container</span></span>

    ```azurecli
    az storage container create --account-name storageAccountName --account-key {storageAccountKey} --name logs
    ```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="52d64-135">Procéder à la résolution des problèmes liés aux ressources Network Watcher</span><span class="sxs-lookup"><span data-stu-id="52d64-135">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="52d64-136">Résolvez les problèmes liés aux ressources avec l’applet de commande `az network watcher troubleshooting`.</span><span class="sxs-lookup"><span data-stu-id="52d64-136">You troubleshoot resources with the `az network watcher troubleshooting` cmdlet.</span></span> <span data-ttu-id="52d64-137">Nous transférons à l’applet de commande le groupe de ressources, le nom de Network Watcher, l’identifiant de la connexion, l’identifiant du compte de stockage, et le chemin d’accès à l’objet blob pour y stocker les résultats de résolution des problèmes.</span><span class="sxs-lookup"><span data-stu-id="52d64-137">We pass the cmdlet the resource group, the name of the Network Watcher, the Id of the connection, the Id of the storage account, and the path to the blob to store the troubleshoot results in.</span></span>

```azurecli
az network watcher troubleshooting start --resource-group resourceGroupName --resource resourceName --resource-type {vnetGateway/vpnConnection} --storage-account storageAccountName  --storage-path https://{storageAccountName}.blob.core.windows.net/{containerName}
```

<span data-ttu-id="52d64-138">Une fois l’applet de commande exécutée, Network Watcher passe en revue la ressource pour vérifier son intégrité.</span><span class="sxs-lookup"><span data-stu-id="52d64-138">Once you run the cmdlet, Network Watcher reviews the resource to verify the health.</span></span> <span data-ttu-id="52d64-139">Les résultats sont renvoyés à l’interpréteur de commandes, et les journaux des résultats sont stockés dans le compte de stockage spécifié.</span><span class="sxs-lookup"><span data-stu-id="52d64-139">It returns the results to the shell and stores logs of the results in the storage account specified.</span></span>

## <a name="understanding-the-results"></a><span data-ttu-id="52d64-140">Compréhension des résultats</span><span class="sxs-lookup"><span data-stu-id="52d64-140">Understanding the results</span></span>

<span data-ttu-id="52d64-141">Le texte d’action fournit des indications générales sur la façon de résoudre le problème.</span><span class="sxs-lookup"><span data-stu-id="52d64-141">The action text provides general guidance on how to resolve the issue.</span></span> <span data-ttu-id="52d64-142">Si une action peut être entreprise pour résoudre le problème, un lien est fourni avec des indications supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="52d64-142">If an action can be taken for the issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="52d64-143">En l’absence d’indications supplémentaires, la réponse fournit l’URL permettant d’ouvrir un dossier de support.</span><span class="sxs-lookup"><span data-stu-id="52d64-143">In the case where there is no additional guidance, the response provides the url to open a support case.</span></span>  <span data-ttu-id="52d64-144">Pour plus d’informations sur les propriétés de la réponse et sur ce qu’elle contient, consultez [Network Watcher Troubleshoot overview (Vue d’ensemble de la résolution des problèmes Network Watcher)](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="52d64-144">For more information about the properties of the response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="52d64-145">Pour obtenir des instructions de téléchargement des fichiers à partir des comptes de stockage Azure, consultez [Prise en main du stockage d’objets blob Azure à l’aide de .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="52d64-145">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="52d64-146">L’explorateur de stockage peut aussi être utilisé.</span><span class="sxs-lookup"><span data-stu-id="52d64-146">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="52d64-147">Pour en savoir plus sur l’explorateur de stockage, cliquez sur le lien suivant : [Explorateur de stockage](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="52d64-147">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="52d64-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="52d64-148">Next steps</span></span>

<span data-ttu-id="52d64-149">Si les paramètres ont été modifiés et arrêtent la connectivité VPN, consultez la page [Gérer les groupes de sécurité réseau à partir du portail](../virtual-network/virtual-network-manage-nsg-arm-portal.md) afin d’effectuer le suivi du groupe de sécurité réseau et des règles de sécurité pouvant être concernés.</span><span class="sxs-lookup"><span data-stu-id="52d64-149">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that may be in question.</span></span>
