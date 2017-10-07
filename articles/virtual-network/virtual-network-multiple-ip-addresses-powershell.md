---
title: aaaMultiple des adresses IP pour les machines virtuelles - PowerShell | Documents Microsoft
description: "Découvrez comment tooassign des adresses IP multiples virtuels tooa à l’aide de PowerShell | Gestionnaire de ressources."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c44ea62f-7e54-4e3b-81ef-0b132111f1f8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/24/2017
ms.author: jdial;annahar
ms.openlocfilehash: df54c4386ce13521e660a3e7208c8c1ab1459bc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-powershell"></a><span data-ttu-id="52b9d-103">Affecter plusieurs adresses IP des ordinateurs de toovirtual à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="52b9d-103">Assign multiple IP addresses toovirtual machines using PowerShell</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="52b9d-104">Cet article explique comment toocreate un ordinateur virtuel (VM) au cours du déploiement d’Azure Resource Manager hello modèle à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="52b9d-104">This article explains how toocreate a virtual machine (VM) through hello Azure Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="52b9d-105">Tooresources créé via le modèle de déploiement classique hello ne peut pas être assignés à plusieurs adresses IP.</span><span class="sxs-lookup"><span data-stu-id="52b9d-105">Multiple IP addresses cannot be assigned tooresources created through hello classic deployment model.</span></span> <span data-ttu-id="52b9d-106">toolearn plus d’informations sur les modèles de déploiement Azure, lisez hello [comprendre les modèles de déploiement](../resource-manager-deployment-model.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="52b9d-106">toolearn more about Azure deployment models, read hello [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="52b9d-107"><a name = "create"></a>Créer une machine virtuelle avec plusieurs adresses IP</span><span class="sxs-lookup"><span data-stu-id="52b9d-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="52b9d-108">Hello étapes qui suivent expliquent comment toocreate un exemple de machine virtuelle avec plusieurs IP, les adresses, comme décrit dans le scénario de hello.</span><span class="sxs-lookup"><span data-stu-id="52b9d-108">hello steps that follow explain how toocreate an example VM with multiple IP addresses, as described in hello scenario.</span></span> <span data-ttu-id="52b9d-109">Modifiez les valeurs des variables en fonction des besoins de votre implémentation.</span><span class="sxs-lookup"><span data-stu-id="52b9d-109">Change variable values as required for your implementation.</span></span>

1. <span data-ttu-id="52b9d-110">Ouvrez une invite de commandes PowerShell et le complète hello restant des étapes de cette section au sein d’une seule session PowerShell.</span><span class="sxs-lookup"><span data-stu-id="52b9d-110">Open a PowerShell command prompt and complete hello remaining steps in this section within a single PowerShell session.</span></span> <span data-ttu-id="52b9d-111">Si vous n’avez pas encore PowerShell est installé et configuré, hello terminé les étapes Bonjour [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) l’article.</span><span class="sxs-lookup"><span data-stu-id="52b9d-111">If you don't already have PowerShell installed and configured, complete hello steps in hello [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="52b9d-112">Compte de tooyour de connexion avec hello `login-azurermaccount` commande.</span><span class="sxs-lookup"><span data-stu-id="52b9d-112">Login tooyour account with hello `login-azurermaccount` command.</span></span>
3. <span data-ttu-id="52b9d-113">Remplacez *myResourceGroup* et *westus* par le nom et l’emplacement de votre choix.</span><span class="sxs-lookup"><span data-stu-id="52b9d-113">Replace *myResourceGroup* and *westus* with a name and location of your choosing.</span></span> <span data-ttu-id="52b9d-114">Créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="52b9d-114">Create a resource group.</span></span> <span data-ttu-id="52b9d-115">Un groupe de ressources est un conteneur logique dans lequel les ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="52b9d-115">A resource group is a logical container into which Azure resources are deployed and managed.</span></span>

    ```powershell
    $RgName   = "MyResourceGroup"
    $Location = "westus"

    New-AzureRmResourceGroup `
    -Name $RgName `
    -Location $Location
    ```

