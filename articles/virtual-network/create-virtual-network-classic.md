---
title: "aaaCreate un réseau virtuel Azure (classique) avec plusieurs sous-réseaux | Documents Microsoft"
description: "Découvrez comment toocreate un réseau virtuel (classique) avec plusieurs sous-réseaux dans Azure."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: cc7b9ad08d5c26dba09584762bedf614d2847032
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-classic-with-multiple-subnets"></a><span data-ttu-id="47700-103">Créer un réseau virtuel (Classic) comprenant plusieurs sous-réseaux</span><span class="sxs-lookup"><span data-stu-id="47700-103">Create a virtual network (classic) with multiple subnets</span></span>

> [!IMPORTANT]
> <span data-ttu-id="47700-104">Azure dispose de deux [modèles de déploiement différents](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) pour créer et utiliser des ressources : le déploiement Resource Manager et le déploiement Classic.</span><span class="sxs-lookup"><span data-stu-id="47700-104">Azure has two [different deployment models](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) for creating and working with resources: Resource Manager and classic.</span></span> <span data-ttu-id="47700-105">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="47700-105">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="47700-106">Microsoft recommande de créer la plupart des nouveaux réseaux virtuels via hello [le Gestionnaire de ressources](virtual-networks-create-vnet-arm-pportal.md) modèle de déploiement.</span><span class="sxs-lookup"><span data-stu-id="47700-106">Microsoft recommends creating most new virtual networks through hello [Resource Manager](virtual-networks-create-vnet-arm-pportal.md) deployment model.</span></span>

<span data-ttu-id="47700-107">Dans ce didacticiel, découvrez comment toocreate un base réseau virtuel Azure (classique) qui a séparer les sous-réseaux privés et publics.</span><span class="sxs-lookup"><span data-stu-id="47700-107">In this tutorial, learn how toocreate a basic Azure virtual network (classic) that has separate public and private subnets.</span></span> <span data-ttu-id="47700-108">Vous pouvez créer des ressources Azure, telles que des machines virtuelles et des services cloud, dans un sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="47700-108">You can create Azure resources, like Virtual machines and Cloud services in a subnet.</span></span> <span data-ttu-id="47700-109">Ressources créées dans des réseaux virtuels (classiques) peuvent communiquer entre eux et avec les ressources d’un autre réseau virtuel connecté tooa de réseaux.</span><span class="sxs-lookup"><span data-stu-id="47700-109">Resources created in virtual networks (classic) can communicate with each other, and with resources in other networks connected tooa virtual network.</span></span>

<span data-ttu-id="47700-110">Apprenez-en davantage sur tous les paramètres de [réseau virtuel](virtual-network-manage-network.md) et de [sous-réseau](virtual-network-manage-subnet.md).</span><span class="sxs-lookup"><span data-stu-id="47700-110">Learn more about all [virtual network](virtual-network-manage-network.md) and [subnet](virtual-network-manage-subnet.md) settings.</span></span>

> [!WARNING]
> <span data-ttu-id="47700-111">Azure supprime immédiatement les réseaux virtuels (Classic) quand un [abonnement est désactivé](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit).</span><span class="sxs-lookup"><span data-stu-id="47700-111">Virtual networks (classic) are immediately deleted by Azure when a [subscription is disabled](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit).</span></span> <span data-ttu-id="47700-112">Les réseaux virtuels (classiques) sont supprimées, quelle que soit l’existent de ressources dans le réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="47700-112">Virtual networks (classic) are deleted regardless of whether resources exist in hello virtual network.</span></span> <span data-ttu-id="47700-113">Si vous ré-activez ultérieurement abonnement de hello, les ressources qui existaient dans le réseau virtuel de hello doivent être recréés.</span><span class="sxs-lookup"><span data-stu-id="47700-113">If you later re-enable hello subscription, resources that existed in hello virtual network must be recreated.</span></span>

