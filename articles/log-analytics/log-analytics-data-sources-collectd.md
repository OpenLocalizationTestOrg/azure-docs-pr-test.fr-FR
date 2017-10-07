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
# <a name="collect-data-from-collectd-on-linux-agents-in-log-analytics"></a>Collecter des données à partir de CollectD sur les agents Linux dans Log Analytics
[CollectD](https://collectd.org/) est un démon Linux open source qui collecte périodiquement des mesures de performances à partir d’applications et d’informations de niveau système. Exemples d’applications incluent Nginx, MySQL Server et hello Machine virtuelle Java (JVM). Cet article fournit des informations sur la collecte des données de performances à partir de CollectD dans Log Analytics.

Vous trouverez la liste complète des plug-ins disponibles dans le [tableau de plug-ins](https://collectd.org/wiki/index.php/Table_of_Plugins).

![Vue d’ensemble de CollectD](media/log-analytics-data-sources-collectd/overview.png)

Hello CollectD de configuration suivant est inclus dans hello Agent OMS pour Linux tooroute CollectD données toohello Agent OMS pour Linux.

    LoadPlugin write_http

    <Plugin write_http>
         <Node "oms">
         URL "127.0.0.1:26000/oms.collectd"
         Format "JSON"
         StoreRates true
         </Node>
    </Plugin>

En outre, si vous utilisez une version de collectD avant 5.5 utiliser hello configuration suivante à la place.

    LoadPlugin write_http

    <Plugin write_http>
       <URL "127.0.0.1:26000/oms.collectd">
        Format "JSON"
         StoreRates true
       </URL>
    </Plugin>

configuration de CollectD Hello utilise par défaut de hello`write_http` données métriques de performances toosend plug-in sur le port de 26000 tooOMS Agent pour Linux. 

> [!NOTE]
> Ce port peut être configuré tooa personnalisées port si nécessaire.

Hello Agent OMS pour Linux écoute également sur le port 26000 CollectD métriques, puis les convertit les métriques de schéma tooOMS. Hello Voici hello Agent OMS pour Linux configuration `collectd.conf`.

    <source>
      type http
      port 26000
      bind 127.0.0.1
    </source>

    <filter oms.collectd>
      type filter_collectd
    </filter>


## <a name="versions-supported"></a>Versions prises en charge
- Log Analytics prend actuellement en charge la version 4.8 et les versions ultérieures de CollectD.
- L’agent OMS pour Linux v1.1.0-217 ou version ultérieure est requis pour la collecte des mesures CollectD.


## <a name="configuration"></a>Configuration
Hello Voici une collection de tooconfigure étapes de base de données CollectD dans le journal Analytique.

1. Configurer CollectD toosend données toohello Agent OMS pour Linux à l’aide du plug-in de write_http hello.  
2. Configurer hello Agent OMS pour toolisten Linux pour hello CollectD données sur le port approprié de hello.
3. Redémarrez CollectD et l’agent OMS pour Linux.

### <a name="configure-collectd-tooforward-data"></a>Configurer les données de tooforward CollectD 

1. tooroute CollectD données toohello Agent OMS pour Linux, `oms.conf` besoins toobe ajouté le répertoire de configuration de tooCollectD. destination Hello de ce fichier dépend de la distribution de Linux hello de votre ordinateur.

    Si votre répertoire de configuration CollectD se trouve dans /etc/collectd.d/ :

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd.d/oms.conf

    Si votre répertoire de configuration CollectD se trouve dans /etc/collectd/collectd.conf.d/ :

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd/collectd.conf.d/oms.conf

    >[!NOTE]
    >Pour les versions CollectD avant 5.5 avoir des balises de hello toomodify dans `oms.conf` comme indiqué ci-dessus.
    >

2. Copiez le répertoire de configuration omsagent collectd.conf toohello souhaité l’espace de travail.

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/collectd.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/
        sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/collectd.conf

3. Redémarrez CollectD et l’Agent OMS pour Linux avec hello suivant les commandes.

    sudo service collectd restart  sudo /opt/microsoft/omsagent/bin/service_control restart

## <a name="collectd-metrics-toolog-analytics-schema-conversion"></a>CollectD métriques tooLog conversion du schéma Analytique
toomaintain un modèle familier entre les mesures d’infrastructure déjà collectées par l’Agent OMS pour Linux et hello nouvelles mesures collectées par CollectD hello suivant le mappage de schéma est utilisé :

| Champ Mesure CollectD | Champ Log Analytics |
|:--|:--|
| host | Ordinateur |
| plugin | Aucun |
| plugin_instance | Nom de l’instance<br>If **plugin_instance** is *null* then InstanceName="*_Total*" |
| type | ObjectName |
| type_instance | CounterName<br>If **type_instance** is *null* then CounterName=**blank** |
| dsnames[] | CounterName |
| dstypes | Aucun |
| values[] | CounterValue |

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur [recherche de journal](log-analytics-log-searches.md) tooanalyze les données de salutation collectées à partir de sources de données et les solutions possibles. 
* Utilisez [les champs personnalisés](log-analytics-custom-fields.md) tooparse des données à partir d’enregistrements syslog dans des champs individuels.

