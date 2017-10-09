---
title: aaaCreate une Machine virtuelle de SQL Server dans Azure PowerShell (Resource Manager) | Documents Microsoft
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
ms.openlocfilehash: 2b8cb8f69ff9894a95eab617816a60c8674eeefa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-resource-manager"></a><span data-ttu-id="6bd0c-103">Approvisionner une machine virtuelle SQL Server à l’aide d’Azure PowerShell (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="6bd0c-103">Provision a SQL Server virtual machine using Azure PowerShell (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6bd0c-104">Portail</span><span class="sxs-lookup"><span data-stu-id="6bd0c-104">Portal</span></span>](virtual-machines-windows-portal-sql-server-provision.md)
> * [<span data-ttu-id="6bd0c-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6bd0c-105">PowerShell</span></span>](virtual-machines-windows-ps-sql-create.md)
>
>

## <a name="overview"></a><span data-ttu-id="6bd0c-106">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="6bd0c-106">Overview</span></span>
<span data-ttu-id="6bd0c-107">Ce didacticiel vous montre comment une seule machine virtuelle Azure à l’aide de toocreate hello **Azure Resource Manager** modèle de déploiement à l’aide des applets de commande PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-107">This tutorial shows you how toocreate a single Azure virtual machine using hello **Azure Resource Manager** deployment model using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="6bd0c-108">Dans ce didacticiel, nous allons créer une seule machine virtuelle à l’aide d’un seul lecteur de disque à partir d’une image Bonjour SQL galerie.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-108">In this tutorial, we will create a single virtual machine using a single disk drive from an image in hello SQL Gallery.</span></span> <span data-ttu-id="6bd0c-109">Nous allons créer de nouveaux fournisseurs de stockage de hello, réseau et les ressources de calcul qui seront utilisées par l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-109">We will create new providers for hello storage, network, and compute resources that will be used by hello virtual machine.</span></span> <span data-ttu-id="6bd0c-110">Si vous avez déjà des fournisseurs pour ces ressources, vous pouvez les utiliser.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-110">If you have existing providers for any of these resources, you can use those providers instead.</span></span>

<span data-ttu-id="6bd0c-111">Si vous avez besoin de hello version classique de cette rubrique, consultez [configurer un ordinateur virtuel de SQL Server à l’aide de PowerShell Azure Classic](../classic/ps-sql-create.md).</span><span class="sxs-lookup"><span data-stu-id="6bd0c-111">If you need hello classic version of this topic, see [Provision a SQL Server virtual machine using Azure PowerShell Classic](../classic/ps-sql-create.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6bd0c-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6bd0c-112">Prerequisites</span></span>
<span data-ttu-id="6bd0c-113">Pour ce didacticiel, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="6bd0c-113">For this tutorial you'll need:</span></span>

* <span data-ttu-id="6bd0c-114">Un compte Azure et un abonnement, avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-114">An Azure account and subscription before you start.</span></span> <span data-ttu-id="6bd0c-115">Si vous n’en avez pas, inscrivez-vous pour un [essai gratuit](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6bd0c-115">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="6bd0c-116">[Azure PowerShell](/powershell/azure/overview)1.4.0 ou version ultérieure (ce didacticiel a été écrit avec la version 1.5.0).</span><span class="sxs-lookup"><span data-stu-id="6bd0c-116">[Azure PowerShell)](/powershell/azure/overview), minimum version of 1.4.0 or later (this tutorial written using version 1.5.0).</span></span>
  * <span data-ttu-id="6bd0c-117">tooretrieve votre version, le type **Azure de Get-Module - ListAvailable**.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-117">tooretrieve your version, type **Get-Module Azure -ListAvailable**.</span></span>

## <a name="configure-your-subscription"></a><span data-ttu-id="6bd0c-118">Configurer votre abonnement</span><span class="sxs-lookup"><span data-stu-id="6bd0c-118">Configure your subscription</span></span>
<span data-ttu-id="6bd0c-119">Ouvrez Windows PowerShell et établir un accès tooyour compte Azure en exécutant hello suivant l’applet de commande.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-119">Open Windows PowerShell and establish access tooyour Azure account by running hello following cmdlet.</span></span> <span data-ttu-id="6bd0c-120">S’affiche avec un signe dans l’écran tooenter vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-120">You will be presented with a sign in screen tooenter your credentials.</span></span> <span data-ttu-id="6bd0c-121">Utilisez hello même courrier électronique et le mot de passe que vous utilisez toosign dans toohello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-121">Use hello same email and password that you use toosign in toohello Azure portal.</span></span>

    Add-AzureRmAccount

