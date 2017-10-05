---
title: "Collecte des données JSON personnalisées dans OMS Log Analytics | Documents Microsoft"
description: "Les sources de données JSON personnalisées peuvent être collectées dans Log Analytics à l’aide de l’agent OMS pour Linux.  Ces sources de données personnalisées peuvent être de simples scripts qui renvoient JSON en tant que cURL ou l’un des 300 plug-ins de FluentD. Cet article décrit la configuration requise pour cette collecte de données."
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
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 800ee1269556e7c2d56fbbf2b497c10509b5c78c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="collecting-custom-json-data-sources-with-the-oms-agent-for-linux-in-log-analytics"></a><span data-ttu-id="c012b-105">Collecte des sources de données JSON personnalisées à l’aide de l’agent OMS pour Linux dans Log Analytics</span><span class="sxs-lookup"><span data-stu-id="c012b-105">Collecting custom JSON data sources with the OMS Agent for Linux in Log Analytics</span></span>
<span data-ttu-id="c012b-106">Les sources de données JSON personnalisées peuvent être collectées dans Log Analytics à l’aide de l’agent OMS pour Linux.</span><span class="sxs-lookup"><span data-stu-id="c012b-106">Custom JSON data sources can be collected into Log Analytics using the OMS Agent for Linux.</span></span>  <span data-ttu-id="c012b-107">Ces sources de données personnalisées peuvent être des scripts simples qui renvoient JSON en tant que [cURL](https://curl.haxx.se/) ou l’un des [300 plug-ins de FluentD](http://www.fluentd.org/plugins/all).</span><span class="sxs-lookup"><span data-stu-id="c012b-107">These custom data sources can be simple scripts returning JSON such as [curl](https://curl.haxx.se/) or one of [FluentD's 300+ plugins](http://www.fluentd.org/plugins/all).</span></span> <span data-ttu-id="c012b-108">Cet article décrit la configuration requise pour cette collecte de données.</span><span class="sxs-lookup"><span data-stu-id="c012b-108">This article describes the configuration required for this data collection.</span></span>

> [!NOTE]
> <span data-ttu-id="c012b-109">L’agent OMS pour Linux v1.1.0-217 et versions ultérieures est requis pour les données JSON personnalisées</span><span class="sxs-lookup"><span data-stu-id="c012b-109">OMS Agent for Linux v1.1.0-217+ is required for Custom JSON Data</span></span>

## <a name="configuration"></a><span data-ttu-id="c012b-110">Configuration</span><span class="sxs-lookup"><span data-stu-id="c012b-110">Configuration</span></span>

### <a name="configure-input-plugin"></a><span data-ttu-id="c012b-111">Configuration du plug-in d’entrée</span><span class="sxs-lookup"><span data-stu-id="c012b-111">Configure input plugin</span></span>

<span data-ttu-id="c012b-112">Pour collecter des données JSON dans Log Analytics, ajoutez `oms.api.` au début d’une balise FluentD dans un plug-in d’entrée.</span><span class="sxs-lookup"><span data-stu-id="c012b-112">To collect JSON data in Log Analytics, add `oms.api.` to the start of a FluentD tag in an input plugin.</span></span>

<span data-ttu-id="c012b-113">Par exemple, ceci est un fichier de configuration distinct `exec-json.conf` dans `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.</span><span class="sxs-lookup"><span data-stu-id="c012b-113">For example, following is a separate configuration file `exec-json.conf` in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.</span></span>  <span data-ttu-id="c012b-114">Cet exemple utilise le plug-in FluentD `exec` pour exécuter une commande cURL toutes les 30 secondes.</span><span class="sxs-lookup"><span data-stu-id="c012b-114">This uses the FluentD plugin `exec` to run a curl command every 30 seconds.</span></span>  <span data-ttu-id="c012b-115">La sortie de cette commande est collectée par le plug-in de sortie JSON.</span><span class="sxs-lookup"><span data-stu-id="c012b-115">The output from this command is collected by the JSON output plugin.</span></span>

```
<source>
  type exec
  command 'curl localhost/json.output'
  format json
  tag oms.api.httpresponse
  run_interval 30s
</source>

<match oms.api.httpresponse>
  type out_oms_api
  log_level info

  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms_api_httpresponse*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
```
<span data-ttu-id="c012b-116">La propriété du fichier de configuration ajouté sous `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` devra être modifiée à l’aide de la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="c012b-116">The configuration file added under `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` will require to have its ownership changed with the following command.</span></span>

`sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/exec-json.conf`

### <a name="configure-output-plugin"></a><span data-ttu-id="c012b-117">Configuration du plug-in de sortie</span><span class="sxs-lookup"><span data-stu-id="c012b-117">Configure output plugin</span></span> 
<span data-ttu-id="c012b-118">Ajouter la configuration de plug-in de sortie suivante à la configuration principale dans `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` ou en tant que fichier de configuration distinct placé dans `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`</span><span class="sxs-lookup"><span data-stu-id="c012b-118">Add the following output plugin configuration to the main configuration in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` or as a separate configuration file placed in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`</span></span>

```
<match oms.api.**>
  type out_oms_api
  log_level info

  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms_api*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
```

### <a name="restart-oms-agent-for-linux"></a><span data-ttu-id="c012b-119">Redémarrage de l’agent OMS pour Linux</span><span class="sxs-lookup"><span data-stu-id="c012b-119">Restart OMS Agent for Linux</span></span>
<span data-ttu-id="c012b-120">Redémarrez l’agent OMS pour le service Linux à l’aide de la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="c012b-120">Restart the OMS Agent for Linux service with the following command.</span></span>

    sudo /opt/microsoft/omsagent/bin/service_control restart 

## <a name="output"></a><span data-ttu-id="c012b-121">Sortie</span><span class="sxs-lookup"><span data-stu-id="c012b-121">Output</span></span>
<span data-ttu-id="c012b-122">Les données seront collectées dans Log Analytics avec un enregistrement de type `<FLUENTD_TAG>_CL`.</span><span class="sxs-lookup"><span data-stu-id="c012b-122">The data will be collected in Log Analytics with a record type of `<FLUENTD_TAG>_CL`.</span></span>

<span data-ttu-id="c012b-123">Par exemple, la balise personnalisée `tag oms.api.tomcat` dans Log Analytics avec un enregistrement de type `tomcat_CL`.</span><span class="sxs-lookup"><span data-stu-id="c012b-123">For example, the custom tag `tag oms.api.tomcat` in Log Analytics with a record type of `tomcat_CL`.</span></span>  <span data-ttu-id="c012b-124">Vous pouvez extraire tous les enregistrements de ce type à l’aide de la recherche de journal suivante.</span><span class="sxs-lookup"><span data-stu-id="c012b-124">You could retrieve all records of this type with the following log search.</span></span>

    Type=tomcat_CL

<span data-ttu-id="c012b-125">Les sources de données JSON imbriquées sont prises en charge, mais sont indexées en fonction du champ parent.</span><span class="sxs-lookup"><span data-stu-id="c012b-125">Nested JSON data sources are supported, but are indexed based off of parent field.</span></span> <span data-ttu-id="c012b-126">Par exemple, les données JSON suivantes sont renvoyées à partir d’une recherche Log Analytics en tant que `tag_s : "[{ "a":"1", "b":"2" }]`.</span><span class="sxs-lookup"><span data-stu-id="c012b-126">For example, the following JSON data is returned from a Log Analytics search as `tag_s : "[{ "a":"1", "b":"2" }]`.</span></span>

```
{
    "tag": [{
        "a":"1",
        "b":"2"
    }]
}
```


## <a name="next-steps"></a><span data-ttu-id="c012b-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c012b-127">Next steps</span></span>
* <span data-ttu-id="c012b-128">Découvrez les [recherches de journal](log-analytics-log-searches.md) pour analyser les données collectées dans des sources de données et des solutions.</span><span class="sxs-lookup"><span data-stu-id="c012b-128">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span> 
 