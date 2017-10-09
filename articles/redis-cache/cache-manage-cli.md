---
title: "aaaManage le Cache Redis Azure à l’aide d’Azure CLI | Documents Microsoft"
description: "Découvrez comment tooinstall hello CLI d’Azure sur n’importe quelle plateforme, comment toouse il tooconnect tooyour compte Azure et comment toocreate et gérer un cache Redis à partir de hello CLI d’Azure."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 964ff245-859d-4bc1-bccf-62e4b3c1169f
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: e8ee30090133e6b4edea93dcd13fd171e75989bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-azure-redis-cache-using-hello-azure-command-line-interface-azure-cli"></a><span data-ttu-id="14674-103">Comment toocreate et gérer le Cache Redis Azure à l’aide de hello Azure Interface de ligne (Azure)</span><span class="sxs-lookup"><span data-stu-id="14674-103">How toocreate and manage Azure Redis Cache using hello Azure Command-Line Interface (Azure CLI)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="14674-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="14674-104">PowerShell</span></span>](cache-howto-manage-redis-cache-powershell.md)
> * [<span data-ttu-id="14674-105">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="14674-105">Azure CLI</span></span>](cache-manage-cli.md)
>
>

<span data-ttu-id="14674-106">Hello CLI d’Azure est un excellent moyen toomanage votre infrastructure Azure à partir de n’importe quelle plateforme.</span><span class="sxs-lookup"><span data-stu-id="14674-106">hello Azure CLI is a great way toomanage your Azure infrastructure from any platform.</span></span> <span data-ttu-id="14674-107">Cet article vous montre comment toocreate et gérer vos instances de Cache Redis Azure à l’aide de hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="14674-107">This article shows you how toocreate and manage your Azure Redis Cache instances using hello Azure CLI.</span></span>

