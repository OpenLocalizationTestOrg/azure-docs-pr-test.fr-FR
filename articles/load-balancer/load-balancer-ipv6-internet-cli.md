---
title: "équilibrage de charge aaaCreate une côté Internet avec IPv6 - CLI d’Azure | Documents Microsoft"
description: "Découvrez comment toocreate un Internet exposés à équilibrage de charge avec IPv6 à l’aide du Gestionnaire de ressources Azure hello CLI d’Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
keywords: "IPv6, équilibreur de charge azure, double pile, adresse ip publique, ipv6 natif, mobile, iot"
ms.assetid: a1957c9c-9c1d-423e-9d5c-d71449bc1f37
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 7ff75ac90d74a74e3d0c27672b36fbd955a086a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internet-facing-load-balancer-with-ipv6-in-azure-resource-manager-using-hello-azure-cli"></a>Créer un Internet exposés à équilibrage de charge avec IPv6 dans Azure Resource Manager à l’aide de hello CLI d’Azure

> [!div class="op_single_selector"]
> * [PowerShell](load-balancer-ipv6-internet-ps.md)
> * [Interface de ligne de commande Azure](load-balancer-ipv6-internet-cli.md)
> * [Modèle](load-balancer-ipv6-internet-template.md)

Un équilibrage de charge Azure est de type Couche 4 (TCP, UDP). équilibrage de charge Hello offre une haute disponibilité en répartissant le trafic entrant entre les instances de service intègre dans les services de cloud computing ou les machines virtuelles dans un jeu d’équilibrage de charge. Azure Load Balancer peut également présenter ces services sur plusieurs ports, plusieurs adresses IP ou les deux.

## <a name="example-deployment-scenario"></a>Exemple de scénario de déploiement

Hello diagramme suivant illustre la solution d’équilibrage de charge de hello en cours de déploiement à l’aide du modèle d’exemple hello décrit dans cet article.

![Scénario d’équilibreur de charge](./media/load-balancer-ipv6-internet-cli/lb-ipv6-scenario-cli.png)

Dans ce scénario, vous allez créer hello suivant des ressources Azure :

* deux machines virtuelles ;
* une interface de réseau virtuel pour chaque machine virtuelle avec des adresses IPv4 et IPv6 affectées ;
* un équilibrage de charge accessible sur Internet avec une adresse IP publique IPv4 et IPv6 ;
* un toothat à haute disponibilité contient des machines virtuelles de hello deux
* deux charge équilibrage règles toomap hello VIP toohello privés points de terminaison publics

## <a name="deploying-hello-solution-using-hello-azure-cli"></a>Déploiement de solution hello à l’aide de hello CLI d’Azure

Hello suit montrent comment toocreate une connecté à Internet l’équilibrage de charge à l’aide du Gestionnaire de ressources Azure avec l’interface CLI. Avec Azure Resource Manager, chaque ressource est créé et configuré individuellement et puis rassembler toocreate une ressource.

toodeploy un équilibreur de charge, que vous créez et configurez les hello objets suivants :

* Configuration d’adresses IP frontales : contient les adresses IP publiques pour le trafic réseau entrant.
* Pool d’adresses principal - contient des interfaces réseau (NIC) pour le trafic réseau tooreceive de hello machines virtuelles à partir de l’équilibrage de charge hello.
* Règles d’équilibrage de charge - contient des règles de mappage d’un port public sur tooport d’équilibrage de charge hello dans un pool d’adresses de serveur principal hello.
* Les règles NAT de trafic entrant - contient des règles de mappage d’un port public sur le port de tooa d’équilibrage de charge hello pour un ordinateur virtuel spécifique dans le pool d’adresses principal hello.
* Sondes - contient la disponibilité de toocheck les sondes utilisées de contrôle d’intégrité des instances de machines virtuelles dans un pool d’adresses de serveur principal hello.

Pour plus d’informations, consultez [Prise en charge d’un équilibreur de charge par Azure Resource Manager](load-balancer-arm.md).

## <a name="set-up-your-cli-environment-toouse-azure-resource-manager"></a>Configurer votre toouse d’environnement CLI Azure Resource Manager

Pour cet exemple, nous utilisons des outils d’interface CLI hello dans une fenêtre de commande PowerShell. Nous n’utilisons pas d’applets de commande PowerShell Azure hello, mais nous utilisons la lisibilité tooimprove de fonctionnalités et la réutilisation script PowerShell.

1. Si vous n’avez jamais utilisé CLI d’Azure, consultez [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md) et suivez les instructions de hello point toohello où vous sélectionnez votre compte Azure et votre abonnement.
2. Exécutez hello **mode config azure** le mode commande tooswitch tooResource Manager.

    ```azurecli
    azure config mode arm
    ```

    Sortie attendue :

        info:    New mode is arm

