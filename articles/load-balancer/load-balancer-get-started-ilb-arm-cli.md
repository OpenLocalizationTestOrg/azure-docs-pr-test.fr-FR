---
title: "aaaCreate un interne l’équilibrage de charge - CLI d’Azure | Documents Microsoft"
description: "Découvrez comment toocreate un équilibreur de charge interne à l’aide de hello CLI d’Azure dans le Gestionnaire de ressources"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: c7a24e92-b4da-43c0-90f2-841c1b7ce489
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 3aea6fdb07600f0d661ec6b8ffc784b03380a127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-by-using-hello-azure-cli"></a>Créer un équilibreur de charge interne à l’aide de hello CLI d’Azure

> [!div class="op_single_selector"]
> * [portail Azure](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [Interface de ligne de commande Azure](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [Modèle](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md).  Cet article couvre l’utilisation de modèle de déploiement Resource Manager hello, qui recommandées par Microsoft pour la plupart des déploiements de nouveau au lieu de hello [modèle de déploiement classique](load-balancer-get-started-ilb-classic-cli.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-solution-by-using-hello-azure-cli"></a>Déployer des solutions de hello à l’aide de hello CLI d’Azure

Hello suit montrent comment toocreate une côté Internet l’équilibrage de charge à l’aide du Gestionnaire de ressources Azure avec l’interface CLI. Avec Azure Resource Manager, chaque ressource est créé et configuré individuellement et puis rassembler toocreate une ressource.

Vous devez toocreate et que vous configurez hello suivant objets toodeploy un équilibreur de charge :

* **Configuration d’adresses IP frontales**: contient les adresses IP publiques pour le trafic réseau entrant.
* **Pool d’adresses de serveur principal**: contient des interfaces réseau (NIC) qui autorisent le trafic réseau tooreceive du hello machines virtuelles à partir de l’équilibrage de charge hello
* **Règles d’équilibrage de charge**: contient des règles pour mappent un port public sur tooport d’équilibrage de charge hello dans un pool d’adresses de serveur principal hello
* **Les règles NAT de trafic entrant**: contient des règles pour mappent un port public sur le port de tooa d’équilibrage de charge de hello pour un ordinateur virtuel spécifique dans le pool d’adresses principal hello
* **Sondes**: contient les sondes d’intégrité qui sont la disponibilité de hello toocheck utilisé d’instances de machines virtuelles dans un pool d’adresses de serveur principal hello

Pour plus d’informations, consultez [Prise en charge d’un équilibreur de charge par Azure Resource Manager](load-balancer-arm.md).

## <a name="set-up-cli-toouse-resource-manager"></a>Configurer CLI toouse Gestionnaire de ressources

1. Si vous n’avez jamais utilisé CLI d’Azure, consultez [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md). Suivez les instructions de hello point toohello où vous sélectionnez votre compte Azure et votre abonnement.
2. Exécutez hello **mode config azure** commande tooswitch tooResource Manager mode, comme suit :

    ```azurecli
    azure config mode arm
    ```

    Sortie attendue :

        info:    New mode is arm

## <a name="create-an-internal-load-balancer-step-by-step"></a>Créer un équilibrage de charge interne, étape par étape

1. Connectez-vous tooAzure.

    ```azurecli
    azure login
    ```

    À l’invite, entrez vos informations d’identification Azure.

2. Modifier le mode Gestionnaire de ressources tooAzure hello commande Outils.

    ```azurecli
    azure config mode arm
    ```

## <a name="create-a-resource-group"></a>Créer un groupe de ressources

Toutes les ressources d’Azure Resource Manager sont associées à un groupe de ressources. Le cas échéant, créez un groupe de ressources.

```azurecli
azure group create <resource group name> <location>
```

## <a name="create-an-internal-load-balancer-set"></a>Créer un jeu d’équilibrage de charge interne

1. Créer un équilibrage de charge interne

    Bonjour scénario, un groupe de ressources nommé nrprg est créé dans la région est des États-Unis.

    ```azurecli
    azure network lb create --name nrprg --location eastus
    ```

   > [!NOTE]
   > Toutes les ressources pour un équilibrage de charge interne, tels que les réseaux virtuels et des sous-réseaux du réseau virtuel, doivent être dans hello du même groupe de ressources et de hello même région.

2. Créer une adresse IP frontale pour l’équilibrage de charge interne hello.

    adresse IP Hello que vous utilisez doit être dans la plage de sous-réseau hello de votre réseau virtuel.

    ```azurecli
    azure network lb frontend-ip create --resource-group nrprg --lb-name ilbset --name feilb --private-ip-address 10.0.0.7 --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet
    ```

3. Créer un pool d’adresses de serveur principal hello.

    ```azurecli
    azure network lb address-pool create --resource-group nrprg --lb-name ilbset --name beilb
    ```

    Après avoir défini une adresse IP frontale et un pool d’adresses principales, vous pouvez créer des règles d’équilibrage de charge, des règles NAT entrantes et des sondes d’intégrité personnalisées.

4. Créer une règle d’équilibreur de charge pour l’équilibrage de charge interne hello.

    Lorsque vous suivez les étapes précédentes hello, commande hello crée une règle d’équilibrage de charge pour l’écoute tooport 1433 dans le pool frontal de hello et envoi équilibrage de la charge du trafic toohello principal pool d’adresses réseau, via le port 1433.

    ```azurecli
    azure network lb rule create --resource-group nrprg --lb-name ilbset --name ilbrule --protocol tcp --frontend-port 1433 --backend-port 1433 --frontend-ip-name feilb --backend-address-pool-name beilb
    ```

5. Créez des règles NAT entrantes.

    Les règles NAT entrantes sont les extrémités de toocreate utilisé dans un équilibreur de charge qui vont l’instance de machine virtuelle spécifique tooa. les étapes précédentes Hello créé deux règles NAT pour le Bureau à distance.

    ```azurecli
    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule1 --protocol TCP --frontend-port 5432 --backend-port 3389

    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule2 --protocol TCP --frontend-port 5433 --backend-port 3389
    ```

6. Créer des sondes d’intégrité pour l’équilibrage de charge hello.

    Une sonde d’intégrité vérifie tous les toomake des instances de machine virtuelle qu’ils peuvent envoyer le trafic réseau. instance de machine virtuelle Hello avec les vérifications de sonde ayant échoué est supprimé à partir de l’équilibrage de charge hello jusqu'à ce qu’il est en ligne et une vérification de la sonde détermine qu’elle est saine.

    ```azurecli
    azure network lb probe create --resource-group nrprg --lb-name ilbset --name ilbprobe --protocol tcp --interval 300 --count 4
    ```

    > [!NOTE]
    > plateforme de Microsoft Azure Hello utilise une adresse IPv4 statique routable publiquement pour un éventail de scénarios d’administration. adresse IP de Hello est 168.63.129.16. Cette adresse IP ne doit pas être bloquée par les pare-feu, car cela peut entraîner un comportement inattendu.
    > En ce qui concerne tooAzure équilibrage de charge interne, cette adresse IP est utilisée par l’analyse des sondes de l’état d’intégrité de hello charge équilibrage toodetermine hello pour les ordinateurs virtuels dans un jeu d’équilibrage de charge. Si un groupe de sécurité réseau est utilisé toorestrict virtuels trafic tooAzure dans un jeu d’équilibrage de charge en interne ou sous-réseau de réseau virtuel tooa appliqués, vérifiez qu’une règle de sécurité réseau est ajoutée tooallow trafic à partir de 168.63.129.16.

## <a name="create-nics"></a>Créer des cartes réseau

Vous devez toocreate NIC (ou modifier des modèles existants) et les associer à des règles de tooNAT, des règles d’équilibrage de charge et des sondes.

1. Créez une carte réseau nommée *être lb-nic1*et l’associer à hello *rdp1* NAT règle et hello *beilb* pool d’adresses du serveur principal.

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" --location eastus
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

2. Créez une carte réseau nommée *être lb-nic2*et l’associer à hello *rdp2* NAT règle et hello *beilb* pool d’adresses du serveur principal.

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" --location eastus
    ```

3. Créer un ordinateur virtuel nommé *DB1*et associez-le ensuite hello carte réseau nommée *être lb-nic1*. Un compte de stockage appelée *web1nrp* est créé avant hello après l’exécution de la commande :

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```
    > [!IMPORTANT]
    > Machines virtuelles dans un toobe de nécessité d’équilibrage de charge dans hello même groupe à haute disponibilité. Utilisez `azure availset create` toocreate un ensemble de disponibilité.

4. Créer un ordinateur virtuel (VM) nommé *DB2*et associez-le ensuite hello carte réseau nommée *être lb-nic2*. Un compte de stockage appelée *web1nrp* a été créé avant d’exécuter hello commande suivante.

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="delete-a-load-balancer"></a>Suppression d’un équilibreur de charge

tooremove un équilibreur de charge, utilisez hello de commande suivante :

```azurecli
azure network lb delete --resource-group nrprg --name ilbset
```

## <a name="next-steps"></a>Étapes suivantes

[Configurer le mode de distribution d’équilibrage de charge à l’aide de l’affinité d’IP source](load-balancer-distribution-mode.md)

[Configuration des paramètres du délai d’expiration TCP inactif pour votre équilibrage de charge](load-balancer-tcp-idle-timeout.md)

