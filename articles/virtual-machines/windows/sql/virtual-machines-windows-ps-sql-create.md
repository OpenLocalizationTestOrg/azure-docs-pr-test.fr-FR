---
title: "Créer une machine virtuelle SQL Server dans Azure PowerShell (Resource Manager) | Microsoft Docs"
description: "Fournit une procédure et des scripts PowerShell pour la création d’une machine virtuelle Azure à l’aide des images de la galerie de machines virtuelles SQL Server."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 98d50dd8-48ad-444f-9031-5378d8270d7b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/17/2017
ms.author: jroth
ms.openlocfilehash: aa90a1d017af5f477407ab33f0580904472f412b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-resource-manager"></a><span data-ttu-id="7e274-103">Approvisionner une machine virtuelle SQL Server à l’aide d’Azure PowerShell (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="7e274-103">Provision a SQL Server virtual machine using Azure PowerShell (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7e274-104">Portail</span><span class="sxs-lookup"><span data-stu-id="7e274-104">Portal</span></span>](virtual-machines-windows-portal-sql-server-provision.md)
> * [<span data-ttu-id="7e274-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7e274-105">PowerShell</span></span>](virtual-machines-windows-ps-sql-create.md)
>
>

## <a name="overview"></a><span data-ttu-id="7e274-106">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="7e274-106">Overview</span></span>
<span data-ttu-id="7e274-107">Ce didacticiel vous montre comment créer une machine virtuelle Azure à l’aide du modèle de déploiement **Azure Resource Manager** et d’applets de commande Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7e274-107">This tutorial shows you how to create a single Azure virtual machine using the **Azure Resource Manager** deployment model using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="7e274-108">Dans ce didacticiel, nous allons créer une machine virtuelle à l’aide d’un lecteur de disque à partir d’une image dans la galerie SQL.</span><span class="sxs-lookup"><span data-stu-id="7e274-108">In this tutorial, we will create a single virtual machine using a single disk drive from an image in the SQL Gallery.</span></span> <span data-ttu-id="7e274-109">Nous allons créer des fournisseurs pour les ressources de stockage, de réseau et de calcul qui seront utilisées par la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7e274-109">We will create new providers for the storage, network, and compute resources that will be used by the virtual machine.</span></span> <span data-ttu-id="7e274-110">Si vous avez déjà des fournisseurs pour ces ressources, vous pouvez les utiliser.</span><span class="sxs-lookup"><span data-stu-id="7e274-110">If you have existing providers for any of these resources, you can use those providers instead.</span></span>