3. Connectez-vous à tooAzure et obtenir la liste des abonnements.

    ```azurecli
    azure login
    ```

    À l’invite, entrez vos informations d’identification Azure.

    ```azurecli
    azure account list
    ```

    Choisissez abonnement hello toouse. Prenez note de l’Id d’abonnement hello pour l’étape suivante de hello.

4. Configurer les variables PowerShell pour une utilisation avec les commandes CLI hello.

    ```powershell
    $subscriptionid = "########-####-####-####-############"  # enter subscription id
    $location = "southcentralus"
    $rgName = "pscontosorg1southctrlus09152016"
    $vnetName = "contosoIPv4Vnet"
    $vnetPrefix = "10.0.0.0/16"
    $subnet1Name = "clicontosoIPv4Subnet1"
    $subnet1Prefix = "10.0.0.0/24"
    $subnet2Name = "clicontosoIPv4Subnet2"
    $subnet2Prefix = "10.0.1.0/24"
    $dnsLabel = "contoso09152016"
    $lbName = "myIPv4IPv6Lb"
    ```

## <a name="create-a-resource-group-a-load-balancer-a-virtual-network-and-subnets"></a>Créer un groupe de ressources, un équilibrage de charge, un réseau virtuel et des sous-réseaux

1. Créer un groupe de ressources

    ```azurecli
    azure group create $rgName $location
    ```

2. Créer un équilibrage de charge

    ```azurecli
    $lb = azure network lb create --resource-group $rgname --location $location --name $lbName
    ```

3. Créez un réseau virtuel (VNet).

    ```azurecli
    $vnet = azure network vnet create  --resource-group $rgname --name $vnetName --location $location --address-prefixes $vnetPrefix
    ```

    Créez deux sous-réseaux dans ce réseau virtuel.

    ```azurecli
    $subnet1 = azure network vnet subnet create --resource-group $rgname --name $subnet1Name --address-prefix $subnet1Prefix --vnet-name $vnetName
    $subnet2 = azure network vnet subnet create --resource-group $rgname --name $subnet2Name --address-prefix $subnet2Prefix --vnet-name $vnetName
    ```

## <a name="create-public-ip-addresses-for-hello-front-end-pool"></a>Créer des adresses IP publiques pour le pool frontal de hello

1. Configurer les variables PowerShell hello

    ```powershell
    $publicIpv4Name = "myIPv4Vip"
    $publicIpv6Name = "myIPv6Vip"
    ```

2. Créer un public hello frontal IP pool d’adresses IP.

    ```azurecli
    $publicipV4 = azure network public-ip create --resource-group $rgname --name $publicIpv4Name --location $location --ip-version IPv4 --allocation-method Dynamic --domain-name-label $dnsLabel
    $publicipV6 = azure network public-ip create --resource-group $rgname --name $publicIpv6Name --location $location --ip-version IPv6 --allocation-method Dynamic --domain-name-label $dnsLabel
    ```

    > [!IMPORTANT]
    > équilibrage de charge Hello utilise le nom de domaine hello de l’adresse IP publique hello comme son nom de domaine complet. Cette une modification à partir d’un déploiement classique, ce qui utilise le nom du service cloud hello comme hello d’équilibrage de charge nom de domaine complet.
    > Dans cet exemple, hello nom de domaine complet est *contoso09152016.southcentralus.cloudapp.azure.com*.

## <a name="create-front-end-and-back-end-pools"></a>Créer ds pools frontaux et principaux

Cet exemple crée le pool IP frontal hello qui reçoit le trafic réseau entrant du hello sur l’équilibrage de charge hello et pool d’adresses IP hello principal où pool frontal de hello envoie le trafic à charge équilibrée hello.

1. Configurer les variables PowerShell hello

    ```powershell
    $frontendV4Name = "FrontendVipIPv4"
    $frontendV6Name = "FrontendVipIPv6"
    $backendAddressPoolV4Name = "BackendPoolIPv4"
    $backendAddressPoolV6Name = "BackendPoolIPv6"
    ```

2. Créez un pool IP frontal association d’adresse IP publique hello créé dans l’étape précédente de hello et équilibrage de charge hello.

    ```azurecli
    $frontendV4 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV4Name --public-ip-name $publicIpv4Name --lb-name $lbName
    $frontendV6 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV6Name --public-ip-name $publicIpv6Name --lb-name $lbName
    $backendAddressPoolV4 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV4Name --lb-name $lbName
    $backendAddressPoolV6 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV6Name --lb-name $lbName
    ```