<span data-ttu-id="6bd0c-122">Une fois connecté avec succès, vous verrez des informations sur l’écran qui inclut l’ID d’abonnement hello avec lequel vous êtes dans.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-122">After successfully signing in you will see some information on screen that includes hello SubscriptionId with which you signed in.</span></span> <span data-ttu-id="6bd0c-123">Il s’agit d’abonnement hello dans lequel les ressources hello pour ce didacticiel sont créées, sauf si vous modifiez tooa autre abonnement.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-123">This is hello subscription in which hello resources for this tutorial will be created unless you change tooa different subscription.</span></span> <span data-ttu-id="6bd0c-124">Si vous avez plusieurs abonnement, exécutez hello suivant l’applet de commande tooreturn une liste de tous les de votre abonnement :</span><span class="sxs-lookup"><span data-stu-id="6bd0c-124">If you have multiple SubscriptionIds, run hello following cmdlet tooreturn a list of all of your SubscriptionIds:</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="6bd0c-125">toochange tooanother ID d’abonnement, exécutez hello suivant l’applet de commande avec votre ID d’abonnement souhaité.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-125">toochange tooanother SubscriptionID, run hello following cmdlet with your desired SubscriptionId.</span></span>

    Select-AzureRmSubscription -SubscriptionId xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

## <a name="define-image-variables"></a><span data-ttu-id="6bd0c-126">Définir des variables d’image</span><span class="sxs-lookup"><span data-stu-id="6bd0c-126">Define image variables</span></span>
<span data-ttu-id="6bd0c-127">utilisation de toosimplify et la compréhension du script hello effectuée à partir de ce didacticiel, nous allons commencer en définissant un nombre de variables.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-127">toosimplify usability and understanding of hello completed script from this tutorial, we will start by defining a number of variables.</span></span> <span data-ttu-id="6bd0c-128">Modifier les valeurs de paramètre de hello que vous convenance mais Méfiez-vous des caractères spéciaux et les longueurs de tooname connexes de restrictions d’affectation de noms lors de la modification des valeurs hello fournies.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-128">Change hello parameter values as you see fit, but beware of naming restrictions related tooname lengths and special characters when modifying hello values provided.</span></span>

### <a name="location-and-resource-group"></a><span data-ttu-id="6bd0c-129">Emplacement et groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="6bd0c-129">Location and Resource Group</span></span>
<span data-ttu-id="6bd0c-130">Utilisez les deux variables toodefine hello données hello et zone de groupe de ressources dans lequel vous allez créer vos autres ressources pour la machine virtuelle de hello hello.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-130">Use two variables toodefine hello data region and hello resource group into which you will create hello other resources for hello virtual machine.</span></span>

<span data-ttu-id="6bd0c-131">Modifiez-le selon vos besoins, puis exécutez hello suivant d’applets de commande tooinitialize à ces variables.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-131">Modify as desired and then execute hello following cmdlets tooinitialize these variables.</span></span>

    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"

### <a name="storage-properties"></a><span data-ttu-id="6bd0c-132">Propriétés de stockage</span><span class="sxs-lookup"><span data-stu-id="6bd0c-132">Storage properties</span></span>
<span data-ttu-id="6bd0c-133">Utilisez hello suivant variables toodefine hello compte et hello type de stockage de toobe de stockage utilisé par l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-133">Use hello following variables toodefine hello storage account and hello type of storage toobe used by hello virtual machine.</span></span>

<span data-ttu-id="6bd0c-134">Modifiez-le selon vos besoins, puis exécutez hello suivant tooinitialize de l’applet de commande à ces variables.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-134">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span> <span data-ttu-id="6bd0c-135">Notez que, dans cet exemple, nous utilisons [Premium Storage](../../../storage/common/storage-premium-storage.md), qui est recommandé pour les charges de travail de production.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-135">Note that in this example, we are using [Premium Storage](../../../storage/common/storage-premium-storage.md), which is recommended for production workloads.</span></span> <span data-ttu-id="6bd0c-136">Pour plus d’informations et d’autres recommandations, consultez [Meilleures pratiques relatives aux performances de SQL Server dans Azure Virtual Machines](virtual-machines-windows-sql-performance.md).</span><span class="sxs-lookup"><span data-stu-id="6bd0c-136">For details on this guidance and other recommendations, see [Performance best practices for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md).</span></span>

    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