> [!NOTE]
> <span data-ttu-id="14674-108">Cet article s’applique tooa la version précédente de CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="14674-108">This article applies tooa previous version of Azure CLI.</span></span> <span data-ttu-id="14674-109">Pour les scripts d’exemple hello dernière Azure CLI 2.0, consultez [exemples de cache Azure Redis de CLI](cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="14674-109">For hello latest Azure CLI 2.0 sample scripts, see [Azure CLI Redis cache samples](cli-samples.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="14674-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="14674-110">Prerequisites</span></span>
<span data-ttu-id="14674-111">toocreate et gérer des instances de Cache Redis Azure à l’aide de CLI d’Azure, vous devez effectuer des hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="14674-111">toocreate and manage Azure Redis Cache instances using Azure CLI, you must complete hello following steps.</span></span>

* <span data-ttu-id="14674-112">Vous devez disposer d’un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="14674-112">You must have an Azure account.</span></span> <span data-ttu-id="14674-113">Si vous n’en avez pas, vous pouvez créer un [compte gratuit](https://azure.microsoft.com/pricing/free-trial/) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="14674-113">If you don't have one, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a few moments.</span></span>
* <span data-ttu-id="14674-114">[Installer hello CLI d’Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="14674-114">[Install hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="14674-115">Se connecter à votre installation du CLI d’Azure avec un compte Azure personnel ou avec un travail ou scolaire compte Azure et connectez-vous à partir de hello CLI Azure à l’aide de hello `azure login` commande.</span><span class="sxs-lookup"><span data-stu-id="14674-115">Connect your Azure CLI installation with a personal Azure account, or with a work or school Azure account, and log in from hello Azure CLI using hello `azure login` command.</span></span> <span data-ttu-id="14674-116">toounderstand hello différences et choisir, consultez [connecter tooan abonnement Azure à partir de hello Azure Interface de ligne (Azure)](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="14674-116">toounderstand hello differences and choose, see [Connect tooan Azure subscription from hello Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="14674-117">Avant d’exécuter un des hello suivant de commandes, basculez hello CLI d’Azure en mode de gestionnaire de ressources en exécutant hello `azure config mode arm` commande.</span><span class="sxs-lookup"><span data-stu-id="14674-117">Before running any of hello following commands, switch hello Azure CLI into Resource Manager mode by running hello `azure config mode arm` command.</span></span> <span data-ttu-id="14674-118">Pour plus d’informations, consultez [utiliser hello CLI d’Azure toomanage Azure ressources et groupes de ressources](../xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="14674-118">For more information, see [Use hello Azure CLI toomanage Azure resources and resource groups](../xplat-cli-azure-resource-manager.md).</span></span>

## <a name="redis-cache-properties"></a><span data-ttu-id="14674-119">Propriétés du cache Redis</span><span class="sxs-lookup"><span data-stu-id="14674-119">Redis Cache properties</span></span>
<span data-ttu-id="14674-120">les propriétés suivantes Hello sont utilisées lors de la création et la mise à jour des instances de Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="14674-120">hello following properties are used when creating and updating Redis Cache instances.</span></span>

| <span data-ttu-id="14674-121">Propriété</span><span class="sxs-lookup"><span data-stu-id="14674-121">Property</span></span> | <span data-ttu-id="14674-122">Switch</span><span class="sxs-lookup"><span data-stu-id="14674-122">Switch</span></span> | <span data-ttu-id="14674-123">Description</span><span class="sxs-lookup"><span data-stu-id="14674-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="14674-124">name</span><span class="sxs-lookup"><span data-stu-id="14674-124">name</span></span> |<span data-ttu-id="14674-125">-n, --name</span><span class="sxs-lookup"><span data-stu-id="14674-125">-n, --name</span></span> |<span data-ttu-id="14674-126">Nom de hello du Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="14674-126">Name of hello Redis Cache.</span></span> |
| <span data-ttu-id="14674-127">resource group</span><span class="sxs-lookup"><span data-stu-id="14674-127">resource group</span></span> |<span data-ttu-id="14674-128">-g, --resource-group</span><span class="sxs-lookup"><span data-stu-id="14674-128">-g, --resource-group</span></span> |<span data-ttu-id="14674-129">Nom du groupe de ressources de hello.</span><span class="sxs-lookup"><span data-stu-id="14674-129">Name of hello Resource Group.</span></span> |
| <span data-ttu-id="14674-130">location</span><span class="sxs-lookup"><span data-stu-id="14674-130">location</span></span> |<span data-ttu-id="14674-131">-l, --location</span><span class="sxs-lookup"><span data-stu-id="14674-131">-l, --location</span></span> |<span data-ttu-id="14674-132">Cache d’emplacements de toocreate.</span><span class="sxs-lookup"><span data-stu-id="14674-132">Location toocreate cache.</span></span> |
| <span data-ttu-id="14674-133">size</span><span class="sxs-lookup"><span data-stu-id="14674-133">size</span></span> |<span data-ttu-id="14674-134">-z, --size</span><span class="sxs-lookup"><span data-stu-id="14674-134">-z, --size</span></span> |<span data-ttu-id="14674-135">Taille de hello du Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="14674-135">Size of hello Redis Cache.</span></span> <span data-ttu-id="14674-136">Valeurs valides : [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span><span class="sxs-lookup"><span data-stu-id="14674-136">Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span></span> |
| <span data-ttu-id="14674-137">sku</span><span class="sxs-lookup"><span data-stu-id="14674-137">sku</span></span> |<span data-ttu-id="14674-138">-x, --sku</span><span class="sxs-lookup"><span data-stu-id="14674-138">-x, --sku</span></span> |<span data-ttu-id="14674-139">SKU Redis.</span><span class="sxs-lookup"><span data-stu-id="14674-139">Redis SKU.</span></span> <span data-ttu-id="14674-140">Doit être une des valeurs : [De Base, Standard, Premium]</span><span class="sxs-lookup"><span data-stu-id="14674-140">Should be one of : [Basic, Standard, Premium]</span></span> |
| <span data-ttu-id="14674-141">enableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="14674-141">EnableNonSslPort</span></span> |<span data-ttu-id="14674-142">-e, --enable-non-ssl-port</span><span class="sxs-lookup"><span data-stu-id="14674-142">-e, --enable-non-ssl-port</span></span> |<span data-ttu-id="14674-143">Propriété EnableNonSslPort Hello du Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="14674-143">EnableNonSslPort property of hello Redis Cache.</span></span> <span data-ttu-id="14674-144">Ajoutez cet indicateur si vous souhaitez que le Port tooenable hello Non SSL pour votre cache</span><span class="sxs-lookup"><span data-stu-id="14674-144">Add this flag if you want tooenable hello Non SSL Port for your cache</span></span> |
| <span data-ttu-id="14674-145">Configuration de Redis</span><span class="sxs-lookup"><span data-stu-id="14674-145">Redis Configuration</span></span> |<span data-ttu-id="14674-146">-c, --redis-configuration</span><span class="sxs-lookup"><span data-stu-id="14674-146">-c, --redis-configuration</span></span> |<span data-ttu-id="14674-147">Configuration de Redis.</span><span class="sxs-lookup"><span data-stu-id="14674-147">Redis Configuration.</span></span> <span data-ttu-id="14674-148">Entrez ici une chaîne au format JSON des clés et des valeurs de configuration.</span><span class="sxs-lookup"><span data-stu-id="14674-148">Enter a JSON formatted string of configuration keys and values here.</span></span> <span data-ttu-id="14674-149">Format :"{"":"","":""}"</span><span class="sxs-lookup"><span data-stu-id="14674-149">Format:"{"":"","":""}"</span></span> |
| <span data-ttu-id="14674-150">Configuration de Redis</span><span class="sxs-lookup"><span data-stu-id="14674-150">Redis Configuration</span></span> |<span data-ttu-id="14674-151">-f, --redis-configuration-file</span><span class="sxs-lookup"><span data-stu-id="14674-151">-f, --redis-configuration-file</span></span> |<span data-ttu-id="14674-152">Configuration de Redis.</span><span class="sxs-lookup"><span data-stu-id="14674-152">Redis Configuration.</span></span> <span data-ttu-id="14674-153">Entrez le chemin d’accès de hello d’un fichier contenant les clés de configuration et les valeurs ici.</span><span class="sxs-lookup"><span data-stu-id="14674-153">Enter hello path of a file containing configuration keys and values here.</span></span> <span data-ttu-id="14674-154">Format d’entrée du fichier hello : { » » : « », « » : « »}</span><span class="sxs-lookup"><span data-stu-id="14674-154">Format for hello file entry: {"":"","":""}</span></span> |
| <span data-ttu-id="14674-155">Nombre de partitions</span><span class="sxs-lookup"><span data-stu-id="14674-155">Shard Count</span></span> |<span data-ttu-id="14674-156">-r, --shard-count</span><span class="sxs-lookup"><span data-stu-id="14674-156">-r, --shard-count</span></span> |<span data-ttu-id="14674-157">Nombre de toocreate de partitions sur un Cache de Cluster Premium avec le clustering.</span><span class="sxs-lookup"><span data-stu-id="14674-157">Number of Shards toocreate on a Premium Cluster Cache with clustering.</span></span> |
| <span data-ttu-id="14674-158">Réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="14674-158">Virtual Network</span></span> |<span data-ttu-id="14674-159">-v, --virtual-network</span><span class="sxs-lookup"><span data-stu-id="14674-159">-v, --virtual-network</span></span> |<span data-ttu-id="14674-160">Lors de l’hébergement de votre cache dans un réseau virtuel spécifie hello exacte ID de ressource ARM Hello de toodeploy de réseau virtuel hello redis cache dans.</span><span class="sxs-lookup"><span data-stu-id="14674-160">When hosting your cache in a VNET, specifies hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in.</span></span> <span data-ttu-id="14674-161">Exemple de format : /subscriptions/{ID_abonnement}/resourceGroups/{nom_groupe_ressources}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span><span class="sxs-lookup"><span data-stu-id="14674-161">Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span></span> |
| <span data-ttu-id="14674-162">key type</span><span class="sxs-lookup"><span data-stu-id="14674-162">key type</span></span> |<span data-ttu-id="14674-163">-t, --key-type</span><span class="sxs-lookup"><span data-stu-id="14674-163">-t, --key-type</span></span> |<span data-ttu-id="14674-164">Type de clé toorenew.</span><span class="sxs-lookup"><span data-stu-id="14674-164">Type of key toorenew.</span></span> <span data-ttu-id="14674-165">Valeurs valides : [Primary, Secondary]</span><span class="sxs-lookup"><span data-stu-id="14674-165">Valid values: [Primary, Secondary]</span></span> |
| <span data-ttu-id="14674-166">StaticIP</span><span class="sxs-lookup"><span data-stu-id="14674-166">StaticIP</span></span> |<span data-ttu-id="14674-167">-p, --static-ip <static-ip></span><span class="sxs-lookup"><span data-stu-id="14674-167">-p, --static-ip <static-ip></span></span> |<span data-ttu-id="14674-168">Lorsque vous hébergez votre cache dans un réseau virtuel, spécifie une adresse IP unique dans un sous-réseau hello pour le cache de hello.</span><span class="sxs-lookup"><span data-stu-id="14674-168">When hosting your cache in a VNET, specifies a unique IP address in hello subnet for hello cache.</span></span> <span data-ttu-id="14674-169">Si n’est fourni, une est choisie pour vous à partir du sous-réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="14674-169">If not provided, one is chosen for you from hello subnet.</span></span> |
| <span data-ttu-id="14674-170">Sous-réseau</span><span class="sxs-lookup"><span data-stu-id="14674-170">Subnet</span></span> |<span data-ttu-id="14674-171">t, --subnet <subnet></span><span class="sxs-lookup"><span data-stu-id="14674-171">t, --subnet <subnet></span></span> |<span data-ttu-id="14674-172">Lorsque vous hébergez votre cache dans un réseau virtuel, spécifie le nom hello du sous-réseau de hello dans le cache de hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="14674-172">When hosting your cache in a VNET, specifies hello name of hello subnet in which toodeploy hello cache.</span></span> |
| <span data-ttu-id="14674-173">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="14674-173">VirtualNetwork</span></span> |<span data-ttu-id="14674-174">-v, --virtual-network <virtual-network></span><span class="sxs-lookup"><span data-stu-id="14674-174">-v, --virtual-network <virtual-network></span></span> |<span data-ttu-id="14674-175">Lors de l’hébergement de votre cache dans un réseau virtuel spécifie hello exacte ID de ressource ARM Hello de toodeploy de réseau virtuel hello redis cache dans.</span><span class="sxs-lookup"><span data-stu-id="14674-175">When hosting your cache in a VNET, specifies hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in.</span></span> <span data-ttu-id="14674-176">Exemple de format : /subscriptions/{ID_abonnement}/resourceGroups/{nom_groupe_ressources}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span><span class="sxs-lookup"><span data-stu-id="14674-176">Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span></span> |
| <span data-ttu-id="14674-177">Abonnement</span><span class="sxs-lookup"><span data-stu-id="14674-177">Subscription</span></span> |<span data-ttu-id="14674-178">-s, --subscription</span><span class="sxs-lookup"><span data-stu-id="14674-178">-s, --subscription</span></span> |<span data-ttu-id="14674-179">identificateur d’abonnement Hello.</span><span class="sxs-lookup"><span data-stu-id="14674-179">hello subscription identifier.</span></span> |

## <a name="see-all-redis-cache-commands"></a><span data-ttu-id="14674-180">Voir toutes les commandes de cache Redis</span><span class="sxs-lookup"><span data-stu-id="14674-180">See all Redis Cache commands</span></span>
<span data-ttu-id="14674-181">toosee toutes les commandes de Cache Redis et leurs paramètres, utilisez hello `azure rediscache -h` commande.</span><span class="sxs-lookup"><span data-stu-id="14674-181">toosee all Redis Cache commands and their parameters, use hello `azure rediscache -h` command.</span></span>

    C:\>azure rediscache -h
    help:    Commands toomanage your Azure Redis Cache(s)
    help:
    help:    Create a Redis Cache
    help:      rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]
    help:
    help:    Delete an existing Redis Cache
    help:      rediscache delete [--name <name> --resource-group <resource-group> ]
    help:
    help:    List all Redis Caches within your Subscription or Resource Group
    help:      rediscache list [options]
    help:
    help:    Show properties of an existing Redis Cache
    help:      rediscache show [--name <name> --resource-group <resource-group>]
    help:
    help:    Change settings of an existing Redis Cache
    help:      rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]
    help:
    help:    Renew hello authentication key for an existing Redis Cache
    help:      rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:      rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help  output usage information
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="create-a-redis-cache"></a><span data-ttu-id="14674-182">Création d’un cache Redis</span><span class="sxs-lookup"><span data-stu-id="14674-182">Create a Redis Cache</span></span>
<span data-ttu-id="14674-183">toocreate un Cache Redis, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="14674-183">toocreate a Redis Cache, use hello following command:</span></span>

    azure rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]

<span data-ttu-id="14674-184">Pour plus d’informations sur cette commande, exécutez hello `azure rediscache create -h` commande.</span><span class="sxs-lookup"><span data-stu-id="14674-184">For more information about this command, run hello `azure rediscache create -h` command.</span></span>

    C:\>azure rediscache create -h
    help:    Create a Redis Cache
    help:
    help:    Usage: rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]
    help:
    help:    Options:
    help:      -h, --help                                               output usage information
    help:      -v, --verbose                                            use verbose output
    help:      -vv                                                      more verbose with debug output
    help:      --json                                                   use json output
    help:      -n, --name <name>                                        Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of hello Resource Group
    help:      -l, --location <location>                                Location toocreate cache.
    help:      -z, --size <size>                                        Size of hello Redis Cache. Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]
    help:      -x, --sku <sku>                                          Redis SKU. Should be one of : [Basic, Standard, Premium]
    help:      -e, --enable-non-ssl-port                                EnableNonSslPort property of hello Redis Cache. Add this flag if you want tooenable hello Non SSL Port for your cache
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here. Format:"{"<key1>":"<value1>","<key2>":"<value2>"}"
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter hello path of a file containing configuration keys and values here. Format for hello file entry: {"<key1>":"<value1>","<key2>":"<value2>"}
    help:      -r, --shard-count <shard-count>                          Number of Shards toocreate on a Premium Cluster Cache
    help:      -v, --virtual-network <virtual-network>                  hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in. Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1
    help:      -t, --subnet <subnet>                                    Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -p, --static-ip <static-ip>                              Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -s, --subscription <id>                                  hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="delete-an-existing-redis-cache"></a><span data-ttu-id="14674-185">Suppression d’un cache Redis</span><span class="sxs-lookup"><span data-stu-id="14674-185">Delete an existing Redis Cache</span></span>
<span data-ttu-id="14674-186">toodelete un Cache Redis, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="14674-186">toodelete a Redis Cache, use hello following command:</span></span>

    azure rediscache delete [--name <name> --resource-group <resource-group> ]

<span data-ttu-id="14674-187">Pour plus d’informations sur cette commande, exécutez hello `azure rediscache delete -h` commande.</span><span class="sxs-lookup"><span data-stu-id="14674-187">For more information about this command, run hello `azure rediscache delete -h` command.</span></span>

    C:\>azure rediscache delete -h
    help:    Delete an existing Redis Cache
    help:
    help:    Usage: rediscache delete [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which hello cache exists
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-all-redis-caches-within-your-subscription-or-resource-group"></a><span data-ttu-id="14674-188">Liste de tous les caches Redis dans votre abonnement ou groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="14674-188">List all Redis Caches within your Subscription or Resource Group</span></span>
<span data-ttu-id="14674-189">utilisation de tous les Caches Redis au sein de votre abonnement ou le groupe de ressources, toolist hello la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="14674-189">toolist all Redis Caches within your Subscription or Resource Group, use hello following command:</span></span>

    azure rediscache list [options]

<span data-ttu-id="14674-190">Pour plus d’informations sur cette commande, exécutez hello `azure rediscache list -h` commande.</span><span class="sxs-lookup"><span data-stu-id="14674-190">For more information about this command, run hello `azure rediscache list -h` command.</span></span>

    C:\>azure rediscache list -h
    help:    List all Redis Caches within your Subscription or Resource Group
    help:
    help:    Usage: rediscache list [options]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="show-properties-of-an-existing-redis-cache"></a><span data-ttu-id="14674-191">Affichage des propriétés d’un cache Redis existant</span><span class="sxs-lookup"><span data-stu-id="14674-191">Show properties of an existing Redis Cache</span></span>
<span data-ttu-id="14674-192">tooshow des propriétés d’un Cache Redis existant, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="14674-192">tooshow properties of an existing Redis Cache, use hello following command:</span></span>

    azure rediscache show [--name <name> --resource-group <resource-group>]

<span data-ttu-id="14674-193">Pour plus d’informations sur cette commande, exécutez hello `azure rediscache show -h` commande.</span><span class="sxs-lookup"><span data-stu-id="14674-193">For more information about this command, run hello `azure rediscache show -h` command.</span></span>

    C:\>azure rediscache show -h
    help:    Show properties of an existing Redis Cache
    help:
    help:    Usage: rediscache show [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

<a name="scale"></a>

## <a name="change-settings-of-an-existing-redis-cache"></a><span data-ttu-id="14674-194">Modification des paramètres d’un cache Redis</span><span class="sxs-lookup"><span data-stu-id="14674-194">Change settings of an existing Redis Cache</span></span>
<span data-ttu-id="14674-195">paramètres toochange d’un Cache Redis existant, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="14674-195">toochange settings of an existing Redis Cache, use hello following command:</span></span>

    azure rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]

<span data-ttu-id="14674-196">Pour plus d’informations sur cette commande, exécutez hello `azure rediscache set -h` commande.</span><span class="sxs-lookup"><span data-stu-id="14674-196">For more information about this command, run hello `azure rediscache set -h` command.</span></span>

    C:\>azure rediscache set -h
    help:    Change settings of an existing Redis Cache
    help:
    help:    Usage: rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]
    help:
    help:    Options:
    help:      -h, --help                                               output usage information
    help:      -v, --verbose                                            use verbose output
    help:      -vv                                                      more verbose with debug output
    help:      --json                                                   use json output
    help:      -n, --name <name>                                        Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of hello Resource Group
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here.
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter hello path of a file containing configuration keys and values here.
    help:      -s, --subscription <subscription>                        hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="renew-hello-authentication-key-for-an-existing-redis-cache"></a><span data-ttu-id="14674-197">Renouveler la clé d’authentification hello pour un Cache Redis existant</span><span class="sxs-lookup"><span data-stu-id="14674-197">Renew hello authentication key for an existing Redis Cache</span></span>
<span data-ttu-id="14674-198">clé d’authentification toorenew hello pour un Redis Cache existant, hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="14674-198">toorenew hello authentication key for an existing Redis Cache, use hello following command:</span></span>

    azure rediscache renew-key [--name <name> --resource-group <resource-group> --key-type <key-type>]

<span data-ttu-id="14674-199">Spécifiez `Primary` ou `Secondary` pour `key-type`.</span><span class="sxs-lookup"><span data-stu-id="14674-199">Specify `Primary` or `Secondary` for `key-type`.</span></span>

<span data-ttu-id="14674-200">Pour plus d’informations sur cette commande, exécutez hello `azure rediscache renew-key -h` commande.</span><span class="sxs-lookup"><span data-stu-id="14674-200">For more information about this command, run hello `azure rediscache renew-key -h` command.</span></span>

    C:\>azure rediscache renew-key -h
    help:    Renew hello authentication key for an existing Redis Cache
    help:
    help:    Usage: rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which cache exists
    help:      -t, --key-type <key-type>              type of key toorenew. Valid values are: 'Primary', 'Secondary'.
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-primary-and-secondary-keys-of-an-existing-redis-cache"></a><span data-ttu-id="14674-201">Liste des clés primaire et secondaire d’un cache Redis</span><span class="sxs-lookup"><span data-stu-id="14674-201">List Primary and Secondary keys of an existing Redis Cache</span></span>
<span data-ttu-id="14674-202">clés primaires et secondaires de toolist d’un Cache Redis existant, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="14674-202">toolist Primary and Secondary keys of an existing Redis Cache, use hello following command:</span></span>

    azure rediscache list-keys [--name <name> --resource-group <resource-group>]

<span data-ttu-id="14674-203">Pour plus d’informations sur cette commande, exécutez hello `azure rediscache list-keys -h` commande.</span><span class="sxs-lookup"><span data-stu-id="14674-203">For more information about this command, run hello `azure rediscache list-keys -h` command.</span></span>

    C:\>azure rediscache list-keys -h
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:
    help:    Usage: rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which Cache exists
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)
