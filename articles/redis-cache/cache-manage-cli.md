---
title: "Gérer le Cache Redis Azure à l’aide d’Azure CLI | Microsoft Docs"
description: "Cette rubrique décrit comment installer l’interface de ligne de commande Azure sur toute plateforme, comment l’utiliser pour se connecter à un compte Azure et comment créer un cache Redis à partir de cette interface."
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
ms.openlocfilehash: ba078a870a3998568170cc197bd6698b97b7fadb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-manage-azure-redis-cache-using-the-azure-command-line-interface-azure-cli"></a><span data-ttu-id="feda8-103">Création et gestion du cache Redis Azure à l’aide de l’interface de ligne de commande Azure (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="feda8-103">How to create and manage Azure Redis Cache using the Azure Command-Line Interface (Azure CLI)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="feda8-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="feda8-104">PowerShell</span></span>](cache-howto-manage-redis-cache-powershell.md)
> * [<span data-ttu-id="feda8-105">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="feda8-105">Azure CLI</span></span>](cache-manage-cli.md)
>
>

<span data-ttu-id="feda8-106">L'interface de ligne de commande Azure est un excellent moyen de gérer votre infrastructure Azure à partir de n'importe quelle plateforme.</span><span class="sxs-lookup"><span data-stu-id="feda8-106">The Azure CLI is a great way to manage your Azure infrastructure from any platform.</span></span> <span data-ttu-id="feda8-107">Cet article montre comment créer et gérer vos instances de cache Redis Azure à l’aide de l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="feda8-107">This article shows you how to create and manage your Azure Redis Cache instances using the Azure CLI.</span></span>