<span data-ttu-id="47700-114">Vous pouvez créer un réseau virtuel (classiques) à l’aide de hello [portail Azure](#portal), hello [Azure interface de ligne de commande (CLI) 1.0](#azure-cli), ou [PowerShell](#powershell).</span><span class="sxs-lookup"><span data-stu-id="47700-114">You can create a virtual network (classic) by using hello [Azure portal](#portal), hello [Azure command-line interface (CLI) 1.0](#azure-cli), or [PowerShell](#powershell).</span></span>

## <a name="portal"></a><span data-ttu-id="47700-115">Portail</span><span class="sxs-lookup"><span data-stu-id="47700-115">Portal</span></span>

1. <span data-ttu-id="47700-116">Dans un navigateur Internet, accédez à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="47700-116">In an Internet browser, go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="47700-117">Connectez-vous à votre [compte Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="47700-117">Log in using your [Azure account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="47700-118">Si vous n’en avez pas, vous pouvez demander un [essai gratuit](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="47700-118">If you don't have an Azure account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="47700-119">Cliquez sur **+ nouveau** dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="47700-119">Click **+New** in hello portal.</span></span>
3. <span data-ttu-id="47700-120">Entrez *réseau virtuel* Bonjour **hello de recherche Marketplace** zone en haut de hello de hello **nouveau** panneau s’affiche.</span><span class="sxs-lookup"><span data-stu-id="47700-120">Enter *Virtual network* in hello **Search hello Marketplace** box at hello top of hello **New** blade that appears.</span></span>  <span data-ttu-id="47700-121">Cliquez sur **réseau virtuel** lorsqu’il apparaît dans les résultats de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="47700-121">Click **Virtual network** when it appears in hello search results.</span></span>
4. <span data-ttu-id="47700-122">Sélectionnez **classique** Bonjour **sélectionner un modèle de déploiement** zone hello **réseau virtuel** panneau qui s’affiche, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="47700-122">Select **Classic** in hello **Select a deployment model** box in hello **Virtual Network** blade that appears, then click **Create**.</span></span> 
5. <span data-ttu-id="47700-123">Entrez hello suivant de valeurs de hello **créer un réseau virtuel (classiques)** panneau, puis cliquez sur **créer**:</span><span class="sxs-lookup"><span data-stu-id="47700-123">Enter hello following values on hello **Create virtual network (classic)** blade and then click **Create**:</span></span>

    |<span data-ttu-id="47700-124">Paramètre</span><span class="sxs-lookup"><span data-stu-id="47700-124">Setting</span></span>|<span data-ttu-id="47700-125">Valeur</span><span class="sxs-lookup"><span data-stu-id="47700-125">Value</span></span>|
    |---|---|
    |<span data-ttu-id="47700-126">Nom</span><span class="sxs-lookup"><span data-stu-id="47700-126">Name</span></span>|<span data-ttu-id="47700-127">myVnet</span><span class="sxs-lookup"><span data-stu-id="47700-127">myVnet</span></span>|
    |<span data-ttu-id="47700-128">Espace d’adressage</span><span class="sxs-lookup"><span data-stu-id="47700-128">Address space</span></span>|<span data-ttu-id="47700-129">10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="47700-129">10.0.0.0/16</span></span>|
    |<span data-ttu-id="47700-130">Nom du sous-réseau</span><span class="sxs-lookup"><span data-stu-id="47700-130">Subnet name</span></span>|<span data-ttu-id="47700-131">Public</span><span class="sxs-lookup"><span data-stu-id="47700-131">Public</span></span>|
    |<span data-ttu-id="47700-132">Plage d’adresses de sous-réseau</span><span class="sxs-lookup"><span data-stu-id="47700-132">Subnet address range</span></span>|<span data-ttu-id="47700-133">10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="47700-133">10.0.0.0/24</span></span>|
    |<span data-ttu-id="47700-134">Groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="47700-134">Resource group</span></span>|<span data-ttu-id="47700-135">Laissez l’option **Créer** activée, puis entrez **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="47700-135">Leave **Create new** selected, and then enter **myResourceGroup**.</span></span>|
    |<span data-ttu-id="47700-136">Abonnement et emplacement</span><span class="sxs-lookup"><span data-stu-id="47700-136">Subscription and location</span></span>|<span data-ttu-id="47700-137">Sélectionnez votre abonnement et son emplacement.</span><span class="sxs-lookup"><span data-stu-id="47700-137">Select your subscription and location.</span></span>

    <span data-ttu-id="47700-138">Si vous êtes tooAzure nouvelle, en savoir plus sur [groupes de ressources](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [abonnements](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), et [emplacements](https://azure.microsoft.com/regions) (également appelée tooas *régions*).</span><span class="sxs-lookup"><span data-stu-id="47700-138">If you're new tooAzure, learn more about [resource groups](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscriptions](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), and [locations](https://azure.microsoft.com/regions) (also referred tooas *regions*).</span></span>
4. <span data-ttu-id="47700-139">Dans le portail hello, vous pouvez créer un seul sous-réseau lorsque vous créez un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="47700-139">In hello portal, you can create only one subnet when you create a virtual network.</span></span> <span data-ttu-id="47700-140">Dans ce didacticiel, vous créez un deuxième sous-réseau après avoir créé le réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="47700-140">In this tutorial, you create a second subnet after you create hello virtual network.</span></span> <span data-ttu-id="47700-141">Vous pouvez créer ultérieurement les ressources accessibles sur Internet dans hello **Public** sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="47700-141">You might later create Internet-accessible resources in hello **Public** subnet.</span></span> <span data-ttu-id="47700-142">Vous pouvez également créer des ressources qui ne sont pas accessibles à partir de hello Internet Bonjour **privé** sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="47700-142">You also might create resources that aren't accessible from hello Internet in hello **Private** subnet.</span></span> <span data-ttu-id="47700-143">toocreate hello deuxième sous-réseau, entrez **myVnet** Bonjour **recherche les ressources** zone en hello haut hello.</span><span class="sxs-lookup"><span data-stu-id="47700-143">toocreate hello second subnet, enter **myVnet** in hello **Search resources** box at hello top of hello page.</span></span> <span data-ttu-id="47700-144">Cliquez sur **myVnet** lorsqu’il apparaît dans les résultats de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="47700-144">Click **myVnet** when it appears in hello search results.</span></span>
5. <span data-ttu-id="47700-145">Cliquez sur **sous-réseaux** (Bonjour **paramètres** section) sur hello **créer un réseau virtuel (classiques)** panneau s’affiche.</span><span class="sxs-lookup"><span data-stu-id="47700-145">Click **Subnets** (in hello **SETTINGS** section) on hello **Create virtual network (classic)** blade that appears.</span></span>
6. <span data-ttu-id="47700-146">Cliquez sur **+ ajouter** sur hello **myVnet - sous-réseaux** panneau s’affiche.</span><span class="sxs-lookup"><span data-stu-id="47700-146">Click **+Add** on hello **myVnet - Subnets** blade that appears.</span></span>
7. <span data-ttu-id="47700-147">Entrez **privé** pour **nom** sur hello **ajouter un sous-réseau** panneau.</span><span class="sxs-lookup"><span data-stu-id="47700-147">Enter **Private** for **Name** on hello **Add subnet** blade.</span></span> <span data-ttu-id="47700-148">Pour **Plage d’adresses**, entrez **10.0.1.0/24**.</span><span class="sxs-lookup"><span data-stu-id="47700-148">Enter **10.0.1.0/24** for **Address range**.</span></span>  <span data-ttu-id="47700-149">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="47700-149">Click **OK**.</span></span>
8. <span data-ttu-id="47700-150">Sur hello **myVnet - sous-réseaux** panneau, vous pouvez voir hello **Public** et **privé** sous-réseaux que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="47700-150">On hello **myVnet - Subnets** blade, you can see hello **Public** and **Private** subnets that you created.</span></span>
9. <span data-ttu-id="47700-151">**Facultatif**: lorsque vous avez terminé ce didacticiel, vous pourriez ressources hello toodelete que vous avez créé, afin que vous ne subissez des frais d’utilisation :</span><span class="sxs-lookup"><span data-stu-id="47700-151">**Optional**: When you finish this tutorial, you might want toodelete hello resources that you created, so that you don't incur usage charges:</span></span>
    - <span data-ttu-id="47700-152">Cliquez sur **vue d’ensemble** sur hello **myVnet** panneau.</span><span class="sxs-lookup"><span data-stu-id="47700-152">Click **Overview** on hello **myVnet** blade.</span></span>
    - <span data-ttu-id="47700-153">Cliquez sur hello **supprimer** icône sur hello **myVnet** panneau.</span><span class="sxs-lookup"><span data-stu-id="47700-153">Click hello **Delete** icon on hello **myVnet** blade.</span></span>
    - <span data-ttu-id="47700-154">suppression de hello tooconfirm, cliquez sur **Oui** Bonjour **réseau virtuel de suppression** boîte.</span><span class="sxs-lookup"><span data-stu-id="47700-154">tooconfirm hello deletion, click **Yes** in hello **Delete virtual network** box.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="47700-155">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="47700-155">Azure CLI</span></span>

1. <span data-ttu-id="47700-156">Vous pouvez soit [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), ou utilisez hello CLI dans hello Azure Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="47700-156">You can either [install and configure hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), or use hello CLI within hello Azure Cloud Shell.</span></span> <span data-ttu-id="47700-157">Bonjour Azure Cloud Shell est un interpréteur de commandes Bash gratuit que vous pouvez exécuter directement à l’intérieur hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="47700-157">hello Azure Cloud Shell is a free Bash shell that you can run directly within hello Azure portal.</span></span> <span data-ttu-id="47700-158">Il a hello CLI d’Azure préinstallé et configuré toouse avec votre compte.</span><span class="sxs-lookup"><span data-stu-id="47700-158">It has hello Azure CLI preinstalled and configured toouse with your account.</span></span> <span data-ttu-id="47700-159">aide tooget pour les commandes CLI, tapez `azure <command> --help`.</span><span class="sxs-lookup"><span data-stu-id="47700-159">tooget help for CLI commands, type `azure <command> --help`.</span></span> 
2. <span data-ttu-id="47700-160">Dans une session CLI, connectez-vous tooAzure avec la commande hello qui suit.</span><span class="sxs-lookup"><span data-stu-id="47700-160">In a CLI session, log in tooAzure with hello command that follows.</span></span> <span data-ttu-id="47700-161">Si vous cliquez sur **essayez-la** dans la zone de hello ci-dessous, un environnement de Cloud s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="47700-161">If you click **Try it** in hello box below, a Cloud Shell opens.</span></span> <span data-ttu-id="47700-162">Vous pouvez vous connecter tooyour abonnement Azure, sans entrer de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="47700-162">You can log in tooyour Azure subscription, without entering hello following command:</span></span>

    ```azurecli-interactive
    azure login
    ```

3. <span data-ttu-id="47700-163">hello tooensure CLI est en mode de gestion de Service, entrez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="47700-163">tooensure hello CLI is in Service Management mode, enter hello following command:</span></span>

    ```azurecli-interactive
    azure config mode asm
    ```

4. <span data-ttu-id="47700-164">Créez un réseau virtuel avec un sous-réseau privé :</span><span class="sxs-lookup"><span data-stu-id="47700-164">Create a virtual network with a private subnet:</span></span>

    ```azurecli-interactive
    azure network vnet create --vnet myVnet --address-space 10.0.0.0 --cidr 16  --subnet-name Private --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --location "East US"
    ```

5. <span data-ttu-id="47700-165">Créer un sous-réseau public dans le réseau virtuel de hello :</span><span class="sxs-lookup"><span data-stu-id="47700-165">Create a public subnet within hello virtual network:</span></span>

    ```azurecli-interactive
    azure network vnet subnet create --name Public --vnet-name myVnet --address-prefix 10.0.1.0/24
    ```    
    
6. <span data-ttu-id="47700-166">Examiner le réseau virtuel hello et sous-réseaux :</span><span class="sxs-lookup"><span data-stu-id="47700-166">Review hello virtual network and subnets:</span></span>

    ```azurecli-interactive
    azure network vnet show --vnet myVnet
    ```

7. <span data-ttu-id="47700-167">**Facultatif**: vous pourriez ressources hello toodelete que vous avez créé lorsque vous avez terminé ce didacticiel, afin que vous ne subissez des frais d’utilisation :</span><span class="sxs-lookup"><span data-stu-id="47700-167">**Optional**: You might want toodelete hello resources that you created when you finish this tutorial, so that you don't incur usage charges:</span></span>

    ```azurecli-interactive
    azure network vnet delete --vnet myVnet --quiet
    ```

> [!NOTE]
> <span data-ttu-id="47700-168">Si vous ne pouvez pas spécifier un toocreate de groupe de ressources un réseau virtuel (classique) à l’aide de hello CLI, Azure crée le réseau virtuel de hello dans un groupe de ressources nommé *réseau par défaut*.</span><span class="sxs-lookup"><span data-stu-id="47700-168">Though you can't specify a resource group toocreate a virtual network (classic) in using hello CLI, Azure creates hello virtual network in a resource group named *Default-Networking*.</span></span>

## <a name="powershell"></a><span data-ttu-id="47700-169">PowerShell</span><span class="sxs-lookup"><span data-stu-id="47700-169">PowerShell</span></span>

1. <span data-ttu-id="47700-170">Installer la version la plus récente de hello PowerShell hello [Azure](https://www.powershellgallery.com/packages/Azure) module.</span><span class="sxs-lookup"><span data-stu-id="47700-170">Install hello latest version of hello PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) module.</span></span> <span data-ttu-id="47700-171">Si vous êtes nouveau tooAzure PowerShell, consultez [vue d’ensemble d’Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="47700-171">If you're new tooAzure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="47700-172">Démarrez une session PowerShell.</span><span class="sxs-lookup"><span data-stu-id="47700-172">Start a PowerShell session.</span></span>
3. <span data-ttu-id="47700-173">Dans PowerShell, connectez-vous tooAzure en entrant hello `Add-AzureAccount` commande.</span><span class="sxs-lookup"><span data-stu-id="47700-173">In PowerShell, log in tooAzure by entering hello `Add-AzureAccount` command.</span></span>
4. <span data-ttu-id="47700-174">Modifier hello suivants chemin d’accès et nom de fichier, comme il convient, puis exporter votre fichier de configuration de réseau existant :</span><span class="sxs-lookup"><span data-stu-id="47700-174">Change hello following path and filename, as appropriate, then export your existing network configuration file:</span></span>

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
    ```

5. <span data-ttu-id="47700-175">toocreate un réseau virtuel avec les sous-réseaux privés et publics, utilisez n’importe quel hello de tooadd de l’éditeur de texte **VirtualNetworkSite** élément qui suit le fichier de configuration réseau toohello.</span><span class="sxs-lookup"><span data-stu-id="47700-175">toocreate a virtual network with public and private subnets, use any text editor tooadd hello **VirtualNetworkSite** element that follows toohello network configuration file.</span></span>

    ```xml
    <VirtualNetworkSite name="myVnet" Location="East US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Private">
            <AddressPrefix>10.0.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Public">
            <AddressPrefix>10.0.1.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    ```

    <span data-ttu-id="47700-176">Hello révision complète [schéma de fichier de configuration réseau](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="47700-176">Review hello full [network configuration file schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>

6. <span data-ttu-id="47700-177">Importez le fichier de configuration de réseau hello :</span><span class="sxs-lookup"><span data-stu-id="47700-177">Import hello network configuration file:</span></span>

    ```powershell
    Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
    ```

    > [!WARNING]
    > <span data-ttu-id="47700-178">Importation d’un fichier de configuration de réseau modifié peut entraîner des modifications tooexisting les réseaux virtuels (classiques) dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="47700-178">Importing a changed network configuration file can cause changes tooexisting virtual networks (classic) in your subscription.</span></span> <span data-ttu-id="47700-179">Assurez-vous que vous ajoutez uniquement réseau virtuel de hello précédente et que vous ne modifiez ou supprimez des réseaux virtuels existants de votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="47700-179">Ensure you only add hello previous virtual network and that you don't change or remove any existing virtual networks from your subscription.</span></span> 

7. <span data-ttu-id="47700-180">Examiner le réseau virtuel hello et sous-réseaux :</span><span class="sxs-lookup"><span data-stu-id="47700-180">Review hello virtual network and subnets:</span></span>

    ```powershell
    Get-AzureVNetSite -VNetName "myVnet"
    ```

8. <span data-ttu-id="47700-181">**Facultatif**: vous pourriez ressources hello toodelete que vous avez créé lorsque vous avez terminé ce didacticiel, afin que vous ne subissez des frais d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="47700-181">**Optional**: You might want toodelete hello resources that you created when you finish this tutorial, so that you don't incur usage charges.</span></span> <span data-ttu-id="47700-182">toodelete hello réseau virtuel, complète étapes 4 à 6, cette hello suppression temps **VirtualNetworkSite** élément ajouté à l’étape 5.</span><span class="sxs-lookup"><span data-stu-id="47700-182">toodelete hello virtual network, complete steps 4-6 again, this time removing hello **VirtualNetworkSite** element you added in step 5.</span></span>
 
> [!NOTE]
> <span data-ttu-id="47700-183">Si vous ne pouvez pas spécifier un toocreate de groupe de ressources un réseau virtuel (classique) dans l’aide de PowerShell, Azure crée le réseau virtuel de hello dans un groupe de ressources nommé *réseau par défaut*.</span><span class="sxs-lookup"><span data-stu-id="47700-183">Though you can't specify a resource group toocreate a virtual network (classic) in using PowerShell, Azure creates hello virtual network in a resource group named *Default-Networking*.</span></span>

---

## <a name="next-steps"></a><span data-ttu-id="47700-184">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="47700-184">Next steps</span></span>

- <span data-ttu-id="47700-185">toolearn sur tous les paramètres réseau virtuel et sous-réseau, consultez [gérer les réseaux virtuels](virtual-network-manage-network.md) et [gérer les sous-réseaux du réseau virtuel](virtual-network-manage-subnet.md).</span><span class="sxs-lookup"><span data-stu-id="47700-185">toolearn about all virtual network and subnet settings, see [Manage virtual networks](virtual-network-manage-network.md) and [Manage virtual network subnets](virtual-network-manage-subnet.md).</span></span> <span data-ttu-id="47700-186">Vous disposez des options différentes pour l’utilisation de réseaux virtuels et sous-réseaux dans les exigences de la toomeet d’environnement de production différent.</span><span class="sxs-lookup"><span data-stu-id="47700-186">You have various options for using virtual networks and subnets in a production environment toomeet different requirements.</span></span>
- <span data-ttu-id="47700-187">toofilter entrant et sortant du trafic de sous-réseau, créer et appliquer [groupes de sécurité réseau](virtual-networks-nsg.md) toosubnets.</span><span class="sxs-lookup"><span data-stu-id="47700-187">toofilter inbound and outbound subnet traffic, create and apply [network security groups](virtual-networks-nsg.md) toosubnets.</span></span>
- <span data-ttu-id="47700-188">Créer un [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ou un [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) machine virtuelle, puis connectez-la tooan de réseau virtuel existant.</span><span class="sxs-lookup"><span data-stu-id="47700-188">Create a [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) or a [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) virtual machine, and then connect it tooan existing virtual network.</span></span>
- <span data-ttu-id="47700-189">tooconnect deux des réseaux virtuels dans hello même emplacement, créez un [réseau virtuel d’homologation](create-peering-different-deployment-models.md) entre les réseaux virtuels hello.</span><span class="sxs-lookup"><span data-stu-id="47700-189">tooconnect two virtual networks in hello same Azure location, create a  [virtual network peering](create-peering-different-deployment-models.md) between hello virtual networks.</span></span> <span data-ttu-id="47700-190">Vous pouvez homologue d’un réseau virtuel de réseau virtuel (Resource Manager) tooa (classique), mais vous ne pouvez pas créer une homologation entre deux réseaux virtuels (classiques).</span><span class="sxs-lookup"><span data-stu-id="47700-190">You can peer a virtual network (Resource Manager) tooa virtual network (classic), but you cannot create a peering between two virtual networks (classic).</span></span>
- <span data-ttu-id="47700-191">Connecter le réseau local de hello réseau virtuel tooan à l’aide un [passerelle VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ou [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) circuit.</span><span class="sxs-lookup"><span data-stu-id="47700-191">Connect hello virtual network tooan on-premises network by using a [VPN Gateway](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) or [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) circuit.</span></span>
