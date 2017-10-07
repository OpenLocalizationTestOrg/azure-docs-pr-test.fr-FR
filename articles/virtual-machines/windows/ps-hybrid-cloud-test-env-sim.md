---
title: environnement de test de cloud hybride aaaSimulated | Documents Microsoft
description: "Créez une simulation d'environnement de cloud hybride pour exécuter des tests informatiques ou de développement, à l'aide de deux réseaux virtuels Azure et d'une connexion de réseau virtuel à réseau virtuel."
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ca5bf294-8172-44a9-8fed-d6f38d345364
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.openlocfilehash: 6063022e373c2b3564e040c4fbee122e2438974b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-simulated-hybrid-cloud-environment-for-testing"></a>Configuration d’une simulation d’environnement de cloud hybride à des fins de test
Cet article vous présente la création d'un environnement de cloud hybride simulé avec Microsoft Azure à l'aide de deux réseaux virtuels Azure. Voici la configuration obtenue de hello.

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

Elle simule un environnement de production cloud hybride et est constituée des éléments suivants :

* Un réseau simulé et simplifiée local hébergé dans un réseau virtuel Azure (réseau virtuel hello labo de test).
* Un réseau virtuel entre sites simulé hébergé dans Azure (TestVNET).
* Connexion au réseau entre les réseaux virtuels hello deux.
* Un contrôleur de domaine secondaire dans le réseau virtuel de TestVNET hello.

Elle fournit une base et un point de départ commun pour :

* Développer et tester des applications dans une simulation d’environnement de cloud hybride.
* Créer des configurations de test des ordinateurs, certains au sein du réseau virtuel du labo de test hello et certaines au sein du réseau virtuel hello TestVNET, charges de travail informatique en nuage hybride toosimulate.

Il existe quatre principales phases toosetting, cet environnement de test de cloud hybride :

1. Configurer un réseau virtuel de hello labo de test.
2. Créer un réseau virtuel intersite de hello.
3. Créer un réseau VPN hello au réseau.
4. Configurer DC2. 

Cette configuration nécessite un abonnement Azure. Si vous avez un abonnement MSDN ou Visual Studio, consultez [Crédit Azure mensuel pour les abonnés Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).

> [!NOTE]
> Les machines virtuelles et les passerelles de réseau virtuel dans Azure entraînent des frais lors de leur utilisation. Ce coût est facturé en fonction de votre abonnement MSDN ou de votre abonnement payant. La passerelle VPN Azure est implémentée comme un ensemble de deux machines virtuelles. toominimize les coûts de hello, créer l’environnement de test hello et réalisez votre nécessaires test et démonstration aussi rapidement que possible.
> 
> 

## <a name="phase-1-configure-hello-testlab-virtual-network"></a>Phase 1 : Configurer le réseau virtuel de hello labo de test
Utilisez les instructions hello hello [environnement de test Configuration de Base](https://technet.microsoft.com/library/mt771177.aspx) rubrique tooconfigure hello DC1, APP1 et CLIENT1 ordinateurs Bonjour réseau virtuel Azure nommé labo de test. 

Ensuite, démarrez une invite de commandes Azure PowerShell.

> [!NOTE]
> Hello ensembles de commande suivants utiliser Azure PowerShell 1.0 et versions ultérieur.
> 
> 

Tooyour compte de connexion.

    Login-AzureRMAccount

Obtenir le nom de votre abonnement à l’aide de hello commande suivante.

    Get-AzureRMSubscription | Sort SubscriptionName | Select SubscriptionName

Définissez votre abonnement Azure. Utilisez hello même abonnement que vous avez utilisé toobuild votre configuration de base à la Phase 1. Remplacez tout le contenu du devis hello, notamment hello < et >, avec le nom correct de hello.

    $subscr="<subscription name>"
    Get-AzureRmSubscription –SubscriptionName $subscr | Select-AzureRmSubscription

Ensuite, ajoutez un passerelle sous-réseau toohello labo de test réseau virtuel de votre configuration de base, qui sera utilisé toohost hello passerelle Azure.

    $rgName="<name of your resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed hello TestLab virtual network, such as West US>"
    $vnet=Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name TestLab
    Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 10.255.255.248/29 -VirtualNetwork $vnet
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet

Ensuite, demander une passerelle de toohello publique des tooassign d’adresse IP pour le réseau virtuel de hello labo de test.

    $gwpip=New-AzureRmPublicIpAddress -Name TestLab_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic

Ensuite, créez votre passerelle.

    $vnet=Get-AzureRmVirtualNetwork -Name TestLab -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name TestLab_GWConfig -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id 
    New-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

Gardez à l’esprit que les nouvelles passerelles peuvent prendre 20 minutes ou plus toocreate.

Hello portail Azure sur votre ordinateur local, connectez-vous avec les informations d’identification CORP\User1 de hello tooDC1. domaine CORP de hello tooconfigure afin que les utilisateurs et les ordinateurs utilisent leur contrôleur de domaine local pour l’authentification, exécutez ces commandes à partir d’une invite de commandes de Windows PowerShell de niveau administrateur sur DC1.

    New-ADReplicationSite -Name "TestLab" 
    New-ADReplicationSite -Name "TestVNET"
    New-ADReplicationSubnet -Name "10.0.0.0/8" -Site "TestLab"
    New-ADReplicationSubnet -Name "192.168.0.0/16" -Site "TestVNET"

Ceci est votre configuration actuelle.

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph1.png)

