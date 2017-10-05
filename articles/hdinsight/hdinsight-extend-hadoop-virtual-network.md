---
title: "Étendre HDInsight avec un réseau virtuel - Azure | Microsoft Docs"
description: "Apprenez à utiliser Azure Virtual Network pour connecter HDInsight à d'autres ressources de cloud ou à des ressources de votre centre de données"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 37b9b600-d7f8-4cb1-a04a-0b3a827c6dcc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: larryfr
ms.openlocfilehash: 380423ec42ad4905c73fcd57501102e9f7062e81
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="extend-azure-hdinsight-using-an-azure-virtual-network"></a><span data-ttu-id="f91c1-103">Étendre HDInsight à l’aide d’un réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="f91c1-103">Extend Azure HDInsight using an Azure Virtual Network</span></span>

<span data-ttu-id="f91c1-104">Découvrez comment utiliser HDInsight avec un [réseau virtuel Azure](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f91c1-104">Learn how to use HDInsight with an [Azure Virtual Network](../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="f91c1-105">L’utilisation d’un réseau virtuel Azure permet les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="f91c1-105">Using an Azure Virtual Network enables the following scenarios:</span></span>

* <span data-ttu-id="f91c1-106">connexion à HDInsight directement à partir d’un réseau local ;</span><span class="sxs-lookup"><span data-stu-id="f91c1-106">Connecting to HDInsight directly from an on-premises network.</span></span>

* <span data-ttu-id="f91c1-107">connexion de HDInsight à des banques de données dans un réseau virtuel Azure ;</span><span class="sxs-lookup"><span data-stu-id="f91c1-107">Connecting HDInsight to data stores in an Azure Virtual network.</span></span>

* <span data-ttu-id="f91c1-108">accès direct aux services Hadoop qui ne sont pas disponibles publiquement sur Internet,</span><span class="sxs-lookup"><span data-stu-id="f91c1-108">Directly accessing Hadoop services that are not available publicly over the internet.</span></span> <span data-ttu-id="f91c1-109">tels que les API Kafka ou l’API Java HBase.</span><span class="sxs-lookup"><span data-stu-id="f91c1-109">For example, Kafka APIs or the HBase Java API.</span></span>

> [!WARNING]
> <span data-ttu-id="f91c1-110">Les informations contenues dans ce document nécessitent une compréhension de la gestion de réseau TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="f91c1-110">The information in this document requires an understanding of TCP/IP networking.</span></span> <span data-ttu-id="f91c1-111">Si vous n’êtes pas familiarisé avec la gestion de réseau TCP/IP, vous devez travailler en partenariat avec une personne connaissant le sujet avant d’apporter des modifications aux réseaux de production.</span><span class="sxs-lookup"><span data-stu-id="f91c1-111">If you are not familiar with TCP/IP networking, you should partner with someone who is before making modifications to production networks.</span></span>

## <a name="planning"></a><span data-ttu-id="f91c1-112">Planification</span><span class="sxs-lookup"><span data-stu-id="f91c1-112">Planning</span></span>

<span data-ttu-id="f91c1-113">Les questions auxquelles vous devez répondre lors de la planification de l’installation de HDInsight dans un réseau virtuel sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="f91c1-113">The following are the questions that you must answer when planning to install HDInsight in a virtual network:</span></span>

* <span data-ttu-id="f91c1-114">Devez installer HDInsight dans un réseau virtuel existant ?</span><span class="sxs-lookup"><span data-stu-id="f91c1-114">Do you need to install HDInsight into an existing virtual network?</span></span> <span data-ttu-id="f91c1-115">Ou bien créez-vous un réseau ?</span><span class="sxs-lookup"><span data-stu-id="f91c1-115">Or are you creating a new network?</span></span>

    <span data-ttu-id="f91c1-116">Si vous utilisez un réseau virtuel existant, vous devrez peut-être modifier la configuration de celui-ci avant d’installer HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f91c1-116">If you are using an existing virtual network, you may need to modify the network configuration before you can install HDInsight.</span></span> <span data-ttu-id="f91c1-117">Pour plus d’informations, voir la section [Ajouter HDInsight à un réseau virtuel existant](#existingvnet).</span><span class="sxs-lookup"><span data-stu-id="f91c1-117">For more information, see the [add HDInsight to an existing virtual network](#existingvnet) section.</span></span>

* <span data-ttu-id="f91c1-118">Vous souhaitez connecter le réseau virtuel contenant HDInsight à un autre réseau virtuel ou à votre réseau local ?</span><span class="sxs-lookup"><span data-stu-id="f91c1-118">Do you want to connect the virtual network containing HDInsight to another virtual network or your on-premises network?</span></span>

    <span data-ttu-id="f91c1-119">Pour utiliser aisément des ressources de différents réseaux, il se peut que vous deviez créer un DNS personnalisé et configurer un transfert de DNS.</span><span class="sxs-lookup"><span data-stu-id="f91c1-119">To easily work with resources across networks, you may need to create a custom DNS and configure DNS forwarding.</span></span> <span data-ttu-id="f91c1-120">Pour plus d’informations, voir la section [Connecter plusieurs réseaux](#multinet).</span><span class="sxs-lookup"><span data-stu-id="f91c1-120">For more information, see the [connecting multiple networks](#multinet) section.</span></span>

* <span data-ttu-id="f91c1-121">Souhaitez-vous restreindre/rediriger le trafic entrant ou sortant échangé avec HDInsight ?</span><span class="sxs-lookup"><span data-stu-id="f91c1-121">Do you want to restrict/redirect inbound or outbound traffic to HDInsight?</span></span>

    <span data-ttu-id="f91c1-122">HDInsight doit disposer d’une communication illimitée avec les adresses IP spécifiques dans le centre de données Azure.</span><span class="sxs-lookup"><span data-stu-id="f91c1-122">HDInsight must have unrestricted communication with specific IP addresses in the Azure data center.</span></span> <span data-ttu-id="f91c1-123">Il existe également plusieurs ports qui doivent être autorisés au travers de pare-feu pour la communication du client.</span><span class="sxs-lookup"><span data-stu-id="f91c1-123">There are also several ports that must be allowed through firewalls for client communication.</span></span> <span data-ttu-id="f91c1-124">Pour plus d’informations, voir la section [Contrôler le trafic réseau](#networktraffic).</span><span class="sxs-lookup"><span data-stu-id="f91c1-124">For more information, see the [controlling network traffic](#networktraffic) section.</span></span>

## <span data-ttu-id="f91c1-125"><a id="existingvnet"></a>Ajouter HDInsight à un réseau virtuel existant</span><span class="sxs-lookup"><span data-stu-id="f91c1-125"><a id="existingvnet"></a>Add HDInsight to an existing virtual network</span></span>

<span data-ttu-id="f91c1-126">Suivez les étapes de cette section pour découvrir comment ajouter un nouveau cluster HDInsight à un réseau virtuel Azure existant.</span><span class="sxs-lookup"><span data-stu-id="f91c1-126">Use the steps in this section to discover how to add a new HDInsight to an existing Azure Virtual Network.</span></span>

> [!NOTE]
> <span data-ttu-id="f91c1-127">Vous ne pouvez pas ajouter un cluster HDInsight existant à un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f91c1-127">You cannot add an existing HDInsight cluster into a virtual network.</span></span>

1. <span data-ttu-id="f91c1-128">Utilisez-vous un modèle de déploiement classique ou Resource Manager pour le réseau virtuel ?</span><span class="sxs-lookup"><span data-stu-id="f91c1-128">Are you using a classic or Resource Manager deployment model for the virtual network?</span></span>

    <span data-ttu-id="f91c1-129">HDInsight 3.4 et versions ultérieures nécessitent un réseau virtuel Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f91c1-129">HDInsight 3.4 and greater requires a Resource Manager virtual network.</span></span> <span data-ttu-id="f91c1-130">Les versions antérieures de HDInsight nécessitaient un réseau virtuel classique.</span><span class="sxs-lookup"><span data-stu-id="f91c1-130">Earlier versions of HDInsight required a classic virtual network.</span></span>

    <span data-ttu-id="f91c1-131">Si votre réseau existant est un réseau virtuel classique, vous devez créer un réseau virtuel Resource Manager, puis connecter les deux.</span><span class="sxs-lookup"><span data-stu-id="f91c1-131">If your existing network is a classic virtual network, then you must create a Resource Manager virtual network and then connect the two.</span></span> <span data-ttu-id="f91c1-132">[Connexion de réseaux virtuels classiques aux nouveaux réseaux virtuels](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f91c1-132">[Connecting classic VNets to new VNets](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).</span></span>

    <span data-ttu-id="f91c1-133">Une fois joint, HDInsight installé dans le réseau peut interagir avec des ressources du réseau classique.</span><span class="sxs-lookup"><span data-stu-id="f91c1-133">Once joined, HDInsight installed in the Resource Manager network can interact with resources in the classic network.</span></span>

2. <span data-ttu-id="f91c1-134">Voulez-vous utiliser un tunneling forcé ?</span><span class="sxs-lookup"><span data-stu-id="f91c1-134">Do you use forced tunneling?</span></span> <span data-ttu-id="f91c1-135">Le tunneling forcé est un paramètre de sous-réseau qui force l’acheminement du trafic Internet sortant vers un appareil à des fins d’inspection et de journalisation.</span><span class="sxs-lookup"><span data-stu-id="f91c1-135">Forced tunneling is a subnet setting that forces outbound Internet traffic to a device for inspection and logging.</span></span> <span data-ttu-id="f91c1-136">HDInsight ne prend pas en charge le tunneling forcé.</span><span class="sxs-lookup"><span data-stu-id="f91c1-136">HDInsight does not support forced tunneling.</span></span> <span data-ttu-id="f91c1-137">Supprimez le tunneling forcé avant d’installer HDInsight dans un sous-réseau, ou de créer un sous-réseau pour HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f91c1-137">Either remove forced tunneling before installing HDInsight into a subnet, or create a new subnet for HDInsight.</span></span>

3. <span data-ttu-id="f91c1-138">Utilisez-vous des groupes de sécurité réseau, des itinéraires définis par l'utilisateur ou des appliances de réseau virtuel pour restreindre le trafic échangé avec le réseau virtuel ?</span><span class="sxs-lookup"><span data-stu-id="f91c1-138">Do you use network security groups, user-defined routes, or Virtual Network Appliances to restrict traffic into or out of the virtual network?</span></span>

    <span data-ttu-id="f91c1-139">Service administré, HDInsight requiert un accès illimité à plusieurs adresses IP dans le centre de données Azure.</span><span class="sxs-lookup"><span data-stu-id="f91c1-139">As a managed service, HDInsight requires unrestricted access to several IP addresses in the Azure data center.</span></span> <span data-ttu-id="f91c1-140">Pour permettre la communication avec ces adresses IP, mettez à jour des groupes de sécurité réseau ou des itinéraires définis par l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f91c1-140">To allow communication with these IP addresses, update any existing network security groups or user-defined routes.</span></span>

    <span data-ttu-id="f91c1-141">HDInsight héberge plusieurs services qui une série de ports.</span><span class="sxs-lookup"><span data-stu-id="f91c1-141">HDInsight  hosts multiple services, which use a variety of ports.</span></span> <span data-ttu-id="f91c1-142">Ne bloquez pas le trafic vers ces ports.</span><span class="sxs-lookup"><span data-stu-id="f91c1-142">Do not block traffic to these ports.</span></span> <span data-ttu-id="f91c1-143">Pour obtenir la liste des ports auxquels autoriser l’accès via des pare-feu d’appliance virtuelle, voir la section [Sécurité](#security).</span><span class="sxs-lookup"><span data-stu-id="f91c1-143">For a list of ports to allow through virtual appliance firewalls, see the [Security](#security) section.</span></span>

    <span data-ttu-id="f91c1-144">Pour rechercher votre configuration de sécurité existante, utilisez les commandes Azure PowerShell ou Azure CLI suivantes :</span><span class="sxs-lookup"><span data-stu-id="f91c1-144">To find your existing security configuration, use the following Azure PowerShell or Azure CLI commands:</span></span>

    * <span data-ttu-id="f91c1-145">groupes de sécurité réseau ;</span><span class="sxs-lookup"><span data-stu-id="f91c1-145">Network security groups</span></span>

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter the resource group that contains the virtual network used with HDInsight"
        get-azurermnetworksecuritygroup -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter the name of the resource group that contains the virtual network: " RESOURCEGROUP
        az network nsg list --resource-group $RESOURCEGROUP
        ```

        <span data-ttu-id="f91c1-146">Pour plus d’informations, voir le document [Résoudre les problèmes relatifs aux groupes de sécurité réseau](../virtual-network/virtual-network-nsg-troubleshoot-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f91c1-146">For more information, see the [Troubleshoot network security groups](../virtual-network/virtual-network-nsg-troubleshoot-portal.md) document.</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="f91c1-147">Les règles de groupe de sécurité réseau sont appliquées dans un ordre basé sur leur priorité.</span><span class="sxs-lookup"><span data-stu-id="f91c1-147">Network security group rules are applied in order based on rule priority.</span></span> <span data-ttu-id="f91c1-148">La première règle correspondant au modèle de trafic est appliquée, et aucune autre n’est appliquée à ce trafic.</span><span class="sxs-lookup"><span data-stu-id="f91c1-148">The first rule that matches the traffic pattern is applied, and no others are applied for that traffic.</span></span> <span data-ttu-id="f91c1-149">Règles d’ordre de la plus permissive à la moins permissive.</span><span class="sxs-lookup"><span data-stu-id="f91c1-149">Order rules from most permissive to least permissive.</span></span> <span data-ttu-id="f91c1-150">Pour plus d’informations, voir le document [Filtrer le trafic réseau avec les groupes de sécurité réseau](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="f91c1-150">For more information, see the [Filter network traffic with network security groups](../virtual-network/virtual-networks-nsg.md) document.</span></span>

    * <span data-ttu-id="f91c1-151">Itinéraires définis par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="f91c1-151">User-defined routes</span></span>

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter the resource group that contains the virtual network used with HDInsight"
        get-azurermroutetable -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter the name of the resource group that contains the virtual network: " RESOURCEGROUP
        az network route-table list --resource-group $RESOURCEGROUP
        ```

        <span data-ttu-id="f91c1-152">Pour plus d’informations, voir le document [Résoudre les problèmes relatifs aux itinéraires](../virtual-network/virtual-network-routes-troubleshoot-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f91c1-152">For more information, see the [Troubleshoot routes](../virtual-network/virtual-network-routes-troubleshoot-portal.md) document.</span></span>

4. <span data-ttu-id="f91c1-153">Créez un cluster HDInsight et sélectionnez le réseau virtuel Azure pendant la configuration.</span><span class="sxs-lookup"><span data-stu-id="f91c1-153">Create an HDInsight cluster and select the Azure Virtual Network during configuration.</span></span> <span data-ttu-id="f91c1-154">Pour comprendre le processus de création du cluster, utilisez les étapes indiquées dans les documents suivants :</span><span class="sxs-lookup"><span data-stu-id="f91c1-154">Use the steps in the following documents to understand the cluster creation process:</span></span>

    * [<span data-ttu-id="f91c1-155">Créer un cluster HDInsight à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="f91c1-155">Create HDInsight using the Azure portal</span></span>](hdinsight-hadoop-create-linux-clusters-portal.md)
    * [<span data-ttu-id="f91c1-156">Créer un cluster HDInsight à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f91c1-156">Create HDInsight using Azure PowerShell</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
    * [<span data-ttu-id="f91c1-157">Créer un cluster HDInsight à l’aide de l’interface de ligne de commande Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="f91c1-157">Create HDInsight using Azure CLI 1.0</span></span>](hdinsight-hadoop-create-linux-clusters-azure-cli.md)
    * [<span data-ttu-id="f91c1-158">Créer un cluster HDInsight à l’aide d’un modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f91c1-158">Create HDInsight using an Azure Resource Manager template</span></span>](hdinsight-hadoop-create-linux-clusters-arm-templates.md)

  > [!IMPORTANT]
  > <span data-ttu-id="f91c1-159">L’ajout de HDInsight à un réseau virtuel est une étape de configuration facultative.</span><span class="sxs-lookup"><span data-stu-id="f91c1-159">Adding HDInsight to a virtual network is an optional configuration step.</span></span> <span data-ttu-id="f91c1-160">Veillez à sélectionner le réseau virtuel lors de la configuration du cluster.</span><span class="sxs-lookup"><span data-stu-id="f91c1-160">Be sure to select the virtual network when configuring the cluster.</span></span>

## <span data-ttu-id="f91c1-161"><a id="multinet"></a>Connexion de plusieurs réseaux</span><span class="sxs-lookup"><span data-stu-id="f91c1-161"><a id="multinet"></a>Connecting multiple networks</span></span>

<span data-ttu-id="f91c1-162">Le principal défi avec une configuration de réseau multiples est la résolution de noms entre les réseaux.</span><span class="sxs-lookup"><span data-stu-id="f91c1-162">The biggest challenge with a multi-network configuration is name resolution between the networks.</span></span>

<span data-ttu-id="f91c1-163">Azure assure la résolution de noms pour les services Azure installés dans un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f91c1-163">Azure provides name resolution for Azure services that are installed in a virtual network.</span></span> <span data-ttu-id="f91c1-164">Cette résolution de noms intégrée permet à HDInsight de se connecter aux ressources suivantes à l’aide d’un nom de domaine complet (FQDN) :</span><span class="sxs-lookup"><span data-stu-id="f91c1-164">This built-in name resolution allows HDInsight to connect to the following resources by using a fully qualified domain name (FQDN):</span></span>

* <span data-ttu-id="f91c1-165">Toute ressource disponible sur Internet.</span><span class="sxs-lookup"><span data-stu-id="f91c1-165">Any resource that is available on the internet.</span></span> <span data-ttu-id="f91c1-166">Par exemple, microsoft.com ou google.com.</span><span class="sxs-lookup"><span data-stu-id="f91c1-166">For example, microsoft.com, google.com.</span></span>

* <span data-ttu-id="f91c1-167">Toute ressource figurant dans le même réseau virtuel Azure, en utilisant le __nom DNS interne__ de la ressource.</span><span class="sxs-lookup"><span data-stu-id="f91c1-167">Any resource that is in the same Azure Virtual Network, by using the __internal DNS name__ of the resource.</span></span> <span data-ttu-id="f91c1-168">Par exemple, lorsque vous utilisez la résolution de noms par défaut, les éléments suivants sont des exemples de noms DNS internes attribués aux nœuds worker HDInsight :</span><span class="sxs-lookup"><span data-stu-id="f91c1-168">For example, when using the default name resolution, the following are example internal DNS names assigned to HDInsight worker nodes:</span></span>

    * <span data-ttu-id="f91c1-169">wn0-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="f91c1-169">wn0-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span></span>
    * <span data-ttu-id="f91c1-170">wn2-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="f91c1-170">wn2-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span></span>

    <span data-ttu-id="f91c1-171">Les deux nœuds peuvent communiquer directement entre eux et avec d’autres nœuds dans HDInsight en utilisant des noms DNS internes.</span><span class="sxs-lookup"><span data-stu-id="f91c1-171">Both these nodes can communicate directly with each other, and other nodes in HDInsight, by using internal DNS names.</span></span>

<span data-ttu-id="f91c1-172">La résolution de noms par défaut ne permet __pas__ à HDInsight de résoudre les noms des ressources en réseaux joints au réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f91c1-172">The default name resolution does __not__ allow HDInsight to resolve the names of resources in networks that are joined to the virtual network.</span></span> <span data-ttu-id="f91c1-173">Par exemple, il est courant de joindre un réseau local au réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f91c1-173">For example, it is common to join your on-premises network to the virtual network.</span></span> <span data-ttu-id="f91c1-174">Avec uniquement la résolution de noms par défaut, HDInsight ne peut pas accéder aux ressources du réseau local par leur nom.</span><span class="sxs-lookup"><span data-stu-id="f91c1-174">With only the default name resolution, HDInsight cannot access resources in the on-premises network by name.</span></span> <span data-ttu-id="f91c1-175">L’inverse est également vrai ; les ressources de votre réseau local ne peuvent pas accéder aux ressources du réseau virtuel par leur nom.</span><span class="sxs-lookup"><span data-stu-id="f91c1-175">The opposite is also true, resources in your on-premises network cannot access resources in the virtual network by name.</span></span>

> [!WARNING]
> <span data-ttu-id="f91c1-176">Vous devez créer le serveur DNS personnalisé et configurer le réseau virtuel pour l’utiliser avant de créer le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f91c1-176">You must create the custom DNS server and configure the virtual network to use it before creating the HDInsight cluster.</span></span>

<span data-ttu-id="f91c1-177">Pour permettre la résolution de noms entre le réseau virtuel et les ressources dans des réseaux joints, vous devez effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="f91c1-177">To enable name resolution between the virtual network and resources in joined networks, you must perform the following actions:</span></span>

1. <span data-ttu-id="f91c1-178">Créez un serveur DNS personnalisé dans le réseau virtuel Azure où vous prévoyez d’installer HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f91c1-178">Create a custom DNS server in the Azure Virtual Network where you plan to install HDInsight.</span></span>

2. <span data-ttu-id="f91c1-179">Configurez le réseau virtuel pour utiliser le serveur DNS personnalisé.</span><span class="sxs-lookup"><span data-stu-id="f91c1-179">Configure the virtual network to use the custom DNS server.</span></span>

3. <span data-ttu-id="f91c1-180">Recherchez le suffixe DNS qu'Azure à affecté à votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f91c1-180">Find the Azure assigned DNS suffix for your virtual network.</span></span> <span data-ttu-id="f91c1-181">Cette valeur est similaire à `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`.</span><span class="sxs-lookup"><span data-stu-id="f91c1-181">This value is similar to `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`.</span></span> <span data-ttu-id="f91c1-182">Pour plus d’informations sur la recherche de suffixe DNS, voir la section [Exemple : DNS personnalisé](#example-dns).</span><span class="sxs-lookup"><span data-stu-id="f91c1-182">For information on finding the DNS suffix, see the [Example: Custom DNS](#example-dns) section.</span></span>

4. <span data-ttu-id="f91c1-183">Configurez le transfert entre les serveurs DNS.</span><span class="sxs-lookup"><span data-stu-id="f91c1-183">Configure forwarding between the DNS servers.</span></span> <span data-ttu-id="f91c1-184">La configuration dépend du type de réseau distant.</span><span class="sxs-lookup"><span data-stu-id="f91c1-184">The configuration depends on the type of remote network.</span></span>

    * <span data-ttu-id="f91c1-185">Si le réseau distant est un réseau local, configurez le DNS comme suit :</span><span class="sxs-lookup"><span data-stu-id="f91c1-185">If the remote network is an on-premises network, configure DNS as follows:</span></span>
        
        * <span data-ttu-id="f91c1-186">__DNS personnalisé__ (dans le réseau virtuel) :</span><span class="sxs-lookup"><span data-stu-id="f91c1-186">__Custom DNS__ (in the virtual network):</span></span>

            * <span data-ttu-id="f91c1-187">Transférez les demandes relatives au suffixe DNS du réseau virtuel au programme de résolution récursive d’Azure (168.63.129.16).</span><span class="sxs-lookup"><span data-stu-id="f91c1-187">Forward requests for the DNS suffix of the virtual network to the Azure recursive resolver (168.63.129.16).</span></span> <span data-ttu-id="f91c1-188">Azure gère les demandes de ressources dans le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f91c1-188">Azure handles requests for resources in the virtual network</span></span>

            * <span data-ttu-id="f91c1-189">Transférez toutes les autres demandes au serveur DNS local.</span><span class="sxs-lookup"><span data-stu-id="f91c1-189">Forward all other requests to the on-premises DNS server.</span></span> <span data-ttu-id="f91c1-190">Le serveur DNS local gère toutes les autres demandes de résolution de noms, y compris les demandes de ressources Internet telles que Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="f91c1-190">The on-premises DNS handles all other name resolution requests, even requests for internet resources such as Microsoft.com.</span></span>

        * <span data-ttu-id="f91c1-191">__DNS local__ : transférez les demandes de suffixe DNS de réseau virtuel vers le serveur DNS personnalisé.</span><span class="sxs-lookup"><span data-stu-id="f91c1-191">__On-premises DNS__: Forward requests for the virtual network DNS suffix to the custom DNS server.</span></span> <span data-ttu-id="f91c1-192">Le serveur DNS personnalisé transfère alors les demandes au programme de résolution récursive d’Azure.</span><span class="sxs-lookup"><span data-stu-id="f91c1-192">The custom DNS server then forwards to the Azure recursive resolver.</span></span>

        <span data-ttu-id="f91c1-193">Cette configuration a pour effet de router les demandes de noms de domaine complets (FQDN) qui contiennent le suffixe DNS du réseau virtuel vers le serveur DNS personnalisé.</span><span class="sxs-lookup"><span data-stu-id="f91c1-193">This configuration routes requests for fully qualified domain names that contain the DNS suffix of the virtual network to the custom DNS server.</span></span> <span data-ttu-id="f91c1-194">Toutes les autres demandes (même d’adresses Internet publiques) sont gérées par le serveur DNS local.</span><span class="sxs-lookup"><span data-stu-id="f91c1-194">All other requests (even for public internet addresses) are handled by the on-premises DNS server.</span></span>

    * <span data-ttu-id="f91c1-195">Si le réseau distant est un autre réseau virtuel Azure, configurez DNS comme suit :</span><span class="sxs-lookup"><span data-stu-id="f91c1-195">If the remote network is another Azure Virtual Network, configure DNS as follows:</span></span>

        * <span data-ttu-id="f91c1-196">__DNS personnalisé__ (dans chaque réseau virtuel) :</span><span class="sxs-lookup"><span data-stu-id="f91c1-196">__Custom DNS__ (in each virtual network):</span></span>

            * <span data-ttu-id="f91c1-197">Les demandes de suffixe DNS des réseaux virtuels sont transférées aux serveurs DNS personnalisés.</span><span class="sxs-lookup"><span data-stu-id="f91c1-197">Requests for the DNS suffix of the virtual networks are forwarded to the custom DNS servers.</span></span> <span data-ttu-id="f91c1-198">Le DNS de chaque réseau virtuel est chargé de résoudre les ressources au sein de son réseau.</span><span class="sxs-lookup"><span data-stu-id="f91c1-198">The DNS in each virtual network is responsible for resolving resources within its network.</span></span>

            * <span data-ttu-id="f91c1-199">Transférez toutes les autres demandes au programme de résolution récursive d’Azure.</span><span class="sxs-lookup"><span data-stu-id="f91c1-199">Forward all other requests to the Azure recursive resolver.</span></span> <span data-ttu-id="f91c1-200">Le programme de résolution récursive est responsable de la résolution des ressources locales et Internet.</span><span class="sxs-lookup"><span data-stu-id="f91c1-200">The recursive resolver is responsible for resolving local and internet resources.</span></span>

        <span data-ttu-id="f91c1-201">Le serveur DNS de chaque réseau transfère les demandes à l’autre, en fonction du suffixe DNS.</span><span class="sxs-lookup"><span data-stu-id="f91c1-201">The DNS server for each network forwards requests to the other, based on DNS suffix.</span></span> <span data-ttu-id="f91c1-202">Les autres requêtes sont résolues à l’aide du programme de résolution récursive d’Azure.</span><span class="sxs-lookup"><span data-stu-id="f91c1-202">Other requests are resolved using the Azure recursive resolver.</span></span>

    <span data-ttu-id="f91c1-203">Pour un exemple de chaque configuration, voir la section [Exemple : DNS personnalisé](#example-dns).</span><span class="sxs-lookup"><span data-stu-id="f91c1-203">For an example of each configuration, see the [Example: Custom DNS](#example-dns) section.</span></span>

<span data-ttu-id="f91c1-204">Pour plus d’informations, voir le document [Résolution de noms pour les machines virtuelles et les instances de rôle](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="f91c1-204">For more information, see the [Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) document.</span></span>

## <a name="directly-connect-to-hadoop-services"></a><span data-ttu-id="f91c1-205">Se connecter directement aux services Hadoop</span><span class="sxs-lookup"><span data-stu-id="f91c1-205">Directly connect to Hadoop services</span></span>

<span data-ttu-id="f91c1-206">L’essentiel de la documentation relative à HDInsight part du principe que vous avez accès au cluster via Internet.</span><span class="sxs-lookup"><span data-stu-id="f91c1-206">Most documentation on HDInsight assumes that you have access to the cluster over the internet.</span></span> <span data-ttu-id="f91c1-207">Par exemple, vous pouvez vous connecter au cluster à l’adresse https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="f91c1-207">For example, that you can connect to the cluster at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="f91c1-208">Cette adresse utilise la passerelle publique qui n’est pas disponible si vous avez utilisé des groupes de sécurité réseau ou des itinéraires définis par l’utilisateur pour restreindre l’accès à partir d’Internet.</span><span class="sxs-lookup"><span data-stu-id="f91c1-208">This address uses the public gateway, which is not available if you have used NSGs or UDRs to restrict access from the internet.</span></span>

<span data-ttu-id="f91c1-209">Pour vous connecter à Ambari et à d’autres pages web via le réseau virtuel, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f91c1-209">To connect to Ambari and other web pages through the virtual network, use the following steps:</span></span>

1. <span data-ttu-id="f91c1-210">Pour découvrir les noms de domaine complets (FQDN) internes des nœuds de cluster HDInsight, utilisez l’une des méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="f91c1-210">To discover the internal fully qualified domain names (FQDN) of the HDInsight cluster nodes, use one of the following methods:</span></span>

    ```powershell
    $resourceGroupName = "The resource group that contains the virtual network used with HDInsight"

    $clusterNICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName | where-object {$_.Name -like "*node*"}

    $nodes = @()
    foreach($nic in $clusterNICs) {
        $node = new-object System.Object
        $node | add-member -MemberType NoteProperty -name "Type" -value $nic.Name.Split('-')[1]
        $node | add-member -MemberType NoteProperty -name "InternalIP" -value $nic.IpConfigurations.PrivateIpAddress
        $node | add-member -MemberType NoteProperty -name "InternalFQDN" -value $nic.DnsSettings.InternalFqdn
        $nodes += $node
    }
    $nodes | sort-object Type
    ```

    ```azurecli
    az network nic list --resource-group <resourcegroupname> --output table --query "[?contains(name,'node')].{NICname:name,InternalIP:ipConfigurations[0].privateIpAddress,InternalFQDN:dnsSettings.internalFqdn}"
    ```

    <span data-ttu-id="f91c1-211">Dans la liste des nœuds retournés, recherchez le nom de domaine complet des nœuds principaux, puis utilisez-les pour vous connecter à Ambari et à d’autres services web.</span><span class="sxs-lookup"><span data-stu-id="f91c1-211">In the list of nodes returned, find the FQDN for the head nodes and use the FQDNs to connect to Ambari and other web services.</span></span> <span data-ttu-id="f91c1-212">Par exemple, utilisez `http://<headnode-fqdn>:8080` pour accéder à Ambari.</span><span class="sxs-lookup"><span data-stu-id="f91c1-212">For example, use `http://<headnode-fqdn>:8080` to access Ambari.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="f91c1-213">Certains services hébergés sur les nœuds principaux ne sont actifs que sur un seul nœud à la fois.</span><span class="sxs-lookup"><span data-stu-id="f91c1-213">Some services hosted on the head nodes are only active on one node at a time.</span></span> <span data-ttu-id="f91c1-214">Si vous tentez d’accéder à un service sur un nœud principal et que l’opération retourne l’erreur 404, basculez vers l’autre nœud principal.</span><span class="sxs-lookup"><span data-stu-id="f91c1-214">If you try accessing a service on one head node and it returns a 404 error, switch to the other head node.</span></span>

2. <span data-ttu-id="f91c1-215">Pour déterminer le nœud et le port sur lesquels un service est disponible, voir [Ports utilisés par les services Hadoop dans HDInsight](./hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="f91c1-215">To determine the node and port that a service is available on, see the [Ports used by Hadoop services on HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

## <span data-ttu-id="f91c1-216"><a id="networktraffic"></a> Contrôler le trafic réseau</span><span class="sxs-lookup"><span data-stu-id="f91c1-216"><a id="networktraffic"></a> Controlling network traffic</span></span>

<span data-ttu-id="f91c1-217">Le trafic réseau dans les réseaux virtuels Azure peut être contrôlé à l’aide des méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="f91c1-217">Network traffic in an Azure Virtual Networks can be controlled using the following methods:</span></span>

* <span data-ttu-id="f91c1-218">Les **Groupes de sécurité réseau** (NSG) vous permettent de filtrer le trafic entrant et sortant changé avec le réseau.</span><span class="sxs-lookup"><span data-stu-id="f91c1-218">**Network security groups** (NSG) allow you to filter inbound and outbound traffic to the network.</span></span> <span data-ttu-id="f91c1-219">Pour plus d’informations, voir le document [Filtrer le trafic réseau avec les groupes de sécurité réseau](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="f91c1-219">For more information, see the [Filter network traffic with network security groups](../virtual-network/virtual-networks-nsg.md) document.</span></span>

    > [!WARNING]
    > <span data-ttu-id="f91c1-220">HDInsight ne prend pas en charge la restriction du trafic sortant.</span><span class="sxs-lookup"><span data-stu-id="f91c1-220">HDInsight does not support restricting outbound traffic.</span></span>

* <span data-ttu-id="f91c1-221">Les **Itinéraires définis par l’utilisateur** définissent la manière dont trafic circule entre les ressources du réseau.</span><span class="sxs-lookup"><span data-stu-id="f91c1-221">**User-defined routes** (UDR) define how traffic flows between resources in the network.</span></span> <span data-ttu-id="f91c1-222">Pour plus d’informations, voir le document [Itinéraires définis par l’utilisateur et transfert IP](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f91c1-222">For more information, see the [User-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md) document.</span></span>

* <span data-ttu-id="f91c1-223">Les **appliances virtuelles réseau** répliquent les fonctionnalités d’appareils tels que des routeurs et pare-feu.</span><span class="sxs-lookup"><span data-stu-id="f91c1-223">**Network virtual appliances** replicate the functionality of devices such as firewalls and routers.</span></span> <span data-ttu-id="f91c1-224">Pour plus d’informations, voir le document [Appliances réseau](https://azure.microsoft.com/solutions/network-appliances).</span><span class="sxs-lookup"><span data-stu-id="f91c1-224">For more information, see the [Network Appliances](https://azure.microsoft.com/solutions/network-appliances) document.</span></span>

<span data-ttu-id="f91c1-225">Service administré, HDInsight requiert un accès illimité aux services de gestion et de contrôle d’intégrité Azure dans le cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="f91c1-225">As a managed service, HDInsight requires unrestricted access to Azure health and management services in the Azure cloud.</span></span> <span data-ttu-id="f91c1-226">Lorsque vous utilisez des groupes de sécurité réseau et des itinéraires définis par l’utilisateur, vous devez vous assurer que ces services peuvent toujours communiquer avec HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f91c1-226">When using NSGs and UDRs, you must ensure that HDInsight these services can still communicate with HDInsight.</span></span>

<span data-ttu-id="f91c1-227">HDInsight expose des services sur plusieurs ports.</span><span class="sxs-lookup"><span data-stu-id="f91c1-227">HDInsight exposes services on several ports.</span></span> <span data-ttu-id="f91c1-228">Lorsque vous utilisez un pare-feu d’appliance virtuelle, vous devez autoriser le trafic sur les ports utilisés pour ces services.</span><span class="sxs-lookup"><span data-stu-id="f91c1-228">When using a virtual appliance firewall, you must allow traffic on the ports used for these services.</span></span> <span data-ttu-id="f91c1-229">Pour plus d’informations, voir la section [Ports requis].</span><span class="sxs-lookup"><span data-stu-id="f91c1-229">For more information, see the [Required ports] section.</span></span>

### <span data-ttu-id="f91c1-230"><a id="hdinsight-ip"></a> HDInsight avec des groupes de sécurité réseau et des itinéraires définis par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="f91c1-230"><a id="hdinsight-ip"></a> HDInsight with network security groups and user-defined routes</span></span>

<span data-ttu-id="f91c1-231">Si vous prévoyez d’utiliser des **groupes de sécurité réseau** ou des **itinéraires définis par l’utilisateur** pour contrôler le trafic réseau, effectuez les actions suivantes avant d’installer HDInsight :</span><span class="sxs-lookup"><span data-stu-id="f91c1-231">If you plan on using **network security groups** or **user-defined routes** to control network traffic, perform the following actions before installing HDInsight:</span></span>

1. <span data-ttu-id="f91c1-232">Identifiez la région Azure que vous projetez d’utiliser pour HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f91c1-232">Identify the Azure region that you plan to use for HDInsight.</span></span>

2. <span data-ttu-id="f91c1-233">Identifiez les adresses IP que HDInsight requiert.</span><span class="sxs-lookup"><span data-stu-id="f91c1-233">Identify the IP addresses required by HDInsight.</span></span> <span data-ttu-id="f91c1-234">Pour plus d’informations, consultez la section [Adresses IP requises par HDInsight](#hdinsight-ip).</span><span class="sxs-lookup"><span data-stu-id="f91c1-234">For more information, see the [IP Addresses required by HDInsight](#hdinsight-ip) section.</span></span>

3. <span data-ttu-id="f91c1-235">Créez ou modifiez les groupes de sécurité réseau ou les itinéraires définis par l’utilisateur pour le sous-réseau dans lequel vous prévoyez d’installer HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f91c1-235">Create or modify the network security groups or user-defined routes for the subnet that you plan to install HDInsight into.</span></span>

    * <span data-ttu-id="f91c1-236">__Groupes de sécurité réseau__ : autorisez le trafic __entrant__ sur le port __443__ à partir des adresses IP.</span><span class="sxs-lookup"><span data-stu-id="f91c1-236">__Network security groups__: allow __inbound__ traffic on port __443__ from the IP addresses.</span></span>
    * <span data-ttu-id="f91c1-237">__Itinéraires définis par l’utilisateur__ : créez un itinéraire pour chaque adresse IP et définissez __Type de tronçon suivant__ sur __Internet__.</span><span class="sxs-lookup"><span data-stu-id="f91c1-237">__User-defined routes__: create a route to each IP address and set the __Next hop type__ to __Internet__.</span></span>

<span data-ttu-id="f91c1-238">Pour plus d’informations sur les groupes de sécurité réseau ou les itinéraires définis par l’utilisateur, voir la documentation suivante :</span><span class="sxs-lookup"><span data-stu-id="f91c1-238">For more information on network security groups or user-defined routes, see the following documentation:</span></span>

* [<span data-ttu-id="f91c1-239">Groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="f91c1-239">Network security group</span></span>](../virtual-network/virtual-networks-nsg.md)

* [<span data-ttu-id="f91c1-240">Itinéraires définis par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="f91c1-240">User-defined routes</span></span>](../virtual-network/virtual-networks-udr-overview.md)

#### <a name="forced-tunneling"></a><span data-ttu-id="f91c1-241">Tunneling forcé</span><span class="sxs-lookup"><span data-stu-id="f91c1-241">Forced tunneling</span></span>

<span data-ttu-id="f91c1-242">Le tunneling forcé est une configuration d’itinéraire défini par l’utilisateur où tout le trafic en provenance d’un sous-réseau est acheminé de force vers un réseau ou un emplacement spécifique, tel que votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="f91c1-242">Forced tunneling is a user-defined routing configuration where all traffic from a subnet is forced to a specific network or location, such as your on-premises network.</span></span> <span data-ttu-id="f91c1-243">HDInsight ne prend __pas__ en charge le tunneling forcé.</span><span class="sxs-lookup"><span data-stu-id="f91c1-243">HDInsight does __not__ support forced tunneling.</span></span>

## <span data-ttu-id="f91c1-244"><a id="hdinsight-ip"></a> Adresses IP requises</span><span class="sxs-lookup"><span data-stu-id="f91c1-244"><a id="hdinsight-ip"></a> Required IP addresses</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f91c1-245">Les services de gestion et de contrôle d’intégrité Azure doivent être en mesure de communiquer avec HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f91c1-245">The Azure health and management services must be able to communicate with HDInsight.</span></span> <span data-ttu-id="f91c1-246">Si vous utilisez des groupes de sécurité réseau ou des itinéraires définis par l’utilisateur, autorisez le trafic provenant des adresses IP de ces services à se diriger vers HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f91c1-246">If you use network security groups or user-defined routes, allow traffic from the IP addresses for these services to reach HDInsight.</span></span>
>
> <span data-ttu-id="f91c1-247">Si vous n’utilisez pas de groupes de sécurité réseau ou d’itinéraires définis par l’utilisateur pour contrôler le trafic, vous pouvez ignorer cette section.</span><span class="sxs-lookup"><span data-stu-id="f91c1-247">If you do not use network security groups or user-defined routes to control traffic, you can ignore this section.</span></span>

<span data-ttu-id="f91c1-248">Si vous utilisez des groupes de sécurité réseau ou des itinéraires définis par l’utilisateur, vous devez autoriser le trafic provenant des services de gestion et d’intégrité Azure à se diriger vers HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f91c1-248">If you use network security groups or user-defined routes, you must allow traffic from the Azure health and management services to reach HDInsight.</span></span> <span data-ttu-id="f91c1-249">Pour trouver les adresses IP qui doivent être autorisées, effectuez les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="f91c1-249">Use the following steps to find the IP addresses that must be allowed:</span></span>

1. <span data-ttu-id="f91c1-250">Vous devez toujours autoriser le trafic à partir des adresses IP suivantes :</span><span class="sxs-lookup"><span data-stu-id="f91c1-250">You must always allow traffic from the following IP addresses:</span></span>

    | <span data-ttu-id="f91c1-251">Adresse IP</span><span class="sxs-lookup"><span data-stu-id="f91c1-251">IP address</span></span> | <span data-ttu-id="f91c1-252">Port autorisé</span><span class="sxs-lookup"><span data-stu-id="f91c1-252">Allowed port</span></span> | <span data-ttu-id="f91c1-253">Direction</span><span class="sxs-lookup"><span data-stu-id="f91c1-253">Direction</span></span> |
    | ---- | ----- | ----- |
    | <span data-ttu-id="f91c1-254">168.61.49.99</span><span class="sxs-lookup"><span data-stu-id="f91c1-254">168.61.49.99</span></span> | <span data-ttu-id="f91c1-255">443</span><span class="sxs-lookup"><span data-stu-id="f91c1-255">443</span></span> | <span data-ttu-id="f91c1-256">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="f91c1-256">Inbound</span></span> |
    | <span data-ttu-id="f91c1-257">23.99.5.239</span><span class="sxs-lookup"><span data-stu-id="f91c1-257">23.99.5.239</span></span> | <span data-ttu-id="f91c1-258">443</span><span class="sxs-lookup"><span data-stu-id="f91c1-258">443</span></span> | <span data-ttu-id="f91c1-259">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="f91c1-259">Inbound</span></span> |
    | <span data-ttu-id="f91c1-260">168.61.48.131</span><span class="sxs-lookup"><span data-stu-id="f91c1-260">168.61.48.131</span></span> | <span data-ttu-id="f91c1-261">443</span><span class="sxs-lookup"><span data-stu-id="f91c1-261">443</span></span> | <span data-ttu-id="f91c1-262">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="f91c1-262">Inbound</span></span> |
    | <span data-ttu-id="f91c1-263">138.91.141.162</span><span class="sxs-lookup"><span data-stu-id="f91c1-263">138.91.141.162</span></span> | <span data-ttu-id="f91c1-264">443</span><span class="sxs-lookup"><span data-stu-id="f91c1-264">443</span></span> | <span data-ttu-id="f91c1-265">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="f91c1-265">Inbound</span></span> |

2. <span data-ttu-id="f91c1-266">Si votre cluster HDInsight est dans une des régions suivantes, vous devez autoriser le trafic à partir des adresses IP répertoriées pour la région concernée :</span><span class="sxs-lookup"><span data-stu-id="f91c1-266">If your HDInsight cluster is in one of the following regions, then you must allow traffic from the IP addresses listed for the region:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="f91c1-267">Si la région Azure que vous utilisez n’est pas répertoriée, utilisez uniquement les quatre adresses IP de l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="f91c1-267">If the Azure region you are using is not listed, then only use the four IP addresses from step 1.</span></span>

    | <span data-ttu-id="f91c1-268">Pays</span><span class="sxs-lookup"><span data-stu-id="f91c1-268">Country</span></span> | <span data-ttu-id="f91c1-269">Région</span><span class="sxs-lookup"><span data-stu-id="f91c1-269">Region</span></span> | <span data-ttu-id="f91c1-270">Adresses IP autorisées</span><span class="sxs-lookup"><span data-stu-id="f91c1-270">Allowed IP addresses</span></span> | <span data-ttu-id="f91c1-271">Port autorisé</span><span class="sxs-lookup"><span data-stu-id="f91c1-271">Allowed port</span></span> | <span data-ttu-id="f91c1-272">Direction</span><span class="sxs-lookup"><span data-stu-id="f91c1-272">Direction</span></span> |
    | ---- | ---- | ---- | ---- | ----- |
    | <span data-ttu-id="f91c1-273">Asie</span><span class="sxs-lookup"><span data-stu-id="f91c1-273">Asia</span></span> | <span data-ttu-id="f91c1-274">Est de l'Asie</span><span class="sxs-lookup"><span data-stu-id="f91c1-274">East Asia</span></span> | <span data-ttu-id="f91c1-275">23.102.235.122</span><span class="sxs-lookup"><span data-stu-id="f91c1-275">23.102.235.122</span></span></br><span data-ttu-id="f91c1-276">52.175.38.134</span><span class="sxs-lookup"><span data-stu-id="f91c1-276">52.175.38.134</span></span> | <span data-ttu-id="f91c1-277">443</span><span class="sxs-lookup"><span data-stu-id="f91c1-277">443</span></span> | <span data-ttu-id="f91c1-278">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="f91c1-278">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="f91c1-279">Asie du Sud-Est</span><span class="sxs-lookup"><span data-stu-id="f91c1-279">Southeast Asia</span></span> | <span data-ttu-id="f91c1-280">13.76.245.160</span><span class="sxs-lookup"><span data-stu-id="f91c1-280">13.76.245.160</span></span></br><span data-ttu-id="f91c1-281">13.76.136.249</span><span class="sxs-lookup"><span data-stu-id="f91c1-281">13.76.136.249</span></span> | <span data-ttu-id="f91c1-282">443</span><span class="sxs-lookup"><span data-stu-id="f91c1-282">443</span></span> | <span data-ttu-id="f91c1-283">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="f91c1-283">Inbound</span></span> |
    | <span data-ttu-id="f91c1-284">Australie</span><span class="sxs-lookup"><span data-stu-id="f91c1-284">Australia</span></span> | <span data-ttu-id="f91c1-285">Est de l’Australie</span><span class="sxs-lookup"><span data-stu-id="f91c1-285">Australia East</span></span> | <span data-ttu-id="f91c1-286">104.210.84.115</span><span class="sxs-lookup"><span data-stu-id="f91c1-286">104.210.84.115</span></span></br><span data-ttu-id="f91c1-287">13.75.152.195</span><span class="sxs-lookup"><span data-stu-id="f91c1-287">13.75.152.195</span></span> | <span data-ttu-id="f91c1-288">443</span><span class="sxs-lookup"><span data-stu-id="f91c1-288">443</span></span> | <span data-ttu-id="f91c1-289">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="f91c1-289">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="f91c1-290">Sud-est de l’Australie</span><span class="sxs-lookup"><span data-stu-id="f91c1-290">Australia Southeast</span></span> | <span data-ttu-id="f91c1-291">13.77.2.56</span><span class="sxs-lookup"><span data-stu-id="f91c1-291">13.77.2.56</span></span></br><span data-ttu-id="f91c1-292">13.77.2.94</span><span class="sxs-lookup"><span data-stu-id="f91c1-292">13.77.2.94</span></span> | <span data-ttu-id="f91c1-293">443</span><span class="sxs-lookup"><span data-stu-id="f91c1-293">443</span></span> | <span data-ttu-id="f91c1-294">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="f91c1-294">Inbound</span></span> |
    | <span data-ttu-id="f91c1-295">Brésil</span><span class="sxs-lookup"><span data-stu-id="f91c1-295">Brazil</span></span> | <span data-ttu-id="f91c1-296">Sud du Brésil</span><span class="sxs-lookup"><span data-stu-id="f91c1-296">Brazil South</span></span> | <span data-ttu-id="f91c1-297">191.235.84.104</span><span class="sxs-lookup"><span data-stu-id="f91c1-297">191.235.84.104</span></span></br><span data-ttu-id="f91c1-298">191.235.87.113</span><span class="sxs-lookup"><span data-stu-id="f91c1-298">191.235.87.113</span></span> | <span data-ttu-id="f91c1-299">443</span><span class="sxs-lookup"><span data-stu-id="f91c1-299">443</span></span> | <span data-ttu-id="f91c1-300">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="f91c1-300">Inbound</span></span> |
    | <span data-ttu-id="f91c1-301">Canada</span><span class="sxs-lookup"><span data-stu-id="f91c1-301">Canada</span></span> | <span data-ttu-id="f91c1-302">Est du Canada</span><span class="sxs-lookup"><span data-stu-id="f91c1-302">Canada East</span></span> | <span data-ttu-id="f91c1-303">52.229.127.96</span><span class="sxs-lookup"><span data-stu-id="f91c1-303">52.229.127.96</span></span></br><span data-ttu-id="f91c1-304">52.229.123.172</span><span class="sxs-lookup"><span data-stu-id="f91c1-304">52.229.123.172</span></span> | <span data-ttu-id="f91c1-305">443</span><span class="sxs-lookup"><span data-stu-id="f91c1-305">443</span></span> | <span data-ttu-id="f91c1-306">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="f91c1-306">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="f91c1-307">Centre du Canada</span><span class="sxs-lookup"><span data-stu-id="f91c1-307">Canada Central</span></span> | <span data-ttu-id="f91c1-308">52.228.37.66</span><span class="sxs-lookup"><span data-stu-id="f91c1-308">52.228.37.66</span></span></br><span data-ttu-id="f91c1-309">52.228.45.222</span><span class="sxs-lookup"><span data-stu-id="f91c1-309">52.228.45.222</span></span> | <span data-ttu-id="f91c1-310">443</span><span class="sxs-lookup"><span data-stu-id="f91c1-310">443</span></span> | <span data-ttu-id="f91c1-311">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="f91c1-311">Inbound</span></span> |
    | <span data-ttu-id="f91c1-312">Chine</span><span class="sxs-lookup"><span data-stu-id="f91c1-312">China</span></span> | <span data-ttu-id="f91c1-313">Chine du Nord</span><span class="sxs-lookup"><span data-stu-id="f91c1-313">China North</span></span> | <span data-ttu-id="f91c1-314">42.159.96.170</span><span class="sxs-lookup"><span data-stu-id="f91c1-314">42.159.96.170</span></span></br><span data-ttu-id="f91c1-315">139.217.2.219</span><span class="sxs-lookup"><span data-stu-id="f91c1-315">139.217.2.219</span></span> | <span data-ttu-id="f91c1-316">443</span><span class="sxs-lookup"><span data-stu-id="f91c1-316">443</span></span> | <span data-ttu-id="f91c1-317">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="f91c1-317">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="f91c1-318">Chine orientale</span><span class="sxs-lookup"><span data-stu-id="f91c1-318">China East</span></span> | <span data-ttu-id="f91c1-319">42.159.198.178</span><span class="sxs-lookup"><span data-stu-id="f91c1-319">42.159.198.178</span></span></br><span data-ttu-id="f91c1-320">42.159.234.157</span><span class="sxs-lookup"><span data-stu-id="f91c1-320">42.159.234.157</span></span> | <span data-ttu-id="f91c1-321">443</span><span class="sxs-lookup"><span data-stu-id="f91c1-321">443</span></span> | <span data-ttu-id="f91c1-322">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="f91c1-322">Inbound</span></span> |
    | <span data-ttu-id="f91c1-323">Europe</span><span class="sxs-lookup"><span data-stu-id="f91c1-323">Europe</span></span> | <span data-ttu-id="f91c1-324">Europe du Nord</span><span class="sxs-lookup"><span data-stu-id="f91c1-324">North Europe</span></span> | <span data-ttu-id="f91c1-325">52.164.210.96</span><span class="sxs-lookup"><span data-stu-id="f91c1-325">52.164.210.96</span></span></br><span data-ttu-id="f91c1-326">13.74.153.132</span><span class="sxs-lookup"><span data-stu-id="f91c1-326">13.74.153.132</span></span> | <span data-ttu-id="f91c1-327">443</span><span class="sxs-lookup"><span data-stu-id="f91c1-327">443</span></span> | <span data-ttu-id="f91c1-328">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="f91c1-328">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="f91c1-329">Europe de l'Ouest</span><span class="sxs-lookup"><span data-stu-id="f91c1-329">West Europe</span></span>| <span data-ttu-id="f91c1-330">52.166.243.90</span><span class="sxs-lookup"><span data-stu-id="f91c1-330">52.166.243.90</span></span></br><span data-ttu-id="f91c1-331">52.174.36.244</span><span class="sxs-lookup"><span data-stu-id="f91c1-331">52.174.36.244</span></span> | <span data-ttu-id="f91c1-332">443</span><span class="sxs-lookup"><span data-stu-id="f91c1-332">443</span></span> | <span data-ttu-id="f91c1-333">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="f91c1-333">Inbound</span></span> |
    | <span data-ttu-id="f91c1-334">Allemagne</span><span class="sxs-lookup"><span data-stu-id="f91c1-334">Germany</span></span> | <span data-ttu-id="f91c1-335">Centre de l’Allemagne</span><span class="sxs-lookup"><span data-stu-id="f91c1-335">Germany Central</span></span> | <span data-ttu-id="f91c1-336">51.4.146.68</span><span class="sxs-lookup"><span data-stu-id="f91c1-336">51.4.146.68</span></span></br><span data-ttu-id="f91c1-337">51.4.146.80</span><span class="sxs-lookup"><span data-stu-id="f91c1-337">51.4.146.80</span></span> | <span data-ttu-id="f91c1-338">443</span><span class="sxs-lookup"><span data-stu-id="f91c1-338">443</span></span> | <span data-ttu-id="f91c1-339">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="f91c1-339">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="f91c1-340">Nord-Est de l’Allemagne</span><span class="sxs-lookup"><span data-stu-id="f91c1-340">Germany Northeast</span></span> | <span data-ttu-id="f91c1-341">51.5.150.132</span><span class="sxs-lookup"><span data-stu-id="f91c1-341">51.5.150.132</span></span></br><span data-ttu-id="f91c1-342">51.5.144.101</span><span class="sxs-lookup"><span data-stu-id="f91c1-342">51.5.144.101</span></span> | <span data-ttu-id="f91c1-343">443</span><span class="sxs-lookup"><span data-stu-id="f91c1-343">443</span></span> | <span data-ttu-id="f91c1-344">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="f91c1-344">Inbound</span></span> |
    | <span data-ttu-id="f91c1-345">Inde</span><span class="sxs-lookup"><span data-stu-id="f91c1-345">India</span></span> | <span data-ttu-id="f91c1-346">Inde centrale</span><span class="sxs-lookup"><span data-stu-id="f91c1-346">Central India</span></span> | <span data-ttu-id="f91c1-347">52.172.153.209</span><span class="sxs-lookup"><span data-stu-id="f91c1-347">52.172.153.209</span></span></br><span data-ttu-id="f91c1-348">52.172.152.49</span><span class="sxs-lookup"><span data-stu-id="f91c1-348">52.172.152.49</span></span> | <span data-ttu-id="f91c1-349">443</span><span class="sxs-lookup"><span data-stu-id="f91c1-349">443</span></span> | <span data-ttu-id="f91c1-350">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="f91c1-350">Inbound</span></span> |
    | <span data-ttu-id="f91c1-351">Japon</span><span class="sxs-lookup"><span data-stu-id="f91c1-351">Japan</span></span> | <span data-ttu-id="f91c1-352">Est du Japon</span><span class="sxs-lookup"><span data-stu-id="f91c1-352">Japan East</span></span> | <span data-ttu-id="f91c1-353">13.78.125.90</span><span class="sxs-lookup"><span data-stu-id="f91c1-353">13.78.125.90</span></span></br><span data-ttu-id="f91c1-354">13.78.89.60</span><span class="sxs-lookup"><span data-stu-id="f91c1-354">13.78.89.60</span></span> | <span data-ttu-id="f91c1-355">443</span><span class="sxs-lookup"><span data-stu-id="f91c1-355">443</span></span> | <span data-ttu-id="f91c1-356">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="f91c1-356">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="f91c1-357">Ouest du Japon</span><span class="sxs-lookup"><span data-stu-id="f91c1-357">Japan West</span></span> | <span data-ttu-id="f91c1-358">40.74.125.69</span><span class="sxs-lookup"><span data-stu-id="f91c1-358">40.74.125.69</span></span></br><span data-ttu-id="f91c1-359">138.91.29.150</span><span class="sxs-lookup"><span data-stu-id="f91c1-359">138.91.29.150</span></span> | <span data-ttu-id="f91c1-360">443</span><span class="sxs-lookup"><span data-stu-id="f91c1-360">443</span></span> | <span data-ttu-id="f91c1-361">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="f91c1-361">Inbound</span></span> |
    | <span data-ttu-id="f91c1-362">Corée du Sud</span><span class="sxs-lookup"><span data-stu-id="f91c1-362">Korea</span></span> | <span data-ttu-id="f91c1-363">Centre de la Corée</span><span class="sxs-lookup"><span data-stu-id="f91c1-363">Korea Central</span></span> | <span data-ttu-id="f91c1-364">52.231.39.142</span><span class="sxs-lookup"><span data-stu-id="f91c1-364">52.231.39.142</span></span></br><span data-ttu-id="f91c1-365">52.231.36.209</span><span class="sxs-lookup"><span data-stu-id="f91c1-365">52.231.36.209</span></span> | <span data-ttu-id="f91c1-366">433</span><span class="sxs-lookup"><span data-stu-id="f91c1-366">433</span></span> | <span data-ttu-id="f91c1-367">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="f91c1-367">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="f91c1-368">Corée du Sud</span><span class="sxs-lookup"><span data-stu-id="f91c1-368">Korea South</span></span> | <span data-ttu-id="f91c1-369">52.231.203.16</span><span class="sxs-lookup"><span data-stu-id="f91c1-369">52.231.203.16</span></span></br><span data-ttu-id="f91c1-370">52.231.205.214</span><span class="sxs-lookup"><span data-stu-id="f91c1-370">52.231.205.214</span></span> | <span data-ttu-id="f91c1-371">443</span><span class="sxs-lookup"><span data-stu-id="f91c1-371">443</span></span> | <span data-ttu-id="f91c1-372">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="f91c1-372">Inbound</span></span>
    | <span data-ttu-id="f91c1-373">Royaume-Uni</span><span class="sxs-lookup"><span data-stu-id="f91c1-373">United Kingdom</span></span> | <span data-ttu-id="f91c1-374">Ouest du Royaume-Uni</span><span class="sxs-lookup"><span data-stu-id="f91c1-374">UK West</span></span> | <span data-ttu-id="f91c1-375">51.141.13.110</span><span class="sxs-lookup"><span data-stu-id="f91c1-375">51.141.13.110</span></span></br><span data-ttu-id="f91c1-376">51.141.7.20</span><span class="sxs-lookup"><span data-stu-id="f91c1-376">51.141.7.20</span></span> | <span data-ttu-id="f91c1-377">443</span><span class="sxs-lookup"><span data-stu-id="f91c1-377">443</span></span> | <span data-ttu-id="f91c1-378">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="f91c1-378">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="f91c1-379">Sud du Royaume-Uni</span><span class="sxs-lookup"><span data-stu-id="f91c1-379">UK South</span></span> | <span data-ttu-id="f91c1-380">51.140.47.39</span><span class="sxs-lookup"><span data-stu-id="f91c1-380">51.140.47.39</span></span></br><span data-ttu-id="f91c1-381">51.140.52.16</span><span class="sxs-lookup"><span data-stu-id="f91c1-381">51.140.52.16</span></span> | <span data-ttu-id="f91c1-382">443</span><span class="sxs-lookup"><span data-stu-id="f91c1-382">443</span></span> | <span data-ttu-id="f91c1-383">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="f91c1-383">Inbound</span></span> |
    | <span data-ttu-id="f91c1-384">États-Unis</span><span class="sxs-lookup"><span data-stu-id="f91c1-384">United States</span></span> | <span data-ttu-id="f91c1-385">Centre des États-Unis</span><span class="sxs-lookup"><span data-stu-id="f91c1-385">Central US</span></span> | <span data-ttu-id="f91c1-386">13.67.223.215</span><span class="sxs-lookup"><span data-stu-id="f91c1-386">13.67.223.215</span></span></br><span data-ttu-id="f91c1-387">40.86.83.253</span><span class="sxs-lookup"><span data-stu-id="f91c1-387">40.86.83.253</span></span> | <span data-ttu-id="f91c1-388">443</span><span class="sxs-lookup"><span data-stu-id="f91c1-388">443</span></span> | <span data-ttu-id="f91c1-389">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="f91c1-389">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="f91c1-390">États-Unis - partie centrale septentrionale</span><span class="sxs-lookup"><span data-stu-id="f91c1-390">North Central US</span></span> | <span data-ttu-id="f91c1-391">157.56.8.38</span><span class="sxs-lookup"><span data-stu-id="f91c1-391">157.56.8.38</span></span></br><span data-ttu-id="f91c1-392">157.55.213.99</span><span class="sxs-lookup"><span data-stu-id="f91c1-392">157.55.213.99</span></span> | <span data-ttu-id="f91c1-393">443</span><span class="sxs-lookup"><span data-stu-id="f91c1-393">443</span></span> | <span data-ttu-id="f91c1-394">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="f91c1-394">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="f91c1-395">Centre-Ouest des États-Unis</span><span class="sxs-lookup"><span data-stu-id="f91c1-395">West Central US</span></span> | <span data-ttu-id="f91c1-396">52.161.23.15</span><span class="sxs-lookup"><span data-stu-id="f91c1-396">52.161.23.15</span></span></br><span data-ttu-id="f91c1-397">52.161.10.167</span><span class="sxs-lookup"><span data-stu-id="f91c1-397">52.161.10.167</span></span> | <span data-ttu-id="f91c1-398">443</span><span class="sxs-lookup"><span data-stu-id="f91c1-398">443</span></span> | <span data-ttu-id="f91c1-399">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="f91c1-399">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="f91c1-400">Ouest des États-Unis 2</span><span class="sxs-lookup"><span data-stu-id="f91c1-400">West US 2</span></span> | <span data-ttu-id="f91c1-401">52.175.211.210</span><span class="sxs-lookup"><span data-stu-id="f91c1-401">52.175.211.210</span></span></br><span data-ttu-id="f91c1-402">52.175.222.222</span><span class="sxs-lookup"><span data-stu-id="f91c1-402">52.175.222.222</span></span> | <span data-ttu-id="f91c1-403">443</span><span class="sxs-lookup"><span data-stu-id="f91c1-403">443</span></span> | <span data-ttu-id="f91c1-404">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="f91c1-404">Inbound</span></span> |

    <span data-ttu-id="f91c1-405">Pour plus d’informations sur les adresses IP à utiliser pour Azure Government, voir le document [Intelligence et analyse Azure Government](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics).</span><span class="sxs-lookup"><span data-stu-id="f91c1-405">For information on the IP addresses to use for Azure Government, see the [Azure Government Intelligence + Analytics](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) document.</span></span>

3. <span data-ttu-id="f91c1-406">Si vous utilisez un serveur DNS personnalisé avec votre réseau virtuel, vous devez également autoriser l’accès à partir de __168.63.129.16__.</span><span class="sxs-lookup"><span data-stu-id="f91c1-406">If you use a custom DNS server with your virtual network, you must also allow access from __168.63.129.16__.</span></span> <span data-ttu-id="f91c1-407">Cette adresse est celle d’un programme de résolution récursive d’Azure.</span><span class="sxs-lookup"><span data-stu-id="f91c1-407">This address is Azure's recursive resolver.</span></span> <span data-ttu-id="f91c1-408">Pour plus d’informations, voir le document [Résolution de noms pour les machines virtuelles et les instances de rôle](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="f91c1-408">For more information, see the [Name resolution for VMs and Role instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) document.</span></span>

<span data-ttu-id="f91c1-409">Pour plus d’informations, voir la section [Contrôler le trafic réseau](#networktraffic).</span><span class="sxs-lookup"><span data-stu-id="f91c1-409">For more information, see the [Controlling network traffic](#networktraffic) section.</span></span>

## <span data-ttu-id="f91c1-410"><a id="hdinsight-ports"></a> Ports requis</span><span class="sxs-lookup"><span data-stu-id="f91c1-410"><a id="hdinsight-ports"></a> Required ports</span></span>

<span data-ttu-id="f91c1-411">Si vous prévoyez d’utiliser un **pare-feu d’appliance virtuelle** réseau pour sécuriser le réseau virtuel, vous devez autoriser le trafic sortant sur les ports suivants :</span><span class="sxs-lookup"><span data-stu-id="f91c1-411">If you plan on using a network **virtual appliance firewall** to secure the virtual network, you must allow outbound traffic on the following ports:</span></span>

* <span data-ttu-id="f91c1-412">53</span><span class="sxs-lookup"><span data-stu-id="f91c1-412">53</span></span>
* <span data-ttu-id="f91c1-413">443</span><span class="sxs-lookup"><span data-stu-id="f91c1-413">443</span></span>
* <span data-ttu-id="f91c1-414">1433</span><span class="sxs-lookup"><span data-stu-id="f91c1-414">1433</span></span>
* <span data-ttu-id="f91c1-415">11000-11999</span><span class="sxs-lookup"><span data-stu-id="f91c1-415">11000-11999</span></span>
* <span data-ttu-id="f91c1-416">14000-14999</span><span class="sxs-lookup"><span data-stu-id="f91c1-416">14000-14999</span></span>

<span data-ttu-id="f91c1-417">Pour obtenir la liste des ports utilisés pour des services spécifiques, voir le document [Ports utilisés par les services Hadoop sur HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="f91c1-417">For a list of ports for specific services, see the [Ports used by Hadoop services on HDInsight](hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

<span data-ttu-id="f91c1-418">Pour plus d’informations sur les règles de pare-feu pour les appliances virtuelles, voir le document [Scénario d’appliance virtuelle](../virtual-network/virtual-network-scenario-udr-gw-nva.md).</span><span class="sxs-lookup"><span data-stu-id="f91c1-418">For more information on firewall rules for virtual appliances, see the [virtual appliance scenario](../virtual-network/virtual-network-scenario-udr-gw-nva.md) document.</span></span>

## <span data-ttu-id="f91c1-419"><a id="hdinsight-nsg"></a>Exemple : groupes de sécurité réseau avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="f91c1-419"><a id="hdinsight-nsg"></a>Example: network security groups with HDInsight</span></span>

<span data-ttu-id="f91c1-420">Les exemples de cette section montrent comment créer des règles de groupe de sécurité réseau qui permettent à HDInsight de communiquer avec les services de gestion Azure.</span><span class="sxs-lookup"><span data-stu-id="f91c1-420">The examples in this section demonstrate how to create network security group rules that allow HDInsight to communicate with the Azure management services.</span></span> <span data-ttu-id="f91c1-421">Avant d’utiliser les exemples, ajustez les adresses IP pour qu’elles correspondent à celles de la région Azure que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="f91c1-421">Before using the examples, adjust the IP addresses to match the ones for the Azure region you are using.</span></span> <span data-ttu-id="f91c1-422">Pour trouver ces informations, voir la section [HDInsight avec des groupes de sécurité réseau et des itinéraires définis par l’utilisateur](#hdinsight-ip).</span><span class="sxs-lookup"><span data-stu-id="f91c1-422">You can find this information in the [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

### <a name="azure-resource-management-template"></a><span data-ttu-id="f91c1-423">Modèle de gestion des ressources Azure</span><span class="sxs-lookup"><span data-stu-id="f91c1-423">Azure Resource Management template</span></span>

<span data-ttu-id="f91c1-424">Le modèle de gestion des ressources suivant crée un réseau virtuel qui restreint le trafic entrant, mais autorise le trafic en provenance des adresses IP requises par HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f91c1-424">The following Resource Management template creates a virtual network that restricts inbound traffic, but allows traffic from the IP addresses required by HDInsight.</span></span> <span data-ttu-id="f91c1-425">Ce modèle crée également un cluster HDInsight dans le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f91c1-425">This template also creates an HDInsight cluster in the virtual network.</span></span>

* [<span data-ttu-id="f91c1-426">Déployer un réseau virtuel Azure sécurisé et un cluster Hadoop HDInsight</span><span class="sxs-lookup"><span data-stu-id="f91c1-426">Deploy a secured Azure Virtual Network and an HDInsight Hadoop cluster</span></span>](https://azure.microsoft.com/resources/templates/101-hdinsight-secure-vnet/)

> [!IMPORTANT]
> <span data-ttu-id="f91c1-427">Modifiez les adresses IP utilisées dans cet exemple pour les faire correspondre à la région Azure que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="f91c1-427">Change the IP addresses used in this example to match the Azure region you are using.</span></span> <span data-ttu-id="f91c1-428">Pour trouver ces informations, voir la section [HDInsight avec des groupes de sécurité réseau et des itinéraires définis par l’utilisateur](#hdinsight-ip).</span><span class="sxs-lookup"><span data-stu-id="f91c1-428">You can find this information in the [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="f91c1-429">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f91c1-429">Azure PowerShell</span></span>

<span data-ttu-id="f91c1-430">Utilisez le script PowerShell suivant pour créer un réseau virtuel qui restreint le trafic entrant et autorise le trafic en provenance des adresses IP de la région Europe du Nord.</span><span class="sxs-lookup"><span data-stu-id="f91c1-430">Use the following PowerShell script to create a virtual network that restricts inbound traffic and allows traffic from the IP addresses for the North Europe region.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f91c1-431">Modifiez les adresses IP utilisées dans cet exemple pour les faire correspondre à la région Azure que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="f91c1-431">Change the IP addresses used in this example to match the Azure region you are using.</span></span> <span data-ttu-id="f91c1-432">Pour trouver ces informations, voir la section [HDInsight avec des groupes de sécurité réseau et des itinéraires définis par l’utilisateur](#hdinsight-ip).</span><span class="sxs-lookup"><span data-stu-id="f91c1-432">You can find this information in the [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

```powershell
$vnetName = "Replace with your virtual network name"
$resourceGroupName = "Replace with the resource group the virtual network is in"
$subnetName = "Replace with the name of the subnet that you plan to use for HDInsight"
# Get the Virtual Network object
$vnet = Get-AzureRmVirtualNetwork `
    -Name $vnetName `
    -ResourceGroupName $resourceGroupName
# Get the region the Virtual network is in.
$location = $vnet.Location
# Get the subnet object
$subnet = $vnet.Subnets | Where-Object Name -eq $subnetName
# Create a Network Security Group.
# And add exemptions for the HDInsight health and management services.
$nsg = New-AzureRmNetworkSecurityGroup `
    -Name "hdisecure" `
    -ResourceGroupName $resourceGroupName `
    -Location $location `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -name "hdirule1" `
        -Description "HDI health and management address 52.164.210.96" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "52.164.210.96" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 300 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 13.74.153.132" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "13.74.153.132" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 301 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 168.61.49.99" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.49.99" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 302 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 23.99.5.239" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "23.99.5.239" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 303 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 168.61.48.131" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.48.131" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 304 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 138.91.141.162" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "138.91.141.162" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 305 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "blockeverything" `
        -Description "Block everything else" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "*" `
        -SourceAddressPrefix "Internet" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Deny `
        -Priority 500 `
        -Direction Inbound
# Set the changes to the security group
Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
# Apply the NSG to the subnet
Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name $subnetName `
    -AddressPrefix $subnet.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

> [!IMPORTANT]
> <span data-ttu-id="f91c1-433">Cet exemple montre comment ajouter des règles pour autoriser le trafic entrant sur les adresses IP requises.</span><span class="sxs-lookup"><span data-stu-id="f91c1-433">This example demonstrates how to add rules to allow inbound traffic on the required IP addresses.</span></span> <span data-ttu-id="f91c1-434">Il ne contient pas de règle pour restreindre l’accès entrant à partir d’autres sources.</span><span class="sxs-lookup"><span data-stu-id="f91c1-434">It does not contain a rule to restrict inbound access from other sources.</span></span>
>
> <span data-ttu-id="f91c1-435">L’exemple suivant montre comment activer l’accès SSH depuis Internet :</span><span class="sxs-lookup"><span data-stu-id="f91c1-435">The following example demonstrates how to enable SSH access from the Internet:</span></span>
>
> ```powershell
> Add-AzureRmNetworkSecurityRuleConfig -Name "SSH" -Description "SSH" -Protocol "*" -SourcePortRange "*" -DestinationPortRange "22" -SourceAddressPrefix "*" -DestinationAddressPrefix "VirtualNetwork" -Access Allow -Priority 306 -Direction Inbound
> ```

### <a name="azure-cli"></a><span data-ttu-id="f91c1-436">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="f91c1-436">Azure CLI</span></span>

<span data-ttu-id="f91c1-437">Suivez les étapes suivantes pour créer un réseau virtuel qui restreint le trafic entrant, mais autorise le trafic en provenance des adresses IP requises par HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f91c1-437">Use the following steps to create a virtual network that restricts inbound traffic, but allows traffic from the IP addresses required by HDInsight.</span></span>

1. <span data-ttu-id="f91c1-438">Utilisez la commande suivante pour créer un groupe de sécurité réseau nommé `hdisecure`.</span><span class="sxs-lookup"><span data-stu-id="f91c1-438">Use the following command to create a new network security group named `hdisecure`.</span></span> <span data-ttu-id="f91c1-439">Remplacez **RESOURCEGROUPNAME** par le groupe de ressources qui contient le réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="f91c1-439">Replace **RESOURCEGROUPNAME** with the resource group that contains the Azure Virtual Network.</span></span> <span data-ttu-id="f91c1-440">Remplacez **LOCATION** par l’emplacement (région) où le groupe a été créé.</span><span class="sxs-lookup"><span data-stu-id="f91c1-440">Replace **LOCATION** with the location (region) that the group was created in.</span></span>

    ```azurecli
    az network nsg create -g RESOURCEGROUPNAME -n hdisecure -l LOCATION
    ```

    <span data-ttu-id="f91c1-441">Une fois que le groupe est créé, vous recevez des informations sur le nouveau groupe.</span><span class="sxs-lookup"><span data-stu-id="f91c1-441">Once the group has been created, you receive information on the new group.</span></span>

2. <span data-ttu-id="f91c1-442">Utilisez ce qui suit pour ajouter des règles au nouveau groupe de sécurité réseau qui autorisent les communications entrantes sur le port 443 à partir du service de gestion et de contrôle d’intégrité Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f91c1-442">Use the following to add rules to the new network security group that allow inbound communication on port 443 from the Azure HDInsight health and management service.</span></span> <span data-ttu-id="f91c1-443">Remplacez la valeur **RESOURCEGROUPNAME** par le nom du groupe de ressources qui contient le réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="f91c1-443">Replace **RESOURCEGROUPNAME** with the name of the resource group that contains the Azure Virtual Network.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="f91c1-444">Modifiez les adresses IP utilisées dans cet exemple pour les faire correspondre à la région Azure que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="f91c1-444">Change the IP addresses used in this example to match the Azure region you are using.</span></span> <span data-ttu-id="f91c1-445">Pour trouver ces informations, voir la section [HDInsight avec des groupes de sécurité réseau et des itinéraires définis par l’utilisateur](#hdinsight-ip).</span><span class="sxs-lookup"><span data-stu-id="f91c1-445">You can find this information in the [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

    ```azurecli
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule1 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "52.164.210.96" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 300 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "13.74.153.132" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 301 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.49.99" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 302 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "23.99.5.239" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 303 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.48.131" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 304 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "138.91.141.162" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 305 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n block --protocol "*" --source-port-range "*" --destination-port-range "*" --source-address-prefix "Internet" --destination-address-prefix "VirtualNetwork" --access "Deny" --priority 500 --direction "Inbound"
    ```

3. <span data-ttu-id="f91c1-446">Pour récupérer l’identificateur unique pour ce groupe de sécurité réseau, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f91c1-446">To retrieve the unique identifier for this network security group, use the following command:</span></span>

    ```azurecli
    az network nsg show -g RESOURCEGROUPNAME -n hdisecure --query 'id'
    ```

    <span data-ttu-id="f91c1-447">Cette commande retourne une valeur semblable au texte suivant :</span><span class="sxs-lookup"><span data-stu-id="f91c1-447">This command returns a value similar to the following text:</span></span>

        "/subscriptions/SUBSCRIPTIONID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"

    <span data-ttu-id="f91c1-448">Utilisez des guillemets autour des ID dans la commande si vous n’obtenez pas les résultats attendus.</span><span class="sxs-lookup"><span data-stu-id="f91c1-448">Use double-quotes around id in the command if you don't get the expected results.</span></span>

4. <span data-ttu-id="f91c1-449">Pour appliquer un groupe de sécurité réseau à un sous-réseau, utilisez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="f91c1-449">Use the following command to apply the network security group to a subnet.</span></span> <span data-ttu-id="f91c1-450">Remplacez les valeurs __GUID__ et __RESOURCEGROUPNAME__ par celles renvoyées à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="f91c1-450">Replace the __GUID__ and __RESOURCEGROUPNAME__ values with the ones returned from the previous step.</span></span> <span data-ttu-id="f91c1-451">Remplacez __VNETNAME__ et __SUBNETNAME__ par le nom de réseau virtuel et le nom de sous-réseau que vous souhaitez créer.</span><span class="sxs-lookup"><span data-stu-id="f91c1-451">Replace __VNETNAME__ and __SUBNETNAME__ with the virtual network name and subnet name that you want to create.</span></span>

    ```azurecli
    az network vnet subnet update -g RESOURCEGROUPNAME --vnet-name VNETNAME --name SUBNETNAME --set networkSecurityGroup.id="/subscriptions/GUID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"
    ```

    <span data-ttu-id="f91c1-452">Une fois l’exécution de cette commande terminée, vous pouvez installer HDInsight dans le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f91c1-452">Once this command completes, you can install HDInsight into the Virtual Network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f91c1-453">Ces étapes donnent uniquement accès au service de gestion et de contrôle d’intégrité de HDInsight sur le cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="f91c1-453">These steps only open access to the HDInsight health and management service on the Azure cloud.</span></span> <span data-ttu-id="f91c1-454">Tout autre accès au cluster HDInsight à partir de l’extérieur du réseau virtuel est bloqué.</span><span class="sxs-lookup"><span data-stu-id="f91c1-454">Any other access to the HDInsight cluster from outside the Virtual Network is blocked.</span></span> <span data-ttu-id="f91c1-455">Pour activer l’accès depuis l’extérieur du réseau virtuel, vous devez ajouter des règles supplémentaires pour le groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="f91c1-455">To enable access from outside the virtual network, you must add additional Network Security Group rules.</span></span>
>
> <span data-ttu-id="f91c1-456">L’exemple suivant montre comment activer l’accès SSH depuis Internet :</span><span class="sxs-lookup"><span data-stu-id="f91c1-456">The following example demonstrates how to enable SSH access from the Internet:</span></span>
>
> ```azurecli
> az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule5 --protocol "*" --source-port-range "*" --destination-port-range "22" --source-address-prefix "*" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 306 --direction "Inbound"
> ```

## <span data-ttu-id="f91c1-457"><a id="example-dns"></a> Exemple : configuration de DNS</span><span class="sxs-lookup"><span data-stu-id="f91c1-457"><a id="example-dns"></a> Example: DNS configuration</span></span>

### <a name="name-resolution-between-a-virtual-network-and-a-connected-on-premises-network"></a><span data-ttu-id="f91c1-458">Résolution de noms entre un réseau virtuel et un réseau local connecté</span><span class="sxs-lookup"><span data-stu-id="f91c1-458">Name resolution between a virtual network and a connected on-premises network</span></span>

<span data-ttu-id="f91c1-459">Cet exemple repose sur les hypothèses suivantes :</span><span class="sxs-lookup"><span data-stu-id="f91c1-459">This example makes the following assumptions:</span></span>

* <span data-ttu-id="f91c1-460">Vous avez un réseau virtuel Azure qui est connecté à un réseau local à l’aide d’une passerelle VPN.</span><span class="sxs-lookup"><span data-stu-id="f91c1-460">You have an Azure Virtual Network that is connected to an on-premises network using a VPN gateway.</span></span>

* <span data-ttu-id="f91c1-461">Le serveur DNS personnalisé dans le réseau virtuel exécute le système d’exploitation Linux ou Unix.</span><span class="sxs-lookup"><span data-stu-id="f91c1-461">The custom DNS server in the virtual network is running Linux or Unix as the operating system.</span></span>

* <span data-ttu-id="f91c1-462">[Bind](https://www.isc.org/downloads/bind/) est installé sur le serveur DNS personnalisé.</span><span class="sxs-lookup"><span data-stu-id="f91c1-462">[Bind](https://www.isc.org/downloads/bind/) is installed on the custom DNS server.</span></span>

<span data-ttu-id="f91c1-463">Sur le serveur DNS personnalisé dans le réseau virtuel :</span><span class="sxs-lookup"><span data-stu-id="f91c1-463">On the custom DNS server in the virtual network:</span></span>

1. <span data-ttu-id="f91c1-464">Utilisez Azure PowerShell ou Azure CLI pour rechercher le suffixe DNS du réseau virtuel :</span><span class="sxs-lookup"><span data-stu-id="f91c1-464">Use either Azure PowerShell or Azure CLI to find the DNS suffix of the virtual network:</span></span>

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter the resource group that contains the virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter the name of the resource group that contains the virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. <span data-ttu-id="f91c1-465">Sur le serveur DNS personnalisé pour le réseau virtuel, utilisez le texte suivant en tant que contenu du fichier `/etc/bind/named.conf.local` :</span><span class="sxs-lookup"><span data-stu-id="f91c1-465">On the custom DNS server for the virtual network, use the following text as the contents of the `/etc/bind/named.conf.local` file:</span></span>

    ```
    // Forward requests for the virtual network suffix to Azure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {168.63.129.16;}; # Azure recursive resolver
    };
    ```

    <span data-ttu-id="f91c1-466">Remplacez la valeur `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` par le suffixe DNS de votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f91c1-466">Replace the `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` value with the DNS suffix of your virtual network.</span></span>

    <span data-ttu-id="f91c1-467">Cette configuration a pour effet de router toutes les demandes DNS pour le suffixe DNS du réseau virtuel vers le programme de résolution récursive d’Azure.</span><span class="sxs-lookup"><span data-stu-id="f91c1-467">This configuration routes all DNS requests for the DNS suffix of the virtual network to the Azure recursive resolver.</span></span>

2. <span data-ttu-id="f91c1-468">Sur le serveur DNS personnalisé pour le réseau virtuel, utilisez le texte suivant en tant que contenu du fichier `/etc/bind/named.conf.options` :</span><span class="sxs-lookup"><span data-stu-id="f91c1-468">On the custom DNS server for the virtual network, use the following text as the contents of the `/etc/bind/named.conf.options` file:</span></span>

    ```
    // Clients to accept requests from
    // TODO: Add the IP range of the joined network to this list
    acl goodclients {
        10.0.0.0/16; # IP address range of the virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            # All other requests are sent to the following
            forwarders {
                192.168.0.1; # Replace with the IP address of your on-premises DNS server
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform to RFC1035
            listen-on { any; };
    };
    ```
    
    * <span data-ttu-id="f91c1-469">Remplacez la valeur `10.0.0.0/16` par la plage d'adresses IP de votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f91c1-469">Replace the `10.0.0.0/16` value with the IP address range of your virtual network.</span></span> <span data-ttu-id="f91c1-470">Cette entrée permet que la résolution de noms demande des adresses à l’intérieur de cette plage.</span><span class="sxs-lookup"><span data-stu-id="f91c1-470">This entry allows name resolution requests addresses within this range.</span></span>

    * <span data-ttu-id="f91c1-471">Ajoutez la plage d’adresses IP du réseau local à la section `acl goodclients { ... }`.</span><span class="sxs-lookup"><span data-stu-id="f91c1-471">Add the IP address range of the on-premises network to the `acl goodclients { ... }` section.</span></span>  <span data-ttu-id="f91c1-472">L’entrée autorise les demandes de résolution de noms en provenance de ressources dans le réseau local.</span><span class="sxs-lookup"><span data-stu-id="f91c1-472">entry allows name resolution requests from resources in the on-premises network.</span></span>
    
    * <span data-ttu-id="f91c1-473">Remplacez la valeur `192.168.0.1` par l’adresse IP de votre serveur DNS local.</span><span class="sxs-lookup"><span data-stu-id="f91c1-473">Replace the value `192.168.0.1` with the IP address of your on-premises DNS server.</span></span> <span data-ttu-id="f91c1-474">Cette entrée a pour effet de router toutes les autres demandes DNS vers le serveur DNS local.</span><span class="sxs-lookup"><span data-stu-id="f91c1-474">This entry routes all other DNS requests to the on-premises DNS server.</span></span>

3. <span data-ttu-id="f91c1-475">Pour utiliser la configuration, redémarrez Bind.</span><span class="sxs-lookup"><span data-stu-id="f91c1-475">To use the configuration, restart Bind.</span></span> <span data-ttu-id="f91c1-476">Par exemple, `sudo service bind9 restart`.</span><span class="sxs-lookup"><span data-stu-id="f91c1-476">For example, `sudo service bind9 restart`.</span></span>

4. <span data-ttu-id="f91c1-477">Ajouter un redirecteur conditionnel au serveur DNS local.</span><span class="sxs-lookup"><span data-stu-id="f91c1-477">Add a conditional forwarder to the on-premises DNS server.</span></span> <span data-ttu-id="f91c1-478">Configurez le redirecteur conditionnel de façon envoyer des demandes du suffixe DNS de l’étape 1 au serveur DNS personnalisé.</span><span class="sxs-lookup"><span data-stu-id="f91c1-478">Configure the conditional forwarder to send requests for the DNS suffix from step 1 to the custom DNS server.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f91c1-479">Pour plus de détails sur l’ajout d’un redirecteur conditionnel, consultez la documentation de votre logiciel DNS.</span><span class="sxs-lookup"><span data-stu-id="f91c1-479">Consult the documentation for your DNS software for specifics on how to add a conditional forwarder.</span></span>

<span data-ttu-id="f91c1-480">Après avoir suivi ces étapes, vous pouvez vous connecter aux ressources de chaque réseau à l’aide de noms de domaine complets (FQDN).</span><span class="sxs-lookup"><span data-stu-id="f91c1-480">After completing these steps, you can connect to resources in either network using fully qualified domain names (FQDN).</span></span> <span data-ttu-id="f91c1-481">Vous pouvez à présent installer HDInsight dans le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f91c1-481">You can now install HDInsight into the virtual network.</span></span>

### <a name="name-resolution-between-two-connected-virtual-networks"></a><span data-ttu-id="f91c1-482">Résolution de noms entre deux réseaux virtuels connectés</span><span class="sxs-lookup"><span data-stu-id="f91c1-482">Name resolution between two connected virtual networks</span></span>

<span data-ttu-id="f91c1-483">Cet exemple repose sur les hypothèses suivantes :</span><span class="sxs-lookup"><span data-stu-id="f91c1-483">This example makes the following assumptions:</span></span>

* <span data-ttu-id="f91c1-484">Vous avez deux réseaux virtuels Azure connectés à l’aide d’une passerelle VPN ou d’une homologation.</span><span class="sxs-lookup"><span data-stu-id="f91c1-484">You have two Azure Virtual Networks that are connected using either a VPN gateway or peering.</span></span>

* <span data-ttu-id="f91c1-485">Le serveur DNS personnalisé dans les deux réseaux exécute le système d’exploitation Linux ou Unix.</span><span class="sxs-lookup"><span data-stu-id="f91c1-485">The custom DNS server in both networks is running Linux or Unix as the operating system.</span></span>

* <span data-ttu-id="f91c1-486">[Bind](https://www.isc.org/downloads/bind/) est installé sur les serveurs DNS personnalisés.</span><span class="sxs-lookup"><span data-stu-id="f91c1-486">[Bind](https://www.isc.org/downloads/bind/) is installed on the custom DNS servers.</span></span>

1. <span data-ttu-id="f91c1-487">Utilisez Azure PowerShell ou Azure CLI pour rechercher le suffixe DNS des deux réseaux virtuels :</span><span class="sxs-lookup"><span data-stu-id="f91c1-487">Use either Azure PowerShell or Azure CLI to find the DNS suffix of both virtual networks:</span></span>

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter the resource group that contains the virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter the name of the resource group that contains the virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. <span data-ttu-id="f91c1-488">Sur le serveur DNS personnalisé, utilisez le texte suivant en tant que contenu du fichier `/etc/bind/named.config.local`.</span><span class="sxs-lookup"><span data-stu-id="f91c1-488">Use the following text as the contents of the `/etc/bind/named.config.local` file on the custom DNS server.</span></span> <span data-ttu-id="f91c1-489">Apportez cette modification sur le serveur DNS personnalisé dans les deux réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="f91c1-489">Make this change on the custom DNS server in both virtual networks.</span></span>

    ```
    // Forward requests for the virtual network suffix to Azure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # The IP address of the DNS server in the other virtual network
    };
    ```

    <span data-ttu-id="f91c1-490">Remplacez la valeur `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` par le suffixe DNS de l’__autre__ réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f91c1-490">Replace the `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` value with the DNS suffix of the __other__ virtual network.</span></span> <span data-ttu-id="f91c1-491">Cette entrée a pour effet de router les demandes du suffixe DNS du réseau distant vers le DNS personnalisé dans ce réseau.</span><span class="sxs-lookup"><span data-stu-id="f91c1-491">This entry routes requests for the DNS suffix of the remote network to the custom DNS in that network.</span></span>

3. <span data-ttu-id="f91c1-492">Sur les serveurs DNS personnalisés dans les deux réseaux virtuels, utilisez le texte suivant en tant que contenu du fichier `/etc/bind/named.conf.options`:</span><span class="sxs-lookup"><span data-stu-id="f91c1-492">On the custom DNS servers in both virtual networks, use the following text as the contents of the `/etc/bind/named.conf.options` file:</span></span>

    ```
    // Clients to accept requests from
    acl goodclients {
        10.1.0.0/16; # The IP address range of one virtual network
        10.0.0.0/16; # The IP address range of the other virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            forwarders {
            168.63.129.16;   # Azure recursive resolver         
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform to RFC1035
            listen-on { any; };
    };
    ```
    
    * <span data-ttu-id="f91c1-493">Remplacez les valeurs `10.0.0.0/16` et `10.1.0.0/16` par les plages d’adresses IP de vos réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="f91c1-493">Replace the `10.0.0.0/16` and `10.1.0.0/16` values with the IP address ranges of your virtual networks.</span></span> <span data-ttu-id="f91c1-494">Cette entrée a pour effet de permettre aux ressources de chaque réseau d’effectuer des demandes des serveurs DNS.</span><span class="sxs-lookup"><span data-stu-id="f91c1-494">This entry allows resources in each network to make requests of the DNS servers.</span></span>

    <span data-ttu-id="f91c1-495">Toute demande n’ayant pas trait au suffixes DNS des réseaux virtuels (par exemple, microsoft.com) est gérée par le programme de résolution récursive d’Azure.</span><span class="sxs-lookup"><span data-stu-id="f91c1-495">Any requests that are not for the DNS suffixes of the virtual networks (for example, microsoft.com) is handled by the Azure recursive resolver.</span></span>

4. <span data-ttu-id="f91c1-496">Pour utiliser la configuration, redémarrez Bind.</span><span class="sxs-lookup"><span data-stu-id="f91c1-496">To use the configuration, restart Bind.</span></span> <span data-ttu-id="f91c1-497">Par exemple, `sudo service bind9 restart` sur les deux serveurs DNS.</span><span class="sxs-lookup"><span data-stu-id="f91c1-497">For example, `sudo service bind9 restart` on both DNS servers.</span></span>

<span data-ttu-id="f91c1-498">Après avoir suivi ces étapes, vous pouvez vous connecter aux ressources du réseau virtuel à l’aide de noms de domaine complets (FQDN).</span><span class="sxs-lookup"><span data-stu-id="f91c1-498">After completing these steps, you can connect to resources in the virtual network using fully qualified domain names (FQDN).</span></span> <span data-ttu-id="f91c1-499">Vous pouvez à présent installer HDInsight dans le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f91c1-499">You can now install HDInsight into the virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f91c1-500">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f91c1-500">Next steps</span></span>

* <span data-ttu-id="f91c1-501">Pour un exemple de bout en bout de configuration de HDInsight pour se connecter à un réseau local, voir [Connecter HDInsight à un réseau local](./connect-on-premises-network.md).</span><span class="sxs-lookup"><span data-stu-id="f91c1-501">For an end-to-end example of configuring HDInsight to connect to an on-premises network, see [Connect HDInsight to an on-premises network](./connect-on-premises-network.md).</span></span>

* <span data-ttu-id="f91c1-502">Pour plus d’informations sur les réseaux virtuels Azure, voir [Vue d'ensemble de Réseau virtuel Azure](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f91c1-502">For more information on Azure virtual networks, see the [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span></span>

* <span data-ttu-id="f91c1-503">Pour plus d’informations sur les groupes de sécurité réseau, consultez [Groupes de sécurité réseau](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="f91c1-503">For more information on network security groups, see [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="f91c1-504">Pour plus d’informations sur les routages par l’utilisateur, consultez [Routage définis par l’utilisateur et transfert IP](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f91c1-504">For more information on user-defined routes, see [USer-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>