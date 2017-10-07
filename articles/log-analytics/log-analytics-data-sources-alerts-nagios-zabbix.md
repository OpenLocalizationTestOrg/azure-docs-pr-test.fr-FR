---
title: alertes de Nagios et Zabbix aaaCollect dans Analytique des journaux OMS | Documents Microsoft
description: "Nagios et Zabbix sont des outils de surveillance open source. Vous pouvez collecter à partir des alertes ces outils dans Analytique de journal dans l’ordre tooanalyze les ainsi que des alertes à partir d’autres sources.  Cet article décrit comment tooconfigure hello Agent OMS pour Linux toocollect des alertes à partir de ces systèmes."
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
ms.openlocfilehash: 23e2252e4fed8bc87baec063694a8472ca84220d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-alerts-from-nagios-and-zabbix-in-log-analytics-from-oms-agent-for-linux"></a>Collecte d’alertes à partir de Nagios et Zabbix dans Log Analytics à partir de l’agent OMS pour Linux 
[Nagios](https://www.nagios.org/) et [Zabbix](http://www.zabbix.com/) sont des outils de surveillance open source.  Vous peut collecter des alertes à partir de ces outils dans Analytique de journal dans l’ordre tooanalyze les avec [alertes provenant d’autres sources](log-analytics-alerts.md).  Cet article décrit comment tooconfigure hello Agent OMS pour Linux toocollect des alertes à partir de ces systèmes.
 
## <a name="configure-alert-collection"></a>Configuration de la collecte d’alertes

### <a name="configuring-nagios-alert-collection"></a>Configuration de la collecte d’alertes Nagios
Effectuer hello sur les alertes de hello Nagios server toocollect comme suit.

1. Utilisateur de subventions hello **omsagent** fichier journal de l’accès en lecture toohello Nagios (c'est-à-dire `/var/log/nagios/nagios.log`). En supposant que le fichier de hello nagios.log est détenu par groupe de hello `nagios`, vous pouvez ajouter hello utilisateur **omsagent** toohello **nagios** groupe. 

    sudo usermod -a -G nagios omsagent

2.  Modifier le fichier de configuration hello à (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`). Vérifiez que hello suivant entrées est présents et pas commentées :  

        <source>  
          type tail  
          #Update path toopoint tooyour nagios.log  
          path /var/log/nagios/nagios.log  
          format none  
          tag oms.nagios  
        </source>  
      
        <filter oms.nagios>  
          type filter_nagios_log  
        </filter>  

3. Redémarrez le démon omsagent de hello

    ```
    sudo sh /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="configuring-zabbix-alert-collection"></a>Configuration de la collecte d’alertes Zabbix
toocollect les alertes d’un serveur Zabbix, vous devez toospecify un utilisateur et mot de passe dans *clair*. Cela n’est pas idéale, mais nous recommandons que vous créez hello utilisateur et accordez des autorisations toomonitor onlu.

Effectuer hello sur les alertes de hello Nagios server toocollect comme suit.

1. Modifier le fichier de configuration hello à (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`). Vérifiez que hello suivant entrées est présents et pas commentées.  Modifier utilisateur hello nom et mot de passe de toovalues pour votre environnement Zabbix.

        <source>
         type zabbix_alerts
         run_interval 1m
         tag oms.zabbix
         zabbix_url http://localhost/zabbix/api_jsonrpc.php
         zabbix_username Admin
         zabbix_password zabbix
        </source>

2. Redémarrez le démon omsagent de hello

    sudo sh /opt/microsoft/omsagent/bin/service_control restart


## <a name="alert-records"></a>Enregistrements d’alerte
Vous pouvez récupérer les enregistrements d’alerte de Nagios et Zabbix à l’aide des [recherches dans les journaux](log-analytics-log-searches.md) dans Log Analytics.

### <a name="nagios-alert-records"></a>Enregistrements d’alerte Nagios

Pour les enregistrements d’alerte collectés par Nagios, le **type** est **Alerte** et la valeur **SourceSystem** est **Nagios**.  Elles ont des propriétés de hello Bonjour tableau suivant.

| Propriété | Description |
|:--- |:--- |
| Type |*Alert* |
| SourceSystem |*Nagios* |
| AlertName |Nom de l’alerte de hello. |
| AlertDescription | Description de l’alerte de hello. |
| AlertState | État du service de hello ou hôte.<br><br>OK<br>AVERTISSEMENT<br>ACTIF<br>INACTIF |
| HostName | Nom d’hôte hello qui a créé l’alerte de hello. |
| PriorityNumber | Niveau de priorité d’alerte de hello. |
| StateType | type Hello de l’état d’alerte de hello.<br><br>LÉGER : problème qui n’a pas été revérifié.<br>URGENT : problème qui a été revérifié un nombre spécifié de fois.  |
| TimeGenerated |Création de l’alerte hello date et heure. |


### <a name="zabbix-alert-records"></a>Enregistrements d’alerte Zabbix
Pour les enregistrements d’alerte collectés par Zabbix, le **type** est **Alerte** et la valeur **SourceSystem** est **Zabbix**.  Elles ont des propriétés de hello Bonjour tableau suivant.

| Propriété | Description |
|:--- |:--- |
| Type |*Alert* |
| SourceSystem |*Zabbix* |
| AlertName | Nom de l’alerte de hello. |
| AlertPriority | Niveau de gravité d’alerte de hello.<br><br>non classée<br>information<br>Avertissement<br>average<br>élevée<br>urgence  |
| AlertState | État d’alerte de hello.<br><br>0 - état est toodate.<br>1 - l’état est inconnu.  |
| AlertTypeNumber | Indique si l’alerte peut générer plusieurs événements de problème.<br><br>0 - état est toodate.<br>1 - l’état est inconnu.    |
| Commentaires | Commentaires supplémentaires pour l’alerte. |
| HostName | Nom d’hôte hello qui a créé l’alerte de hello. |
| PriorityNumber | Valeur qui indique la gravité d’alerte de hello.<br><br>0 - non classée<br>1 - information<br>2 - avertissement<br>3 - moyenne<br>4 - élevée<br>5 - urgence |
| TimeGenerated |Création de l’alerte hello date et heure. |
| TimeLastModified |Dernière modification de date et heure état hello d’alerte de hello. |


## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur les [alertes](log-analytics-alerts.md) dans Log Analytics.
* En savoir plus sur [recherche de journal](log-analytics-log-searches.md) tooanalyze les données de salutation collectées à partir de sources de données et les solutions possibles. 
