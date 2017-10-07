---
title: aaaHow tooconfigure Cache Redis Azure | Documents Microsoft
description: "Configuration de Redis hello par défaut pour le Cache Redis Azure de découvrir et comprendre comment tooconfigure votre Azure Redis Cache des instances"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: d0bf2e1f-6a26-4e62-85ba-d82b35fc5aa6
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 08/22/2017
ms.author: sdanie
ms.openlocfilehash: 46bffb74cdf40e0e0a99c3a83dbe06d6fe1ea65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-azure-redis-cache"></a><span data-ttu-id="bbf0a-103">Comment tooconfigure Cache Redis Azure</span><span class="sxs-lookup"><span data-stu-id="bbf0a-103">How tooconfigure Azure Redis Cache</span></span>
<span data-ttu-id="bbf0a-104">Cette rubrique décrit comment tooreview et mise à jour hello configuration pour vos instances de Cache Redis Azure et la configuration du serveur Redis couvre hello par défaut pour les instances de Cache Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-104">This topic describes how tooreview and update hello configuration for your Azure Redis Cache instances, and covers hello default Redis server configuration for Azure Redis Cache instances.</span></span>

> [!NOTE]
> <span data-ttu-id="bbf0a-105">Pour plus d’informations sur la configuration et l’utilisation des fonctionnalités de cache premium, consultez [la persistance de tooconfigure](cache-how-to-premium-persistence.md), [comment tooconfigure clustering](cache-how-to-premium-clustering.md), et [comment tooconfigure réseau virtuel prend en charge ](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="bbf0a-105">For more information on configuring and using premium cache features, see [How tooconfigure persistence](cache-how-to-premium-persistence.md), [How tooconfigure clustering](cache-how-to-premium-clustering.md), and [How tooconfigure Virtual Network support](cache-how-to-premium-vnet.md).</span></span>
> 
> 

## <a name="configure-redis-cache-settings"></a><span data-ttu-id="bbf0a-106">Configuration des paramètres de cache Redis</span><span class="sxs-lookup"><span data-stu-id="bbf0a-106">Configure Redis cache settings</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

<span data-ttu-id="bbf0a-107">Les paramètres de Cache Redis Azure sont affichés et configurés sur hello **Cache Redis** panneau à l’aide de hello **ressource Menu**.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-107">Azure Redis Cache settings are viewed and configured on hello **Redis Cache** blade using hello **Resource Menu**.</span></span>

![Paramètres de Cache Redis](./media/cache-configure/redis-cache-settings.png)

<span data-ttu-id="bbf0a-109">Vous pouvez afficher et configurer hello suivant les paramètres à l’aide de hello **ressource Menu**.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-109">You can view and configure hello following settings using hello **Resource Menu**.</span></span>

* [<span data-ttu-id="bbf0a-110">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="bbf0a-110">Overview</span></span>](#overview)
* [<span data-ttu-id="bbf0a-111">Journal d’activité</span><span class="sxs-lookup"><span data-stu-id="bbf0a-111">Activity log</span></span>](#activity-log)
* [<span data-ttu-id="bbf0a-112">Contrôle d’accès (IAM)</span><span class="sxs-lookup"><span data-stu-id="bbf0a-112">Access control (IAM)</span></span>](#access-control-iam)
* [<span data-ttu-id="bbf0a-113">Balises</span><span class="sxs-lookup"><span data-stu-id="bbf0a-113">Tags</span></span>](#tags)
* [<span data-ttu-id="bbf0a-114">Diagnostiquer et résoudre les problèmes</span><span class="sxs-lookup"><span data-stu-id="bbf0a-114">Diagnose and solve problems</span></span>](#diagnose-and-solve-problems)
* [<span data-ttu-id="bbf0a-115">Paramètres</span><span class="sxs-lookup"><span data-stu-id="bbf0a-115">Settings</span></span>](#settings)
    * [<span data-ttu-id="bbf0a-116">Clés d’accès</span><span class="sxs-lookup"><span data-stu-id="bbf0a-116">Access keys</span></span>](#access-keys)
    * [<span data-ttu-id="bbf0a-117">Paramètres avancés</span><span class="sxs-lookup"><span data-stu-id="bbf0a-117">Advanced settings</span></span>](#advanced-settings)
    * [<span data-ttu-id="bbf0a-118">Redis Cache Advisor</span><span class="sxs-lookup"><span data-stu-id="bbf0a-118">Redis Cache Advisor</span></span>](#redis-cache-advisor)
    * [<span data-ttu-id="bbf0a-119">Mettre à l'échelle</span><span class="sxs-lookup"><span data-stu-id="bbf0a-119">Scale</span></span>](#scale)
    * [<span data-ttu-id="bbf0a-120">Taille du cluster Redis</span><span class="sxs-lookup"><span data-stu-id="bbf0a-120">Redis cluster size</span></span>](#cluster-size)
    * [<span data-ttu-id="bbf0a-121">Persistance des données Redis</span><span class="sxs-lookup"><span data-stu-id="bbf0a-121">Redis data persistence</span></span>](#redis-data-persistence)
    * [<span data-ttu-id="bbf0a-122">Planification de mises à jour</span><span class="sxs-lookup"><span data-stu-id="bbf0a-122">Schedule updates</span></span>](#schedule-updates)
    * [<span data-ttu-id="bbf0a-123">Géoréplication</span><span class="sxs-lookup"><span data-stu-id="bbf0a-123">Geo-replication</span></span>](#geo-replication)
    * [<span data-ttu-id="bbf0a-124">Réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="bbf0a-124">Virtual Network</span></span>](#virtual-network)
    * [<span data-ttu-id="bbf0a-125">Pare-feu</span><span class="sxs-lookup"><span data-stu-id="bbf0a-125">Firewall</span></span>](#firewall)
    * [<span data-ttu-id="bbf0a-126">Propriétés</span><span class="sxs-lookup"><span data-stu-id="bbf0a-126">Properties</span></span>](#properties)
    * [<span data-ttu-id="bbf0a-127">Verrous</span><span class="sxs-lookup"><span data-stu-id="bbf0a-127">Locks</span></span>](#locks)
    * [<span data-ttu-id="bbf0a-128">Script Automation</span><span class="sxs-lookup"><span data-stu-id="bbf0a-128">Automation script</span></span>](#automation-script)
* [<span data-ttu-id="bbf0a-129">Administration</span><span class="sxs-lookup"><span data-stu-id="bbf0a-129">Administration</span></span>](#administration)
    * [<span data-ttu-id="bbf0a-130">Importer des données</span><span class="sxs-lookup"><span data-stu-id="bbf0a-130">Import data</span></span>](#importexport)
    * [<span data-ttu-id="bbf0a-131">Exporter des données</span><span class="sxs-lookup"><span data-stu-id="bbf0a-131">Export data</span></span>](#importexport)
    * [<span data-ttu-id="bbf0a-132">Reboot</span><span class="sxs-lookup"><span data-stu-id="bbf0a-132">Reboot</span></span>](#reboot)
* [<span data-ttu-id="bbf0a-133">Surveillance</span><span class="sxs-lookup"><span data-stu-id="bbf0a-133">Monitoring</span></span>](#monitoring)
    * [<span data-ttu-id="bbf0a-134">Mesures Redis</span><span class="sxs-lookup"><span data-stu-id="bbf0a-134">Redis metrics</span></span>](#redis-metrics)
    * [<span data-ttu-id="bbf0a-135">Règles d'alerte</span><span class="sxs-lookup"><span data-stu-id="bbf0a-135">Alert rules</span></span>](#alert-rules)
    * [<span data-ttu-id="bbf0a-136">Diagnostics</span><span class="sxs-lookup"><span data-stu-id="bbf0a-136">Diagnostics</span></span>](#diagnostics)
* [<span data-ttu-id="bbf0a-137">Paramètres de support et dépannage</span><span class="sxs-lookup"><span data-stu-id="bbf0a-137">Support & troubleshooting settings</span></span>](#support-amp-troubleshooting-settings)
    * [<span data-ttu-id="bbf0a-138">Intégrité des ressources</span><span class="sxs-lookup"><span data-stu-id="bbf0a-138">Resource health</span></span>](#resource-health)
    * [<span data-ttu-id="bbf0a-139">Nouvelle demande de support</span><span class="sxs-lookup"><span data-stu-id="bbf0a-139">New support request</span></span>](#new-support-request)


## <a name="overview"></a><span data-ttu-id="bbf0a-140">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="bbf0a-140">Overview</span></span>

<span data-ttu-id="bbf0a-141">La **Vue d’ensemble** fournit des informations de base sur votre cache, notamment le nom, les ports, le niveau tarifaire et des mesures de cache sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-141">**Overview** provides you with basic information about your cache, such as name, ports, pricing tier, and selected cache metrics.</span></span>

### <a name="activity-log"></a><span data-ttu-id="bbf0a-142">Journal d’activité</span><span class="sxs-lookup"><span data-stu-id="bbf0a-142">Activity log</span></span>

<span data-ttu-id="bbf0a-143">Cliquez sur **le journal d’activité** tooview actions exécutées sur votre cache.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-143">Click **Activity log** tooview actions performed on your cache.</span></span> <span data-ttu-id="bbf0a-144">Vous pouvez également utiliser tooexpand filtrage tooinclude de cette vue autres ressources.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-144">You can also use filtering tooexpand this view tooinclude other resources.</span></span> <span data-ttu-id="bbf0a-145">Pour en savoir plus sur l’utilisation des journaux d’audit, voir [Afficher les journaux d’activité pour auditer les actions sur les ressources](../azure-resource-manager/resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="bbf0a-145">For more information on working with audit logs, see [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md).</span></span> <span data-ttu-id="bbf0a-146">Pour plus d’informations sur la surveillance des événements du Cache Redis Azure, consultez [Opérations et alertes](cache-how-to-monitor.md#operations-and-alerts).</span><span class="sxs-lookup"><span data-stu-id="bbf0a-146">For more information on monitoring Azure Redis Cache events, see [Operations and alerts](cache-how-to-monitor.md#operations-and-alerts).</span></span>

### <a name="access-control-iam"></a><span data-ttu-id="bbf0a-147">Contrôle d’accès (IAM)</span><span class="sxs-lookup"><span data-stu-id="bbf0a-147">Access control (IAM)</span></span>

<span data-ttu-id="bbf0a-148">Hello **(IAM) de contrôle d’accès** section prend en charge pour le contrôle d’accès basé sur un rôle (RBAC) dans les organisations hello toohelp portail Azure à de leurs exigences de gestion des accès purement et simplement.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-148">hello **Access control (IAM)** section provides support for role-based access control (RBAC) in hello Azure portal toohelp organizations meet their access management requirements simply and precisely.</span></span> <span data-ttu-id="bbf0a-149">Pour plus d’informations, consultez [contrôle d’accès en fonction du rôle Bonjour portail Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="bbf0a-149">For more information, see [Role-based access control in hello Azure portal](../active-directory/role-based-access-control-configure.md).</span></span>

### <a name="tags"></a><span data-ttu-id="bbf0a-150">Tags</span><span class="sxs-lookup"><span data-stu-id="bbf0a-150">Tags</span></span>

<span data-ttu-id="bbf0a-151">Hello **balises** section vous aide à organiser vos ressources.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-151">hello **Tags** section helps you organize your resources.</span></span> <span data-ttu-id="bbf0a-152">Pour plus d’informations, consultez [à l’aide des balises tooorganize vos ressources Azure](../azure-resource-manager/resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="bbf0a-152">For more information, see [Using tags tooorganize your Azure resources](../azure-resource-manager/resource-group-using-tags.md).</span></span>


### <a name="diagnose-and-solve-problems"></a><span data-ttu-id="bbf0a-153">Diagnostiquer et résoudre les problèmes</span><span class="sxs-lookup"><span data-stu-id="bbf0a-153">Diagnose and solve problems</span></span>

<span data-ttu-id="bbf0a-154">Cliquez sur **diagnostiquer et résoudre les problèmes** toobe fourni avec des problèmes courants et des stratégies pour les résoudre.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-154">Click **Diagnose and solve problems** toobe provided with common issues and strategies for resolving them.</span></span>



## <a name="settings"></a><span data-ttu-id="bbf0a-155">Paramètres</span><span class="sxs-lookup"><span data-stu-id="bbf0a-155">Settings</span></span>
<span data-ttu-id="bbf0a-156">Hello **paramètres** section vous permet de tooaccess et configurer hello suivant les paramètres de votre cache.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-156">hello **Settings** section allows you tooaccess and configure hello following settings for your cache.</span></span>

* [<span data-ttu-id="bbf0a-157">Clés d’accès</span><span class="sxs-lookup"><span data-stu-id="bbf0a-157">Access keys</span></span>](#access-keys)
* [<span data-ttu-id="bbf0a-158">Paramètres avancés</span><span class="sxs-lookup"><span data-stu-id="bbf0a-158">Advanced settings</span></span>](#advanced-settings)
* [<span data-ttu-id="bbf0a-159">Redis Cache Advisor</span><span class="sxs-lookup"><span data-stu-id="bbf0a-159">Redis Cache Advisor</span></span>](#redis-cache-advisor)
* [<span data-ttu-id="bbf0a-160">Mettre à l'échelle</span><span class="sxs-lookup"><span data-stu-id="bbf0a-160">Scale</span></span>](#scale)
* [<span data-ttu-id="bbf0a-161">Taille du cluster Redis</span><span class="sxs-lookup"><span data-stu-id="bbf0a-161">Redis cluster size</span></span>](#cluster-size)
* [<span data-ttu-id="bbf0a-162">Persistance des données Redis</span><span class="sxs-lookup"><span data-stu-id="bbf0a-162">Redis data persistence</span></span>](#redis-data-persistence)
* [<span data-ttu-id="bbf0a-163">Planification de mises à jour</span><span class="sxs-lookup"><span data-stu-id="bbf0a-163">Schedule updates</span></span>](#schedule-updates)
* [<span data-ttu-id="bbf0a-164">Géoréplication</span><span class="sxs-lookup"><span data-stu-id="bbf0a-164">Geo-replication</span></span>](#geo-replication)
* [<span data-ttu-id="bbf0a-165">Réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="bbf0a-165">Virtual Network</span></span>](#virtual-network)
* [<span data-ttu-id="bbf0a-166">Pare-feu</span><span class="sxs-lookup"><span data-stu-id="bbf0a-166">Firewall</span></span>](#firewall)
* [<span data-ttu-id="bbf0a-167">Propriétés</span><span class="sxs-lookup"><span data-stu-id="bbf0a-167">Properties</span></span>](#properties)
* [<span data-ttu-id="bbf0a-168">Verrous</span><span class="sxs-lookup"><span data-stu-id="bbf0a-168">Locks</span></span>](#locks)
* [<span data-ttu-id="bbf0a-169">Script Automation</span><span class="sxs-lookup"><span data-stu-id="bbf0a-169">Automation script</span></span>](#automation-script)



### <a name="access-keys"></a><span data-ttu-id="bbf0a-170">Clés d’accès</span><span class="sxs-lookup"><span data-stu-id="bbf0a-170">Access keys</span></span>
<span data-ttu-id="bbf0a-171">Cliquez sur **clés d’accès** tooview ou régénérez l’accès hello clés pour votre cache.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-171">Click **Access keys** tooview or regenerate hello access keys for your cache.</span></span> <span data-ttu-id="bbf0a-172">Ces clés sont utilisées par les clients hello tooyour cache de connexion.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-172">These keys are used by hello clients connecting tooyour cache.</span></span>

![Clés d’accès de Cache Redis](./media/cache-configure/redis-cache-manage-keys.png)

### <a name="advanced-settings"></a><span data-ttu-id="bbf0a-174">Paramètres avancés</span><span class="sxs-lookup"><span data-stu-id="bbf0a-174">Advanced settings</span></span>
<span data-ttu-id="bbf0a-175">Hello paramètres suivants sont configurés sur hello **paramètres avancés** panneau.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-175">hello following settings are configured on hello **Advanced settings** blade.</span></span>

* [<span data-ttu-id="bbf0a-176">Ports d’accès</span><span class="sxs-lookup"><span data-stu-id="bbf0a-176">Access Ports</span></span>](#access-ports)
* [<span data-ttu-id="bbf0a-177">Stratégies de mémoire</span><span class="sxs-lookup"><span data-stu-id="bbf0a-177">Memory policies</span></span>](#memory-policies)
* [<span data-ttu-id="bbf0a-178">Notifications de Keyspace (paramètres avancés)</span><span class="sxs-lookup"><span data-stu-id="bbf0a-178">Keyspace notifications (advanced settings)</span></span>](#keyspace-notifications-advanced-settings)

#### <a name="access-ports"></a><span data-ttu-id="bbf0a-179">Ports d’accès</span><span class="sxs-lookup"><span data-stu-id="bbf0a-179">Access Ports</span></span>
<span data-ttu-id="bbf0a-180">Par défaut, l’accès non SSL est désactivé pour les nouveaux caches.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-180">By default, non-SSL access is disabled for new caches.</span></span> <span data-ttu-id="bbf0a-181">tooenable hello non-SSL du port, cliquez sur **non** pour **autoriser l’accès uniquement via SSL** sur hello **paramètres avancés** panneau, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-181">tooenable hello non-SSL port, click **No** for **Allow access only via SSL** on hello **Advanced settings** blade and then click **Save**.</span></span>

![Ports d’accès de Cache Redis](./media/cache-configure/redis-cache-access-ports.png)

<a name="maxmemory-policy-and-maxmemory-reserved"></a>
#### <a name="memory-policies"></a><span data-ttu-id="bbf0a-183">Stratégies de mémoire</span><span class="sxs-lookup"><span data-stu-id="bbf0a-183">Memory policies</span></span>
<span data-ttu-id="bbf0a-184">Hello **stratégie Maxmemory**, **réservés maxmemory**, et **réservés maxfragmentationmemory** paramètres hello **paramètresavancés**panneau configurer des stratégies de mémoire hello pour le cache de hello.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-184">hello **Maxmemory policy**, **maxmemory-reserved**, and **maxfragmentationmemory-reserved** settings on hello **Advanced settings** blade configure hello memory policies for hello cache.</span></span>

![Stratégie Maxmemory de Cache Redis](./media/cache-configure/redis-cache-maxmemory-policy.png)

<span data-ttu-id="bbf0a-186">**Stratégie MaxMemory** configure la stratégie d’éviction hello pour le cache de hello et vous permet de toochoose de hello suivant des stratégies d’éviction :</span><span class="sxs-lookup"><span data-stu-id="bbf0a-186">**Maxmemory policy** configures hello eviction policy for hello cache and allows you toochoose from hello following eviction policies:</span></span>

* <span data-ttu-id="bbf0a-187">`volatile-lru`-Il s’agit par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-187">`volatile-lru` - this is hello default.</span></span>
* `allkeys-lru`
* `volatile-random`
* `allkeys-random`
* `volatile-ttl`
* `noeviction`

<span data-ttu-id="bbf0a-188">Pour plus d’informations sur les stratégies `maxmemory`, voir [Stratégies d’éviction](http://redis.io/topics/lru-cache#eviction-policies).</span><span class="sxs-lookup"><span data-stu-id="bbf0a-188">For more information about `maxmemory` policies, see [Eviction policies](http://redis.io/topics/lru-cache#eviction-policies).</span></span>

<span data-ttu-id="bbf0a-189">Hello **réservés maxmemory** paramètre configure la quantité hello de mémoire en Mo est réservé pour les opérations telles que la réplication pendant le basculement non mises en cache.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-189">hello **maxmemory-reserved** setting configures hello amount of memory in MB that is reserved for non-cache operations such as replication during failover.</span></span> <span data-ttu-id="bbf0a-190">Ce paramètre vous permet de toohave un environnement de serveur Redis cohérent dans la varie en fonction de votre charge.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-190">Setting this value allows you toohave a more consistent Redis server experience when your load varies.</span></span> <span data-ttu-id="bbf0a-191">Cette valeur doit être plus élevée pour les charges de travail comportant de nombreuses écritures.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-191">This value should be set higher for workloads that are write heavy.</span></span> <span data-ttu-id="bbf0a-192">Lorsque la mémoire est réservée pour ces opérations, elle n’est pas disponible pour le stockage des données mises en cache.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-192">When memory is reserved for such operations, it is unavailable for storage of cached data.</span></span>

<span data-ttu-id="bbf0a-193">Hello **maxfragmentationmemory réservés** paramètre configure la quantité hello de mémoire en Mo est tooaccommodate réservé pour la fragmentation de mémoire.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-193">hello **maxfragmentationmemory-reserved** setting configures hello amount of memory in MB that is reserved tooaccommodate for memory fragmentation.</span></span> <span data-ttu-id="bbf0a-194">Ce paramètre vous permet de toohave un environnement de serveur Redis cohérent lorsque hello cache est plein ou fermer les taux de fragmentation toofull et hello sont également élevée.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-194">Setting this value allows you toohave a more consistent Redis server experience when hello cache is full or close toofull and hello fragmentation ratio is also high.</span></span> <span data-ttu-id="bbf0a-195">Lorsque la mémoire est réservée pour ces opérations, elle n’est pas disponible pour le stockage des données mises en cache.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-195">When memory is reserved for such operations, it is unavailable for storage of cached data.</span></span>

<span data-ttu-id="bbf0a-196">Une chose tooconsider lors du choix d’une nouvelle valeur de réserve de mémoire (**réservés maxmemory** ou **maxfragmentationmemory réservés**) est la manière dont cette modification peut affecter un cache qui est déjà en cours d’exécution avec grandes quantités de données.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-196">One thing tooconsider when choosing a new memory reservation value (**maxmemory-reserved** or **maxfragmentationmemory-reserved**) is how this change might affect a cache that is already running with large amounts of data in it.</span></span> <span data-ttu-id="bbf0a-197">Par exemple, si vous avez un cache 53 Go 49 Go de données, puis modifiez hello réservation valeur too8 Go, cela supprimera hello maximale de mémoire disponible pour système hello too45 go.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-197">For instance, if you have a 53 GB cache with 49 GB of data, then change hello reservation value too8 GB, this will drop hello max available memory for hello system down too45 GB.</span></span> <span data-ttu-id="bbf0a-198">Si le paramètre actuel `used_memory` ou votre `used_memory_rss` valeurs sont supérieures à la nouvelle limite de hello de 45 Go, puis hello système n’aura tooevict données tant que les `used_memory` et `used_memory_rss` sont inférieure à 45 Go.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-198">If either your current `used_memory` or your `used_memory_rss` values are higher than hello new limit of 45 GB, then hello system will have tooevict data until both `used_memory` and `used_memory_rss` are below 45 GB.</span></span> <span data-ttu-id="bbf0a-199">La suppression de données peut augmenter la fragmentation de la charge et de la mémoire du serveur.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-199">Eviction can increase server load and memory fragmentation.</span></span> <span data-ttu-id="bbf0a-200">Pour plus d’informations sur les métriques de cache, telles que `used_memory` et `used_memory_rss`, voir [Mesures disponibles et intervalles de création des rapports](cache-how-to-monitor.md#available-metrics-and-reporting-intervals).</span><span class="sxs-lookup"><span data-stu-id="bbf0a-200">For more information on cache metrics such as `used_memory` and `used_memory_rss`, see [Available metrics and reporting intervals](cache-how-to-monitor.md#available-metrics-and-reporting-intervals).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bbf0a-201">Hello **réservés maxmemory** et **maxfragmentationmemory réservés** paramètres sont uniquement disponibles pour Standard et Premium met en cache.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-201">hello **maxmemory-reserved** and **maxfragmentationmemory-reserved** settings are only available for Standard and Premium caches.</span></span>
> 
> 

#### <a name="keyspace-notifications-advanced-settings"></a><span data-ttu-id="bbf0a-202">Notifications de Keyspace (paramètres avancés)</span><span class="sxs-lookup"><span data-stu-id="bbf0a-202">Keyspace notifications (advanced settings)</span></span>
<span data-ttu-id="bbf0a-203">Les notifications sont configurées sur hello espace de clés de redis **paramètres avancés** panneau.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-203">Redis keyspace notifications are configured on hello **Advanced settings** blade.</span></span> <span data-ttu-id="bbf0a-204">Notifications de l’espace de clés permettent aux clients de tooreceive notifications lorsque certains événements se produisent.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-204">Keyspace notifications allow clients tooreceive notifications when certain events occur.</span></span>

![Paramètres avancés de Cache Redis](./media/cache-configure/redis-cache-advanced-settings.png)

> [!IMPORTANT]
> <span data-ttu-id="bbf0a-206">Espace de clés des notifications et hello **événements espace de clés notifier** sont uniquement disponibles pour les caches Standard et Premium.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-206">Keyspace notifications and hello **notify-keyspace-events** setting are only available for Standard and Premium caches.</span></span>
> 
> 

<span data-ttu-id="bbf0a-207">Pour plus d’informations, voir [Notifications de keyspace Redis](http://redis.io/topics/notifications).</span><span class="sxs-lookup"><span data-stu-id="bbf0a-207">For more information, see [Redis Keyspace Notifications](http://redis.io/topics/notifications).</span></span> <span data-ttu-id="bbf0a-208">Pour un exemple de code, consultez hello [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) fichier Bonjour [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) exemple.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-208">For sample code, see hello [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) file in hello [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) sample.</span></span>


<a name="recommendations"></a>
## <a name="redis-cache-advisor"></a><span data-ttu-id="bbf0a-209">Redis Cache Advisor</span><span class="sxs-lookup"><span data-stu-id="bbf0a-209">Redis Cache Advisor</span></span>
<span data-ttu-id="bbf0a-210">Hello **Advisor de Cache Redis** panneau affiche les recommandations pour votre cache.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-210">hello **Redis Cache Advisor** blade displays recommendations for your cache.</span></span> <span data-ttu-id="bbf0a-211">Pendant les opérations normales, aucune recommandation n’est affichée.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-211">During normal operations, no recommendations are displayed.</span></span> 

![Recommandations](./media/cache-configure/redis-cache-no-recommendations.png)

<span data-ttu-id="bbf0a-213">Si toutes les conditions se produisent lors des opérations de hello de votre cache, telles que l’utilisation de mémoire haute, la bande passante du réseau ou de charge du serveur, une alerte s’affiche sur hello **Cache Redis** panneau.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-213">If any conditions occur during hello operations of your cache such as high memory usage, network bandwidth, or server load, an alert is displayed on hello **Redis Cache** blade.</span></span>

![Recommandations](./media/cache-configure/redis-cache-recommendations-alert.png)

<span data-ttu-id="bbf0a-215">Vous trouverez plus d’informations sur hello **recommandations** panneau.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-215">Further information can be found on hello **Recommendations** blade.</span></span>

![Recommandations](./media/cache-configure/redis-cache-recommendations.png)

<span data-ttu-id="bbf0a-217">Vous pouvez surveiller ces métriques sur hello [graphiques de surveillance](cache-how-to-monitor.md#monitoring-charts) et [graphiques d’utilisation](cache-how-to-monitor.md#usage-charts) sections Hello **Cache Redis** panneau.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-217">You can monitor these metrics on hello [Monitoring charts](cache-how-to-monitor.md#monitoring-charts) and [Usage charts](cache-how-to-monitor.md#usage-charts) sections of hello **Redis Cache** blade.</span></span>

<span data-ttu-id="bbf0a-218">Chaque niveau tarifaire est associé à des limites spécifiques concernant les connexions clientes, la mémoire et la bande passante.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-218">Each pricing tier has different limits for client connections, memory, and bandwidth.</span></span> <span data-ttu-id="bbf0a-219">Si votre cache est proche de la capacité maximale pour ces mesures pendant une période prolongée, une recommandation est créée.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-219">If your cache approaches maximum capacity for these metrics over a sustained period of time, a recommendation is created.</span></span> <span data-ttu-id="bbf0a-220">Pour plus d’informations sur les métriques hello et limites révisées par hello **recommandations** outil, consultez hello tableau suivant :</span><span class="sxs-lookup"><span data-stu-id="bbf0a-220">For more information about hello metrics and limits reviewed by hello **Recommendations** tool, see hello following table:</span></span>

| <span data-ttu-id="bbf0a-221">Mesure du Cache Redis</span><span class="sxs-lookup"><span data-stu-id="bbf0a-221">Redis Cache metric</span></span> | <span data-ttu-id="bbf0a-222">Plus d’informations</span><span class="sxs-lookup"><span data-stu-id="bbf0a-222">More information</span></span> |
| --- | --- |
| <span data-ttu-id="bbf0a-223">Utilisation de la bande passante réseau</span><span class="sxs-lookup"><span data-stu-id="bbf0a-223">Network bandwidth usage</span></span> |[<span data-ttu-id="bbf0a-224">Performances du cache - Bande passante disponible</span><span class="sxs-lookup"><span data-stu-id="bbf0a-224">Cache performance - available bandwidth</span></span>](cache-faq.md#cache-performance) |
| <span data-ttu-id="bbf0a-225">Clients connectés</span><span class="sxs-lookup"><span data-stu-id="bbf0a-225">Connected clients</span></span> |[<span data-ttu-id="bbf0a-226">Configuration du serveur Redis par défaut - maxclients</span><span class="sxs-lookup"><span data-stu-id="bbf0a-226">Default Redis server configuration - maxclients</span></span>](#maxclients) |
| <span data-ttu-id="bbf0a-227">Charge du serveur</span><span class="sxs-lookup"><span data-stu-id="bbf0a-227">Server load</span></span> |[<span data-ttu-id="bbf0a-228">Graphiques d’utilisation - Charge du serveur Redis</span><span class="sxs-lookup"><span data-stu-id="bbf0a-228">Usage charts - Redis Server Load</span></span>](cache-how-to-monitor.md#usage-charts) |
| <span data-ttu-id="bbf0a-229">Utilisation de la mémoire</span><span class="sxs-lookup"><span data-stu-id="bbf0a-229">Memory usage</span></span> |[<span data-ttu-id="bbf0a-230">Performance du cache - Taille</span><span class="sxs-lookup"><span data-stu-id="bbf0a-230">Cache performance - size</span></span>](cache-faq.md#cache-performance) |

<span data-ttu-id="bbf0a-231">tooupgrade votre cache, cliquez sur **mettre à niveau maintenant** hello toochange niveau tarifaire et [échelle](#scale) votre cache.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-231">tooupgrade your cache, click **Upgrade now** toochange hello pricing tier and [scale](#scale) your cache.</span></span> <span data-ttu-id="bbf0a-232">Pour plus d’informations sur le choix d’un niveau tarifaire, voir la section [Que propose Cache Redis et quelle taille dois-je utiliser ?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)</span><span class="sxs-lookup"><span data-stu-id="bbf0a-232">For more information on choosing a pricing tier, see [What Redis Cache offering and size should I use?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)</span></span>


### <a name="scale"></a><span data-ttu-id="bbf0a-233">Mettre à l'échelle</span><span class="sxs-lookup"><span data-stu-id="bbf0a-233">Scale</span></span>
<span data-ttu-id="bbf0a-234">Cliquez sur **échelle** hello tooview ou modification de niveau tarifaire pour votre cache.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-234">Click **Scale** tooview or change hello pricing tier for your cache.</span></span> <span data-ttu-id="bbf0a-235">Pour plus d’informations sur la mise à l’échelle, consultez [comment tooScale Cache Redis Azure](cache-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="bbf0a-235">For more information on scaling, see [How tooScale Azure Redis Cache](cache-how-to-scale.md).</span></span>

![Niveau de tarification de Cache Redis](./media/cache-configure/pricing-tier.png)

<a name="cluster-size"></a>

### <a name="redis-cluster-size"></a><span data-ttu-id="bbf0a-237">Taille du cluster Redis</span><span class="sxs-lookup"><span data-stu-id="bbf0a-237">Redis Cluster Size</span></span>
<span data-ttu-id="bbf0a-238">Cliquez sur **taille du Cluster Redis (version préliminaire)** avec activation des clusters de cache de taille de cluster toochange hello pour une prime en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-238">Click **(PREVIEW) Redis Cluster Size** toochange hello cluster size for a running premium cache with clustering enabled.</span></span>

> [!NOTE]
> <span data-ttu-id="bbf0a-239">Notez que lorsque hello Azure Redis Cache Premium couche a été publié tooGeneral disponibilité, la fonctionnalité de taille de Cluster Redis hello est actuellement en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-239">Note that while hello Azure Redis Cache Premium tier has been released tooGeneral Availability, hello Redis Cluster Size feature is currently in preview.</span></span>
> 
> 

![Taille du cluster Redis](./media/cache-configure/redis-cache-redis-cluster-size.png)

<span data-ttu-id="bbf0a-241">taille de cluster toochange hello, utilisez hello curseur ou tapez un nombre compris entre 1 et 10 dans hello **nombre de partitions** zone de texte et cliquez sur **OK** toosave.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-241">toochange hello cluster size, use hello slider or type a number between 1 and 10 in hello **Shard count** text box and click **OK** toosave.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bbf0a-242">Le clustering Redis est disponible uniquement pour les caches de niveau Premium.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-242">Redis clustering is only available for Premium caches.</span></span> <span data-ttu-id="bbf0a-243">Pour plus d’informations, consultez [comment tooconfigure clustering Premium Azure Redis cache](cache-how-to-premium-clustering.md).</span><span class="sxs-lookup"><span data-stu-id="bbf0a-243">For more information, see [How tooconfigure clustering for a Premium Azure Redis Cache](cache-how-to-premium-clustering.md).</span></span>
> 
> 


### <a name="redis-data-persistence"></a><span data-ttu-id="bbf0a-244">Persistance des données Redis</span><span class="sxs-lookup"><span data-stu-id="bbf0a-244">Redis data persistence</span></span>
<span data-ttu-id="bbf0a-245">Cliquez sur **Redis la persistance des données** tooenable, désactiver ou configurer la persistance des données pour votre cache premium.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-245">Click **Redis data persistence** tooenable, disable, or configure data persistence for your premium cache.</span></span> <span data-ttu-id="bbf0a-246">Cache Redis Azure offre la persistance Redis grâce à la [persistance RDB](cache-how-to-premium-persistence.md#configure-rdb-persistence) et à la [persistance AOF](cache-how-to-premium-persistence.md#configure-aof-persistence).</span><span class="sxs-lookup"><span data-stu-id="bbf0a-246">Azure Redis Cache offers Redis persistence using either [RDB persistence](cache-how-to-premium-persistence.md#configure-rdb-persistence) or [AOF persistence](cache-how-to-premium-persistence.md#configure-aof-persistence).</span></span>

<span data-ttu-id="bbf0a-247">Pour plus d’informations, consultez [la persistance tooconfigure cache Redis Azure Premium](cache-how-to-premium-persistence.md).</span><span class="sxs-lookup"><span data-stu-id="bbf0a-247">For more information, see [How tooconfigure persistence for a Premium Azure Redis Cache](cache-how-to-premium-persistence.md).</span></span>


> [!IMPORTANT]
> <span data-ttu-id="bbf0a-248">La persistance des données Redis est disponible uniquement pour les caches de niveau Premium.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-248">Redis data persistence is only available for Premium caches.</span></span> 
> 
> 

### <a name="schedule-updates"></a><span data-ttu-id="bbf0a-249">Planifier les mises à jour</span><span class="sxs-lookup"><span data-stu-id="bbf0a-249">Schedule updates</span></span>
<span data-ttu-id="bbf0a-250">Hello **planifier les mises à jour** panneau vous permet de toodesignate une fenêtre de maintenance des mises à jour du serveur Redis pour votre cache.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-250">hello **Schedule updates** blade allows you toodesignate a maintenance window for Redis server updates for your cache.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="bbf0a-251">fenêtre de maintenance Hello s’applique uniquement les mises à jour du serveur tooRedis et pas tooany Azure met à jour ou mises à jour du système d’exploitation de toohello de machines virtuelles hello qui hébergent le cache de hello.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-251">hello maintenance window applies only tooRedis server updates, and not tooany Azure updates or updates toohello operating system of hello VMs that host hello cache.</span></span>
> 
> 

![Planifier les mises à jour](./media/cache-configure/redis-schedule-updates.png)

<span data-ttu-id="bbf0a-253">toospecify une fenêtre de maintenance, vérifiez les jours hello souhaité et spécifier l’heure de début de fenêtre de maintenance hello pour chaque jour, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-253">toospecify a maintenance window, check hello desired days and specify hello maintenance window start hour for each day, and click **OK**.</span></span> <span data-ttu-id="bbf0a-254">Notez que l’heure de la fenêtre maintenance hello est au format UTC.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-254">Note that hello maintenance window time is in UTC.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="bbf0a-255">Hello **planifier les mises à jour** fonctionnalité est disponible uniquement pour les caches de niveau Premium.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-255">hello **Schedule updates** functionality is only available for Premium tier caches.</span></span> <span data-ttu-id="bbf0a-256">Pour plus d’informations et pour obtenir des instructions, consultez la page [Administration du cache Redis Azure - Planification de mises à jour](cache-administration.md#schedule-updates).</span><span class="sxs-lookup"><span data-stu-id="bbf0a-256">For more information and instructions, see [Azure Redis Cache administration - Schedule updates](cache-administration.md#schedule-updates).</span></span>
> 
> 

### <a name="geo-replication"></a><span data-ttu-id="bbf0a-257">Géoréplication</span><span class="sxs-lookup"><span data-stu-id="bbf0a-257">Geo-replication</span></span>

<span data-ttu-id="bbf0a-258">Hello **géo-réplication** panneau fournit un mécanisme permettant de lier les deux instances de Cache Redis Azure de niveau Premium.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-258">hello **Geo-replication** blade provides a mechanism for linking two Premium tier Azure Redis Cache instances.</span></span> <span data-ttu-id="bbf0a-259">Un cache est désigné comme le cache de lié principal hello et hello autre en tant que cache de lié secondaire hello.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-259">One cache is designated as hello primary linked cache, and hello other as hello secondary linked cache.</span></span> <span data-ttu-id="bbf0a-260">cache lié de Hello secondaire devient en lecture seule, et les données toohello écrit le cache principal est répliquée toohello cache lié secondaire.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-260">hello secondary linked cache becomes read-only, and data written toohello primary cache is replicated toohello secondary linked cache.</span></span> <span data-ttu-id="bbf0a-261">Cette fonctionnalité peut être utilisé tooreplicate un cache entre les régions Azure.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-261">This functionality can be used tooreplicate a cache across Azure regions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bbf0a-262">La **Géoréplication** est uniquement disponible pour les caches de niveau Premium.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-262">**Geo-replication** is only available for Premium tier caches.</span></span> <span data-ttu-id="bbf0a-263">Pour plus d’informations et pour obtenir des instructions, consultez [comment tooconfigure géo-réplication Azure Redis cache](cache-how-to-geo-replication.md).</span><span class="sxs-lookup"><span data-stu-id="bbf0a-263">For more information and instructions, see [How tooconfigure Geo-replication for Azure Redis Cache](cache-how-to-geo-replication.md).</span></span>
> 
> 

### <a name="virtual-network"></a><span data-ttu-id="bbf0a-264">Réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="bbf0a-264">Virtual Network</span></span>
<span data-ttu-id="bbf0a-265">Hello **réseau virtuel** section vous permet de paramètres de réseau virtuel tooconfigure hello pour votre cache.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-265">hello **Virtual Network** section allows you tooconfigure hello virtual network settings for your cache.</span></span> <span data-ttu-id="bbf0a-266">Pour plus d’informations sur la création d’un cache premium avec le réseau virtuel prend en charge et la mise à jour ses paramètres, consultez [comment tooconfigure réseau virtuel prend en charge un Premium Azure Redis cache](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="bbf0a-266">For information on creating a premium cache with VNET support and updating its settings, see [How tooconfigure Virtual Network Support for a Premium Azure Redis Cache](cache-how-to-premium-vnet.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bbf0a-267">Les paramètres de réseau virtuel sont disponibles uniquement pour les caches Premium qui ont été configurés avec la prise en charge de réseau virtuel lors de la création du cache.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-267">Virtual network settings are only available for premium caches that were configured with VNET support during cache creation.</span></span> 
> 
> 

### <a name="firewall"></a><span data-ttu-id="bbf0a-268">Pare-feu</span><span class="sxs-lookup"><span data-stu-id="bbf0a-268">Firewall</span></span>

<span data-ttu-id="bbf0a-269">Cliquez sur **pare-feu** tooview et configurer des règles de pare-feu pour votre Premium le Cache Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-269">Click **Firewall** tooview and configure firewall rules for your Premium Azure Redis Cache.</span></span>

![Pare-feu](./media/cache-configure/redis-firewall-rules.png)

<span data-ttu-id="bbf0a-271">Vous pouvez spécifier des règles de pare-feu avec une des valeurs de début et de fin de plage d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-271">You can specify firewall rules with a start and end IP address range.</span></span> <span data-ttu-id="bbf0a-272">Lorsque les règles de pare-feu sont configurés, uniquement les connexions client à partir de hello spécifié de plages d’adresses IP peuvent se connecter toohello cache.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-272">When firewall rules are configured, only client connections from hello specified IP address ranges can connect toohello cache.</span></span> <span data-ttu-id="bbf0a-273">Lorsqu’une règle de pare-feu est enregistrée est un bref délai avant de la règle de hello est effective.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-273">When a firewall rule is saved there is a short delay before hello rule is effective.</span></span> <span data-ttu-id="bbf0a-274">Ce délai est généralement inférieur à une minute.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-274">This delay is typically less than one minute.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bbf0a-275">Les connexions depuis les systèmes de surveillance de cache Redis Azure sont toujours autorisées, même si des règles de pare-feu sont configurées.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-275">Connections from Azure Redis Cache monitoring systems are always permitted, even if firewall rules are configured.</span></span>
> 
> <span data-ttu-id="bbf0a-276">Les règles de pare-feu son uniquement disponibles pour les caches de niveau Premium.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-276">Firewall rules are only available for Premium tier caches.</span></span>
> 
> 

### <a name="properties"></a><span data-ttu-id="bbf0a-277">Propriétés</span><span class="sxs-lookup"><span data-stu-id="bbf0a-277">Properties</span></span>
<span data-ttu-id="bbf0a-278">Cliquez sur **propriétés** tooview plus d’informations sur le cache, y compris le point de terminaison de cache hello et ports.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-278">Click **Properties** tooview information about your cache, including hello cache endpoint and ports.</span></span>

![Propriétés de Cache Redis](./media/cache-configure/redis-cache-properties.png)

### <a name="locks"></a><span data-ttu-id="bbf0a-280">Verrous</span><span class="sxs-lookup"><span data-stu-id="bbf0a-280">Locks</span></span>
<span data-ttu-id="bbf0a-281">Hello **verrouille** section vous permet de toolock un abonnement, groupe de ressources ou ressource tooprevent autres utilisateurs de votre organisation d’accidentellement supprimer ou modifier des ressources critiques.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-281">hello **Locks** section allows you toolock a subscription, resource group, or resource tooprevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="bbf0a-282">Pour plus d’informations, consultez [Verrouiller des ressources avec Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="bbf0a-282">For more information, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

### <a name="automation-script"></a><span data-ttu-id="bbf0a-283">Script Automation</span><span class="sxs-lookup"><span data-stu-id="bbf0a-283">Automation script</span></span>

<span data-ttu-id="bbf0a-284">Cliquez sur **script d’automatisation** toobuild et exporter un modèle de vos ressources déployées pour les déploiements futurs.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-284">Click **Automation script** toobuild and export a template of your deployed resources for future deployments.</span></span> <span data-ttu-id="bbf0a-285">Pour plus d’informations sur le fonctionnement des modèles, consultez [Déployer des ressources à l’aide de modèles Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="bbf0a-285">For more information about working with templates, see [Deploy resources with Azure Resource Manager templates](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

## <a name="administration-settings"></a><span data-ttu-id="bbf0a-286">Paramètres d’administration</span><span class="sxs-lookup"><span data-stu-id="bbf0a-286">Administration settings</span></span>
<span data-ttu-id="bbf0a-287">Hello paramètres Bonjour **Administration** section permettent de hello tooperform suivant des tâches d’administration pour votre cache.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-287">hello settings in hello **Administration** section allow you tooperform hello following administrative tasks for your cache.</span></span> 

![Administration](./media/cache-configure/redis-cache-administration.png)

* [<span data-ttu-id="bbf0a-289">Importer des données</span><span class="sxs-lookup"><span data-stu-id="bbf0a-289">Import data</span></span>](#importexport)
* [<span data-ttu-id="bbf0a-290">Exporter des données</span><span class="sxs-lookup"><span data-stu-id="bbf0a-290">Export data</span></span>](#importexport)
* [<span data-ttu-id="bbf0a-291">Reboot</span><span class="sxs-lookup"><span data-stu-id="bbf0a-291">Reboot</span></span>](#reboot)


### <a name="importexport"></a><span data-ttu-id="bbf0a-292">Importation/Exportation</span><span class="sxs-lookup"><span data-stu-id="bbf0a-292">Import/Export</span></span>
<span data-ttu-id="bbf0a-293">Importation/exportation est une opération de gestion de données de Cache Redis Azure, qui vous permet de tooimport et exporter des données dans le cache de hello par importation et exportation d’un instantané de base de données de Cache Redis (RDB) à partir de premium cache tooa objet blob de pages dans un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-293">Import/Export is an Azure Redis Cache data management operation, which allows you tooimport and export data in hello cache by importing and exporting a Redis Cache Database (RDB) snapshot from a premium cache tooa page blob in an Azure Storage Account.</span></span> <span data-ttu-id="bbf0a-294">Importation/exportation vous permet de toomigrate entre différentes instances de Cache Redis Azure ou remplir le cache de hello avec les données avant des utiliser.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-294">Import/Export enables you toomigrate between different Azure Redis Cache instances or populate hello cache with data before use.</span></span>

<span data-ttu-id="bbf0a-295">Importation peut être des fichiers compatibles RDB toobring utilisé Redis à partir de n’importe quel serveur Redis en cours d’exécution dans n’importe quel cloud ou l’environnement, y compris Redis en cours d’exécution sur Linux, Windows ou n’importe quel fournisseur de cloud comme Amazon Web Services et d’autres.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-295">Import can be used toobring Redis compatible RDB files from any Redis server running in any cloud or environment, including Redis running on Linux, Windows, or any cloud provider such as Amazon Web Services and others.</span></span> <span data-ttu-id="bbf0a-296">L’importation de données est un toocreate facilement un cache de données prédéfinis.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-296">Importing data is an easy way toocreate a cache with pre-populated data.</span></span> <span data-ttu-id="bbf0a-297">Au cours du processus d’importation hello, le Cache Redis Azure charge les fichiers RDB hello depuis le stockage Azure en mémoire et les insère les clés hello dans le cache de hello.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-297">During hello import process, Azure Redis Cache loads hello RDB files from Azure storage into memory, and then inserts hello keys into hello cache.</span></span>

<span data-ttu-id="bbf0a-298">Exportation vous permet des données de salutation tooexport stockées dans les fichiers de Cache Redis Azure tooRedis compatibles RDB.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-298">Export allows you tooexport hello data stored in Azure Redis Cache tooRedis compatible RDB files.</span></span> <span data-ttu-id="bbf0a-299">Vous pouvez utiliser ces données toomove de fonctionnalité à partir d’un Cache Redis Azure instance tooanother ou tooanother Redis server.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-299">You can use this feature toomove data from one Azure Redis Cache instance tooanother or tooanother Redis server.</span></span> <span data-ttu-id="bbf0a-300">Au cours du processus d’exportation hello, un fichier temporaire est créé sur hello VM que hôtes hello l’instance de serveur de Cache Redis Azure et hello fichier téléchargé toohello désigné du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-300">During hello export process, a temporary file is created on hello VM that hosts hello Azure Redis Cache server instance, and hello file is uploaded toohello designated storage account.</span></span> <span data-ttu-id="bbf0a-301">Lors de l’opération d’exportation hello se termine avec l’état de réussite ou l’échec, le fichier temporaire de hello est supprimé.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-301">When hello export operation completes with either a status of success or failure, hello temporary file is deleted.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bbf0a-302">L’importation/exportation est uniquement disponible pour les caches de niveau Premium.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-302">Import/Export is only available for Premium tier caches.</span></span> <span data-ttu-id="bbf0a-303">Pour plus d’informations et pour obtenir des instructions, consultez la rubrique [Importer et exporter des données dans le cache Redis Azure](cache-how-to-import-export-data.md).</span><span class="sxs-lookup"><span data-stu-id="bbf0a-303">For more information and instructions, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

### <a name="reboot"></a><span data-ttu-id="bbf0a-304">Reboot</span><span class="sxs-lookup"><span data-stu-id="bbf0a-304">Reboot</span></span>
<span data-ttu-id="bbf0a-305">Hello **redémarrer** panneau vous permet de nœuds de hello tooreboot de votre cache.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-305">hello **Reboot** blade allows you tooreboot hello nodes of your cache.</span></span> <span data-ttu-id="bbf0a-306">Cette fonctionnalité de redémarrage permet de vous tootest votre application pour assurer la résilience en cas de panne d’un nœud de cache.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-306">This reboot capability enables you tootest your application for resiliency if there is a failure of a cache node.</span></span>

![Reboot](./media/cache-configure/redis-cache-reboot.png)

<span data-ttu-id="bbf0a-308">Si vous avez un cache premium avec activation des clusters, vous pouvez sélectionner les partitions de hello cache tooreboot.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-308">If you have a premium cache with clustering enabled, you can select which shards of hello cache tooreboot.</span></span>

![Reboot](./media/cache-configure/redis-cache-reboot-cluster.png)

<span data-ttu-id="bbf0a-310">tooreboot un ou plusieurs nœuds de votre cache, sélectionnez les nœuds de hello souhaité et cliquez sur **redémarrer**.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-310">tooreboot one or more nodes of your cache, select hello desired nodes and click **Reboot**.</span></span> <span data-ttu-id="bbf0a-311">Si vous avez un cache premium avec activation des clusters, sélectionnez hello partitions tooreboot puis **redémarrer**.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-311">If you have a premium cache with clustering enabled, select hello shard(s) tooreboot and then click **Reboot**.</span></span> <span data-ttu-id="bbf0a-312">Après quelques minutes, hello redémarrage d’un ou plusieurs nœuds sélectionnés et sont en ligne quelques minutes plus tard.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-312">After a few minutes, hello selected node(s) reboot, and are back online a few minutes later.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bbf0a-313">Le redémarrage est désormais disponible pour tous les niveaux de tarification.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-313">Reboot is now available for all pricing tiers.</span></span> <span data-ttu-id="bbf0a-314">Pour plus d’informations et pour obtenir des instructions, consultez la page [Administration du cache Redis Azure - Redémarrage](cache-administration.md#reboot).</span><span class="sxs-lookup"><span data-stu-id="bbf0a-314">For more information and instructions, see [Azure Redis Cache administration - Reboot](cache-administration.md#reboot).</span></span>
> 
> 


## <a name="monitoring"></a><span data-ttu-id="bbf0a-315">Surveillance</span><span class="sxs-lookup"><span data-stu-id="bbf0a-315">Monitoring</span></span>

<span data-ttu-id="bbf0a-316">Hello **analyse** section vous permet de tooconfigure diagnostics et analyse pour votre Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-316">hello **Monitoring** section allows you tooconfigure diagnostics and monitoring for your Redis Cache.</span></span> <span data-ttu-id="bbf0a-317">Pour plus d’informations sur la surveillance de Cache Redis Azure et de diagnostics, consultez [comment toomonitor Cache Redis Azure](cache-how-to-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="bbf0a-317">For more information on Azure Redis Cache monitoring and diagnostics, see [How toomonitor Azure Redis Cache](cache-how-to-monitor.md).</span></span>

![Diagnostics](./media/cache-configure/redis-cache-diagnostics.png)

* [<span data-ttu-id="bbf0a-319">Mesures Redis</span><span class="sxs-lookup"><span data-stu-id="bbf0a-319">Redis metrics</span></span>](#redis-metrics)
* [<span data-ttu-id="bbf0a-320">Règles d'alerte</span><span class="sxs-lookup"><span data-stu-id="bbf0a-320">Alert rules</span></span>](#alert-rules)
* [<span data-ttu-id="bbf0a-321">Diagnostics</span><span class="sxs-lookup"><span data-stu-id="bbf0a-321">Diagnostics</span></span>](#diagnostics)

### <a name="redis-metrics"></a><span data-ttu-id="bbf0a-322">Mesures Redis</span><span class="sxs-lookup"><span data-stu-id="bbf0a-322">Redis metrics</span></span>
<span data-ttu-id="bbf0a-323">Cliquez sur **Redis métriques** trop[afficher les métriques](cache-how-to-monitor.md#view-cache-metrics) pour votre cache.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-323">Click **Redis metrics** too[view metrics](cache-how-to-monitor.md#view-cache-metrics) for your cache.</span></span>

### <a name="alert-rules"></a><span data-ttu-id="bbf0a-324">Règles d'alerte</span><span class="sxs-lookup"><span data-stu-id="bbf0a-324">Alert rules</span></span>

<span data-ttu-id="bbf0a-325">Cliquez sur **règles d’alerte** tooconfigure alertes en fonction des métriques de Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-325">Click **Alert rules** tooconfigure alerts based on Redis Cache metrics.</span></span> <span data-ttu-id="bbf0a-326">Pour plus d'informations, consultez [Alertes](cache-how-to-monitor.md#alerts).</span><span class="sxs-lookup"><span data-stu-id="bbf0a-326">For more information, see [Alerts](cache-how-to-monitor.md#alerts).</span></span>

### <a name="diagnostics"></a><span data-ttu-id="bbf0a-327">Diagnostics</span><span class="sxs-lookup"><span data-stu-id="bbf0a-327">Diagnostics</span></span>

<span data-ttu-id="bbf0a-328">Par défaut, les mesures de cache dans Azure Monitor sont [stockées pendant 30 jours](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive), puis supprimées.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-328">By default, cache metrics in Azure Monitor are [stored for 30 days](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive) and then deleted.</span></span> <span data-ttu-id="bbf0a-329">Cliquez sur les métriques de votre cache pendant plus de 30 jours, toopersist **Diagnostics** trop[configurer le compte de stockage hello](cache-how-to-monitor.md#export-cache-metrics) utilisé toostore les diagnostics de cache.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-329">toopersist your cache metrics for longer than 30 days, click **Diagnostics** too[configure hello storage account](cache-how-to-monitor.md#export-cache-metrics) used toostore cache diagnostics.</span></span>

>[!NOTE]
><span data-ttu-id="bbf0a-330">En outre tooarchiving votre toostorage de métriques de cache, vous pouvez également [les diffuser un concentrateur d’événements tooan ou les envoyer tooLog Analytique](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).</span><span class="sxs-lookup"><span data-stu-id="bbf0a-330">In addition tooarchiving your cache metrics toostorage, you can also [stream them tooan Event hub or send them tooLog Analytics](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).</span></span>
>
>

## <a name="support--troubleshooting-settings"></a><span data-ttu-id="bbf0a-331">Paramètres de support et dépannage</span><span class="sxs-lookup"><span data-stu-id="bbf0a-331">Support & troubleshooting settings</span></span>
<span data-ttu-id="bbf0a-332">Hello paramètres Bonjour **prise en charge + dépannage** section vous fournir des options pour la résolution des problèmes avec votre cache.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-332">hello settings in hello **Support + troubleshooting** section provide you with options for resolving issues with your cache.</span></span>

![prise en charge et à la résolution des problèmes](./media/cache-configure/redis-cache-support-troubleshooting.png)

* [<span data-ttu-id="bbf0a-334">Intégrité des ressources</span><span class="sxs-lookup"><span data-stu-id="bbf0a-334">Resource health</span></span>](#resource-health)
* [<span data-ttu-id="bbf0a-335">Nouvelle demande de support</span><span class="sxs-lookup"><span data-stu-id="bbf0a-335">New support request</span></span>](#new-support-request)

### <a name="resource-health"></a><span data-ttu-id="bbf0a-336">Intégrité des ressources</span><span class="sxs-lookup"><span data-stu-id="bbf0a-336">Resource health</span></span>
<span data-ttu-id="bbf0a-337">**Resource Health** surveille vos ressources et vous indique si elles s’exécutent comme prévu.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-337">**Resource health** watches your resource and tells you if it's running as expected.</span></span> <span data-ttu-id="bbf0a-338">Pour plus d’informations sur hello service d’intégrité de ressource Azure, consultez [vue d’ensemble du contrôle d’intégrité Azure Resource](../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bbf0a-338">For more information about hello Azure Resource health service, see [Azure Resource health overview](../resource-health/resource-health-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="bbf0a-339">L’intégrité des ressources est actuellement incapable de tooreport intégrité hello d’instances de Cache Redis Azure hébergée dans un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-339">Resource health is currently unable tooreport on hello health of Azure Redis Cache instances hosted in a virtual network.</span></span> <span data-ttu-id="bbf0a-340">Pour plus d’informations, voir [Toutes les fonctionnalités fonctionnent-elles lorsque vous hébergez un cache dans un réseau virtuel ?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)</span><span class="sxs-lookup"><span data-stu-id="bbf0a-340">For more information, see [Do all cache features work when hosting a cache in a VNET?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)</span></span>
> 
> 

### <a name="new-support-request"></a><span data-ttu-id="bbf0a-341">Nouvelle demande de support</span><span class="sxs-lookup"><span data-stu-id="bbf0a-341">New support request</span></span>
<span data-ttu-id="bbf0a-342">Cliquez sur **nouveau prend en charge la demande** tooopen une demande de support pour votre cache.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-342">Click **New support request** tooopen a support request for your cache.</span></span>





## <a name="default-redis-server-configuration"></a><span data-ttu-id="bbf0a-343">Configuration du serveur Redis par défaut</span><span class="sxs-lookup"><span data-stu-id="bbf0a-343">Default Redis server configuration</span></span>
<span data-ttu-id="bbf0a-344">Nouveau Cache Redis Azure sont configurées avec hello suivant de valeurs de configuration par défaut Redis.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-344">New Azure Redis Cache instances are configured with hello following default Redis configuration values.</span></span>

> [!NOTE]
> <span data-ttu-id="bbf0a-345">paramètres Hello dans cette section ne peut pas être modifiés à l’aide de hello `StackExchange.Redis.IServer.ConfigSet` (méthode).</span><span class="sxs-lookup"><span data-stu-id="bbf0a-345">hello settings in this section cannot be changed using hello `StackExchange.Redis.IServer.ConfigSet` method.</span></span> <span data-ttu-id="bbf0a-346">Si cette méthode est appelée avec une des commandes hello dans cette section, une suivant toohello similaire d’exception est levée :</span><span class="sxs-lookup"><span data-stu-id="bbf0a-346">If this method is called with one of hello commands in this section, an exception similar toohello following is thrown:</span></span>  
> 
> `StackExchange.Redis.RedisServerException: ERR unknown command 'CONFIG'`
> 
> <span data-ttu-id="bbf0a-347">Toutes les valeurs qui sont configurables, telles que **max-mémoire-policy**, sont configurables via hello portail Azure ou des outils de gestion de ligne de commande tel que Azure CLI ou PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-347">Any values that are configurable, such as **max-memory-policy**, are configurable through hello Azure portal or command-line management tools such as Azure CLI or PowerShell.</span></span>
> 
> 

| <span data-ttu-id="bbf0a-348">Paramètre</span><span class="sxs-lookup"><span data-stu-id="bbf0a-348">Setting</span></span> | <span data-ttu-id="bbf0a-349">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="bbf0a-349">Default value</span></span> | <span data-ttu-id="bbf0a-350">Description</span><span class="sxs-lookup"><span data-stu-id="bbf0a-350">Description</span></span> |
| --- | --- | --- |
| `databases` |<span data-ttu-id="bbf0a-351">16</span><span class="sxs-lookup"><span data-stu-id="bbf0a-351">16</span></span> |<span data-ttu-id="bbf0a-352">nombre de bases de données par défaut de Hello est 16, mais vous pouvez configurer un autre hello selon numéro niveau tarifaire. <sup>1</sup> hello par défaut est DB 0, vous pouvez sélectionner une autre sur une base de chaque connexion à l’aide de `connection.GetDatabase(dbid)` où `dbid` est un nombre compris entre `0` et `databases - 1`.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-352">hello default number of databases is 16 but you can configure a different number based on hello pricing tier.<sup>1</sup> hello default database is DB 0, you can select a different one on a per-connection basis using `connection.GetDatabase(dbid)` where `dbid` is a number between `0` and `databases - 1`.</span></span> |
| `maxclients` |<span data-ttu-id="bbf0a-353">Varie selon le niveau tarifaire de hello<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="bbf0a-353">Depends on hello pricing tier<sup>2</sup></span></span> |<span data-ttu-id="bbf0a-354">Il s’agit hello le nombre maximal de clients connectés autorisé à hello même temps.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-354">This is hello maximum number of connected clients allowed at hello same time.</span></span> <span data-ttu-id="bbf0a-355">Hello limite atteinte Redis ferme toutes les connexions de la nouvelle hello, une erreur « nombre maximal de clients atteint ».</span><span class="sxs-lookup"><span data-stu-id="bbf0a-355">Once hello limit is reached Redis closes all hello new connections, returning a 'max number of clients reached' error.</span></span> |
| `maxmemory-policy` |`volatile-lru` |<span data-ttu-id="bbf0a-356">Stratégie MaxMemory est un paramètre de hello pour comment Redis sélectionne le tooremove lorsque `maxmemory` (hello la taille du cache hello offre vous avez sélectionné lors de la création du cache de hello) est atteinte.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-356">Maxmemory policy is hello setting for how Redis selects what tooremove when `maxmemory` (hello size of hello cache offering you selected when you created hello cache) is reached.</span></span> <span data-ttu-id="bbf0a-357">Valeur par défaut de Cache Redis Azure hello paramètre est `volatile-lru`, qui supprime les clés hello avec un délai d’expiration défini à l’aide d’un algorithme LRU.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-357">With Azure Redis Cache hello default setting is `volatile-lru`, which removes hello keys with an expiration set using an LRU algorithm.</span></span> <span data-ttu-id="bbf0a-358">Ce paramètre peut être configuré dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-358">This setting can be configured in hello Azure portal.</span></span> <span data-ttu-id="bbf0a-359">Pour plus d’informations, voir [Stratégies de mémoire](#memory-policies).</span><span class="sxs-lookup"><span data-stu-id="bbf0a-359">For more information, see [Memory policies](#memory-policies).</span></span> |
| `maxmemory-samples` |<span data-ttu-id="bbf0a-360">3</span><span class="sxs-lookup"><span data-stu-id="bbf0a-360">3</span></span> |<span data-ttu-id="bbf0a-361">toosave mémoire, LRU et les algorithmes de durée de vie minimale sont des algorithmes approximatives au lieu d’algorithmes précis.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-361">toosave memory, LRU and minimal TTL algorithms are approximated algorithms instead of precise algorithms.</span></span> <span data-ttu-id="bbf0a-362">Par défaut, Redis vérifie trois clés et récupère hello un moins récemment utilisé.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-362">By default Redis checks three keys and picks hello one that was used less recently.</span></span> |
| `lua-time-limit` |<span data-ttu-id="bbf0a-363">5 000</span><span class="sxs-lookup"><span data-stu-id="bbf0a-363">5,000</span></span> |<span data-ttu-id="bbf0a-364">Temps d’exécution maximal d’un script Lua en millisecondes.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-364">Max execution time of a Lua script in milliseconds.</span></span> <span data-ttu-id="bbf0a-365">Si la durée d’exécution maximale de hello est atteinte, Redis consigne qu’un script est toujours en exécution après hello maximale autorisée de temps et démarre tooreply tooqueries avec une erreur.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-365">If hello maximum execution time is reached, Redis logs that a script is still in execution after hello maximum allowed time, and starts tooreply tooqueries with an error.</span></span> |
| `lua-event-limit` |<span data-ttu-id="bbf0a-366">500</span><span class="sxs-lookup"><span data-stu-id="bbf0a-366">500</span></span> |<span data-ttu-id="bbf0a-367">Taille maximale de la file d’attente des événements de script.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-367">Max size of script event queue.</span></span> |
| <span data-ttu-id="bbf0a-368">`client-output-buffer-limit``normalclient-output-buffer-limit``pubsub`</span><span class="sxs-lookup"><span data-stu-id="bbf0a-368">`client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub`</span></span> |<span data-ttu-id="bbf0a-369">0 0 032mb 8mb 60</span><span class="sxs-lookup"><span data-stu-id="bbf0a-369">0 0 032mb 8mb 60</span></span> |<span data-ttu-id="bbf0a-370">Hello limites de mémoire tampon de sortie de client peuvent être utilisé tooforce une déconnexion des clients qui ne lisent pas les données à partir du serveur hello suffisamment rapide pour une raison quelconque (une raison courante est qu’un client Pub/Sub ne peuvent pas consommer les messages aussi rapidement qu’hello éditeur les produit).</span><span class="sxs-lookup"><span data-stu-id="bbf0a-370">hello client output buffer limits can be used tooforce disconnection of clients that are not reading data from hello server fast enough for some reason (a common reason is that a Pub/Sub client can't consume messages as fast as hello publisher can produce them).</span></span> <span data-ttu-id="bbf0a-371">Pour plus d’informations, consultez [http://redis.io/topics/clients](http://redis.io/topics/clients).</span><span class="sxs-lookup"><span data-stu-id="bbf0a-371">For more information, see [http://redis.io/topics/clients](http://redis.io/topics/clients).</span></span> |

<span data-ttu-id="bbf0a-372"><a name="databases"></a>
<sup>1</sup>limite hello pour `databases` est différent pour chaque Cache Azure Redis au niveau de tarification et peut être définie lors de la création du cache.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-372"><a name="databases"></a>
<sup>1</sup>hello limit for `databases` is different for each Azure Redis Cache pricing tier and can be set at cache creation.</span></span> <span data-ttu-id="bbf0a-373">Si aucun `databases` paramètre est spécifié lors de la création du cache, par défaut de hello est 16.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-373">If no `databases` setting is specified during cache creation, hello default is 16.</span></span>

* <span data-ttu-id="bbf0a-374">Caches De base et Standard</span><span class="sxs-lookup"><span data-stu-id="bbf0a-374">Basic and Standard caches</span></span>
  * <span data-ttu-id="bbf0a-375">C0 (250 Mo) de cache - des bases de données too16</span><span class="sxs-lookup"><span data-stu-id="bbf0a-375">C0 (250 MB) cache - up too16 databases</span></span>
  * <span data-ttu-id="bbf0a-376">C1 cache de (1 Go) - les bases de données too16</span><span class="sxs-lookup"><span data-stu-id="bbf0a-376">C1 (1 GB) cache - up too16 databases</span></span>
  * <span data-ttu-id="bbf0a-377">C2 cache de (2,5 Go) - les bases de données too16</span><span class="sxs-lookup"><span data-stu-id="bbf0a-377">C2 (2.5 GB) cache - up too16 databases</span></span>
  * <span data-ttu-id="bbf0a-378">C3 (6 Go) cache - les bases de données too16</span><span class="sxs-lookup"><span data-stu-id="bbf0a-378">C3 (6 GB) cache - up too16 databases</span></span>
  * <span data-ttu-id="bbf0a-379">C4 cache de (13 Go) - les bases de données too32</span><span class="sxs-lookup"><span data-stu-id="bbf0a-379">C4 (13 GB) cache - up too32 databases</span></span>
  * <span data-ttu-id="bbf0a-380">C5 (26 Go) de cache - les bases de données too48</span><span class="sxs-lookup"><span data-stu-id="bbf0a-380">C5 (26 GB) cache - up too48 databases</span></span>
  * <span data-ttu-id="bbf0a-381">C6 (53 Go) de cache - les bases de données too64</span><span class="sxs-lookup"><span data-stu-id="bbf0a-381">C6 (53 GB) cache - up too64 databases</span></span>
* <span data-ttu-id="bbf0a-382">Caches Premium</span><span class="sxs-lookup"><span data-stu-id="bbf0a-382">Premium caches</span></span>
  * <span data-ttu-id="bbf0a-383">P1 (6 Go - 60 Go) - les bases de données too16</span><span class="sxs-lookup"><span data-stu-id="bbf0a-383">P1 (6 GB - 60 GB) - up too16 databases</span></span>
  * <span data-ttu-id="bbf0a-384">P2 (13 à 130 Go) - les bases de données too32</span><span class="sxs-lookup"><span data-stu-id="bbf0a-384">P2 (13 GB - 130 GB) - up too32 databases</span></span>
  * <span data-ttu-id="bbf0a-385">P3 (26 à 260 Go) - les bases de données too48</span><span class="sxs-lookup"><span data-stu-id="bbf0a-385">P3 (26 GB - 260 GB) - up too48 databases</span></span>
  * <span data-ttu-id="bbf0a-386">P4 (53 à 530 Go) - les bases de données too64</span><span class="sxs-lookup"><span data-stu-id="bbf0a-386">P4 (53 GB - 530 GB) - up too64 databases</span></span>
  * <span data-ttu-id="bbf0a-387">Tous les caches de niveau premium avec le cluster Redis activé - Redis cluster prend uniquement en charge l’utilisation de la base de données 0 hello donc `databases` limiter pour n’importe quel cache premium avec le cluster Redis activé est effectivement 1 et hello [sélectionnez](http://redis.io/commands/select) commande n’est pas autorisée.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-387">All premium caches with Redis cluster enabled - Redis cluster only supports use of database 0 so hello `databases` limit for any premium cache with Redis cluster enabled is effectively 1 and hello [Select](http://redis.io/commands/select) command is not allowed.</span></span> <span data-ttu-id="bbf0a-388">Pour plus d’informations, consultez [dois-je toomake tout toouse d’application de modifications toomy client clustering ?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)</span><span class="sxs-lookup"><span data-stu-id="bbf0a-388">For more information, see [Do I need toomake any changes toomy client application toouse clustering?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)</span></span>

<span data-ttu-id="bbf0a-389">Pour plus d’informations sur les bases de données, consultez [Quelles sont les bases de données Redis ?](cache-faq.md#what-are-redis-databases)</span><span class="sxs-lookup"><span data-stu-id="bbf0a-389">For more information about databases, see [What are Redis databases?](cache-faq.md#what-are-redis-databases)</span></span>

> [!NOTE]
> <span data-ttu-id="bbf0a-390">Hello `databases` paramètre peut être configuré uniquement pendant la création du cache et uniquement à l’aide de PowerShell, CLI ou autres clients de gestion.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-390">hello `databases` setting can be configured only during cache creation and only using PowerShell, CLI, or other management clients.</span></span> <span data-ttu-id="bbf0a-391">Pour obtenir un exemple de configuration de `databases` lors de la création du cache à l’aide de PowerShell, voir [New-AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases).</span><span class="sxs-lookup"><span data-stu-id="bbf0a-391">For an example of configuring `databases` during cache creation using PowerShell, see [New-AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases).</span></span>
> 
> 

<span data-ttu-id="bbf0a-392"><a name="maxclients"></a>
<sup>2</sup>`maxclients` est différent pour chaque niveau tarifaire du cache Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-392"><a name="maxclients"></a>
<sup>2</sup>`maxclients` is different for each Azure Redis Cache pricing tier.</span></span>

* <span data-ttu-id="bbf0a-393">Caches De base et Standard</span><span class="sxs-lookup"><span data-stu-id="bbf0a-393">Basic and Standard caches</span></span>
  * <span data-ttu-id="bbf0a-394">C0 cache de (250 Mo) - les connexions de too256</span><span class="sxs-lookup"><span data-stu-id="bbf0a-394">C0 (250 MB) cache - up too256 connections</span></span>
  * <span data-ttu-id="bbf0a-395">C1 cache de (1 Go) - des too1, 000 connexions</span><span class="sxs-lookup"><span data-stu-id="bbf0a-395">C1 (1 GB) cache - up too1,000 connections</span></span>
  * <span data-ttu-id="bbf0a-396">C2 (2,5 Go) cache - des too2, 000 connexions</span><span class="sxs-lookup"><span data-stu-id="bbf0a-396">C2 (2.5 GB) cache - up too2,000 connections</span></span>
  * <span data-ttu-id="bbf0a-397">C3 (6 Go) cache - des too5, 000 connexions</span><span class="sxs-lookup"><span data-stu-id="bbf0a-397">C3 (6 GB) cache - up too5,000 connections</span></span>
  * <span data-ttu-id="bbf0a-398">C4 (13 Go) cache - des too10, 000 connexions</span><span class="sxs-lookup"><span data-stu-id="bbf0a-398">C4 (13 GB) cache - up too10,000 connections</span></span>
  * <span data-ttu-id="bbf0a-399">C5 (26 Go) cache - des too15, 000 connexions</span><span class="sxs-lookup"><span data-stu-id="bbf0a-399">C5 (26 GB) cache - up too15,000 connections</span></span>
  * <span data-ttu-id="bbf0a-400">C6 (53 Go) cache - des too20, 000 connexions</span><span class="sxs-lookup"><span data-stu-id="bbf0a-400">C6 (53 GB) cache - up too20,000 connections</span></span>
* <span data-ttu-id="bbf0a-401">Caches Premium</span><span class="sxs-lookup"><span data-stu-id="bbf0a-401">Premium caches</span></span>
  * <span data-ttu-id="bbf0a-402">P1 (6 Go - 60 Go) - des too7, 500 connexions</span><span class="sxs-lookup"><span data-stu-id="bbf0a-402">P1 (6 GB - 60 GB) - up too7,500 connections</span></span>
  * <span data-ttu-id="bbf0a-403">P2 (13 à 130 Go) - des too15, 000 connexions</span><span class="sxs-lookup"><span data-stu-id="bbf0a-403">P2 (13 GB - 130 GB) - up too15,000 connections</span></span>
  * <span data-ttu-id="bbf0a-404">P3 (26 à 260 Go) - des too30, 000 connexions</span><span class="sxs-lookup"><span data-stu-id="bbf0a-404">P3 (26 GB - 260 GB) - up too30,000 connections</span></span>
  * <span data-ttu-id="bbf0a-405">P4 (53 à 530 Go) - des too40, 000 connexions</span><span class="sxs-lookup"><span data-stu-id="bbf0a-405">P4 (53 GB - 530 GB) - up too40,000 connections</span></span>

> [!NOTE]
> <span data-ttu-id="bbf0a-406">Tandis que chaque taille de cache permet aux *jusqu'à* un certain nombre de connexions, chaque tooRedis connexion surcharge associée.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-406">While each size of cache allows *up to* a certain number of connections, each connection tooRedis has overhead associated with it.</span></span> <span data-ttu-id="bbf0a-407">Un exemple d’une telle surcharge est l’utilisation du processeur et de la mémoire à la suite d’un chiffrement TLS/SSL.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-407">An example of such overhead would be CPU and memory usage as a result of TLS/SSL encryption.</span></span> <span data-ttu-id="bbf0a-408">limite du nombre maximal de connexions Hello pour une taille de cache donné suppose un cache peu chargé.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-408">hello maximum connection limit for a given cache size assumes a lightly loaded cache.</span></span> <span data-ttu-id="bbf0a-409">Si charger à partir de la charge de la connexion *plus* charge à partir d’opérations du client dépasse la capacité pour le système de hello, le cache de hello peut rencontrer des problèmes de capacité même si vous ne dépassez pas la limite de connexions hello pour hello taille actuelle du cache.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-409">If load from connection overhead *plus* load from client operations exceeds capacity for hello system, hello cache can experience capacity issues even if you have not exceeded hello connection limit for hello current cache size.</span></span>
> 
> 



## <a name="redis-commands-not-supported-in-azure-redis-cache"></a><span data-ttu-id="bbf0a-410">Commandes Redis non prises en charge dans le Cache Redis Azure</span><span class="sxs-lookup"><span data-stu-id="bbf0a-410">Redis commands not supported in Azure Redis Cache</span></span>
> [!IMPORTANT]
> <span data-ttu-id="bbf0a-411">Étant donné que la configuration et la gestion des instances de Cache Redis Azure est géré par Microsoft, hello commandes suivantes sont désactivées.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-411">Because configuration and management of Azure Redis Cache instances is managed by Microsoft, hello following commands are disabled.</span></span> <span data-ttu-id="bbf0a-412">Si vous essayez de tooinvoke les, vous recevez un message d’erreur similaire trop`"(error) ERR unknown command"`.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-412">If you try tooinvoke them, you receive an error message similar too`"(error) ERR unknown command"`.</span></span>
> 
> * <span data-ttu-id="bbf0a-413">BGREWRITEAOF</span><span class="sxs-lookup"><span data-stu-id="bbf0a-413">BGREWRITEAOF</span></span>
> * <span data-ttu-id="bbf0a-414">BGSAVE</span><span class="sxs-lookup"><span data-stu-id="bbf0a-414">BGSAVE</span></span>
> * <span data-ttu-id="bbf0a-415">CONFIG</span><span class="sxs-lookup"><span data-stu-id="bbf0a-415">CONFIG</span></span>
> * <span data-ttu-id="bbf0a-416">DEBUG</span><span class="sxs-lookup"><span data-stu-id="bbf0a-416">DEBUG</span></span>
> * <span data-ttu-id="bbf0a-417">MIGRATE</span><span class="sxs-lookup"><span data-stu-id="bbf0a-417">MIGRATE</span></span>
> * <span data-ttu-id="bbf0a-418">Enregistrer</span><span class="sxs-lookup"><span data-stu-id="bbf0a-418">SAVE</span></span>
> * <span data-ttu-id="bbf0a-419">SHUTDOWN</span><span class="sxs-lookup"><span data-stu-id="bbf0a-419">SHUTDOWN</span></span>
> * <span data-ttu-id="bbf0a-420">SLAVEOF</span><span class="sxs-lookup"><span data-stu-id="bbf0a-420">SLAVEOF</span></span>
> * <span data-ttu-id="bbf0a-421">CLUSTER : les commandes d’écriture du cluster sont désactivées, mais celles de lecture seule sont autorisées.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-421">CLUSTER - Cluster write commands are disabled, but read-only Cluster commands are permitted.</span></span>
> 
> 

<span data-ttu-id="bbf0a-422">Pour plus d’informations sur les commandes Redis, consultez [http://redis.io/commands](http://redis.io/commands).</span><span class="sxs-lookup"><span data-stu-id="bbf0a-422">For more information about Redis commands, see [http://redis.io/commands](http://redis.io/commands).</span></span>

## <a name="redis-console"></a><span data-ttu-id="bbf0a-423">Console Redis</span><span class="sxs-lookup"><span data-stu-id="bbf0a-423">Redis console</span></span>
<span data-ttu-id="bbf0a-424">Vous pouvez exécuter en toute sécurité des commandes tooyour instances de Cache Redis Azure à l’aide de hello **Redis de Console**, qui est disponible dans le portail Azure pour tous les niveaux de cache de hello.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-424">You can securely issue commands tooyour Azure Redis Cache instances using hello **Redis Console**, which is available in hello Azure portal for all cache tiers.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="bbf0a-425">Hello Redis Console ne fonctionne pas avec [réseau virtuel](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="bbf0a-425">hello Redis Console does not work with [VNET](cache-how-to-premium-vnet.md).</span></span> <span data-ttu-id="bbf0a-426">Lorsque votre cache fait partie d’un réseau virtuel, uniquement les clients Bonjour réseau virtuel peuvent accéder les cache hello.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-426">When your cache is part of a VNET, only clients in hello VNET can access hello cache.</span></span> <span data-ttu-id="bbf0a-427">Console de Redis s’exécutant dans votre navigateur, qui est en dehors de hello réseau virtuel, il ne peut pas se connecter tooyour cache.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-427">Because Redis Console runs in your local browser, which is outside hello VNET, it can't connect tooyour cache.</span></span>
> - <span data-ttu-id="bbf0a-428">Les commandes Redis ne sont pas toutes prises en charge dans le Cache Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-428">Not all Redis commands are supported in Azure Redis Cache.</span></span> <span data-ttu-id="bbf0a-429">Pour obtenir la liste des commandes de Redis sont désactivées pour le Cache Redis Azure, consultez hello précédente [Redis commandes non prises en charge dans le Cache Redis Azure](#redis-commands-not-supported-in-azure-redis-cache) section.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-429">For a list of Redis commands that are disabled for Azure Redis Cache, see hello previous [Redis commands not supported in Azure Redis Cache](#redis-commands-not-supported-in-azure-redis-cache) section.</span></span> <span data-ttu-id="bbf0a-430">Pour plus d’informations sur les commandes Redis, consultez [http://redis.io/commands](http://redis.io/commands).</span><span class="sxs-lookup"><span data-stu-id="bbf0a-430">For more information about Redis commands, see [http://redis.io/commands](http://redis.io/commands).</span></span>
> 
> 

<span data-ttu-id="bbf0a-431">tooaccess hello Console Redis, cliquez sur **Console** de hello **Cache Redis** panneau.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-431">tooaccess hello Redis Console, click **Console** from hello **Redis Cache** blade.</span></span>

![Console Redis](./media/cache-configure/redis-console-menu.png)

<span data-ttu-id="bbf0a-433">commandes de tooissue sur votre instance de cache, hello de type simplement souhaité commande dans la console de hello.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-433">tooissue commands against your cache instance, simply type hello desired command into hello console.</span></span>

![Console Redis](./media/cache-configure/redis-console.png)


### <a name="using-hello-redis-console-with-a-premium-clustered-cache"></a><span data-ttu-id="bbf0a-435">À l’aide de hello Redis de Console avec une prime en cluster du cache</span><span class="sxs-lookup"><span data-stu-id="bbf0a-435">Using hello Redis Console with a premium clustered cache</span></span>

<span data-ttu-id="bbf0a-436">Lorsque le cache à l’aide de hello Redis de Console avec une prime de cluster, vous pouvez émettre des commandes tooa même partition du cache de hello.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-436">When using hello Redis Console with a premium clustered cache, you can issue commands tooa single shard of hello cache.</span></span> <span data-ttu-id="bbf0a-437">tooissue une partition spécifique tooa de commande, connectez-vous d’abord toohello partition de votre choix en cliquant dessus dans le sélecteur de partitions hello.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-437">tooissue a command tooa specific shard, first connect toohello desired shard by clicking it on hello shard picker.</span></span>

![Console Redis](./media/cache-configure/redis-console-premium-cluster.png)

<span data-ttu-id="bbf0a-439">Si vous essayez de tooaccess une clé qui est stockée dans une autre partition que hello partition connectée, vous recevez une erreur message similaire toohello message suivant.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-439">If you attempt tooaccess a key that is stored in a different shard than hello connected shard, you receive an error message similar toohello following message.</span></span>

```
shard1>get myKey
(error) MOVED 866 13.90.202.154:13000 (shard 0)
```

<span data-ttu-id="bbf0a-440">Dans l’exemple précédent de hello, partition 1 est la partition sélectionnée de hello, mais `myKey` se trouve dans la partition 0, comme indiqué par hello `(shard 0)` partie du message d’erreur hello.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-440">In hello previous example, shard 1 is hello selected shard, but `myKey` is located in shard 0, as indicated by hello `(shard 0)` portion of hello error message.</span></span> <span data-ttu-id="bbf0a-441">Dans cet exemple, tooaccess `myKey`, sélectionnez à l’aide de la partition 0 hello sélecteur de partition, puis commande hello souhaité de problème.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-441">In this example, tooaccess `myKey`, select shard 0 using hello shard picker, and then issue hello desired command.</span></span>


## <a name="move-your-cache-tooa-new-subscription"></a><span data-ttu-id="bbf0a-442">Déplacez votre cache tooa un nouvel abonnement</span><span class="sxs-lookup"><span data-stu-id="bbf0a-442">Move your cache tooa new subscription</span></span>
<span data-ttu-id="bbf0a-443">Vous pouvez déplacer votre cache tooa un nouvel abonnement en cliquant sur **déplacer**.</span><span class="sxs-lookup"><span data-stu-id="bbf0a-443">You can move your cache tooa new subscription by clicking **Move**.</span></span>

![Déplacer le Cache Redis](./media/cache-configure/redis-cache-move.png)

<span data-ttu-id="bbf0a-445">Pour plus d’informations sur le déplacement de ressources à partir d’une ressource groupe tooanother et à partir d’un seul abonnement tooanother, consultez [déplacer le groupe de ressources toonew ressources ou d’un abonnement](../azure-resource-manager/resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="bbf0a-445">For information on moving resources from one resource group tooanother, and from one subscription tooanother, see [Move resources toonew resource group or subscription](../azure-resource-manager/resource-group-move-resources.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bbf0a-446">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bbf0a-446">Next steps</span></span>
* <span data-ttu-id="bbf0a-447">Pour plus d’informations sur l’utilisation des commandes Redis, voir [Exécution des commandes Redis](cache-faq.md#how-can-i-run-redis-commands).</span><span class="sxs-lookup"><span data-stu-id="bbf0a-447">For more information on working with Redis commands, see [How can I run Redis commands?](cache-faq.md#how-can-i-run-redis-commands)</span></span>

