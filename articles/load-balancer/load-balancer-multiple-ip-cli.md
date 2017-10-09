---
title: "aaaLoad équilibrage sur plusieurs configurations IP à l’aide d’Azure CLI | Documents Microsoft"
description: "Découvrez comment tooassign des adresses IP multiples virtuels tooa à l’aide d’Azure CLI | Gestionnaire de ressources."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: annahar
ms.openlocfilehash: df81e1b8193f274bad435d6b506c7be824117416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balancing-on-multiple-ip-configurations"></a>Équilibrage de charge sur plusieurs configurations IP

> [!div class="op_single_selector"]
> * [Portail](load-balancer-multiple-ip.md)
> * [INTERFACE DE LIGNE DE COMMANDE](load-balancer-multiple-ip-cli.md)
> * [PowerShell](load-balancer-multiple-ip-powershell.md)

Cet article décrit comment toouse équilibrage de charge Azure avec adresse IP de plusieurs adresses sur une interface réseau secondaire (NIC). Avec ce scénario, nous disposons de deux machines virtuelles exécutant Windows, chacune avec une carte réseau principale et secondaire. Chacun des hello secondaire cartes réseau ont deux configurations IP. Chaque machine virtuelle héberge les deux sites web contoso.com et fabrikam.com. Chaque site Web est lié tooone de configurations IP hello hello seconde. Nous utilisons équilibrage de charge Azure tooexpose deux frontal adresses IP, une pour chaque site Web, toodistribute toohello respectifs IP configuration du trafic pour le site Web de hello. Ce scénario utilise hello même numéro de port entre les serveurs frontaux, ainsi que les deux adresses IP du pool principal.

