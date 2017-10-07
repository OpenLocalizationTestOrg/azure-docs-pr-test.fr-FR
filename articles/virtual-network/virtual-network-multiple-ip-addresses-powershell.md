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
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-powershell"></a>Affecter plusieurs adresses IP des ordinateurs de toovirtual à l’aide de PowerShell

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

Cet article explique comment toocreate un ordinateur virtuel (VM) au cours du déploiement d’Azure Resource Manager hello modèle à l’aide de PowerShell. Tooresources créé via le modèle de déploiement classique hello ne peut pas être assignés à plusieurs adresses IP. toolearn plus d’informations sur les modèles de déploiement Azure, lisez hello [comprendre les modèles de déploiement](../resource-manager-deployment-model.md) l’article.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>Créer une machine virtuelle avec plusieurs adresses IP

Hello étapes qui suivent expliquent comment toocreate un exemple de machine virtuelle avec plusieurs IP, les adresses, comme décrit dans le scénario de hello. Modifiez les valeurs des variables en fonction des besoins de votre implémentation.

1. Ouvrez une invite de commandes PowerShell et le complète hello restant des étapes de cette section au sein d’une seule session PowerShell. Si vous n’avez pas encore PowerShell est installé et configuré, hello terminé les étapes Bonjour [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) l’article.
2. Compte de tooyour de connexion avec hello `login-azurermaccount` commande.
3. Remplacez *myResourceGroup* et *westus* par le nom et l’emplacement de votre choix. Créez un groupe de ressources. Un groupe de ressources est un conteneur logique dans lequel les ressources Azure sont déployées et gérées.

    ```powershell
    $RgName   = "MyResourceGroup"
    $Location = "westus"

    New-AzureRmResourceGroup `
    -Name $RgName `
    -Location $Location
    ```

4. Créer un réseau virtuel (VNet) et le sous-réseau Bonjour même emplacement que le groupe de ressources hello :

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

5. Créez un groupe de sécurité réseau (NSG) et une règle. Hello NSG sécurise hello machine virtuelle à l’aide des règles de trafic entrants et sortants. Dans ce cas, une règle entrante est créée pour le port 3389, qui autorise les connexions Bureau à distance entrantes.

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

