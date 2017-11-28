---
title: aaaExtend HDInsight avec Virtual Network - Azure | Documents Microsoft
description: "Découvrez comment toouse réseau virtuel Azure tooconnect HDInsight tooother cloud ressources ou des ressources dans votre centre de données"
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
ms.openlocfilehash: ba80be4d9f280c6c62fa8acc996ef5f921acdbbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="extend-azure-hdinsight-using-an-azure-virtual-network"></a><span data-ttu-id="8ed45-103">Étendre HDInsight à l’aide d’un réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="8ed45-103">Extend Azure HDInsight using an Azure Virtual Network</span></span>

<span data-ttu-id="8ed45-104">Découvrez comment toouse HDInsight avec un [réseau virtuel Azure](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8ed45-104">Learn how toouse HDInsight with an [Azure Virtual Network](../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="8ed45-105">À l’aide d’un réseau virtuel Azure permet de hello les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="8ed45-105">Using an Azure Virtual Network enables hello following scenarios:</span></span>

* <span data-ttu-id="8ed45-106">Connexion tooHDInsight directement à partir d’un réseau local.</span><span class="sxs-lookup"><span data-stu-id="8ed45-106">Connecting tooHDInsight directly from an on-premises network.</span></span>

* <span data-ttu-id="8ed45-107">Connexion HDInsight toodata stocke dans un réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="8ed45-107">Connecting HDInsight toodata stores in an Azure Virtual network.</span></span>

* <span data-ttu-id="8ed45-108">Directement l’accès aux services Hadoop qui ne sont pas disponibles publiquement sur hello internet.</span><span class="sxs-lookup"><span data-stu-id="8ed45-108">Directly accessing Hadoop services that are not available publicly over hello internet.</span></span> <span data-ttu-id="8ed45-109">Par exemple, les API Kafka ou hello HBase Java API.</span><span class="sxs-lookup"><span data-stu-id="8ed45-109">For example, Kafka APIs or hello HBase Java API.</span></span>

> [!WARNING]
> <span data-ttu-id="8ed45-110">informations Hello dans ce document nécessitent une compréhension de la mise en réseau TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="8ed45-110">hello information in this document requires an understanding of TCP/IP networking.</span></span> <span data-ttu-id="8ed45-111">Si vous n’êtes pas familiarisé avec la mise en réseau TCP/IP, vous devez en partenariat avec personne avant d’apporter des modifications tooproduction réseaux.</span><span class="sxs-lookup"><span data-stu-id="8ed45-111">If you are not familiar with TCP/IP networking, you should partner with someone who is before making modifications tooproduction networks.</span></span>

## <a name="planning"></a><span data-ttu-id="8ed45-112">Planification</span><span class="sxs-lookup"><span data-stu-id="8ed45-112">Planning</span></span>

<span data-ttu-id="8ed45-113">Hello Voici les questions de hello auxquelles vous devez répondre lors de la planification tooinstall HDInsight dans un réseau virtuel :</span><span class="sxs-lookup"><span data-stu-id="8ed45-113">hello following are hello questions that you must answer when planning tooinstall HDInsight in a virtual network:</span></span>

* <span data-ttu-id="8ed45-114">Avez-vous besoin de tooinstall HDInsight dans un réseau virtuel existant ?</span><span class="sxs-lookup"><span data-stu-id="8ed45-114">Do you need tooinstall HDInsight into an existing virtual network?</span></span> <span data-ttu-id="8ed45-115">Ou bien créez-vous un réseau ?</span><span class="sxs-lookup"><span data-stu-id="8ed45-115">Or are you creating a new network?</span></span>

    <span data-ttu-id="8ed45-116">Si vous utilisez un réseau virtuel existant, vous devrez peut-être la configuration du réseau toomodify hello avant que vous puissiez installer HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8ed45-116">If you are using an existing virtual network, you may need toomodify hello network configuration before you can install HDInsight.</span></span> <span data-ttu-id="8ed45-117">Pour plus d’informations, consultez hello [ajouter le réseau virtuel tooan HDInsight](#existingvnet) section.</span><span class="sxs-lookup"><span data-stu-id="8ed45-117">For more information, see hello [add HDInsight tooan existing virtual network](#existingvnet) section.</span></span>

* <span data-ttu-id="8ed45-118">Voulez-vous contenant le réseau virtuel de HDInsight tooanother du réseau virtuel hello tooconnect ou votre réseau local ?</span><span class="sxs-lookup"><span data-stu-id="8ed45-118">Do you want tooconnect hello virtual network containing HDInsight tooanother virtual network or your on-premises network?</span></span>

    <span data-ttu-id="8ed45-119">tooeasily travail avec des ressources sur des réseaux, vous pouvez peut-être toocreate DNS personnalisé et configurer la redirection DNS.</span><span class="sxs-lookup"><span data-stu-id="8ed45-119">tooeasily work with resources across networks, you may need toocreate a custom DNS and configure DNS forwarding.</span></span> <span data-ttu-id="8ed45-120">Pour plus d’informations, consultez hello [connecter plusieurs réseaux](#multinet) section.</span><span class="sxs-lookup"><span data-stu-id="8ed45-120">For more information, see hello [connecting multiple networks](#multinet) section.</span></span>

* <span data-ttu-id="8ed45-121">Voulez-vous vraiment toorestrict/redirection tooHDInsight de trafic entrant ou sortant ?</span><span class="sxs-lookup"><span data-stu-id="8ed45-121">Do you want toorestrict/redirect inbound or outbound traffic tooHDInsight?</span></span>

    <span data-ttu-id="8ed45-122">HDInsight doit avoir un communication avec des adresses IP spécifiques dans le centre de données Azure hello illimité.</span><span class="sxs-lookup"><span data-stu-id="8ed45-122">HDInsight must have unrestricted communication with specific IP addresses in hello Azure data center.</span></span> <span data-ttu-id="8ed45-123">Il existe également plusieurs ports qui doivent être autorisés au travers de pare-feu pour la communication du client.</span><span class="sxs-lookup"><span data-stu-id="8ed45-123">There are also several ports that must be allowed through firewalls for client communication.</span></span> <span data-ttu-id="8ed45-124">Pour plus d’informations, consultez hello [contrôler le trafic réseau](#networktraffic) section.</span><span class="sxs-lookup"><span data-stu-id="8ed45-124">For more information, see hello [controlling network traffic](#networktraffic) section.</span></span>

## <span data-ttu-id="8ed45-125"><a id="existingvnet"></a>Ajouter le réseau virtuel tooan HDInsight</span><span class="sxs-lookup"><span data-stu-id="8ed45-125"><a id="existingvnet"></a>Add HDInsight tooan existing virtual network</span></span>

<span data-ttu-id="8ed45-126">Utilisez les étapes hello dans toodiscover de cette section Comment tooadd un tooan HDInsight nouveau existant du réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="8ed45-126">Use hello steps in this section toodiscover how tooadd a new HDInsight tooan existing Azure Virtual Network.</span></span>

> [!NOTE]
> <span data-ttu-id="8ed45-127">Vous ne pouvez pas ajouter un cluster HDInsight existant à un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="8ed45-127">You cannot add an existing HDInsight cluster into a virtual network.</span></span>

1. <span data-ttu-id="8ed45-128">Si vous utilisez un classique ou le modèle de déploiement de gestionnaire de ressources pour le réseau virtuel de hello ?</span><span class="sxs-lookup"><span data-stu-id="8ed45-128">Are you using a classic or Resource Manager deployment model for hello virtual network?</span></span>

    <span data-ttu-id="8ed45-129">HDInsight 3.4 et versions ultérieures nécessitent un réseau virtuel Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8ed45-129">HDInsight 3.4 and greater requires a Resource Manager virtual network.</span></span> <span data-ttu-id="8ed45-130">Les versions antérieures de HDInsight nécessitaient un réseau virtuel classique.</span><span class="sxs-lookup"><span data-stu-id="8ed45-130">Earlier versions of HDInsight required a classic virtual network.</span></span>

    <span data-ttu-id="8ed45-131">Si votre réseau existant est un réseau virtuel classique, vous devez créer un réseau virtuel du Gestionnaire de ressources et connectez-vous hello deux.</span><span class="sxs-lookup"><span data-stu-id="8ed45-131">If your existing network is a classic virtual network, then you must create a Resource Manager virtual network and then connect hello two.</span></span> <span data-ttu-id="8ed45-132">[Connexion classique des réseaux virtuels toonew réseaux virtuels](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8ed45-132">[Connecting classic VNets toonew VNets](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).</span></span>

    <span data-ttu-id="8ed45-133">Une fois joint, HDInsight sur hello Gestionnaire de ressources du réseau peut interagir avec les ressources réseau classiques de hello.</span><span class="sxs-lookup"><span data-stu-id="8ed45-133">Once joined, HDInsight installed in hello Resource Manager network can interact with resources in hello classic network.</span></span>

2. <span data-ttu-id="8ed45-134">Voulez-vous utiliser un tunneling forcé ?</span><span class="sxs-lookup"><span data-stu-id="8ed45-134">Do you use forced tunneling?</span></span> <span data-ttu-id="8ed45-135">Le tunneling forcé est un paramètre de sous-réseau qui force le périphérique tooa de trafic Internet sortant pour l’inspection et la journalisation.</span><span class="sxs-lookup"><span data-stu-id="8ed45-135">Forced tunneling is a subnet setting that forces outbound Internet traffic tooa device for inspection and logging.</span></span> <span data-ttu-id="8ed45-136">HDInsight ne prend pas en charge le tunneling forcé.</span><span class="sxs-lookup"><span data-stu-id="8ed45-136">HDInsight does not support forced tunneling.</span></span> <span data-ttu-id="8ed45-137">Supprimez le tunneling forcé avant d’installer HDInsight dans un sous-réseau, ou de créer un sous-réseau pour HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8ed45-137">Either remove forced tunneling before installing HDInsight into a subnet, or create a new subnet for HDInsight.</span></span>

3. <span data-ttu-id="8ed45-138">Utilisez-vous des groupes de sécurité réseau, itinéraires définis par l’utilisateur ou le trafic toorestrict de dispositifs de réseau virtuel dans ou en dehors du réseau virtuel de hello ?</span><span class="sxs-lookup"><span data-stu-id="8ed45-138">Do you use network security groups, user-defined routes, or Virtual Network Appliances toorestrict traffic into or out of hello virtual network?</span></span>

    <span data-ttu-id="8ed45-139">Un service géré, HDInsight requiert un accès illimité tooseveral des adresses IP dans le centre de données Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8ed45-139">As a managed service, HDInsight requires unrestricted access tooseveral IP addresses in hello Azure data center.</span></span> <span data-ttu-id="8ed45-140">communication tooallow avec ces adresses IP, mettre à jour les groupes de sécurité réseau existant ou des itinéraires de défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8ed45-140">tooallow communication with these IP addresses, update any existing network security groups or user-defined routes.</span></span>

    <span data-ttu-id="8ed45-141">HDInsight héberge plusieurs services qui une série de ports.</span><span class="sxs-lookup"><span data-stu-id="8ed45-141">HDInsight  hosts multiple services, which use a variety of ports.</span></span> <span data-ttu-id="8ed45-142">Ne bloquent pas le trafic des ports toothese.</span><span class="sxs-lookup"><span data-stu-id="8ed45-142">Do not block traffic toothese ports.</span></span> <span data-ttu-id="8ed45-143">Pour obtenir la liste de tooallow de ports à travers des pare-feu d’appliance virtuelle, consultez hello [sécurité](#security) section.</span><span class="sxs-lookup"><span data-stu-id="8ed45-143">For a list of ports tooallow through virtual appliance firewalls, see hello [Security](#security) section.</span></span>

    <span data-ttu-id="8ed45-144">toofind votre configuration de sécurité existante, hello utilisation suivant les commandes Azure PowerShell ou CLI d’Azure :</span><span class="sxs-lookup"><span data-stu-id="8ed45-144">toofind your existing security configuration, use hello following Azure PowerShell or Azure CLI commands:</span></span>

    * <span data-ttu-id="8ed45-145">groupes de sécurité réseau ;</span><span class="sxs-lookup"><span data-stu-id="8ed45-145">Network security groups</span></span>

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
        get-azurermnetworksecuritygroup -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
        az network nsg list --resource-group $RESOURCEGROUP
        ```

        <span data-ttu-id="8ed45-146">Pour plus d’informations, consultez hello [résoudre les groupes de sécurité réseau](../virtual-network/virtual-network-nsg-troubleshoot-portal.md) document.</span><span class="sxs-lookup"><span data-stu-id="8ed45-146">For more information, see hello [Troubleshoot network security groups](../virtual-network/virtual-network-nsg-troubleshoot-portal.md) document.</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="8ed45-147">Les règles de groupe de sécurité réseau sont appliquées dans un ordre basé sur leur priorité.</span><span class="sxs-lookup"><span data-stu-id="8ed45-147">Network security group rules are applied in order based on rule priority.</span></span> <span data-ttu-id="8ed45-148">Hello première règle qui correspond au modèle de trafic hello est appliquée, et aucune autre ne sont appliquées à ce trafic.</span><span class="sxs-lookup"><span data-stu-id="8ed45-148">hello first rule that matches hello traffic pattern is applied, and no others are applied for that traffic.</span></span> <span data-ttu-id="8ed45-149">Ordre des règles à partir de tooleast plus permissif permissif.</span><span class="sxs-lookup"><span data-stu-id="8ed45-149">Order rules from most permissive tooleast permissive.</span></span> <span data-ttu-id="8ed45-150">Pour plus d’informations, consultez hello [filtrer le trafic réseau avec les groupes de sécurité réseau](../virtual-network/virtual-networks-nsg.md) document.</span><span class="sxs-lookup"><span data-stu-id="8ed45-150">For more information, see hello [Filter network traffic with network security groups](../virtual-network/virtual-networks-nsg.md) document.</span></span>

    * <span data-ttu-id="8ed45-151">Itinéraires définis par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="8ed45-151">User-defined routes</span></span>

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
        get-azurermroutetable -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
        az network route-table list --resource-group $RESOURCEGROUP
        ```

        <span data-ttu-id="8ed45-152">Pour plus d’informations, consultez hello [résoudre les itinéraires](../virtual-network/virtual-network-routes-troubleshoot-portal.md) document.</span><span class="sxs-lookup"><span data-stu-id="8ed45-152">For more information, see hello [Troubleshoot routes](../virtual-network/virtual-network-routes-troubleshoot-portal.md) document.</span></span>

4. <span data-ttu-id="8ed45-153">Créer un cluster HDInsight et sélectionnez hello réseau virtuel Azure lors de la configuration.</span><span class="sxs-lookup"><span data-stu-id="8ed45-153">Create an HDInsight cluster and select hello Azure Virtual Network during configuration.</span></span> <span data-ttu-id="8ed45-154">Utilisez les étapes de hello Bonjour suivant le processus de création de documents toounderstand hello cluster :</span><span class="sxs-lookup"><span data-stu-id="8ed45-154">Use hello steps in hello following documents toounderstand hello cluster creation process:</span></span>

    * [<span data-ttu-id="8ed45-155">Créer HDInsight à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="8ed45-155">Create HDInsight using hello Azure portal</span></span>](hdinsight-hadoop-create-linux-clusters-portal.md)
    * [<span data-ttu-id="8ed45-156">Créer un cluster HDInsight à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ed45-156">Create HDInsight using Azure PowerShell</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
    * [<span data-ttu-id="8ed45-157">Créer un cluster HDInsight à l’aide de l’interface de ligne de commande Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="8ed45-157">Create HDInsight using Azure CLI 1.0</span></span>](hdinsight-hadoop-create-linux-clusters-azure-cli.md)
    * [<span data-ttu-id="8ed45-158">Créer un cluster HDInsight à l’aide d’un modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8ed45-158">Create HDInsight using an Azure Resource Manager template</span></span>](hdinsight-hadoop-create-linux-clusters-arm-templates.md)

  > [!IMPORTANT]
  > <span data-ttu-id="8ed45-159">Ajout de HDInsight tooa des réseaux virtuels sont une étape de configuration facultatives.</span><span class="sxs-lookup"><span data-stu-id="8ed45-159">Adding HDInsight tooa virtual network is an optional configuration step.</span></span> <span data-ttu-id="8ed45-160">Être sûr de réseau virtuel hello de tooselect lors de la configuration de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="8ed45-160">Be sure tooselect hello virtual network when configuring hello cluster.</span></span>

## <span data-ttu-id="8ed45-161"><a id="multinet"></a>Connexion de plusieurs réseaux</span><span class="sxs-lookup"><span data-stu-id="8ed45-161"><a id="multinet"></a>Connecting multiple networks</span></span>

<span data-ttu-id="8ed45-162">défi le plus important Hello avec une configuration de réseau multiples est la résolution de noms entre des réseaux hello.</span><span class="sxs-lookup"><span data-stu-id="8ed45-162">hello biggest challenge with a multi-network configuration is name resolution between hello networks.</span></span>

<span data-ttu-id="8ed45-163">Azure assure la résolution de noms pour les services Azure installés dans un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="8ed45-163">Azure provides name resolution for Azure services that are installed in a virtual network.</span></span> <span data-ttu-id="8ed45-164">Cette résolution de nom intégré permet toohello de tooconnect HDInsight suivant des ressources à l’aide d’un nom de domaine complet (FQDN) :</span><span class="sxs-lookup"><span data-stu-id="8ed45-164">This built-in name resolution allows HDInsight tooconnect toohello following resources by using a fully qualified domain name (FQDN):</span></span>

* <span data-ttu-id="8ed45-165">Est disponible sur n’importe quelle ressource hello internet.</span><span class="sxs-lookup"><span data-stu-id="8ed45-165">Any resource that is available on hello internet.</span></span> <span data-ttu-id="8ed45-166">Par exemple, microsoft.com ou google.com.</span><span class="sxs-lookup"><span data-stu-id="8ed45-166">For example, microsoft.com, google.com.</span></span>

* <span data-ttu-id="8ed45-167">N’importe quelle ressource est hello dans même réseau virtuel Azure, à l’aide de hello __nom DNS interne__ de ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="8ed45-167">Any resource that is in hello same Azure Virtual Network, by using hello __internal DNS name__ of hello resource.</span></span> <span data-ttu-id="8ed45-168">Par exemple, lorsque vous utilisez la résolution de noms par défaut hello, hello Voici exemple interne DNS noms tooHDInsight attribué de nœuds de travail :</span><span class="sxs-lookup"><span data-stu-id="8ed45-168">For example, when using hello default name resolution, hello following are example internal DNS names assigned tooHDInsight worker nodes:</span></span>

    * <span data-ttu-id="8ed45-169">wn0-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="8ed45-169">wn0-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span></span>
    * <span data-ttu-id="8ed45-170">wn2-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="8ed45-170">wn2-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span></span>

    <span data-ttu-id="8ed45-171">Les deux nœuds peuvent communiquer directement entre eux et avec d’autres nœuds dans HDInsight en utilisant des noms DNS internes.</span><span class="sxs-lookup"><span data-stu-id="8ed45-171">Both these nodes can communicate directly with each other, and other nodes in HDInsight, by using internal DNS names.</span></span>

<span data-ttu-id="8ed45-172">résolution de noms par défaut Hello est __pas__ autoriser HDInsight tooresolve noms hello de ressources dans des réseaux qui sont jointes toohello des réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="8ed45-172">hello default name resolution does __not__ allow HDInsight tooresolve hello names of resources in networks that are joined toohello virtual network.</span></span> <span data-ttu-id="8ed45-173">Par exemple, il est commun toojoin toohello des réseaux virtuels du réseau de votre site.</span><span class="sxs-lookup"><span data-stu-id="8ed45-173">For example, it is common toojoin your on-premises network toohello virtual network.</span></span> <span data-ttu-id="8ed45-174">Uniquement hello par défaut résolution du nom, HDInsight ne peut pas accéder aux ressources réseau local de hello par nom.</span><span class="sxs-lookup"><span data-stu-id="8ed45-174">With only hello default name resolution, HDInsight cannot access resources in hello on-premises network by name.</span></span> <span data-ttu-id="8ed45-175">Hello inverse est également true, les ressources de votre réseau local ne peut pas accéder aux ressources de réseau virtuel de hello par nom.</span><span class="sxs-lookup"><span data-stu-id="8ed45-175">hello opposite is also true, resources in your on-premises network cannot access resources in hello virtual network by name.</span></span>

> [!WARNING]
> <span data-ttu-id="8ed45-176">Vous devez créer un serveur DNS personnalisé hello et configurer toouse de réseau virtuel hello avant la création d’hello cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8ed45-176">You must create hello custom DNS server and configure hello virtual network toouse it before creating hello HDInsight cluster.</span></span>

<span data-ttu-id="8ed45-177">résolution de noms tooenable entre le réseau virtuel de hello et les ressources dans les réseaux jointes, vous devez effectuer hello suivant des actions :</span><span class="sxs-lookup"><span data-stu-id="8ed45-177">tooenable name resolution between hello virtual network and resources in joined networks, you must perform hello following actions:</span></span>

1. <span data-ttu-id="8ed45-178">Créer un serveur DNS personnalisé Bonjour Azure Virtual Network où vous prévoyez de tooinstall HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8ed45-178">Create a custom DNS server in hello Azure Virtual Network where you plan tooinstall HDInsight.</span></span>

2. <span data-ttu-id="8ed45-179">Configurer hello réseau virtuel toouse hello serveur DNS personnalisé.</span><span class="sxs-lookup"><span data-stu-id="8ed45-179">Configure hello virtual network toouse hello custom DNS server.</span></span>

3. <span data-ttu-id="8ed45-180">Recherche hello Qu'azure affecté le suffixe DNS pour votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="8ed45-180">Find hello Azure assigned DNS suffix for your virtual network.</span></span> <span data-ttu-id="8ed45-181">Cette valeur est trop similaire`0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`.</span><span class="sxs-lookup"><span data-stu-id="8ed45-181">This value is similar too`0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`.</span></span> <span data-ttu-id="8ed45-182">Pour plus d’informations sur la recherche de suffixe DNS de hello, consultez hello [exemple : Custom DNS](#example-dns) section.</span><span class="sxs-lookup"><span data-stu-id="8ed45-182">For information on finding hello DNS suffix, see hello [Example: Custom DNS](#example-dns) section.</span></span>

4. <span data-ttu-id="8ed45-183">Configurer le transfert entre les serveurs DNS de hello.</span><span class="sxs-lookup"><span data-stu-id="8ed45-183">Configure forwarding between hello DNS servers.</span></span> <span data-ttu-id="8ed45-184">configuration de Hello dépend du type hello du réseau à distance.</span><span class="sxs-lookup"><span data-stu-id="8ed45-184">hello configuration depends on hello type of remote network.</span></span>

    * <span data-ttu-id="8ed45-185">Si le réseau à distance de hello est un réseau local, configurez DNS comme suit :</span><span class="sxs-lookup"><span data-stu-id="8ed45-185">If hello remote network is an on-premises network, configure DNS as follows:</span></span>
        
        * <span data-ttu-id="8ed45-186">__DNS personnalisé__ (dans le réseau virtuel de hello) :</span><span class="sxs-lookup"><span data-stu-id="8ed45-186">__Custom DNS__ (in hello virtual network):</span></span>

            * <span data-ttu-id="8ed45-187">Transférer les demandes pour le suffixe DNS de hello du programme de résolution de Azure récursive toohello hello réseau virtuel (168.63.129.16).</span><span class="sxs-lookup"><span data-stu-id="8ed45-187">Forward requests for hello DNS suffix of hello virtual network toohello Azure recursive resolver (168.63.129.16).</span></span> <span data-ttu-id="8ed45-188">Azure gère les demandes de ressources de réseau virtuel de hello</span><span class="sxs-lookup"><span data-stu-id="8ed45-188">Azure handles requests for resources in hello virtual network</span></span>

            * <span data-ttu-id="8ed45-189">Transférer toutes les autres demandes toohello locale DNS server.</span><span class="sxs-lookup"><span data-stu-id="8ed45-189">Forward all other requests toohello on-premises DNS server.</span></span> <span data-ttu-id="8ed45-190">Hello locale DNS gère toutes les autres demandes de résolution de nom, y compris les requêtes de ressources internet telles que Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="8ed45-190">hello on-premises DNS handles all other name resolution requests, even requests for internet resources such as Microsoft.com.</span></span>

        * <span data-ttu-id="8ed45-191">__DNS local__: demandes de hello réseau virtuel DNS suffixe toohello un serveur DNS personnalisé.</span><span class="sxs-lookup"><span data-stu-id="8ed45-191">__On-premises DNS__: Forward requests for hello virtual network DNS suffix toohello custom DNS server.</span></span> <span data-ttu-id="8ed45-192">un serveur DNS personnalisé Hello transmet ensuite le programme de résolution toohello récursive Azure.</span><span class="sxs-lookup"><span data-stu-id="8ed45-192">hello custom DNS server then forwards toohello Azure recursive resolver.</span></span>

        <span data-ttu-id="8ed45-193">Demandes de configuration de cette itinéraires pour complet des noms de domaine qui contiennent le suffixe DNS hello hello réseau virtuel toohello un serveur DNS personnalisé.</span><span class="sxs-lookup"><span data-stu-id="8ed45-193">This configuration routes requests for fully qualified domain names that contain hello DNS suffix of hello virtual network toohello custom DNS server.</span></span> <span data-ttu-id="8ed45-194">Toutes les autres demandes (même pour les adresses internet publics) sont gérées par le serveur DNS hello local.</span><span class="sxs-lookup"><span data-stu-id="8ed45-194">All other requests (even for public internet addresses) are handled by hello on-premises DNS server.</span></span>

    * <span data-ttu-id="8ed45-195">Si le réseau à distance de hello est un autre réseau virtuel Azure, configurez DNS comme suit :</span><span class="sxs-lookup"><span data-stu-id="8ed45-195">If hello remote network is another Azure Virtual Network, configure DNS as follows:</span></span>

        * <span data-ttu-id="8ed45-196">__DNS personnalisé__ (dans chaque réseau virtuel) :</span><span class="sxs-lookup"><span data-stu-id="8ed45-196">__Custom DNS__ (in each virtual network):</span></span>

            * <span data-ttu-id="8ed45-197">Demandes pour le suffixe DNS de hello des réseaux virtuels de hello sont transférées toohello des serveurs DNS personnalisés.</span><span class="sxs-lookup"><span data-stu-id="8ed45-197">Requests for hello DNS suffix of hello virtual networks are forwarded toohello custom DNS servers.</span></span> <span data-ttu-id="8ed45-198">Hello DNS de chaque réseau virtuel est chargé de résoudre des ressources au sein de son réseau.</span><span class="sxs-lookup"><span data-stu-id="8ed45-198">hello DNS in each virtual network is responsible for resolving resources within its network.</span></span>

            * <span data-ttu-id="8ed45-199">Transférer toutes les autres demandes toohello récursive Azure programme de résolution.</span><span class="sxs-lookup"><span data-stu-id="8ed45-199">Forward all other requests toohello Azure recursive resolver.</span></span> <span data-ttu-id="8ed45-200">programme de résolution récursive Hello est responsable de la résolution local et les ressources internet.</span><span class="sxs-lookup"><span data-stu-id="8ed45-200">hello recursive resolver is responsible for resolving local and internet resources.</span></span>

        <span data-ttu-id="8ed45-201">serveur DNS de Hello pour chaque réseau transfère les demandes toohello autres, en fonction de suffixe DNS.</span><span class="sxs-lookup"><span data-stu-id="8ed45-201">hello DNS server for each network forwards requests toohello other, based on DNS suffix.</span></span> <span data-ttu-id="8ed45-202">Autres requêtes sont résolues à l’aide du programme de résolution récursive Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8ed45-202">Other requests are resolved using hello Azure recursive resolver.</span></span>

    <span data-ttu-id="8ed45-203">Pour obtenir un exemple de chaque configuration, consultez hello [exemple : Custom DNS](#example-dns) section.</span><span class="sxs-lookup"><span data-stu-id="8ed45-203">For an example of each configuration, see hello [Example: Custom DNS](#example-dns) section.</span></span>

<span data-ttu-id="8ed45-204">Pour plus d’informations, consultez hello [résolution de noms pour les machines virtuelles et Instances de rôle](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) document.</span><span class="sxs-lookup"><span data-stu-id="8ed45-204">For more information, see hello [Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) document.</span></span>

## <a name="directly-connect-toohadoop-services"></a><span data-ttu-id="8ed45-205">Se connecter directement des services de tooHadoop</span><span class="sxs-lookup"><span data-stu-id="8ed45-205">Directly connect tooHadoop services</span></span>

<span data-ttu-id="8ed45-206">La plupart des documentation sur HDInsight suppose que vous avez des cluster toohello d’accès sur hello internet.</span><span class="sxs-lookup"><span data-stu-id="8ed45-206">Most documentation on HDInsight assumes that you have access toohello cluster over hello internet.</span></span> <span data-ttu-id="8ed45-207">Par exemple, que vous pouvez vous connecter à cluster toohello à https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="8ed45-207">For example, that you can connect toohello cluster at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="8ed45-208">Cette adresse utilise la passerelle publique hello, qui n’est pas disponible si vous avez utilisé des groupes de sécurité réseau ou d’accès toorestrict UDRs hello internet.</span><span class="sxs-lookup"><span data-stu-id="8ed45-208">This address uses hello public gateway, which is not available if you have used NSGs or UDRs toorestrict access from hello internet.</span></span>

<span data-ttu-id="8ed45-209">tooconnect tooAmbari et autres pages web via un réseau virtuel de hello, utilisez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8ed45-209">tooconnect tooAmbari and other web pages through hello virtual network, use hello following steps:</span></span>

1. <span data-ttu-id="8ed45-210">noms de domaine complet interne toodiscover hello (FQDN) des nœuds de cluster HDInsight hello, utilisez une des méthodes suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="8ed45-210">toodiscover hello internal fully qualified domain names (FQDN) of hello HDInsight cluster nodes, use one of hello following methods:</span></span>

    ```powershell
    $resourceGroupName = "hello resource group that contains hello virtual network used with HDInsight"

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

    <span data-ttu-id="8ed45-211">Dans la liste hello de nœuds retournés, rechercher hello nom de domaine complet pour hello noeuds head, hello FQDN tooconnect tooAmbari et autres services web.</span><span class="sxs-lookup"><span data-stu-id="8ed45-211">In hello list of nodes returned, find hello FQDN for hello head nodes and use hello FQDNs tooconnect tooAmbari and other web services.</span></span> <span data-ttu-id="8ed45-212">Par exemple, utilisez `http://<headnode-fqdn>:8080` tooaccess Ambari.</span><span class="sxs-lookup"><span data-stu-id="8ed45-212">For example, use `http://<headnode-fqdn>:8080` tooaccess Ambari.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="8ed45-213">Certains services hébergés sur les nœuds principaux hello sont uniquement actifs sur un seul nœud à la fois.</span><span class="sxs-lookup"><span data-stu-id="8ed45-213">Some services hosted on hello head nodes are only active on one node at a time.</span></span> <span data-ttu-id="8ed45-214">Si vous essayez d’accéder à un service sur un seul nœud principal, et retourne une erreur 404, basculez toohello autre nœud principal.</span><span class="sxs-lookup"><span data-stu-id="8ed45-214">If you try accessing a service on one head node and it returns a 404 error, switch toohello other head node.</span></span>

2. <span data-ttu-id="8ed45-215">nœud de hello toodetermine et de port d’un service est disponible, consultez hello [Ports utilisés par les services de Hadoop dans HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span><span class="sxs-lookup"><span data-stu-id="8ed45-215">toodetermine hello node and port that a service is available on, see hello [Ports used by Hadoop services on HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

## <span data-ttu-id="8ed45-216"><a id="networktraffic"></a> Contrôler le trafic réseau</span><span class="sxs-lookup"><span data-stu-id="8ed45-216"><a id="networktraffic"></a> Controlling network traffic</span></span>

<span data-ttu-id="8ed45-217">Le trafic réseau dans des réseaux virtuels Azure peut être contrôlé à l’aide de hello méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="8ed45-217">Network traffic in an Azure Virtual Networks can be controlled using hello following methods:</span></span>

* <span data-ttu-id="8ed45-218">**Groupes de sécurité réseau** (NSG) permettent de réseau de toohello toofilter trafic entrant et sortant.</span><span class="sxs-lookup"><span data-stu-id="8ed45-218">**Network security groups** (NSG) allow you toofilter inbound and outbound traffic toohello network.</span></span> <span data-ttu-id="8ed45-219">Pour plus d’informations, consultez hello [filtrer le trafic réseau avec les groupes de sécurité réseau](../virtual-network/virtual-networks-nsg.md) document.</span><span class="sxs-lookup"><span data-stu-id="8ed45-219">For more information, see hello [Filter network traffic with network security groups](../virtual-network/virtual-networks-nsg.md) document.</span></span>

    > [!WARNING]
    > <span data-ttu-id="8ed45-220">HDInsight ne prend pas en charge la restriction du trafic sortant.</span><span class="sxs-lookup"><span data-stu-id="8ed45-220">HDInsight does not support restricting outbound traffic.</span></span>

* <span data-ttu-id="8ed45-221">**Itinéraires définis par l’utilisateur** (UDR) définissent le flux de trafic entre les ressources réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="8ed45-221">**User-defined routes** (UDR) define how traffic flows between resources in hello network.</span></span> <span data-ttu-id="8ed45-222">Pour plus d’informations, consultez hello [itinéraires définis par l’utilisateur et le transfert IP](../virtual-network/virtual-networks-udr-overview.md) document.</span><span class="sxs-lookup"><span data-stu-id="8ed45-222">For more information, see hello [User-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md) document.</span></span>

* <span data-ttu-id="8ed45-223">**Réseau virtuel** répliquer fonctionnalité hello des périphériques tels que les routeurs et pare-feu.</span><span class="sxs-lookup"><span data-stu-id="8ed45-223">**Network virtual appliances** replicate hello functionality of devices such as firewalls and routers.</span></span> <span data-ttu-id="8ed45-224">Pour plus d’informations, consultez hello [dispositifs réseau](https://azure.microsoft.com/solutions/network-appliances) document.</span><span class="sxs-lookup"><span data-stu-id="8ed45-224">For more information, see hello [Network Appliances](https://azure.microsoft.com/solutions/network-appliances) document.</span></span>

<span data-ttu-id="8ed45-225">Un service géré, HDInsight nécessite les services de gestion et de contrôle d’intégrité de tooAzure Bonjour Azure cloud un accès illimité.</span><span class="sxs-lookup"><span data-stu-id="8ed45-225">As a managed service, HDInsight requires unrestricted access tooAzure health and management services in hello Azure cloud.</span></span> <span data-ttu-id="8ed45-226">Lorsque vous utilisez des groupes de sécurité réseau et des itinéraires définis par l’utilisateur, vous devez vous assurer que ces services peuvent toujours communiquer avec HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8ed45-226">When using NSGs and UDRs, you must ensure that HDInsight these services can still communicate with HDInsight.</span></span>

<span data-ttu-id="8ed45-227">HDInsight expose des services sur plusieurs ports.</span><span class="sxs-lookup"><span data-stu-id="8ed45-227">HDInsight exposes services on several ports.</span></span> <span data-ttu-id="8ed45-228">Lorsque vous utilisez un pare-feu d’appliance virtuelle, vous devez autoriser le trafic sur hello ports utilisés pour ces services.</span><span class="sxs-lookup"><span data-stu-id="8ed45-228">When using a virtual appliance firewall, you must allow traffic on hello ports used for these services.</span></span> <span data-ttu-id="8ed45-229">Pour plus d’informations, consultez hello [ports requis].</span><span class="sxs-lookup"><span data-stu-id="8ed45-229">For more information, see hello [Required ports] section.</span></span>

### <span data-ttu-id="8ed45-230"><a id="hdinsight-ip"></a> HDInsight avec des groupes de sécurité réseau et des itinéraires définis par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="8ed45-230"><a id="hdinsight-ip"></a> HDInsight with network security groups and user-defined routes</span></span>

<span data-ttu-id="8ed45-231">Si vous prévoyez d’utiliser **groupes de sécurité réseau** ou **itinéraires définis par l’utilisateur** toocontrol le trafic réseau, effectuer hello suivant des actions avant d’installer HDInsight :</span><span class="sxs-lookup"><span data-stu-id="8ed45-231">If you plan on using **network security groups** or **user-defined routes** toocontrol network traffic, perform hello following actions before installing HDInsight:</span></span>

1. <span data-ttu-id="8ed45-232">Identifiez hello région Azure que vous envisagez de toouse pour HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8ed45-232">Identify hello Azure region that you plan toouse for HDInsight.</span></span>

2. <span data-ttu-id="8ed45-233">Identifiez les adresses IP hello requis par HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8ed45-233">Identify hello IP addresses required by HDInsight.</span></span> <span data-ttu-id="8ed45-234">Pour plus d’informations, consultez hello [les adresses IP requises par HDInsight](#hdinsight-ip) section.</span><span class="sxs-lookup"><span data-stu-id="8ed45-234">For more information, see hello [IP Addresses required by HDInsight](#hdinsight-ip) section.</span></span>

3. <span data-ttu-id="8ed45-235">Créer ou modifier des groupes de sécurité réseau hello ou défini par l’utilisateur les itinéraires de sous-réseau hello que vous envisagez de tooinstall HDInsight dans.</span><span class="sxs-lookup"><span data-stu-id="8ed45-235">Create or modify hello network security groups or user-defined routes for hello subnet that you plan tooinstall HDInsight into.</span></span>

    * <span data-ttu-id="8ed45-236">__Groupes de sécurité réseau__: autoriser __entrant__ le trafic sur le port __443__ à partir d’adresses IP de hello.</span><span class="sxs-lookup"><span data-stu-id="8ed45-236">__Network security groups__: allow __inbound__ traffic on port __443__ from hello IP addresses.</span></span>
    * <span data-ttu-id="8ed45-237">__Itinéraires définis par l’utilisateur__: créer une itinéraire tooeach une adresse IP et de définir hello __type de tronçon suivant__ too__Internet__.</span><span class="sxs-lookup"><span data-stu-id="8ed45-237">__User-defined routes__: create a route tooeach IP address and set hello __Next hop type__ too__Internet__.</span></span>

<span data-ttu-id="8ed45-238">Pour plus d’informations sur les groupes de sécurité réseau ou des itinéraires définis par l’utilisateur, consultez hello suivant la documentation :</span><span class="sxs-lookup"><span data-stu-id="8ed45-238">For more information on network security groups or user-defined routes, see hello following documentation:</span></span>

* [<span data-ttu-id="8ed45-239">Groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="8ed45-239">Network security group</span></span>](../virtual-network/virtual-networks-nsg.md)

* [<span data-ttu-id="8ed45-240">Itinéraires définis par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="8ed45-240">User-defined routes</span></span>](../virtual-network/virtual-networks-udr-overview.md)

#### <a name="forced-tunneling"></a><span data-ttu-id="8ed45-241">Tunneling forcé</span><span class="sxs-lookup"><span data-stu-id="8ed45-241">Forced tunneling</span></span>

<span data-ttu-id="8ed45-242">Le tunneling forcé est une configuration de routage défini par l’utilisateur où tout le trafic à partir d’un sous-réseau de réseau tooa forcé ou emplacement, tel que votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="8ed45-242">Forced tunneling is a user-defined routing configuration where all traffic from a subnet is forced tooa specific network or location, such as your on-premises network.</span></span> <span data-ttu-id="8ed45-243">HDInsight ne prend __pas__ en charge le tunneling forcé.</span><span class="sxs-lookup"><span data-stu-id="8ed45-243">HDInsight does __not__ support forced tunneling.</span></span>

## <span data-ttu-id="8ed45-244"><a id="hdinsight-ip"></a> Adresses IP requises</span><span class="sxs-lookup"><span data-stu-id="8ed45-244"><a id="hdinsight-ip"></a> Required IP addresses</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ed45-245">Hello Azure health et services de gestion doivent être en mesure de toocommunicate avec HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8ed45-245">hello Azure health and management services must be able toocommunicate with HDInsight.</span></span> <span data-ttu-id="8ed45-246">Si vous utilisez des groupes de sécurité réseau ou des itinéraires définis par l’utilisateur, vous pouvez autoriser le trafic hello adresses IP pour ces tooreach services HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8ed45-246">If you use network security groups or user-defined routes, allow traffic from hello IP addresses for these services tooreach HDInsight.</span></span>
>
> <span data-ttu-id="8ed45-247">Si vous n’utilisez pas le trafic de toocontrol itinéraires définis par l’utilisateur ou de groupes de sécurité réseau, vous pouvez ignorer cette section.</span><span class="sxs-lookup"><span data-stu-id="8ed45-247">If you do not use network security groups or user-defined routes toocontrol traffic, you can ignore this section.</span></span>

<span data-ttu-id="8ed45-248">Si vous utilisez des groupes de sécurité réseau ou des itinéraires définis par l’utilisateur, vous devez autoriser le trafic hello Azure health et gestion des services tooreach HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8ed45-248">If you use network security groups or user-defined routes, you must allow traffic from hello Azure health and management services tooreach HDInsight.</span></span> <span data-ttu-id="8ed45-249">Utilisez hello suivant les étapes toofind hello adresses IP qui doivent être autorisées :</span><span class="sxs-lookup"><span data-stu-id="8ed45-249">Use hello following steps toofind hello IP addresses that must be allowed:</span></span>

1. <span data-ttu-id="8ed45-250">Vous devez toujours autoriser le trafic à partir de hello suivant des adresses IP :</span><span class="sxs-lookup"><span data-stu-id="8ed45-250">You must always allow traffic from hello following IP addresses:</span></span>

    | <span data-ttu-id="8ed45-251">Adresse IP</span><span class="sxs-lookup"><span data-stu-id="8ed45-251">IP address</span></span> | <span data-ttu-id="8ed45-252">Port autorisé</span><span class="sxs-lookup"><span data-stu-id="8ed45-252">Allowed port</span></span> | <span data-ttu-id="8ed45-253">Direction</span><span class="sxs-lookup"><span data-stu-id="8ed45-253">Direction</span></span> |
    | ---- | ----- | ----- |
    | <span data-ttu-id="8ed45-254">168.61.49.99</span><span class="sxs-lookup"><span data-stu-id="8ed45-254">168.61.49.99</span></span> | <span data-ttu-id="8ed45-255">443</span><span class="sxs-lookup"><span data-stu-id="8ed45-255">443</span></span> | <span data-ttu-id="8ed45-256">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="8ed45-256">Inbound</span></span> |
    | <span data-ttu-id="8ed45-257">23.99.5.239</span><span class="sxs-lookup"><span data-stu-id="8ed45-257">23.99.5.239</span></span> | <span data-ttu-id="8ed45-258">443</span><span class="sxs-lookup"><span data-stu-id="8ed45-258">443</span></span> | <span data-ttu-id="8ed45-259">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="8ed45-259">Inbound</span></span> |
    | <span data-ttu-id="8ed45-260">168.61.48.131</span><span class="sxs-lookup"><span data-stu-id="8ed45-260">168.61.48.131</span></span> | <span data-ttu-id="8ed45-261">443</span><span class="sxs-lookup"><span data-stu-id="8ed45-261">443</span></span> | <span data-ttu-id="8ed45-262">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="8ed45-262">Inbound</span></span> |
    | <span data-ttu-id="8ed45-263">138.91.141.162</span><span class="sxs-lookup"><span data-stu-id="8ed45-263">138.91.141.162</span></span> | <span data-ttu-id="8ed45-264">443</span><span class="sxs-lookup"><span data-stu-id="8ed45-264">443</span></span> | <span data-ttu-id="8ed45-265">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="8ed45-265">Inbound</span></span> |

2. <span data-ttu-id="8ed45-266">Si votre cluster HDInsight est dans un des hello suivant des régions, vous devez autoriser le trafic provenant d’adresses IP de hello répertoriées pour la région de hello :</span><span class="sxs-lookup"><span data-stu-id="8ed45-266">If your HDInsight cluster is in one of hello following regions, then you must allow traffic from hello IP addresses listed for hello region:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="8ed45-267">Si hello région Azure que vous utilisez n’est pas répertorié, utilisez uniquement les adresses IP quatre hello à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="8ed45-267">If hello Azure region you are using is not listed, then only use hello four IP addresses from step 1.</span></span>

    | <span data-ttu-id="8ed45-268">Pays</span><span class="sxs-lookup"><span data-stu-id="8ed45-268">Country</span></span> | <span data-ttu-id="8ed45-269">Région</span><span class="sxs-lookup"><span data-stu-id="8ed45-269">Region</span></span> | <span data-ttu-id="8ed45-270">Adresses IP autorisées</span><span class="sxs-lookup"><span data-stu-id="8ed45-270">Allowed IP addresses</span></span> | <span data-ttu-id="8ed45-271">Port autorisé</span><span class="sxs-lookup"><span data-stu-id="8ed45-271">Allowed port</span></span> | <span data-ttu-id="8ed45-272">Direction</span><span class="sxs-lookup"><span data-stu-id="8ed45-272">Direction</span></span> |
    | ---- | ---- | ---- | ---- | ----- |
    | <span data-ttu-id="8ed45-273">Asie</span><span class="sxs-lookup"><span data-stu-id="8ed45-273">Asia</span></span> | <span data-ttu-id="8ed45-274">Est de l'Asie</span><span class="sxs-lookup"><span data-stu-id="8ed45-274">East Asia</span></span> | <span data-ttu-id="8ed45-275">23.102.235.122</span><span class="sxs-lookup"><span data-stu-id="8ed45-275">23.102.235.122</span></span></br><span data-ttu-id="8ed45-276">52.175.38.134</span><span class="sxs-lookup"><span data-stu-id="8ed45-276">52.175.38.134</span></span> | <span data-ttu-id="8ed45-277">443</span><span class="sxs-lookup"><span data-stu-id="8ed45-277">443</span></span> | <span data-ttu-id="8ed45-278">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="8ed45-278">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="8ed45-279">Asie du Sud-Est</span><span class="sxs-lookup"><span data-stu-id="8ed45-279">Southeast Asia</span></span> | <span data-ttu-id="8ed45-280">13.76.245.160</span><span class="sxs-lookup"><span data-stu-id="8ed45-280">13.76.245.160</span></span></br><span data-ttu-id="8ed45-281">13.76.136.249</span><span class="sxs-lookup"><span data-stu-id="8ed45-281">13.76.136.249</span></span> | <span data-ttu-id="8ed45-282">443</span><span class="sxs-lookup"><span data-stu-id="8ed45-282">443</span></span> | <span data-ttu-id="8ed45-283">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="8ed45-283">Inbound</span></span> |
    | <span data-ttu-id="8ed45-284">Australie</span><span class="sxs-lookup"><span data-stu-id="8ed45-284">Australia</span></span> | <span data-ttu-id="8ed45-285">Est de l’Australie</span><span class="sxs-lookup"><span data-stu-id="8ed45-285">Australia East</span></span> | <span data-ttu-id="8ed45-286">104.210.84.115</span><span class="sxs-lookup"><span data-stu-id="8ed45-286">104.210.84.115</span></span></br><span data-ttu-id="8ed45-287">13.75.152.195</span><span class="sxs-lookup"><span data-stu-id="8ed45-287">13.75.152.195</span></span> | <span data-ttu-id="8ed45-288">443</span><span class="sxs-lookup"><span data-stu-id="8ed45-288">443</span></span> | <span data-ttu-id="8ed45-289">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="8ed45-289">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="8ed45-290">Sud-est de l’Australie</span><span class="sxs-lookup"><span data-stu-id="8ed45-290">Australia Southeast</span></span> | <span data-ttu-id="8ed45-291">13.77.2.56</span><span class="sxs-lookup"><span data-stu-id="8ed45-291">13.77.2.56</span></span></br><span data-ttu-id="8ed45-292">13.77.2.94</span><span class="sxs-lookup"><span data-stu-id="8ed45-292">13.77.2.94</span></span> | <span data-ttu-id="8ed45-293">443</span><span class="sxs-lookup"><span data-stu-id="8ed45-293">443</span></span> | <span data-ttu-id="8ed45-294">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="8ed45-294">Inbound</span></span> |
    | <span data-ttu-id="8ed45-295">Brésil</span><span class="sxs-lookup"><span data-stu-id="8ed45-295">Brazil</span></span> | <span data-ttu-id="8ed45-296">Sud du Brésil</span><span class="sxs-lookup"><span data-stu-id="8ed45-296">Brazil South</span></span> | <span data-ttu-id="8ed45-297">191.235.84.104</span><span class="sxs-lookup"><span data-stu-id="8ed45-297">191.235.84.104</span></span></br><span data-ttu-id="8ed45-298">191.235.87.113</span><span class="sxs-lookup"><span data-stu-id="8ed45-298">191.235.87.113</span></span> | <span data-ttu-id="8ed45-299">443</span><span class="sxs-lookup"><span data-stu-id="8ed45-299">443</span></span> | <span data-ttu-id="8ed45-300">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="8ed45-300">Inbound</span></span> |
    | <span data-ttu-id="8ed45-301">Canada</span><span class="sxs-lookup"><span data-stu-id="8ed45-301">Canada</span></span> | <span data-ttu-id="8ed45-302">Est du Canada</span><span class="sxs-lookup"><span data-stu-id="8ed45-302">Canada East</span></span> | <span data-ttu-id="8ed45-303">52.229.127.96</span><span class="sxs-lookup"><span data-stu-id="8ed45-303">52.229.127.96</span></span></br><span data-ttu-id="8ed45-304">52.229.123.172</span><span class="sxs-lookup"><span data-stu-id="8ed45-304">52.229.123.172</span></span> | <span data-ttu-id="8ed45-305">443</span><span class="sxs-lookup"><span data-stu-id="8ed45-305">443</span></span> | <span data-ttu-id="8ed45-306">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="8ed45-306">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="8ed45-307">Centre du Canada</span><span class="sxs-lookup"><span data-stu-id="8ed45-307">Canada Central</span></span> | <span data-ttu-id="8ed45-308">52.228.37.66</span><span class="sxs-lookup"><span data-stu-id="8ed45-308">52.228.37.66</span></span></br><span data-ttu-id="8ed45-309">52.228.45.222</span><span class="sxs-lookup"><span data-stu-id="8ed45-309">52.228.45.222</span></span> | <span data-ttu-id="8ed45-310">443</span><span class="sxs-lookup"><span data-stu-id="8ed45-310">443</span></span> | <span data-ttu-id="8ed45-311">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="8ed45-311">Inbound</span></span> |
    | <span data-ttu-id="8ed45-312">Chine</span><span class="sxs-lookup"><span data-stu-id="8ed45-312">China</span></span> | <span data-ttu-id="8ed45-313">Chine du Nord</span><span class="sxs-lookup"><span data-stu-id="8ed45-313">China North</span></span> | <span data-ttu-id="8ed45-314">42.159.96.170</span><span class="sxs-lookup"><span data-stu-id="8ed45-314">42.159.96.170</span></span></br><span data-ttu-id="8ed45-315">139.217.2.219</span><span class="sxs-lookup"><span data-stu-id="8ed45-315">139.217.2.219</span></span> | <span data-ttu-id="8ed45-316">443</span><span class="sxs-lookup"><span data-stu-id="8ed45-316">443</span></span> | <span data-ttu-id="8ed45-317">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="8ed45-317">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="8ed45-318">Chine orientale</span><span class="sxs-lookup"><span data-stu-id="8ed45-318">China East</span></span> | <span data-ttu-id="8ed45-319">42.159.198.178</span><span class="sxs-lookup"><span data-stu-id="8ed45-319">42.159.198.178</span></span></br><span data-ttu-id="8ed45-320">42.159.234.157</span><span class="sxs-lookup"><span data-stu-id="8ed45-320">42.159.234.157</span></span> | <span data-ttu-id="8ed45-321">443</span><span class="sxs-lookup"><span data-stu-id="8ed45-321">443</span></span> | <span data-ttu-id="8ed45-322">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="8ed45-322">Inbound</span></span> |
    | <span data-ttu-id="8ed45-323">Europe</span><span class="sxs-lookup"><span data-stu-id="8ed45-323">Europe</span></span> | <span data-ttu-id="8ed45-324">Europe du Nord</span><span class="sxs-lookup"><span data-stu-id="8ed45-324">North Europe</span></span> | <span data-ttu-id="8ed45-325">52.164.210.96</span><span class="sxs-lookup"><span data-stu-id="8ed45-325">52.164.210.96</span></span></br><span data-ttu-id="8ed45-326">13.74.153.132</span><span class="sxs-lookup"><span data-stu-id="8ed45-326">13.74.153.132</span></span> | <span data-ttu-id="8ed45-327">443</span><span class="sxs-lookup"><span data-stu-id="8ed45-327">443</span></span> | <span data-ttu-id="8ed45-328">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="8ed45-328">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="8ed45-329">Europe de l'Ouest</span><span class="sxs-lookup"><span data-stu-id="8ed45-329">West Europe</span></span>| <span data-ttu-id="8ed45-330">52.166.243.90</span><span class="sxs-lookup"><span data-stu-id="8ed45-330">52.166.243.90</span></span></br><span data-ttu-id="8ed45-331">52.174.36.244</span><span class="sxs-lookup"><span data-stu-id="8ed45-331">52.174.36.244</span></span> | <span data-ttu-id="8ed45-332">443</span><span class="sxs-lookup"><span data-stu-id="8ed45-332">443</span></span> | <span data-ttu-id="8ed45-333">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="8ed45-333">Inbound</span></span> |
    | <span data-ttu-id="8ed45-334">Allemagne</span><span class="sxs-lookup"><span data-stu-id="8ed45-334">Germany</span></span> | <span data-ttu-id="8ed45-335">Centre de l’Allemagne</span><span class="sxs-lookup"><span data-stu-id="8ed45-335">Germany Central</span></span> | <span data-ttu-id="8ed45-336">51.4.146.68</span><span class="sxs-lookup"><span data-stu-id="8ed45-336">51.4.146.68</span></span></br><span data-ttu-id="8ed45-337">51.4.146.80</span><span class="sxs-lookup"><span data-stu-id="8ed45-337">51.4.146.80</span></span> | <span data-ttu-id="8ed45-338">443</span><span class="sxs-lookup"><span data-stu-id="8ed45-338">443</span></span> | <span data-ttu-id="8ed45-339">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="8ed45-339">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="8ed45-340">Nord-Est de l’Allemagne</span><span class="sxs-lookup"><span data-stu-id="8ed45-340">Germany Northeast</span></span> | <span data-ttu-id="8ed45-341">51.5.150.132</span><span class="sxs-lookup"><span data-stu-id="8ed45-341">51.5.150.132</span></span></br><span data-ttu-id="8ed45-342">51.5.144.101</span><span class="sxs-lookup"><span data-stu-id="8ed45-342">51.5.144.101</span></span> | <span data-ttu-id="8ed45-343">443</span><span class="sxs-lookup"><span data-stu-id="8ed45-343">443</span></span> | <span data-ttu-id="8ed45-344">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="8ed45-344">Inbound</span></span> |
    | <span data-ttu-id="8ed45-345">Inde</span><span class="sxs-lookup"><span data-stu-id="8ed45-345">India</span></span> | <span data-ttu-id="8ed45-346">Inde centrale</span><span class="sxs-lookup"><span data-stu-id="8ed45-346">Central India</span></span> | <span data-ttu-id="8ed45-347">52.172.153.209</span><span class="sxs-lookup"><span data-stu-id="8ed45-347">52.172.153.209</span></span></br><span data-ttu-id="8ed45-348">52.172.152.49</span><span class="sxs-lookup"><span data-stu-id="8ed45-348">52.172.152.49</span></span> | <span data-ttu-id="8ed45-349">443</span><span class="sxs-lookup"><span data-stu-id="8ed45-349">443</span></span> | <span data-ttu-id="8ed45-350">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="8ed45-350">Inbound</span></span> |
    | <span data-ttu-id="8ed45-351">Japon</span><span class="sxs-lookup"><span data-stu-id="8ed45-351">Japan</span></span> | <span data-ttu-id="8ed45-352">Est du Japon</span><span class="sxs-lookup"><span data-stu-id="8ed45-352">Japan East</span></span> | <span data-ttu-id="8ed45-353">13.78.125.90</span><span class="sxs-lookup"><span data-stu-id="8ed45-353">13.78.125.90</span></span></br><span data-ttu-id="8ed45-354">13.78.89.60</span><span class="sxs-lookup"><span data-stu-id="8ed45-354">13.78.89.60</span></span> | <span data-ttu-id="8ed45-355">443</span><span class="sxs-lookup"><span data-stu-id="8ed45-355">443</span></span> | <span data-ttu-id="8ed45-356">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="8ed45-356">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="8ed45-357">Ouest du Japon</span><span class="sxs-lookup"><span data-stu-id="8ed45-357">Japan West</span></span> | <span data-ttu-id="8ed45-358">40.74.125.69</span><span class="sxs-lookup"><span data-stu-id="8ed45-358">40.74.125.69</span></span></br><span data-ttu-id="8ed45-359">138.91.29.150</span><span class="sxs-lookup"><span data-stu-id="8ed45-359">138.91.29.150</span></span> | <span data-ttu-id="8ed45-360">443</span><span class="sxs-lookup"><span data-stu-id="8ed45-360">443</span></span> | <span data-ttu-id="8ed45-361">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="8ed45-361">Inbound</span></span> |
    | <span data-ttu-id="8ed45-362">Corée du Sud</span><span class="sxs-lookup"><span data-stu-id="8ed45-362">Korea</span></span> | <span data-ttu-id="8ed45-363">Centre de la Corée</span><span class="sxs-lookup"><span data-stu-id="8ed45-363">Korea Central</span></span> | <span data-ttu-id="8ed45-364">52.231.39.142</span><span class="sxs-lookup"><span data-stu-id="8ed45-364">52.231.39.142</span></span></br><span data-ttu-id="8ed45-365">52.231.36.209</span><span class="sxs-lookup"><span data-stu-id="8ed45-365">52.231.36.209</span></span> | <span data-ttu-id="8ed45-366">433</span><span class="sxs-lookup"><span data-stu-id="8ed45-366">433</span></span> | <span data-ttu-id="8ed45-367">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="8ed45-367">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="8ed45-368">Corée du Sud</span><span class="sxs-lookup"><span data-stu-id="8ed45-368">Korea South</span></span> | <span data-ttu-id="8ed45-369">52.231.203.16</span><span class="sxs-lookup"><span data-stu-id="8ed45-369">52.231.203.16</span></span></br><span data-ttu-id="8ed45-370">52.231.205.214</span><span class="sxs-lookup"><span data-stu-id="8ed45-370">52.231.205.214</span></span> | <span data-ttu-id="8ed45-371">443</span><span class="sxs-lookup"><span data-stu-id="8ed45-371">443</span></span> | <span data-ttu-id="8ed45-372">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="8ed45-372">Inbound</span></span>
    | <span data-ttu-id="8ed45-373">Royaume-Uni</span><span class="sxs-lookup"><span data-stu-id="8ed45-373">United Kingdom</span></span> | <span data-ttu-id="8ed45-374">Ouest du Royaume-Uni</span><span class="sxs-lookup"><span data-stu-id="8ed45-374">UK West</span></span> | <span data-ttu-id="8ed45-375">51.141.13.110</span><span class="sxs-lookup"><span data-stu-id="8ed45-375">51.141.13.110</span></span></br><span data-ttu-id="8ed45-376">51.141.7.20</span><span class="sxs-lookup"><span data-stu-id="8ed45-376">51.141.7.20</span></span> | <span data-ttu-id="8ed45-377">443</span><span class="sxs-lookup"><span data-stu-id="8ed45-377">443</span></span> | <span data-ttu-id="8ed45-378">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="8ed45-378">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="8ed45-379">Sud du Royaume-Uni</span><span class="sxs-lookup"><span data-stu-id="8ed45-379">UK South</span></span> | <span data-ttu-id="8ed45-380">51.140.47.39</span><span class="sxs-lookup"><span data-stu-id="8ed45-380">51.140.47.39</span></span></br><span data-ttu-id="8ed45-381">51.140.52.16</span><span class="sxs-lookup"><span data-stu-id="8ed45-381">51.140.52.16</span></span> | <span data-ttu-id="8ed45-382">443</span><span class="sxs-lookup"><span data-stu-id="8ed45-382">443</span></span> | <span data-ttu-id="8ed45-383">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="8ed45-383">Inbound</span></span> |
    | <span data-ttu-id="8ed45-384">États-Unis</span><span class="sxs-lookup"><span data-stu-id="8ed45-384">United States</span></span> | <span data-ttu-id="8ed45-385">Centre des États-Unis</span><span class="sxs-lookup"><span data-stu-id="8ed45-385">Central US</span></span> | <span data-ttu-id="8ed45-386">13.67.223.215</span><span class="sxs-lookup"><span data-stu-id="8ed45-386">13.67.223.215</span></span></br><span data-ttu-id="8ed45-387">40.86.83.253</span><span class="sxs-lookup"><span data-stu-id="8ed45-387">40.86.83.253</span></span> | <span data-ttu-id="8ed45-388">443</span><span class="sxs-lookup"><span data-stu-id="8ed45-388">443</span></span> | <span data-ttu-id="8ed45-389">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="8ed45-389">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="8ed45-390">États-Unis - partie centrale septentrionale</span><span class="sxs-lookup"><span data-stu-id="8ed45-390">North Central US</span></span> | <span data-ttu-id="8ed45-391">157.56.8.38</span><span class="sxs-lookup"><span data-stu-id="8ed45-391">157.56.8.38</span></span></br><span data-ttu-id="8ed45-392">157.55.213.99</span><span class="sxs-lookup"><span data-stu-id="8ed45-392">157.55.213.99</span></span> | <span data-ttu-id="8ed45-393">443</span><span class="sxs-lookup"><span data-stu-id="8ed45-393">443</span></span> | <span data-ttu-id="8ed45-394">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="8ed45-394">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="8ed45-395">Centre-Ouest des États-Unis</span><span class="sxs-lookup"><span data-stu-id="8ed45-395">West Central US</span></span> | <span data-ttu-id="8ed45-396">52.161.23.15</span><span class="sxs-lookup"><span data-stu-id="8ed45-396">52.161.23.15</span></span></br><span data-ttu-id="8ed45-397">52.161.10.167</span><span class="sxs-lookup"><span data-stu-id="8ed45-397">52.161.10.167</span></span> | <span data-ttu-id="8ed45-398">443</span><span class="sxs-lookup"><span data-stu-id="8ed45-398">443</span></span> | <span data-ttu-id="8ed45-399">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="8ed45-399">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="8ed45-400">Ouest des États-Unis 2</span><span class="sxs-lookup"><span data-stu-id="8ed45-400">West US 2</span></span> | <span data-ttu-id="8ed45-401">52.175.211.210</span><span class="sxs-lookup"><span data-stu-id="8ed45-401">52.175.211.210</span></span></br><span data-ttu-id="8ed45-402">52.175.222.222</span><span class="sxs-lookup"><span data-stu-id="8ed45-402">52.175.222.222</span></span> | <span data-ttu-id="8ed45-403">443</span><span class="sxs-lookup"><span data-stu-id="8ed45-403">443</span></span> | <span data-ttu-id="8ed45-404">Trafic entrant</span><span class="sxs-lookup"><span data-stu-id="8ed45-404">Inbound</span></span> |

    <span data-ttu-id="8ed45-405">Pour plus d’informations sur l’IP de hello des adresses toouse pour Azure Government, consultez hello [Azure Government Intelligence + Analytique](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) document.</span><span class="sxs-lookup"><span data-stu-id="8ed45-405">For information on hello IP addresses toouse for Azure Government, see hello [Azure Government Intelligence + Analytics](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) document.</span></span>

3. <span data-ttu-id="8ed45-406">Si vous utilisez un serveur DNS personnalisé avec votre réseau virtuel, vous devez également autoriser l’accès à partir de __168.63.129.16__.</span><span class="sxs-lookup"><span data-stu-id="8ed45-406">If you use a custom DNS server with your virtual network, you must also allow access from __168.63.129.16__.</span></span> <span data-ttu-id="8ed45-407">Cette adresse est celle d’un programme de résolution récursive d’Azure.</span><span class="sxs-lookup"><span data-stu-id="8ed45-407">This address is Azure's recursive resolver.</span></span> <span data-ttu-id="8ed45-408">Pour plus d’informations, consultez hello [la résolution de noms pour les ordinateurs virtuels et de rôle instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) document.</span><span class="sxs-lookup"><span data-stu-id="8ed45-408">For more information, see hello [Name resolution for VMs and Role instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) document.</span></span>

<span data-ttu-id="8ed45-409">Pour plus d’informations, consultez hello [contrôler le trafic réseau](#networktraffic) section.</span><span class="sxs-lookup"><span data-stu-id="8ed45-409">For more information, see hello [Controlling network traffic](#networktraffic) section.</span></span>

## <span data-ttu-id="8ed45-410"><a id="hdinsight-ports"></a> Ports requis</span><span class="sxs-lookup"><span data-stu-id="8ed45-410"><a id="hdinsight-ports"></a> Required ports</span></span>

<span data-ttu-id="8ed45-411">Si vous prévoyez d’utiliser un réseau **pare-feu d’appliance virtuelle** toosecure hello réseau virtuel, et vous devez autoriser le trafic sortant sur hello suivant des ports :</span><span class="sxs-lookup"><span data-stu-id="8ed45-411">If you plan on using a network **virtual appliance firewall** toosecure hello virtual network, you must allow outbound traffic on hello following ports:</span></span>

* <span data-ttu-id="8ed45-412">53</span><span class="sxs-lookup"><span data-stu-id="8ed45-412">53</span></span>
* <span data-ttu-id="8ed45-413">443</span><span class="sxs-lookup"><span data-stu-id="8ed45-413">443</span></span>
* <span data-ttu-id="8ed45-414">1433</span><span class="sxs-lookup"><span data-stu-id="8ed45-414">1433</span></span>
* <span data-ttu-id="8ed45-415">11000-11999</span><span class="sxs-lookup"><span data-stu-id="8ed45-415">11000-11999</span></span>
* <span data-ttu-id="8ed45-416">14000-14999</span><span class="sxs-lookup"><span data-stu-id="8ed45-416">14000-14999</span></span>

<span data-ttu-id="8ed45-417">Pour obtenir la liste des ports utilisés pour des services spécifiques, consultez hello [Ports utilisés par les services de Hadoop dans HDInsight](hdinsight-hadoop-port-settings-for-services.md) document.</span><span class="sxs-lookup"><span data-stu-id="8ed45-417">For a list of ports for specific services, see hello [Ports used by Hadoop services on HDInsight](hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

<span data-ttu-id="8ed45-418">Pour plus d’informations sur les règles de pare-feu pour les équipements virtuels, consultez hello [scénario d’appliance virtuelle](../virtual-network/virtual-network-scenario-udr-gw-nva.md) document.</span><span class="sxs-lookup"><span data-stu-id="8ed45-418">For more information on firewall rules for virtual appliances, see hello [virtual appliance scenario](../virtual-network/virtual-network-scenario-udr-gw-nva.md) document.</span></span>

## <span data-ttu-id="8ed45-419"><a id="hdinsight-nsg"></a>Exemple : groupes de sécurité réseau avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="8ed45-419"><a id="hdinsight-nsg"></a>Example: network security groups with HDInsight</span></span>

<span data-ttu-id="8ed45-420">exemples Hello dans cette section illustrent le fonctionnement des règles de groupe de sécurité réseau toocreate qui autorisent des services de gestion Azure toocommunicate HDInsight avec hello.</span><span class="sxs-lookup"><span data-stu-id="8ed45-420">hello examples in this section demonstrate how toocreate network security group rules that allow HDInsight toocommunicate with hello Azure management services.</span></span> <span data-ttu-id="8ed45-421">Avant d’utiliser les exemples de hello, ajustez hello IP adresses toomatch hello ceux pour hello région Azure que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="8ed45-421">Before using hello examples, adjust hello IP addresses toomatch hello ones for hello Azure region you are using.</span></span> <span data-ttu-id="8ed45-422">Vous pouvez trouver ces informations dans hello [HDInsight avec des groupes de sécurité réseau et les itinéraires définis par l’utilisateur](#hdinsight-ip) section.</span><span class="sxs-lookup"><span data-stu-id="8ed45-422">You can find this information in hello [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

### <a name="azure-resource-management-template"></a><span data-ttu-id="8ed45-423">Modèle de gestion des ressources Azure</span><span class="sxs-lookup"><span data-stu-id="8ed45-423">Azure Resource Management template</span></span>

<span data-ttu-id="8ed45-424">Hello modèle de gestion des ressources suivant crée un réseau virtuel qui restreint le trafic entrant, mais autorise le trafic à partir d’adresses IP de hello requis par HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8ed45-424">hello following Resource Management template creates a virtual network that restricts inbound traffic, but allows traffic from hello IP addresses required by HDInsight.</span></span> <span data-ttu-id="8ed45-425">Ce modèle crée également un cluster HDInsight dans le réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="8ed45-425">This template also creates an HDInsight cluster in hello virtual network.</span></span>

* [<span data-ttu-id="8ed45-426">Déployer un réseau virtuel Azure sécurisé et un cluster Hadoop HDInsight</span><span class="sxs-lookup"><span data-stu-id="8ed45-426">Deploy a secured Azure Virtual Network and an HDInsight Hadoop cluster</span></span>](https://azure.microsoft.com/resources/templates/101-hdinsight-secure-vnet/)

> [!IMPORTANT]
> <span data-ttu-id="8ed45-427">Modifier les adresses IP hello utilisés dans cette hello de toomatch exemple région Azure que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="8ed45-427">Change hello IP addresses used in this example toomatch hello Azure region you are using.</span></span> <span data-ttu-id="8ed45-428">Vous pouvez trouver ces informations dans hello [HDInsight avec des groupes de sécurité réseau et les itinéraires définis par l’utilisateur](#hdinsight-ip) section.</span><span class="sxs-lookup"><span data-stu-id="8ed45-428">You can find this information in hello [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="8ed45-429">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ed45-429">Azure PowerShell</span></span>

<span data-ttu-id="8ed45-430">Utilisez hello suivant toocreate de script PowerShell un réseau virtuel qui restreint le trafic entrant et autorise le trafic de hello des adresses IP pour la région Europe du Nord hello.</span><span class="sxs-lookup"><span data-stu-id="8ed45-430">Use hello following PowerShell script toocreate a virtual network that restricts inbound traffic and allows traffic from hello IP addresses for hello North Europe region.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ed45-431">Modifier les adresses IP hello utilisés dans cette hello de toomatch exemple région Azure que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="8ed45-431">Change hello IP addresses used in this example toomatch hello Azure region you are using.</span></span> <span data-ttu-id="8ed45-432">Vous pouvez trouver ces informations dans hello [HDInsight avec des groupes de sécurité réseau et les itinéraires définis par l’utilisateur](#hdinsight-ip) section.</span><span class="sxs-lookup"><span data-stu-id="8ed45-432">You can find this information in hello [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

```powershell
$vnetName = "Replace with your virtual network name"
$resourceGroupName = "Replace with hello resource group hello virtual network is in"
$subnetName = "Replace with hello name of hello subnet that you plan toouse for HDInsight"
# Get hello Virtual Network object
$vnet = Get-AzureRmVirtualNetwork `
    -Name $vnetName `
    -ResourceGroupName $resourceGroupName
# Get hello region hello Virtual network is in.
$location = $vnet.Location
# Get hello subnet object
$subnet = $vnet.Subnets | Where-Object Name -eq $subnetName
# Create a Network Security Group.
# And add exemptions for hello HDInsight health and management services.
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
# Set hello changes toohello security group
Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
# Apply hello NSG toohello subnet
Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name $subnetName `
    -AddressPrefix $subnet.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

> [!IMPORTANT]
> <span data-ttu-id="8ed45-433">Cet exemple montre comment le trafic sur des adresses IP hello requis entrant tooadd règles tooallow.</span><span class="sxs-lookup"><span data-stu-id="8ed45-433">This example demonstrates how tooadd rules tooallow inbound traffic on hello required IP addresses.</span></span> <span data-ttu-id="8ed45-434">Il ne contient pas une règle toorestrict accès entrant depuis d’autres sources.</span><span class="sxs-lookup"><span data-stu-id="8ed45-434">It does not contain a rule toorestrict inbound access from other sources.</span></span>
>
> <span data-ttu-id="8ed45-435">Hello, l’exemple suivant montre comment accéder à tooenable SSH à partir de hello Internet :</span><span class="sxs-lookup"><span data-stu-id="8ed45-435">hello following example demonstrates how tooenable SSH access from hello Internet:</span></span>
>
> ```powershell
> Add-AzureRmNetworkSecurityRuleConfig -Name "SSH" -Description "SSH" -Protocol "*" -SourcePortRange "*" -DestinationPortRange "22" -SourceAddressPrefix "*" -DestinationAddressPrefix "VirtualNetwork" -Access Allow -Priority 306 -Direction Inbound
> ```

### <a name="azure-cli"></a><span data-ttu-id="8ed45-436">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="8ed45-436">Azure CLI</span></span>

<span data-ttu-id="8ed45-437">Utilisez hello suivant les étapes toocreate un réseau virtuel qui restreint le trafic entrant, mais autorise le trafic à partir d’adresses IP de hello requis par HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8ed45-437">Use hello following steps toocreate a virtual network that restricts inbound traffic, but allows traffic from hello IP addresses required by HDInsight.</span></span>

1. <span data-ttu-id="8ed45-438">Hello utilisation suivant toocreate de commande nommé d’un nouveau groupe de sécurité réseau `hdisecure`.</span><span class="sxs-lookup"><span data-stu-id="8ed45-438">Use hello following command toocreate a new network security group named `hdisecure`.</span></span> <span data-ttu-id="8ed45-439">Remplacez **RESOURCEGROUPNAME** avec le groupe de ressources hello contient hello réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="8ed45-439">Replace **RESOURCEGROUPNAME** with hello resource group that contains hello Azure Virtual Network.</span></span> <span data-ttu-id="8ed45-440">Remplacez **emplacement** avec l’emplacement hello (région), ce groupe hello a été créé dans.</span><span class="sxs-lookup"><span data-stu-id="8ed45-440">Replace **LOCATION** with hello location (region) that hello group was created in.</span></span>

    ```azurecli
    az network nsg create -g RESOURCEGROUPNAME -n hdisecure -l LOCATION
    ```

    <span data-ttu-id="8ed45-441">Une fois le groupe de hello a été créé, vous recevez des informations sur le nouveau groupe de hello.</span><span class="sxs-lookup"><span data-stu-id="8ed45-441">Once hello group has been created, you receive information on hello new group.</span></span>

2. <span data-ttu-id="8ed45-442">Utilisez hello suivant tooadd règles toohello nouveau groupe de sécurité réseau qui autorisent les communications entrantes sur le port 443 à partir de hello service de contrôle d’intégrité et de gestion Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8ed45-442">Use hello following tooadd rules toohello new network security group that allow inbound communication on port 443 from hello Azure HDInsight health and management service.</span></span> <span data-ttu-id="8ed45-443">Remplacez **RESOURCEGROUPNAME** avec nom hello hello du groupe de ressources contenant hello réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="8ed45-443">Replace **RESOURCEGROUPNAME** with hello name of hello resource group that contains hello Azure Virtual Network.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="8ed45-444">Modifier les adresses IP hello utilisés dans cette hello de toomatch exemple région Azure que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="8ed45-444">Change hello IP addresses used in this example toomatch hello Azure region you are using.</span></span> <span data-ttu-id="8ed45-445">Vous pouvez trouver ces informations dans hello [HDInsight avec des groupes de sécurité réseau et les itinéraires définis par l’utilisateur](#hdinsight-ip) section.</span><span class="sxs-lookup"><span data-stu-id="8ed45-445">You can find this information in hello [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

    ```azurecli
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule1 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "52.164.210.96" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 300 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "13.74.153.132" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 301 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.49.99" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 302 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "23.99.5.239" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 303 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.48.131" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 304 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "138.91.141.162" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 305 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n block --protocol "*" --source-port-range "*" --destination-port-range "*" --source-address-prefix "Internet" --destination-address-prefix "VirtualNetwork" --access "Deny" --priority 500 --direction "Inbound"
    ```

3. <span data-ttu-id="8ed45-446">tooretrieve hello identificateur unique pour ce groupe de sécurité réseau, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8ed45-446">tooretrieve hello unique identifier for this network security group, use hello following command:</span></span>

    ```azurecli
    az network nsg show -g RESOURCEGROUPNAME -n hdisecure --query 'id'
    ```

    <span data-ttu-id="8ed45-447">Cette commande retourne un toohello similaire valeur suit texte :</span><span class="sxs-lookup"><span data-stu-id="8ed45-447">This command returns a value similar toohello following text:</span></span>

        "/subscriptions/SUBSCRIPTIONID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"

    <span data-ttu-id="8ed45-448">Utilisez des guillemets doubles autour d’id dans la commande hello si vous n’obtenez pas les résultats de hello attendu.</span><span class="sxs-lookup"><span data-stu-id="8ed45-448">Use double-quotes around id in hello command if you don't get hello expected results.</span></span>

4. <span data-ttu-id="8ed45-449">Utilisez hello suivant commande tooapply hello sécurité groupe tooa sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="8ed45-449">Use hello following command tooapply hello network security group tooa subnet.</span></span> <span data-ttu-id="8ed45-450">Remplacez hello __GUID__ et __RESOURCEGROUPNAME__ valeurs avec hello ceux qui sont retournées à partir de l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="8ed45-450">Replace hello __GUID__ and __RESOURCEGROUPNAME__ values with hello ones returned from hello previous step.</span></span> <span data-ttu-id="8ed45-451">Remplacez __VNETNAME__ et __SUBNETNAME__ avec le nom de réseau virtuel hello et le nom du sous-réseau que vous souhaitez toocreate.</span><span class="sxs-lookup"><span data-stu-id="8ed45-451">Replace __VNETNAME__ and __SUBNETNAME__ with hello virtual network name and subnet name that you want toocreate.</span></span>

    ```azurecli
    az network vnet subnet update -g RESOURCEGROUPNAME --vnet-name VNETNAME --name SUBNETNAME --set networkSecurityGroup.id="/subscriptions/GUID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"
    ```

    <span data-ttu-id="8ed45-452">Une fois cette commande terminée, vous pouvez installer HDInsight dans hello réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="8ed45-452">Once this command completes, you can install HDInsight into hello Virtual Network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ed45-453">Ces étapes uniquement ouvrir accès toohello HDInsight d’intégrité et de gestion de service sur hello cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="8ed45-453">These steps only open access toohello HDInsight health and management service on hello Azure cloud.</span></span> <span data-ttu-id="8ed45-454">N’importe quel autre accès toohello cluster HDInsight à partir de l’extérieur hello réseau virtuel est bloquée.</span><span class="sxs-lookup"><span data-stu-id="8ed45-454">Any other access toohello HDInsight cluster from outside hello Virtual Network is blocked.</span></span> <span data-ttu-id="8ed45-455">tooenable accès à partir du réseau virtuel externe hello, vous devez ajouter des règles de groupe de sécurité réseau supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="8ed45-455">tooenable access from outside hello virtual network, you must add additional Network Security Group rules.</span></span>
>
> <span data-ttu-id="8ed45-456">Hello, l’exemple suivant montre comment accéder à tooenable SSH à partir de hello Internet :</span><span class="sxs-lookup"><span data-stu-id="8ed45-456">hello following example demonstrates how tooenable SSH access from hello Internet:</span></span>
>
> ```azurecli
> az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule5 --protocol "*" --source-port-range "*" --destination-port-range "22" --source-address-prefix "*" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 306 --direction "Inbound"
> ```

## <span data-ttu-id="8ed45-457"><a id="example-dns"></a> Exemple : configuration de DNS</span><span class="sxs-lookup"><span data-stu-id="8ed45-457"><a id="example-dns"></a> Example: DNS configuration</span></span>

### <a name="name-resolution-between-a-virtual-network-and-a-connected-on-premises-network"></a><span data-ttu-id="8ed45-458">Résolution de noms entre un réseau virtuel et un réseau local connecté</span><span class="sxs-lookup"><span data-stu-id="8ed45-458">Name resolution between a virtual network and a connected on-premises network</span></span>

<span data-ttu-id="8ed45-459">Cet exemple montre comment hello suivant hypothèses :</span><span class="sxs-lookup"><span data-stu-id="8ed45-459">This example makes hello following assumptions:</span></span>

* <span data-ttu-id="8ed45-460">Vous avez un réseau virtuel Azure qui est le réseau local de tooan connecté à l’aide d’une passerelle VPN.</span><span class="sxs-lookup"><span data-stu-id="8ed45-460">You have an Azure Virtual Network that is connected tooan on-premises network using a VPN gateway.</span></span>

* <span data-ttu-id="8ed45-461">un serveur DNS personnalisé Hello dans le réseau virtuel de hello est en cours d’exécution Unix ou Linux comme système d’exploitation de hello.</span><span class="sxs-lookup"><span data-stu-id="8ed45-461">hello custom DNS server in hello virtual network is running Linux or Unix as hello operating system.</span></span>

* <span data-ttu-id="8ed45-462">[Lier](https://www.isc.org/downloads/bind/) est installé sur un serveur DNS personnalisé hello.</span><span class="sxs-lookup"><span data-stu-id="8ed45-462">[Bind](https://www.isc.org/downloads/bind/) is installed on hello custom DNS server.</span></span>

<span data-ttu-id="8ed45-463">Sur hello un serveur DNS personnalisé dans le réseau virtuel de hello :</span><span class="sxs-lookup"><span data-stu-id="8ed45-463">On hello custom DNS server in hello virtual network:</span></span>

1. <span data-ttu-id="8ed45-464">Utiliser Azure PowerShell ou CLI d’Azure toofind hello suffixe DNS du réseau virtuel de hello :</span><span class="sxs-lookup"><span data-stu-id="8ed45-464">Use either Azure PowerShell or Azure CLI toofind hello DNS suffix of hello virtual network:</span></span>

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. <span data-ttu-id="8ed45-465">Sur hello un serveur DNS personnalisé pour le réseau virtuel de hello, utilisez hello après le texte en tant que contenu hello Hello `/etc/bind/named.conf.local` fichier :</span><span class="sxs-lookup"><span data-stu-id="8ed45-465">On hello custom DNS server for hello virtual network, use hello following text as hello contents of hello `/etc/bind/named.conf.local` file:</span></span>

    ```
    // Forward requests for hello virtual network suffix tooAzure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {168.63.129.16;}; # Azure recursive resolver
    };
    ```

    <span data-ttu-id="8ed45-466">Remplacez hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` valeur dont le suffixe DNS hello votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="8ed45-466">Replace hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` value with hello DNS suffix of your virtual network.</span></span>

    <span data-ttu-id="8ed45-467">Cette configuration achemine toutes les requêtes DNS pour le suffixe DNS de hello du programme de résolution de Azure récursive toohello hello réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="8ed45-467">This configuration routes all DNS requests for hello DNS suffix of hello virtual network toohello Azure recursive resolver.</span></span>

2. <span data-ttu-id="8ed45-468">Sur hello un serveur DNS personnalisé pour le réseau virtuel de hello, utilisez hello après le texte en tant que contenu hello Hello `/etc/bind/named.conf.options` fichier :</span><span class="sxs-lookup"><span data-stu-id="8ed45-468">On hello custom DNS server for hello virtual network, use hello following text as hello contents of hello `/etc/bind/named.conf.options` file:</span></span>

    ```
    // Clients tooaccept requests from
    // TODO: Add hello IP range of hello joined network toothis list
    acl goodclients {
        10.0.0.0/16; # IP address range of hello virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            # All other requests are sent toohello following
            forwarders {
                192.168.0.1; # Replace with hello IP address of your on-premises DNS server
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform tooRFC1035
            listen-on { any; };
    };
    ```
    
    * <span data-ttu-id="8ed45-469">Remplacez hello `10.0.0.0/16` la valeur de la plage d’adresses IP hello de votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="8ed45-469">Replace hello `10.0.0.0/16` value with hello IP address range of your virtual network.</span></span> <span data-ttu-id="8ed45-470">Cette entrée permet que la résolution de noms demande des adresses à l’intérieur de cette plage.</span><span class="sxs-lookup"><span data-stu-id="8ed45-470">This entry allows name resolution requests addresses within this range.</span></span>

    * <span data-ttu-id="8ed45-471">Ajouter la plage d’adresses IP hello de toohello de réseau local hello `acl goodclients { ... }` section.</span><span class="sxs-lookup"><span data-stu-id="8ed45-471">Add hello IP address range of hello on-premises network toohello `acl goodclients { ... }` section.</span></span>  <span data-ttu-id="8ed45-472">entrée autorise les demandes de résolution de noms à partir des ressources dans un réseau local de hello.</span><span class="sxs-lookup"><span data-stu-id="8ed45-472">entry allows name resolution requests from resources in hello on-premises network.</span></span>
    
    * <span data-ttu-id="8ed45-473">Remplacez la valeur de hello `192.168.0.1` avec l’adresse IP de hello du serveur DNS local.</span><span class="sxs-lookup"><span data-stu-id="8ed45-473">Replace hello value `192.168.0.1` with hello IP address of your on-premises DNS server.</span></span> <span data-ttu-id="8ed45-474">Cette entrée achemine toutes les autres demandes toohello locale DNS serveur DNS.</span><span class="sxs-lookup"><span data-stu-id="8ed45-474">This entry routes all other DNS requests toohello on-premises DNS server.</span></span>

3. <span data-ttu-id="8ed45-475">configuration de hello toouse, redémarrez la liaison.</span><span class="sxs-lookup"><span data-stu-id="8ed45-475">toouse hello configuration, restart Bind.</span></span> <span data-ttu-id="8ed45-476">Par exemple, `sudo service bind9 restart`.</span><span class="sxs-lookup"><span data-stu-id="8ed45-476">For example, `sudo service bind9 restart`.</span></span>

4. <span data-ttu-id="8ed45-477">Ajouter un serveur DNS de redirecteur conditionnel toohello local.</span><span class="sxs-lookup"><span data-stu-id="8ed45-477">Add a conditional forwarder toohello on-premises DNS server.</span></span> <span data-ttu-id="8ed45-478">Configurer les demandes de toosend de redirecteur conditionnel hello le suffixe DNS à partir d’un serveur DNS personnalisé étape 1 toohello hello.</span><span class="sxs-lookup"><span data-stu-id="8ed45-478">Configure hello conditional forwarder toosend requests for hello DNS suffix from step 1 toohello custom DNS server.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8ed45-479">Consultez la documentation de hello pour votre logiciel DNS pour plus de détails sur la façon de tooadd un redirecteur conditionnel.</span><span class="sxs-lookup"><span data-stu-id="8ed45-479">Consult hello documentation for your DNS software for specifics on how tooadd a conditional forwarder.</span></span>

<span data-ttu-id="8ed45-480">Après avoir effectué ces étapes, vous pouvez vous connecter tooresources dans un réseau à l’aide de noms de domaine complet (FQDN).</span><span class="sxs-lookup"><span data-stu-id="8ed45-480">After completing these steps, you can connect tooresources in either network using fully qualified domain names (FQDN).</span></span> <span data-ttu-id="8ed45-481">Vous pouvez maintenant installer HDInsight dans le réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="8ed45-481">You can now install HDInsight into hello virtual network.</span></span>

### <a name="name-resolution-between-two-connected-virtual-networks"></a><span data-ttu-id="8ed45-482">Résolution de noms entre deux réseaux virtuels connectés</span><span class="sxs-lookup"><span data-stu-id="8ed45-482">Name resolution between two connected virtual networks</span></span>

<span data-ttu-id="8ed45-483">Cet exemple montre comment hello suivant hypothèses :</span><span class="sxs-lookup"><span data-stu-id="8ed45-483">This example makes hello following assumptions:</span></span>

* <span data-ttu-id="8ed45-484">Vous avez deux réseaux virtuels Azure connectés à l’aide d’une passerelle VPN ou d’une homologation.</span><span class="sxs-lookup"><span data-stu-id="8ed45-484">You have two Azure Virtual Networks that are connected using either a VPN gateway or peering.</span></span>

* <span data-ttu-id="8ed45-485">un serveur DNS personnalisé Hello dans les deux réseaux exécute Linux ou Unix en tant que système d’exploitation de hello.</span><span class="sxs-lookup"><span data-stu-id="8ed45-485">hello custom DNS server in both networks is running Linux or Unix as hello operating system.</span></span>

* <span data-ttu-id="8ed45-486">[Lier](https://www.isc.org/downloads/bind/) est installé sur des serveurs DNS personnalisés hello.</span><span class="sxs-lookup"><span data-stu-id="8ed45-486">[Bind](https://www.isc.org/downloads/bind/) is installed on hello custom DNS servers.</span></span>

1. <span data-ttu-id="8ed45-487">Utiliser Azure PowerShell ou CLI d’Azure toofind hello suffixe DNS de deux réseaux virtuels :</span><span class="sxs-lookup"><span data-stu-id="8ed45-487">Use either Azure PowerShell or Azure CLI toofind hello DNS suffix of both virtual networks:</span></span>

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. <span data-ttu-id="8ed45-488">Hello utilisation après le texte en tant que contenu hello Hello `/etc/bind/named.config.local` fichier sur un serveur DNS personnalisé hello.</span><span class="sxs-lookup"><span data-stu-id="8ed45-488">Use hello following text as hello contents of hello `/etc/bind/named.config.local` file on hello custom DNS server.</span></span> <span data-ttu-id="8ed45-489">Effectuez cette modification sur un serveur DNS personnalisé hello dans les deux réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="8ed45-489">Make this change on hello custom DNS server in both virtual networks.</span></span>

    ```
    // Forward requests for hello virtual network suffix tooAzure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # hello IP address of hello DNS server in hello other virtual network
    };
    ```

    <span data-ttu-id="8ed45-490">Remplacez hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` valeur dont le suffixe DNS hello hello __autres__ réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="8ed45-490">Replace hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` value with hello DNS suffix of hello __other__ virtual network.</span></span> <span data-ttu-id="8ed45-491">Cette entrée achemine les requêtes pour le suffixe DNS hello hello réseau distant toohello DNS personnalisé de ce réseau.</span><span class="sxs-lookup"><span data-stu-id="8ed45-491">This entry routes requests for hello DNS suffix of hello remote network toohello custom DNS in that network.</span></span>

3. <span data-ttu-id="8ed45-492">Sur hello des serveurs DNS personnalisés dans les deux réseaux virtuels, utilisez hello après le texte en tant que contenu hello Hello `/etc/bind/named.conf.options` fichier :</span><span class="sxs-lookup"><span data-stu-id="8ed45-492">On hello custom DNS servers in both virtual networks, use hello following text as hello contents of hello `/etc/bind/named.conf.options` file:</span></span>

    ```
    // Clients tooaccept requests from
    acl goodclients {
        10.1.0.0/16; # hello IP address range of one virtual network
        10.0.0.0/16; # hello IP address range of hello other virtual network
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

            auth-nxdomain no;    # conform tooRFC1035
            listen-on { any; };
    };
    ```
    
    * <span data-ttu-id="8ed45-493">Remplacez hello `10.0.0.0/16` et `10.1.0.0/16` valeurs hello IP adresse des plages de vos réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="8ed45-493">Replace hello `10.0.0.0/16` and `10.1.0.0/16` values with hello IP address ranges of your virtual networks.</span></span> <span data-ttu-id="8ed45-494">Cette entrée permet aux ressources de chaque réseau de demandes toomake des serveurs DNS de hello.</span><span class="sxs-lookup"><span data-stu-id="8ed45-494">This entry allows resources in each network toomake requests of hello DNS servers.</span></span>

    <span data-ttu-id="8ed45-495">Toutes les demandes qui ne sont pas pour les suffixes DNS de hello des réseaux virtuels de hello (par exemple, microsoft.com) est géré par le programme de résolution récursive Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8ed45-495">Any requests that are not for hello DNS suffixes of hello virtual networks (for example, microsoft.com) is handled by hello Azure recursive resolver.</span></span>

4. <span data-ttu-id="8ed45-496">configuration de hello toouse, redémarrez la liaison.</span><span class="sxs-lookup"><span data-stu-id="8ed45-496">toouse hello configuration, restart Bind.</span></span> <span data-ttu-id="8ed45-497">Par exemple, `sudo service bind9 restart` sur les deux serveurs DNS.</span><span class="sxs-lookup"><span data-stu-id="8ed45-497">For example, `sudo service bind9 restart` on both DNS servers.</span></span>

<span data-ttu-id="8ed45-498">Après avoir effectué ces étapes, vous pouvez vous connecter tooresources dans le réseau virtuel de hello à l’aide de noms de domaine complet (FQDN).</span><span class="sxs-lookup"><span data-stu-id="8ed45-498">After completing these steps, you can connect tooresources in hello virtual network using fully qualified domain names (FQDN).</span></span> <span data-ttu-id="8ed45-499">Vous pouvez maintenant installer HDInsight dans le réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="8ed45-499">You can now install HDInsight into hello virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ed45-500">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8ed45-500">Next steps</span></span>

* <span data-ttu-id="8ed45-501">Pour obtenir un exemple de bout en bout de la configuration de réseau local de HDInsight tooconnect tooan, consultez [réseau de se connecter de HDInsight tooan local](./connect-on-premises-network.md).</span><span class="sxs-lookup"><span data-stu-id="8ed45-501">For an end-to-end example of configuring HDInsight tooconnect tooan on-premises network, see [Connect HDInsight tooan on-premises network](./connect-on-premises-network.md).</span></span>

* <span data-ttu-id="8ed45-502">Pour plus d’informations sur les réseaux virtuels Azure, consultez hello [vue d’ensemble du réseau virtuel Azure](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8ed45-502">For more information on Azure virtual networks, see hello [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span></span>

* <span data-ttu-id="8ed45-503">Pour plus d’informations sur les groupes de sécurité réseau, consultez [Groupes de sécurité réseau](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="8ed45-503">For more information on network security groups, see [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="8ed45-504">Pour plus d’informations sur les routages par l’utilisateur, consultez [Routage définis par l’utilisateur et transfert IP](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8ed45-504">For more information on user-defined routes, see [USer-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>