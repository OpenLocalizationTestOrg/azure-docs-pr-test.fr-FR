---
title: "Collecter les données à partir de CollectD dans OMS Log Analytics | Documents Microsoft"
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
ms.openlocfilehash: a63b15ca5126b45451f0694c9ee75d7b67b1ceaf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="collect-data-from-collectd-on-linux-agents-in-log-analytics"></a><span data-ttu-id="95607-104">Collecter des données à partir de CollectD sur les agents Linux dans Log Analytics</span><span class="sxs-lookup"><span data-stu-id="95607-104">Collect data from CollectD on Linux agents in Log Analytics</span></span>
<span data-ttu-id="95607-105">[CollectD](https://collectd.org/) est un démon Linux open source qui collecte périodiquement des mesures de performances à partir d’applications et d’informations de niveau système.</span><span class="sxs-lookup"><span data-stu-id="95607-105">[CollectD](https://collectd.org/) is an open source Linux daemon that periodically collects performance metrics from applications and system level information.</span></span> <span data-ttu-id="95607-106">Les applications peuvent être, par exemple, la machine virtuelle Java (JVM), le serveur MySQL et Nginx.</span><span class="sxs-lookup"><span data-stu-id="95607-106">Example applications include the Java Virtual Machine (JVM), MySQL Server, and Nginx.</span></span> <span data-ttu-id="95607-107">Cet article fournit des informations sur la collecte des données de performances à partir de CollectD dans Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="95607-107">This article provides information on collecting performance data from CollectD in Log Analytics.</span></span>

<span data-ttu-id="95607-108">Vous trouverez la liste complète des plug-ins disponibles dans le [tableau de plug-ins](https://collectd.org/wiki/index.php/Table_of_Plugins).</span><span class="sxs-lookup"><span data-stu-id="95607-108">A full list of available plugins can be found at [Table of Plugins](https://collectd.org/wiki/index.php/Table_of_Plugins).</span></span>

![Vue d’ensemble de CollectD](media/log-analytics-data-sources-collectd/overview.png)

<span data-ttu-id="95607-110">La configuration CollectD suivante est incluse dans l’agent OMS pour Linux pour acheminer des données CollectD vers l’agent OMS pour Linux.</span><span class="sxs-lookup"><span data-stu-id="95607-110">The following CollectD configuration is included in the OMS Agent for Linux to route  CollectD data to the OMS Agent for Linux.</span></span>

    LoadPlugin write_http

    <Plugin write_http>
         <Node "oms">
         URL "127.0.0.1:26000/oms.collectd"
         Format "JSON"
         StoreRates true
         </Node>
    </Plugin>

<span data-ttu-id="95607-111">En outre, si vous utilisez une version de CollectD antérieure à 5.5, utilisez plutôt la configuration suivante.</span><span class="sxs-lookup"><span data-stu-id="95607-111">Additionally, if using an versions of collectD before 5.5 use the following configuration instead.</span></span>

    LoadPlugin write_http

    <Plugin write_http>
       <URL "127.0.0.1:26000/oms.collectd">
        Format "JSON"
         StoreRates true
       </URL>
    </Plugin>

<span data-ttu-id="95607-112">La configuration CollectD utilise le plug-in par défaut`write_http` pour envoyer des données de mesure de performances sur le port 26000 à l’agent OMS pour Linux.</span><span class="sxs-lookup"><span data-stu-id="95607-112">The CollectD configuration uses the default`write_http` plugin to send performance metric data over port 26000 to OMS Agent for Linux.</span></span> 

> [!NOTE]
> <span data-ttu-id="95607-113">Ce port peut être configuré sur un port personnalisé, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="95607-113">This port can be configured to a custom-defined port if needed.</span></span>

<span data-ttu-id="95607-114">L’agent OMS pour Linux écoute également les mesures CollectD sur le port 26000 et les convertit ensuite en mesures de schéma OMS.</span><span class="sxs-lookup"><span data-stu-id="95607-114">The OMS Agent for Linux also listens on port 26000 for CollectD metrics and then converts them to OMS schema metrics.</span></span> <span data-ttu-id="95607-115">L’agent OMS pour la configuration Linux est le suivant : `collectd.conf`.</span><span class="sxs-lookup"><span data-stu-id="95607-115">The following is the OMS Agent for Linux configuration  `collectd.conf`.</span></span>

    <source>
      type http
      port 26000
      bind 127.0.0.1
    </source>

    <filter oms.collectd>
      type filter_collectd
    </filter>


## <a name="versions-supported"></a><span data-ttu-id="95607-116">Versions prises en charge</span><span class="sxs-lookup"><span data-stu-id="95607-116">Versions supported</span></span>
- <span data-ttu-id="95607-117">Log Analytics prend actuellement en charge la version 4.8 et les versions ultérieures de CollectD.</span><span class="sxs-lookup"><span data-stu-id="95607-117">Log Analytics currently supports CollectD version 4.8 and above.</span></span>
- <span data-ttu-id="95607-118">L’agent OMS pour Linux v1.1.0-217 ou version ultérieure est requis pour la collecte des mesures CollectD.</span><span class="sxs-lookup"><span data-stu-id="95607-118">OMS Agent for Linux v1.1.0-217 or above is required for CollectD metric collection.</span></span>


## <a name="configuration"></a><span data-ttu-id="95607-119">Configuration</span><span class="sxs-lookup"><span data-stu-id="95607-119">Configuration</span></span>
<span data-ttu-id="95607-120">Les étapes de base pour configurer la collecte des données CollectD dans Log Analytics sont les suivantes.</span><span class="sxs-lookup"><span data-stu-id="95607-120">The following are basic steps to configure collection of CollectD data in Log Analytics.</span></span>

1. <span data-ttu-id="95607-121">Configurez CollectD pour qu’il envoie des données à l’agent OMS pour Linux à l’aide du plug-in write_http.</span><span class="sxs-lookup"><span data-stu-id="95607-121">Configure CollectD to send data to the OMS Agent for Linux using the write_http plugin.</span></span>  
2. <span data-ttu-id="95607-122">Configurez l’agent OMS pour Linux afin qu’il écoute les données CollectD sur le port approprié.</span><span class="sxs-lookup"><span data-stu-id="95607-122">Configure the OMS Agent for Linux to listen for the CollectD data on the appropriate port.</span></span>
3. <span data-ttu-id="95607-123">Redémarrez CollectD et l’agent OMS pour Linux.</span><span class="sxs-lookup"><span data-stu-id="95607-123">Restart CollectD and OMS Agent for Linux.</span></span>

### <a name="configure-collectd-to-forward-data"></a><span data-ttu-id="95607-124">Configuration de CollectD pour le transfert des données</span><span class="sxs-lookup"><span data-stu-id="95607-124">Configure CollectD to forward data</span></span> 

1. <span data-ttu-id="95607-125">Pour acheminer les données CollectD vers l’agent OMS pour Linux, `oms.conf` doit être ajouté au répertoire de configuration de CollectD.</span><span class="sxs-lookup"><span data-stu-id="95607-125">To route CollectD data to the OMS Agent for Linux, `oms.conf` needs to be added to CollectD's configuration directory.</span></span> <span data-ttu-id="95607-126">La destination de ce fichier dépend de la distribution Linux de votre machine.</span><span class="sxs-lookup"><span data-stu-id="95607-126">The destination of this file depends on the Linux  distro of your machine.</span></span>

    <span data-ttu-id="95607-127">Si votre répertoire de configuration CollectD se trouve dans /etc/collectd.d/ :</span><span class="sxs-lookup"><span data-stu-id="95607-127">If your CollectD config directory is located in /etc/collectd.d/:</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd.d/oms.conf

    <span data-ttu-id="95607-128">Si votre répertoire de configuration CollectD se trouve dans /etc/collectd/collectd.conf.d/ :</span><span class="sxs-lookup"><span data-stu-id="95607-128">If your CollectD config directory is located in /etc/collectd/collectd.conf.d/:</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd/collectd.conf.d/oms.conf

    >[!NOTE]
    ><span data-ttu-id="95607-129">Pour les versions de CollectD antérieures à 5.5, vous devrez modifier les balises dans `oms.conf`, comme indiqué ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="95607-129">For CollectD versions before 5.5 you will have to modify the tags in `oms.conf` as shown above.</span></span>
    >

2. <span data-ttu-id="95607-130">Copiez collectd.conf vers le répertoire de configuration omsagent de l’espace de travail souhaité.</span><span class="sxs-lookup"><span data-stu-id="95607-130">Copy collectd.conf to the desired workspace's omsagent configuration directory.</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/collectd.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/
        sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/collectd.conf

3. <span data-ttu-id="95607-131">Redémarrez CollectD et l’agent OMS pour Linux à l’aide des commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="95607-131">Restart CollectD and OMS Agent for Linux with the following commands.</span></span>

    <span data-ttu-id="95607-132">sudo service collectd restart  sudo /opt/microsoft/omsagent/bin/service_control restart</span><span class="sxs-lookup"><span data-stu-id="95607-132">sudo service collectd restart  sudo /opt/microsoft/omsagent/bin/service_control restart</span></span>

## <a name="collectd-metrics-to-log-analytics-schema-conversion"></a><span data-ttu-id="95607-133">Mesures CollectD pour la conversion de schéma Log Analytics</span><span class="sxs-lookup"><span data-stu-id="95607-133">CollectD metrics to Log Analytics schema conversion</span></span>
<span data-ttu-id="95607-134">Pour conserver un modèle cohérent entre les mesures d’infrastructure déjà collectées par l’agent OMS pour Linux et les nouvelles mesures collectées par CollectD, le mappage de schéma suivant est utilisé :</span><span class="sxs-lookup"><span data-stu-id="95607-134">To maintain a familiar model between infrastructure metrics already collected by OMS Agent for Linux and the new metrics collected by CollectD the following schema mapping is used:</span></span>

| <span data-ttu-id="95607-135">Champ Mesure CollectD</span><span class="sxs-lookup"><span data-stu-id="95607-135">CollectD Metric field</span></span> | <span data-ttu-id="95607-136">Champ Log Analytics</span><span class="sxs-lookup"><span data-stu-id="95607-136">Log Analytics field</span></span> |
|:--|:--|
| <span data-ttu-id="95607-137">host</span><span class="sxs-lookup"><span data-stu-id="95607-137">host</span></span> | <span data-ttu-id="95607-138">Ordinateur</span><span class="sxs-lookup"><span data-stu-id="95607-138">Computer</span></span> |
| <span data-ttu-id="95607-139">plugin</span><span class="sxs-lookup"><span data-stu-id="95607-139">plugin</span></span> | <span data-ttu-id="95607-140">Aucun</span><span class="sxs-lookup"><span data-stu-id="95607-140">None</span></span> |
| <span data-ttu-id="95607-141">plugin_instance</span><span class="sxs-lookup"><span data-stu-id="95607-141">plugin_instance</span></span> | <span data-ttu-id="95607-142">Nom de l’instance</span><span class="sxs-lookup"><span data-stu-id="95607-142">Instance Name</span></span><br><span data-ttu-id="95607-143">If **plugin_instance** is *null* then InstanceName="*_Total*"</span><span class="sxs-lookup"><span data-stu-id="95607-143">If **plugin_instance** is *null* then InstanceName="*_Total*"</span></span> |
| <span data-ttu-id="95607-144">type</span><span class="sxs-lookup"><span data-stu-id="95607-144">type</span></span> | <span data-ttu-id="95607-145">ObjectName</span><span class="sxs-lookup"><span data-stu-id="95607-145">ObjectName</span></span> |
| <span data-ttu-id="95607-146">type_instance</span><span class="sxs-lookup"><span data-stu-id="95607-146">type_instance</span></span> | <span data-ttu-id="95607-147">CounterName</span><span class="sxs-lookup"><span data-stu-id="95607-147">CounterName</span></span><br><span data-ttu-id="95607-148">If **type_instance** is *null* then CounterName=**blank**</span><span class="sxs-lookup"><span data-stu-id="95607-148">If **type_instance** is *null* then CounterName=**blank**</span></span> |
| <span data-ttu-id="95607-149">dsnames[]</span><span class="sxs-lookup"><span data-stu-id="95607-149">dsnames[]</span></span> | <span data-ttu-id="95607-150">CounterName</span><span class="sxs-lookup"><span data-stu-id="95607-150">CounterName</span></span> |
| <span data-ttu-id="95607-151">dstypes</span><span class="sxs-lookup"><span data-stu-id="95607-151">dstypes</span></span> | <span data-ttu-id="95607-152">Aucun</span><span class="sxs-lookup"><span data-stu-id="95607-152">None</span></span> |
| <span data-ttu-id="95607-153">values[]</span><span class="sxs-lookup"><span data-stu-id="95607-153">values[]</span></span> | <span data-ttu-id="95607-154">CounterValue</span><span class="sxs-lookup"><span data-stu-id="95607-154">CounterValue</span></span> |

## <a name="next-steps"></a><span data-ttu-id="95607-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="95607-155">Next steps</span></span>
* <span data-ttu-id="95607-156">Découvrez les [recherches de journal](log-analytics-log-searches.md) pour analyser les données collectées dans des sources de données et des solutions.</span><span class="sxs-lookup"><span data-stu-id="95607-156">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span> 
* <span data-ttu-id="95607-157">Utilisez les [Champs personnalisés](log-analytics-custom-fields.md) pour analyser les données des enregistrements syslog dans des champs individuels.</span><span class="sxs-lookup"><span data-stu-id="95607-157">Use [Custom Fields](log-analytics-custom-fields.md) to parse data from syslog records into individual fields.</span></span>

