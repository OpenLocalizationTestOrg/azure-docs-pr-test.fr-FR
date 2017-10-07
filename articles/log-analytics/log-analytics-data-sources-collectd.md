---
title: "données aaaCollect CollectD dans Analytique des journaux OMS | Documents Microsoft"
description: "CollectD est un démon Linux open source qui collecte périodiquement les données des applications et des informations de niveau système.  Cet article fournit des informations sur la collecte de données à partir de CollectD dans Log Analytics."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: f1d5bde4-6b86-4b8e-b5c1-3ecbaba76198
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/02/2017
ms.author: magoedte
ms.openlocfilehash: 7ad82c9c67a664aabd44f08bef2253d84cd2dfba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-data-from-collectd-on-linux-agents-in-log-analytics"></a><span data-ttu-id="e0800-104">Collecter des données à partir de CollectD sur les agents Linux dans Log Analytics</span><span class="sxs-lookup"><span data-stu-id="e0800-104">Collect data from CollectD on Linux agents in Log Analytics</span></span>
<span data-ttu-id="e0800-105">[CollectD](https://collectd.org/) est un démon Linux open source qui collecte périodiquement des mesures de performances à partir d’applications et d’informations de niveau système.</span><span class="sxs-lookup"><span data-stu-id="e0800-105">[CollectD](https://collectd.org/) is an open source Linux daemon that periodically collects performance metrics from applications and system level information.</span></span> <span data-ttu-id="e0800-106">Exemples d’applications incluent Nginx, MySQL Server et hello Machine virtuelle Java (JVM).</span><span class="sxs-lookup"><span data-stu-id="e0800-106">Example applications include hello Java Virtual Machine (JVM), MySQL Server, and Nginx.</span></span> <span data-ttu-id="e0800-107">Cet article fournit des informations sur la collecte des données de performances à partir de CollectD dans Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="e0800-107">This article provides information on collecting performance data from CollectD in Log Analytics.</span></span>

<span data-ttu-id="e0800-108">Vous trouverez la liste complète des plug-ins disponibles dans le [tableau de plug-ins](https://collectd.org/wiki/index.php/Table_of_Plugins).</span><span class="sxs-lookup"><span data-stu-id="e0800-108">A full list of available plugins can be found at [Table of Plugins](https://collectd.org/wiki/index.php/Table_of_Plugins).</span></span>

![Vue d’ensemble de CollectD](media/log-analytics-data-sources-collectd/overview.png)

<span data-ttu-id="e0800-110">Hello CollectD de configuration suivant est inclus dans hello Agent OMS pour Linux tooroute CollectD données toohello Agent OMS pour Linux.</span><span class="sxs-lookup"><span data-stu-id="e0800-110">hello following CollectD configuration is included in hello OMS Agent for Linux tooroute  CollectD data toohello OMS Agent for Linux.</span></span>

    LoadPlugin write_http

    <Plugin write_http>
         <Node "oms">
         URL "127.0.0.1:26000/oms.collectd"
         Format "JSON"
         StoreRates true
         </Node>
    </Plugin>

<span data-ttu-id="e0800-111">En outre, si vous utilisez une version de collectD avant 5.5 utiliser hello configuration suivante à la place.</span><span class="sxs-lookup"><span data-stu-id="e0800-111">Additionally, if using an versions of collectD before 5.5 use hello following configuration instead.</span></span>

    LoadPlugin write_http

    <Plugin write_http>
       <URL "127.0.0.1:26000/oms.collectd">
        Format "JSON"
         StoreRates true
       </URL>
    </Plugin>

<span data-ttu-id="e0800-112">configuration de CollectD Hello utilise par défaut de hello`write_http` données métriques de performances toosend plug-in sur le port de 26000 tooOMS Agent pour Linux.</span><span class="sxs-lookup"><span data-stu-id="e0800-112">hello CollectD configuration uses hello default`write_http` plugin toosend performance metric data over port 26000 tooOMS Agent for Linux.</span></span> 

> [!NOTE]
> <span data-ttu-id="e0800-113">Ce port peut être configuré tooa personnalisées port si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e0800-113">This port can be configured tooa custom-defined port if needed.</span></span>

<span data-ttu-id="e0800-114">Hello Agent OMS pour Linux écoute également sur le port 26000 CollectD métriques, puis les convertit les métriques de schéma tooOMS.</span><span class="sxs-lookup"><span data-stu-id="e0800-114">hello OMS Agent for Linux also listens on port 26000 for CollectD metrics and then converts them tooOMS schema metrics.</span></span> <span data-ttu-id="e0800-115">Hello Voici hello Agent OMS pour Linux configuration `collectd.conf`.</span><span class="sxs-lookup"><span data-stu-id="e0800-115">hello following is hello OMS Agent for Linux configuration  `collectd.conf`.</span></span>

    <source>
      type http
      port 26000
      bind 127.0.0.1
    </source>

    <filter oms.collectd>
      type filter_collectd
    </filter>


## <a name="versions-supported"></a><span data-ttu-id="e0800-116">Versions prises en charge</span><span class="sxs-lookup"><span data-stu-id="e0800-116">Versions supported</span></span>
- <span data-ttu-id="e0800-117">Log Analytics prend actuellement en charge la version 4.8 et les versions ultérieures de CollectD.</span><span class="sxs-lookup"><span data-stu-id="e0800-117">Log Analytics currently supports CollectD version 4.8 and above.</span></span>
- <span data-ttu-id="e0800-118">L’agent OMS pour Linux v1.1.0-217 ou version ultérieure est requis pour la collecte des mesures CollectD.</span><span class="sxs-lookup"><span data-stu-id="e0800-118">OMS Agent for Linux v1.1.0-217 or above is required for CollectD metric collection.</span></span>


## <a name="configuration"></a><span data-ttu-id="e0800-119">Configuration</span><span class="sxs-lookup"><span data-stu-id="e0800-119">Configuration</span></span>
<span data-ttu-id="e0800-120">Hello Voici une collection de tooconfigure étapes de base de données CollectD dans le journal Analytique.</span><span class="sxs-lookup"><span data-stu-id="e0800-120">hello following are basic steps tooconfigure collection of CollectD data in Log Analytics.</span></span>

1. <span data-ttu-id="e0800-121">Configurer CollectD toosend données toohello Agent OMS pour Linux à l’aide du plug-in de write_http hello.</span><span class="sxs-lookup"><span data-stu-id="e0800-121">Configure CollectD toosend data toohello OMS Agent for Linux using hello write_http plugin.</span></span>  
2. <span data-ttu-id="e0800-122">Configurer hello Agent OMS pour toolisten Linux pour hello CollectD données sur le port approprié de hello.</span><span class="sxs-lookup"><span data-stu-id="e0800-122">Configure hello OMS Agent for Linux toolisten for hello CollectD data on hello appropriate port.</span></span>
3. <span data-ttu-id="e0800-123">Redémarrez CollectD et l’agent OMS pour Linux.</span><span class="sxs-lookup"><span data-stu-id="e0800-123">Restart CollectD and OMS Agent for Linux.</span></span>

### <a name="configure-collectd-tooforward-data"></a><span data-ttu-id="e0800-124">Configurer les données de tooforward CollectD</span><span class="sxs-lookup"><span data-stu-id="e0800-124">Configure CollectD tooforward data</span></span> 

1. <span data-ttu-id="e0800-125">tooroute CollectD données toohello Agent OMS pour Linux, `oms.conf` besoins toobe ajouté le répertoire de configuration de tooCollectD.</span><span class="sxs-lookup"><span data-stu-id="e0800-125">tooroute CollectD data toohello OMS Agent for Linux, `oms.conf` needs toobe added tooCollectD's configuration directory.</span></span> <span data-ttu-id="e0800-126">destination Hello de ce fichier dépend de la distribution de Linux hello de votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="e0800-126">hello destination of this file depends on hello Linux  distro of your machine.</span></span>

    <span data-ttu-id="e0800-127">Si votre répertoire de configuration CollectD se trouve dans /etc/collectd.d/ :</span><span class="sxs-lookup"><span data-stu-id="e0800-127">If your CollectD config directory is located in /etc/collectd.d/:</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd.d/oms.conf

    <span data-ttu-id="e0800-128">Si votre répertoire de configuration CollectD se trouve dans /etc/collectd/collectd.conf.d/ :</span><span class="sxs-lookup"><span data-stu-id="e0800-128">If your CollectD config directory is located in /etc/collectd/collectd.conf.d/:</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd/collectd.conf.d/oms.conf

    >[!NOTE]
    ><span data-ttu-id="e0800-129">Pour les versions CollectD avant 5.5 avoir des balises de hello toomodify dans `oms.conf` comme indiqué ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="e0800-129">For CollectD versions before 5.5 you will have toomodify hello tags in `oms.conf` as shown above.</span></span>
    >

2. <span data-ttu-id="e0800-130">Copiez le répertoire de configuration omsagent collectd.conf toohello souhaité l’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="e0800-130">Copy collectd.conf toohello desired workspace's omsagent configuration directory.</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/collectd.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/
        sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/collectd.conf

3. <span data-ttu-id="e0800-131">Redémarrez CollectD et l’Agent OMS pour Linux avec hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="e0800-131">Restart CollectD and OMS Agent for Linux with hello following commands.</span></span>

    <span data-ttu-id="e0800-132">sudo service collectd restart  sudo /opt/microsoft/omsagent/bin/service_control restart</span><span class="sxs-lookup"><span data-stu-id="e0800-132">sudo service collectd restart  sudo /opt/microsoft/omsagent/bin/service_control restart</span></span>

## <a name="collectd-metrics-toolog-analytics-schema-conversion"></a><span data-ttu-id="e0800-133">CollectD métriques tooLog conversion du schéma Analytique</span><span class="sxs-lookup"><span data-stu-id="e0800-133">CollectD metrics tooLog Analytics schema conversion</span></span>
<span data-ttu-id="e0800-134">toomaintain un modèle familier entre les mesures d’infrastructure déjà collectées par l’Agent OMS pour Linux et hello nouvelles mesures collectées par CollectD hello suivant le mappage de schéma est utilisé :</span><span class="sxs-lookup"><span data-stu-id="e0800-134">toomaintain a familiar model between infrastructure metrics already collected by OMS Agent for Linux and hello new metrics collected by CollectD hello following schema mapping is used:</span></span>

| <span data-ttu-id="e0800-135">Champ Mesure CollectD</span><span class="sxs-lookup"><span data-stu-id="e0800-135">CollectD Metric field</span></span> | <span data-ttu-id="e0800-136">Champ Log Analytics</span><span class="sxs-lookup"><span data-stu-id="e0800-136">Log Analytics field</span></span> |
|:--|:--|
| <span data-ttu-id="e0800-137">host</span><span class="sxs-lookup"><span data-stu-id="e0800-137">host</span></span> | <span data-ttu-id="e0800-138">Ordinateur</span><span class="sxs-lookup"><span data-stu-id="e0800-138">Computer</span></span> |
| <span data-ttu-id="e0800-139">plugin</span><span class="sxs-lookup"><span data-stu-id="e0800-139">plugin</span></span> | <span data-ttu-id="e0800-140">Aucun</span><span class="sxs-lookup"><span data-stu-id="e0800-140">None</span></span> |
| <span data-ttu-id="e0800-141">plugin_instance</span><span class="sxs-lookup"><span data-stu-id="e0800-141">plugin_instance</span></span> | <span data-ttu-id="e0800-142">Nom de l’instance</span><span class="sxs-lookup"><span data-stu-id="e0800-142">Instance Name</span></span><br><span data-ttu-id="e0800-143">If **plugin_instance** is *null* then InstanceName="*_Total*"</span><span class="sxs-lookup"><span data-stu-id="e0800-143">If **plugin_instance** is *null* then InstanceName="*_Total*"</span></span> |
| <span data-ttu-id="e0800-144">type</span><span class="sxs-lookup"><span data-stu-id="e0800-144">type</span></span> | <span data-ttu-id="e0800-145">ObjectName</span><span class="sxs-lookup"><span data-stu-id="e0800-145">ObjectName</span></span> |
| <span data-ttu-id="e0800-146">type_instance</span><span class="sxs-lookup"><span data-stu-id="e0800-146">type_instance</span></span> | <span data-ttu-id="e0800-147">CounterName</span><span class="sxs-lookup"><span data-stu-id="e0800-147">CounterName</span></span><br><span data-ttu-id="e0800-148">If **type_instance** is *null* then CounterName=**blank**</span><span class="sxs-lookup"><span data-stu-id="e0800-148">If **type_instance** is *null* then CounterName=**blank**</span></span> |
| <span data-ttu-id="e0800-149">dsnames[]</span><span class="sxs-lookup"><span data-stu-id="e0800-149">dsnames[]</span></span> | <span data-ttu-id="e0800-150">CounterName</span><span class="sxs-lookup"><span data-stu-id="e0800-150">CounterName</span></span> |
| <span data-ttu-id="e0800-151">dstypes</span><span class="sxs-lookup"><span data-stu-id="e0800-151">dstypes</span></span> | <span data-ttu-id="e0800-152">Aucun</span><span class="sxs-lookup"><span data-stu-id="e0800-152">None</span></span> |
| <span data-ttu-id="e0800-153">values[]</span><span class="sxs-lookup"><span data-stu-id="e0800-153">values[]</span></span> | <span data-ttu-id="e0800-154">CounterValue</span><span class="sxs-lookup"><span data-stu-id="e0800-154">CounterValue</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e0800-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e0800-155">Next steps</span></span>
* <span data-ttu-id="e0800-156">En savoir plus sur [recherche de journal](log-analytics-log-searches.md) tooanalyze les données de salutation collectées à partir de sources de données et les solutions possibles.</span><span class="sxs-lookup"><span data-stu-id="e0800-156">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span> 
* <span data-ttu-id="e0800-157">Utilisez [les champs personnalisés](log-analytics-custom-fields.md) tooparse des données à partir d’enregistrements syslog dans des champs individuels.</span><span class="sxs-lookup"><span data-stu-id="e0800-157">Use [Custom Fields](log-analytics-custom-fields.md) tooparse data from syslog records into individual fields.</span></span>

