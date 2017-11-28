---
title: Gestion du Cache Redis Azure avec Azure PowerShell | Microsoft Docs
description: "Découvrez comment effectuer des tâches administratives pour le Cache Redis Azure à l'aide d'Azure PowerShell."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 1136efe5-1e33-4d91-bb49-c8e2a6dca475
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: sdanie
ms.openlocfilehash: 0a5c95eab3fd01f611fc049e80c5c506857e0b81
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="manage-azure-redis-cache-with-azure-powershell"></a><span data-ttu-id="370c9-103">Gestion du Cache Redis Azure avec Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="370c9-103">Manage Azure Redis Cache with Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="370c9-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="370c9-104">PowerShell</span></span>](cache-howto-manage-redis-cache-powershell.md)
> * [<span data-ttu-id="370c9-105">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="370c9-105">Azure CLI</span></span>](cache-manage-cli.md)
> 
> 

<span data-ttu-id="370c9-106">Cette rubrique décrit comment effectuer des tâches courantes telles que la création, la mise à jour et la mise à l’échelle de vos instances de cache Redis Azure, comment régénérer les clés d'accès et comment afficher des informations sur vos caches.</span><span class="sxs-lookup"><span data-stu-id="370c9-106">This topic shows you how to perform common tasks such as create, update, and scale your Azure Redis Cache instances, how to regenerate access keys, and how to view information about your caches.</span></span> <span data-ttu-id="370c9-107">Pour obtenir une liste complète des applets de commande PowerShell de cache Redis Azure, consultez [Applets de commande de cache Redis Azure](https://msdn.microsoft.com/library/azure/mt634513.aspx).</span><span class="sxs-lookup"><span data-stu-id="370c9-107">For a complete list of Azure Redis Cache PowerShell cmdlets, see [Azure Redis Cache cmdlets](https://msdn.microsoft.com/library/azure/mt634513.aspx).</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="370c9-108">Pour en savoir plus sur le modèle de déploiement Classic, consultez [Déploiement Azure Resource Manager et déploiement Classic : comprendre les modèles de déploiement et l’état de vos ressources](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics).</span><span class="sxs-lookup"><span data-stu-id="370c9-108">For more information about the classic deployment model, see [Azure Resource Manager vs. classic deployment: Understand deployment models and the state of your resources](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="370c9-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="370c9-109">Prerequisites</span></span>
<span data-ttu-id="370c9-110">Si vous avez déjà installé Azure PowerShell, vous devez disposer d’Azure PowerShell version 1.0.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="370c9-110">If you have already installed Azure PowerShell, you must have Azure PowerShell version 1.0.0 or later.</span></span> <span data-ttu-id="370c9-111">Vous pouvez vérifier la version d’Azure PowerShell que vous avez installée à l’aide de cette commande à l’invite de commandes Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="370c9-111">You can check the version of Azure PowerShell that you have installed with this command at the Azure PowerShell command prompt.</span></span>

    Get-Module azure | format-table version


<span data-ttu-id="370c9-112">Tout d’abord, vous devez vous connecter à Azure avec cette commande.</span><span class="sxs-lookup"><span data-stu-id="370c9-112">First, you must log in to Azure with this command.</span></span>

    Login-AzureRmAccount

<span data-ttu-id="370c9-113">Spécifiez l'adresse de messagerie électronique et le mot de passe de votre compte Azure dans la boîte de dialogue de connexion à Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="370c9-113">Specify the email address of your Azure account and its password in the Microsoft Azure sign-in dialog.</span></span>

<span data-ttu-id="370c9-114">Ensuite, si vous avez plusieurs abonnements, vous devez sélectionner l’abonnement Azure à utiliser.</span><span class="sxs-lookup"><span data-stu-id="370c9-114">Next, if you have multiple Azure subscriptions, you need to set your Azure subscription.</span></span> <span data-ttu-id="370c9-115">Pour afficher une liste de vos abonnements en cours, exécutez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="370c9-115">To see a list of your current subscriptions, run this command.</span></span>

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="370c9-116">Pour spécifier l’abonnement, exécutez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="370c9-116">To specify the subscription, run the following command.</span></span> <span data-ttu-id="370c9-117">Dans l’exemple suivant, le nom de l’abonnement est `ContosoSubscription`.</span><span class="sxs-lookup"><span data-stu-id="370c9-117">In the following example, the subscription name is `ContosoSubscription`.</span></span>

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

<span data-ttu-id="370c9-118">Avant de pouvoir utiliser Windows PowerShell avec Azure Resource Manager, vous devez disposer des composants suivants :</span><span class="sxs-lookup"><span data-stu-id="370c9-118">Before you can use Windows PowerShell with Azure Resource Manager, you need the following:</span></span>