## <a name="create-hello-probe-nat-rules-and-lb-rules"></a>Créer une sonde de hello, des règles NAT et des règles d’équilibrage de charge

Cet exemple crée hello éléments suivants :

* un toocheck de règle de sonde de connectivité tooTCP port 80
* un NAT règle tootranslate tout le trafic entrant sur le port 3389 tooport 3389 pour RDP<sup>1</sup>
* un NAT règle tootranslate tout le trafic entrant sur le port 3391 tooport 3389 pour RDP<sup>1</sup>
* un toobalance de règle d’équilibrage de charge tout le trafic entrant sur le port 80 tooport 80 sur hello adresses dans le pool principal d’hello.

<sup>1</sup> les règles NAT sont instance de machine virtuelle spécifique associé tooa derrière un équilibreur de charge hello. le trafic réseau de Hello arrivant sur le port 3389 est envoyé ordinateur virtuel spécifique de toohello et de port associé à une règle NAT hello. Vous devez spécifier un protocole (TCP ou UDP) pour une règle NAT. Les deux protocoles ne peut pas être assigné toohello même port.

1. Configurer les variables PowerShell hello

    ```powershell
    $probeV4V6Name = "ProbeForIPv4AndIPv6"
    $natRule1V4Name = "NatRule-For-Rdp-VM1"
    $natRule2V4Name = "NatRule-For-Rdp-VM2"
    $lbRule1V4Name = "LBRuleForIPv4-Port80"
    $lbRule1V6Name = "LBRuleForIPv6-Port80"
    ```

2. Création de la sonde de hello

    Hello exemple suivant crée une sonde TCP vérifie pour le port connectivité tooback-end TCP 80 toutes les 15 secondes. Il marque ressources principales de hello indisponible après deux échecs consécutifs.

    ```azurecli
    $probeV4V6 = azure network lb probe create --resource-group $rgname --name $probeV4V6Name --protocol tcp --port 80 --interval 15 --count 2 --lb-name $lbName
    ```

3. Créer des règles NAT entrantes qui autorisent les connexions RDP ressources de back-end toohello

    ```azurecli
    $inboundNatRuleRdp1 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule1V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3389 --backend-port 3389 --lb-name $lbName
    $inboundNatRuleRdp2 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule2V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3391 --backend-port 3389 --lb-name $lbName
    ```

4. Créer des règles qui envoient le trafic toodifferent les ports de back-end en fonction de la requête hello frontal a reçu un équilibreur de charge

    ```azurecli
    $lbruleIPv4 = azure network lb rule create --resource-group $rgname --name $lbRule1V4Name --frontend-ip-name $frontendV4Name --backend-address-pool-name $backendAddressPoolV4Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 80 --lb-name $lbName
    $lbruleIPv6 = azure network lb rule create --resource-group $rgname --name $lbRule1V6Name --frontend-ip-name $frontendV6Name --backend-address-pool-name $backendAddressPoolV6Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 8080 --lb-name $lbName
    ```

5. Vérifier vos paramètres

    ```azurecli
    azure network lb show --resource-group $rgName --name $lbName
    ```

    Sortie attendue :

        info:    Executing command network lb show
        info:    Looking up hello load balancer "myIPv4IPv6Lb"
        data:    Id                              : /subscriptions/########-####-####-####-############/resourceGroups/pscontosorg1southctrlus09152016/providers/Microsoft.Network/loadBalancers/myIPv4IPv6Lb
        data:    Name                            : myIPv4IPv6Lb
        data:    Type                            : Microsoft.Network/loadBalancers
        data:    Location                        : southcentralus
        data:    Provisioning state              : Succeeded
        data:
        data:    Frontend IP configurations:
        data:    Name             Provisioning state  Private IP allocation  Private IP   Subnet  Public IP
        data:    ---------------  ------------------  ---------------------  -----------  ------  ---------
        data:    FrontendVipIPv4  Succeeded           Dynamic                                     myIPv4Vip
        data:    FrontendVipIPv6  Succeeded           Dynamic                                     myIPv6Vip
        data:
        data:    Probes:
        data:    Name                 Provisioning state  Protocol  Port  Path  Interval  Count
        data:    -------------------  ------------------  --------  ----  ----  --------  -----
        data:    ProbeForIPv4AndIPv6  Succeeded           Tcp       80          15        2
        data:
        data:    Backend Address Pools:
        data:    Name             Provisioning state
        data:    ---------------  ------------------
        data:    BackendPoolIPv4  Succeeded
        data:    BackendPoolIPv6  Succeeded
        data:
        data:    Load Balancing Rules:
        data:    Name                  Provisioning state  Load distribution  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    --------------------  ------------------  -----------------  --------  -------------  ------------  ------------------  -----------------------
        data:    LBRuleForIPv4-Port80  Succeeded           Default            Tcp       80             80            false               4
        data:    LBRuleForIPv6-Port80  Succeeded           Default            Tcp       80             8080          false               4
        data:
        data:    Inbound NAT Rules:
        data:    Name                 Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    -------------------  ------------------  --------  -------------  ------------  ------------------  -----------------------
        data:    NatRule-For-Rdp-VM1  Succeeded           Tcp       3389           3389          false               4
        data:    NatRule-For-Rdp-VM2  Succeeded           Tcp       3391           3389          false               4
        info:    network lb show

