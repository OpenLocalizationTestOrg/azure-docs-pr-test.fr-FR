---
title: "aaaCreate une machine virtuelle Azure avec réseau d’accélérée | Documents Microsoft"
description: "Découvrez comment toocreate une machine virtuelle avec l’accélération de mise en réseau."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/10/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 241362891bfe083ab32c2f558be54f63f87c0693
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-with-accelerated-networking"></a>Créer une machine virtuelle avec mise en réseau accélérée

Dans ce didacticiel, vous apprendrez comment toocreate une Machine virtuelle Azure (VM) avec l’accélération de réseau. La mise en réseau accélérée a été mise à disposition générale pour Windows et est proposée en préversion publique pour certaines distributions Linux. Mise en réseau d’accélérée permet tooa de virtualisation (SR-IOV) d’e/s de racine unique machine virtuelle, ce qui améliore considérablement les performances de mise en réseau. Ce chemin d’accès de hautes performances ignore hôte hello à partir du chemin de données hello en réduisant la latence, l’instabilité et l’utilisation du processeur, pour une utilisation avec les plus exigeantes charges de travail réseau hello sur les types de machine virtuelle pris en charge. Hello suivant image montre communication entre les deux machines virtuelles (VM) avec et sans mise en réseau d’accélérée :

![Opérateurs de comparaison](./media/virtual-network-create-vm-accelerated-networking/image1.png)