## <a name="phase-2-create-hello-testvnet-virtual-network"></a>Phase 2 : Créer le réseau virtuel de hello TestVNET
D’abord créer le réseau virtuel de TestVNET hello et protéger à l’aide d’un groupe de sécurité réseau.

    $rgName="<name of hello resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed hello TestLab virtual network, such as West US>"
    $locShortName="<Azure location name from $locName in all lowercase letters with spaces removed. Example:  westus>"
    $testSubnet=New-AzureRMVirtualNetworkSubnetConfig -Name "TestSubnet" -AddressPrefix 192.168.0.0/24
    $gatewaySubnet=New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 192.168.255.248/29
    New-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName -Location $locName -AddressPrefix 192.168.0.0/16 -Subnet $testSubnet,$gatewaySubnet –DNSServer 10.0.0.4
    $rule1=New-AzureRMNetworkSecurityRuleConfig -Name "RDPTraffic" -Description "Allow RDP tooall VMs on hello subnet" -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * -DestinationPortRange 3389
    New-AzureRMNetworkSecurityGroup -Name "TestSubnet" -ResourceGroupName $rgName -Location $locShortName -SecurityRules $rule1
    $vnet=Get-AzureRMVirtualNetwork -ResourceGroupName $rgName -Name TestVNET
    $nsg=Get-AzureRMNetworkSecurityGroup -Name "TestSubnet" -ResourceGroupName $rgName
    Set-AzureRMVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet" -AddressPrefix 192.168.0.0/24 -NetworkSecurityGroup $nsg

Ensuite, demande un toobe d’adresse IP publique allouée toohello passerelle pour réseau virtuel de TestVNET hello et créer votre passerelle.

    $gwpip=New-AzureRmPublicIpAddress -Name TestVNET_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $vnet=Get-AzureRmVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name "TestVNET_GWConfig" -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
    New-AzureRmVirtualNetworkGateway -Name "TestVNET_GW" -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

Ceci est votre configuration actuelle.

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph2.png)

## <a name="phase-3-create-hello-vnet-to-vnet-connection"></a>Phase 3 : Créer des connexions de hello au réseau
Tout d'abord, obtenez une clé prépartagée, aléatoire, à chiffrement fort, de 32 caractères auprès de votre administrateur réseau ou de sécurité. Vous pouvez également utiliser les informations de hello à [créer une chaîne aléatoire pour une clé prépartagée IPsec](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx) tooobtain une clé prépartagée.

Ensuite, utilisez ces commandes toocreate hello au réseau VPN de connexion, ce qui peut prendre quelques toocomplete de temps.

    $sharedKey="<pre-shared key value>"
    $gwTestLab=Get-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName
    $gwTestVNET=Get-AzureRmVirtualNetworkGateway -Name TestVNET_GW -ResourceGroupName $rgName
    New-AzureRmVirtualNetworkGatewayConnection -Name TestLab_to_TestVNET -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestLab -VirtualNetworkGateway2 $gwTestVNET -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey
    New-AzureRmVirtualNetworkGatewayConnection -Name TestVNET_to_TestLab -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestVNET -VirtualNetworkGateway2 $gwTestLab -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey

Après quelques minutes, la connexion de hello doit être établie.

Ceci est votre configuration actuelle.

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph3.png)

## <a name="phase-4-configure-dc2"></a>Phase 4 : configurer DC2
Créez d’abord une machine virtuelle pour DC2. Exécutez ces commandes à l’invite de commande Azure PowerShell hello sur votre ordinateur local.

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<hello storage account name for hello base configuration>"
    $vnet=Get-AzureRMVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $pip=New-AzureRMPublicIpAddress -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -PrivateIpAddress 192.168.0.4
    $vm=New-AzureRMVMConfig -VMName DC2 -VMSize Standard_A1
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/DC2-TestVNET-ADDSDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name ADDS-Data -DiskSizeInGB 20 -VhdUri $vhdURI  -CreateOption empty
    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for DC2."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName DC2 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/DC2-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name DC2-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

Connectez-vous ensuite toohello DC2 machine virtuelle à partir de hello portail Azure.

Ensuite, configurez un trafic de tooallow de règle de pare-feu Windows pour le test de connectivité de base. À partir d’une invite de commandes Windows PowerShell de niveau administrateur sur DC2, exécutez ces commandes.

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc1.corp.contoso.com

commande ping de Hello doit aboutir à quatre réponses de réussite de l’adresse IP 10.0.0.4. Ceci est un test de trafic entre hello connexion de réseau virtuel à réseau virtuel.

Ensuite, ajoutez hello disque de données supplémentaire sur DC2 en tant que nouveau volume avec la lettre de lecteur hello F:.

1. Dans le volet gauche hello du Gestionnaire de serveur, cliquez sur **File and Storage Services**, puis cliquez sur **disques**.
2. Dans le volet du sommaire hello, Bonjour **disques** , cliquez sur **disque 2** (avec hello **Partition** défini trop**inconnu**).
3. Cliquez sur **Tâches**, puis sur **Nouveau volume**.
4. Sur hello avant de commencer, page de hello Assistant Nouveau Volume, cliquez sur **suivant**.
5. Sur le serveur hello Select de hello et page de disque, cliquez sur **Disk 2**, puis cliquez sur **suivant**. À l’invite, cliquez sur **OK**.
6. Dans spécifier la taille de page de volume hello hello de hello, cliquez sur **suivant**.
7. Hello Assign tooa lecteur lettre ou un dossier de page, cliquez sur **suivant**.
8. Dans la page des paramètres système hello sélectionner un fichier, cliquez sur **suivant**.
9. Dans hello page Confirmer les sélections, cliquez sur **créer**.
10. Lorsque vous avez terminé, cliquez sur **Fermer**.

Ensuite, configurez DC2 en tant que contrôleur de domaine répliqué pour le domaine corp.contoso.com hello. Exécutez ces commandes à partir de l’invite de commandes Windows PowerShell hello sur DC2.

    Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
    Install-ADDSDomainController -Credential (Get-Credential CORP\User1) -DomainName "corp.contoso.com" -InstallDns:$true -DatabasePath "F:\NTDS" -LogPath "F:\Logs" -SysvolPath "F:\SYSVOL"

Notez que vous êtes invité à toosupply à la fois hello CORP\User1 le mot de passe et un mot de passe en Mode de restauration des Services annuaire (DSRM) et toorestart DC2.

Maintenant que hello TestVNET réseau virtuel n’a son propre serveur DNS (DC2), vous devez configurer ce serveur DNS toouse de réseau virtuel TestVNET hello.

1. Dans le volet gauche de hello Hello portail Azure, cliquez sur icône de réseaux virtuels hello, puis cliquez sur **TestVNET**.
2. Sur hello **paramètres** , cliquez sur **serveurs DNS**.
3. Dans **serveur DNS principal**, type **192.168.0.4** tooreplace 10.0.0.4.
4. Cliquez sur **Enregistrer**.

Ceci est votre configuration actuelle. 

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

Votre environnement de cloud hybride simulé est maintenant prêt pour les tests.

## <a name="next-step"></a>Étape suivante
* Configurez une [application métier basée sur le web](ps-hybrid-cloud-test-env-lob.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) dans cet environnement.