* <span data-ttu-id="370c9-119">Windows PowerShell, version 3.0 ou 4.0.</span><span class="sxs-lookup"><span data-stu-id="370c9-119">Windows PowerShell, Version 3.0 or 4.0.</span></span> <span data-ttu-id="370c9-120">Pour trouver la version de Windows PowerShell, tapez : `$PSVersionTable` et vérifiez que la valeur de `PSVersion` est 3.0 ou 4.0.</span><span class="sxs-lookup"><span data-stu-id="370c9-120">To find the version of Windows PowerShell, type:`$PSVersionTable` and verify the value of `PSVersion` is 3.0 or 4.0.</span></span> <span data-ttu-id="370c9-121">Pour installer une version compatible, voir la section [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) ou [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span><span class="sxs-lookup"><span data-stu-id="370c9-121">To install a compatible version, see [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) or [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span></span>

<span data-ttu-id="370c9-122">Pour accéder à l’aide détaillée d’un applet de commande présenté dans ce didacticiel, utilisez l’applet de commande Get-Help.</span><span class="sxs-lookup"><span data-stu-id="370c9-122">To get detailed help for any cmdlet you see in this tutorial, use the Get-Help cmdlet.</span></span>

    Get-Help <cmdlet-name> -Detailed

<span data-ttu-id="370c9-123">Par exemple, pour obtenir de l’aide sur l’applet de commande `New-AzureRmRedisCache` , tapez :</span><span class="sxs-lookup"><span data-stu-id="370c9-123">For example, to get help for the `New-AzureRmRedisCache` cmdlet, type:</span></span>

    Get-Help New-AzureRmRedisCache -Detailed

### <a name="how-to-connect-to-other-clouds"></a><span data-ttu-id="370c9-124">Guide pratique pour se connecter à d’autres clouds</span><span class="sxs-lookup"><span data-stu-id="370c9-124">How to connect to other clouds</span></span>
<span data-ttu-id="370c9-125">Par défaut, l’environnement Azure est `AzureCloud`, qui représente l’instance globale du cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="370c9-125">By default the Azure environment is `AzureCloud`, which represents the global Azure cloud instance.</span></span> <span data-ttu-id="370c9-126">Pour vous connecter à une autre instance, utilisez la commande `Add-AzureRmAccount` avec le commutateur de ligne de commande `-Environment` ou -`EnvironmentName` accompagné de l’environnement ou du nom d’environnement désiré.</span><span class="sxs-lookup"><span data-stu-id="370c9-126">To connect to a different instance, use the `Add-AzureRmAccount` command with the `-Environment` or -`EnvironmentName` command line switch with the desired environment or environment name.</span></span>

<span data-ttu-id="370c9-127">Pour afficher la liste des environnements disponibles, exécutez l’applet de commande `Get-AzureRmEnvironment` .</span><span class="sxs-lookup"><span data-stu-id="370c9-127">To see the list of available environments, run the `Get-AzureRmEnvironment` cmdlet.</span></span>

### <a name="to-connect-to-the-azure-government-cloud"></a><span data-ttu-id="370c9-128">Pour vous connecter au cloud Azure Government</span><span class="sxs-lookup"><span data-stu-id="370c9-128">To connect to the Azure Government Cloud</span></span>
<span data-ttu-id="370c9-129">Pour vous connecter au cloud Azure Government, utilisez une des commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="370c9-129">To connect to the Azure Government Cloud, use one of the following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureUSGovernment

<span data-ttu-id="370c9-130">ou</span><span class="sxs-lookup"><span data-stu-id="370c9-130">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureUSGovernment)

<span data-ttu-id="370c9-131">Pour créer un cache dans le cloud Azure Government, utilisez un des emplacements suivants.</span><span class="sxs-lookup"><span data-stu-id="370c9-131">To create a cache in the Azure Government Cloud, use one of the following locations.</span></span>

* <span data-ttu-id="370c9-132">Gouvernement américain - Virginie</span><span class="sxs-lookup"><span data-stu-id="370c9-132">USGov Virginia</span></span>
* <span data-ttu-id="370c9-133">USGov Iowa</span><span class="sxs-lookup"><span data-stu-id="370c9-133">USGov Iowa</span></span>

<span data-ttu-id="370c9-134">Pour plus d’informations sur le cloud Azure Government, voir [Microsoft Azure Government](https://azure.microsoft.com/features/gov/) et [Guide du développeur Microsoft Azure Government](../azure-government-developer-guide.md).</span><span class="sxs-lookup"><span data-stu-id="370c9-134">For more information about the Azure Government Cloud, see [Microsoft Azure Government](https://azure.microsoft.com/features/gov/) and [Microsoft Azure Government Developer Guide](../azure-government-developer-guide.md).</span></span>

### <a name="to-connect-to-the-azure-china-cloud"></a><span data-ttu-id="370c9-135">Pour vous connecter au cloud Azure de Chine</span><span class="sxs-lookup"><span data-stu-id="370c9-135">To connect to the Azure China Cloud</span></span>
<span data-ttu-id="370c9-136">Pour vous connecter au cloud Azure de Chine, utilisez une des commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="370c9-136">To connect to the Azure China Cloud, use one of the following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureChinaCloud

<span data-ttu-id="370c9-137">ou</span><span class="sxs-lookup"><span data-stu-id="370c9-137">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureChinaCloud)

<span data-ttu-id="370c9-138">Pour créer un cache dans le cloud Azure de Chine, utilisez un des emplacements suivants.</span><span class="sxs-lookup"><span data-stu-id="370c9-138">To create a cache in the Azure China Cloud, use one of the following locations.</span></span>

* <span data-ttu-id="370c9-139">Chine orientale</span><span class="sxs-lookup"><span data-stu-id="370c9-139">China East</span></span>
* <span data-ttu-id="370c9-140">Chine du Nord</span><span class="sxs-lookup"><span data-stu-id="370c9-140">China North</span></span>

<span data-ttu-id="370c9-141">Pour plus d’informations sur le cloud Azure de Chine, consultez [AzureChinaCloud pour Azure géré par 21Vianet en Chine](http://www.windowsazure.cn/).</span><span class="sxs-lookup"><span data-stu-id="370c9-141">For more information about the Azure China Cloud, see [AzureChinaCloud for Azure operated by 21Vianet in China](http://www.windowsazure.cn/).</span></span>

### <a name="to-connect-to-microsoft-azure-germany"></a><span data-ttu-id="370c9-142">Pour se connecter à Microsoft Azure Allemagne</span><span class="sxs-lookup"><span data-stu-id="370c9-142">To connect to Microsoft Azure Germany</span></span>
<span data-ttu-id="370c9-143">Pour vous connecter à Microsoft Azure Allemagne, utilisez une des commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="370c9-143">To connect to Microsoft Azure Germany, use one of the following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureGermanCloud


<span data-ttu-id="370c9-144">ou</span><span class="sxs-lookup"><span data-stu-id="370c9-144">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureGermanCloud)

<span data-ttu-id="370c9-145">Pour créer un cache dans Microsoft Azure Allemagne, utilisez un des emplacements suivants.</span><span class="sxs-lookup"><span data-stu-id="370c9-145">To create a cache in Microsoft Azure Germany, use one of the following locations.</span></span>

* <span data-ttu-id="370c9-146">Centre de l’Allemagne</span><span class="sxs-lookup"><span data-stu-id="370c9-146">Germany Central</span></span>
* <span data-ttu-id="370c9-147">Nord-Est de l’Allemagne</span><span class="sxs-lookup"><span data-stu-id="370c9-147">Germany Northeast</span></span>

<span data-ttu-id="370c9-148">Pour plus d’informations sur Microsoft Azure Allemagne, consultez [Microsoft Azure Allemagne](https://azure.microsoft.com/overview/clouds/germany/).</span><span class="sxs-lookup"><span data-stu-id="370c9-148">For more information about Microsoft Azure Germany, see [Microsoft Azure Germany](https://azure.microsoft.com/overview/clouds/germany/).</span></span>

### <a name="properties-used-for-azure-redis-cache-powershell"></a><span data-ttu-id="370c9-149">Propriétés utilisées pour le cache Redis Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="370c9-149">Properties used for Azure Redis Cache PowerShell</span></span>
<span data-ttu-id="370c9-150">Le tableau suivant contient les propriétés et les descriptions pour les paramètres fréquemment utilisés lors de la création et de la gestion de vos instances de cache Redis Azure avec Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="370c9-150">The following table contains properties and descriptions for commonly used parameters when creating and managing your Azure Redis Cache instances using Azure PowerShell.</span></span>

| <span data-ttu-id="370c9-151">Paramètre</span><span class="sxs-lookup"><span data-stu-id="370c9-151">Parameter</span></span> | <span data-ttu-id="370c9-152">Description</span><span class="sxs-lookup"><span data-stu-id="370c9-152">Description</span></span> | <span data-ttu-id="370c9-153">Default</span><span class="sxs-lookup"><span data-stu-id="370c9-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="370c9-154">Name</span><span class="sxs-lookup"><span data-stu-id="370c9-154">Name</span></span> |<span data-ttu-id="370c9-155">Nom du cache</span><span class="sxs-lookup"><span data-stu-id="370c9-155">Name of the cache</span></span> | |
| <span data-ttu-id="370c9-156">Emplacement</span><span class="sxs-lookup"><span data-stu-id="370c9-156">Location</span></span> |<span data-ttu-id="370c9-157">Emplacement du cache</span><span class="sxs-lookup"><span data-stu-id="370c9-157">Location of the cache</span></span> | |
| <span data-ttu-id="370c9-158">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="370c9-158">ResourceGroupName</span></span> |<span data-ttu-id="370c9-159">Nom du groupe de ressources dans lequel créer le cache</span><span class="sxs-lookup"><span data-stu-id="370c9-159">Resource group name in which to create the cache</span></span> | |
| <span data-ttu-id="370c9-160">Taille</span><span class="sxs-lookup"><span data-stu-id="370c9-160">Size</span></span> |<span data-ttu-id="370c9-161">Taille du cache.</span><span class="sxs-lookup"><span data-stu-id="370c9-161">The size of the cache.</span></span> <span data-ttu-id="370c9-162">Les valeurs valides sont : P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250 Mo, 1 Go, 2,5 Go, 6 Go, 13 Go, 26 Go, 53 Go</span><span class="sxs-lookup"><span data-stu-id="370c9-162">Valid values are: P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB</span></span> |<span data-ttu-id="370c9-163">1 Go</span><span class="sxs-lookup"><span data-stu-id="370c9-163">1GB</span></span> |
| <span data-ttu-id="370c9-164">Nombre de partitions</span><span class="sxs-lookup"><span data-stu-id="370c9-164">ShardCount</span></span> |<span data-ttu-id="370c9-165">Le nombre de partitions à créer lors de la création d'un cache premium avec le clustering activé.</span><span class="sxs-lookup"><span data-stu-id="370c9-165">The number of shards to create when creating a premium cache with clustering enabled.</span></span> <span data-ttu-id="370c9-166">Les valeurs valides sont : 1, 2, 3, 4, 5, 6, 7, 8, 9, 10</span><span class="sxs-lookup"><span data-stu-id="370c9-166">Valid values are: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10</span></span> | |
| <span data-ttu-id="370c9-167">SKU</span><span class="sxs-lookup"><span data-stu-id="370c9-167">SKU</span></span> |<span data-ttu-id="370c9-168">Spécifie la référence du cache.</span><span class="sxs-lookup"><span data-stu-id="370c9-168">Specifies the SKU of the cache.</span></span> <span data-ttu-id="370c9-169">Les valeurs valides sont : De base, Standard, Premium</span><span class="sxs-lookup"><span data-stu-id="370c9-169">Valid values are: Basic, Standard, Premium</span></span> |<span data-ttu-id="370c9-170">Standard</span><span class="sxs-lookup"><span data-stu-id="370c9-170">Standard</span></span> |
| <span data-ttu-id="370c9-171">RedisConfiguration</span><span class="sxs-lookup"><span data-stu-id="370c9-171">RedisConfiguration</span></span> |<span data-ttu-id="370c9-172">Spécifie les paramètres de configuration de Redis.</span><span class="sxs-lookup"><span data-stu-id="370c9-172">Specifies Redis configuration settings.</span></span> <span data-ttu-id="370c9-173">Pour plus d’informations sur chaque paramètre, consultez le tableau [Propriétés RedisConfiguration](#redisconfiguration-properties) suivant.</span><span class="sxs-lookup"><span data-stu-id="370c9-173">For details on each setting, see the following [RedisConfiguration properties](#redisconfiguration-properties) table.</span></span> | |
| <span data-ttu-id="370c9-174">enableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="370c9-174">EnableNonSslPort</span></span> |<span data-ttu-id="370c9-175">Indique si le port non SSL est activé.</span><span class="sxs-lookup"><span data-stu-id="370c9-175">Indicates whether the non-SSL port is enabled.</span></span> |<span data-ttu-id="370c9-176">False</span><span class="sxs-lookup"><span data-stu-id="370c9-176">False</span></span> |
| <span data-ttu-id="370c9-177">MaxMemoryPolicy</span><span class="sxs-lookup"><span data-stu-id="370c9-177">MaxMemoryPolicy</span></span> |<span data-ttu-id="370c9-178">Ce paramètre est obsolète. Utilisez RedisConfiguration à la place.</span><span class="sxs-lookup"><span data-stu-id="370c9-178">This parameter has been deprecated - use RedisConfiguration instead.</span></span> | |
| <span data-ttu-id="370c9-179">StaticIP</span><span class="sxs-lookup"><span data-stu-id="370c9-179">StaticIP</span></span> |<span data-ttu-id="370c9-180">Lorsque vous hébergez votre cache dans un réseau virtuel, spécifie une adresse IP unique dans le sous-réseau pour le cache.</span><span class="sxs-lookup"><span data-stu-id="370c9-180">When hosting your cache in a VNET, specifies a unique IP address in the subnet for the cache.</span></span> <span data-ttu-id="370c9-181">Si elle est omise, une adresse IP est choisie pour vous dans le sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="370c9-181">If not provided, one is chosen for you from the subnet.</span></span> | |
| <span data-ttu-id="370c9-182">Sous-réseau</span><span class="sxs-lookup"><span data-stu-id="370c9-182">Subnet</span></span> |<span data-ttu-id="370c9-183">Lorsque vous hébergez votre cache dans un réseau virtuel, spécifie le nom du sous-réseau dans lequel déployer le cache.</span><span class="sxs-lookup"><span data-stu-id="370c9-183">When hosting your cache in a VNET, specifies the name of the subnet in which to deploy the cache.</span></span> | |
| <span data-ttu-id="370c9-184">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="370c9-184">VirtualNetwork</span></span> |<span data-ttu-id="370c9-185">Lorsque vous hébergez votre cache dans un réseau virtuel, spécifie l’ID de ressource du réseau virtuel dans lequel déployer le cache.</span><span class="sxs-lookup"><span data-stu-id="370c9-185">When hosting your cache in a VNET, specifies the resource ID of the VNET in which to deploy the cache.</span></span> | |
| <span data-ttu-id="370c9-186">KeyType</span><span class="sxs-lookup"><span data-stu-id="370c9-186">KeyType</span></span> |<span data-ttu-id="370c9-187">Spécifie la clé d'accès à régénérer lors du renouvellement des clés d'accès.</span><span class="sxs-lookup"><span data-stu-id="370c9-187">Specifies which access key to regenerate when renewing access keys.</span></span> <span data-ttu-id="370c9-188">Les valeurs valides sont : Primaire, Secondaire</span><span class="sxs-lookup"><span data-stu-id="370c9-188">Valid values are: Primary, Secondary</span></span> | |

### <a name="redisconfiguration-properties"></a><span data-ttu-id="370c9-189">Propriétés RedisConfiguration</span><span class="sxs-lookup"><span data-stu-id="370c9-189">RedisConfiguration properties</span></span>
| <span data-ttu-id="370c9-190">Propriété</span><span class="sxs-lookup"><span data-stu-id="370c9-190">Property</span></span> | <span data-ttu-id="370c9-191">Description</span><span class="sxs-lookup"><span data-stu-id="370c9-191">Description</span></span> | <span data-ttu-id="370c9-192">Niveaux de tarification</span><span class="sxs-lookup"><span data-stu-id="370c9-192">Pricing tiers</span></span> |
| --- | --- | --- |
| <span data-ttu-id="370c9-193">rdb-backup-enabled</span><span class="sxs-lookup"><span data-stu-id="370c9-193">rdb-backup-enabled</span></span> |<span data-ttu-id="370c9-194">Indique si [la persistance des données Redis](cache-how-to-premium-persistence.md) est activée</span><span class="sxs-lookup"><span data-stu-id="370c9-194">Whether [Redis data persistence](cache-how-to-premium-persistence.md) is enabled</span></span> |<span data-ttu-id="370c9-195">Premium uniquement</span><span class="sxs-lookup"><span data-stu-id="370c9-195">Premium only</span></span> |
| <span data-ttu-id="370c9-196">rdb-storage-connection-string</span><span class="sxs-lookup"><span data-stu-id="370c9-196">rdb-storage-connection-string</span></span> |<span data-ttu-id="370c9-197">La chaîne de connexion au compte de stockage pour [la persistance des données Redis](cache-how-to-premium-persistence.md)</span><span class="sxs-lookup"><span data-stu-id="370c9-197">The connection string to the storage account for [Redis data persistence](cache-how-to-premium-persistence.md)</span></span> |<span data-ttu-id="370c9-198">Premium uniquement</span><span class="sxs-lookup"><span data-stu-id="370c9-198">Premium only</span></span> |
| <span data-ttu-id="370c9-199">rdb-backup-frequency</span><span class="sxs-lookup"><span data-stu-id="370c9-199">rdb-backup-frequency</span></span> |<span data-ttu-id="370c9-200">La fréquence de sauvegarde pour [la persistance des données Redis](cache-how-to-premium-persistence.md)</span><span class="sxs-lookup"><span data-stu-id="370c9-200">The backup frequency for [Redis data persistence](cache-how-to-premium-persistence.md)</span></span> |<span data-ttu-id="370c9-201">Premium uniquement</span><span class="sxs-lookup"><span data-stu-id="370c9-201">Premium only</span></span> |
| <span data-ttu-id="370c9-202">maxmemory-reserved</span><span class="sxs-lookup"><span data-stu-id="370c9-202">maxmemory-reserved</span></span> |<span data-ttu-id="370c9-203">Configure la [mémoire réservée](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) aux processus sans mise en cache</span><span class="sxs-lookup"><span data-stu-id="370c9-203">Configures the [memory reserved](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) for non-cache processes</span></span> |<span data-ttu-id="370c9-204">Standard et Premium</span><span class="sxs-lookup"><span data-stu-id="370c9-204">Standard and Premium</span></span> |
| <span data-ttu-id="370c9-205">maxmemory-policy</span><span class="sxs-lookup"><span data-stu-id="370c9-205">maxmemory-policy</span></span> |<span data-ttu-id="370c9-206">Configure la [stratégie d’éviction](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) pour le cache</span><span class="sxs-lookup"><span data-stu-id="370c9-206">Configures the [eviction policy](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) for the cache</span></span> |<span data-ttu-id="370c9-207">Tous les niveaux de tarification</span><span class="sxs-lookup"><span data-stu-id="370c9-207">All pricing tiers</span></span> |
| <span data-ttu-id="370c9-208">notify-keyspace-events</span><span class="sxs-lookup"><span data-stu-id="370c9-208">notify-keyspace-events</span></span> |<span data-ttu-id="370c9-209">Configure les [notifications d’espace de clés](cache-configure.md#keyspace-notifications-advanced-settings)</span><span class="sxs-lookup"><span data-stu-id="370c9-209">Configures [keyspace notifications](cache-configure.md#keyspace-notifications-advanced-settings)</span></span> |<span data-ttu-id="370c9-210">Standard et Premium</span><span class="sxs-lookup"><span data-stu-id="370c9-210">Standard and Premium</span></span> |
| <span data-ttu-id="370c9-211">hash-max-ziplist-entries</span><span class="sxs-lookup"><span data-stu-id="370c9-211">hash-max-ziplist-entries</span></span> |<span data-ttu-id="370c9-212">Configure [l’optimisation de la mémoire](http://redis.io/topics/memory-optimization) pour les petites quantités de types de données agrégées</span><span class="sxs-lookup"><span data-stu-id="370c9-212">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="370c9-213">Standard et Premium</span><span class="sxs-lookup"><span data-stu-id="370c9-213">Standard and Premium</span></span> |
| <span data-ttu-id="370c9-214">hash-max-ziplist-value</span><span class="sxs-lookup"><span data-stu-id="370c9-214">hash-max-ziplist-value</span></span> |<span data-ttu-id="370c9-215">Configure [l’optimisation de la mémoire](http://redis.io/topics/memory-optimization) pour les petites quantités de types de données agrégées</span><span class="sxs-lookup"><span data-stu-id="370c9-215">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="370c9-216">Standard et Premium</span><span class="sxs-lookup"><span data-stu-id="370c9-216">Standard and Premium</span></span> |
| <span data-ttu-id="370c9-217">set-max-intset-entries</span><span class="sxs-lookup"><span data-stu-id="370c9-217">set-max-intset-entries</span></span> |<span data-ttu-id="370c9-218">Configure [l’optimisation de la mémoire](http://redis.io/topics/memory-optimization) pour les petites quantités de types de données agrégées</span><span class="sxs-lookup"><span data-stu-id="370c9-218">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="370c9-219">Standard et Premium</span><span class="sxs-lookup"><span data-stu-id="370c9-219">Standard and Premium</span></span> |
| <span data-ttu-id="370c9-220">zset-max-ziplist-entries</span><span class="sxs-lookup"><span data-stu-id="370c9-220">zset-max-ziplist-entries</span></span> |<span data-ttu-id="370c9-221">Configure [l’optimisation de la mémoire](http://redis.io/topics/memory-optimization) pour les petites quantités de types de données agrégées</span><span class="sxs-lookup"><span data-stu-id="370c9-221">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="370c9-222">Standard et Premium</span><span class="sxs-lookup"><span data-stu-id="370c9-222">Standard and Premium</span></span> |
| <span data-ttu-id="370c9-223">zset-max-ziplist-value</span><span class="sxs-lookup"><span data-stu-id="370c9-223">zset-max-ziplist-value</span></span> |<span data-ttu-id="370c9-224">Configure [l’optimisation de la mémoire](http://redis.io/topics/memory-optimization) pour les petites quantités de types de données agrégées</span><span class="sxs-lookup"><span data-stu-id="370c9-224">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="370c9-225">Standard et Premium</span><span class="sxs-lookup"><span data-stu-id="370c9-225">Standard and Premium</span></span> |
| <span data-ttu-id="370c9-226">bases de données</span><span class="sxs-lookup"><span data-stu-id="370c9-226">databases</span></span> |<span data-ttu-id="370c9-227">Configure le nombre de bases de données.</span><span class="sxs-lookup"><span data-stu-id="370c9-227">Configures the number of databases.</span></span> <span data-ttu-id="370c9-228">Cette propriété ne peut être configurée qu’au moment de la création du cache.</span><span class="sxs-lookup"><span data-stu-id="370c9-228">This property can be configured only at cache creation.</span></span> |<span data-ttu-id="370c9-229">Standard et Premium</span><span class="sxs-lookup"><span data-stu-id="370c9-229">Standard and Premium</span></span> |

## <a name="to-create-a-redis-cache"></a><span data-ttu-id="370c9-230">Création d’un cache Redis</span><span class="sxs-lookup"><span data-stu-id="370c9-230">To create a Redis Cache</span></span>
<span data-ttu-id="370c9-231">Les nouvelles instances de cache Redis Azure sont créées à l’aide de l’applet de commande [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) .</span><span class="sxs-lookup"><span data-stu-id="370c9-231">New Azure Redis Cache instances are created using the [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="370c9-232">La première fois que vous créez un cache Redis dans un abonnement à l’aide du portail Azure, le portail inscrit l’espace de noms `Microsoft.Cache` pour cet abonnement.</span><span class="sxs-lookup"><span data-stu-id="370c9-232">The first time you create a Redis cache in a subscription using the Azure portal, the portal registers the `Microsoft.Cache` namespace for that subscription.</span></span> <span data-ttu-id="370c9-233">Si vous tentez de créer le premier cache Redis dans un abonnement à l’aide de PowerShell, vous devez d’abord inscrire cet espace de noms à l’aide de la commande suivante. Dans le cas contraire, les applets de commande comme `New-AzureRmRedisCache` et `Get-AzureRmRedisCache` échoueront.</span><span class="sxs-lookup"><span data-stu-id="370c9-233">If you attempt to create the first Redis cache in a subscription using PowerShell, you must first register that namespace using the following command; otherwise cmdlets such as `New-AzureRmRedisCache` and `Get-AzureRmRedisCache` fail.</span></span>
> 
> `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Cache"`
> 
> 

<span data-ttu-id="370c9-234">Pour afficher la liste des paramètres disponibles et leurs descriptions pour `New-AzureRmRedisCache`, exécutez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="370c9-234">To see a list of available parameters and their descriptions for `New-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help New-AzureRmRedisCache -detailed

    NAME
        New-AzureRmRedisCache

    SYNOPSIS
        Creates a new redis cache.


    SYNTAX
        New-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Location <String> [-RedisVersion <String>]
        [-Size <String>] [-Sku <String>] [-MaxMemoryPolicy <String>] [-RedisConfiguration <Hashtable>] [-EnableNonSslPort
        <Boolean>] [-ShardCount <Integer>] [-VirtualNetwork <String>] [-Subnet <String>] [-StaticIP <String>]
        [<CommonParameters>]


    DESCRIPTION
        The New-AzureRmRedisCache cmdlet creates a new redis cache.


    PARAMETERS
        -Name <String>
            Name of the redis cache to create.

        -ResourceGroupName <String>
            Name of resource group in which to create the redis cache.

        -Location <String>
            Location in which to create the redis cache.

        -RedisVersion <String>
            RedisVersion is deprecated and will be removed in future release.

        -Size <String>
            Size of the redis cache. The default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. The default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            The 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting to set
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value, databases.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. If no value is provided, the default value is false and the
            non-SSL port will be disabled. Possible values are true and false.

        -ShardCount <Integer>
            The number of shards to create on a Premium Cluster Cache.

        -VirtualNetwork <String>
            The exact ARM resource ID of the virtual network to deploy the redis cache in. Example format: /subscriptions/{
            subid}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicNetwork/VirtualNetworks/{vnetName}

        -Subnet <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        -StaticIP <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="370c9-235">Pour créer un cache avec les paramètres par défaut, exécutez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="370c9-235">To create a cache with default parameters, run the following command.</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US"

<span data-ttu-id="370c9-236">`ResourceGroupName`, `Name`, et `Location` sont des paramètres obligatoires, mais les autres sont facultatifs et disposent de valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="370c9-236">`ResourceGroupName`, `Name`, and `Location` are required parameters, but the rest are optional and have default values.</span></span> <span data-ttu-id="370c9-237">L’exécution de la commande précédente crée une instance de cache Redis Azure avec référence standard avec le nom, l’emplacement et le groupe de ressources spécifiés, dont la taille est 1 Go avec le port non SSL désactivé.</span><span class="sxs-lookup"><span data-stu-id="370c9-237">Running the previous command creates a Standard SKU Azure Redis Cache instance with the specified name, location, and resource group, that is 1 GB in size with the non-SSL port disabled.</span></span>

<span data-ttu-id="370c9-238">Pour créer un cache premium, spécifiez la taille de P1 (de 6 Go à 60 Go), P2 (de 13 Go à 130 Go), P3 (de 26 Go à 260 Go) ou P4 (de 53 Go à 530 Go).</span><span class="sxs-lookup"><span data-stu-id="370c9-238">To create a premium cache, specify a size of P1 (6 GB - 60 GB), P2 (13 GB - 130 GB), P3 (26 GB - 260 GB), or P4 (53 GB - 530 GB).</span></span> <span data-ttu-id="370c9-239">Pour activer le clustering, spécifiez un nombre de partitions à l'aide du paramètre `ShardCount`.</span><span class="sxs-lookup"><span data-stu-id="370c9-239">To enable clustering, specify a shard count using the `ShardCount` parameter.</span></span> <span data-ttu-id="370c9-240">L'exemple suivant permet de créer un cache premium P1 avec 3 partitions.</span><span class="sxs-lookup"><span data-stu-id="370c9-240">The following example creates a P1 premium cache with 3 shards.</span></span> <span data-ttu-id="370c9-241">La taille d’un cache premium P1 est de 6 Go. Puisque nous avons spécifié trois partitions, la taille totale est de 18 Go (3 x 6 Go).</span><span class="sxs-lookup"><span data-stu-id="370c9-241">A P1 premium cache is 6 GB in size, and since we specified three shards the total size is 18 GB (3 x 6 GB).</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P1 -ShardCount 3

<span data-ttu-id="370c9-242">Pour spécifier des valeurs pour le paramètre `RedisConfiguration`, entourez les valeurs dans `{}` en tant que paire clé/valeur telle que `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`.</span><span class="sxs-lookup"><span data-stu-id="370c9-242">To specify values for the `RedisConfiguration` parameter, enclose the values inside `{}` as key/value pairs like `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`.</span></span> <span data-ttu-id="370c9-243">L'exemple suivant permet de créer un cache standard de 1 Go avec la stratégie maxmemory `allkeys-random` et les notifications de keyspace configurées avec `KEA`.</span><span class="sxs-lookup"><span data-stu-id="370c9-243">The following example creates a standard 1 GB cache with `allkeys-random` maxmemory policy and keyspace notifications configured with `KEA`.</span></span> <span data-ttu-id="370c9-244">Pour plus d’informations, voir [Notifications de keyspace (paramètres avancés)](cache-configure.md#keyspace-notifications-advanced-settings) et [Stratégies de mémoire](cache-configure.md#memory-policies).</span><span class="sxs-lookup"><span data-stu-id="370c9-244">For more information, see [Keyspace notifications (advanced settings)](cache-configure.md#keyspace-notifications-advanced-settings) and [Memory policies](cache-configure.md#memory-policies).</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}

<a name="databases"></a>

## <a name="to-configure-the-databases-setting-during-cache-creation"></a><span data-ttu-id="370c9-245">Pour configurer les paramètres des bases de données lors de la création du cache</span><span class="sxs-lookup"><span data-stu-id="370c9-245">To configure the databases setting during cache creation</span></span>
<span data-ttu-id="370c9-246">Le paramètre `databases` ne peut être configuré qu’au moment de la création du cache.</span><span class="sxs-lookup"><span data-stu-id="370c9-246">The `databases` setting can be configured only during cache creation.</span></span> <span data-ttu-id="370c9-247">L’exemple suivant crée un cache premium P3 (26 Go) avec 48 bases de données à l’aide de l’applet de commande [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) .</span><span class="sxs-lookup"><span data-stu-id="370c9-247">The following example creates a premium P3 (26 GB) cache with 48 databases using the [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P3 -RedisConfiguration @{"databases" = "48"}

<span data-ttu-id="370c9-248">Pour plus d’informations sur la propriété `databases` , consultez la section [Configuration du serveur de cache Azure Redis par défaut](cache-configure.md#default-redis-server-configuration).</span><span class="sxs-lookup"><span data-stu-id="370c9-248">For more information on the `databases` property, see [Default Azure Redis Cache server configuration](cache-configure.md#default-redis-server-configuration).</span></span> <span data-ttu-id="370c9-249">Pour plus d’informations sur la création d’un cache à l’aide de l’applet de commande [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx), voir la section précédente, [Création d’un cache Redis](#to-create-a-redis-cache).</span><span class="sxs-lookup"><span data-stu-id="370c9-249">For more information on creating a cache using the [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet, see the previous [To create a Redis Cache](#to-create-a-redis-cache) section.</span></span>

## <a name="to-update-a-redis-cache"></a><span data-ttu-id="370c9-250">Mise à jour d’un cache Redis</span><span class="sxs-lookup"><span data-stu-id="370c9-250">To update a Redis cache</span></span>
<span data-ttu-id="370c9-251">Les instances de cache Redis Azure sont mises à jour à l'aide de l’applet de commande [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) .</span><span class="sxs-lookup"><span data-stu-id="370c9-251">Azure Redis Cache instances are updated using the [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet.</span></span>

<span data-ttu-id="370c9-252">Pour afficher la liste des paramètres disponibles et leurs descriptions pour `Set-AzureRmRedisCache`, exécutez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="370c9-252">To see a list of available parameters and their descriptions for `Set-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help Set-AzureRmRedisCache -detailed

    NAME
        Set-AzureRmRedisCache

    SYNOPSIS
        Set redis cache updatable parameters.

    SYNTAX
        Set-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Size <String>] [-Sku <String>]
        [-MaxMemoryPolicy <String>] [-RedisConfiguration <Hashtable>] [-EnableNonSslPort <Boolean>] [-ShardCount
        <Integer>] [<CommonParameters>]

    DESCRIPTION
        The Set-AzureRmRedisCache cmdlet sets redis cache parameters.

    PARAMETERS
        -Name <String>
            Name of the redis cache to update.

        -ResourceGroupName <String>
            Name of the resource group for the cache.

        -Size <String>
            Size of the redis cache. The default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. The default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            The 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting to set
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. The default value is null and no change will be made to the
            currently configured value. Possible values are true and false.

        -ShardCount <Integer>
            The number of shards to create on a Premium Cluster Cache.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="370c9-253">L'applet de commande `Set-AzureRmRedisCache` peut être utilisée pour mettre à jour des propriétés telles que les valeurs `Size`, `Sku`, `EnableNonSslPort` et `RedisConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="370c9-253">The `Set-AzureRmRedisCache` cmdlet can be used to update properties such as `Size`, `Sku`, `EnableNonSslPort`, and the `RedisConfiguration` values.</span></span> 

<span data-ttu-id="370c9-254">La commande suivante met à jour le paramètre maxmemory-policy du cache Redis appelé myCache.</span><span class="sxs-lookup"><span data-stu-id="370c9-254">The following command updates the maxmemory-policy for the Redis Cache named myCache.</span></span>

    Set-AzureRmRedisCache -ResourceGroupName "myGroup" -Name "myCache" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random"}

<a name="scale"></a>

## <a name="to-scale-a-redis-cache"></a><span data-ttu-id="370c9-255">Pour mettre à l’échelle un cache Redis</span><span class="sxs-lookup"><span data-stu-id="370c9-255">To scale a Redis cache</span></span>
<span data-ttu-id="370c9-256">`Set-AzureRmRedisCache` peut être utilisé pour mettre à l’échelle une instance de cache Redis Azure quand les propriétés `Size`, `Sku` ou `ShardCount` sont modifiées.</span><span class="sxs-lookup"><span data-stu-id="370c9-256">`Set-AzureRmRedisCache` can be used to scale an Azure Redis cache instance when the `Size`, `Sku`, or `ShardCount` properties are modified.</span></span> 

> [!NOTE]
> <span data-ttu-id="370c9-257">La mise à l’échelle d’un cache à l’aide de PowerShell est soumise aux mêmes limites et recommandations que la mise à l’échelle d’un cache à l’aide du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="370c9-257">Scaling a cache using PowerShell is subject to the same limits and guidelines as scaling a cache from the Azure portal.</span></span> <span data-ttu-id="370c9-258">Vous pouvez choisir un niveau tarifaire différent avec les restrictions suivantes.</span><span class="sxs-lookup"><span data-stu-id="370c9-258">You can scale to a different pricing tier with the following restrictions.</span></span>
> 
> * <span data-ttu-id="370c9-259">Vous ne pouvez pas passer d’un niveau de tarification supérieur à un niveau de tarification inférieur.</span><span class="sxs-lookup"><span data-stu-id="370c9-259">You can't scale from a higher pricing tier to a lower pricing tier.</span></span>
> * <span data-ttu-id="370c9-260">Vous ne pouvez pas passer d’un cache **Premium** à un cache **Standard** ou **De base**.</span><span class="sxs-lookup"><span data-stu-id="370c9-260">You can't scale from a **Premium** cache down to a **Standard** or a **Basic** cache.</span></span>
> * <span data-ttu-id="370c9-261">Vous ne pouvez pas passer d’un cache **Standard** à un cache **De base**.</span><span class="sxs-lookup"><span data-stu-id="370c9-261">You can't scale from a **Standard** cache down to a **Basic** cache.</span></span>
> * <span data-ttu-id="370c9-262">Vous pouvez passer d’un cache **De base** à un cache **Standard**, mais vous ne pouvez pas modifier la taille en même temps.</span><span class="sxs-lookup"><span data-stu-id="370c9-262">You can scale from a **Basic** cache to a **Standard** cache but you can't change the size at the same time.</span></span> <span data-ttu-id="370c9-263">Si vous avez besoin d'une taille différente, vous pouvez effectuer ultérieurement une opération de mise à l'échelle vers la taille voulue.</span><span class="sxs-lookup"><span data-stu-id="370c9-263">If you need a different size, you can do a subsequent scaling operation to the desired size.</span></span>
> * <span data-ttu-id="370c9-264">Vous ne pouvez pas passer directement d’un cache **De base** à un cache **Premium**.</span><span class="sxs-lookup"><span data-stu-id="370c9-264">You can't scale from a **Basic** cache directly to a **Premium** cache.</span></span> <span data-ttu-id="370c9-265">Vous devez passer du niveau **De base** au niveau **Standard** en une opération de mise à l’échelle, puis du niveau **Standard** au niveau **Premium** en une deuxième opération.</span><span class="sxs-lookup"><span data-stu-id="370c9-265">You must scale from **Basic** to **Standard** in one scaling operation, and then from **Standard** to **Premium** in a subsequent scaling operation.</span></span>
> * <span data-ttu-id="370c9-266">Vous ne pouvez pas mettre à l’échelle depuis une taille supérieure vers la taille **C0 (250 Mo)** .</span><span class="sxs-lookup"><span data-stu-id="370c9-266">You can't scale from a larger size down to the **C0 (250 MB)** size.</span></span>
> 
> <span data-ttu-id="370c9-267">Pour plus d’informations, voir [Mise à l’échelle du cache Redis Azure](cache-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="370c9-267">For more information, see [How to Scale Azure Redis Cache](cache-how-to-scale.md).</span></span>
> 
> 

<span data-ttu-id="370c9-268">L’exemple suivant montre comment mettre à l’échelle un cache nommé `myCache` vers un cache de 2,5 Go.</span><span class="sxs-lookup"><span data-stu-id="370c9-268">The following example shows how to scale a cache named `myCache` to a 2.5 GB cache.</span></span> <span data-ttu-id="370c9-269">Notez que cette commande fonctionne pour un cache De base ou un cache Standard.</span><span class="sxs-lookup"><span data-stu-id="370c9-269">Note that this command works for both a Basic or a Standard cache.</span></span>

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

<span data-ttu-id="370c9-270">Une fois cette commande émise, l’état du cache est retourné (ceci est similaire à l’appel `Get-AzureRmRedisCache`).</span><span class="sxs-lookup"><span data-stu-id="370c9-270">After this command is issued, the status of the cache is returned (similar to calling `Get-AzureRmRedisCache`).</span></span> <span data-ttu-id="370c9-271">Notez que `ProvisioningState` est `Scaling`.</span><span class="sxs-lookup"><span data-stu-id="370c9-271">Note that the `ProvisioningState` is `Scaling`.</span></span>

    PS C:\> Set-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup -Size 2.5GB


    Name               : mycache
    Id                 : /subscriptions/12ad12bd-abdc-2231-a2ed-a2b8b246bbad4/resourceGroups/mygroup/providers/Mi
                         crosoft.Cache/Redis/mycache
    Location           : South Central US
    Type               : Microsoft.Cache/Redis
    HostName           : mycache.redis.cache.windows.net
    Port               : 6379
    ProvisioningState  : Scaling
    SslPort            : 6380
    RedisConfiguration : {[maxmemory-policy, volatile-lru], [maxmemory-reserved, 150], [notify-keyspace-events, KEA],
                         [maxmemory-delta, 150]...}
    EnableNonSslPort   : False
    RedisVersion       : 3.0
    Size               : 1GB
    Sku                : Standard
    ResourceGroupName  : mygroup
    PrimaryKey         : ....
    SecondaryKey       : ....
    VirtualNetwork     :
    Subnet             :
    StaticIP           :
    TenantSettings     : {}
    ShardCount         :

<span data-ttu-id="370c9-272">Quand l’opération de mise à l’échelle est terminée, `ProvisioningState` passe à `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="370c9-272">When the scaling operation is complete, the `ProvisioningState` changes to `Succeeded`.</span></span> <span data-ttu-id="370c9-273">Si vous devez effectuer une opération de mise à l'échelle associée, comme mettre à l’échelle un cache De base vers un cache Standard, puis changer la taille, vous devez patienter jusqu’à ce que l’opération précédente soit terminée. Dans le cas contraire, vous recevrez une erreur similaire à la suivante.</span><span class="sxs-lookup"><span data-stu-id="370c9-273">If you need to make a subsequent scaling operation, such as changing from Basic to Standard and then changing the size, you must wait until the previous operation is complete or you receive an error similar to the following.</span></span>

    Set-AzureRmRedisCache : Conflict: The resource '...' is not in a stable state, and is currently unable to accept the update request.

## <a name="to-get-information-about-a-redis-cache"></a><span data-ttu-id="370c9-274">Obtention d’informations sur un cache Redis</span><span class="sxs-lookup"><span data-stu-id="370c9-274">To get information about a Redis cache</span></span>
<span data-ttu-id="370c9-275">Vous pouvez récupérer des informations sur un cache à l’aide de l’applet de commande [Get-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634514.aspx) .</span><span class="sxs-lookup"><span data-stu-id="370c9-275">You can retrieve information about a cache using the [Get-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634514.aspx) cmdlet.</span></span>

<span data-ttu-id="370c9-276">Pour afficher la liste des paramètres disponibles et leurs descriptions pour `Get-AzureRmRedisCache`, exécutez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="370c9-276">To see a list of available parameters and their descriptions for `Get-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help Get-AzureRmRedisCache -detailed

    NAME
        Get-AzureRmRedisCache

    SYNOPSIS
        Gets details about a single cache or all caches in the specified resource group or all caches in the current
        subscription.

    SYNTAX
        Get-AzureRmRedisCache [-Name <String>] [-ResourceGroupName <String>] [<CommonParameters>]

    DESCRIPTION
        The Get-AzureRmRedisCache cmdlet gets the details about a cache or caches depending on input parameters. If both
        ResourceGroupName and Name parameters are provided then Get-AzureRmRedisCache will return details about the
        specific cache name provided.

        If only ResourceGroupName is provided than it will return details about all caches in the specified resource group.

        If no parameters are given than it will return details about all caches the current subscription.

    PARAMETERS
        -Name <String>
            The name of the cache. When this parameter is provided along with ResourceGroupName, Get-AzureRmRedisCache
            returns the details for the cache.

        -ResourceGroupName <String>
            The name of the resource group that contains the cache or caches. If ResourceGroupName is provided with Name
            then Get-AzureRmRedisCache returns the details of the cache specified by Name. If only the ResourceGroup
            parameter is provided, then details for all caches in the resource group are returned.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="370c9-277">Pour retourner des informations sur tous les caches de l’abonnement actuel, exécutez `Get-AzureRmRedisCache` sans aucun paramètre.</span><span class="sxs-lookup"><span data-stu-id="370c9-277">To return information about all caches in the current subscription, run `Get-AzureRmRedisCache` without any parameters.</span></span>

    Get-AzureRmRedisCache

<span data-ttu-id="370c9-278">Pour retourner des informations sur tous les caches d’un groupe de ressources spécifique, exécutez `Get-AzureRmRedisCache` avec le paramètre `ResourceGroupName`.</span><span class="sxs-lookup"><span data-stu-id="370c9-278">To return information about all caches in a specific resource group, run `Get-AzureRmRedisCache` with the `ResourceGroupName` parameter.</span></span>

    Get-AzureRmRedisCache -ResourceGroupName myGroup

<span data-ttu-id="370c9-279">Pour retourner des informations sur un cache spécifique, exécutez `Get-AzureRmRedisCache` avec le paramètre `Name` contenant le nom du cache et le paramètre `ResourceGroupName` avec le groupe de ressources contenant ce cache.</span><span class="sxs-lookup"><span data-stu-id="370c9-279">To return information about a specific cache, run `Get-AzureRmRedisCache` with the `Name` parameter containing the name of the cache, and the `ResourceGroupName` parameter with the resource group containing that cache.</span></span>

    PS C:\> Get-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Name               : mycache
    Id                 : /subscriptions/12ad12bd-abdc-2231-a2ed-a2b8b246bbad4/resourceGroups/myGroup/providers/Mi
                         crosoft.Cache/Redis/mycache
    Location           : South Central US
    Type               : Microsoft.Cache/Redis
    HostName           : mycache.redis.cache.windows.net
    Port               : 6379
    ProvisioningState  : Succeeded
    SslPort            : 6380
    RedisConfiguration : {[maxmemory-policy, volatile-lru], [maxmemory-reserved, 62], [notify-keyspace-events, KEA],
                         [maxclients, 1000]...}
    EnableNonSslPort   : False
    RedisVersion       : 3.0
    Size               : 1GB
    Sku                : Standard
    ResourceGroupName  : myGroup
    VirtualNetwork     :
    Subnet             :
    StaticIP           :
    TenantSettings     : {}
    ShardCount         :

## <a name="to-retrieve-the-access-keys-for-a-redis-cache"></a><span data-ttu-id="370c9-280">Récupération des clés d'accès d’un cache Redis</span><span class="sxs-lookup"><span data-stu-id="370c9-280">To retrieve the access keys for a Redis cache</span></span>
<span data-ttu-id="370c9-281">Pour récupérer les clés d'accès de votre cache, vous pouvez utiliser l’applet de commande [Get-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634516.aspx) .</span><span class="sxs-lookup"><span data-stu-id="370c9-281">To retrieve the access keys for your cache, you can use the [Get-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634516.aspx) cmdlet.</span></span>

<span data-ttu-id="370c9-282">Pour afficher la liste des paramètres disponibles et leurs descriptions pour `Get-AzureRmRedisCacheKey`, exécutez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="370c9-282">To see a list of available parameters and their descriptions for `Get-AzureRmRedisCacheKey`, run the following command.</span></span>

    PS C:\> Get-Help Get-AzureRmRedisCacheKey -detailed

    NAME
        Get-AzureRmRedisCacheKey

    SYNOPSIS
        Gets the accesskeys for the specified redis cache.


    SYNTAX
        Get-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> [<CommonParameters>]

    DESCRIPTION
        The Get-AzureRmRedisCacheKey cmdlet gets the access keys for the specified cache.

    PARAMETERS
        -Name <String>
            Name of the redis cache.

        -ResourceGroupName <String>
            Name of the resource group for the cache.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="370c9-283">Pour récupérer les clés de votre cache, appelez l’applet de commande `Get-AzureRmRedisCacheKey` , et passez le nom de votre cache et le nom du groupe de ressources contenant le cache.</span><span class="sxs-lookup"><span data-stu-id="370c9-283">To retrieve the keys for your cache, call the `Get-AzureRmRedisCacheKey` cmdlet and pass in the name of your cache the name of the resource group that contains the cache.</span></span>

    PS C:\> Get-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup

    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : ABhfB757JgjIgt785JgKH9865eifmekfnn649303JKL=

## <a name="to-regenerate-access-keys-for-your-redis-cache"></a><span data-ttu-id="370c9-284">Régénération des clés d’accès de votre cache Redis</span><span class="sxs-lookup"><span data-stu-id="370c9-284">To regenerate access keys for your Redis cache</span></span>
<span data-ttu-id="370c9-285">Pour régénérer les clés d’accès de votre cache, vous pouvez utiliser l’applet de commande [New-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634512.aspx) .</span><span class="sxs-lookup"><span data-stu-id="370c9-285">To regenerate the access keys for your cache, you can use the [New-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634512.aspx) cmdlet.</span></span>

<span data-ttu-id="370c9-286">Pour afficher la liste des paramètres disponibles et leurs descriptions pour `New-AzureRmRedisCacheKey`, exécutez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="370c9-286">To see a list of available parameters and their descriptions for `New-AzureRmRedisCacheKey`, run the following command.</span></span>

    PS C:\> Get-Help New-AzureRmRedisCacheKey -detailed

    NAME
        New-AzureRmRedisCacheKey

    SYNOPSIS
        Regenerates the access key of a redis cache.

    SYNTAX
        New-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> -KeyType <String> [-Force] [<CommonParameters>]

    DESCRIPTION
        The New-AzureRmRedisCacheKey cmdlet regenerate the access key of a redis cache.

    PARAMETERS
        -Name <String>
            Name of the redis cache.

        -ResourceGroupName <String>
            Name of the resource group for the cache.

        -KeyType <String>
            Specifies whether to regenerate the primary or secondary access key. Possible values are Primary or Secondary.

        -Force
            When the Force parameter is provided, the specified access key is regenerated without any confirmation prompts.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="370c9-287">Pour régénérer la clé principale ou secondaire de votre cache, appelez l’applet de commande `New-AzureRmRedisCacheKey` et passez le nom et le groupe de ressources, et spécifiez `Primary` ou `Secondary` pour le paramètre `KeyType`.</span><span class="sxs-lookup"><span data-stu-id="370c9-287">To regenerate the primary or secondary key for your cache, call the `New-AzureRmRedisCacheKey` cmdlet and pass in the name, resource group, and specify either `Primary` or `Secondary` for the `KeyType` parameter.</span></span> <span data-ttu-id="370c9-288">Dans l’exemple suivant, la clé d’accès secondaire d’un cache est régénérée.</span><span class="sxs-lookup"><span data-stu-id="370c9-288">In the following example, the secondary access key for a cache is regenerated.</span></span>

    PS C:\> New-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup -KeyType Secondary

    Confirm
    Are you sure you want to regenerate Secondary key for redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : c53hj3kh4jhHjPJk8l0jji785JgKH9865eifmekfnn6=

## <a name="to-delete-a-redis-cache"></a><span data-ttu-id="370c9-289">Suppression d’un cache Redis</span><span class="sxs-lookup"><span data-stu-id="370c9-289">To delete a Redis cache</span></span>
<span data-ttu-id="370c9-290">Pour supprimer un cache Redis, utilisez l’applet de commande [Remove-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634515.aspx) .</span><span class="sxs-lookup"><span data-stu-id="370c9-290">To delete a Redis cache, use the [Remove-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634515.aspx) cmdlet.</span></span>

<span data-ttu-id="370c9-291">Pour afficher la liste des paramètres disponibles et leurs descriptions pour `Remove-AzureRmRedisCache`, exécutez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="370c9-291">To see a list of available parameters and their descriptions for `Remove-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help Remove-AzureRmRedisCache -detailed

    NAME
        Remove-AzureRmRedisCache

    SYNOPSIS
        Remove redis cache if exists.

    SYNTAX
        Remove-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Force] [-PassThru] [<CommonParameters>

    DESCRIPTION
        The Remove-AzureRmRedisCache cmdlet removes a redis cache if it exists.

    PARAMETERS
        -Name <String>
            Name of the redis cache to remove.

        -ResourceGroupName <String>
            Name of the resource group of the cache to remove.

        -Force
            When the Force parameter is provided, the cache is removed without any confirmation prompts.

        -PassThru
            By default Remove-AzureRmRedisCache removes the cache and does not return any value. If the PassThru par
            is provided then Remove-AzureRmRedisCache returns a boolean value indicating the success of the operatio

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="370c9-292">Dans l’exemple suivant, le cache nommé `myCache` est supprimé.</span><span class="sxs-lookup"><span data-stu-id="370c9-292">In the following example, the cache named `myCache` is removed.</span></span>

    PS C:\> Remove-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Confirm
    Are you sure you want to remove redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


## <a name="to-import-a-redis-cache"></a><span data-ttu-id="370c9-293">Pour importer un cache Redis</span><span class="sxs-lookup"><span data-stu-id="370c9-293">To import a Redis cache</span></span>
<span data-ttu-id="370c9-294">Vous pouvez importer des données dans une instance du cache Redis Azure à l’aide de l’applet de commande `Import-AzureRmRedisCache` .</span><span class="sxs-lookup"><span data-stu-id="370c9-294">You can import data into an Azure Redis Cache instance using the `Import-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="370c9-295">L’importation/exportation est uniquement disponible pour les caches de niveau [Premium](cache-premium-tier-intro.md) .</span><span class="sxs-lookup"><span data-stu-id="370c9-295">Import/Export is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="370c9-296">Pour plus d’informations sur l’importation/exportation, voir [Importer et exporter des données dans le cache Redis Azure](cache-how-to-import-export-data.md).</span><span class="sxs-lookup"><span data-stu-id="370c9-296">For more information about Import/Export, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

<span data-ttu-id="370c9-297">Pour afficher la liste des paramètres disponibles et leurs descriptions pour `Import-AzureRmRedisCache`, exécutez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="370c9-297">To see a list of available parameters and their descriptions for `Import-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help Import-AzureRmRedisCache -detailed

    NAME
        Import-AzureRmRedisCache

    SYNOPSIS
        Import data from blobs to Azure Redis Cache.


    SYNTAX
        Import-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Files <String[]> [-Format <String>] [-Force]
        [-PassThru] [<CommonParameters>]


    DESCRIPTION
        The Import-AzureRmRedisCache cmdlet imports data from the specified blobs into Azure Redis Cache.


    PARAMETERS
        -Name <String>
            The name of the cache.

        -ResourceGroupName <String>
            The name of the resource group that contains the cache.

        -Files <String[]>
            SAS urls of blobs whose content should be imported into the cache.

        -Format <String>
            Format for the blob.  Currently "rdb" is the only supported, with other formats expected in the future.

        -Force
            When the Force parameter is provided, import will be performed without any confirmation prompts.

        -PassThru
            By default Import-AzureRmRedisCache imports data in cache and does not return any value. If the PassThru
            parameter is provided then Import-AzureRmRedisCache returns a boolean value indicating the success of the
            operation.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="370c9-298">La commande suivante importe des données à partir de l’objet blob spécifié par l’URI SAP dans le cache Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="370c9-298">The following command imports data from the blob specified by the SAS uri into Azure Redis Cache.</span></span>

    PS C:\>Import-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Files @("https://mystorageaccount.blob.core.windows.net/mycontainername/blobname?sv=2015-04-05&sr=b&sig=caIwutG2uDa0NZ8mjdNJdgOY8%2F8mhwRuGNdICU%2B0pI4%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwd") -Force

## <a name="to-export-a-redis-cache"></a><span data-ttu-id="370c9-299">Pour exporter un cache Redis</span><span class="sxs-lookup"><span data-stu-id="370c9-299">To export a Redis cache</span></span>
<span data-ttu-id="370c9-300">Vous pouvez exporter des données depuis une instance du cache Redis Azure à l’aide de l’applet de commande `Export-AzureRmRedisCache` .</span><span class="sxs-lookup"><span data-stu-id="370c9-300">You can export data from an Azure Redis Cache instance using the `Export-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="370c9-301">L’importation/exportation est uniquement disponible pour les caches de niveau [Premium](cache-premium-tier-intro.md) .</span><span class="sxs-lookup"><span data-stu-id="370c9-301">Import/Export is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="370c9-302">Pour plus d’informations sur l’importation/exportation, voir [Importer et exporter des données dans le cache Redis Azure](cache-how-to-import-export-data.md).</span><span class="sxs-lookup"><span data-stu-id="370c9-302">For more information about Import/Export, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

<span data-ttu-id="370c9-303">Pour afficher la liste des paramètres disponibles et leurs descriptions pour `Export-AzureRmRedisCache`, exécutez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="370c9-303">To see a list of available parameters and their descriptions for `Export-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help Export-AzureRmRedisCache -detailed

    NAME
        Export-AzureRmRedisCache

    SYNOPSIS
        Exports data from Azure Redis Cache to a specified container.


    SYNTAX
        Export-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Prefix <String> -Container <String> [-Format
        <String>] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        The Export-AzureRmRedisCache cmdlet exports data from Azure Redis Cache to a specified container.


    PARAMETERS
        -Name <String>
            The name of the cache.

        -ResourceGroupName <String>
            The name of the resource group that contains the cache.

        -Prefix <String>
            Prefix to use for blob names.

        -Container <String>
            SAS url of container where data should be exported.

        -Format <String>
            Format for the blob.  Currently "rdb" is the only supported, with other formats expected in the future.

        -PassThru
            By default Export-AzureRmRedisCache does not return any value. If the PassThru parameter is provided
            then Export-AzureRmRedisCache returns a boolean value indicating the success of the operation.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="370c9-304">La commande suivante exporte les données à partir d’une instance du cache Redis Azure vers le conteneur spécifié par l’URI SAP.</span><span class="sxs-lookup"><span data-stu-id="370c9-304">The following command exports data from an Azure Redis Cache instance into the container specified by the SAS uri.</span></span>

        PS C:\>Export-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Prefix "blobprefix"
        -Container "https://mystorageaccount.blob.core.windows.net/mycontainer?sv=2015-04-05&sr=c&sig=HezZtBZ3DURmEGDduauE7
        pvETY4kqlPI8JCNa8ATmaw%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwdl"

## <a name="to-reboot-a-redis-cache"></a><span data-ttu-id="370c9-305">Pour redémarrer un cache Redis</span><span class="sxs-lookup"><span data-stu-id="370c9-305">To reboot a Redis cache</span></span>
<span data-ttu-id="370c9-306">Vous pouvez redémarrer votre cache Redis Azure à l’aide de l’applet de commande `Reset-AzureRmRedisCache` .</span><span class="sxs-lookup"><span data-stu-id="370c9-306">You can reboot your Azure Redis Cache instance using the `Reset-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="370c9-307">Le redémarrage est uniquement disponible pour les caches de [niveau Premium](cache-premium-tier-intro.md) .</span><span class="sxs-lookup"><span data-stu-id="370c9-307">Reboot is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="370c9-308">Pour plus d’informations sur le redémarrage de votre cache, voir [Administration du cache - Redémarrage](cache-administration.md#reboot).</span><span class="sxs-lookup"><span data-stu-id="370c9-308">For more information about rebooting your cache, see [Cache administration - reboot](cache-administration.md#reboot).</span></span>
> 
> 

<span data-ttu-id="370c9-309">Pour afficher la liste des paramètres disponibles et leurs descriptions pour `Reset-AzureRmRedisCache`, exécutez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="370c9-309">To see a list of available parameters and their descriptions for `Reset-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help Reset-AzureRmRedisCache -detailed

    NAME
        Reset-AzureRmRedisCache

    SYNOPSIS
        Reboot specified node(s) of an Azure Redis Cache instance.


    SYNTAX
        Reset-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -RebootType <String> [-ShardId <Integer>]
        [-Force] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        The Reset-AzureRmRedisCache cmdlet reboots the specified node(s) of an Azure Redis Cache instance.


    PARAMETERS
        -Name <String>
            The name of the cache.

        -ResourceGroupName <String>
            The name of the resource group that contains the cache.

        -RebootType <String>
            Which node to reboot. Possible values are "PrimaryNode", "SecondaryNode", "AllNodes".

        -ShardId <Integer>
            Which shard to reboot when rebooting a premium cache with clustering enabled.

        -Force
            When the Force parameter is provided, reset will be performed without any confirmation prompts.

        -PassThru
            By default Reset-AzureRmRedisCache does not return any value. If the PassThru parameter is provided
            then Reset-AzureRmRedisCache returns a boolean value indicating the success of the operation.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="370c9-310">La commande suivante redémarre les deux nœuds du cache spécifié.</span><span class="sxs-lookup"><span data-stu-id="370c9-310">The following command reboots both nodes of the specified cache.</span></span>

        PS C:\>Reset-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -RebootType "AllNodes"
        -Force


## <a name="next-steps"></a><span data-ttu-id="370c9-311">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="370c9-311">Next steps</span></span>
<span data-ttu-id="370c9-312">Pour en savoir plus sur l’utilisation de Windows PowerShell avec Azure, reportez-vous aux ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="370c9-312">To learn more about using Windows PowerShell with Azure, see the following resources:</span></span>

* [<span data-ttu-id="370c9-313">Documentation relative à l’applet de commande Cache Redis Azure sur MSDN</span><span class="sxs-lookup"><span data-stu-id="370c9-313">Azure Redis Cache cmdlet documentation on MSDN</span></span>](https://msdn.microsoft.com/library/azure/mt634513.aspx)
* <span data-ttu-id="370c9-314">[Applets de commande Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkID=394765) : découvrez comment utiliser les applets de commande dans le module Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="370c9-314">[Azure Resource Manager Cmdlets](http://go.microsoft.com/fwlink/?LinkID=394765): Learn to use the cmdlets in the Azure Resource Manager module.</span></span>
* <span data-ttu-id="370c9-315">[Utilisation de groupes de ressources pour gérer vos ressources Azure](../azure-resource-manager/resource-group-template-deploy-portal.md): découvrez comment créer et gérer des groupes de ressources dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="370c9-315">[Using Resource groups to manage your Azure resources](../azure-resource-manager/resource-group-template-deploy-portal.md): Learn how to create and manage resource groups in the Azure portal.</span></span>
* <span data-ttu-id="370c9-316">[Blog Azure](http://blogs.msdn.com/windowsazure): découvrez les nouvelles fonctionnalités d'Azure.</span><span class="sxs-lookup"><span data-stu-id="370c9-316">[Azure blog](http://blogs.msdn.com/windowsazure): Learn about new features in Azure.</span></span>
* <span data-ttu-id="370c9-317">[Blog Windows PowerShell](http://blogs.msdn.com/powershell): découvrez les nouvelles fonctionnalités de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="370c9-317">[Windows PowerShell blog](http://blogs.msdn.com/powershell): Learn about new features in Windows PowerShell.</span></span>
* <span data-ttu-id="370c9-318">[Blog « Hey, Scripting Guy! »](http://blogs.technet.com/b/heyscriptingguy/) : bénéficiez des conseils et astuces de la communauté Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="370c9-318">["Hey, Scripting Guy!" Blog](http://blogs.technet.com/b/heyscriptingguy/): Get real-world tips and tricks from the Windows PowerShell community.</span></span>