4. <span data-ttu-id="52b9d-116">Créer un réseau virtuel (VNet) et le sous-réseau Bonjour même emplacement que le groupe de ressources hello :</span><span class="sxs-lookup"><span data-stu-id="52b9d-116">Create a virtual network (VNet) and subnet in hello same location as hello resource group:</span></span>

    ```powershell
    
    # Create a subnet configuration
    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name MySubnet `
    -AddressPrefix 10.0.0.0/24

    # Create a virtual network
    $VNet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $RgName `
    -Location $Location `
    -Name MyVNet `
    -AddressPrefix 10.0.0.0/16 `
    -Subnet $subnetConfig

    # Get hello subnet object
    $Subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $SubnetConfig.Name -VirtualNetwork $VNet
    ```

5. <span data-ttu-id="52b9d-117">Créez un groupe de sécurité réseau (NSG) et une règle.</span><span class="sxs-lookup"><span data-stu-id="52b9d-117">Create a network security group (NSG) and a rule.</span></span> <span data-ttu-id="52b9d-118">Hello NSG sécurise hello machine virtuelle à l’aide des règles de trafic entrants et sortants.</span><span class="sxs-lookup"><span data-stu-id="52b9d-118">hello NSG secures hello VM using inbound and outbound rules.</span></span> <span data-ttu-id="52b9d-119">Dans ce cas, une règle entrante est créée pour le port 3389, qui autorise les connexions Bureau à distance entrantes.</span><span class="sxs-lookup"><span data-stu-id="52b9d-119">In this case, an inbound rule is created for port 3389, which allows incoming remote desktop connections.</span></span>

    ```powershell
    
    # Create an inbound network security group rule for port 3389

    $NSGRule = New-AzureRmNetworkSecurityRuleConfig `
    -Name MyNsgRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 -Access Allow
    
    # Create a network security group
    $NSG = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName $RgName `
    -Location $Location `
    -Name MyNetworkSecurityGroup `
    -SecurityRules $NSGRule
    ```

6. <span data-ttu-id="52b9d-120">Définir la configuration IP du principale hello pour hello carte réseau.</span><span class="sxs-lookup"><span data-stu-id="52b9d-120">Define hello primary IP configuration for hello NIC.</span></span> <span data-ttu-id="52b9d-121">Modification 10.0.0.4 tooa adresse valide dans un sous-réseau hello créé, si vous n’avez pas utilisé la valeur hello précédemment définie.</span><span class="sxs-lookup"><span data-stu-id="52b9d-121">Change 10.0.0.4 tooa valid address in hello subnet you created, if you didn't use hello value defined previously.</span></span> <span data-ttu-id="52b9d-122">Avant d’attribuer une adresse IP statique, il est recommandé de vérifier tout d’abord qu’elle n’est pas déjà utilisée.</span><span class="sxs-lookup"><span data-stu-id="52b9d-122">Before assigning a static IP address, it's recommended that you first confirm it's not already in use.</span></span> <span data-ttu-id="52b9d-123">Entrez la commande hello `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`.</span><span class="sxs-lookup"><span data-stu-id="52b9d-123">Enter hello command `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`.</span></span> <span data-ttu-id="52b9d-124">Si l’adresse de hello est disponible, hello sortie retourne *True*.</span><span class="sxs-lookup"><span data-stu-id="52b9d-124">If hello address is available, hello output returns *True*.</span></span> <span data-ttu-id="52b9d-125">S’il n’est pas disponible, hello sortie retourne *False* et une liste d’adresses qui sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="52b9d-125">If it's not available, hello output returns *False* and a list of addresses that are available.</span></span> 

    <span data-ttu-id="52b9d-126">Bonjour, suivant les commandes, **remplacez < remplacer-avec-your-unique-name > par hello toouse du nom DNS unique.**</span><span class="sxs-lookup"><span data-stu-id="52b9d-126">In hello following commands, **Replace <replace-with-your-unique-name> with hello unique DNS name toouse.**</span></span> <span data-ttu-id="52b9d-127">nom de Hello doit être unique sur toutes les adresses IP publiques au sein d’une région Azure.</span><span class="sxs-lookup"><span data-stu-id="52b9d-127">hello name must be unique across all public IP addresses within an Azure region.</span></span> <span data-ttu-id="52b9d-128">Paramètre facultatif.</span><span class="sxs-lookup"><span data-stu-id="52b9d-128">This is an optional parameter.</span></span> <span data-ttu-id="52b9d-129">Il peut être supprimé si vous souhaitez uniquement tooconnect toohello machine virtuelle à l’aide de l’adresse IP hello.</span><span class="sxs-lookup"><span data-stu-id="52b9d-129">It can be removed if you only want tooconnect toohello VM using hello public IP address.</span></span>

    ```powershell
    
    # Create a public IP address
    $PublicIP1 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP1" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -DomainNameLabel <replace-with-your-unique-name> `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign hello public IP ddress tooit
    $IpConfigName1 = "IPConfig-1"
    $IpConfig1     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName1 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.4 `
    -PublicIpAddress $PublicIP1 `
    -Primary
    ```

    <span data-ttu-id="52b9d-130">Lorsque vous affectez tooa de configurations IP plusieurs cartes réseau, une configuration doit être affectée comme hello *-principal*.</span><span class="sxs-lookup"><span data-stu-id="52b9d-130">When you assign multiple IP configurations tooa NIC, one configuration must be assigned as hello *-Primary*.</span></span>

    > [!NOTE]
    > <span data-ttu-id="52b9d-131">Les adresses IP publiques ont un coût nominal.</span><span class="sxs-lookup"><span data-stu-id="52b9d-131">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="52b9d-132">toolearn en savoir plus sur le protocole IP adresse tarification, lire hello [tarification d’adresse IP](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span><span class="sxs-lookup"><span data-stu-id="52b9d-132">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="52b9d-133">Il existe un toohello limiter le nombre d’adresses IP publiques qui peut être utilisé dans un abonnement.</span><span class="sxs-lookup"><span data-stu-id="52b9d-133">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="52b9d-134">toolearn plus d’informations sur les limites de hello, lire hello [Azure limite](../azure-subscription-service-limits.md#networking-limits) l’article.</span><span class="sxs-lookup"><span data-stu-id="52b9d-134">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

7. <span data-ttu-id="52b9d-135">Définir les configurations IP secondaires hello pour hello carte réseau.</span><span class="sxs-lookup"><span data-stu-id="52b9d-135">Define hello secondary IP configurations for hello NIC.</span></span> <span data-ttu-id="52b9d-136">Vous pouvez ajouter ou supprimer des configurations si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="52b9d-136">You can add or remove configurations as necessary.</span></span> <span data-ttu-id="52b9d-137">Chaque configuration IP doit avoir une adresse IP privée attribuée.</span><span class="sxs-lookup"><span data-stu-id="52b9d-137">Each IP configuration must have a private IP address assigned.</span></span> <span data-ttu-id="52b9d-138">Chaque configuration peut avoir une adresse IP publique attribuée.</span><span class="sxs-lookup"><span data-stu-id="52b9d-138">Each configuration can optionally have one public IP address assigned.</span></span>

    ```powershell
    
    # Create a public IP address
    $PublicIP2 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP2" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign hello public IP ddress tooit
    $IpConfigName2 = "IPConfig-2"
    $IpConfig2     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName2 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.5 `
    -PublicIpAddress $PublicIP2
        
    $IpConfigName3 = "IpConfig-3"
    $IpConfig3 = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IPConfigName3 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.6
    ```

