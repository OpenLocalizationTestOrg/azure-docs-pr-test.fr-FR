---
title: aaaManage du Cache Redis Azure avec Azure PowerShell | Documents Microsoft
description: "Découvrez comment tooperform les tâches d’administration pour le Cache Redis Azure à l’aide d’Azure PowerShell."
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
ms.openlocfilehash: 1d526ce65c4bc05345cd6c3ff370211ed562cab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-redis-cache-with-azure-powershell"></a><span data-ttu-id="3bbec-103">Gestion du Cache Redis Azure avec Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3bbec-103">Manage Azure Redis Cache with Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3bbec-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3bbec-104">PowerShell</span></span>](cache-howto-manage-redis-cache-powershell.md)
> * [<span data-ttu-id="3bbec-105">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="3bbec-105">Azure CLI</span></span>](cache-manage-cli.md)
> 
> 

<span data-ttu-id="3bbec-106">Cette rubrique vous montre comment tooperform courants des tâches telles que créer, mettre à jour et mettre à l’échelle vos instances de Cache Redis Azure, comment tooregenerate clés d’accès et la manière dont les informations de tooview sur vos caches.</span><span class="sxs-lookup"><span data-stu-id="3bbec-106">This topic shows you how tooperform common tasks such as create, update, and scale your Azure Redis Cache instances, how tooregenerate access keys, and how tooview information about your caches.</span></span> <span data-ttu-id="3bbec-107">Pour obtenir une liste complète des applets de commande PowerShell de cache Redis Azure, consultez [Applets de commande de cache Redis Azure](https://msdn.microsoft.com/library/azure/mt634513.aspx).</span><span class="sxs-lookup"><span data-stu-id="3bbec-107">For a complete list of Azure Redis Cache PowerShell cmdlets, see [Azure Redis Cache cmdlets](https://msdn.microsoft.com/library/azure/mt634513.aspx).</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="3bbec-108">Pour plus d’informations sur le modèle de déploiement classique de hello, consultez [Azure Resource Manager et déploiement classique : comprendre les modèles de déploiement et état de vos ressources de hello](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics).</span><span class="sxs-lookup"><span data-stu-id="3bbec-108">For more information about hello classic deployment model, see [Azure Resource Manager vs. classic deployment: Understand deployment models and hello state of your resources](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3bbec-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="3bbec-109">Prerequisites</span></span>
<span data-ttu-id="3bbec-110">Si vous avez déjà installé Azure PowerShell, vous devez disposer d’Azure PowerShell version 1.0.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="3bbec-110">If you have already installed Azure PowerShell, you must have Azure PowerShell version 1.0.0 or later.</span></span> <span data-ttu-id="3bbec-111">Vous pouvez vérifier la version de hello d’Azure PowerShell que vous avez installé avec cette commande à l’invite de commande Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="3bbec-111">You can check hello version of Azure PowerShell that you have installed with this command at hello Azure PowerShell command prompt.</span></span>

    Get-Module azure | format-table version


<span data-ttu-id="3bbec-112">Tout d’abord, vous devez vous connecter tooAzure avec cette commande.</span><span class="sxs-lookup"><span data-stu-id="3bbec-112">First, you must log in tooAzure with this command.</span></span>

    Login-AzureRmAccount

<span data-ttu-id="3bbec-113">Spécifiez l’adresse de messagerie de hello de votre compte Azure et son mot de passe dans la boîte de dialogue hello signe dans Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="3bbec-113">Specify hello email address of your Azure account and its password in hello Microsoft Azure sign-in dialog.</span></span>

<span data-ttu-id="3bbec-114">Si vous avez plusieurs abonnements Azure, vous devez ensuite tooset votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="3bbec-114">Next, if you have multiple Azure subscriptions, you need tooset your Azure subscription.</span></span> <span data-ttu-id="3bbec-115">toosee une liste de vos abonnements en cours, exécutez la commande.</span><span class="sxs-lookup"><span data-stu-id="3bbec-115">toosee a list of your current subscriptions, run this command.</span></span>

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="3bbec-116">abonnement de hello toospecify, exécutez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="3bbec-116">toospecify hello subscription, run hello following command.</span></span> <span data-ttu-id="3bbec-117">Dans l’exemple suivant de hello, nom de l’abonnement hello est `ContosoSubscription`.</span><span class="sxs-lookup"><span data-stu-id="3bbec-117">In hello following example, hello subscription name is `ContosoSubscription`.</span></span>

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

<span data-ttu-id="3bbec-118">Avant de pouvoir utiliser Windows PowerShell avec Azure Resource Manager, vous devez suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="3bbec-118">Before you can use Windows PowerShell with Azure Resource Manager, you need hello following:</span></span>

* <span data-ttu-id="3bbec-119">Windows PowerShell, version 3.0 ou 4.0.</span><span class="sxs-lookup"><span data-stu-id="3bbec-119">Windows PowerShell, Version 3.0 or 4.0.</span></span> <span data-ttu-id="3bbec-120">version de hello toofind de Windows PowerShell, tapez :`$PSVersionTable` et vérifiez la valeur hello `PSVersion` est 3.0 ou 4.0.</span><span class="sxs-lookup"><span data-stu-id="3bbec-120">toofind hello version of Windows PowerShell, type:`$PSVersionTable` and verify hello value of `PSVersion` is 3.0 or 4.0.</span></span> <span data-ttu-id="3bbec-121">tooinstall une version compatible, consultez [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) ou [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span><span class="sxs-lookup"><span data-stu-id="3bbec-121">tooinstall a compatible version, see [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) or [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span></span>

<span data-ttu-id="3bbec-122">tooget détaillées aide pour une applet de commande que vous voyez dans ce didacticiel, l’applet de commande Get-Help utilisez hello.</span><span class="sxs-lookup"><span data-stu-id="3bbec-122">tooget detailed help for any cmdlet you see in this tutorial, use hello Get-Help cmdlet.</span></span>

    Get-Help <cmdlet-name> -Detailed

<span data-ttu-id="3bbec-123">Par exemple, tooget aide hello `New-AzureRmRedisCache` applet, tapez :</span><span class="sxs-lookup"><span data-stu-id="3bbec-123">For example, tooget help for hello `New-AzureRmRedisCache` cmdlet, type:</span></span>

    Get-Help New-AzureRmRedisCache -Detailed

### <a name="how-tooconnect-tooother-clouds"></a><span data-ttu-id="3bbec-124">Comment tooconnect tooother clouds</span><span class="sxs-lookup"><span data-stu-id="3bbec-124">How tooconnect tooother clouds</span></span>
<span data-ttu-id="3bbec-125">Par hello de valeur par défaut Azure environnement est `AzureCloud`, qui représente hello instance globale de cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="3bbec-125">By default hello Azure environment is `AzureCloud`, which represents hello global Azure cloud instance.</span></span> <span data-ttu-id="3bbec-126">tooconnect tooa instance différente, utilisez hello `Add-AzureRmAccount` avec hello `-Environment` ou -`EnvironmentName` commutateur de ligne de commande avec l’environnement désiré de hello ou nom de l’environnement.</span><span class="sxs-lookup"><span data-stu-id="3bbec-126">tooconnect tooa different instance, use hello `Add-AzureRmAccount` command with hello `-Environment` or -`EnvironmentName` command line switch with hello desired environment or environment name.</span></span>

<span data-ttu-id="3bbec-127">liste de hello toosee des environnements disponibles, exécutez hello `Get-AzureRmEnvironment` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="3bbec-127">toosee hello list of available environments, run hello `Get-AzureRmEnvironment` cmdlet.</span></span>

### <a name="tooconnect-toohello-azure-government-cloud"></a><span data-ttu-id="3bbec-128">tooconnect toohello le Cloud Azure Government</span><span class="sxs-lookup"><span data-stu-id="3bbec-128">tooconnect toohello Azure Government Cloud</span></span>
<span data-ttu-id="3bbec-129">tooconnect toohello Azure Government Cloud, utilisez une des hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="3bbec-129">tooconnect toohello Azure Government Cloud, use one of hello following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureUSGovernment

<span data-ttu-id="3bbec-130">ou</span><span class="sxs-lookup"><span data-stu-id="3bbec-130">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureUSGovernment)

<span data-ttu-id="3bbec-131">toocreate un cache Bonjour Azure Government Cloud, utilisez un des emplacements suivants de hello.</span><span class="sxs-lookup"><span data-stu-id="3bbec-131">toocreate a cache in hello Azure Government Cloud, use one of hello following locations.</span></span>

* <span data-ttu-id="3bbec-132">Gouvernement américain - Virginie</span><span class="sxs-lookup"><span data-stu-id="3bbec-132">USGov Virginia</span></span>
* <span data-ttu-id="3bbec-133">USGov Iowa</span><span class="sxs-lookup"><span data-stu-id="3bbec-133">USGov Iowa</span></span>

<span data-ttu-id="3bbec-134">Pour plus d’informations sur hello gouvernement le Cloud Azure, consultez [Microsoft Azure Government](https://azure.microsoft.com/features/gov/) et [Guide de développement Microsoft Azure Government](../azure-government-developer-guide.md).</span><span class="sxs-lookup"><span data-stu-id="3bbec-134">For more information about hello Azure Government Cloud, see [Microsoft Azure Government](https://azure.microsoft.com/features/gov/) and [Microsoft Azure Government Developer Guide](../azure-government-developer-guide.md).</span></span>

### <a name="tooconnect-toohello-azure-china-cloud"></a><span data-ttu-id="3bbec-135">tooconnect toohello le Cloud Azure en Chine</span><span class="sxs-lookup"><span data-stu-id="3bbec-135">tooconnect toohello Azure China Cloud</span></span>
<span data-ttu-id="3bbec-136">tooconnect toohello Azure en Chine Cloud, utilisez une des hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="3bbec-136">tooconnect toohello Azure China Cloud, use one of hello following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureChinaCloud

<span data-ttu-id="3bbec-137">ou</span><span class="sxs-lookup"><span data-stu-id="3bbec-137">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureChinaCloud)

<span data-ttu-id="3bbec-138">toocreate un cache Bonjour Azure en Chine Cloud, utilisez un des emplacements suivants de hello.</span><span class="sxs-lookup"><span data-stu-id="3bbec-138">toocreate a cache in hello Azure China Cloud, use one of hello following locations.</span></span>

* <span data-ttu-id="3bbec-139">Chine orientale</span><span class="sxs-lookup"><span data-stu-id="3bbec-139">China East</span></span>
* <span data-ttu-id="3bbec-140">Chine du Nord</span><span class="sxs-lookup"><span data-stu-id="3bbec-140">China North</span></span>

<span data-ttu-id="3bbec-141">Pour plus d’informations sur hello le Cloud Azure en Chine, consultez [AzureChinaCloud pour Azure géré par 21Vianet en Chine](http://www.windowsazure.cn/).</span><span class="sxs-lookup"><span data-stu-id="3bbec-141">For more information about hello Azure China Cloud, see [AzureChinaCloud for Azure operated by 21Vianet in China](http://www.windowsazure.cn/).</span></span>

### <a name="tooconnect-toomicrosoft-azure-germany"></a><span data-ttu-id="3bbec-142">tooconnect tooMicrosoft Azure situés en Allemagne</span><span class="sxs-lookup"><span data-stu-id="3bbec-142">tooconnect tooMicrosoft Azure Germany</span></span>
<span data-ttu-id="3bbec-143">tooconnect tooMicrosoft Allemagne d’Azure, utilisez une des hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="3bbec-143">tooconnect tooMicrosoft Azure Germany, use one of hello following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureGermanCloud


<span data-ttu-id="3bbec-144">ou</span><span class="sxs-lookup"><span data-stu-id="3bbec-144">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureGermanCloud)

<span data-ttu-id="3bbec-145">toocreate un cache dans Microsoft Azure Allemagne, utilisez un des emplacements suivants de hello.</span><span class="sxs-lookup"><span data-stu-id="3bbec-145">toocreate a cache in Microsoft Azure Germany, use one of hello following locations.</span></span>

* <span data-ttu-id="3bbec-146">Centre de l’Allemagne</span><span class="sxs-lookup"><span data-stu-id="3bbec-146">Germany Central</span></span>
* <span data-ttu-id="3bbec-147">Nord-Est de l’Allemagne</span><span class="sxs-lookup"><span data-stu-id="3bbec-147">Germany Northeast</span></span>

<span data-ttu-id="3bbec-148">Pour plus d’informations sur Microsoft Azure Allemagne, consultez [Microsoft Azure Allemagne](https://azure.microsoft.com/overview/clouds/germany/).</span><span class="sxs-lookup"><span data-stu-id="3bbec-148">For more information about Microsoft Azure Germany, see [Microsoft Azure Germany](https://azure.microsoft.com/overview/clouds/germany/).</span></span>

### <a name="properties-used-for-azure-redis-cache-powershell"></a><span data-ttu-id="3bbec-149">Propriétés utilisées pour le cache Redis Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3bbec-149">Properties used for Azure Redis Cache PowerShell</span></span>
<span data-ttu-id="3bbec-150">Hello tableau suivant contient les propriétés et les descriptions de paramètres couramment utilisés lors de la création et la gestion de vos instances de Cache Redis Azure à l’aide d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3bbec-150">hello following table contains properties and descriptions for commonly used parameters when creating and managing your Azure Redis Cache instances using Azure PowerShell.</span></span>

| <span data-ttu-id="3bbec-151">Paramètre</span><span class="sxs-lookup"><span data-stu-id="3bbec-151">Parameter</span></span> | <span data-ttu-id="3bbec-152">Description</span><span class="sxs-lookup"><span data-stu-id="3bbec-152">Description</span></span> | <span data-ttu-id="3bbec-153">Default</span><span class="sxs-lookup"><span data-stu-id="3bbec-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3bbec-154">Nom</span><span class="sxs-lookup"><span data-stu-id="3bbec-154">Name</span></span> |<span data-ttu-id="3bbec-155">Nom du cache de hello</span><span class="sxs-lookup"><span data-stu-id="3bbec-155">Name of hello cache</span></span> | |
| <span data-ttu-id="3bbec-156">Lieu</span><span class="sxs-lookup"><span data-stu-id="3bbec-156">Location</span></span> |<span data-ttu-id="3bbec-157">Emplacement du cache de hello</span><span class="sxs-lookup"><span data-stu-id="3bbec-157">Location of hello cache</span></span> | |
| <span data-ttu-id="3bbec-158">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="3bbec-158">ResourceGroupName</span></span> |<span data-ttu-id="3bbec-159">Nom de groupe de ressources dans le cache de hello toocreate</span><span class="sxs-lookup"><span data-stu-id="3bbec-159">Resource group name in which toocreate hello cache</span></span> | |
| <span data-ttu-id="3bbec-160">Taille</span><span class="sxs-lookup"><span data-stu-id="3bbec-160">Size</span></span> |<span data-ttu-id="3bbec-161">taille de Hello du cache de hello.</span><span class="sxs-lookup"><span data-stu-id="3bbec-161">hello size of hello cache.</span></span> <span data-ttu-id="3bbec-162">Les valeurs valides sont : P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250 Mo, 1 Go, 2,5 Go, 6 Go, 13 Go, 26 Go, 53 Go</span><span class="sxs-lookup"><span data-stu-id="3bbec-162">Valid values are: P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB</span></span> |<span data-ttu-id="3bbec-163">1 Go</span><span class="sxs-lookup"><span data-stu-id="3bbec-163">1GB</span></span> |
| <span data-ttu-id="3bbec-164">Nombre de partitions</span><span class="sxs-lookup"><span data-stu-id="3bbec-164">ShardCount</span></span> |<span data-ttu-id="3bbec-165">nombre de Hello de partitions toocreate lors de la création d’un cache premium avec activation des clusters.</span><span class="sxs-lookup"><span data-stu-id="3bbec-165">hello number of shards toocreate when creating a premium cache with clustering enabled.</span></span> <span data-ttu-id="3bbec-166">Les valeurs valides sont : 1, 2, 3, 4, 5, 6, 7, 8, 9, 10</span><span class="sxs-lookup"><span data-stu-id="3bbec-166">Valid values are: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10</span></span> | |
| <span data-ttu-id="3bbec-167">SKU</span><span class="sxs-lookup"><span data-stu-id="3bbec-167">SKU</span></span> |<span data-ttu-id="3bbec-168">Spécifie les hello référence (SKU) du cache de hello.</span><span class="sxs-lookup"><span data-stu-id="3bbec-168">Specifies hello SKU of hello cache.</span></span> <span data-ttu-id="3bbec-169">Les valeurs valides sont : De base, Standard, Premium</span><span class="sxs-lookup"><span data-stu-id="3bbec-169">Valid values are: Basic, Standard, Premium</span></span> |<span data-ttu-id="3bbec-170">Standard</span><span class="sxs-lookup"><span data-stu-id="3bbec-170">Standard</span></span> |
| <span data-ttu-id="3bbec-171">RedisConfiguration</span><span class="sxs-lookup"><span data-stu-id="3bbec-171">RedisConfiguration</span></span> |<span data-ttu-id="3bbec-172">Spécifie les paramètres de configuration de Redis.</span><span class="sxs-lookup"><span data-stu-id="3bbec-172">Specifies Redis configuration settings.</span></span> <span data-ttu-id="3bbec-173">Pour plus d’informations sur chaque paramètre, voir hello [RedisConfiguration propriétés](#redisconfiguration-properties) table.</span><span class="sxs-lookup"><span data-stu-id="3bbec-173">For details on each setting, see hello following [RedisConfiguration properties](#redisconfiguration-properties) table.</span></span> | |
| <span data-ttu-id="3bbec-174">enableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="3bbec-174">EnableNonSslPort</span></span> |<span data-ttu-id="3bbec-175">Indique si le port de hello non-SSL est activé.</span><span class="sxs-lookup"><span data-stu-id="3bbec-175">Indicates whether hello non-SSL port is enabled.</span></span> |<span data-ttu-id="3bbec-176">False</span><span class="sxs-lookup"><span data-stu-id="3bbec-176">False</span></span> |
| <span data-ttu-id="3bbec-177">MaxMemoryPolicy</span><span class="sxs-lookup"><span data-stu-id="3bbec-177">MaxMemoryPolicy</span></span> |<span data-ttu-id="3bbec-178">Ce paramètre est obsolète. Utilisez RedisConfiguration à la place.</span><span class="sxs-lookup"><span data-stu-id="3bbec-178">This parameter has been deprecated - use RedisConfiguration instead.</span></span> | |
| <span data-ttu-id="3bbec-179">StaticIP</span><span class="sxs-lookup"><span data-stu-id="3bbec-179">StaticIP</span></span> |<span data-ttu-id="3bbec-180">Lorsque vous hébergez votre cache dans un réseau virtuel, spécifie une adresse IP unique dans un sous-réseau hello pour le cache de hello.</span><span class="sxs-lookup"><span data-stu-id="3bbec-180">When hosting your cache in a VNET, specifies a unique IP address in hello subnet for hello cache.</span></span> <span data-ttu-id="3bbec-181">Si n’est fourni, une est choisie pour vous à partir du sous-réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="3bbec-181">If not provided, one is chosen for you from hello subnet.</span></span> | |
| <span data-ttu-id="3bbec-182">Sous-réseau</span><span class="sxs-lookup"><span data-stu-id="3bbec-182">Subnet</span></span> |<span data-ttu-id="3bbec-183">Lorsque vous hébergez votre cache dans un réseau virtuel, spécifie le nom hello du sous-réseau de hello dans le cache de hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="3bbec-183">When hosting your cache in a VNET, specifies hello name of hello subnet in which toodeploy hello cache.</span></span> | |
| <span data-ttu-id="3bbec-184">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="3bbec-184">VirtualNetwork</span></span> |<span data-ttu-id="3bbec-185">Lorsque votre cache dans un réseau virtuel, d’hébergement spécifie hello les ID de ressource de hello réseau virtuel dans le cache de hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="3bbec-185">When hosting your cache in a VNET, specifies hello resource ID of hello VNET in which toodeploy hello cache.</span></span> | |
| <span data-ttu-id="3bbec-186">KeyType</span><span class="sxs-lookup"><span data-stu-id="3bbec-186">KeyType</span></span> |<span data-ttu-id="3bbec-187">Spécifie la clé d’accès tooregenerate lors du renouvellement de clés d’accès.</span><span class="sxs-lookup"><span data-stu-id="3bbec-187">Specifies which access key tooregenerate when renewing access keys.</span></span> <span data-ttu-id="3bbec-188">Les valeurs valides sont : Primaire, Secondaire</span><span class="sxs-lookup"><span data-stu-id="3bbec-188">Valid values are: Primary, Secondary</span></span> | |

### <a name="redisconfiguration-properties"></a><span data-ttu-id="3bbec-189">Propriétés RedisConfiguration</span><span class="sxs-lookup"><span data-stu-id="3bbec-189">RedisConfiguration properties</span></span>
| <span data-ttu-id="3bbec-190">Propriété</span><span class="sxs-lookup"><span data-stu-id="3bbec-190">Property</span></span> | <span data-ttu-id="3bbec-191">Description</span><span class="sxs-lookup"><span data-stu-id="3bbec-191">Description</span></span> | <span data-ttu-id="3bbec-192">Niveaux de tarification</span><span class="sxs-lookup"><span data-stu-id="3bbec-192">Pricing tiers</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3bbec-193">rdb-backup-enabled</span><span class="sxs-lookup"><span data-stu-id="3bbec-193">rdb-backup-enabled</span></span> |<span data-ttu-id="3bbec-194">Indique si [la persistance des données Redis](cache-how-to-premium-persistence.md) est activée</span><span class="sxs-lookup"><span data-stu-id="3bbec-194">Whether [Redis data persistence](cache-how-to-premium-persistence.md) is enabled</span></span> |<span data-ttu-id="3bbec-195">Premium uniquement</span><span class="sxs-lookup"><span data-stu-id="3bbec-195">Premium only</span></span> |
| <span data-ttu-id="3bbec-196">rdb-storage-connection-string</span><span class="sxs-lookup"><span data-stu-id="3bbec-196">rdb-storage-connection-string</span></span> |<span data-ttu-id="3bbec-197">Hello compte de stockage de toohello de chaîne de connexion pour [Redis la persistance des données](cache-how-to-premium-persistence.md)</span><span class="sxs-lookup"><span data-stu-id="3bbec-197">hello connection string toohello storage account for [Redis data persistence](cache-how-to-premium-persistence.md)</span></span> |<span data-ttu-id="3bbec-198">Premium uniquement</span><span class="sxs-lookup"><span data-stu-id="3bbec-198">Premium only</span></span> |
| <span data-ttu-id="3bbec-199">rdb-backup-frequency</span><span class="sxs-lookup"><span data-stu-id="3bbec-199">rdb-backup-frequency</span></span> |<span data-ttu-id="3bbec-200">Hello fréquence de sauvegarde pour [Redis la persistance des données](cache-how-to-premium-persistence.md)</span><span class="sxs-lookup"><span data-stu-id="3bbec-200">hello backup frequency for [Redis data persistence](cache-how-to-premium-persistence.md)</span></span> |<span data-ttu-id="3bbec-201">Premium uniquement</span><span class="sxs-lookup"><span data-stu-id="3bbec-201">Premium only</span></span> |
| <span data-ttu-id="3bbec-202">maxmemory-reserved</span><span class="sxs-lookup"><span data-stu-id="3bbec-202">maxmemory-reserved</span></span> |<span data-ttu-id="3bbec-203">Configure hello [mémoire réservée](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) pour les processus non mises en cache</span><span class="sxs-lookup"><span data-stu-id="3bbec-203">Configures hello [memory reserved](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) for non-cache processes</span></span> |<span data-ttu-id="3bbec-204">Standard et Premium</span><span class="sxs-lookup"><span data-stu-id="3bbec-204">Standard and Premium</span></span> |
| <span data-ttu-id="3bbec-205">maxmemory-policy</span><span class="sxs-lookup"><span data-stu-id="3bbec-205">maxmemory-policy</span></span> |<span data-ttu-id="3bbec-206">Configure hello [stratégie d’éviction](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) pour cache de hello</span><span class="sxs-lookup"><span data-stu-id="3bbec-206">Configures hello [eviction policy](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) for hello cache</span></span> |<span data-ttu-id="3bbec-207">Tous les niveaux de tarification</span><span class="sxs-lookup"><span data-stu-id="3bbec-207">All pricing tiers</span></span> |
| <span data-ttu-id="3bbec-208">notify-keyspace-events</span><span class="sxs-lookup"><span data-stu-id="3bbec-208">notify-keyspace-events</span></span> |<span data-ttu-id="3bbec-209">Configure les [notifications d’espace de clés](cache-configure.md#keyspace-notifications-advanced-settings)</span><span class="sxs-lookup"><span data-stu-id="3bbec-209">Configures [keyspace notifications](cache-configure.md#keyspace-notifications-advanced-settings)</span></span> |<span data-ttu-id="3bbec-210">Standard et Premium</span><span class="sxs-lookup"><span data-stu-id="3bbec-210">Standard and Premium</span></span> |
| <span data-ttu-id="3bbec-211">hash-max-ziplist-entries</span><span class="sxs-lookup"><span data-stu-id="3bbec-211">hash-max-ziplist-entries</span></span> |<span data-ttu-id="3bbec-212">Configure [l’optimisation de la mémoire](http://redis.io/topics/memory-optimization) pour les petites quantités de types de données agrégées</span><span class="sxs-lookup"><span data-stu-id="3bbec-212">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="3bbec-213">Standard et Premium</span><span class="sxs-lookup"><span data-stu-id="3bbec-213">Standard and Premium</span></span> |
| <span data-ttu-id="3bbec-214">hash-max-ziplist-value</span><span class="sxs-lookup"><span data-stu-id="3bbec-214">hash-max-ziplist-value</span></span> |<span data-ttu-id="3bbec-215">Configure [l’optimisation de la mémoire](http://redis.io/topics/memory-optimization) pour les petites quantités de types de données agrégées</span><span class="sxs-lookup"><span data-stu-id="3bbec-215">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="3bbec-216">Standard et Premium</span><span class="sxs-lookup"><span data-stu-id="3bbec-216">Standard and Premium</span></span> |
| <span data-ttu-id="3bbec-217">set-max-intset-entries</span><span class="sxs-lookup"><span data-stu-id="3bbec-217">set-max-intset-entries</span></span> |<span data-ttu-id="3bbec-218">Configure [l’optimisation de la mémoire](http://redis.io/topics/memory-optimization) pour les petites quantités de types de données agrégées</span><span class="sxs-lookup"><span data-stu-id="3bbec-218">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="3bbec-219">Standard et Premium</span><span class="sxs-lookup"><span data-stu-id="3bbec-219">Standard and Premium</span></span> |
| <span data-ttu-id="3bbec-220">zset-max-ziplist-entries</span><span class="sxs-lookup"><span data-stu-id="3bbec-220">zset-max-ziplist-entries</span></span> |<span data-ttu-id="3bbec-221">Configure [l’optimisation de la mémoire](http://redis.io/topics/memory-optimization) pour les petites quantités de types de données agrégées</span><span class="sxs-lookup"><span data-stu-id="3bbec-221">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="3bbec-222">Standard et Premium</span><span class="sxs-lookup"><span data-stu-id="3bbec-222">Standard and Premium</span></span> |
| <span data-ttu-id="3bbec-223">zset-max-ziplist-value</span><span class="sxs-lookup"><span data-stu-id="3bbec-223">zset-max-ziplist-value</span></span> |<span data-ttu-id="3bbec-224">Configure [l’optimisation de la mémoire](http://redis.io/topics/memory-optimization) pour les petites quantités de types de données agrégées</span><span class="sxs-lookup"><span data-stu-id="3bbec-224">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="3bbec-225">Standard et Premium</span><span class="sxs-lookup"><span data-stu-id="3bbec-225">Standard and Premium</span></span> |
| <span data-ttu-id="3bbec-226">bases de données</span><span class="sxs-lookup"><span data-stu-id="3bbec-226">databases</span></span> |<span data-ttu-id="3bbec-227">Configure le nombre de hello de bases de données.</span><span class="sxs-lookup"><span data-stu-id="3bbec-227">Configures hello number of databases.</span></span> <span data-ttu-id="3bbec-228">Cette propriété ne peut être configurée qu’au moment de la création du cache.</span><span class="sxs-lookup"><span data-stu-id="3bbec-228">This property can be configured only at cache creation.</span></span> |<span data-ttu-id="3bbec-229">Standard et Premium</span><span class="sxs-lookup"><span data-stu-id="3bbec-229">Standard and Premium</span></span> |

## <a name="toocreate-a-redis-cache"></a><span data-ttu-id="3bbec-230">toocreate un Cache Redis</span><span class="sxs-lookup"><span data-stu-id="3bbec-230">toocreate a Redis Cache</span></span>
<span data-ttu-id="3bbec-231">Nouvelle instance de Cache Redis Azure est créée à l’aide de hello [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="3bbec-231">New Azure Redis Cache instances are created using hello [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3bbec-232">Hello lors de la création d’un cache Redis dans un abonnement à l’aide de hello portail Azure, le portail de hello inscrit hello `Microsoft.Cache` espace de noms pour cet abonnement.</span><span class="sxs-lookup"><span data-stu-id="3bbec-232">hello first time you create a Redis cache in a subscription using hello Azure portal, hello portal registers hello `Microsoft.Cache` namespace for that subscription.</span></span> <span data-ttu-id="3bbec-233">Si vous essayez toocreate hello Redis tout d’abord le cache d’un abonnement à l’aide de PowerShell, vous devez d’abord inscrire cet espace de noms à l’aide de hello suivant de commande ; applets de commande sinon comme `New-AzureRmRedisCache` et `Get-AzureRmRedisCache` échouent.</span><span class="sxs-lookup"><span data-stu-id="3bbec-233">If you attempt toocreate hello first Redis cache in a subscription using PowerShell, you must first register that namespace using hello following command; otherwise cmdlets such as `New-AzureRmRedisCache` and `Get-AzureRmRedisCache` fail.</span></span>
> 
> `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Cache"`
> 
> 

<span data-ttu-id="3bbec-234">toosee une liste des paramètres disponibles et leurs descriptions pour `New-AzureRmRedisCache`, exécutez hello après une commande.</span><span class="sxs-lookup"><span data-stu-id="3bbec-234">toosee a list of available parameters and their descriptions for `New-AzureRmRedisCache`, run hello following command.</span></span>

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
        hello New-AzureRmRedisCache cmdlet creates a new redis cache.


    PARAMETERS
        -Name <String>
            Name of hello redis cache toocreate.

        -ResourceGroupName <String>
            Name of resource group in which toocreate hello redis cache.

        -Location <String>
            Location in which toocreate hello redis cache.

        -RedisVersion <String>
            RedisVersion is deprecated and will be removed in future release.

        -Size <String>
            Size of hello redis cache. hello default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. hello default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            hello 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting tooset
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value, databases.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. If no value is provided, hello default value is false and the
            non-SSL port will be disabled. Possible values are true and false.

        -ShardCount <Integer>
            hello number of shards toocreate on a Premium Cluster Cache.

        -VirtualNetwork <String>
            hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in. Example format: /subscriptions/{
            subid}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicNetwork/VirtualNetworks/{vnetName}

        -Subnet <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        -StaticIP <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="3bbec-235">toocreate un cache avec les paramètres par défaut, exécutez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="3bbec-235">toocreate a cache with default parameters, run hello following command.</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US"

<span data-ttu-id="3bbec-236">`ResourceGroupName`, `Name`, et `Location` sont des paramètres obligatoires, mais le reste de hello sont facultative et leurs valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="3bbec-236">`ResourceGroupName`, `Name`, and `Location` are required parameters, but hello rest are optional and have default values.</span></span> <span data-ttu-id="3bbec-237">Exécute la commande précédente hello de crée une instance Standard référence (SKU) du Cache Redis Azure avec le nom spécifié de hello, l’emplacement et groupe de ressources, qui est de 1 Go de taille avec hello non-SSL port est désactivé.</span><span class="sxs-lookup"><span data-stu-id="3bbec-237">Running hello previous command creates a Standard SKU Azure Redis Cache instance with hello specified name, location, and resource group, that is 1 GB in size with hello non-SSL port disabled.</span></span>

<span data-ttu-id="3bbec-238">toocreate un cache premium, spécifiez une taille de P1 (6 Go - 60 Go), P2 (13 à 130 Go), P3 (26 à 260 Go), ou P4 (53 à 530 Go).</span><span class="sxs-lookup"><span data-stu-id="3bbec-238">toocreate a premium cache, specify a size of P1 (6 GB - 60 GB), P2 (13 GB - 130 GB), P3 (26 GB - 260 GB), or P4 (53 GB - 530 GB).</span></span> <span data-ttu-id="3bbec-239">tooenable clustering, spécifiez un nombre de partitions à l’aide de hello `ShardCount` paramètre.</span><span class="sxs-lookup"><span data-stu-id="3bbec-239">tooenable clustering, specify a shard count using hello `ShardCount` parameter.</span></span> <span data-ttu-id="3bbec-240">Hello exemple suivant crée un cache premium de P1 avec 3 partitions.</span><span class="sxs-lookup"><span data-stu-id="3bbec-240">hello following example creates a P1 premium cache with 3 shards.</span></span> <span data-ttu-id="3bbec-241">Un cache premium de P1 est de 6 Go de taille, et étant donné que nous avons spécifié trois partitions hello taille totale est 18 (3 x 6 Go).</span><span class="sxs-lookup"><span data-stu-id="3bbec-241">A P1 premium cache is 6 GB in size, and since we specified three shards hello total size is 18 GB (3 x 6 GB).</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P1 -ShardCount 3

<span data-ttu-id="3bbec-242">valeurs toospecify pour hello `RedisConfiguration` paramètre, placer les valeurs à l’intérieur de hello `{}` en tant que clé/valeur comme paires `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`.</span><span class="sxs-lookup"><span data-stu-id="3bbec-242">toospecify values for hello `RedisConfiguration` parameter, enclose hello values inside `{}` as key/value pairs like `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`.</span></span> <span data-ttu-id="3bbec-243">Hello exemple suivant crée un cache de 1 Go standard avec `allkeys-random` maxmemory de stratégie et d’espace de clés les notifications configurées avec `KEA`.</span><span class="sxs-lookup"><span data-stu-id="3bbec-243">hello following example creates a standard 1 GB cache with `allkeys-random` maxmemory policy and keyspace notifications configured with `KEA`.</span></span> <span data-ttu-id="3bbec-244">Pour plus d’informations, voir [Notifications de keyspace (paramètres avancés)](cache-configure.md#keyspace-notifications-advanced-settings) et [Stratégies de mémoire](cache-configure.md#memory-policies).</span><span class="sxs-lookup"><span data-stu-id="3bbec-244">For more information, see [Keyspace notifications (advanced settings)](cache-configure.md#keyspace-notifications-advanced-settings) and [Memory policies](cache-configure.md#memory-policies).</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}

<a name="databases"></a>

## <a name="tooconfigure-hello-databases-setting-during-cache-creation"></a><span data-ttu-id="3bbec-245">tooconfigure hello paramètre bases de données lors de la création du cache</span><span class="sxs-lookup"><span data-stu-id="3bbec-245">tooconfigure hello databases setting during cache creation</span></span>
<span data-ttu-id="3bbec-246">Hello `databases` paramètre peut être configuré uniquement pendant la création du cache.</span><span class="sxs-lookup"><span data-stu-id="3bbec-246">hello `databases` setting can be configured only during cache creation.</span></span> <span data-ttu-id="3bbec-247">Hello exemple suivant crée un premium P3 (26 Go) de cache avec 48 bases de données à l’aide de hello [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="3bbec-247">hello following example creates a premium P3 (26 GB) cache with 48 databases using hello [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P3 -RedisConfiguration @{"databases" = "48"}

<span data-ttu-id="3bbec-248">Pour plus d’informations sur hello `databases` propriété, consultez [configuration du serveur par défaut le Cache Redis Azure](cache-configure.md#default-redis-server-configuration).</span><span class="sxs-lookup"><span data-stu-id="3bbec-248">For more information on hello `databases` property, see [Default Azure Redis Cache server configuration](cache-configure.md#default-redis-server-configuration).</span></span> <span data-ttu-id="3bbec-249">Pour plus d’informations sur la création d’un cache à l’aide de hello [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) applet de commande, consultez hello précédente [toocreate un Cache Redis](#to-create-a-redis-cache) section.</span><span class="sxs-lookup"><span data-stu-id="3bbec-249">For more information on creating a cache using hello [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet, see hello previous [toocreate a Redis Cache](#to-create-a-redis-cache) section.</span></span>

## <a name="tooupdate-a-redis-cache"></a><span data-ttu-id="3bbec-250">tooupdate un cache Redis</span><span class="sxs-lookup"><span data-stu-id="3bbec-250">tooupdate a Redis cache</span></span>
<span data-ttu-id="3bbec-251">Les instances de Cache Redis Azure sont mis à jour à l’aide de hello [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="3bbec-251">Azure Redis Cache instances are updated using hello [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet.</span></span>

<span data-ttu-id="3bbec-252">toosee une liste des paramètres disponibles et leurs descriptions pour `Set-AzureRmRedisCache`, exécutez hello après une commande.</span><span class="sxs-lookup"><span data-stu-id="3bbec-252">toosee a list of available parameters and their descriptions for `Set-AzureRmRedisCache`, run hello following command.</span></span>

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
        hello Set-AzureRmRedisCache cmdlet sets redis cache parameters.

    PARAMETERS
        -Name <String>
            Name of hello redis cache tooupdate.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        -Size <String>
            Size of hello redis cache. hello default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. hello default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            hello 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting tooset
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. hello default value is null and no change will be made toothe
            currently configured value. Possible values are true and false.

        -ShardCount <Integer>
            hello number of shards toocreate on a Premium Cluster Cache.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="3bbec-253">Hello `Set-AzureRmRedisCache` applet de commande peut être utilisé tooupdate des propriétés, telles que `Size`, `Sku`, `EnableNonSslPort`et hello `RedisConfiguration` valeurs.</span><span class="sxs-lookup"><span data-stu-id="3bbec-253">hello `Set-AzureRmRedisCache` cmdlet can be used tooupdate properties such as `Size`, `Sku`, `EnableNonSslPort`, and hello `RedisConfiguration` values.</span></span> 

<span data-ttu-id="3bbec-254">Hello commande suivante, les mises à jour hello maxmemory-policy pour hello Cache Redis nommé myCache.</span><span class="sxs-lookup"><span data-stu-id="3bbec-254">hello following command updates hello maxmemory-policy for hello Redis Cache named myCache.</span></span>

    Set-AzureRmRedisCache -ResourceGroupName "myGroup" -Name "myCache" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random"}

<a name="scale"></a>

## <a name="tooscale-a-redis-cache"></a><span data-ttu-id="3bbec-255">tooscale un cache Redis</span><span class="sxs-lookup"><span data-stu-id="3bbec-255">tooscale a Redis cache</span></span>
<span data-ttu-id="3bbec-256">`Set-AzureRmRedisCache`peut être utilisé tooscale une instance de cache Redis Azure lorsque hello `Size`, `Sku`, ou `ShardCount` propriétés sont modifiées.</span><span class="sxs-lookup"><span data-stu-id="3bbec-256">`Set-AzureRmRedisCache` can be used tooscale an Azure Redis cache instance when hello `Size`, `Sku`, or `ShardCount` properties are modified.</span></span> 

> [!NOTE]
> <span data-ttu-id="3bbec-257">Mise à l’échelle un cache à l’aide de PowerShell est sujet toohello mêmes limites et des recommandations en tant que la mise à l’échelle un cache à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3bbec-257">Scaling a cache using PowerShell is subject toohello same limits and guidelines as scaling a cache from hello Azure portal.</span></span> <span data-ttu-id="3bbec-258">Vous pouvez faire évoluer tooa autre niveau de tarification par hello suivant des restrictions.</span><span class="sxs-lookup"><span data-stu-id="3bbec-258">You can scale tooa different pricing tier with hello following restrictions.</span></span>
> 
> * <span data-ttu-id="3bbec-259">Vous ne pouvez pas mettre à l’échelle à partir d’un tooa niveau tarifaire la plus élevée plus faible niveau de tarification.</span><span class="sxs-lookup"><span data-stu-id="3bbec-259">You can't scale from a higher pricing tier tooa lower pricing tier.</span></span>
> * <span data-ttu-id="3bbec-260">Vous ne pouvez pas mettre à l’échelle à partir d’un **Premium** cache vers le bas tooa **Standard** ou un **base** cache.</span><span class="sxs-lookup"><span data-stu-id="3bbec-260">You can't scale from a **Premium** cache down tooa **Standard** or a **Basic** cache.</span></span>
> * <span data-ttu-id="3bbec-261">Vous ne pouvez pas mettre à l’échelle à partir d’un **Standard** cache vers le bas tooa **base** cache.</span><span class="sxs-lookup"><span data-stu-id="3bbec-261">You can't scale from a **Standard** cache down tooa **Basic** cache.</span></span>
> * <span data-ttu-id="3bbec-262">Vous pouvez mettre à l’échelle d’un **base** cache tooa **Standard** cache, mais que vous ne pouvez pas modifier la taille de hello en hello même temps.</span><span class="sxs-lookup"><span data-stu-id="3bbec-262">You can scale from a **Basic** cache tooa **Standard** cache but you can't change hello size at hello same time.</span></span> <span data-ttu-id="3bbec-263">Si vous avez besoin d’une taille différente, vous pouvez effectuer une taille suivantes toohello souhaité d’opération mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="3bbec-263">If you need a different size, you can do a subsequent scaling operation toohello desired size.</span></span>
> * <span data-ttu-id="3bbec-264">Vous ne pouvez pas mettre à l’échelle à partir d’un **base** mettre en cache directement tooa **Premium** cache.</span><span class="sxs-lookup"><span data-stu-id="3bbec-264">You can't scale from a **Basic** cache directly tooa **Premium** cache.</span></span> <span data-ttu-id="3bbec-265">Vous devez mettre à l’échelle à partir de **base** trop**Standard** en une seule opération de mise à l’échelle, puis de **Standard** trop**Premium** dans une mise à l’échelle suivantes opération.</span><span class="sxs-lookup"><span data-stu-id="3bbec-265">You must scale from **Basic** too**Standard** in one scaling operation, and then from **Standard** too**Premium** in a subsequent scaling operation.</span></span>
> * <span data-ttu-id="3bbec-266">Vous ne peut pas mettre à l’échelle à partir d’une plus grande taille vers le bas toohello **C0 (250 Mo)** taille.</span><span class="sxs-lookup"><span data-stu-id="3bbec-266">You can't scale from a larger size down toohello **C0 (250 MB)** size.</span></span>
> 
> <span data-ttu-id="3bbec-267">Pour plus d’informations, consultez [comment tooScale Cache Redis Azure](cache-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="3bbec-267">For more information, see [How tooScale Azure Redis Cache](cache-how-to-scale.md).</span></span>
> 
> 

<span data-ttu-id="3bbec-268">Hello suivant montre comment tooscale un cache nommé `myCache` tooa 2,5 Go de cache.</span><span class="sxs-lookup"><span data-stu-id="3bbec-268">hello following example shows how tooscale a cache named `myCache` tooa 2.5 GB cache.</span></span> <span data-ttu-id="3bbec-269">Notez que cette commande fonctionne pour un cache De base ou un cache Standard.</span><span class="sxs-lookup"><span data-stu-id="3bbec-269">Note that this command works for both a Basic or a Standard cache.</span></span>

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

<span data-ttu-id="3bbec-270">Une fois cette commande est émise, état hello du cache de hello est retourné (similaire toocalling `Get-AzureRmRedisCache`).</span><span class="sxs-lookup"><span data-stu-id="3bbec-270">After this command is issued, hello status of hello cache is returned (similar toocalling `Get-AzureRmRedisCache`).</span></span> <span data-ttu-id="3bbec-271">Notez que hello `ProvisioningState` est `Scaling`.</span><span class="sxs-lookup"><span data-stu-id="3bbec-271">Note that hello `ProvisioningState` is `Scaling`.</span></span>

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

<span data-ttu-id="3bbec-272">Lorsque hello mise à l’échelle d’opération est terminée, hello `ProvisioningState` change également`Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="3bbec-272">When hello scaling operation is complete, hello `ProvisioningState` changes too`Succeeded`.</span></span> <span data-ttu-id="3bbec-273">Si vous avez besoin de toomake une opération de mise à l’échelle suivante, telles que la modification de base tooStandard et puis taille de hello, vous devez attendre jusqu'à ce que l’opération précédente hello est terminée ou vous recevez un suivant de toohello erreur similaire.</span><span class="sxs-lookup"><span data-stu-id="3bbec-273">If you need toomake a subsequent scaling operation, such as changing from Basic tooStandard and then changing hello size, you must wait until hello previous operation is complete or you receive an error similar toohello following.</span></span>

    Set-AzureRmRedisCache : Conflict: hello resource '...' is not in a stable state, and is currently unable tooaccept hello update request.

## <a name="tooget-information-about-a-redis-cache"></a><span data-ttu-id="3bbec-274">informations de tooget sur un cache Redis</span><span class="sxs-lookup"><span data-stu-id="3bbec-274">tooget information about a Redis cache</span></span>
<span data-ttu-id="3bbec-275">Vous pouvez récupérer des informations sur un cache à l’aide de hello [Get-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634514.aspx) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="3bbec-275">You can retrieve information about a cache using hello [Get-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634514.aspx) cmdlet.</span></span>

<span data-ttu-id="3bbec-276">toosee une liste des paramètres disponibles et leurs descriptions pour `Get-AzureRmRedisCache`, exécutez hello après une commande.</span><span class="sxs-lookup"><span data-stu-id="3bbec-276">toosee a list of available parameters and their descriptions for `Get-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Get-AzureRmRedisCache -detailed

    NAME
        Get-AzureRmRedisCache

    SYNOPSIS
        Gets details about a single cache or all caches in hello specified resource group or all caches in hello current
        subscription.

    SYNTAX
        Get-AzureRmRedisCache [-Name <String>] [-ResourceGroupName <String>] [<CommonParameters>]

    DESCRIPTION
        hello Get-AzureRmRedisCache cmdlet gets hello details about a cache or caches depending on input parameters. If both
        ResourceGroupName and Name parameters are provided then Get-AzureRmRedisCache will return details about the
        specific cache name provided.

        If only ResourceGroupName is provided than it will return details about all caches in hello specified resource group.

        If no parameters are given than it will return details about all caches hello current subscription.

    PARAMETERS
        -Name <String>
            hello name of hello cache. When this parameter is provided along with ResourceGroupName, Get-AzureRmRedisCache
            returns hello details for hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache or caches. If ResourceGroupName is provided with Name
            then Get-AzureRmRedisCache returns hello details of hello cache specified by Name. If only hello ResourceGroup
            parameter is provided, then details for all caches in hello resource group are returned.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="3bbec-277">tooreturn plus d’informations sur tous les caches de l’abonnement actuel de hello, exécutez `Get-AzureRmRedisCache` sans aucun paramètre.</span><span class="sxs-lookup"><span data-stu-id="3bbec-277">tooreturn information about all caches in hello current subscription, run `Get-AzureRmRedisCache` without any parameters.</span></span>

    Get-AzureRmRedisCache

<span data-ttu-id="3bbec-278">tooreturn plus d’informations sur tous les caches dans le groupe de ressources spécifique, exécutez `Get-AzureRmRedisCache` avec hello `ResourceGroupName` paramètre.</span><span class="sxs-lookup"><span data-stu-id="3bbec-278">tooreturn information about all caches in a specific resource group, run `Get-AzureRmRedisCache` with hello `ResourceGroupName` parameter.</span></span>

    Get-AzureRmRedisCache -ResourceGroupName myGroup

<span data-ttu-id="3bbec-279">tooreturn plus d’informations sur un cache en particulier, exécutez `Get-AzureRmRedisCache` avec hello `Name` paramètre contenant le nom hello du cache de hello et hello `ResourceGroupName` paramètre avec le groupe de ressources hello contenant ce cache.</span><span class="sxs-lookup"><span data-stu-id="3bbec-279">tooreturn information about a specific cache, run `Get-AzureRmRedisCache` with hello `Name` parameter containing hello name of hello cache, and hello `ResourceGroupName` parameter with hello resource group containing that cache.</span></span>

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

## <a name="tooretrieve-hello-access-keys-for-a-redis-cache"></a><span data-ttu-id="3bbec-280">touches d’accès tooretrieve hello pour un cache Redis</span><span class="sxs-lookup"><span data-stu-id="3bbec-280">tooretrieve hello access keys for a Redis cache</span></span>
<span data-ttu-id="3bbec-281">touches d’accès tooretrieve hello pour votre cache, vous pouvez utiliser hello [Get-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634516.aspx) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="3bbec-281">tooretrieve hello access keys for your cache, you can use hello [Get-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634516.aspx) cmdlet.</span></span>

<span data-ttu-id="3bbec-282">toosee une liste des paramètres disponibles et leurs descriptions pour `Get-AzureRmRedisCacheKey`, exécutez hello après une commande.</span><span class="sxs-lookup"><span data-stu-id="3bbec-282">toosee a list of available parameters and their descriptions for `Get-AzureRmRedisCacheKey`, run hello following command.</span></span>

    PS C:\> Get-Help Get-AzureRmRedisCacheKey -detailed

    NAME
        Get-AzureRmRedisCacheKey

    SYNOPSIS
        Gets hello accesskeys for hello specified redis cache.


    SYNTAX
        Get-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> [<CommonParameters>]

    DESCRIPTION
        hello Get-AzureRmRedisCacheKey cmdlet gets hello access keys for hello specified cache.

    PARAMETERS
        -Name <String>
            Name of hello redis cache.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="3bbec-283">tooretrieve hello clés pour votre cache, appel hello `Get-AzureRmRedisCacheKey` applet de commande et passez nom hello de votre cache hello nom hello du groupe de ressources qui contient le cache de hello.</span><span class="sxs-lookup"><span data-stu-id="3bbec-283">tooretrieve hello keys for your cache, call hello `Get-AzureRmRedisCacheKey` cmdlet and pass in hello name of your cache hello name of hello resource group that contains hello cache.</span></span>

    PS C:\> Get-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup

    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : ABhfB757JgjIgt785JgKH9865eifmekfnn649303JKL=

## <a name="tooregenerate-access-keys-for-your-redis-cache"></a><span data-ttu-id="3bbec-284">touches d’accès tooregenerate pour votre cache Redis</span><span class="sxs-lookup"><span data-stu-id="3bbec-284">tooregenerate access keys for your Redis cache</span></span>
<span data-ttu-id="3bbec-285">touches d’accès tooregenerate hello pour votre cache, vous pouvez utiliser hello [New-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634512.aspx) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="3bbec-285">tooregenerate hello access keys for your cache, you can use hello [New-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634512.aspx) cmdlet.</span></span>

<span data-ttu-id="3bbec-286">toosee une liste des paramètres disponibles et leurs descriptions pour `New-AzureRmRedisCacheKey`, exécutez hello après une commande.</span><span class="sxs-lookup"><span data-stu-id="3bbec-286">toosee a list of available parameters and their descriptions for `New-AzureRmRedisCacheKey`, run hello following command.</span></span>

    PS C:\> Get-Help New-AzureRmRedisCacheKey -detailed

    NAME
        New-AzureRmRedisCacheKey

    SYNOPSIS
        Regenerates hello access key of a redis cache.

    SYNTAX
        New-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> -KeyType <String> [-Force] [<CommonParameters>]

    DESCRIPTION
        hello New-AzureRmRedisCacheKey cmdlet regenerate hello access key of a redis cache.

    PARAMETERS
        -Name <String>
            Name of hello redis cache.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        -KeyType <String>
            Specifies whether tooregenerate hello primary or secondary access key. Possible values are Primary or Secondary.

        -Force
            When hello Force parameter is provided, hello specified access key is regenerated without any confirmation prompts.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="3bbec-287">clé de principale ou secondaire de hello pour votre cache, appel hello tooregenerate `New-AzureRmRedisCacheKey` applet de commande et passez hello nom, groupe de ressources et spécifier `Primary` ou `Secondary` pour hello `KeyType` paramètre.</span><span class="sxs-lookup"><span data-stu-id="3bbec-287">tooregenerate hello primary or secondary key for your cache, call hello `New-AzureRmRedisCacheKey` cmdlet and pass in hello name, resource group, and specify either `Primary` or `Secondary` for hello `KeyType` parameter.</span></span> <span data-ttu-id="3bbec-288">Bonjour l’exemple suivant, la clé d’accès secondaire hello pour un cache est régénéré.</span><span class="sxs-lookup"><span data-stu-id="3bbec-288">In hello following example, hello secondary access key for a cache is regenerated.</span></span>

    PS C:\> New-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup -KeyType Secondary

    Confirm
    Are you sure you want tooregenerate Secondary key for redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : c53hj3kh4jhHjPJk8l0jji785JgKH9865eifmekfnn6=

## <a name="toodelete-a-redis-cache"></a><span data-ttu-id="3bbec-289">toodelete un cache Redis</span><span class="sxs-lookup"><span data-stu-id="3bbec-289">toodelete a Redis cache</span></span>
<span data-ttu-id="3bbec-290">toodelete un cache Redis, utilisez hello [Remove-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634515.aspx) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="3bbec-290">toodelete a Redis cache, use hello [Remove-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634515.aspx) cmdlet.</span></span>

<span data-ttu-id="3bbec-291">toosee une liste des paramètres disponibles et leurs descriptions pour `Remove-AzureRmRedisCache`, exécutez hello après une commande.</span><span class="sxs-lookup"><span data-stu-id="3bbec-291">toosee a list of available parameters and their descriptions for `Remove-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Remove-AzureRmRedisCache -detailed

    NAME
        Remove-AzureRmRedisCache

    SYNOPSIS
        Remove redis cache if exists.

    SYNTAX
        Remove-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Force] [-PassThru] [<CommonParameters>

    DESCRIPTION
        hello Remove-AzureRmRedisCache cmdlet removes a redis cache if it exists.

    PARAMETERS
        -Name <String>
            Name of hello redis cache tooremove.

        -ResourceGroupName <String>
            Name of hello resource group of hello cache tooremove.

        -Force
            When hello Force parameter is provided, hello cache is removed without any confirmation prompts.

        -PassThru
            By default Remove-AzureRmRedisCache removes hello cache and does not return any value. If hello PassThru par
            is provided then Remove-AzureRmRedisCache returns a boolean value indicating hello success of hello operatio

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="3bbec-292">Dans l’exemple suivant de hello, hello cache nommé `myCache` est supprimé.</span><span class="sxs-lookup"><span data-stu-id="3bbec-292">In hello following example, hello cache named `myCache` is removed.</span></span>

    PS C:\> Remove-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Confirm
    Are you sure you want tooremove redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


## <a name="tooimport-a-redis-cache"></a><span data-ttu-id="3bbec-293">tooimport un cache Redis</span><span class="sxs-lookup"><span data-stu-id="3bbec-293">tooimport a Redis cache</span></span>
<span data-ttu-id="3bbec-294">Vous pouvez importer des données dans une instance de Cache Redis Azure à l’aide de hello `Import-AzureRmRedisCache` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="3bbec-294">You can import data into an Azure Redis Cache instance using hello `Import-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3bbec-295">L’importation/exportation est uniquement disponible pour les caches de niveau [Premium](cache-premium-tier-intro.md) .</span><span class="sxs-lookup"><span data-stu-id="3bbec-295">Import/Export is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="3bbec-296">Pour plus d’informations sur l’importation/exportation, voir [Importer et exporter des données dans le cache Redis Azure](cache-how-to-import-export-data.md).</span><span class="sxs-lookup"><span data-stu-id="3bbec-296">For more information about Import/Export, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

<span data-ttu-id="3bbec-297">toosee une liste des paramètres disponibles et leurs descriptions pour `Import-AzureRmRedisCache`, exécutez hello après une commande.</span><span class="sxs-lookup"><span data-stu-id="3bbec-297">toosee a list of available parameters and their descriptions for `Import-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Import-AzureRmRedisCache -detailed

    NAME
        Import-AzureRmRedisCache

    SYNOPSIS
        Import data from blobs tooAzure Redis Cache.


    SYNTAX
        Import-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Files <String[]> [-Format <String>] [-Force]
        [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Import-AzureRmRedisCache cmdlet imports data from hello specified blobs into Azure Redis Cache.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -Files <String[]>
            SAS urls of blobs whose content should be imported into hello cache.

        -Format <String>
            Format for hello blob.  Currently "rdb" is hello only supported, with other formats expected in hello future.

        -Force
            When hello Force parameter is provided, import will be performed without any confirmation prompts.

        -PassThru
            By default Import-AzureRmRedisCache imports data in cache and does not return any value. If hello PassThru
            parameter is provided then Import-AzureRmRedisCache returns a boolean value indicating hello success of the
            operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="3bbec-298">Hello commande suivante importe les données d’objet blob de hello spécifié par l’uri SAS hello dans le Cache Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="3bbec-298">hello following command imports data from hello blob specified by hello SAS uri into Azure Redis Cache.</span></span>

    PS C:\>Import-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Files @("https://mystorageaccount.blob.core.windows.net/mycontainername/blobname?sv=2015-04-05&sr=b&sig=caIwutG2uDa0NZ8mjdNJdgOY8%2F8mhwRuGNdICU%2B0pI4%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwd") -Force

## <a name="tooexport-a-redis-cache"></a><span data-ttu-id="3bbec-299">tooexport un cache Redis</span><span class="sxs-lookup"><span data-stu-id="3bbec-299">tooexport a Redis cache</span></span>
<span data-ttu-id="3bbec-300">Vous pouvez exporter des données à partir d’une instance de Cache Redis Azure à l’aide de hello `Export-AzureRmRedisCache` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="3bbec-300">You can export data from an Azure Redis Cache instance using hello `Export-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3bbec-301">L’importation/exportation est uniquement disponible pour les caches de niveau [Premium](cache-premium-tier-intro.md) .</span><span class="sxs-lookup"><span data-stu-id="3bbec-301">Import/Export is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="3bbec-302">Pour plus d’informations sur l’importation/exportation, voir [Importer et exporter des données dans le cache Redis Azure](cache-how-to-import-export-data.md).</span><span class="sxs-lookup"><span data-stu-id="3bbec-302">For more information about Import/Export, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

<span data-ttu-id="3bbec-303">toosee une liste des paramètres disponibles et leurs descriptions pour `Export-AzureRmRedisCache`, exécutez hello après une commande.</span><span class="sxs-lookup"><span data-stu-id="3bbec-303">toosee a list of available parameters and their descriptions for `Export-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Export-AzureRmRedisCache -detailed

    NAME
        Export-AzureRmRedisCache

    SYNOPSIS
        Exports data from Azure Redis Cache tooa specified container.


    SYNTAX
        Export-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Prefix <String> -Container <String> [-Format
        <String>] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Export-AzureRmRedisCache cmdlet exports data from Azure Redis Cache tooa specified container.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -Prefix <String>
            Prefix toouse for blob names.

        -Container <String>
            SAS url of container where data should be exported.

        -Format <String>
            Format for hello blob.  Currently "rdb" is hello only supported, with other formats expected in hello future.

        -PassThru
            By default Export-AzureRmRedisCache does not return any value. If hello PassThru parameter is provided
            then Export-AzureRmRedisCache returns a boolean value indicating hello success of hello operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="3bbec-304">Hello commande suivante exporte les données à partir d’une instance de Cache Redis Azure dans le conteneur de hello spécifié par l’uri SAS hello.</span><span class="sxs-lookup"><span data-stu-id="3bbec-304">hello following command exports data from an Azure Redis Cache instance into hello container specified by hello SAS uri.</span></span>

        PS C:\>Export-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Prefix "blobprefix"
        -Container "https://mystorageaccount.blob.core.windows.net/mycontainer?sv=2015-04-05&sr=c&sig=HezZtBZ3DURmEGDduauE7
        pvETY4kqlPI8JCNa8ATmaw%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwdl"

## <a name="tooreboot-a-redis-cache"></a><span data-ttu-id="3bbec-305">tooreboot un cache Redis</span><span class="sxs-lookup"><span data-stu-id="3bbec-305">tooreboot a Redis cache</span></span>
<span data-ttu-id="3bbec-306">Vous pouvez redémarrer votre instance de Cache Redis Azure à l’aide de hello `Reset-AzureRmRedisCache` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="3bbec-306">You can reboot your Azure Redis Cache instance using hello `Reset-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3bbec-307">Le redémarrage est uniquement disponible pour les caches de [niveau Premium](cache-premium-tier-intro.md) .</span><span class="sxs-lookup"><span data-stu-id="3bbec-307">Reboot is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="3bbec-308">Pour plus d’informations sur le redémarrage de votre cache, voir [Administration du cache - Redémarrage](cache-administration.md#reboot).</span><span class="sxs-lookup"><span data-stu-id="3bbec-308">For more information about rebooting your cache, see [Cache administration - reboot](cache-administration.md#reboot).</span></span>
> 
> 

<span data-ttu-id="3bbec-309">toosee une liste des paramètres disponibles et leurs descriptions pour `Reset-AzureRmRedisCache`, exécutez hello après une commande.</span><span class="sxs-lookup"><span data-stu-id="3bbec-309">toosee a list of available parameters and their descriptions for `Reset-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Reset-AzureRmRedisCache -detailed

    NAME
        Reset-AzureRmRedisCache

    SYNOPSIS
        Reboot specified node(s) of an Azure Redis Cache instance.


    SYNTAX
        Reset-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -RebootType <String> [-ShardId <Integer>]
        [-Force] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Reset-AzureRmRedisCache cmdlet reboots hello specified node(s) of an Azure Redis Cache instance.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -RebootType <String>
            Which node tooreboot. Possible values are "PrimaryNode", "SecondaryNode", "AllNodes".

        -ShardId <Integer>
            Which shard tooreboot when rebooting a premium cache with clustering enabled.

        -Force
            When hello Force parameter is provided, reset will be performed without any confirmation prompts.

        -PassThru
            By default Reset-AzureRmRedisCache does not return any value. If hello PassThru parameter is provided
            then Reset-AzureRmRedisCache returns a boolean value indicating hello success of hello operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="3bbec-310">Hello commande suivante redémarre les deux nœuds de hello spécifié cache.</span><span class="sxs-lookup"><span data-stu-id="3bbec-310">hello following command reboots both nodes of hello specified cache.</span></span>

        PS C:\>Reset-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -RebootType "AllNodes"
        -Force


## <a name="next-steps"></a><span data-ttu-id="3bbec-311">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3bbec-311">Next steps</span></span>
<span data-ttu-id="3bbec-312">toolearn savoir plus sur l’utilisation de Windows PowerShell avec Azure, consultez hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="3bbec-312">toolearn more about using Windows PowerShell with Azure, see hello following resources:</span></span>

* [<span data-ttu-id="3bbec-313">Documentation relative à l’applet de commande Cache Redis Azure sur MSDN</span><span class="sxs-lookup"><span data-stu-id="3bbec-313">Azure Redis Cache cmdlet documentation on MSDN</span></span>](https://msdn.microsoft.com/library/azure/mt634513.aspx)
* <span data-ttu-id="3bbec-314">[Azure Resource Manager Cmdlets](http://go.microsoft.com/fwlink/?LinkID=394765): découvrir toouse hello applets de commande dans le module du Gestionnaire de ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="3bbec-314">[Azure Resource Manager Cmdlets](http://go.microsoft.com/fwlink/?LinkID=394765): Learn toouse hello cmdlets in hello Azure Resource Manager module.</span></span>
* <span data-ttu-id="3bbec-315">[À l’aide de la ressource groupes toomanage vos ressources Azure](../azure-resource-manager/resource-group-template-deploy-portal.md): Découvrez comment toocreate et gérer des groupes de ressources de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3bbec-315">[Using Resource groups toomanage your Azure resources](../azure-resource-manager/resource-group-template-deploy-portal.md): Learn how toocreate and manage resource groups in hello Azure portal.</span></span>
* <span data-ttu-id="3bbec-316">[Blog Azure](http://blogs.msdn.com/windowsazure): découvrez les nouvelles fonctionnalités d'Azure.</span><span class="sxs-lookup"><span data-stu-id="3bbec-316">[Azure blog](http://blogs.msdn.com/windowsazure): Learn about new features in Azure.</span></span>
* <span data-ttu-id="3bbec-317">[Blog Windows PowerShell](http://blogs.msdn.com/powershell): découvrez les nouvelles fonctionnalités de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3bbec-317">[Windows PowerShell blog](http://blogs.msdn.com/powershell): Learn about new features in Windows PowerShell.</span></span>
* <span data-ttu-id="3bbec-318">[Blog Blog](http://blogs.technet.com/b/heyscriptingguy/): obtenir réel trucs et astuces de hello Communauté de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3bbec-318">["Hey, Scripting Guy!" Blog](http://blogs.technet.com/b/heyscriptingguy/): Get real-world tips and tricks from hello Windows PowerShell community.</span></span>