Sans mise en réseau d’accélérée, le trafic réseau vers et depuis hello machine virtuelle doit parcourir hôte de hello et du commutateur virtuel de hello. commutateur virtuel de Hello fournit toutes les stratégies, telles que réseau des groupes de sécurité, accéder à des listes de contrôle, d’isolement et le trafic réseau virtualisé services toonetwork. toolearn plus d’informations sur les commutateurs virtuels, lire hello [virtualisation de réseau Hyper-V et le commutateur virtuel](https://technet.microsoft.com/library/jj945275.aspx) l’article.

Avec un réseau d’accélérée, le trafic réseau arrive sur l’interface réseau de la machine virtuelle hello (NIC) et est ensuite transféré toohello machine virtuelle. Toutes les stratégies de réseau qui hello commutateur virtuel applique sans mise en réseau d’accélérée sont déchargées et appliquées sur le matériel. Application de la stratégie dans le matériel permet hello NIC tooforward trafic réseau directement toohello machine virtuelle, en ignorant les hôte hello et du commutateur virtuel de hello, tout en conservant toutes les stratégies de hello elle appliquée dans l’hôte de hello.

Hello avantages d’un réseau d’accélérée s’appliquent uniquement toohello ordinateur virtuel sur lequel il est activé sur. Pour de meilleurs résultats de hello, elle est idéale tooenable cette fonctionnalité au moins deux machines virtuelles connectées toohello même réseau virtuel Azure (VNet). Lors de la communication entre les réseaux virtuels ou de la connexion locale, cette fonctionnalité a une latence toooverall un impact minimal.

> [!WARNING]
> Cette Linux version préliminaire publique ne peut pas avoir de hello même niveau de disponibilité et la fiabilité en tant que fonctionnalités qui sont en général version en disponibilité. fonctionnalité de Hello n’est pas pris en charge peut-être avoir limitées des fonctionnalités et ne peut-être pas être disponible dans tous les emplacements Azure. Hello plus récentes des notifications sur disponibilité et l’état de cette fonctionnalité, vérifiez la page mises à jour de réseau virtuel Azure hello.

## <a name="benefits"></a>Avantages
* **Latence inférieure / plus élevé de paquets par seconde (pps) :** suppression hello commutateur à partir du chemin de données hello supprime hello temps paquets dans hôte hello pour le traitement de la stratégie et d’augmente hello le nombre de paquets qui peuvent être traitées à l’intérieur de hello machine virtuelle.
* **Réduit l’instabilité :** commutateur virtuel traitement dépend de hello de stratégie qui a besoin de toobe appliquée et hello charge de travail de hello CPU qui effectue le traitement de hello. Hello stratégie mise en œuvre toohello matériel de déchargement supprime cette variabilité remettre des paquets directement toohello machine virtuelle, la suppression de communication de tooVM hôte hello et toutes les interruptions de logiciel et contexte bascule.
* **Réduit l’utilisation du processeur :** commutateur virtuel de contournement hello dans l’hôte de hello entraîne l’utilisation du processeur accessible sans pour traiter le trafic réseau.

## <a name="Limitations"></a>Limitations
Hello limites suivantes existe lors de l’utilisation de cette fonctionnalité :

* **Création d’interface réseau :** la mise en réseau accélérée ne peut être activée que pour une nouvelle carte réseau. Elle ne peut pas être activée pour une carte réseau existante.
* **Création d’ordinateurs virtuels :** une carte d’interface réseau avec un réseau d’accélérée activée peut uniquement être attachée tooa VM lorsque hello la machine virtuelle est créée. Hello carte réseau ne peut pas être attaché tooan existant de machine virtuelle.
* **Régions :** des machines virtuelles Windows avec mise en réseau accélérée sont proposées dans la plupart des régions Azure. Des machines virtuelles Linux avec mise en réseau accélérée sont proposées dans plusieurs régions. Cette fonctionnalité est disponible dans des régions Hello se développe. Consultez hello Azure virtuel réseau blog mises à jour ci-dessous pour les informations les plus récentes hello.   
* **Systèmes d’exploitation pris en charge :** Windows : Microsoft Windows Server 2012 R2 Datacenter et Windows Server 2016. Linux : Ubuntu Server 16.04 LTS avec noyau 4.4.0-77 ou supérieur, SLES 12 SP2, RHEL 7.3 et CentOS 7.3 (publié par « Rogue Wave Software »).
* **Taille de machine virtuelle :** tailles d’instance à usage général et de calcul optimisé avec au moins huit cœurs. Pour plus d’informations, consultez hello [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) et [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) articles des tailles de machine virtuelle. Hello des tailles prises en charge instance développera Bonjour futures.
* **Déploiement via Azure Resource Manager (ARM) uniquement :** la mise en réseau accélérée n’est pas disponible pour le déploiement via ASM/RDFE.

Modifications toothese limitations sont annoncées via hello [le réseau virtuel Azure met à jour](https://azure.microsoft.com/updates/accelerated-networking-in-preview) page.

## <a name="create-a-windows-vm"></a>Créer une machine virtuelle Windows
Vous pouvez utiliser hello portail Azure ou Azure [PowerShell](#windows-powershell) toocreate hello machine virtuelle.

### <a name="windows-portal"></a>Portail

1. À partir d’un navigateur Internet, ouvrez hello Azure [portal](https://portal.azure.com) et connectez-vous avec votre Azure [compte](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Si vous n’avez pas de compte, vous pouvez vous inscrire pour bénéficier d’un [essai gratuit](https://azure.microsoft.com/offers/ms-azr-0044p).
2. Dans le portail de hello, cliquez sur **+ nouveau** > **de calcul** > **Windows Server 2016 Datacenter**. 
3. Bonjour **Datacenter de Windows Server 2016** panneau qui s’affiche, laissez le champ *le Gestionnaire de ressources* sélectionné sous **sélectionner un modèle de déploiement**, puis cliquez sur **créer** .
4. Bonjour **notions de base** panneau qui s’affiche, entrez hello valeurs suivantes, laissez hello restant des options par défaut ou sélectionnez ou entrez vos propres valeurs, puis cliquez sur hello **OK** bouton :

    |Paramètre|Valeur|
    |---|---|
    |Nom|MyVm|
    |Groupe de ressources|Laissez l’option **Créer un nouveau** activée et entrez *MyResourceGroup*|
    |Lieu|Ouest des États-Unis 2|

    Si vous êtes tooAzure nouvelle, en savoir plus sur [groupes de ressources](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [abonnements](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), et [emplacements](https://azure.microsoft.com/regions) (également appelée le tooas régions).
5. Bonjour **choisir une taille** panneau qui s’affiche, entrez *8* Bonjour **nombre Minimum de cœurs** zone, puis cliquez sur **afficher toutes les**.
6. Cliquez sur **DS4_V2 Standard**, ou tout pris en charge d’ordinateur virtuel, puis cliquez sur hello **sélectionnez** bouton.
7. Bonjour **paramètres** panneau qui s’affiche, conservez tous les paramètres en tant que-est, à l’exception de clic **activé** sous **Accelerated réseau**, puis cliquez sur hello **OK** bouton. **Remarque :** si, dans les étapes précédentes, vous avez sélectionné pour la taille de machine virtuelle, système d’exploitation ou emplacement, les valeurs qui ne sont pas répertoriées dans hello [Limitations](#Limitations) section de cet article, **Accelerated réseau**n’est pas visible.
8. Bonjour **Résumé** panneau qui s’affiche, cliquez sur hello **OK** bouton. Azure démarre la création de hello machine virtuelle. La création de la machine virtuelle prend quelques minutes.
9. tooinstall hello accelerated pilote réseau pour Windows, hello terminé les étapes Bonjour [configurer Windows](#configure-windows) section de cet article.

### <a name="windows-powershell"></a>PowerShell
1. Installez hello dernière version de hello Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module. Si vous êtes nouveau tooAzure PowerShell, lisez hello [vue d’ensemble d’Azure PowerShell](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) l’article.
2. Démarrez une session PowerShell en cliquant sur le bouton Démarrer de Windows hello, en tapant **powershell**, puis en cliquant sur **PowerShell** hello résultats de recherche.
3. Dans la fenêtre PowerShell, entrez hello `login-azurermaccount` toosign de commande avec votre Azure [compte](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Si vous n’avez pas de compte, vous pouvez vous inscrire pour bénéficier d’un [essai gratuit](https://azure.microsoft.com/offers/ms-azr-0044p).
4. Dans votre navigateur, copiez hello script suivant :
    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Windows `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName MicrosoftWindowsServer `
      -Offer WindowsServer `
      -Skus 2016-Datacenter `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id 

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    #
    ```
5. Dans la fenêtre PowerShell, avec le bouton droit de script de hello toopaste et démarrer son exécution. Vous êtes invité à entrer un nom d’utilisateur et un mot de passe. Utilisez ces informations d’identification toolog dans toohello machine virtuelle lors de la connexion tooit à l’étape suivante de hello. Si le script de hello échoue et que vous avez modifié les valeurs dans le script de hello avant son exécution, vérifiez les valeurs hello utilisées pour la taille de machine virtuelle, système d’exploitation, et qu’emplacement sont répertoriés dans hello [Limitations](#Limitations) section de cet article.
6. tooinstall hello accelerated pilote réseau pour Windows, hello terminé les étapes Bonjour [configurer Windows](#configure-windows) section de cet article.

### <a name="configure-windows"></a>Configurer Windows
Une fois que vous créez hello machine virtuelle dans Azure, vous devez installer le pilote de réseau d’accélérée hello pour Windows. Avant d’exécuter hello comme suit, vous devez avoir créé une machine virtuelle Windows avec un réseau d’accélérée à l’aide soit hello [portal](#windows-portal) ou [PowerShell](#windows-powershell) les étapes de cet article. 

1. À partir d’un navigateur Internet, ouvrez hello Azure [portal](https://portal.azure.com) et connectez-vous avec votre Azure [compte](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Si vous n’avez pas de compte, vous pouvez vous inscrire pour bénéficier d’un [essai gratuit](https://azure.microsoft.com/offers/ms-azr-0044p).
2. Dans la zone hello qui contient le texte hello *recherche les ressources* haut hello de hello portail Azure, tapez *MyVm*. Lorsque **MyVm** s’affiche dans les résultats de recherche hello, cliquez dessus.
3. Bonjour **MyVm** panneau qui s’affiche, cliquez sur hello **Connect** bouton hello en haut à gauche du Panneau de hello. **Remarque :** si **création** est visible sous hello **Connect** bouton, Azure n’est pas encore terminée création hello machine virtuelle. Cliquez sur **Connect** uniquement une fois que vous ne voyez plus **création** sous hello **Connect** bouton.
4. Autoriser votre hello toodownload de navigateur **MyVm.rdp** fichier.  Une fois téléchargé, cliquez sur hello fichier tooopen il. 
5. Cliquez sur hello **Connect** bouton Bonjour **connexion Bureau à distance** zone qui s’affiche vous informant que hello éditeur de connexion à distance de hello ne peut pas être identifié.
6. Bonjour **sécurité Windows** zone qui s’affiche, cliquez sur **plus de choix**, puis cliquez sur **utiliser un autre compte**. Entrez le nom d’utilisateur hello et le mot de passe entré à l’étape 4, puis cliquez sur hello **OK** bouton.
7. Cliquez sur hello **Oui** bouton de boîte de connexion Bureau à distance hello qui s’affiche, indiquant que l’identité hello de l’ordinateur distant de hello ne peut pas être vérifiée.
8. Cliquez sur le bouton de démarrage de Windows hello, sur **le Gestionnaire de périphériques**. Développez hello **cartes réseau** nœud. Vérifiez que hello **Mellanox ConnectX-3 virtuel fonction Ethernet adaptateur** s’affiche, comme indiqué dans hello illustration suivante :
   
    ![Gestionnaire de périphériques](./media/virtual-network-create-vm-accelerated-networking/image2.png)

9. La mise en réseau accélérée est maintenant activée pour votre machine virtuelle.

## <a name="create-a-linux-vm"></a>Créer une machine virtuelle Linux
Vous pouvez utiliser hello portail Azure ou Azure [PowerShell](#linux-powershell) toocreate un Ubuntu ou le SLES VM. Le flux de travail est différent pour les machines virtuelles RHEL et CentOS.  Consultez les instructions hello ci-dessous.

### <a name="linux-portal"></a>Portail
1. S’inscrire à hello accéléré mise en réseau pour l’aperçu de Linux en effectuant les étapes 1 à 5 de hello [créer un VM Linux - PowerShell](#linux-powershell) section de cet article.  Impossible d’inscrire pour l’aperçu hello dans le portail de hello.
2. Complète les étapes 1-8 les hello en [créer une machine virtuelle Windows - portail](#windows-portal) section de cet article. À l’étape 2, cliquez sur **Ubuntu Server 16.04 LTS** au lieu de **Windows Server Datacenter 2016**. Pour ce didacticiel, choisissez toouse un mot de passe, plutôt que d’une clé SSH, bien que pour les déploiements de production, vous pouvez utiliser. Si **Accelerated réseau** n’apparaît pas lorsque vous terminez l’étape 7 de hello [créer une machine virtuelle Windows - portail](#windows-portal) section de cet article, il est probablement pour l’une des hello suivant raisons :
    - Vous n’êtes pas encore inscrit pour l’aperçu de hello. Vérifiez que votre état de l’enregistrement est **inscrit**, comme expliqué à l’étape 4 de hello [créer un VM Linux - Powershell](#linux-powershell) section de cet article. **Remarque :** si vous avez participé hello Accelerated mise en réseau pour l’aperçu de machines virtuelles Windows (son aucun toouse tooregister nécessaire plu ne Accelerated mise en réseau pour les machines virtuelles Windows), vous n'êtes pas automatiquement enregistré pour hello Accelerated mise en réseau pour Afficher un aperçu des machines virtuelles Linux. Vous devez vous inscrire pour hello Accelerated mise en réseau pour afficher un aperçu des machines virtuelles Linux tooparticipate qu’il contient.
    - Vous n’avez pas sélectionné une taille de machine virtuelle, système d’exploitation ou emplacement répertorié dans hello [Limitations](#limitations) section de cet article.
3. tooinstall hello accelerated pilote réseau pour Linux, hello terminé les étapes Bonjour [configurer de Linux](#configure-linux) section de cet article.

### <a name="linux-powershell"></a>PowerShell

>[!WARNING]
>Si vous créez les machines virtuelles Linux avec un réseau d’accélérée dans un abonnement et que vous tentez ensuite toocreate une machine virtuelle de Windows avec un réseau d’accélérée Bonjour même abonnement, hello la création de la machine virtuelle Windows risque d’échouer. Dans cette version préliminaire, il est recommandé de tester les machines virtuelles Linux et Windows avec une mise en réseau accélérée dans des abonnements distincts.
>

1. Installez hello dernière version de hello Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module. Si vous êtes nouveau tooAzure PowerShell, lisez hello [vue d’ensemble d’Azure PowerShell](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) l’article.
2. Démarrez une session PowerShell en cliquant sur le bouton Démarrer de Windows hello, en tapant **powershell**, puis en cliquant sur **PowerShell** hello résultats de recherche.
3. Dans la fenêtre PowerShell, entrez hello `login-azurermaccount` toosign de commande avec votre Azure [compte](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Si vous n’avez pas de compte, vous pouvez vous inscrire pour bénéficier d’un [essai gratuit](https://azure.microsoft.com/offers/ms-azr-0044p).
4. S’inscrire à hello accéléré mise en réseau pour Azure preview en complétant hello comme suit :
    - Envoyer un courrier électronique trop[ axnpreview@microsoft.com ](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e) avec votre ID d’abonnement Azure et l’utilisation prévue. Veuillez attendre un e-mail de confirmation de la part de Microsoft concernant l’activation de votre abonnement.
    - Entrez hello suivant tooconfirm de commande que vous êtes inscrit pour l’aperçu de hello :
    
        ```powershell
        Get-AzureRmProviderFeature -FeatureName AllowAcceleratedNetworkingForLinux -ProviderNamespace Microsoft.Network
        ```

        Ne poursuivez pas à l’étape 5 jusqu'à ce que **inscrit** apparaît dans hello de sortie après avoir entré la commande précédente hello. Votre sortie doit ressembler à la suivante hello de sortie avant de continuer :
    
        ```powershell
        FeatureName                        ProviderName      RegistrationState
        -----------                        ------------      -----------------
        AllowAcceleratedNetworkingForLinux Microsoft.Network Registered
        ```
        
      >[!NOTE]
      >Si vous avez participé hello Accelerated mise en réseau pour l’aperçu de machines virtuelles Windows (son aucun toouse tooregister nécessaire plu ne Accelerated mise en réseau pour les machines virtuelles Windows), vous n'êtes pas automatiquement enregistré pour hello Accelerated mise en réseau pour les machines virtuelles Linux preview. Vous devez vous inscrire pour hello Accelerated mise en réseau pour afficher un aperçu des machines virtuelles Linux tooparticipate qu’il contient.
      >
5. Dans votre navigateur, copiez hello suivant le script en remplaçant Ubuntu ou SLES comme vous le souhaitez.  Ici encore, Redhat et CentOS ont un flux de travail différent, décrit ci-dessous :

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Create a new Storage account and define hello new VM’s OSDisk name and its URI
    # Must end with ".vhd" extension
    $OSDiskName = "MyOsDiskName.vhd"
    # Storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.
    $OSDiskSAName = "thestorageaccountname"  
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $RgName -Name $OSDiskSAName -Type "Standard_GRS" -Location $Location
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName
 
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Linux `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName Canonical `
      -Offer UbuntuServer `
      -Skus 16.04-LTS `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk -Name $OSDiskName `
      -VhdUri $OSDiskUri `
      -CreateOption FromImage 

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    ```
    
6. Dans la fenêtre PowerShell, avec le bouton droit de script de hello toopaste et démarrer son exécution. Vous êtes invité à entrer un nom d’utilisateur et un mot de passe. Utilisez ces informations d’identification toolog dans toohello machine virtuelle lors de la connexion tooit à l’étape suivante de hello. Si le script de hello échoue, vérifiez que :
    - Vous êtes inscrit pour l’aperçu de hello, comme expliqué à l’étape 4
    - Si vous avez modifié taille d’ordinateur virtuel, type de système d’exploitation ou les valeurs d’emplacement dans le script de hello avant son exécution, que les valeurs hello sont répertoriés dans hello [Limitations](#Limitations) section de cet article.
7. tooinstall hello accelerated pilote réseau pour Linux, hello terminé les étapes Bonjour [configurer de Linux](#configure-linux) section de cet article.

### <a name="configure-linux"></a>Configurer Linux

Une fois que vous créez hello machine virtuelle dans Azure, vous devez installer le pilote de réseau d’accélérée hello pour Linux. Avant d’exécuter hello comme suit, vous devez avoir créé un VM Linux avec un réseau d’accélérée à l’aide soit hello [portal](#linux-portal) ou [PowerShell](#linux-powershell) les étapes de cet article. 

1. À partir d’un navigateur Internet, ouvrez hello Azure [portal](https://portal.azure.com) et connectez-vous avec votre Azure [compte](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Si vous n’avez pas de compte, vous pouvez vous inscrire pour bénéficier d’un [essai gratuit](https://azure.microsoft.com/offers/ms-azr-0044p).
2. Haut hello hello portail, toohello droite de hello *recherche les ressources* barre, cliquez sur hello **> _** icône toostart un shell de cloud d’un interpréteur de commandes (version préliminaire). Hello Bash cloud shell volet s’affiche en bas de hello du portail de hello et après quelques secondes, présente une  **username@Azure:~ $** invite. Si vous pouvez SSH toohello machine virtuelle à partir de votre ordinateur, plutôt que de shell du cloud hello, instructions hello dans ce didacticiel supposent à l’aide de shell du cloud hello.
3. Haut hello du portail de hello, dans la zone de hello contient texte hello *recherche les ressources*, type *MyVm*. Lorsque **MyVm** s’affiche dans les résultats de recherche hello, cliquez dessus.
4. Bonjour **MyVm** panneau qui s’affiche, cliquez sur hello **Connect** bouton hello en haut à gauche du Panneau de hello. **Remarque :** si **création** est visible sous hello **Connect** bouton, Azure n’est pas encore terminée création hello machine virtuelle. Cliquez sur **Connect** uniquement une fois que vous ne voyez plus **création** sous hello **Connect** bouton.
5. Azure ouvre un message vous en informant tooenter hello `ssh adminuser@<ipaddress>`. Entrez cette commande dans hello cloud shell (ou la copie à partir de la zone hello apparues dans l’étape 4 et le coller dans le shell toohello cloud), puis appuyez sur ENTRÉE.
6. Entrée **Oui** question toohello demandant vous si vous souhaitez que toocontinue vous vous connectez, puis appuyez sur ENTRÉE.
7. Mot de passe hello que vous avez entré lors de la création de hello machine virtuelle. Une fois connecté avec succès toohello machine virtuelle, vous voyez un adminuser@MyVm:~ invite$. Vous êtes désormais connecté toohello machine virtuelle via une session cloud hello. **Remarque :** les sessions de Cloud Shell expirent après 10 minutes d’inactivité.

À ce stade, les instructions de hello varient en fonction distribution hello que vous utilisez. 

#### <a name="ubuntusles"></a>Ubuntu/SLES

1. À l’invite de hello, entrez `uname -r` et vérifiez la version de hello pour :

    * Ubuntu « 4.4.0-77-generic », ou supérieur
    * SLES « 4.4.59-92.20-default » ou supérieur

2. Créer une liaison entre la carte de mise en réseau standard hello et hello accéléré la carte réseau virtuelle mise en réseau par les commandes hello en cours d’exécution qui suivent. Le trafic réseau utilise hello plu performants d’accélérée vNIC mise en réseau, alors que l’obligation de hello garantit que le trafic réseau n’est pas interrompu sur certaines modifications de configuration.
          
     ```bash
     wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/configure_hv_sriov.sh
     chmod +x ./configure_hv_sriov.sh
     sudo ./configure_hv_sriov.sh
     ```
3. Après l’exécution du script hello, hello machine virtuelle redémarre après une seconde 60 suspendre.
4. Une fois hello machine virtuelle est redémarrée, reconnectez tooit en effectuant les étapes 5 à 7 à nouveau.
5. Exécutez hello `ifconfig` commande et confirmer que bond0 n’a rien et interface de hello est affiché comme étant en service. 
 
 >[!NOTE]
      >Applications à l’aide de la mise en réseau d’accélérée doivent communiquer sur hello *bond0* interface non *eth0*.  nom de l’interface Hello peut changer avant la mise en réseau d’accélérée rendue publique.

#### <a name="rhelcentos"></a>RHEL/CentOS

Création d’un Red Hat Enterprise Linux ou la machine virtuelle de CentOS 7.3 requiert certains extra étapes tooload hello pilotes les plus récents nécessaires pour SR-IOV et hello virtuel fonction aucun pilote de carte réseau de hello. Hello première phase d’instructions de hello prépare une image qui peut être utilisé toomake un ou plusieurs ordinateurs virtuels qui ont des pilotes hello préchargés.

##### <a name="phase-one-prepare-a-red-hat-enterprise-linux-or-centos-73-base-image"></a>Phase 1 : préparer une image de base Red Hat Enterprise Linux ou CentOS 7.3. 

1.  Approvisionner une machine virtuelle non-SRIOV CentOS 7.3 sur Azure

2.  Installer LIS 4.2.2 :
    
    ```bash
    wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
    tar -xvf lis-rpms-4.2.2-2.tar.gz
    cd LISISO && sudo ./install.sh
    ```

3.  Télécharger les fichiers de configuration
    
    ```bash
    cd /etc/udev/rules.d/  
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/60-hyperv-vf-name.rules 
    cd /usr/sbin/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/hv_vf_name 
    sudo chmod +x hv_vf_name
    cd /etc/sysconfig/network-scripts/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/ifcfg-vf1   
    ```

4.  Annuler l’approvisionnement de cette machine virtuelle

    ```bash
    sudo waagent -deprovision+user 
    ```

5.  À partir du portail Azure, arrêter cet ordinateur virtuel ; et accédez « Disques » de tooVM, capture URI de hello OSDisk VHD. Cet URI contient le nom de disque dur virtuel de l’image de base hello et son compte de stockage. 
 
##### <a name="phase-two-provision-new-vms-on-azure"></a>Phase 2 : approvisionner de nouvelles machines virtuelles sur Azure

1.  Configurer de nouveaux ordinateurs virtuels en fonction avec New-AzureRMVMConfig à l’aide de hello base image VHD capturé dans la première phase, avec AcceleratedNetworking activé sur une carte réseau virtuelle hello :

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
     -Name $RgName `
     -Location $Location

    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
     -Name MySubnet `
     -AddressPrefix 10.0.0.0/24

    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
     -ResourceGroupName $RgName `
     -Location $Location `
     -Name MyVnet `
     -AddressPrefix 10.0.0.0/16 `
     -Subnet $Subnet
    
    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
     -Name MyPublicIp `
     -ResourceGroupName $RgName `
     -Location $Location `
     -AllocationMethod Static
    
    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
     -Name MyNic `
     -ResourceGroupName $RgName `
     -Location $Location `
     -SubnetId $Vnet.Subnets[0].Id `
     -PublicIpAddressId $Pip.Id `
     -EnableAcceleratedNetworking
    
    # Specify hello base image's VHD URI (from phase one step 5). 
    # Note: hello storage account of this base image vhd should have "Storage service encryption" disabled
    # See more from here: https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption
    # This is just an example URI, you will need tooreplace this when running this script
    $sourceUri="https://myexamplesa.blob.core.windows.net/vhds/CentOS73-Base-Test120170629111341.vhd" 

    # Specify a URI for hello location from which hello new image binary large object (BLOB) is copied toostart hello virtual machine. 
    # Must end with ".vhd" extension
    $OsDiskName = "MyOsDiskName.vhd" 
    $destOsDiskUri = "https://myexamplesa.blob.core.windows.net/vhds/" + $OsDiskName
    
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential
    
    # Create a custom virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
     -VMName MyVM -VMSize Standard_DS4_v2 | `
    Set-AzureRmVMOperatingSystem `
     -Linux `
     -ComputerName myVM `
     -Credential $Cred | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk `
     -Name $OsDiskName `
     -SourceImageUri $sourceUri `
     -VhdUri $destOsDiskUri `
     -CreateOption FromImage `
     -Linux
    
    # Create hello virtual machine.    
    New-AzureRmVM `
     -ResourceGroupName $RgName `
     -Location $Location `
     -VM $VmConfig
    ```

2.  Après l’heure de démarrage des machines virtuelles, appareil de fonction virtuelle hello par « lspci » et vérifiez l’entrée de Mellanox hello. Par exemple, nous devrions voir cet élément dans la sortie de lspci hello :
    
    ```
    0001:00:02.0 Ethernet controller: Mellanox Technologies MT27500/MT27520 Family [ConnectX-3/ConnectX-3 Pro Virtual Function]
    ```
    
3.  Exécutez le script de liaison hello par :

    ```bash
    sudo bondvf.sh
    ```

4.  Redémarrez hello nouvelles machines virtuelles :

    ```bash
    sudo reboot
    ```

Hello machine virtuelle doit commencer par bond0 configuré et hello chemin Accelerated réseau activé.  Exécutez `ifconfig` tooconfirm.