![Image du scénario LB](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a>Solde de tooload étapes sur plusieurs configurations IP

Suivez les étapes de hello ci-dessous le scénario de hello tooachieve présentée dans cet article :

1. [Installer et configurer hello CLI d’Azure](../cli-install-nodejs.md) hello CLI d’Azure en suivant les étapes de hello dans l’article lié à hello et connectez-vous à votre compte Azure.
2. [Créez un groupe de ressources](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-resource-group) appelé *contosofabrikam*, tel que décrit ci-dessus.

    ```azurecli
    azure group create contosofabrikam westcentralus
    ```

3. [Créer un ensemble de disponibilité](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-an-availability-set) toofor hello deux machines virtuelles. Pour ce scénario, utilisez hello de commande suivante :

    ```azurecli
    azure availset create --resource-group contosofabrikam --location westcentralus --name myAvailabilitySet
    ```

4. [Créez un réseau virtuel](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-network-and-subnet) appelé *myVNet* et un sous-réseau appelé *mySubnet* :

    ```azurecli
    azure network vnet create --resource-group contosofabrikam --name myVnet --address-prefixes 10.0.0.0/16  --location westcentralus

    azure network vnet subnet create --resource-group contosofabrikam --vnet-name myVnet --name mySubnet --address-prefix 10.0.0.0/24
    ```

5. [Créer l’équilibreur de charge hello](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) appelé *mylb*:

    ```azurecli
    azure network lb create --resource-group contosofabrikam --location westcentralus --name mylb
    ```

6. Créez deux adresses IP publiques dynamiques pour les configurations IP hello frontale de votre équilibreur de charge :

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name PublicIp1 --domain-name-label contoso --allocation-method Dynamic

    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name PublicIp2 --domain-name-label fabrikam --allocation-method Dynamic
    ```

7. Créer des configurations IP, serveur frontal de hello deux *contosofe* et *fabrikamfe* respectivement :

    ```azurecli
    azure network lb frontend-ip create --resource-group contosofabrikam --lb-name mylb --public-ip-name PublicIp1 --name contosofe
    azure network lb frontend-ip create --resource-group contosofabrikam --lb-name mylb --public-ip-name PublicIp2 --name fabrkamfe
    ```

8. Créez deux pools d’adresses frontales, *contosopool* et *fabrikampool*, une [sonde](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) - *HTTP* et vos règles d’équilibrage de charge, *HTTPc* et *HTTPf* :

    ```azurecli
    azure network lb address-pool create --resource-group contosofabrikam --lb-name mylb --name contosopool
    azure network lb address-pool create --resource-group contosofabrikam --lb-name mylb --name fabrikampool

    azure network lb probe create --resource-group contosofabrikam --lb-name mylb --name HTTP --protocol "http" --interval 15 --count 2 --path index.html

    azure network lb rule create --resource-group contosofabrikam --lb-name mylb --name HTTPc --protocol tcp --probe-name http--frontend-port 5000 --backend-port 5000 --frontend-ip-name contosofe --backend-address-pool-name contosopool
    azure network lb rule create --resource-group contosofabrikam --lb-name mylb --name HTTPf --protocol tcp --probe-name http --frontend-port 5000 --backend-port 5000 --frontend-ip-name fabrkamfe --backend-address-pool-name fabrikampool
    ```

9. Suivante d’exécution hello commande ci-dessous, puis à vérifier les sortie hello trop[vérifier votre équilibreur de charge](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) a été créé correctement :

    ```azurecli
    azure network lb show --resource-group contosofabrikam --name mylb
    ```

10. [Créez une adresse IP publique](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-public-ip-address), *myPublicIp* et [un compte de stockage](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json), *mystorageaccont1* pour votre première machine virtuelle VM1, tel que représenté ci-dessous :

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name myPublicIP --domain-name-label mypublicdns345 --allocation-method Dynamic

    azure storage account create --location westcentralus --resource-group contosofabrikam --kind Storage --sku-name GRS mystorageaccount1
    ```

11. [Créer des interfaces réseau hello](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-nic) de VM1 et ajouter une deuxième configuration IP, *ipconfig2 de VM1*, et [créer hello VM](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-the-linux-vms) comme indiqué ci-dessous :

    ```azurecli
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM1Nic1 --ip-config-name NIC1-ipconfig1
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM1Nic2 --ip-config-name VM1-ipconfig1 --public-ip-name myPublicIP --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/contosopool"
    azure network nic ip-config create --resource-group contosofabrikam --nic-name VM1Nic2 --name VM1-ipconfig2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/fabrikampool"
    azure vm create --resource-group contosofabrikam --name VM1 --location westcentralus --os-type linux --nic-names VM1Nic1,VM1Nic2  --vnet-name VNet1 --vnet-subnet-name Subnet1 --availset-name myAvailabilitySet --vm-size Standard_DS3_v2 --storage-account-name mystorageaccount1 --image-urn canonical:UbuntuServer:16.04.0-LTS:latest --admin-username <your username>  --admin-password <your password>
    ```

12. Répétez les étapes 10-11 pour votre seconde machine virtuelle :

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name myPublicIP2 --domain-name-label mypublicdns785 --allocation-method Dynamic
    azure storage account create --location westcentralus --resource-group contosofabrikam --kind Storage --sku-name GRS mystorageaccount2
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM2Nic1
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM2Nic2 --ip-config-name VM2-ipconfig1 --public-ip-name myPublicIP2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/contosopool"
    azure network nic ip-config create --resource-group contosofabrikam --nic-name VM2Nic2 --name VM2-ipconfig2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/fabrikampool"
    azure vm create --resource-group contosofabrikam --name VM2 --location westcentralus --os-type linux --nic-names VM2Nic1,VM2Nic2 --vnet-name VNet1 --vnet-subnet-name Subnet1 --availset-name myAvailabilitySet --vm-size Standard_DS3_v2 --storage-account-name mystorageaccount2 --image-urn canonical:UbuntuServer:16.04.0-LTS:latest --admin-username <your username>  --admin-password <your password>
    ```

13. Enfin, vous devez configurer DNS ressource enregistrements toopoint toohello respectifs adresse IP frontale de hello équilibrage de charge. Vous pouvez héberger vos domaines dans Azure DNS. Pour plus d’informations sur l’utilisation d’Azure DNS avec un équilibrage de charge, voir [Utiliser Azure DNS avec d’autres services Azure](../dns/dns-for-azure-services.md).

## <a name="next-steps"></a>Étapes suivantes
- En savoir plus sur le fonctionnement des services de l’équilibrage de charge toocombine dans Azure dans [à l’aide des services d’équilibrage de charge dans Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).
- Découvrez comment vous pouvez utiliser différents types de journaux dans Azure toomanage et résoudre les problèmes d’équilibrage de charge dans [journal analytique pour l’équilibrage de charge Azure](../load-balancer/load-balancer-monitor-log.md).
