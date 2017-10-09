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
# <a name="collecting-custom-json-data-sources-with-hello-oms-agent-for-linux-in-log-analytics"></a>Collecte des sources de données JSON personnalisées avec hello Agent OMS pour Linux dans le journal Analytique
Les sources de données JSON personnalisées peuvent être regroupées dans Analytique de journal à l’aide de hello Agent OMS pour Linux.  Ces sources de données personnalisées peuvent être des scripts simples qui renvoient JSON en tant que [cURL](https://curl.haxx.se/) ou l’un des [300 plug-ins de FluentD](http://www.fluentd.org/plugins/all). Cet article décrit la configuration de hello requise pour cette collection de données.

> [!NOTE]
> L’agent OMS pour Linux v1.1.0-217 et versions ultérieures est requis pour les données JSON personnalisées

## <a name="configuration"></a>Configuration

### <a name="configure-input-plugin"></a>Configuration du plug-in d’entrée

ajouter des données JSON toocollect Analytique de journal, `oms.api.` début toohello d’une balise FluentD dans un plug-in d’entrée.

Par exemple, ceci est un fichier de configuration distinct `exec-json.conf` dans `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.  Cette méthode utilise le plug-in de hello FluentD `exec` toorun une commande curl toutes les 30 secondes.  sortie Hello de cette commande est collectée par le plug-in sortie hello JSON.

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
fichier de configuration Hello ajoutée sous `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` nécessitera toohave la propriété modifiée par hello commande suivante.

`sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/exec-json.conf`

### <a name="configure-output-plugin"></a>Configuration du plug-in de sortie 
Ajouter hello suivant sortie plug-in configuration toohello configuration principales dans `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` ou comme un fichier de configuration distinct placé dans`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`

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

### <a name="restart-oms-agent-for-linux"></a>Redémarrage de l’agent OMS pour Linux
Redémarrez hello Agent OMS pour Linux service avec hello commande suivante.

    sudo /opt/microsoft/omsagent/bin/service_control restart 

## <a name="output"></a>Sortie
Hello sera collectée dans le journal Analytique avec un type d’enregistrement de `<FLUENTD_TAG>_CL`.

Par exemple, hello balise personnalisée `tag oms.api.tomcat` dans Analytique de journal avec un type d’enregistrement de `tomcat_CL`.  Impossible de récupérer tous les enregistrements de ce type avec hello suivant recherche de journal.

    Type=tomcat_CL

Les sources de données JSON imbriquées sont prises en charge, mais sont indexées en fonction du champ parent. Par exemple, hello suivant des données JSON est retourné à partir d’une recherche Analytique de journal en tant que `tag_s : "[{ "a":"1", "b":"2" }]`.

```
{
    "tag": [{
        "a":"1",
        "b":"2"
    }]
}
```


## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur [recherche de journal](log-analytics-log-searches.md) tooanalyze les données de salutation collectées à partir de sources de données et les solutions possibles. 
 