### <a name="network-properties"></a><span data-ttu-id="6bd0c-137">Propriétés du réseau</span><span class="sxs-lookup"><span data-stu-id="6bd0c-137">Network properties</span></span>
<span data-ttu-id="6bd0c-138">Utilisez hello suivant l’interface de réseau variables toodefine hello, méthode d’allocation de TCP/IP hello, nom de réseau virtuel hello, nom de sous-réseau virtuel hello, hello plage d’adresses IP pour le réseau virtuel de hello, hello plage d’adresses IP pour le sous-réseau de hello et hello domaine public toobe d’étiquette nom utilisé par le réseau hello dans la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-138">Use hello following variables toodefine hello network interface, hello TCP/IP allocation method, hello virtual network name, hello virtual subnet name, hello range of IP addresses for hello virtual network, hello range of IP addresses for hello subnet, and hello public domain name label toobe used by hello network in hello virtual machine.</span></span>

<span data-ttu-id="6bd0c-139">Modifiez-le selon vos besoins, puis exécutez hello suivant tooinitialize de l’applet de commande à ces variables.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-139">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span>

    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $TCPIPAllocationMethod = "Dynamic"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $DomainName = "sqlvm1"

### <a name="virtual-machine-properties"></a><span data-ttu-id="6bd0c-140">Propriétés de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="6bd0c-140">Virtual machine properties</span></span>
<span data-ttu-id="6bd0c-141">Utilisez hello suivant le nom d’ordinateur virtuel de variables toodefine hello, Nom_Ordinateur hello, taille de machine virtuelle hello et nom du disque de système d’exploitation pour la machine virtuelle de hello hello.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-141">Use hello following variables toodefine hello virtual machine name, hello computer name, hello virtual machine size, and hello operating system disk name for hello virtual machine.</span></span>

<span data-ttu-id="6bd0c-142">Modifiez-le selon vos besoins, puis exécutez hello suivant tooinitialize de l’applet de commande à ces variables.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-142">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span>

    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

### <a name="image-properties"></a><span data-ttu-id="6bd0c-143">Propriétés de l’image</span><span class="sxs-lookup"><span data-stu-id="6bd0c-143">Image properties</span></span>
<span data-ttu-id="6bd0c-144">Utilisez hello suivant variables toodefine hello image toouse pour la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-144">Use hello following variables toodefine hello image toouse for hello virtual machine.</span></span> <span data-ttu-id="6bd0c-145">Dans cet exemple, l’image de SQL Server 2016 Enterprise hello est utilisé.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-145">In this example, hello SQL Server 2016 Enterprise image is used.</span></span>

<span data-ttu-id="6bd0c-146">Modifiez-le selon vos besoins, puis exécutez hello suivant tooinitialize de l’applet de commande à ces variables.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-146">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span>

    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

<span data-ttu-id="6bd0c-147">Notez que vous pouvez obtenir une liste complète des offres d’image de SQL Server avec la commande hello Get-AzureRmVMImageOffer :</span><span class="sxs-lookup"><span data-stu-id="6bd0c-147">Note that you can get a full list of SQL Server image offerings with hello Get-AzureRmVMImageOffer command:</span></span>

    Get-AzureRmVMImageOffer -Location 'East US' -Publisher 'MicrosoftSQLServer'

<span data-ttu-id="6bd0c-148">Et vous pouvez voir hello références (SKU) disponible pour une offre avec la commande Get-AzureRmVMImageSku de hello.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-148">And you can see hello Skus available for an offering with hello Get-AzureRmVMImageSku command.</span></span> <span data-ttu-id="6bd0c-149">Hello commande suivante affiche toutes les références (SKU) disponible pour hello **SQL2014SP1-WS2012R2** offre.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-149">hello following command shows all Skus available for hello **SQL2014SP1-WS2012R2** offer.</span></span>

    Get-AzureRmVMImageSku -Location 'East US' -Publisher 'MicrosoftSQLServer' -Offer 'SQL2014SP1-WS2012R2' | Select Skus

## <a name="create-a-resource-group"></a><span data-ttu-id="6bd0c-150">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="6bd0c-150">Create a resource group</span></span>
<span data-ttu-id="6bd0c-151">Avec le modèle de déploiement du Gestionnaire de ressources hello, hello premier objet que vous créez est le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-151">With hello Resource Manager deployment model, hello first object that you create is hello resource group.</span></span> <span data-ttu-id="6bd0c-152">Nous allons utiliser hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) toocreate de l’applet de commande un groupe de ressources Azure et ses ressources avec des ressources de hello groupe le nom et l’emplacement défini par des variables hello que vous avez déjà initialisé.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-152">We will use hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet toocreate an Azure resource group and its resources with hello resource group name and location defined by hello variables that you previously initialized.</span></span>