6. Définir la configuration IP du principale hello pour hello carte réseau. Modification 10.0.0.4 tooa adresse valide dans un sous-réseau hello créé, si vous n’avez pas utilisé la valeur hello précédemment définie. Avant d’attribuer une adresse IP statique, il est recommandé de vérifier tout d’abord qu’elle n’est pas déjà utilisée. Entrez la commande hello `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`. Si l’adresse de hello est disponible, hello sortie retourne *True*. S’il n’est pas disponible, hello sortie retourne *False* et une liste d’adresses qui sont disponibles. 

    Bonjour, suivant les commandes, **remplacez < remplacer-avec-your-unique-name > par hello toouse du nom DNS unique.** nom de Hello doit être unique sur toutes les adresses IP publiques au sein d’une région Azure. Paramètre facultatif. Il peut être supprimé si vous souhaitez uniquement tooconnect toohello machine virtuelle à l’aide de l’adresse IP hello.

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

    Lorsque vous affectez tooa de configurations IP plusieurs cartes réseau, une configuration doit être affectée comme hello *-principal*.

    > [!NOTE]
    > Les adresses IP publiques ont un coût nominal. toolearn en savoir plus sur le protocole IP adresse tarification, lire hello [tarification d’adresse IP](https://azure.microsoft.com/pricing/details/ip-addresses) page. Il existe un toohello limiter le nombre d’adresses IP publiques qui peut être utilisé dans un abonnement. toolearn plus d’informations sur les limites de hello, lire hello [Azure limite](../azure-subscription-service-limits.md#networking-limits) l’article.

7. Définir les configurations IP secondaires hello pour hello carte réseau. Vous pouvez ajouter ou supprimer des configurations si nécessaire. Chaque configuration IP doit avoir une adresse IP privée attribuée. Chaque configuration peut avoir une adresse IP publique attribuée.

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

8. Créer hello NIC et associer les trois tooit de configurations IP hello :

    ```powershell
    
    $NIC = New-AzureRmNetworkInterface `
    -Name MyNIC `
    -ResourceGroupName $RgName `
    -Location $Location `
    -NetworkSecurityGroupId $NSG.Id `
    -IpConfiguration $IpConfig1,$IpConfig2,$IpConfig3
    ```

    >[!NOTE]
    >Bien que toutes les configurations sont affectées tooone NIC dans cet article, vous pouvez affecter plusieurs IP configurations tooevery carte réseau attachée toohello machine virtuelle. toolearn comment toocreate une machine virtuelle avec plusieurs cartes réseau, lire hello [créer une machine virtuelle avec plusieurs cartes réseau](virtual-network-deploy-multinic-arm-ps.md) l’article.

9. Créer hello machine virtuelle en entrant hello suivant de commandes :

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

10. Système d’exploitation de l’ordinateur virtuel toohello les adresses IP privée de hello ajouter en procédant comme hello pour votre système d’exploitation Bonjour [ajouter une adresse IP traite le système d’exploitation de l’ordinateur virtuel tooa](#os-config) section de cet article. N’ajoutez pas hello publique IP adresses toohello système d’exploitation.

## <a name="add"></a>Ajouter tooa d’adresses IP virtuelle

Vous pouvez ajouter privé et public tooa adresses IP réseau en effectuant les étapes hello qui suivent. Bonjour Bonjour les sections suivantes supposent que vous avez déjà une machine virtuelle avec des configurations IP hello trois décrites dans hello [scénario](#Scenario) dans cet article, mais il n’est pas nécessaire de procéder.

1. Ouvrez une invite de commandes PowerShell et le complète hello restant des étapes de cette section au sein d’une seule session PowerShell. Si vous n’avez pas encore PowerShell est installé et configuré, hello terminé les étapes Bonjour [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) l’article.
2. Modifier les hello « valeurs » de hello suivant nom de toohello $Variables de hello carte réseau vous souhaitez tooadd IP adresse tooand hello ressource groupe et l’emplacement hello dans QU'ASSOCIATION existe :

    ```powershell
    $NicName  = "MyNIC"
    $RgName   = "MyResourceGroup"
    $Location = "westus"
    ```

    Si vous ne connaissez pas nom hello Hello carte réseau que vous souhaitez toochange, entrez hello suivant de commandes, puis modifier les valeurs hello de variables précédentes de hello :

    ```powershell
    Get-AzureRmNetworkInterface | Format-Table Name, ResourceGroupName, Location
    ```
3. Créer une variable et la définir toohello existant de carte réseau en tapant hello de commande suivante :

    ```powershell
    $MyNIC = Get-AzureRmNetworkInterface -Name $NicName -ResourceGroupName $RgName
    ```
4. Bonjour suivant de commandes, modifiez *MyVNet* et *MySubnet* toohello les noms de hello réseau virtuel et sous-réseau hello carte réseau est connectée à. Entrez hello commandes tooretrieve hello réseau virtuel et sous-réseau objets hello à que carte réseau est connectée :

    ```powershell
    $MyVNet = Get-AzureRMVirtualnetwork -Name MyVNet -ResourceGroupName $RgName
    $Subnet = $MyVnet.Subnets | Where-Object { $_.Name -eq "MySubnet" }
    ```
    Si vous ne connaissez pas hello réseau virtuel ou un sous-réseau nom hello à que carte réseau est connectée, entrez hello de commande suivante :
    ```powershell
    $MyNIC.IpConfigurations
    ```
    Dans la sortie de hello, recherchez toohello similaire de texte suivant l’exemple de sortie :
    
    ```
    "Id": "/subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/MyVNet/subnets/MySubnet"
    ```
    Dans cette sortie, *MyVnet* est hello réseau virtuel et *MySubnet* est hello de sous-réseau hello carte réseau est connectée à.

5. Suivez les étapes de hello dans un des hello les sections, en fonction de vos exigences suivantes :

    **Ajouter une adresse IP privée**

    tooadd un tooa d’adresse IP privée carte réseau, vous devez créer une configuration IP. Hello commande suivante crée une configuration avec une adresse IP statique 10.0.0.7. Lorsque vous spécifiez une adresse IP statique, il doit être une adresse non utilisée pour le sous-réseau de hello. Il est recommandé de tester tout d’abord tooensure d’adresse hello est disponible, en entrant hello `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet` commande. Si l’adresse IP de hello est disponible, hello sortie retourne *True*. S’il n’est pas disponible, hello sortie retourne *False*et une liste d’adresses qui sont disponibles.

    ```powershell
    Add-AzureRmNetworkInterfaceIpConfig -Name IPConfig-4 -NetworkInterface `
    $MyNIC -Subnet $Subnet -PrivateIpAddress 10.0.0.7
    ```
    Créez autant de configurations que nécessaire, à l’aide de noms de configuration unique et d’adresses IP privées (pour les configurations avec des adresses IP statiques).

    Ajouter un système de d’exploitation de hello privé IP adresse toohello machine virtuelle en effectuant les étapes hello pour votre système d’exploitation Bonjour [ajouter une adresse IP traite le système d’exploitation de l’ordinateur virtuel tooa](#os-config) section de cet article.

    **Ajouter une adresse IP publique**

    Une adresse IP publique est ajoutée en associant un tooeither de ressource d’adresse IP publique, une nouvelle configuration IP ou une configuration IP existante. Effectuez les étapes de hello dans une des sections hello qui suivent, dont vous avez besoin.

    > [!NOTE]
    > Les adresses IP publiques ont un coût nominal. toolearn en savoir plus sur le protocole IP adresse tarification, lire hello [tarification d’adresse IP](https://azure.microsoft.com/pricing/details/ip-addresses) page. Il existe un toohello limiter le nombre d’adresses IP publiques qui peut être utilisé dans un abonnement. toolearn plus d’informations sur les limites de hello, lire hello [Azure limite](../azure-subscription-service-limits.md#networking-limits) l’article.
    >

    - **Associer hello publique ressource tooa nouveau IP configuration d’adresse IP**
    
        Lorsque vous ajoutez une adresse IP publique dans une nouvelle configuration IP, vous devez également ajouter une adresse IP privée, car toutes les configurations IP doivent avoir une adresse IP privée. Vous pouvez ajouter une ressource d’adresse IP publique existante ou en créer une. toocreate un nouveau, entrez hello de commande suivante :
    
        ```powershell
        $myPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "myPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location `
        -AllocationMethod Static
        ```

        toocreate une nouvelle configuration IP avec une adresse IP privée statique et le hello associés *myPublicIp3* adresse IP publique de ressources d’adresses, entrez hello de commande suivante :

        ```powershell
        Add-AzureRmNetworkInterfaceIpConfig `
        -Name IPConfig-4 `
        -NetworkInterface $myNIC `
        -Subnet $Subnet `
        -PrivateIpAddress 10.0.0.7 `
        -PublicIpAddress $myPublicIp3
        ```

    - **Associer hello publique ressource tooan existant IP configuration d’adresse IP**

        Une ressource d’adresse IP publique peut être uniquement la configuration IP tooan associés qui n’en avez pas encore associé. Vous pouvez déterminer si une configuration IP a une adresse IP publique associée en saisissant hello de commande suivante :

        ```powershell
        $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
        ```

        Vous consultez suivant toohello similaire de sortie :

        ```     
        Name       PrivateIpAddress PublicIpAddress                                           Primary
        
        IPConfig-1 10.0.0.4         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress    True
        IPConfig-2 10.0.0.5         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress   False
        IpConfig-3 10.0.0.6                                                                     False
        ```

        Depuis hello **PublicIpAddress** colonne *IpConfig-3* est vide, aucune ressource d’adresse IP publique n’est tooit actuellement associé. Vous pouvez ajouter un existant publique IP adresse ressource tooIpConfig-3, ou entrez hello suivant toocreate commande une :

        ```powershell
        $MyPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "MyPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location -AllocationMethod Static
        ```

        Entrez hello commande hello tooassociate adresse IP publique adresse configuration IP existante toohello ressource nommée suivante *IpConfig-3*:
    
        ```powershell
        Set-AzureRmNetworkInterfaceIpConfig `
        -Name IpConfig-3 `
        -NetworkInterface $mynic `
        -Subnet $Subnet `
        -PublicIpAddress $myPublicIp3
        ```

6. Définir hello carte réseau avec la nouvelle configuration IP de hello en entrant hello de commande suivante :

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $MyNIC
    ```

7. Afficher les adresses IP privées hello et hello toohello attribué ressources IP adresse publique carte réseau en entrant hello la commande suivante :

    ```powershell   
    $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
    ```
8. Ajouter un système de d’exploitation de hello privé IP adresse toohello machine virtuelle en effectuant les étapes hello pour votre système d’exploitation Bonjour [ajouter une adresse IP traite le système d’exploitation de l’ordinateur virtuel tooa](#os-config) section de cet article. N’ajoutez pas hello publique IP adresse toohello système d’exploitation.

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
