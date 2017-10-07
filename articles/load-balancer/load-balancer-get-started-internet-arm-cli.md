---
title: "aaaCreate une côté Internet l’équilibrage de charge - CLI d’Azure | Documents Microsoft"
description: "Découvrez comment toocreate un équilibrage de charge exposés à Internet à l’aide du Gestionnaire de ressources hello CLI d’Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a8bcdd88-f94c-4537-8143-c710eaa86818
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: cadb5edb3b4a4e2f0813109d027eaafdc7ef7303
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-load-balancer-using-hello-azure-cli"></a>Création d’un équilibrage de charge d’internet à l’aide de hello CLI d’Azure

> [!div class="op_single_selector"]
> * [Portail](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [Interface de ligne de commande Azure](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [Modèle](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Cet article décrit le modèle de déploiement du Gestionnaire de ressources hello. Vous pouvez également [apprendre comment toocreate une connecté à Internet à l’aide de déploiement classique de l’équilibrage de charge](load-balancer-get-started-internet-classic-portal.md)

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-hello-solution-using-hello-azure-cli"></a>Déploiement de solution hello à l’aide de hello CLI d’Azure

Hello suit montrent comment toocreate une connecté à Internet l’équilibrage de charge à l’aide du Gestionnaire de ressources Azure avec l’interface CLI. Avec Azure Resource Manager chaque ressource est créé et configuré individuellement, puis mis au point toocreate une ressource.

Vous devez créer et configurer hello suivant objets toodeploy un équilibreur de charge :

* Configuration d’adresses IP frontales : contient les adresses IP publiques pour le trafic réseau entrant.
* Pool d’adresses principal - contient des interfaces réseau (NIC) pour le trafic réseau tooreceive de hello machines virtuelles à partir de l’équilibrage de charge hello.
* Règles d’équilibrage de charge - contient des règles de mappage d’un port public sur tooport d’équilibrage de charge hello dans un pool d’adresses de serveur principal hello.
* Les règles NAT de trafic entrant - contient des règles de mappage d’un port public sur le port de tooa d’équilibrage de charge hello pour un ordinateur virtuel spécifique dans le pool d’adresses principal hello.
* Sondes - contient la disponibilité de toocheck les sondes utilisées de contrôle d’intégrité des instances de machines virtuelles dans un pool d’adresses de serveur principal hello.

Pour plus d’informations, consultez [Prise en charge d’un équilibrage de charge par Azure Resource Manager](load-balancer-arm.md).

## <a name="set-up-cli-toouse-resource-manager"></a>Configurer CLI toouse Gestionnaire de ressources

1. Si vous n’avez jamais utilisé CLI d’Azure, consultez [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md) et suivez les instructions de hello point toohello où vous sélectionnez votre compte Azure et votre abonnement.
2. Exécutez hello **configuration azure mode** mode Manager tooResource commande tooswitch, comme indiqué ci-dessous.

    ```azurecli
        azure config mode arm
    ```

    Sortie attendue :

        info:    New mode is arm

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a>Créer un réseau virtuel et une adresse IP publique hello frontal pool d’adresses IP

1. Créer un réseau virtuel (VNet) nommé *NRPVnet* dans l’emplacement d’États-Unis hello à l’aide d’un groupe de ressources nommé *NRPRG*.

    ```azurecli
        azure network vnet create NRPRG NRPVnet eastUS -a 10.0.0.0/16
    ```

    Créez un sous-réseau nommé *NRPVnetSubnet* avec un bloc CIDR 10.0.0.0/24 dans *NRPVnet*.

    ```azurecli
        azure network vnet subnet create NRPRG NRPVnet NRPVnetSubnet -a 10.0.0.0/24
    ```

2. Créer une adresse IP publique nommée *NRPPublicIP* toobe utilisé par un pool IP frontal portant le nom DNS *loadbalancernrp.eastus.cloudapp.azure.com*. commande hello ci-dessous utilise le type d’allocation statique hello et délai d’inactivité de 4 minutes.

    ```azurecli
        azure network public-ip create -g NRPRG -n NRPPublicIP -l eastus -d loadbalancernrp -a static -i 4
    ```

   > [!IMPORTANT]
   > équilibrage de charge Hello utilisera le nom de domaine hello de l’adresse IP publique hello en tant que son nom de domaine complet. Cette une modification à partir d’un déploiement classique, ce qui utilise le service de cloud computing hello comme hello d’équilibrage de charge nom de domaine complet (FQDN).
   > Dans cet exemple, hello nom de domaine complet est *loadbalancernrp.eastus.cloudapp.azure.com*.

## <a name="create-a-load-balancer"></a>Créer un équilibrage de charge

Hello de commande suivant crée un équilibreur de charge nommé *NRPlb* Bonjour *NRPRG* groupe de ressources dans hello *États-Unis* emplacement Azure.

    ```azurecli
    azure network lb create NRPRG NRPlb eastus
    ```

## <a name="create-a-front-end-ip-pool-and-a-backend-address-pool"></a>Création d’un pool d’adresses IP frontales et d’un pool d’adresses principales
Cet exemple montre comment les toocreate hello IP pool frontal qui reçoit le trafic réseau entrant du hello sur hello l’équilibrage de charge et hello du pool d’adresses IP de serveur principal où pool frontal de hello envoie le trafic à charge équilibrée hello.

1. Créez un pool IP frontal association d’adresse IP publique hello créé dans l’étape précédente de hello et équilibrage de charge hello.

    ```azurecli
        azure network lb frontend-ip create nrpRG NRPlb NRPfrontendpool -i nrppublicip
    ```

2. Configurer un pool d’adresses de serveur principal utilisé tooreceive du trafic entrant à partir du pool d’adresses IP frontal hello.

    ```azurecli
        azure network lb address-pool create NRPRG NRPlb NRPbackendpool
    ```

## <a name="create-lb-rules-nat-rules-and-probe"></a>Créer des règles LB, des règles NAT et de sonde

Cet exemple crée hello éléments suivants.

* la règle NAT tootranslate tout le trafic entrant sur le port 21 tooport 22<sup>1</sup>
* la règle NAT tootranslate tout le trafic entrant sur le port 23 tooport 22
* un toobalance de règle d’équilibrage de charge tout le trafic entrant sur le port 80 tooport 80 sur hello adresses dans le pool principal d’hello.
* un état d’intégrité sonde règle toocheck hello, dans une page nommée *HealthProbe.aspx*.

<sup>1</sup> les règles NAT sont instance de machine virtuelle spécifique associé tooa derrière un équilibreur de charge hello. le trafic réseau de Hello arrivant sur le port 21 est envoyé tooa les ordinateur virtuel spécifique sur le port 22 associé à cette règle NAT. Vous devez spécifier un protocole (TCP ou UDP) pour une règle NAT. Les deux protocoles ne peut pas être assigné toohello même port.

1. Créer des règles NAT hello.

    ```azurecli
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh1 --protocol tcp --frontend-port 21 --backend-port 22
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh2 --protocol tcp --frontend-port 23 --backend-port 22
    ```

2. Créez une règle d’équilibreur de charge.

    ```azurecli
        azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule --protocol tcp --frontend-port 80 --backend-port 80 --frontend-ip-name NRPfrontendpool --backend-address-pool-name NRPbackendpool
    ```

3. Créer une sonde d’intégrité.

    ```azurecli
        azure network lb probe create --resource-group nrprg --lb-name nrplb --name healthprobe --protocol "http" --port 80 --path healthprobe.aspx --interval 15 --count 4
    ```

4. Enregistrer vos paramètres.

    ```azurecli
        azure network lb show nrprg nrplb
    ```

    Sortie attendue :

        info:    Executing command network lb show
        + Looking up hello load balancer "nrplb"
        + Looking up hello public ip "NRPPublicIP"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb
        data:    Name                            : nrplb
        data:    Type                            : Microsoft.Network/loadBalancers
        data:    Location                        : eastus
        data:    Provisioning State              : Succeeded
        data:    Frontend IP configurations:
        data:      Name                          : NRPfrontendpool
        data:      Provisioning state            : Succeeded
        data:      Public IP address id          : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/publicIPAddresses/NRPPublicIP
        data:      Public IP allocation method   : Static
        data:      Public IP address             : 40.114.13.145
        data:
        data:    Backend address pools:
        data:      Name                          : NRPbackendpool
        data:      Provisioning state            : Succeeded
        data:
        data:    Load balancing rules:
        data:      Name                          : HTTP
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 80
        data:      Backend port                  : 80
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:      Backend address pool          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:
        data:    Inbound NAT rules:
        data:      Name                          : ssh1
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 21
        data:      Backend port                  : 22
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:
        data:      Name                          : ssh2
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 23
        data:      Backend port                  : 22
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:
        data:    Probes:
        data:      Name                          : healthprobe
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Http
        data:      Port                          : 80
        data:      Interval in seconds           : 15
        data:      Number of probes              : 4
        data:
        info:    network lb show command OK

## <a name="create-nics"></a>Créer des cartes réseau

Vous devez toocreate NIC (ou modifier des modèles existants) et les associer à des règles de tooNAT, des règles d’équilibrage de charge et des sondes.

1. Créez une carte réseau nommée *être lb-nic1*et l’associer à hello *rdp1* NAT règle et hello *NRPbackendpool* pool d’adresses du serveur principal.

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" eastus
    ```

    Sortie attendue :

        info:    Executing command network nic create
        + Looking up hello network interface "lb-nic1-be"
        + Looking up hello subnet "nrpvnetsubnet"
        + Creating network interface "lb-nic1-be"
        + Looking up hello network interface "lb-nic1-be"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        data:    Name                            : lb-nic1-be
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : eastus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 10.0.0.4
        data:      Private IP Allocation Method  : Dynamic
        data:      Subnet                        : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet
        data:      Load balancer backend address pools
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:      Load balancer inbound NAT rules:
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1
        data:
        info:    network nic create command OK

2. Créez une carte réseau nommée *être lb-nic2*et l’associer à hello *rdp2* NAT règle et hello *NRPbackendpool* pool d’adresses du serveur principal.

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" eastus
    ```

3. Créer un ordinateur virtuel (VM) nommé *web1*et l’associer à hello carte réseau nommée *être lb-nic1*. Un compte de stockage appelée *web1nrp* a été créé avant d’exécuter la commande hello ci-dessous.

    ```azurecli
        azure vm create --resource-group nrprg --name web1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

    > [!IMPORTANT]
    > Machines virtuelles dans un toobe de nécessité d’équilibrage de charge dans hello même groupe à haute disponibilité. Utilisez `azure availset create` toocreate un ensemble de disponibilité.

    sortie de Hello sont similaires toohello suivants :

        info:    Executing command vm create
        + Looking up hello VM "web1"
        Enter username: azureuser
        Enter password for azureuser: *********
        Confirm password: *********
        info:    Using hello VM Size "Standard_A1"
        info:    hello [OS, Data] Disk or image configuration requires storage account
        + Looking up hello storage account web1nrp
        + Looking up hello availability set "nrp-avset"
        info:    Found an Availability set "nrp-avset"
        + Looking up hello NIC "lb-nic1-be"
        info:    Found an existing NIC "lb-nic1-be"
        info:    Found an IP configuration with virtual network subnet id "/subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet" in hello NIC "lb-nic1-be"
        info:    This is a NIC without publicIP configured
        + Creating VM "web1"
        info:    vm create command OK

    > [!NOTE]
    > message d’information de type Hello **il s’agit d’une carte réseau sans adresse IP publique configurée** est attendu dans la mesure où hello NIC créée pour l’équilibrage de charge hello connexion tooInternet à l’aide de l’adresse publique IP hello charge équilibrage.

    Depuis hello *être lb-nic1* carte réseau est associé à hello *rdp1* de règle NAT, vous pouvez vous connecter trop*web1* utilisant le protocole RDP via le port 3441 sur l’équilibrage de charge hello.

4. Créer un ordinateur virtuel (VM) nommé *web2*et l’associer à hello carte réseau nommée *être lb-nic2*. Un compte de stockage appelée *web1nrp* a été créé avant d’exécuter la commande hello ci-dessous.

    ```azurecli
        azure vm create --resource-group nrprg --name web2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="update-an-existing-load-balancer"></a>Mettre à jour un équilibreur de charge existant
Vous pouvez ajouter des règles faisant référence à l’équilibrage de charge existant. Dans l’exemple suivant de hello, une nouvelle règle d’équilibreur de charge est ajoutée à équilibrage de charge existant tooan **NRPlb**

```azurecli
azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule2 --protocol tcp --frontend-port 8080 --backend-port 8051 --frontend-ip-name frontendnrppool --backend-address-pool-name NRPbackendpool
```

## <a name="delete-a-load-balancer"></a>Suppression d’un équilibreur de charge
Utilisez hello suivant commande tooremove un équilibreur de charge :

```azurecli
azure network lb delete --resource-group nrprg --name nrplb
```

## <a name="next-steps"></a>Étapes suivantes
[Prise en main de la configuration d’un équilibrage de charge interne](load-balancer-get-started-ilb-arm-cli.md)

[Configuration d'un mode de distribution d'équilibrage de charge](load-balancer-distribution-mode.md)

[Configuration des paramètres du délai d’expiration TCP inactif pour votre équilibrage de charge](load-balancer-tcp-idle-timeout.md)