> [!NOTE]
> <span data-ttu-id="feda8-108">Cet article s’applique à une version précédente d’Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="feda8-108">This article applies to a previous version of Azure CLI.</span></span> <span data-ttu-id="feda8-109">Pour les exemples de scripts Azure CLI 2.0 les plus récents, consultez [Exemples de cache Redis Azure CLI](cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="feda8-109">For the latest Azure CLI 2.0 sample scripts, see [Azure CLI Redis cache samples](cli-samples.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="feda8-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="feda8-110">Prerequisites</span></span>
<span data-ttu-id="feda8-111">Pour créer et gérer des instances de cache Redis Azure à l’aide de l’interface de ligne de commande Azure, vous devez procéder comme suit.</span><span class="sxs-lookup"><span data-stu-id="feda8-111">To create and manage Azure Redis Cache instances using Azure CLI, you must complete the following steps.</span></span>

* <span data-ttu-id="feda8-112">Vous devez disposer d’un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="feda8-112">You must have an Azure account.</span></span> <span data-ttu-id="feda8-113">Si vous n’en avez pas, vous pouvez créer un [compte gratuit](https://azure.microsoft.com/pricing/free-trial/) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="feda8-113">If you don't have one, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a few moments.</span></span>
* <span data-ttu-id="feda8-114">[Installer l’interface de ligne de commande Microsoft Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="feda8-114">[Install the Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="feda8-115">Connectez votre installation d’interface de ligne de commande Azure à un compte Azure personnel ou à un compte Azure professionnel ou scolaire, puis connectez-vous à partir de l’interface de ligne de commande Azure à l’aide de la commande `azure login` .</span><span class="sxs-lookup"><span data-stu-id="feda8-115">Connect your Azure CLI installation with a personal Azure account, or with a work or school Azure account, and log in from the Azure CLI using the `azure login` command.</span></span> <span data-ttu-id="feda8-116">Pour comprendre les différences et faire votre choix, consultez [Se connecter à un abonnement Azure à partir de l'interface de ligne de commande Azure (Azure CLI)](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="feda8-116">To understand the differences and choose, see [Connect to an Azure subscription from the Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="feda8-117">Avant d'exécuter les commandes suivantes, basculez l'interface de ligne de commande Azure en mode Gestionnaire de ressources en exécutant la commande `azure config mode arm` .</span><span class="sxs-lookup"><span data-stu-id="feda8-117">Before running any of the following commands, switch the Azure CLI into Resource Manager mode by running the `azure config mode arm` command.</span></span> <span data-ttu-id="feda8-118">Pour plus d’informations, consultez [Utiliser l’interface de ligne de commande Azure pour gérer les ressources et les groupes de ressources Azure](../xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="feda8-118">For more information, see [Use the Azure CLI to manage Azure resources and resource groups](../xplat-cli-azure-resource-manager.md).</span></span>

## <a name="redis-cache-properties"></a><span data-ttu-id="feda8-119">Propriétés du cache Redis</span><span class="sxs-lookup"><span data-stu-id="feda8-119">Redis Cache properties</span></span>
<span data-ttu-id="feda8-120">Les propriétés suivantes sont utilisées lors de la création et de la mise à jour des instances de cache Redis.</span><span class="sxs-lookup"><span data-stu-id="feda8-120">The following properties are used when creating and updating Redis Cache instances.</span></span>

| <span data-ttu-id="feda8-121">Propriété</span><span class="sxs-lookup"><span data-stu-id="feda8-121">Property</span></span> | <span data-ttu-id="feda8-122">Switch</span><span class="sxs-lookup"><span data-stu-id="feda8-122">Switch</span></span> | <span data-ttu-id="feda8-123">Description</span><span class="sxs-lookup"><span data-stu-id="feda8-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="feda8-124">name</span><span class="sxs-lookup"><span data-stu-id="feda8-124">name</span></span> |<span data-ttu-id="feda8-125">-n, --name</span><span class="sxs-lookup"><span data-stu-id="feda8-125">-n, --name</span></span> |<span data-ttu-id="feda8-126">Nom du cache Redis.</span><span class="sxs-lookup"><span data-stu-id="feda8-126">Name of the Redis Cache.</span></span> |
| <span data-ttu-id="feda8-127">resource group</span><span class="sxs-lookup"><span data-stu-id="feda8-127">resource group</span></span> |<span data-ttu-id="feda8-128">-g, --resource-group</span><span class="sxs-lookup"><span data-stu-id="feda8-128">-g, --resource-group</span></span> |<span data-ttu-id="feda8-129">Nom du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="feda8-129">Name of the Resource Group.</span></span> |
| <span data-ttu-id="feda8-130">location</span><span class="sxs-lookup"><span data-stu-id="feda8-130">location</span></span> |<span data-ttu-id="feda8-131">-l, --location</span><span class="sxs-lookup"><span data-stu-id="feda8-131">-l, --location</span></span> |<span data-ttu-id="feda8-132">Emplacement où créer le cache.</span><span class="sxs-lookup"><span data-stu-id="feda8-132">Location to create cache.</span></span> |
| <span data-ttu-id="feda8-133">size</span><span class="sxs-lookup"><span data-stu-id="feda8-133">size</span></span> |<span data-ttu-id="feda8-134">-z, --size</span><span class="sxs-lookup"><span data-stu-id="feda8-134">-z, --size</span></span> |<span data-ttu-id="feda8-135">Taille du cache Redis.</span><span class="sxs-lookup"><span data-stu-id="feda8-135">Size of the Redis Cache.</span></span> <span data-ttu-id="feda8-136">Valeurs valides : [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span><span class="sxs-lookup"><span data-stu-id="feda8-136">Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span></span> |
| <span data-ttu-id="feda8-137">sku</span><span class="sxs-lookup"><span data-stu-id="feda8-137">sku</span></span> |<span data-ttu-id="feda8-138">-x, --sku</span><span class="sxs-lookup"><span data-stu-id="feda8-138">-x, --sku</span></span> |<span data-ttu-id="feda8-139">SKU Redis.</span><span class="sxs-lookup"><span data-stu-id="feda8-139">Redis SKU.</span></span> <span data-ttu-id="feda8-140">Doit être une des valeurs : [De Base, Standard, Premium]</span><span class="sxs-lookup"><span data-stu-id="feda8-140">Should be one of : [Basic, Standard, Premium]</span></span> |
| <span data-ttu-id="feda8-141">enableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="feda8-141">EnableNonSslPort</span></span> |<span data-ttu-id="feda8-142">-e, --enable-non-ssl-port</span><span class="sxs-lookup"><span data-stu-id="feda8-142">-e, --enable-non-ssl-port</span></span> |<span data-ttu-id="feda8-143">Propriété EnableNonSslPort du cache Redis.</span><span class="sxs-lookup"><span data-stu-id="feda8-143">EnableNonSslPort property of the Redis Cache.</span></span> <span data-ttu-id="feda8-144">Ajoutez cet indicateur si vous souhaitez activer le port non-SSL pour votre cache</span><span class="sxs-lookup"><span data-stu-id="feda8-144">Add this flag if you want to enable the Non SSL Port for your cache</span></span> |
| <span data-ttu-id="feda8-145">Configuration de Redis</span><span class="sxs-lookup"><span data-stu-id="feda8-145">Redis Configuration</span></span> |<span data-ttu-id="feda8-146">-c, --redis-configuration</span><span class="sxs-lookup"><span data-stu-id="feda8-146">-c, --redis-configuration</span></span> |<span data-ttu-id="feda8-147">Configuration de Redis.</span><span class="sxs-lookup"><span data-stu-id="feda8-147">Redis Configuration.</span></span> <span data-ttu-id="feda8-148">Entrez ici une chaîne au format JSON des clés et des valeurs de configuration.</span><span class="sxs-lookup"><span data-stu-id="feda8-148">Enter a JSON formatted string of configuration keys and values here.</span></span> <span data-ttu-id="feda8-149">Format :"{"":"","":""}"</span><span class="sxs-lookup"><span data-stu-id="feda8-149">Format:"{"":"","":""}"</span></span> |
| <span data-ttu-id="feda8-150">Configuration de Redis</span><span class="sxs-lookup"><span data-stu-id="feda8-150">Redis Configuration</span></span> |<span data-ttu-id="feda8-151">-f, --redis-configuration-file</span><span class="sxs-lookup"><span data-stu-id="feda8-151">-f, --redis-configuration-file</span></span> |<span data-ttu-id="feda8-152">Configuration de Redis.</span><span class="sxs-lookup"><span data-stu-id="feda8-152">Redis Configuration.</span></span> <span data-ttu-id="feda8-153">Entrez ici le chemin d’un fichier contenant les clés et les valeurs de configuration.</span><span class="sxs-lookup"><span data-stu-id="feda8-153">Enter the path of a file containing configuration keys and values here.</span></span> <span data-ttu-id="feda8-154">Format pour l’entrée du fichier : {"":"","":""}</span><span class="sxs-lookup"><span data-stu-id="feda8-154">Format for the file entry: {"":"","":""}</span></span> |
| <span data-ttu-id="feda8-155">Nombre de partitions</span><span class="sxs-lookup"><span data-stu-id="feda8-155">Shard Count</span></span> |<span data-ttu-id="feda8-156">-r, --shard-count</span><span class="sxs-lookup"><span data-stu-id="feda8-156">-r, --shard-count</span></span> |<span data-ttu-id="feda8-157">Nombre de partitions à créer sur un cache de cluster Premium avec clustering.</span><span class="sxs-lookup"><span data-stu-id="feda8-157">Number of Shards to create on a Premium Cluster Cache with clustering.</span></span> |
| <span data-ttu-id="feda8-158">Réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="feda8-158">Virtual Network</span></span> |<span data-ttu-id="feda8-159">-v, --virtual-network</span><span class="sxs-lookup"><span data-stu-id="feda8-159">-v, --virtual-network</span></span> |<span data-ttu-id="feda8-160">Quand vous hébergez votre cache dans un réseau virtuel, spécifie l’ID de la ressource ARM exacte du réseau virtuel où déployer le cache Redis.</span><span class="sxs-lookup"><span data-stu-id="feda8-160">When hosting your cache in a VNET, specifies the exact ARM resource ID of the virtual network to deploy the redis cache in.</span></span> <span data-ttu-id="feda8-161">Exemple de format : /subscriptions/{ID_abonnement}/resourceGroups/{nom_groupe_ressources}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span><span class="sxs-lookup"><span data-stu-id="feda8-161">Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span></span> |
| <span data-ttu-id="feda8-162">key type</span><span class="sxs-lookup"><span data-stu-id="feda8-162">key type</span></span> |<span data-ttu-id="feda8-163">-t, --key-type</span><span class="sxs-lookup"><span data-stu-id="feda8-163">-t, --key-type</span></span> |<span data-ttu-id="feda8-164">Type de clé à renouveler.</span><span class="sxs-lookup"><span data-stu-id="feda8-164">Type of key to renew.</span></span> <span data-ttu-id="feda8-165">Valeurs valides : [Primary, Secondary]</span><span class="sxs-lookup"><span data-stu-id="feda8-165">Valid values: [Primary, Secondary]</span></span> |
| <span data-ttu-id="feda8-166">StaticIP</span><span class="sxs-lookup"><span data-stu-id="feda8-166">StaticIP</span></span> |<span data-ttu-id="feda8-167">-p, --static-ip <static-ip></span><span class="sxs-lookup"><span data-stu-id="feda8-167">-p, --static-ip <static-ip></span></span> |<span data-ttu-id="feda8-168">Lorsque vous hébergez votre cache dans un réseau virtuel, spécifie une adresse IP unique dans le sous-réseau pour le cache.</span><span class="sxs-lookup"><span data-stu-id="feda8-168">When hosting your cache in a VNET, specifies a unique IP address in the subnet for the cache.</span></span> <span data-ttu-id="feda8-169">Si elle est omise, une adresse IP est choisie pour vous dans le sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="feda8-169">If not provided, one is chosen for you from the subnet.</span></span> |
| <span data-ttu-id="feda8-170">Sous-réseau</span><span class="sxs-lookup"><span data-stu-id="feda8-170">Subnet</span></span> |<span data-ttu-id="feda8-171">t, --subnet <subnet></span><span class="sxs-lookup"><span data-stu-id="feda8-171">t, --subnet <subnet></span></span> |<span data-ttu-id="feda8-172">Lorsque vous hébergez votre cache dans un réseau virtuel, spécifie le nom du sous-réseau dans lequel déployer le cache.</span><span class="sxs-lookup"><span data-stu-id="feda8-172">When hosting your cache in a VNET, specifies the name of the subnet in which to deploy the cache.</span></span> |
| <span data-ttu-id="feda8-173">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="feda8-173">VirtualNetwork</span></span> |<span data-ttu-id="feda8-174">-v, --virtual-network <virtual-network></span><span class="sxs-lookup"><span data-stu-id="feda8-174">-v, --virtual-network <virtual-network></span></span> |<span data-ttu-id="feda8-175">Quand vous hébergez votre cache dans un réseau virtuel, spécifie l’ID de la ressource ARM exacte du réseau virtuel où déployer le cache Redis.</span><span class="sxs-lookup"><span data-stu-id="feda8-175">When hosting your cache in a VNET, specifies the exact ARM resource ID of the virtual network to deploy the redis cache in.</span></span> <span data-ttu-id="feda8-176">Exemple de format : /subscriptions/{ID_abonnement}/resourceGroups/{nom_groupe_ressources}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span><span class="sxs-lookup"><span data-stu-id="feda8-176">Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span></span> |
| <span data-ttu-id="feda8-177">Abonnement</span><span class="sxs-lookup"><span data-stu-id="feda8-177">Subscription</span></span> |<span data-ttu-id="feda8-178">-s, --subscription</span><span class="sxs-lookup"><span data-stu-id="feda8-178">-s, --subscription</span></span> |<span data-ttu-id="feda8-179">Identificateur de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="feda8-179">The subscription identifier.</span></span> |

## <a name="see-all-redis-cache-commands"></a><span data-ttu-id="feda8-180">Voir toutes les commandes de cache Redis</span><span class="sxs-lookup"><span data-stu-id="feda8-180">See all Redis Cache commands</span></span>
<span data-ttu-id="feda8-181">Pour afficher toutes les commandes de cache Redis et leurs paramètres, utilisez la commande `azure rediscache -h` .</span><span class="sxs-lookup"><span data-stu-id="feda8-181">To see all Redis Cache commands and their parameters, use the `azure rediscache -h` command.</span></span>

    C:\>azure rediscache -h
    help:    Commands to manage your Azure Redis Cache(s)
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
    help:    Renew the authentication key for an existing Redis Cache
    help:      rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:      rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help  output usage information
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="create-a-redis-cache"></a><span data-ttu-id="feda8-182">Création d’un cache Redis</span><span class="sxs-lookup"><span data-stu-id="feda8-182">Create a Redis Cache</span></span>
<span data-ttu-id="feda8-183">Pour créer un cache Redis, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="feda8-183">To create a Redis Cache, use the following command:</span></span>

    azure rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]

<span data-ttu-id="feda8-184">Pour plus d’informations sur cette commande, exécutez la commande `azure rediscache create -h` .</span><span class="sxs-lookup"><span data-stu-id="feda8-184">For more information about this command, run the `azure rediscache create -h` command.</span></span>

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
    help:      -n, --name <name>                                        Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of the Resource Group
    help:      -l, --location <location>                                Location to create cache.
    help:      -z, --size <size>                                        Size of the Redis Cache. Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]
    help:      -x, --sku <sku>                                          Redis SKU. Should be one of : [Basic, Standard, Premium]
    help:      -e, --enable-non-ssl-port                                EnableNonSslPort property of the Redis Cache. Add this flag if you want to enable the Non SSL Port for your cache
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here. Format:"{"<key1>":"<value1>","<key2>":"<value2>"}"
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter the path of a file containing configuration keys and values here. Format for the file entry: {"<key1>":"<value1>","<key2>":"<value2>"}
    help:      -r, --shard-count <shard-count>                          Number of Shards to create on a Premium Cluster Cache
    help:      -v, --virtual-network <virtual-network>                  The exact ARM resource ID of the virtual network to deploy the redis cache in. Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1
    help:      -t, --subnet <subnet>                                    Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -p, --static-ip <static-ip>                              Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -s, --subscription <id>                                  the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="delete-an-existing-redis-cache"></a><span data-ttu-id="feda8-185">Suppression d’un cache Redis</span><span class="sxs-lookup"><span data-stu-id="feda8-185">Delete an existing Redis Cache</span></span>
<span data-ttu-id="feda8-186">Pour supprimer un cache Redis, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="feda8-186">To delete a Redis Cache, use the following command:</span></span>

    azure rediscache delete [--name <name> --resource-group <resource-group> ]

<span data-ttu-id="feda8-187">Pour plus d’informations sur cette commande, exécutez la commande `azure rediscache delete -h` .</span><span class="sxs-lookup"><span data-stu-id="feda8-187">For more information about this command, run the `azure rediscache delete -h` command.</span></span>

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
    help:      -n, --name <name>                      Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of the Resource Group under which the cache exists
    help:      -s, --subscription <subscription>      the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-all-redis-caches-within-your-subscription-or-resource-group"></a><span data-ttu-id="feda8-188">Liste de tous les caches Redis dans votre abonnement ou groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="feda8-188">List all Redis Caches within your Subscription or Resource Group</span></span>
<span data-ttu-id="feda8-189">Pour répertorier tous les caches Redis dans votre abonnement ou groupe de ressources, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="feda8-189">To list all Redis Caches within your Subscription or Resource Group, use the following command:</span></span>

    azure rediscache list [options]

<span data-ttu-id="feda8-190">Pour plus d’informations sur cette commande, exécutez la commande `azure rediscache list -h` .</span><span class="sxs-lookup"><span data-stu-id="feda8-190">For more information about this command, run the `azure rediscache list -h` command.</span></span>

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
    help:      -g, --resource-group <resource-group>  Name of the Resource Group
    help:      -s, --subscription <subscription>      the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="show-properties-of-an-existing-redis-cache"></a><span data-ttu-id="feda8-191">Affichage des propriétés d’un cache Redis existant</span><span class="sxs-lookup"><span data-stu-id="feda8-191">Show properties of an existing Redis Cache</span></span>
<span data-ttu-id="feda8-192">Pour afficher les propriétés d’un cache Redis existant, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="feda8-192">To show properties of an existing Redis Cache, use the following command:</span></span>

    azure rediscache show [--name <name> --resource-group <resource-group>]

<span data-ttu-id="feda8-193">Pour plus d’informations sur cette commande, exécutez la commande `azure rediscache show -h` .</span><span class="sxs-lookup"><span data-stu-id="feda8-193">For more information about this command, run the `azure rediscache show -h` command.</span></span>

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
    help:      -n, --name <name>                      Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of the Resource Group
    help:      -s, --subscription <subscription>      the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

<a name="scale"></a>

## <a name="change-settings-of-an-existing-redis-cache"></a><span data-ttu-id="feda8-194">Modification des paramètres d’un cache Redis</span><span class="sxs-lookup"><span data-stu-id="feda8-194">Change settings of an existing Redis Cache</span></span>
<span data-ttu-id="feda8-195">Pour modifier les paramètres d’un cache Redis, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="feda8-195">To change settings of an existing Redis Cache, use the following command:</span></span>

    azure rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]

<span data-ttu-id="feda8-196">Pour plus d’informations sur cette commande, exécutez la commande `azure rediscache set -h` .</span><span class="sxs-lookup"><span data-stu-id="feda8-196">For more information about this command, run the `azure rediscache set -h` command.</span></span>

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
    help:      -n, --name <name>                                        Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of the Resource Group
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here.
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter the path of a file containing configuration keys and values here.
    help:      -s, --subscription <subscription>                        the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="renew-the-authentication-key-for-an-existing-redis-cache"></a><span data-ttu-id="feda8-197">Renouvellement de la clé d’authentification pour un cache Redis</span><span class="sxs-lookup"><span data-stu-id="feda8-197">Renew the authentication key for an existing Redis Cache</span></span>
<span data-ttu-id="feda8-198">Pour renouveler la clé d’authentification pour un cache Redis, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="feda8-198">To renew the authentication key for an existing Redis Cache, use the following command:</span></span>

    azure rediscache renew-key [--name <name> --resource-group <resource-group> --key-type <key-type>]

<span data-ttu-id="feda8-199">Spécifiez `Primary` ou `Secondary` pour `key-type`.</span><span class="sxs-lookup"><span data-stu-id="feda8-199">Specify `Primary` or `Secondary` for `key-type`.</span></span>

<span data-ttu-id="feda8-200">Pour plus d’informations sur cette commande, exécutez la commande `azure rediscache renew-key -h`.</span><span class="sxs-lookup"><span data-stu-id="feda8-200">For more information about this command, run the `azure rediscache renew-key -h` command.</span></span>

    C:\>azure rediscache renew-key -h
    help:    Renew the authentication key for an existing Redis Cache
    help:
    help:    Usage: rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of the Resource Group under which cache exists
    help:      -t, --key-type <key-type>              type of key to renew. Valid values are: 'Primary', 'Secondary'.
    help:      -s, --subscription <subscription>      the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-primary-and-secondary-keys-of-an-existing-redis-cache"></a><span data-ttu-id="feda8-201">Liste des clés primaire et secondaire d’un cache Redis</span><span class="sxs-lookup"><span data-stu-id="feda8-201">List Primary and Secondary keys of an existing Redis Cache</span></span>
<span data-ttu-id="feda8-202">Pour répertorier les clés primaire et secondaire d’un cache Redis, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="feda8-202">To list Primary and Secondary keys of an existing Redis Cache, use the following command:</span></span>

    azure rediscache list-keys [--name <name> --resource-group <resource-group>]

<span data-ttu-id="feda8-203">Pour plus d’informations sur cette commande, exécutez la commande `azure rediscache list-keys -h` .</span><span class="sxs-lookup"><span data-stu-id="feda8-203">For more information about this command, run the `azure rediscache list-keys -h` command.</span></span>

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
    help:      -n, --name <name>                      Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of the Resource Group under which Cache exists
    help:      -s, --subscription <subscription>      the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)