8. <span data-ttu-id="52b9d-139">Créer hello NIC et associer les trois tooit de configurations IP hello :</span><span class="sxs-lookup"><span data-stu-id="52b9d-139">Create hello NIC and associate hello three IP configurations tooit:</span></span>

    ```powershell
    
    $NIC = New-AzureRmNetworkInterface `
    -Name MyNIC `
    -ResourceGroupName $RgName `
    -Location $Location `
    -NetworkSecurityGroupId $NSG.Id `
    -IpConfiguration $IpConfig1,$IpConfig2,$IpConfig3
    ```

    >[!NOTE]
    ><span data-ttu-id="52b9d-140">Bien que toutes les configurations sont affectées tooone NIC dans cet article, vous pouvez affecter plusieurs IP configurations tooevery carte réseau attachée toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="52b9d-140">Though all configurations are assigned tooone NIC in this article, you can assign multiple IP configurations tooevery NIC attached toohello VM.</span></span> <span data-ttu-id="52b9d-141">toolearn comment toocreate une machine virtuelle avec plusieurs cartes réseau, lire hello [créer une machine virtuelle avec plusieurs cartes réseau](virtual-network-deploy-multinic-arm-ps.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="52b9d-141">toolearn how toocreate a VM with multiple NICs, read hello [Create a VM with multiple NICs](virtual-network-deploy-multinic-arm-ps.md) article.</span></span>

9. <span data-ttu-id="52b9d-142">Créer hello machine virtuelle en entrant hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="52b9d-142">Create hello VM by entering hello following commands:</span></span>

    ```powershell
    
    # Define a credential object. When you run these commands, you're prompted tooenter a sername and password for hello VM you're reating.
    $cred = Get-Credential
    
    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
    -VMName MyVM `
    -VMSize Standard_DS1_v2 | `
    Set-AzureRmVMOperatingSystem -Windows `
    -ComputerName MyVM `
    -Credential $cred | `
    Set-AzureRmVMSourceImage `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest | `
    Add-AzureRmVMNetworkInterface `
    -Id $NIC.Id
    
    # Create hello VM
    New-AzureRmVM `
    -ResourceGroupName $RgName `
    -Location $Location `
    -VM $VmConfig
    ```