<span data-ttu-id="6bd0c-153">Exécutez hello suivant l’applet de commande toocreate votre nouveau groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-153">Execute hello following cmdlet toocreate your new resource group.</span></span>

    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

## <a name="create-a-storage-account"></a><span data-ttu-id="6bd0c-154">Créez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-154">Create a storage account</span></span>
<span data-ttu-id="6bd0c-155">Hello virtual machine nécessite des ressources de stockage pour le disque du système d’exploitation hello et hello de données SQL Server et les fichiers journaux.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-155">hello virtual machine requires storage resources for hello operating system disk and for hello SQL Server data and log files.</span></span> <span data-ttu-id="6bd0c-156">Pour plus de simplicité, nous allons créer un seul disque pour les deux.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-156">For simplicity, we will create a single disk for both.</span></span> <span data-ttu-id="6bd0c-157">Vous pouvez attacher des disques supplémentaires ultérieurement à l’aide de hello [disque Add-Azure](/powershell/module/azure/add-azuredisk) applet de commande de commande tooplace vos données SQL Server et les journaux sur des disques dédiés.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-157">You can attach additional disks later using hello [Add-Azure Disk](/powershell/module/azure/add-azuredisk) cmdlet in order tooplace your SQL Server data and log files on dedicated disks.</span></span> <span data-ttu-id="6bd0c-158">Nous allons utiliser hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) toocreate de l’applet de commande un stockage standard de compte dans votre nouveau groupe de ressources et avec le nom de compte de stockage hello, nom de référence (SKU) de stockage et l’emplacement définis à l’aide de variables de hello que vous avez précédemment initialisé.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-158">We will use hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet toocreate a standard storage account in your new resource group and with hello storage account name, storage Sku name, and location defined using hello variables that you previously initialized.</span></span>

<span data-ttu-id="6bd0c-159">Exécutez hello suivant l’applet de commande toocreate votre nouveau compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-159">Execute hello following cmdlet toocreate your new storage account.</span></span>

    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

## <a name="create-network-resources"></a><span data-ttu-id="6bd0c-160">Créer des ressources réseau</span><span class="sxs-lookup"><span data-stu-id="6bd0c-160">Create network resources</span></span>
<span data-ttu-id="6bd0c-161">machine virtuelle de Hello nécessite un nombre de ressources réseau pour la connectivité réseau.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-161">hello virtual machine requires a number of network resources for network connectivity.</span></span>

* <span data-ttu-id="6bd0c-162">Chaque machine virtuelle requiert un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-162">Each virtual machine requires a virtual network.</span></span>
* <span data-ttu-id="6bd0c-163">Un réseau virtuel doit avoir au moins un sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-163">A virtual network must have at least one subnet defined.</span></span>
* <span data-ttu-id="6bd0c-164">Une interface réseau doit être définie avec une adresse IP privée ou publique.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-164">A network interface must be defined with either a public or a private IP address.</span></span>

### <a name="create-a-virtual-network-subnet-configuration"></a><span data-ttu-id="6bd0c-165">Créer une configuration de sous-réseau de réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="6bd0c-165">Create a virtual network subnet configuration</span></span>
<span data-ttu-id="6bd0c-166">Nous allons commencer par créer une configuration de sous-réseau pour notre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-166">We will start by creating a subnet configuration for our virtual network.</span></span> <span data-ttu-id="6bd0c-167">Pour notre didacticiel, nous allons créer un sous-réseau par défaut à l’aide de hello [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-167">For our tutorial, we will create a default subnet using hello [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) cmdlet.</span></span> <span data-ttu-id="6bd0c-168">Nous allons créer notre configuration de sous-réseau de réseau virtuel avec hello nom et adresse de préfixe du sous-réseau défini à l’aide de variables hello que vous avez déjà initialisé.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-168">We will create our virtual network subnet configuration with hello subnet name and address prefix defined using hello variables that you previously initialized.</span></span>

> [!NOTE]
> <span data-ttu-id="6bd0c-169">Vous pouvez définir des propriétés supplémentaires de la configuration de sous-réseau de réseau virtuel hello à l’aide de cette applet de commande, mais qui est abordée dans ce didacticiel hello.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-169">You can define additional properties of hello virtual network subnet configuration using this cmdlet, but that is beyond hello scope of this tutorial.</span></span>
>
>

