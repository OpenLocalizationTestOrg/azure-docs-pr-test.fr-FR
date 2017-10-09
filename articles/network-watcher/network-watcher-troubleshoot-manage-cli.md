---
title: "aaaTroubleshoot connexions - Azure CLI 2.0 et la passerelle de réseau virtuel Azure | Documents Microsoft"
description: "Cette page explique comment toouse hello Observateur de réseau Azure dépanner Azure CLI 2.0"
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
ms.openlocfilehash: 389e86f247722412a1d0e2e722dbf80bb7cff291
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-azure-cli-20"></a><span data-ttu-id="a1cea-103">Résoudre des problèmes liés à la passerelle de réseau virtuel et aux connexions à l’aide de l’Azure CLI 2.0 d’Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="a1cea-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="a1cea-104">Portail</span><span class="sxs-lookup"><span data-stu-id="a1cea-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="a1cea-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a1cea-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="a1cea-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a1cea-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="a1cea-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a1cea-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="a1cea-108">API REST</span><span class="sxs-lookup"><span data-stu-id="a1cea-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="a1cea-109">Observateur réseau fournit de nombreuses fonctionnalités en matière de toounderstanding vos ressources réseau dans Azure.</span><span class="sxs-lookup"><span data-stu-id="a1cea-109">Network Watcher provides many capabilities as it relates toounderstanding your network resources in Azure.</span></span> <span data-ttu-id="a1cea-110">Il permet notamment de résoudre les problèmes liés aux ressources.</span><span class="sxs-lookup"><span data-stu-id="a1cea-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="a1cea-111">Résolution des problèmes de ressource peuvent être appelée via le portail de hello, PowerShell, CLI ou API REST.</span><span class="sxs-lookup"><span data-stu-id="a1cea-111">Resource troubleshooting can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="a1cea-112">Lorsqu’elle est appelée, Observateur réseau inspecte le contrôle d’intégrité hello d’une passerelle de réseau virtuel ou d’une connexion et retourne les résultats obtenus.</span><span class="sxs-lookup"><span data-stu-id="a1cea-112">When called, Network Watcher inspects hello health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="a1cea-113">Cet article utilise notre prochaine génération CLI pour le modèle de déploiement de la gestion des ressources d’hello, Azure CLI 2.0, qui est disponible pour Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="a1cea-113">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="a1cea-114">les étapes tooperform hello dans cet article, vous devez trop[installer hello Interface de ligne de commande Azure pour Mac, Linux et Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="a1cea-114">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a1cea-115">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="a1cea-115">Before you begin</span></span>

<span data-ttu-id="a1cea-116">Ce scénario suppose que vous avez déjà suivi les étapes hello dans [créer un observateur réseau](network-watcher-create.md) toocreate un observateur réseau.</span><span class="sxs-lookup"><span data-stu-id="a1cea-116">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

<span data-ttu-id="a1cea-117">Vous trouverez la liste des types de passerelles pris en charge sur la page [Types de passerelles pris en charge](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="a1cea-117">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="a1cea-118">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="a1cea-118">Overview</span></span>

<span data-ttu-id="a1cea-119">Résolution des problèmes de ressource permet de hello résoudre les problèmes qui surviennent avec les connexions et les passerelles de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="a1cea-119">Resource troubleshooting provides hello ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="a1cea-120">Lorsqu’une demande est faite tooresource résolution des problèmes, les journaux sont en cours interrogées et inspecté.</span><span class="sxs-lookup"><span data-stu-id="a1cea-120">When a request is made tooresource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="a1cea-121">Lors de l’inspection est terminée, les résultats de hello sont retournés.</span><span class="sxs-lookup"><span data-stu-id="a1cea-121">When inspection is complete, hello results are returned.</span></span> <span data-ttu-id="a1cea-122">Demandes de résolution des problèmes sont à long terme des ressources des demandes, ce qui peut prendre plusieurs minutes tooreturn un résultat.</span><span class="sxs-lookup"><span data-stu-id="a1cea-122">Resource troubleshooting requests are long running requests, which could take multiple minutes tooreturn a result.</span></span> <span data-ttu-id="a1cea-123">journaux de Hello à partir de la résolution des problèmes sont stockés dans un conteneur sur un compte de stockage spécifié.</span><span class="sxs-lookup"><span data-stu-id="a1cea-123">hello logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="a1cea-124">Récupérer une connexion de passerelle de réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="a1cea-124">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="a1cea-125">Dans cet exemple, la résolution des problèmes liés aux ressources s’effectue sur une connexion.</span><span class="sxs-lookup"><span data-stu-id="a1cea-125">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="a1cea-126">Vous pouvez également la transférer à une passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="a1cea-126">You can also pass it a Virtual Network Gateway.</span></span> <span data-ttu-id="a1cea-127">Hello applet de commande suivante répertorie les connexions vpn hello dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="a1cea-127">hello following cmdlet lists hello vpn-connections in a resource group.</span></span>

```azurecli
az network vpn-connection list --resource-group resourceGroupName
```

<span data-ttu-id="a1cea-128">Une fois que vous avez nom hello de connexion de hello, vous pouvez exécuter cette commande tooget son Id de ressource :</span><span class="sxs-lookup"><span data-stu-id="a1cea-128">Once you have hello name of hello connection, you can run this command tooget its resource Id:</span></span>

```azurecli
az network vpn-connection show --resource-group resourceGroupName --ids vpnConnectionIds
```

## <a name="create-a-storage-account"></a><span data-ttu-id="a1cea-129">Créez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="a1cea-129">Create a storage account</span></span>

<span data-ttu-id="a1cea-130">Résolution des problèmes de ressource retourne des données concernant la santé de ressource de hello hello, il enregistre également les journaux tooa stockage compte toobe révisé.</span><span class="sxs-lookup"><span data-stu-id="a1cea-130">Resource troubleshooting returns data about hello health of hello resource, it also saves logs tooa storage account toobe reviewed.</span></span> <span data-ttu-id="a1cea-131">À cette étape, nous créons un compte de stockage. Si vous disposez déjà d’un compte de stockage existant, vous pouvez l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="a1cea-131">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

1. <span data-ttu-id="a1cea-132">Créer le compte de stockage hello</span><span class="sxs-lookup"><span data-stu-id="a1cea-132">Create hello storage account</span></span>

    ```azurecli
    az storage account create --name storageAccountName --location westcentralus --resource-group resourceGroupName --sku Standard_LRS
    ```

1. <span data-ttu-id="a1cea-133">Obtenir les clés de compte de stockage hello</span><span class="sxs-lookup"><span data-stu-id="a1cea-133">Get hello storage account keys</span></span>

    ```azurecli
    az storage account keys list --resource-group resourcegroupName --account-name storageAccountName
    ```

1. <span data-ttu-id="a1cea-134">Créer un conteneur de hello</span><span class="sxs-lookup"><span data-stu-id="a1cea-134">Create hello container</span></span>

    ```azurecli
    az storage container create --account-name storageAccountName --account-key {storageAccountKey} --name logs
    ```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="a1cea-135">Procéder à la résolution des problèmes liés aux ressources Network Watcher</span><span class="sxs-lookup"><span data-stu-id="a1cea-135">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="a1cea-136">Résolution de ressources avec hello `az network watcher troubleshooting` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="a1cea-136">You troubleshoot resources with hello `az network watcher troubleshooting` cmdlet.</span></span> <span data-ttu-id="a1cea-137">Nous transmettons le groupe de ressources hello applet de commande hello et Id de compte de stockage hello hello hello nom Hello Observateur réseau, hello Id de connexion de hello, Bonjour chemin d’accès toohello blob toostore Bonjour résoudre les résultats dans.</span><span class="sxs-lookup"><span data-stu-id="a1cea-137">We pass hello cmdlet hello resource group, hello name of hello Network Watcher, hello Id of hello connection, hello Id of hello storage account, and hello path toohello blob toostore hello troubleshoot results in.</span></span>

```azurecli
az network watcher troubleshooting start --resource-group resourceGroupName --resource resourceName --resource-type {vnetGateway/vpnConnection} --storage-account storageAccountName  --storage-path https://{storageAccountName}.blob.core.windows.net/{containerName}
```

<span data-ttu-id="a1cea-138">Une fois que vous exécutez applet de commande hello, Observateur réseau passe en revue hello tooverify hello contrôle d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="a1cea-138">Once you run hello cmdlet, Network Watcher reviews hello resource tooverify hello health.</span></span> <span data-ttu-id="a1cea-139">Il retourne les résultats hello toohello shell et stocke les journaux des résultats de hello hello compte de stockage spécifié.</span><span class="sxs-lookup"><span data-stu-id="a1cea-139">It returns hello results toohello shell and stores logs of hello results in hello storage account specified.</span></span>

## <a name="understanding-hello-results"></a><span data-ttu-id="a1cea-140">Présentation des résultats de hello</span><span class="sxs-lookup"><span data-stu-id="a1cea-140">Understanding hello results</span></span>

<span data-ttu-id="a1cea-141">texte d’action Hello fournit des indications générales sur la façon dont tooresolve hello problème.</span><span class="sxs-lookup"><span data-stu-id="a1cea-141">hello action text provides general guidance on how tooresolve hello issue.</span></span> <span data-ttu-id="a1cea-142">Si le problème de hello peut entreprendre une action, un lien est fourni avec des instructions supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="a1cea-142">If an action can be taken for hello issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="a1cea-143">Dans le cas de hello où il n’existe pas d’instructions supplémentaires, réponse de hello fournit hello url tooopen un cas de prise en charge.</span><span class="sxs-lookup"><span data-stu-id="a1cea-143">In hello case where there is no additional guidance, hello response provides hello url tooopen a support case.</span></span>  <span data-ttu-id="a1cea-144">Pour plus d’informations sur les propriétés de hello de réponse de hello et ce qui est inclus, visitez [vue d’ensemble de la résolution de l’Observateur réseau](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="a1cea-144">For more information about hello properties of hello response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="a1cea-145">Pour obtenir des instructions sur le téléchargement de fichiers à partir des comptes de stockage azure, consultez trop[prise en main le stockage Blob Azure à l’aide de .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="a1cea-145">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="a1cea-146">L’explorateur de stockage peut aussi être utilisé.</span><span class="sxs-lookup"><span data-stu-id="a1cea-146">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="a1cea-147">Plus d’informations sur l’Explorateur de stockage trouverez ici hello lien : [Explorateur de stockage](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="a1cea-147">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1cea-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a1cea-148">Next steps</span></span>

<span data-ttu-id="a1cea-149">Si les paramètres ont été modifiés qu’arrêter la connectivité VPN, consultez [gérer les groupes de sécurité réseau](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack vers le bas hello sécurité et groupe de règles de sécurité réseau qui peuvent être en question.</span><span class="sxs-lookup"><span data-stu-id="a1cea-149">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that may be in question.</span></span>
