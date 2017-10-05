---
title: "Équilibrage de charge sur plusieurs configurations IP à l’aide de l’interface Azure CLI | Microsoft Docs"
description: "Apprendre à affecter plusieurs adresses IP à une machine virtuelle avec Azure CLI | Resource Manager."
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
ms.openlocfilehash: bd15713752ea01ad403d8e3dcfed0c9a7adcc7fa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="load-balancing-on-multiple-ip-configurations"></a><span data-ttu-id="380b7-103">Équilibrage de charge sur plusieurs configurations IP</span><span class="sxs-lookup"><span data-stu-id="380b7-103">Load balancing on multiple IP configurations</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="380b7-104">Portail</span><span class="sxs-lookup"><span data-stu-id="380b7-104">Portal</span></span>](load-balancer-multiple-ip.md)
> * [<span data-ttu-id="380b7-105">INTERFACE DE LIGNE DE COMMANDE</span><span class="sxs-lookup"><span data-stu-id="380b7-105">CLI</span></span>](load-balancer-multiple-ip-cli.md)
> * [<span data-ttu-id="380b7-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="380b7-106">PowerShell</span></span>](load-balancer-multiple-ip-powershell.md)

<span data-ttu-id="380b7-107">Cet article décrit comment utiliser Azure Load Balancer avec plusieurs adresses IP sur une interface réseau secondaire (carte réseau).</span><span class="sxs-lookup"><span data-stu-id="380b7-107">This article describes how to use Azure Load Balancer with multiple IP addresses on a secondary network interface (NIC).</span></span> <span data-ttu-id="380b7-108">Avec ce scénario, nous disposons de deux machines virtuelles exécutant Windows, chacune avec une carte réseau principale et secondaire.</span><span class="sxs-lookup"><span data-stu-id="380b7-108">For this scenario, we have two VMs running Windows, each with a primary and a secondary NIC.</span></span> <span data-ttu-id="380b7-109">Chacune des cartes réseau secondaires dispose de deux configurations IP.</span><span class="sxs-lookup"><span data-stu-id="380b7-109">Each of the secondary NICs have two IP configurations.</span></span> <span data-ttu-id="380b7-110">Chaque machine virtuelle héberge les deux sites web contoso.com et fabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="380b7-110">Each VM hosts both websites contoso.com and fabrikam.com.</span></span> <span data-ttu-id="380b7-111">Chaque site web est lié à l’une des configurations IP sur la carte réseau secondaire.</span><span class="sxs-lookup"><span data-stu-id="380b7-111">Each website is bound to one of the IP configurations on the secondary NIC.</span></span> <span data-ttu-id="380b7-112">Nous utilisons Azure Load Balancer pour exposer deux adresses IP frontales, une par site web, afin de distribuer le trafic à la configuration IP correspondante pour le site web.</span><span class="sxs-lookup"><span data-stu-id="380b7-112">We use Azure Load Balancer to expose two frontend IP addresses, one for each website, to distribute traffic to the respective IP configuration for the website.</span></span> <span data-ttu-id="380b7-113">Ce scénario utilise le même numéro de port sur les deux serveurs frontaux, ainsi que les deux adresses IP de pool principal.</span><span class="sxs-lookup"><span data-stu-id="380b7-113">This scenario uses the same port number across both frontends, as well as both backend pool IP addresses.</span></span>

![Image du scénario LB](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-to-load-balance-on-multiple-ip-configurations"></a><span data-ttu-id="380b7-115">Étapes pour équilibrer la charge sur plusieurs configurations IP</span><span class="sxs-lookup"><span data-stu-id="380b7-115">Steps to load balance on multiple IP configurations</span></span>

<span data-ttu-id="380b7-116">Exécutez la procédure ci-dessous afin de respecter le scénario décrit dans cet article :</span><span class="sxs-lookup"><span data-stu-id="380b7-116">Follow the steps below to achieve the scenario outlined in this article:</span></span>

1. <span data-ttu-id="380b7-117">[Installez et configurez l’interface Azure CLI](../cli-install-nodejs.md) en suivant les étapes de l’article lié, puis connectez-vous au compte Azure.</span><span class="sxs-lookup"><span data-stu-id="380b7-117">[Install and Configure the Azure CLI](../cli-install-nodejs.md) the Azure CLI by following the steps in the linked article and log into your Azure account.</span></span>
2. <span data-ttu-id="380b7-118">[Créez un groupe de ressources](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-resource-group) appelé *contosofabrikam*, tel que décrit ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="380b7-118">[Create a resource group](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-resource-group) called *contosofabrikam* as described above.</span></span>

    ```azurecli
    azure group create contosofabrikam westcentralus
    ```

3. <span data-ttu-id="380b7-119">[Créez un groupe à haute disponibilité](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-an-availability-set) pour les deux machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="380b7-119">[Create an availability set](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-an-availability-set) to for the two VMs.</span></span> <span data-ttu-id="380b7-120">Pour ce scénario, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="380b7-120">For this scenario, use the following command:</span></span>

    ```azurecli
    azure availset create --resource-group contosofabrikam --location westcentralus --name myAvailabilitySet
    ```

4. <span data-ttu-id="380b7-121">[Créez un réseau virtuel](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-network-and-subnet) appelé *myVNet* et un sous-réseau appelé *mySubnet* :</span><span class="sxs-lookup"><span data-stu-id="380b7-121">[Create a virtual network](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-network-and-subnet) called *myVNet* and a subnet called *mySubnet*:</span></span>

    ```azurecli
    azure network vnet create --resource-group contosofabrikam --name myVnet --address-prefixes 10.0.0.0/16  --location westcentralus

    azure network vnet subnet create --resource-group contosofabrikam --vnet-name myVnet --name mySubnet --address-prefix 10.0.0.0/24
    ```

5. <span data-ttu-id="380b7-122">[Créez l’équilibrage de charge](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) appelé *mylb* :</span><span class="sxs-lookup"><span data-stu-id="380b7-122">[Create the load balancer](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) called *mylb*:</span></span>

    ```azurecli
    azure network lb create --resource-group contosofabrikam --location westcentralus --name mylb
    ```

6. <span data-ttu-id="380b7-123">Créez deux adresses IP publiques dynamiques pour les configurations IP frontales de votre équilibrage de charge :</span><span class="sxs-lookup"><span data-stu-id="380b7-123">Create two dynamic public IP addresses for the frontend IP configurations of your load balancer:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name PublicIp1 --domain-name-label contoso --allocation-method Dynamic

    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name PublicIp2 --domain-name-label fabrikam --allocation-method Dynamic
    ```

7. <span data-ttu-id="380b7-124">Créez deux configurations IP frontales, *contosofe* et *fabrikamfe*, respectivement :</span><span class="sxs-lookup"><span data-stu-id="380b7-124">Create the two frontend IP configurations, *contosofe* and *fabrikamfe* respectively:</span></span>

    ```azurecli
    azure network lb frontend-ip create --resource-group contosofabrikam --lb-name mylb --public-ip-name PublicIp1 --name contosofe
    azure network lb frontend-ip create --resource-group contosofabrikam --lb-name mylb --public-ip-name PublicIp2 --name fabrkamfe
    ```

8. <span data-ttu-id="380b7-125">Créez deux pools d’adresses frontales, *contosopool* et *fabrikampool*, une [sonde](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) - *HTTP* et vos règles d’équilibrage de charge, *HTTPc* et *HTTPf* :</span><span class="sxs-lookup"><span data-stu-id="380b7-125">Create your backend address pools - *contosopool* and *fabrikampool*, a [probe](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) - *HTTP*, and your load balancing rules - *HTTPc* and *HTTPf*:</span></span>

    ```azurecli
    azure network lb address-pool create --resource-group contosofabrikam --lb-name mylb --name contosopool
    azure network lb address-pool create --resource-group contosofabrikam --lb-name mylb --name fabrikampool

    azure network lb probe create --resource-group contosofabrikam --lb-name mylb --name HTTP --protocol "http" --interval 15 --count 2 --path index.html

    azure network lb rule create --resource-group contosofabrikam --lb-name mylb --name HTTPc --protocol tcp --probe-name http--frontend-port 5000 --backend-port 5000 --frontend-ip-name contosofe --backend-address-pool-name contosopool
    azure network lb rule create --resource-group contosofabrikam --lb-name mylb --name HTTPf --protocol tcp --probe-name http --frontend-port 5000 --backend-port 5000 --frontend-ip-name fabrkamfe --backend-address-pool-name fabrikampool
    ```

9. <span data-ttu-id="380b7-126">Exécutez la commande suivante, puis vérifiez la sortie afin de [confirmer que votre équilibrage de charge](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) a été correctement créé :</span><span class="sxs-lookup"><span data-stu-id="380b7-126">Run the following command below and then check the output to [verify your load balancer](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) was created correctly:</span></span>

    ```azurecli
    azure network lb show --resource-group contosofabrikam --name mylb
    ```

10. <span data-ttu-id="380b7-127">[Créez une adresse IP publique](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-public-ip-address), *myPublicIp* et [un compte de stockage](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json), *mystorageaccont1* pour votre première machine virtuelle VM1, tel que représenté ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="380b7-127">[Create a public IP](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-public-ip-address), *myPublicIp*, and [storage account](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json), *mystorageaccont1* for your first virtual machine VM1 as shown below:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name myPublicIP --domain-name-label mypublicdns345 --allocation-method Dynamic

    azure storage account create --location westcentralus --resource-group contosofabrikam --kind Storage --sku-name GRS mystorageaccount1
    ```

11. <span data-ttu-id="380b7-128">[Créez les interfaces réseau](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-nic) pour VM1 et ajoutez une seconde configuration IP, *VM1-ipconfig2*, puis [créez la machine virtuelle](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-the-linux-vms), tel que représenté ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="380b7-128">[Create the network interfaces](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-nic) for VM1 and add a second IP configuration, *VM1-ipconfig2*, and [create the VM](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-the-linux-vms) as shown below:</span></span>

    ```azurecli
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM1Nic1 --ip-config-name NIC1-ipconfig1
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM1Nic2 --ip-config-name VM1-ipconfig1 --public-ip-name myPublicIP --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/contosopool"
    azure network nic ip-config create --resource-group contosofabrikam --nic-name VM1Nic2 --name VM1-ipconfig2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/fabrikampool"
    azure vm create --resource-group contosofabrikam --name VM1 --location westcentralus --os-type linux --nic-names VM1Nic1,VM1Nic2  --vnet-name VNet1 --vnet-subnet-name Subnet1 --availset-name myAvailabilitySet --vm-size Standard_DS3_v2 --storage-account-name mystorageaccount1 --image-urn canonical:UbuntuServer:16.04.0-LTS:latest --admin-username <your username>  --admin-password <your password>
    ```

12. <span data-ttu-id="380b7-129">Répétez les étapes 10-11 pour votre seconde machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="380b7-129">Repeat steps 10-11 for your second VM:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name myPublicIP2 --domain-name-label mypublicdns785 --allocation-method Dynamic
    azure storage account create --location westcentralus --resource-group contosofabrikam --kind Storage --sku-name GRS mystorageaccount2
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM2Nic1
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM2Nic2 --ip-config-name VM2-ipconfig1 --public-ip-name myPublicIP2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/contosopool"
    azure network nic ip-config create --resource-group contosofabrikam --nic-name VM2Nic2 --name VM2-ipconfig2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/fabrikampool"
    azure vm create --resource-group contosofabrikam --name VM2 --location westcentralus --os-type linux --nic-names VM2Nic1,VM2Nic2 --vnet-name VNet1 --vnet-subnet-name Subnet1 --availset-name myAvailabilitySet --vm-size Standard_DS3_v2 --storage-account-name mystorageaccount2 --image-urn canonical:UbuntuServer:16.04.0-LTS:latest --admin-username <your username>  --admin-password <your password>
    ```

13. <span data-ttu-id="380b7-130">Enfin, vous devez configurer les enregistrements de ressource DNS pour qu’ils pointent sur l’adresse IP frontale respective de l’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="380b7-130">Finally, you must configure DNS resource records to point to the respective frontend IP address of the Load Balancer.</span></span> <span data-ttu-id="380b7-131">Vous pouvez héberger vos domaines dans Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="380b7-131">You may host your domains in Azure DNS.</span></span> <span data-ttu-id="380b7-132">Pour plus d’informations sur l’utilisation d’Azure DNS avec un équilibrage de charge, voir [Utiliser Azure DNS avec d’autres services Azure](../dns/dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="380b7-132">For more information about using Azure DNS with Load Balancer, see [Using Azure DNS with other Azure services](../dns/dns-for-azure-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="380b7-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="380b7-133">Next steps</span></span>
- <span data-ttu-id="380b7-134">Pour en savoir plus sur la combinaison de services d’équilibrage de charge dans Azure, consultez [Utilisation des services d’équilibrage de charge dans Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span><span class="sxs-lookup"><span data-stu-id="380b7-134">Learn more about how to combine load balancing services in Azure in [Using load-balancing services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span></span>
- <span data-ttu-id="380b7-135">Pour savoir comment gérer et dépanner l’équilibrage de charge à l’aide de différents types de journaux dans Azure, consultez [Log Analytics pour Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span><span class="sxs-lookup"><span data-stu-id="380b7-135">Learn how you can use different types of logs in Azure to manage and troubleshoot load balancer in [Log analytics for Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span></span>