10. <span data-ttu-id="52b9d-143">Système d’exploitation de l’ordinateur virtuel toohello les adresses IP privée de hello ajouter en procédant comme hello pour votre système d’exploitation Bonjour [ajouter une adresse IP traite le système d’exploitation de l’ordinateur virtuel tooa](#os-config) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="52b9d-143">Add hello private IP addresses toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="52b9d-144">N’ajoutez pas hello publique IP adresses toohello système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="52b9d-144">Do not add hello public IP addresses toohello operating system.</span></span>

## <span data-ttu-id="52b9d-145"><a name="add"></a>Ajouter tooa d’adresses IP virtuelle</span><span class="sxs-lookup"><span data-stu-id="52b9d-145"><a name="add"></a>Add IP addresses tooa VM</span></span>

<span data-ttu-id="52b9d-146">Vous pouvez ajouter privé et public tooa adresses IP réseau en effectuant les étapes hello qui suivent.</span><span class="sxs-lookup"><span data-stu-id="52b9d-146">You can add private and public IP addresses tooa NIC by completing hello steps that follow.</span></span> <span data-ttu-id="52b9d-147">Bonjour Bonjour les sections suivantes supposent que vous avez déjà une machine virtuelle avec des configurations IP hello trois décrites dans hello [scénario](#Scenario) dans cet article, mais il n’est pas nécessaire de procéder.</span><span class="sxs-lookup"><span data-stu-id="52b9d-147">hello examples in hello following sections assume that you already have a VM with hello three IP configurations described in hello [scenario](#Scenario) in this article, but it's not required that you do.</span></span>

1. <span data-ttu-id="52b9d-148">Ouvrez une invite de commandes PowerShell et le complète hello restant des étapes de cette section au sein d’une seule session PowerShell.</span><span class="sxs-lookup"><span data-stu-id="52b9d-148">Open a PowerShell command prompt and complete hello remaining steps in this section within a single PowerShell session.</span></span> <span data-ttu-id="52b9d-149">Si vous n’avez pas encore PowerShell est installé et configuré, hello terminé les étapes Bonjour [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) l’article.</span><span class="sxs-lookup"><span data-stu-id="52b9d-149">If you don't already have PowerShell installed and configured, complete hello steps in hello [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="52b9d-150">Modifier les hello « valeurs » de hello suivant nom de toohello $Variables de hello carte réseau vous souhaitez tooadd IP adresse tooand hello ressource groupe et l’emplacement hello dans QU'ASSOCIATION existe :</span><span class="sxs-lookup"><span data-stu-id="52b9d-150">Change hello "values" of hello following $Variables toohello name of hello NIC you want tooadd IP address tooand hello resource group and location hello NIC exists in:</span></span>

    ```powershell
    $NicName  = "MyNIC"
    $RgName   = "MyResourceGroup"
    $Location = "westus"
    ```

    <span data-ttu-id="52b9d-151">Si vous ne connaissez pas nom hello Hello carte réseau que vous souhaitez toochange, entrez hello suivant de commandes, puis modifier les valeurs hello de variables précédentes de hello :</span><span class="sxs-lookup"><span data-stu-id="52b9d-151">If you don't know hello name of hello NIC you want toochange, enter hello following commands, then change hello values of hello previous variables:</span></span>

    ```powershell
    Get-AzureRmNetworkInterface | Format-Table Name, ResourceGroupName, Location
    ```
3. <span data-ttu-id="52b9d-152">Créer une variable et la définir toohello existant de carte réseau en tapant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="52b9d-152">Create a variable and set it toohello existing NIC by typing hello following command:</span></span>

    ```powershell
    $MyNIC = Get-AzureRmNetworkInterface -Name $NicName -ResourceGroupName $RgName
    ```
4. <span data-ttu-id="52b9d-153">Bonjour suivant de commandes, modifiez *MyVNet* et *MySubnet* toohello les noms de hello réseau virtuel et sous-réseau hello carte réseau est connectée à.</span><span class="sxs-lookup"><span data-stu-id="52b9d-153">In hello following commands, change *MyVNet* and *MySubnet* toohello names of hello VNet and subnet hello NIC is connected to.</span></span> <span data-ttu-id="52b9d-154">Entrez hello commandes tooretrieve hello réseau virtuel et sous-réseau objets hello à que carte réseau est connectée :</span><span class="sxs-lookup"><span data-stu-id="52b9d-154">Enter hello commands tooretrieve hello VNet and subnet objects hello NIC is connected to:</span></span>

    ```powershell
    $MyVNet = Get-AzureRMVirtualnetwork -Name MyVNet -ResourceGroupName $RgName
    $Subnet = $MyVnet.Subnets | Where-Object { $_.Name -eq "MySubnet" }
    ```
    <span data-ttu-id="52b9d-155">Si vous ne connaissez pas hello réseau virtuel ou un sous-réseau nom hello à que carte réseau est connectée, entrez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="52b9d-155">If you don't know hello VNet or subnet name hello NIC is connected to, enter hello following command:</span></span>
    ```powershell
    $MyNIC.IpConfigurations
    ```
    <span data-ttu-id="52b9d-156">Dans la sortie de hello, recherchez toohello similaire de texte suivant l’exemple de sortie :</span><span class="sxs-lookup"><span data-stu-id="52b9d-156">In hello output, look for text similar toohello following example output:</span></span>
    
    ```
    "Id": "/subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/MyVNet/subnets/MySubnet"
    ```
    <span data-ttu-id="52b9d-157">Dans cette sortie, *MyVnet* est hello réseau virtuel et *MySubnet* est hello de sous-réseau hello carte réseau est connectée à.</span><span class="sxs-lookup"><span data-stu-id="52b9d-157">In this output, *MyVnet* is hello VNet and *MySubnet* is hello subnet hello NIC is connected to.</span></span>

5. <span data-ttu-id="52b9d-158">Suivez les étapes de hello dans un des hello les sections, en fonction de vos exigences suivantes :</span><span class="sxs-lookup"><span data-stu-id="52b9d-158">Complete hello steps in one of hello following sections, based on your requirements:</span></span>

    <span data-ttu-id="52b9d-159">**Ajouter une adresse IP privée**</span><span class="sxs-lookup"><span data-stu-id="52b9d-159">**Add a private IP address**</span></span>

    <span data-ttu-id="52b9d-160">tooadd un tooa d’adresse IP privée carte réseau, vous devez créer une configuration IP.</span><span class="sxs-lookup"><span data-stu-id="52b9d-160">tooadd a private IP address tooa NIC, you must create an IP configuration.</span></span> <span data-ttu-id="52b9d-161">Hello commande suivante crée une configuration avec une adresse IP statique 10.0.0.7.</span><span class="sxs-lookup"><span data-stu-id="52b9d-161">hello following command creates a configuration with a static IP address of 10.0.0.7.</span></span> <span data-ttu-id="52b9d-162">Lorsque vous spécifiez une adresse IP statique, il doit être une adresse non utilisée pour le sous-réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="52b9d-162">When specifying a static IP address, it must be an unused address for hello subnet.</span></span> <span data-ttu-id="52b9d-163">Il est recommandé de tester tout d’abord tooensure d’adresse hello est disponible, en entrant hello `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet` commande.</span><span class="sxs-lookup"><span data-stu-id="52b9d-163">It's recommended that you first test hello address tooensure it's available by entering hello `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet` command.</span></span> <span data-ttu-id="52b9d-164">Si l’adresse IP de hello est disponible, hello sortie retourne *True*.</span><span class="sxs-lookup"><span data-stu-id="52b9d-164">If hello IP address is available, hello output returns *True*.</span></span> <span data-ttu-id="52b9d-165">S’il n’est pas disponible, hello sortie retourne *False*et une liste d’adresses qui sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="52b9d-165">If it's not available, hello output returns *False*, and a list of addresses that are available.</span></span>

    ```powershell
    Add-AzureRmNetworkInterfaceIpConfig -Name IPConfig-4 -NetworkInterface `
    $MyNIC -Subnet $Subnet -PrivateIpAddress 10.0.0.7
    ```
    <span data-ttu-id="52b9d-166">Créez autant de configurations que nécessaire, à l’aide de noms de configuration unique et d’adresses IP privées (pour les configurations avec des adresses IP statiques).</span><span class="sxs-lookup"><span data-stu-id="52b9d-166">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    <span data-ttu-id="52b9d-167">Ajouter un système de d’exploitation de hello privé IP adresse toohello machine virtuelle en effectuant les étapes hello pour votre système d’exploitation Bonjour [ajouter une adresse IP traite le système d’exploitation de l’ordinateur virtuel tooa](#os-config) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="52b9d-167">Add hello private IP address toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span>

    <span data-ttu-id="52b9d-168">**Ajouter une adresse IP publique**</span><span class="sxs-lookup"><span data-stu-id="52b9d-168">**Add a public IP address**</span></span>

    <span data-ttu-id="52b9d-169">Une adresse IP publique est ajoutée en associant un tooeither de ressource d’adresse IP publique, une nouvelle configuration IP ou une configuration IP existante.</span><span class="sxs-lookup"><span data-stu-id="52b9d-169">A public IP address is added by associating a public IP address resource tooeither a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="52b9d-170">Effectuez les étapes de hello dans une des sections hello qui suivent, dont vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="52b9d-170">Complete hello steps in one of hello sections that follow, as you require.</span></span>

    > [!NOTE]
    > <span data-ttu-id="52b9d-171">Les adresses IP publiques ont un coût nominal.</span><span class="sxs-lookup"><span data-stu-id="52b9d-171">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="52b9d-172">toolearn en savoir plus sur le protocole IP adresse tarification, lire hello [tarification d’adresse IP](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span><span class="sxs-lookup"><span data-stu-id="52b9d-172">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="52b9d-173">Il existe un toohello limiter le nombre d’adresses IP publiques qui peut être utilisé dans un abonnement.</span><span class="sxs-lookup"><span data-stu-id="52b9d-173">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="52b9d-174">toolearn plus d’informations sur les limites de hello, lire hello [Azure limite](../azure-subscription-service-limits.md#networking-limits) l’article.</span><span class="sxs-lookup"><span data-stu-id="52b9d-174">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
    >

    - <span data-ttu-id="52b9d-175">**Associer hello publique ressource tooa nouveau IP configuration d’adresse IP**</span><span class="sxs-lookup"><span data-stu-id="52b9d-175">**Associate hello public IP address resource tooa new IP configuration**</span></span>
    
        <span data-ttu-id="52b9d-176">Lorsque vous ajoutez une adresse IP publique dans une nouvelle configuration IP, vous devez également ajouter une adresse IP privée, car toutes les configurations IP doivent avoir une adresse IP privée.</span><span class="sxs-lookup"><span data-stu-id="52b9d-176">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="52b9d-177">Vous pouvez ajouter une ressource d’adresse IP publique existante ou en créer une.</span><span class="sxs-lookup"><span data-stu-id="52b9d-177">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="52b9d-178">toocreate un nouveau, entrez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="52b9d-178">toocreate a new one, enter hello following command:</span></span>
    
        ```powershell
        $myPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "myPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location `
        -AllocationMethod Static
        ```

        <span data-ttu-id="52b9d-179">toocreate une nouvelle configuration IP avec une adresse IP privée statique et le hello associés *myPublicIp3* adresse IP publique de ressources d’adresses, entrez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="52b9d-179">toocreate a new IP configuration with a static private IP address and hello associated *myPublicIp3* public IP address resource, enter hello following command:</span></span>

        ```powershell
        Add-AzureRmNetworkInterfaceIpConfig `
        -Name IPConfig-4 `
        -NetworkInterface $myNIC `
        -Subnet $Subnet `
        -PrivateIpAddress 10.0.0.7 `
        -PublicIpAddress $myPublicIp3
        ```

    - <span data-ttu-id="52b9d-180">**Associer hello publique ressource tooan existant IP configuration d’adresse IP**</span><span class="sxs-lookup"><span data-stu-id="52b9d-180">**Associate hello public IP address resource tooan existing IP configuration**</span></span>

        <span data-ttu-id="52b9d-181">Une ressource d’adresse IP publique peut être uniquement la configuration IP tooan associés qui n’en avez pas encore associé.</span><span class="sxs-lookup"><span data-stu-id="52b9d-181">A public IP address resource can only be associated tooan IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="52b9d-182">Vous pouvez déterminer si une configuration IP a une adresse IP publique associée en saisissant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="52b9d-182">You can determine whether an IP configuration has an associated public IP address by entering hello following command:</span></span>

        ```powershell
        $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
        ```

        <span data-ttu-id="52b9d-183">Vous consultez suivant toohello similaire de sortie :</span><span class="sxs-lookup"><span data-stu-id="52b9d-183">You see output similar toohello following:</span></span>

        ```     
        Name       PrivateIpAddress PublicIpAddress                                           Primary
        
        IPConfig-1 10.0.0.4         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress    True
        IPConfig-2 10.0.0.5         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress   False
        IpConfig-3 10.0.0.6                                                                     False
        ```

        <span data-ttu-id="52b9d-184">Depuis hello **PublicIpAddress** colonne *IpConfig-3* est vide, aucune ressource d’adresse IP publique n’est tooit actuellement associé.</span><span class="sxs-lookup"><span data-stu-id="52b9d-184">Since hello **PublicIpAddress** column for *IpConfig-3* is blank, no public IP address resource is currently associated tooit.</span></span> <span data-ttu-id="52b9d-185">Vous pouvez ajouter un existant publique IP adresse ressource tooIpConfig-3, ou entrez hello suivant toocreate commande une :</span><span class="sxs-lookup"><span data-stu-id="52b9d-185">You can add an existing public IP address resource tooIpConfig-3, or enter hello following command toocreate one:</span></span>

        ```powershell
        $MyPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "MyPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location -AllocationMethod Static
        ```

        <span data-ttu-id="52b9d-186">Entrez hello commande hello tooassociate adresse IP publique adresse configuration IP existante toohello ressource nommée suivante *IpConfig-3*:</span><span class="sxs-lookup"><span data-stu-id="52b9d-186">Enter hello following command tooassociate hello public IP address resource toohello existing IP configuration named *IpConfig-3*:</span></span>
    
        ```powershell
        Set-AzureRmNetworkInterfaceIpConfig `
        -Name IpConfig-3 `
        -NetworkInterface $mynic `
        -Subnet $Subnet `
        -PublicIpAddress $myPublicIp3
        ```

6. <span data-ttu-id="52b9d-187">Définir hello carte réseau avec la nouvelle configuration IP de hello en entrant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="52b9d-187">Set hello NIC with hello new IP configuration by entering hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $MyNIC
    ```

7. <span data-ttu-id="52b9d-188">Afficher les adresses IP privées hello et hello toohello attribué ressources IP adresse publique carte réseau en entrant hello la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="52b9d-188">View hello private IP addresses and hello public IP address resources assigned toohello NIC by entering hello following command:</span></span>

    ```powershell   
    $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
    ```
8. <span data-ttu-id="52b9d-189">Ajouter un système de d’exploitation de hello privé IP adresse toohello machine virtuelle en effectuant les étapes hello pour votre système d’exploitation Bonjour [ajouter une adresse IP traite le système d’exploitation de l’ordinateur virtuel tooa](#os-config) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="52b9d-189">Add hello private IP address toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="52b9d-190">N’ajoutez pas hello publique IP adresse toohello système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="52b9d-190">Do not add hello public IP address toohello operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
