---
title: "les données JSON personnalisées aaaCollecting dans Analytique des journaux OMS | Documents Microsoft"
description: "Les sources de données JSON personnalisées peuvent être regroupées dans Analytique de journal à l’aide de hello Agent OMS pour Linux.  Ces sources de données personnalisées peuvent être de simples scripts qui renvoient JSON en tant que cURL ou l’un des 300 plug-ins de FluentD. Cet article décrit la configuration de hello requise pour cette collection de données."
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
ms.openlocfilehash: 97d401408a8c206d4a9ef2ec9b13ba1ca6b5e92b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="collecting-custom-json-data-sources-with-hello-oms-agent-for-linux-in-log-analytics"></a><span data-ttu-id="8c0b2-105">Collecte des sources de données JSON personnalisées avec hello Agent OMS pour Linux dans le journal Analytique</span><span class="sxs-lookup"><span data-stu-id="8c0b2-105">Collecting custom JSON data sources with hello OMS Agent for Linux in Log Analytics</span></span>
<span data-ttu-id="8c0b2-106">Les sources de données JSON personnalisées peuvent être regroupées dans Analytique de journal à l’aide de hello Agent OMS pour Linux.</span><span class="sxs-lookup"><span data-stu-id="8c0b2-106">Custom JSON data sources can be collected into Log Analytics using hello OMS Agent for Linux.</span></span>  <span data-ttu-id="8c0b2-107">Ces sources de données personnalisées peuvent être des scripts simples qui renvoient JSON en tant que [cURL](https://curl.haxx.se/) ou l’un des [300 plug-ins de FluentD](http://www.fluentd.org/plugins/all).</span><span class="sxs-lookup"><span data-stu-id="8c0b2-107">These custom data sources can be simple scripts returning JSON such as [curl](https://curl.haxx.se/) or one of [FluentD's 300+ plugins](http://www.fluentd.org/plugins/all).</span></span> <span data-ttu-id="8c0b2-108">Cet article décrit la configuration de hello requise pour cette collection de données.</span><span class="sxs-lookup"><span data-stu-id="8c0b2-108">This article describes hello configuration required for this data collection.</span></span>

> [!NOTE]
> <span data-ttu-id="8c0b2-109">L’agent OMS pour Linux v1.1.0-217 et versions ultérieures est requis pour les données JSON personnalisées</span><span class="sxs-lookup"><span data-stu-id="8c0b2-109">OMS Agent for Linux v1.1.0-217+ is required for Custom JSON Data</span></span>

## <a name="configuration"></a><span data-ttu-id="8c0b2-110">Configuration</span><span class="sxs-lookup"><span data-stu-id="8c0b2-110">Configuration</span></span>

### <a name="configure-input-plugin"></a><span data-ttu-id="8c0b2-111">Configuration du plug-in d’entrée</span><span class="sxs-lookup"><span data-stu-id="8c0b2-111">Configure input plugin</span></span>

<span data-ttu-id="8c0b2-112">ajouter des données JSON toocollect Analytique de journal, `oms.api.` début toohello d’une balise FluentD dans un plug-in d’entrée.</span><span class="sxs-lookup"><span data-stu-id="8c0b2-112">toocollect JSON data in Log Analytics, add `oms.api.` toohello start of a FluentD tag in an input plugin.</span></span>

<span data-ttu-id="8c0b2-113">Par exemple, ceci est un fichier de configuration distinct `exec-json.conf` dans `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.</span><span class="sxs-lookup"><span data-stu-id="8c0b2-113">For example, following is a separate configuration file `exec-json.conf` in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.</span></span>  <span data-ttu-id="8c0b2-114">Cette méthode utilise le plug-in de hello FluentD `exec` toorun une commande curl toutes les 30 secondes.</span><span class="sxs-lookup"><span data-stu-id="8c0b2-114">This uses hello FluentD plugin `exec` toorun a curl command every 30 seconds.</span></span>  <span data-ttu-id="8c0b2-115">sortie Hello de cette commande est collectée par le plug-in sortie hello JSON.</span><span class="sxs-lookup"><span data-stu-id="8c0b2-115">hello output from this command is collected by hello JSON output plugin.</span></span>

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
<span data-ttu-id="8c0b2-116">fichier de configuration Hello ajoutée sous `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` nécessitera toohave la propriété modifiée par hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="8c0b2-116">hello configuration file added under `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` will require toohave its ownership changed with hello following command.</span></span>

`sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/exec-json.conf`

### <a name="configure-output-plugin"></a><span data-ttu-id="8c0b2-117">Configuration du plug-in de sortie</span><span class="sxs-lookup"><span data-stu-id="8c0b2-117">Configure output plugin</span></span> 
<span data-ttu-id="8c0b2-118">Ajouter hello suivant sortie plug-in configuration toohello configuration principales dans `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` ou comme un fichier de configuration distinct placé dans`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`</span><span class="sxs-lookup"><span data-stu-id="8c0b2-118">Add hello following output plugin configuration toohello main configuration in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` or as a separate configuration file placed in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`</span></span>

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

### <a name="restart-oms-agent-for-linux"></a><span data-ttu-id="8c0b2-119">Redémarrage de l’agent OMS pour Linux</span><span class="sxs-lookup"><span data-stu-id="8c0b2-119">Restart OMS Agent for Linux</span></span>
<span data-ttu-id="8c0b2-120">Redémarrez hello Agent OMS pour Linux service avec hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="8c0b2-120">Restart hello OMS Agent for Linux service with hello following command.</span></span>

    sudo /opt/microsoft/omsagent/bin/service_control restart 

## <a name="output"></a><span data-ttu-id="8c0b2-121">Sortie</span><span class="sxs-lookup"><span data-stu-id="8c0b2-121">Output</span></span>
<span data-ttu-id="8c0b2-122">Hello sera collectée dans le journal Analytique avec un type d’enregistrement de `<FLUENTD_TAG>_CL`.</span><span class="sxs-lookup"><span data-stu-id="8c0b2-122">hello data will be collected in Log Analytics with a record type of `<FLUENTD_TAG>_CL`.</span></span>

<span data-ttu-id="8c0b2-123">Par exemple, hello balise personnalisée `tag oms.api.tomcat` dans Analytique de journal avec un type d’enregistrement de `tomcat_CL`.</span><span class="sxs-lookup"><span data-stu-id="8c0b2-123">For example, hello custom tag `tag oms.api.tomcat` in Log Analytics with a record type of `tomcat_CL`.</span></span>  <span data-ttu-id="8c0b2-124">Impossible de récupérer tous les enregistrements de ce type avec hello suivant recherche de journal.</span><span class="sxs-lookup"><span data-stu-id="8c0b2-124">You could retrieve all records of this type with hello following log search.</span></span>

    Type=tomcat_CL

<span data-ttu-id="8c0b2-125">Les sources de données JSON imbriquées sont prises en charge, mais sont indexées en fonction du champ parent.</span><span class="sxs-lookup"><span data-stu-id="8c0b2-125">Nested JSON data sources are supported, but are indexed based off of parent field.</span></span> <span data-ttu-id="8c0b2-126">Par exemple, hello suivant des données JSON est retourné à partir d’une recherche Analytique de journal en tant que `tag_s : "[{ "a":"1", "b":"2" }]`.</span><span class="sxs-lookup"><span data-stu-id="8c0b2-126">For example, hello following JSON data is returned from a Log Analytics search as `tag_s : "[{ "a":"1", "b":"2" }]`.</span></span>

```
{
    "tag": [{
        "a":"1",
        "b":"2"
    }]
}
```


## <a name="next-steps"></a><span data-ttu-id="8c0b2-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8c0b2-127">Next steps</span></span>
* <span data-ttu-id="8c0b2-128">En savoir plus sur [recherche de journal](log-analytics-log-searches.md) tooanalyze les données de salutation collectées à partir de sources de données et les solutions possibles.</span><span class="sxs-lookup"><span data-stu-id="8c0b2-128">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span> 
 