<span data-ttu-id="7e274-111">Si vous avez besoin de la version classique de cette rubrique, consultez la page [Approvisionner une machine virtuelle SQL Server à l’aide d’Azure PowerShell (Classic)](../classic/ps-sql-create.md).</span><span class="sxs-lookup"><span data-stu-id="7e274-111">If you need the classic version of this topic, see [Provision a SQL Server virtual machine using Azure PowerShell Classic](../classic/ps-sql-create.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e274-112">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="7e274-112">Prerequisites</span></span>
<span data-ttu-id="7e274-113">Pour ce didacticiel, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="7e274-113">For this tutorial you'll need:</span></span>

* <span data-ttu-id="7e274-114">Un compte Azure et un abonnement, avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="7e274-114">An Azure account and subscription before you start.</span></span> <span data-ttu-id="7e274-115">Si vous n’en avez pas, inscrivez-vous pour un [essai gratuit](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7e274-115">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="7e274-116">[Azure PowerShell](/powershell/azure/overview)1.4.0 ou version ultérieure (ce didacticiel a été écrit avec la version 1.5.0).</span><span class="sxs-lookup"><span data-stu-id="7e274-116">[Azure PowerShell)](/powershell/azure/overview), minimum version of 1.4.0 or later (this tutorial written using version 1.5.0).</span></span>
  * <span data-ttu-id="7e274-117">Pour récupérer votre version, tapez **Get-Module Azure -ListAvailable**.</span><span class="sxs-lookup"><span data-stu-id="7e274-117">To retrieve your version, type **Get-Module Azure -ListAvailable**.</span></span>

## <a name="configure-your-subscription"></a><span data-ttu-id="7e274-118">Configurer votre abonnement</span><span class="sxs-lookup"><span data-stu-id="7e274-118">Configure your subscription</span></span>
<span data-ttu-id="7e274-119">Ouvrez Windows PowerShell et accédez à votre compte Azure en exécutant l’applet de commande suivante.</span><span class="sxs-lookup"><span data-stu-id="7e274-119">Open Windows PowerShell and establish access to your Azure account by running the following cmdlet.</span></span> <span data-ttu-id="7e274-120">Un écran de connexion vous invite à entrer vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="7e274-120">You will be presented with a sign in screen to enter your credentials.</span></span> <span data-ttu-id="7e274-121">Utilisez l'adresse électronique et le mot de passe que vous utilisez pour vous connecter au portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7e274-121">Use the same email and password that you use to sign in to the Azure portal.</span></span>

    Add-AzureRmAccount

<span data-ttu-id="7e274-122">Une fois que vous êtes connecté, l’écran affiche plusieurs informations, dont l’ID d’abonnement avec lequel vous vous êtes identifié.</span><span class="sxs-lookup"><span data-stu-id="7e274-122">After successfully signing in you will see some information on screen that includes the SubscriptionId with which you signed in.</span></span> <span data-ttu-id="7e274-123">Il s’agit de l’abonnement dans lequel les ressources de ce didacticiel vont être créées, sauf si vous en changez.</span><span class="sxs-lookup"><span data-stu-id="7e274-123">This is the subscription in which the resources for this tutorial will be created unless you change to a different subscription.</span></span> <span data-ttu-id="7e274-124">Si vous avez plusieurs ID d’abonnement, exécutez l’applet de commande suivante pour renvoyer la liste de tous vos ID d’abonnement :</span><span class="sxs-lookup"><span data-stu-id="7e274-124">If you have multiple SubscriptionIds, run the following cmdlet to return a list of all of your SubscriptionIds:</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="7e274-125">Pour basculer vers un autre ID d’abonnement, exécutez l’applet de commande avec l’ID d’abonnement souhaité.</span><span class="sxs-lookup"><span data-stu-id="7e274-125">To change to another SubscriptionID, run the following cmdlet with your desired SubscriptionId.</span></span>

    Select-AzureRmSubscription -SubscriptionId xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

## <a name="define-image-variables"></a><span data-ttu-id="7e274-126">Définir des variables d’image</span><span class="sxs-lookup"><span data-stu-id="7e274-126">Define image variables</span></span>
<span data-ttu-id="7e274-127">Pour simplifier l’utilisation et la compréhension du script complet de ce didacticiel, nous allons commencer par définir plusieurs variables.</span><span class="sxs-lookup"><span data-stu-id="7e274-127">To simplify usability and understanding of the completed script from this tutorial, we will start by defining a number of variables.</span></span> <span data-ttu-id="7e274-128">Modifiez les valeurs des paramètres comme vous le souhaitez, mais sachez que des restrictions s’appliquent à la longueur des noms et aux caractères spéciaux en cas de modification des valeurs fournies.</span><span class="sxs-lookup"><span data-stu-id="7e274-128">Change the parameter values as you see fit, but beware of naming restrictions related to name lengths and special characters when modifying the values provided.</span></span>

### <a name="location-and-resource-group"></a><span data-ttu-id="7e274-129">Emplacement et groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="7e274-129">Location and Resource Group</span></span>
<span data-ttu-id="7e274-130">Utilisez deux variables pour définir la région des données et le groupe de ressources dans lequel vous allez créer les autres ressources de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7e274-130">Use two variables to define the data region and the resource group into which you will create the other resources for the virtual machine.</span></span>

<span data-ttu-id="7e274-131">Apportez les modifications souhaitées, puis exécutez les applets de commande suivantes pour initialiser ces variables.</span><span class="sxs-lookup"><span data-stu-id="7e274-131">Modify as desired and then execute the following cmdlets to initialize these variables.</span></span>

    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"

### <a name="storage-properties"></a><span data-ttu-id="7e274-132">Propriétés de stockage</span><span class="sxs-lookup"><span data-stu-id="7e274-132">Storage properties</span></span>
<span data-ttu-id="7e274-133">Utilisez les variables suivantes pour définir le compte de stockage et le type de stockage à utiliser par la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7e274-133">Use the following variables to define the storage account and the type of storage to be used by the virtual machine.</span></span>

<span data-ttu-id="7e274-134">Apportez les modifications souhaitées, puis exécutez l’applet de commande suivante pour initialiser ces variables.</span><span class="sxs-lookup"><span data-stu-id="7e274-134">Modify as desired and then execute the following cmdlet to initialize these variables.</span></span> <span data-ttu-id="7e274-135">Notez que, dans cet exemple, nous utilisons [Premium Storage](../../../storage/common/storage-premium-storage.md), qui est recommandé pour les charges de travail de production.</span><span class="sxs-lookup"><span data-stu-id="7e274-135">Note that in this example, we are using [Premium Storage](../../../storage/common/storage-premium-storage.md), which is recommended for production workloads.</span></span> <span data-ttu-id="7e274-136">Pour plus d’informations et d’autres recommandations, consultez [Meilleures pratiques relatives aux performances de SQL Server dans Azure Virtual Machines](virtual-machines-windows-sql-performance.md).</span><span class="sxs-lookup"><span data-stu-id="7e274-136">For details on this guidance and other recommendations, see [Performance best practices for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md).</span></span>

    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

### <a name="network-properties"></a><span data-ttu-id="7e274-137">Propriétés du réseau</span><span class="sxs-lookup"><span data-stu-id="7e274-137">Network properties</span></span>
<span data-ttu-id="7e274-138">Utilisez les variables suivantes pour définir l’interface réseau, la méthode d’allocation TCP/IP, le nom du réseau virtuel, le nom du sous-réseau virtuel, la plage d’adresses IP du réseau virtuel, la plage d’adresses IP du sous-réseau et le libellé du nom de domaine public à utiliser par le réseau dans la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7e274-138">Use the following variables to define the network interface, the TCP/IP allocation method, the virtual network name, the virtual subnet name, the range of IP addresses for the virtual network, the range of IP addresses for the subnet, and the public domain name label to be used by the network in the virtual machine.</span></span>

<span data-ttu-id="7e274-139">Apportez les modifications souhaitées, puis exécutez l’applet de commande suivante pour initialiser ces variables.</span><span class="sxs-lookup"><span data-stu-id="7e274-139">Modify as desired and then execute the following cmdlet to initialize these variables.</span></span>

    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $TCPIPAllocationMethod = "Dynamic"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $DomainName = "sqlvm1"

### <a name="virtual-machine-properties"></a><span data-ttu-id="7e274-140">Propriétés de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="7e274-140">Virtual machine properties</span></span>
<span data-ttu-id="7e274-141">Utilisez les variables suivantes pour définir le nom de la machine virtuelle, le nom de l’ordinateur, la taille de la machine virtuelle et le nom du disque du système d’exploitation de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7e274-141">Use the following variables to define the virtual machine name, the computer name, the virtual machine size, and the operating system disk name for the virtual machine.</span></span>

<span data-ttu-id="7e274-142">Apportez les modifications souhaitées, puis exécutez l’applet de commande suivante pour initialiser ces variables.</span><span class="sxs-lookup"><span data-stu-id="7e274-142">Modify as desired and then execute the following cmdlet to initialize these variables.</span></span>

    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

### <a name="image-properties"></a><span data-ttu-id="7e274-143">Propriétés de l’image</span><span class="sxs-lookup"><span data-stu-id="7e274-143">Image properties</span></span>
<span data-ttu-id="7e274-144">Utilisez les variables suivantes pour définir l’image à utiliser pour la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7e274-144">Use the following variables to define the image to use for the virtual machine.</span></span> <span data-ttu-id="7e274-145">Dans cet exemple, l’image d’évaluation SQL Server 2016 Enterprise est utilisée.</span><span class="sxs-lookup"><span data-stu-id="7e274-145">In this example, the SQL Server 2016 Enterprise image is used.</span></span>

<span data-ttu-id="7e274-146">Apportez les modifications souhaitées, puis exécutez l’applet de commande suivante pour initialiser ces variables.</span><span class="sxs-lookup"><span data-stu-id="7e274-146">Modify as desired and then execute the following cmdlet to initialize these variables.</span></span>

    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

<span data-ttu-id="7e274-147">Notez que vous pouvez obtenir la liste complète des images SQL Server avec la commande Get-AzureRmVMImageOffer :</span><span class="sxs-lookup"><span data-stu-id="7e274-147">Note that you can get a full list of SQL Server image offerings with the Get-AzureRmVMImageOffer command:</span></span>

    Get-AzureRmVMImageOffer -Location 'East US' -Publisher 'MicrosoftSQLServer'

<span data-ttu-id="7e274-148">Et vous pouvez voir les références SKU disponibles pour une offre avec la commande Get-AzureRmVMImageSku.</span><span class="sxs-lookup"><span data-stu-id="7e274-148">And you can see the Skus available for an offering with the Get-AzureRmVMImageSku command.</span></span> <span data-ttu-id="7e274-149">La commande suivante affiche toutes les références disponibles pour l’offre **SQL2014SP1-WS2012R2** .</span><span class="sxs-lookup"><span data-stu-id="7e274-149">The following command shows all Skus available for the **SQL2014SP1-WS2012R2** offer.</span></span>

    Get-AzureRmVMImageSku -Location 'East US' -Publisher 'MicrosoftSQLServer' -Offer 'SQL2014SP1-WS2012R2' | Select Skus

## <a name="create-a-resource-group"></a><span data-ttu-id="7e274-150">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="7e274-150">Create a resource group</span></span>
<span data-ttu-id="7e274-151">Avec le modèle de déploiement Resource Manager, le premier objet que vous créez est le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="7e274-151">With the Resource Manager deployment model, the first object that you create is the resource group.</span></span> <span data-ttu-id="7e274-152">Nous allons utiliser l’applet de commande [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) pour créer un groupe de ressources Azure et ses ressources avec le nom et l’emplacement du groupe de ressources définis par les variables que vous avez déjà initialisées.</span><span class="sxs-lookup"><span data-stu-id="7e274-152">We will use the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet to create an Azure resource group and its resources with the resource group name and location defined by the variables that you previously initialized.</span></span>

<span data-ttu-id="7e274-153">Exécutez l’applet de commande suivante pour créer votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="7e274-153">Execute the following cmdlet to create your new resource group.</span></span>

    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

## <a name="create-a-storage-account"></a><span data-ttu-id="7e274-154">Créer un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="7e274-154">Create a storage account</span></span>
<span data-ttu-id="7e274-155">La machine virtuelle nécessite des ressources de stockage pour le disque du système d’exploitation ainsi que pour les données et fichiers journaux de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="7e274-155">The virtual machine requires storage resources for the operating system disk and for the SQL Server data and log files.</span></span> <span data-ttu-id="7e274-156">Pour plus de simplicité, nous allons créer un seul disque pour les deux.</span><span class="sxs-lookup"><span data-stu-id="7e274-156">For simplicity, we will create a single disk for both.</span></span> <span data-ttu-id="7e274-157">Vous pouvez attacher des disques supplémentaires ultérieurement, à l’aide de l’applet de commande [Add-Azure Disk](/powershell/module/azure/add-azuredisk) , pour placer vos données et vos fichiers journaux SQL Server sur des disques dédiés.</span><span class="sxs-lookup"><span data-stu-id="7e274-157">You can attach additional disks later using the [Add-Azure Disk](/powershell/module/azure/add-azuredisk) cmdlet in order to place your SQL Server data and log files on dedicated disks.</span></span> <span data-ttu-id="7e274-158">Nous allons utiliser l’applet de commande [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) pour créer un compte de stockage standard dans votre nouveau groupe de ressources, avec le nom du compte de stockage, le nom de référence du stockage et l’emplacement définis à l’aide des variables que vous avez déjà initialisées.</span><span class="sxs-lookup"><span data-stu-id="7e274-158">We will use the [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet to create a standard storage account in your new resource group and with the storage account name, storage Sku name, and location defined using the variables that you previously initialized.</span></span>

<span data-ttu-id="7e274-159">Exécutez l’applet de commande suivante pour créer votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="7e274-159">Execute the following cmdlet to create your new storage account.</span></span>

    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

## <a name="create-network-resources"></a><span data-ttu-id="7e274-160">Créer des ressources réseau</span><span class="sxs-lookup"><span data-stu-id="7e274-160">Create network resources</span></span>
<span data-ttu-id="7e274-161">La machine virtuelle requiert plusieurs ressources réseau pour la connectivité réseau.</span><span class="sxs-lookup"><span data-stu-id="7e274-161">The virtual machine requires a number of network resources for network connectivity.</span></span>

* <span data-ttu-id="7e274-162">Chaque machine virtuelle requiert un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="7e274-162">Each virtual machine requires a virtual network.</span></span>
* <span data-ttu-id="7e274-163">Un réseau virtuel doit avoir au moins un sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="7e274-163">A virtual network must have at least one subnet defined.</span></span>
* <span data-ttu-id="7e274-164">Une interface réseau doit être définie avec une adresse IP privée ou publique.</span><span class="sxs-lookup"><span data-stu-id="7e274-164">A network interface must be defined with either a public or a private IP address.</span></span>

### <a name="create-a-virtual-network-subnet-configuration"></a><span data-ttu-id="7e274-165">Créer une configuration de sous-réseau de réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="7e274-165">Create a virtual network subnet configuration</span></span>
<span data-ttu-id="7e274-166">Nous allons commencer par créer une configuration de sous-réseau pour notre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="7e274-166">We will start by creating a subnet configuration for our virtual network.</span></span> <span data-ttu-id="7e274-167">Dans notre didacticiel, nous allons créer un sous-réseau par défaut à l’aide de l’applet de commande [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) .</span><span class="sxs-lookup"><span data-stu-id="7e274-167">For our tutorial, we will create a default subnet using the [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) cmdlet.</span></span> <span data-ttu-id="7e274-168">Nous allons créer notre configuration de sous-réseau de réseau virtuel avec le nom et le préfixe d’adresse définis à l’aide des variables déjà initialisées.</span><span class="sxs-lookup"><span data-stu-id="7e274-168">We will create our virtual network subnet configuration with the subnet name and address prefix defined using the variables that you previously initialized.</span></span>

> [!NOTE]
> <span data-ttu-id="7e274-169">Vous pouvez définir des propriétés supplémentaires dans la configuration de sous-réseau de réseau virtuel à l’aide de cette applet de commande, mais cela sort du cadre de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="7e274-169">You can define additional properties of the virtual network subnet configuration using this cmdlet, but that is beyond the scope of this tutorial.</span></span>
>
>

<span data-ttu-id="7e274-170">Exécutez l’applet de commande suivante pour créer la configuration de votre sous-réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="7e274-170">Execute the following cmdlet to create your virtual subnet configuration.</span></span>

    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix

### <a name="create-a-virtual-network"></a><span data-ttu-id="7e274-171">Créez un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="7e274-171">Create a virtual network</span></span>
<span data-ttu-id="7e274-172">Ensuite, nous allons créer notre réseau virtuel à l’aide de l’applet de commande [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) .</span><span class="sxs-lookup"><span data-stu-id="7e274-172">Next, we will create our virtual network using the [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) cmdlet.</span></span> <span data-ttu-id="7e274-173">Nous allons créer notre réseau virtuel dans votre nouveau groupe de ressources, avec le nom, l’emplacement et le préfixe d’adresse définis avec les variables que vous avez déjà initialisées, et à l’aide de la configuration de sous-réseau définie à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="7e274-173">We will create our virtual network in your new resource group, with the name, location, and address prefix defined using the variables that you previously initialized, and using the subnet configuration that you defined in the previous step.</span></span>

<span data-ttu-id="7e274-174">Exécutez l’applet de commande suivante pour créer votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="7e274-174">Execute the following cmdlet to create your virtual network.</span></span>

    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig

### <a name="create-the-public-ip-address"></a><span data-ttu-id="7e274-175">Créer une adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="7e274-175">Create the public IP address</span></span>
<span data-ttu-id="7e274-176">Maintenant que nous avons défini notre réseau virtuel, nous devons configurer une adresse IP pour la connectivité à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7e274-176">Now that we have our virtual network defined, we need to configure an IP address for connectivity to the virtual machine.</span></span> <span data-ttu-id="7e274-177">Dans ce didacticiel, nous allons créer une adresse IP publique à l’aide de l’adressage IP dynamique pour la connectivité Internet.</span><span class="sxs-lookup"><span data-stu-id="7e274-177">For this tutorial, we will create a public IP address using dynamic IP addressing to support Internet connectivity.</span></span> <span data-ttu-id="7e274-178">Nous allons utiliser l’applet de commande [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) pour créer l’adresse IP publique dans le groupe de ressources déjà créé, avec le nom, l’emplacement, la méthode d’allocation et le libellé du nom de domaine DNS définis à l’aide des variables que vous avez déjà initialisées.</span><span class="sxs-lookup"><span data-stu-id="7e274-178">We will use the [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) cmdlet to create the public IP address in the resource group created prevously and with the name, location, allocation method, and DNS domain name label defined using the variables that you previously initialized.</span></span>

> [!NOTE]
> <span data-ttu-id="7e274-179">Vous pouvez définir des propriétés supplémentaires de l’adresse IP publique à l’aide de cette applet de commande, mais cela sort du cadre de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="7e274-179">You can define additional properties of the public IP address using this cmdlet, but that is beyond the scope of this initial tutorial.</span></span> <span data-ttu-id="7e274-180">Vous pouvez également créer une adresse privée ou une adresse avec une adresse statique, mais cela sort du cadre de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="7e274-180">You could also create a private address or an address with a static address, but that is also beyond the scope of this tutorial.</span></span>
>
>

<span data-ttu-id="7e274-181">Exécutez l’applet de commande suivante pour créer votre adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="7e274-181">Execute the following cmdlet to create your public IP address.</span></span>

    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName

### <a name="create-the-network-interface"></a><span data-ttu-id="7e274-182">Créer l’interface réseau</span><span class="sxs-lookup"><span data-stu-id="7e274-182">Create the network interface</span></span>
<span data-ttu-id="7e274-183">Nous sommes maintenant prêts à créer l’interface réseau que notre machine virtuelle utilisera.</span><span class="sxs-lookup"><span data-stu-id="7e274-183">We are now ready to create the network interface that our virtual machine will use.</span></span> <span data-ttu-id="7e274-184">Nous allons utiliser l’applet de commande [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) pour créer notre interface réseau dans le groupe de ressources déjà créé, et avec le nom, l’emplacement, le sous-réseau et l’adresse IP publique définis auparavant.</span><span class="sxs-lookup"><span data-stu-id="7e274-184">We will use the [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) cmdlet to create our network interface in the resource group created earlier and with the name, location, subnet and public IP address previously defined.</span></span>

<span data-ttu-id="7e274-185">Exécutez l’applet de commande suivante pour créer votre interface réseau.</span><span class="sxs-lookup"><span data-stu-id="7e274-185">Execute the following cmdlet to create your network interface.</span></span>

    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

## <a name="configure-a-vm-object"></a><span data-ttu-id="7e274-186">Configurer un objet de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="7e274-186">Configure a VM object</span></span>
<span data-ttu-id="7e274-187">Maintenant que nous avons défini les ressources réseau et de stockage, nous pouvons définir les ressources de calcul de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7e274-187">Now that we have storage and network resources defined, we are ready to define compute resources for the virtual machine.</span></span> <span data-ttu-id="7e274-188">Dans notre didacticiel, nous allons configurer la taille de la machine virtuelle et plusieurs propriétés du système d’exploitation, spécifier l’interface réseau que nous avons créée auparavant, définir le Blob Storage et identifier le disque du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="7e274-188">For our tutorial, we will specify the virtual machine size and various operating system properties, specify the network interface that we previously created, define blob storage, and then specify the operating system disk.</span></span>

### <a name="create-the-vm-object"></a><span data-ttu-id="7e274-189">Créer l’objet de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="7e274-189">Create the VM object</span></span>
<span data-ttu-id="7e274-190">Nous allons commencer par spécifier la taille de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7e274-190">We will start by specifying the virtual machine size.</span></span> <span data-ttu-id="7e274-191">Dans ce didacticiel, nous spécifions une DS13.</span><span class="sxs-lookup"><span data-stu-id="7e274-191">For this tutorial, we are specifying a DS13.</span></span> <span data-ttu-id="7e274-192">Nous allons utiliser l’applet de commande [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) pour créer une machine virtuelle configurable, avec le nom et la taille définis à l’aide des variables que vous avez déjà initialisées.</span><span class="sxs-lookup"><span data-stu-id="7e274-192">We will use the [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) cmdlet to create a configurable virtual machine object with the name and size defined using the variables that you previously initialized.</span></span>

<span data-ttu-id="7e274-193">Exécutez l’applet de commande suivante pour créer l’objet de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7e274-193">Execute the following cmdlet to create the virtual machine object.</span></span>

    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize

### <a name="create-a-credential-object-to-hold-the-name-and-password-for-the-local-administrator-credentials"></a><span data-ttu-id="7e274-194">Créer un objet d’informations d’identification pour stocker le nom et le mot de passe de l’administrateur local</span><span class="sxs-lookup"><span data-stu-id="7e274-194">Create a credential object to hold the name and password for the local administrator credentials</span></span>
<span data-ttu-id="7e274-195">Avant de définir les propriétés du système d’exploitation de la machine virtuelle, nous devons indiquer les informations d’identification du compte d’administrateur local sous la forme d’une chaîne de caractères sécurisée.</span><span class="sxs-lookup"><span data-stu-id="7e274-195">Before we can set the operating system properties for the virtual machine, we need to supply the credentials for the local administrator account as a secure string.</span></span> <span data-ttu-id="7e274-196">Pour ce faire, nous allons utiliser l’applet de commande [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) .</span><span class="sxs-lookup"><span data-stu-id="7e274-196">To accomplish this, we will use the [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

<span data-ttu-id="7e274-197">Exécutez l’applet de commande suivante puis, dans la fenêtre de demande d’informations d’identification Windows PowerShell, tapez le nom et le mot de passe à utiliser pour le compte d’administrateur local sur la machine virtuelle Windows.</span><span class="sxs-lookup"><span data-stu-id="7e274-197">Execute the following cmdlet and, in the Windows PowerShell credential request window, type the name and password to use for the local administrator account in the Windows virtual machine.</span></span>

    $Credential = Get-Credential -Message "Type the name and password of the local administrator account."

### <a name="set-the-operating-system-properties-for-the-virtual-machine"></a><span data-ttu-id="7e274-198">Configurer les propriétés du système d’exploitation de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="7e274-198">Set the operating system properties for the virtual machine</span></span>
<span data-ttu-id="7e274-199">Nous pouvons maintenant configurer les propriétés du système d’exploitation de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7e274-199">Now we are ready to set the virtual machine's operating system properties.</span></span> <span data-ttu-id="7e274-200">Nous allons utiliser l’applet de commande [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) pour configurer le système d’exploitation Windows, exiger l’installation de [l’agent de machine virtuelle](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json), spécifier que l’applet de commande active la mise à jour automatique et définir le nom de la machine virtuelle, le nom de l’ordinateur et les informations d’identification à l’aide des variables que vous avez déjà initialisées.</span><span class="sxs-lookup"><span data-stu-id="7e274-200">We will use the [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) cmdlet to set the type of operating system as Windows, require the [virtual machine agent](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) to be installed, specify that the cmdlet enables auto update and set the virtual machine name, the computer name, and the credential using the variables that you previously initialized.</span></span>

<span data-ttu-id="7e274-201">Exécutez l’applet de commande suivante pour définir les propriétés du système d’exploitation de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7e274-201">Execute the following cmdlet to set the operating system properties for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate

### <a name="add-the-network-interface-to-the-virtual-machine"></a><span data-ttu-id="7e274-202">Ajouter l’interface réseau à la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="7e274-202">Add the network interface to the virtual machine</span></span>
<span data-ttu-id="7e274-203">Ensuite, nous allons ajouter l’interface réseau précédemment créée à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7e274-203">Next, we will add the network interface that we created previously to the virtual machine.</span></span> <span data-ttu-id="7e274-204">Nous allons utiliser l’applet de commande [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) pour ajouter l’interface réseau à l’aide de la variable d’interface réseau définie auparavant.</span><span class="sxs-lookup"><span data-stu-id="7e274-204">We will use the [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) cmdlet to add the network interface using the network interface variable that you defined earlier.</span></span>

<span data-ttu-id="7e274-205">Exécutez l’applet de commande suivante pour définir l’interface réseau de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7e274-205">Execute the following cmdlet to set the network interface for your virtual machine.</span></span>

    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id

### <a name="set-the-blob-storage-location-for-the-disk-to-be-used-by-the-virtual-machine"></a><span data-ttu-id="7e274-206">Définir l’emplacement de Blob Storage du disque à utiliser par la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="7e274-206">Set the blob storage location for the disk to be used by the virtual machine</span></span>
<span data-ttu-id="7e274-207">Ensuite, nous allons définir l’emplacement de Blob Storage du disque à utiliser par la machine virtuelle à l’aide des variables définies auparavant.</span><span class="sxs-lookup"><span data-stu-id="7e274-207">Next, we will set the blob storage location for the disk to be used by the virtual machine using the variables that you defined earlier.</span></span>

<span data-ttu-id="7e274-208">Exécutez l’applet de commande suivante pour définir l’emplacement de Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="7e274-208">Execute the following cmdlet to set the blob storage location.</span></span>

    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"

### <a name="set-the-operating-system-disk-properties-for-the-virtual-machine"></a><span data-ttu-id="7e274-209">Configurer les propriétés du disque du système d’exploitation de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="7e274-209">Set the operating system disk properties for the virtual machine</span></span>
<span data-ttu-id="7e274-210">Ensuite, nous allons configurer les propriétés du disque du système d’exploitation de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7e274-210">Next, we will set the operating system disk properties for the virtual machine.</span></span> <span data-ttu-id="7e274-211">Nous allons utiliser l’applet de commande [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) pour spécifier que le système d’exploitation de la machine virtuelle proviendra d’une image, pour définir la mise en cache en lecture seule (car SQL Server est installé sur le même disque) et spécifier le nom de la machine virtuelle ainsi que le disque du système d’exploitation définis à l’aide des variables configurées auparavant.</span><span class="sxs-lookup"><span data-stu-id="7e274-211">We will use the [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) cmdlet to specify that the operating system for the virtual machine will come from an image, to set caching to read only (because SQL Server is being installed on the same disk) and define the virtual machine name and the operating system disk defined using the variables that we defined earlier.</span></span>

<span data-ttu-id="7e274-212">Exécutez l’applet de commande suivante pour configurer les propriétés du disque du système d’exploitation de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7e274-212">Execute the following cmdlet to set the operating system disk properties for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

### <a name="specify-the-platform-image-for-the-virtual-machine"></a><span data-ttu-id="7e274-213">Spécifier l’image de plateforme de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="7e274-213">Specify the platform image for the virtual machine</span></span>
<span data-ttu-id="7e274-214">Notre dernière étape de configuration consiste à spécifier l’image de plateforme de notre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7e274-214">Our last configuration step is to specify the platform image for our virtual machine.</span></span> <span data-ttu-id="7e274-215">Dans notre didacticiel, nous utilisons la dernière image en date de SQL Server 2016 CTP.</span><span class="sxs-lookup"><span data-stu-id="7e274-215">For our tutorial, we are using the latest SQL Server 2016 CTP image.</span></span> <span data-ttu-id="7e274-216">Nous allons utiliser l’applet de commande [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) pour utiliser cette image définie par les variables définies auparavant.</span><span class="sxs-lookup"><span data-stu-id="7e274-216">We will use the [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) cmdlet to use this image as defined by the variables that you defined earlier.</span></span>

<span data-ttu-id="7e274-217">Exécutez l’applet de commande suivante pour définir l’image de plateforme de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7e274-217">Execute the following cmdlet to specify the platform image for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

## <a name="create-the-sql-vm"></a><span data-ttu-id="7e274-218">Créer la machine virtuelle SQL</span><span class="sxs-lookup"><span data-stu-id="7e274-218">Create the SQL VM</span></span>
<span data-ttu-id="7e274-219">Une fois les étapes de configuration terminées, vous pouvez créer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7e274-219">Now that you have finished the configuration steps, you are ready to create the virtual machine.</span></span> <span data-ttu-id="7e274-220">Nous allons utiliser l’applet de commande [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) pour créer la machine virtuelle à l’aide des variables que nous avons définies.</span><span class="sxs-lookup"><span data-stu-id="7e274-220">We will use the [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) cmdlet to create the virtual machine using the variables that we have defined.</span></span>

<span data-ttu-id="7e274-221">Exécutez l’applet de commande suivante pour créer votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7e274-221">Execute the following cmdlet to create your virtual machine.</span></span>

    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

<span data-ttu-id="7e274-222">La machine virtuelle est créée.</span><span class="sxs-lookup"><span data-stu-id="7e274-222">The virtual machine is created.</span></span> <span data-ttu-id="7e274-223">Remarquez qu’un compte de stockage standard est créé pour les diagnostics de démarrage, car le compte de stockage spécifié pour le disque de la machine virtuelle est un compte Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="7e274-223">Notice that a standard storage account is created for boot diagnostics because the specified storage account for the virtual machine's disk is a premium storage account.</span></span>

<span data-ttu-id="7e274-224">Vous pouvez maintenant afficher cette machine dans le portail Azure pour [voir son adresse IP publique et son nom de domaine complet](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="7e274-224">You can now view this machine in the Azure Portal to see [its public IP address and its fully qualified domain name](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

## <a name="example-script"></a><span data-ttu-id="7e274-225">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="7e274-225">Example script</span></span>
<span data-ttu-id="7e274-226">Le script suivant contient le script PowerShell complet pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="7e274-226">The following script contains the complete PowerShell script for this tutorial.</span></span> <span data-ttu-id="7e274-227">Nous considérons que vous avez déjà configuré l’abonnement Azure à utiliser avec les commandes **Add-AzureRmAccount** et **Select-AzureRmSubscription**.</span><span class="sxs-lookup"><span data-stu-id="7e274-227">It assumes that you have already setup the Azure subscription to use with the **Add-AzureRmAccount** and **Select-AzureRmSubscription** commands.</span></span>

    # Variables
    ## Global
    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"
    ## Storage
    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

    ## Network
    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $TCPIPAllocationMethod = "Dynamic"
    $DomainName = "sqlvm1"

    ##Compute
    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

    ##Image
    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

    # Resource Group
    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

    # Storage
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

    # Network
    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix
    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig
    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName
    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

    # Compute
    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize
    $Credential = Get-Credential -Message "Type the name and password of the local administrator account."
    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate #-TimeZone = $TimeZone
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

    # Image
    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

    ## Create the VM in Azure
    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

## <a name="next-steps"></a><span data-ttu-id="7e274-228">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7e274-228">Next steps</span></span>
<span data-ttu-id="7e274-229">Une fois la machine virtuelle créée, vous pouvez vous y connecter à l’aide du protocole RDP et en configurant la connectivité.</span><span class="sxs-lookup"><span data-stu-id="7e274-229">After the virtual machine is created, you are ready to connect to the virtual machine using RDP and setup connectivity.</span></span> <span data-ttu-id="7e274-230">Pour plus d’informations, consultez [Se connecter à une machine virtuelle SQL Server sur Azure (Resource Manager)](virtual-machines-windows-sql-connect.md).</span><span class="sxs-lookup"><span data-stu-id="7e274-230">For more information, see [Connect to a SQL Server Virtual Machine on Azure (Resource Manager)](virtual-machines-windows-sql-connect.md).</span></span>