<span data-ttu-id="6bd0c-170">Exécutez hello suivant toocreate de l’applet de commande de votre configuration de sous-réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-170">Execute hello following cmdlet toocreate your virtual subnet configuration.</span></span>

    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix

### <a name="create-a-virtual-network"></a><span data-ttu-id="6bd0c-171">Créez un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="6bd0c-171">Create a virtual network</span></span>
<span data-ttu-id="6bd0c-172">Ensuite, nous allons créer notre réseau virtuel à l’aide de hello [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-172">Next, we will create our virtual network using hello [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) cmdlet.</span></span> <span data-ttu-id="6bd0c-173">Nous allons créer notre réseau virtuel dans votre nouveau groupe de ressources, avec un préfixe d’adresse définie à l’aide de variables de hello précédemment initialisée et à l’aide de la configuration de sous-réseau hello que vous avez définie à l’étape précédente de hello, l’emplacement et nom de hello.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-173">We will create our virtual network in your new resource group, with hello name, location, and address prefix defined using hello variables that you previously initialized, and using hello subnet configuration that you defined in hello previous step.</span></span>

<span data-ttu-id="6bd0c-174">Exécutez hello suivant toocreate de l’applet de commande de votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-174">Execute hello following cmdlet toocreate your virtual network.</span></span>

    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig

### <a name="create-hello-public-ip-address"></a><span data-ttu-id="6bd0c-175">Créer une adresse IP publique hello</span><span class="sxs-lookup"><span data-stu-id="6bd0c-175">Create hello public IP address</span></span>
<span data-ttu-id="6bd0c-176">Maintenant que nous avons notre réseau virtuel défini, nous devons tooconfigure une adresse IP pour la machine virtuelle de toohello connectivité.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-176">Now that we have our virtual network defined, we need tooconfigure an IP address for connectivity toohello virtual machine.</span></span> <span data-ttu-id="6bd0c-177">Pour ce didacticiel, nous allons créer une adresse IP publique à l’aide de la connectivité Internet de toosupport d’adressage IP dynamique.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-177">For this tutorial, we will create a public IP address using dynamic IP addressing toosupport Internet connectivity.</span></span> <span data-ttu-id="6bd0c-178">Nous allons utiliser hello [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) applet de commande toocreate hello adresse IP publique dans hello ressource groupe créé prevously et avec le nom de hello, l’emplacement, méthode d’allocation et étiquette de nom de domaine DNS défini à l’aide de hello variables que vous avez déjà initialisé.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-178">We will use hello [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) cmdlet toocreate hello public IP address in hello resource group created prevously and with hello name, location, allocation method, and DNS domain name label defined using hello variables that you previously initialized.</span></span>

> [!NOTE]
> <span data-ttu-id="6bd0c-179">Vous pouvez définir des propriétés supplémentaires de l’adresse IP publique hello à l’aide de cette applet de commande, mais qui est abordée dans ce didacticiel initial hello.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-179">You can define additional properties of hello public IP address using this cmdlet, but that is beyond hello scope of this initial tutorial.</span></span> <span data-ttu-id="6bd0c-180">Vous pouvez également créer une adresse privée ou une adresse avec une adresse statique, mais qui est également abordée dans ce didacticiel hello.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-180">You could also create a private address or an address with a static address, but that is also beyond hello scope of this tutorial.</span></span>
>
>

<span data-ttu-id="6bd0c-181">Exécutez hello suivant l’applet de commande toocreate votre adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-181">Execute hello following cmdlet toocreate your public IP address.</span></span>

    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName

### <a name="create-hello-network-interface"></a><span data-ttu-id="6bd0c-182">Créer l’interface de réseau hello</span><span class="sxs-lookup"><span data-stu-id="6bd0c-182">Create hello network interface</span></span>
<span data-ttu-id="6bd0c-183">Nous sommes maintenant interface réseau hello prêt toocreate notre ordinateur virtuel utilisera.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-183">We are now ready toocreate hello network interface that our virtual machine will use.</span></span> <span data-ttu-id="6bd0c-184">Nous allons utiliser hello [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) toocreate de l’applet de commande notre interface réseau dans le groupe de ressources hello créé précédemment et avec le nom de hello, l’emplacement, sous-réseau et adresse IP publique définie précédemment.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-184">We will use hello [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) cmdlet toocreate our network interface in hello resource group created earlier and with hello name, location, subnet and public IP address previously defined.</span></span>

<span data-ttu-id="6bd0c-185">Exécutez hello suivant l’applet de commande toocreate votre interface réseau.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-185">Execute hello following cmdlet toocreate your network interface.</span></span>

    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

## <a name="configure-a-vm-object"></a><span data-ttu-id="6bd0c-186">Configurer un objet de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="6bd0c-186">Configure a VM object</span></span>
<span data-ttu-id="6bd0c-187">Maintenant que nous avons des ressources réseau et de stockage définies, nous sommes les ressources de calcul toodefine prêt pour la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-187">Now that we have storage and network resources defined, we are ready toodefine compute resources for hello virtual machine.</span></span> <span data-ttu-id="6bd0c-188">Pour notre didacticiel, nous sera spécifier la taille de machine virtuelle hello et diverses propriétés de système d’exploitation, spécifiez hello une interface réseau que vous avez créée précédemment, définir le stockage d’objets blob, puis spécifiez le disque du système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-188">For our tutorial, we will specify hello virtual machine size and various operating system properties, specify hello network interface that we previously created, define blob storage, and then specify hello operating system disk.</span></span>

### <a name="create-hello-vm-object"></a><span data-ttu-id="6bd0c-189">Créer l’objet d’ordinateur virtuel hello</span><span class="sxs-lookup"><span data-stu-id="6bd0c-189">Create hello VM object</span></span>
<span data-ttu-id="6bd0c-190">Nous allons commencer en spécifiant la taille de machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-190">We will start by specifying hello virtual machine size.</span></span> <span data-ttu-id="6bd0c-191">Dans ce didacticiel, nous spécifions une DS13.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-191">For this tutorial, we are specifying a DS13.</span></span> <span data-ttu-id="6bd0c-192">Nous allons utiliser hello [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) toocreate de l’applet de commande un objet configurables par l’ordinateur virtuel avec le nom de hello et la taille définie à l’aide de variables hello que vous avez déjà initialisé.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-192">We will use hello [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) cmdlet toocreate a configurable virtual machine object with hello name and size defined using hello variables that you previously initialized.</span></span>

<span data-ttu-id="6bd0c-193">Exécutez hello suivant l’objet d’ordinateur virtuel d’applet de commande toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-193">Execute hello following cmdlet toocreate hello virtual machine object.</span></span>

    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize

### <a name="create-a-credential-object-toohold-hello-name-and-password-for-hello-local-administrator-credentials"></a><span data-ttu-id="6bd0c-194">Créer un nom de hello toohold l’objet d’informations d’identification et un mot de passe pour les informations d’identification d’administrateur local de hello</span><span class="sxs-lookup"><span data-stu-id="6bd0c-194">Create a credential object toohold hello name and password for hello local administrator credentials</span></span>
<span data-ttu-id="6bd0c-195">Nous pouvons définir les propriétés de système d’exploitation hello pour la machine virtuelle de hello, nous devons informations d’identification de toosupply hello pour le compte d’administrateur local hello sous forme de chaîne sécurisée.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-195">Before we can set hello operating system properties for hello virtual machine, we need toosupply hello credentials for hello local administrator account as a secure string.</span></span> <span data-ttu-id="6bd0c-196">tooaccomplish, nous allons utiliser hello [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-196">tooaccomplish this, we will use hello [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

<span data-ttu-id="6bd0c-197">Exécutez hello suivant l’applet de commande et, dans la fenêtre de demande d’informations d’identification hello Windows PowerShell, tapez toouse de hello nom et mot de passe pour le compte d’administrateur local hello dans l’ordinateur virtuel Windows hello.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-197">Execute hello following cmdlet and, in hello Windows PowerShell credential request window, type hello name and password toouse for hello local administrator account in hello Windows virtual machine.</span></span>

    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."

### <a name="set-hello-operating-system-properties-for-hello-virtual-machine"></a><span data-ttu-id="6bd0c-198">Définir les propriétés de système d’exploitation hello pour la machine virtuelle de hello</span><span class="sxs-lookup"><span data-stu-id="6bd0c-198">Set hello operating system properties for hello virtual machine</span></span>
<span data-ttu-id="6bd0c-199">Nous sommes maintenant les propriétés de système d’exploitation de l’ordinateur virtuel tooset prêt hello.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-199">Now we are ready tooset hello virtual machine's operating system properties.</span></span> <span data-ttu-id="6bd0c-200">Nous allons utiliser hello [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) type de hello tooset applet de commande du système d’exploitation Windows, nécessitent hello [agent de machine virtuelle](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toobe installé, spécifiez cette applet de commande hello active automatiquement mettre à jour et définir le nom de machine virtuelle hello, Nom_Ordinateur hello et informations d’identification hello à l’aide de variables hello que vous avez déjà initialisé.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-200">We will use hello [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) cmdlet tooset hello type of operating system as Windows, require hello [virtual machine agent](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toobe installed, specify that hello cmdlet enables auto update and set hello virtual machine name, hello computer name, and hello credential using hello variables that you previously initialized.</span></span>

<span data-ttu-id="6bd0c-201">Exécutez hello suivant des propriétés de système d’exploitation tooset hello applet de commande pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-201">Execute hello following cmdlet tooset hello operating system properties for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate

### <a name="add-hello-network-interface-toohello-virtual-machine"></a><span data-ttu-id="6bd0c-202">Ajouter une machine virtuelle de hello réseau interface toohello</span><span class="sxs-lookup"><span data-stu-id="6bd0c-202">Add hello network interface toohello virtual machine</span></span>
<span data-ttu-id="6bd0c-203">Ensuite, nous allons ajouter interface de réseau hello que nous avons créé précédemment toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-203">Next, we will add hello network interface that we created previously toohello virtual machine.</span></span> <span data-ttu-id="6bd0c-204">Nous allons utiliser hello [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) interface de réseau hello tooadd applet de commande à l’aide de la variable d’interface réseau hello que vous avez défini précédemment.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-204">We will use hello [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) cmdlet tooadd hello network interface using hello network interface variable that you defined earlier.</span></span>

<span data-ttu-id="6bd0c-205">Exécutez hello suivant l’interface de réseau tooset hello applet de commande pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-205">Execute hello following cmdlet tooset hello network interface for your virtual machine.</span></span>

    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id

### <a name="set-hello-blob-storage-location-for-hello-disk-toobe-used-by-hello-virtual-machine"></a><span data-ttu-id="6bd0c-206">Définir l’emplacement de stockage d’objets blob hello pour hello toobe de disque utilisé par l’ordinateur virtuel de hello</span><span class="sxs-lookup"><span data-stu-id="6bd0c-206">Set hello blob storage location for hello disk toobe used by hello virtual machine</span></span>
<span data-ttu-id="6bd0c-207">Ensuite, nous allons définir emplacement de stockage d’objets blob hello pour hello toobe de disque utilisé par l’ordinateur virtuel de hello à l’aide de variables hello que vous avez défini précédemment.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-207">Next, we will set hello blob storage location for hello disk toobe used by hello virtual machine using hello variables that you defined earlier.</span></span>

<span data-ttu-id="6bd0c-208">Exécutez hello suivant l’emplacement de stockage des objets blob applet de commande tooset hello.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-208">Execute hello following cmdlet tooset hello blob storage location.</span></span>

    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"

### <a name="set-hello-operating-system-disk-properties-for-hello-virtual-machine"></a><span data-ttu-id="6bd0c-209">Définir des propriétés du disque pour la machine virtuelle de hello de système d’exploitation de hello</span><span class="sxs-lookup"><span data-stu-id="6bd0c-209">Set hello operating system disk properties for hello virtual machine</span></span>
<span data-ttu-id="6bd0c-210">Ensuite, nous allons définir système d’exploitation de hello propriétés du disque pour la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-210">Next, we will set hello operating system disk properties for hello virtual machine.</span></span> <span data-ttu-id="6bd0c-211">Nous allons utiliser hello [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) toospecify d’applet de commande qui hello du système d’exploitation pour la machine virtuelle de hello est issu d’une image, tooset tooread uniquement la mise en cache (étant donné que SQL Server est installé sur hello même disque) et définir nom d’ordinateur virtuel Hello et disque de système d’exploitation hello définis à l’aide de variables hello définie précédemment.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-211">We will use hello [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) cmdlet toospecify that hello operating system for hello virtual machine will come from an image, tooset caching tooread only (because SQL Server is being installed on hello same disk) and define hello virtual machine name and hello operating system disk defined using hello variables that we defined earlier.</span></span>

<span data-ttu-id="6bd0c-212">Exécutez hello suivant des propriétés de disque de système d’exploitation applet de commande tooset hello pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-212">Execute hello following cmdlet tooset hello operating system disk properties for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

### <a name="specify-hello-platform-image-for-hello-virtual-machine"></a><span data-ttu-id="6bd0c-213">Spécifiez l’image de plateforme hello pour la machine virtuelle de hello</span><span class="sxs-lookup"><span data-stu-id="6bd0c-213">Specify hello platform image for hello virtual machine</span></span>
<span data-ttu-id="6bd0c-214">Notre dernière étape de configuration est l’image de plateforme toospecify hello pour notre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-214">Our last configuration step is toospecify hello platform image for our virtual machine.</span></span> <span data-ttu-id="6bd0c-215">Pour notre didacticiel, nous utilisons dernière image de SQL Server 2016 CTP hello.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-215">For our tutorial, we are using hello latest SQL Server 2016 CTP image.</span></span> <span data-ttu-id="6bd0c-216">Nous allons utiliser hello [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) toouse de l’applet de commande cette image comme défini par les variables hello que vous avez défini précédemment.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-216">We will use hello [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) cmdlet toouse this image as defined by hello variables that you defined earlier.</span></span>

<span data-ttu-id="6bd0c-217">Exécutez hello suivant l’image de plateforme toospecify hello applet de commande pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-217">Execute hello following cmdlet toospecify hello platform image for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

## <a name="create-hello-sql-vm"></a><span data-ttu-id="6bd0c-218">Créer hello SQL VM</span><span class="sxs-lookup"><span data-stu-id="6bd0c-218">Create hello SQL VM</span></span>
<span data-ttu-id="6bd0c-219">Maintenant que vous avez terminé les étapes de configuration hello, vous êtes prêt toocreate hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-219">Now that you have finished hello configuration steps, you are ready toocreate hello virtual machine.</span></span> <span data-ttu-id="6bd0c-220">Nous allons utiliser hello [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) applet de commande toocreate hello virtual machine à l’aide de variables hello que nous avons définie.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-220">We will use hello [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) cmdlet toocreate hello virtual machine using hello variables that we have defined.</span></span>

<span data-ttu-id="6bd0c-221">Exécutez hello suivant toocreate de l’applet de commande à votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-221">Execute hello following cmdlet toocreate your virtual machine.</span></span>

    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

<span data-ttu-id="6bd0c-222">machine virtuelle de Hello est créé.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-222">hello virtual machine is created.</span></span> <span data-ttu-id="6bd0c-223">Notez qu’un compte de stockage standard est créé pour les diagnostics de démarrage car hello spécifié de compte de stockage pour le disque de l’ordinateur virtuel de hello est un compte de stockage premium.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-223">Notice that a standard storage account is created for boot diagnostics because hello specified storage account for hello virtual machine's disk is a premium storage account.</span></span>

<span data-ttu-id="6bd0c-224">Vous pouvez maintenant afficher cet ordinateur dans hello Azure Portal toosee [son adresse IP publique et son nom de domaine complet](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="6bd0c-224">You can now view this machine in hello Azure Portal toosee [its public IP address and its fully qualified domain name](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

## <a name="example-script"></a><span data-ttu-id="6bd0c-225">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="6bd0c-225">Example script</span></span>
<span data-ttu-id="6bd0c-226">Hello script suivant contient complète du script PowerShell hello pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-226">hello following script contains hello complete PowerShell script for this tutorial.</span></span> <span data-ttu-id="6bd0c-227">Il suppose que vous avez déjà le programme d’installation hello abonnement Azure toouse avec hello **Add-AzureRmAccount** et **sélectionnez-AzureRmSubscription** commandes.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-227">It assumes that you have already setup hello Azure subscription toouse with hello **Add-AzureRmAccount** and **Select-AzureRmSubscription** commands.</span></span>

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
    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."
    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate #-TimeZone = $TimeZone
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

    # Image
    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

    ## Create hello VM in Azure
    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

## <a name="next-steps"></a><span data-ttu-id="6bd0c-228">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6bd0c-228">Next steps</span></span>
<span data-ttu-id="6bd0c-229">Après la création de la machine virtuelle de hello, vous êtes prêt tooconnect toohello virtuels à l’aide de la connexion RDP et le programme d’installation.</span><span class="sxs-lookup"><span data-stu-id="6bd0c-229">After hello virtual machine is created, you are ready tooconnect toohello virtual machine using RDP and setup connectivity.</span></span> <span data-ttu-id="6bd0c-230">Pour plus d’informations, consultez [connecter tooa Machine virtuelle de SQL Server sur Azure (Resource Manager)](virtual-machines-windows-sql-connect.md).</span><span class="sxs-lookup"><span data-stu-id="6bd0c-230">For more information, see [Connect tooa SQL Server Virtual Machine on Azure (Resource Manager)](virtual-machines-windows-sql-connect.md).</span></span>