## <a name="create-nics"></a>Créer des cartes réseau

Créer des cartes réseau et les associer à tooNAT règles, des règles d’équilibrage de charge et des sondes.

1. Configurer les variables PowerShell hello

    ```powershell
    $nic1Name = "myIPv4IPv6Nic1"
    $nic2Name = "myIPv4IPv6Nic2"
    $subnet1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet1Name"
    $subnet2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet2Name"
    $backendAddressPoolV4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV4Name"
    $backendAddressPoolV6Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV6Name"
    $natRule1V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule1V4Name"
    $natRule2V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule2V4Name"
    ```

2. Créez une carte réseau pour chaque instance principale et ajoutez une configuration IPv6.

    ```azurecli
    $nic1 = azure network nic create --name $nic1Name --resource-group $rgname --location $location --private-ip-version "IPv4" --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule1V4Id
    $nic1IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic1Name

    $nic2 = azure network nic create --name $nic2Name --resource-group $rgname --location $location --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule2V4Id
    $nic2IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic2Name
    ```

## <a name="create-hello-back-end-vm-resources-and-attach-each-nic"></a>Créer des ressources d’ordinateur virtuel principal hello et joindre chaque carte réseau

toocreate machines virtuelles, vous devez disposer d’un compte de stockage. Pour l’équilibrage de charge, machines virtuelles de hello doivent toobe les membres d’un ensemble de disponibilité. Pour plus d’informations sur la création des machines virtuelles, consultez la section [Création d’une machine virtuelle Windows à l’aide de Resource Manager et de PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)

1. Configurer les variables PowerShell hello

    ```powershell
    $storageAccountName = "ps08092016v6sa0"
    $availabilitySetName = "myIPv4IPv6AvailabilitySet"
    $vm1Name = "myIPv4IPv6VM1"
    $vm2Name = "myIPv4IPv6VM2"
    $nic1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic1Name"
    $nic2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic2Name"
    $disk1Name = "WindowsVMosDisk1"
    $disk2Name = "WindowsVMosDisk2"
    $osDisk1Uri = "https://$storageAccountName.blob.core.windows.net/vhds/$disk1Name.vhd"
    $osDisk2Uri = "https://$storageAccountName.blob.core.windows.net/vhds/$disk2Name.vhd"
    $imageurn "MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest"
    $vmUserName = "vmUser"
    $mySecurePassword = "PlainTextPassword*1"
    ```

    > [!WARNING]
    > Cet exemple utilise hello username et password pour les machines virtuelles de hello en texte clair. Approprié doit être vigilant lorsqu’à l’aide des informations d’identification Bonjour effacer. Pour obtenir une méthode plus sécurisée de la gestion des informations d’identification dans PowerShell, consultez hello [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) applet de commande.

2. Créer l’ensemble de compte et la disponibilité du stockage hello

    Vous pouvez utiliser un compte de stockage existant lorsque vous créez des machines virtuelles de hello. Hello commande suivante crée un nouveau compte de stockage.

    ```azurecli
    $storageAcc = azure storage account create $storageAccountName --resource-group $rgName --location $location --sku-name "LRS" --kind "Storage"
    ```

    Ensuite, créez le groupe à haute disponibilité hello.

    ```azurecli
    $availabilitySet = azure availset create --name $availabilitySetName --resource-group $rgName --location $location
    ```

3. Créer des machines virtuelles de hello avec des cartes réseau de hello associé

    ```azurecli
    $vm1 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm1Name --nic-id $nic1Id --os-disk-vhd $osDisk1Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension

    $vm2 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm2Name --nic-id $nic2Id --os-disk-vhd $osDisk2Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension
    ```

## <a name="next-steps"></a>Étapes suivantes

[Prise en main de la configuration d’un équilibrage de charge interne](load-balancer-get-started-ilb-arm-cli.md)

[Configuration d'un mode de distribution d'équilibrage de charge](load-balancer-distribution-mode.md)

[Configuration des paramètres du délai d’expiration TCP inactif pour votre équilibrage de charge](load-balancer-tcp-idle-timeout.md)
