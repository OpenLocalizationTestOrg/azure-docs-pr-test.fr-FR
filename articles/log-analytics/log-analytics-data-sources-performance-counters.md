---
title: "aaaCollect et analyser les compteurs de performance de l’Analytique des journaux Azure | Documents Microsoft"
description: "Les compteurs de performance sont collectées par des performances tooanalyze Analytique de journal sur les agents Windows et Linux.  Cet article décrit comment collection tooconfigure des performances des compteurs des agents Windows et Linux, les détails d’elles sont stockées dans le référentiel d’OMS hello et comment tooanalyze dans le portail OMS est hello."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 20e145e4-2ace-4cd9-b252-71fb4f94099e
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/12/2017
ms.author: magoedte
ms.openlocfilehash: 30146fecf8db1d8851b89fdb970f757bbb24abf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-and-linux-performance-data-sources-in-log-analytics"></a>Sources de données de performance Windows et Linux dans Log Analytics
Compteurs de performances dans Windows et Linux donnent une idée des performances hello de composants matériels, des systèmes d’exploitation et des applications.  Analytique de journal peut collecter les compteurs de performances à intervalles fréquents pour l’analyse en temps réel (NRT) près addition tooaggregating les données de performance pour l’analyse de terme plus de temps et de la création de rapports.

![Compteurs de performances](media/log-analytics-data-sources-performance-counters/overview.png)

## <a name="configuring-performance-counters"></a>Configuration des compteurs de performances
Configurer les compteurs de performances dans le portail OMS est hello de hello [menu données de paramètres de journal Analytique](log-analytics-data-sources.md#configuring-data-sources).

Lorsque vous configurez tout d’abord Windows ou de compteurs de Performance de Linux pour un espace de travail OMS, vous pouvez soit hello option tooquickly créer plusieurs compteurs courants.  Ils sont répertoriés avec un tooeach suivant de case à cocher.  Vérifiez que les compteurs que vous souhaitez tooinitially créez sont vérifiées, puis cliquez sur **ajouter hello sélectionné les compteurs de performance**.

Pour les compteurs de performances Windows, vous pouvez choisir une instance spécifique de chaque compteur de performances. Pour les compteurs de performances Linux, instance hello de chaque compteur que vous choisissez s’applique ses compteurs enfants tooall compteur parent de hello. Hello tableau suivant montre les instances courantes hello les compteurs de performances Linux et Windows tooboth disponibles.

| Nom de l’instance | Description |
| --- | --- |
| \_Total |Nombre total de toutes les instances de hello |
| \* |Toutes les instances |
| (/&#124;/var) |Correspond aux instances nommées : / ou /var |

### <a name="windows-performance-counters"></a>Compteurs de performances Windows

![Configurer des compteurs de performances Windows](media/log-analytics-data-sources-performance-counters/configure-windows.png)

Suivez cette procédure de tooadd un nouveau toocollect de compteur de performances Windows.

1. Nom du type hello du compteur de hello dans la zone de texte hello dans un format de hello *objet (instance) \counter*.  Lorsque vous commencez à taper, la liste des compteurs correspondants s’affiche.  Vous pouvez sélectionner un compteur à partir de la liste de hello ou un type dans un des vôtres.  Vous pouvez également retourner toutes les instances d’un compteur particulier en spécifiant *objet\compteur*.  

    Lors de la collecte des compteurs de performances de SQL Server à partir d’instances nommées, toutes nommées commencent des compteurs par instance *MSSQL$* et suivi par nom hello d’instance de hello.  Par exemple, toocollect hello taux d’accès au Cache de journal de compteur pour toutes les bases de données à partir de l’objet de performance de base de données hello pour SQL nommée instance INST2, spécifier `MSSQL$INST2:Databases(*)\Log Cache Hit Ratio`.

2. Cliquez sur  **+**  ou appuyez sur **entrée** liste toohello tooadd hello.
3. Lorsque vous ajoutez un compteur, il utilise par défaut de hello de 10 secondes pour son **intervalle d’échantillonnage**.  Vous pouvez modifier cette valeur plus élevée tooa de configuration too1800 secondes (30 minutes) si vous souhaitez que les besoins en stockage hello tooreduce hello collecté des données de performances.
4. Lorsque vous avez terminé l’ajout de compteurs, cliquez sur hello **enregistrer** bouton en haut de hello de configuration de hello toosave l’écran hello.

### <a name="linux-performance-counters"></a>Compteurs de performances Linux

![Configurer des compteurs de performances Linux](media/log-analytics-data-sources-performance-counters/configure-linux.png)

Suivez cette procédure de tooadd un nouveau toocollect de compteur de performances Linux.

1. Par défaut, toutes les modifications de configuration sont automatiquement récupérées tooall agents.  Pour les agents de Linux, un fichier de configuration est envoyé toohello Fluentd de collecteurs de données.  Si vous le souhaitez toomodify ce fichier manuellement sur chaque agent Linux, puis hello désactivez case à cocher *appliquer ci-dessous les machines Linux configuration toomy* et suivez les instructions de hello ci-dessous.
2. Nom du type hello du compteur de hello dans la zone de texte hello dans un format de hello *objet (instance) \counter*.  Lorsque vous commencez à taper, la liste des compteurs correspondants s’affiche.  Vous pouvez sélectionner un compteur à partir de la liste de hello ou un type dans un des vôtres.  
3. Cliquez sur  **+**  ou appuyez sur **entrée** tooadd hello compteur toohello la liste des autres compteurs pour l’objet de hello.
4. Tous les compteurs pour une utilisation de l’objet hello même **intervalle d’échantillonnage**.  valeur par défaut Hello est de 10 secondes.  Vous modifier cette valeur plus élevée tooa de configuration too1800 secondes (30 minutes) si vous souhaitez que les besoins en stockage hello tooreduce hello collecté des données de performances.
5. Lorsque vous avez terminé l’ajout de compteurs, cliquez sur hello **enregistrer** bouton en haut de hello de configuration de hello toosave l’écran hello.

#### <a name="configure-linux-performance-counters-in-configuration-file"></a>Configuration des compteurs de performances Linux dans le fichier de configuration
Au lieu de configurer les compteurs de performances Linux à l’aide du portail OMS hello, vous pouvez hello de modification des fichiers de configuration sur l’agent Linux de hello.  Toocollect des métriques de performances sont contrôlées par la configuration de hello dans **/etc/opt/microsoft/omsagent/\<id de l’espace de travail\>/conf/omsagent.conf**.

Chaque objet ou la catégorie de toocollect des métriques de performances doit être définie dans le fichier de configuration hello en tant qu’un seul `<source>` élément. syntaxe de Hello suit le modèle hello ci-dessous.

    <source>
      type oms_omi  
      object_name "Processor"
      instance_regex ".*"
      counter_name_regex ".*"
      interval 30s
    </source>


paramètres de Hello dans cet élément sont décrits dans hello tableau suivant.

| Paramètres | Description |
|:--|:--|
| object\_name | Nom d’objet de collection de hello. |
| instance\_regex |  A *expression régulière* définissant l’instances toocollect. valeur de Hello : `.*` spécifie toutes les instances. métriques de processeur toocollect pour hello uniquement \_nombre Total d’instances, vous pouvez spécifier `_Total`. les métriques de processus toocollect pour hello uniquement les instances crond ou sshd uniquement, vous pouvez spécifier : ' (crond\|sshd)`. |
| counter\_name\_regex | A *expression régulière* définissant le toocollect compteurs (pour l’objet de hello). Spécifiez de tous les compteurs pour l’objet de hello, toocollect : `.*`. toocollect permutation compteurs d’espace pour l’objet de mémoire hello, par exemple, vous pouvez spécifier :`.+Swap.+` |
| interval | Fréquence à quels hello les compteurs de l’objet sont collectés. |


Hello tableau suivant répertorie les objets de hello et les compteurs que vous pouvez spécifier dans le fichier de configuration hello.  Des compteurs supplémentaires sont disponibles pour certaines applications tel que décrit dans [Collecte des compteurs de performances pour les applications Linux dans Log Analytics](log-analytics-data-sources-linux-applications.md).

| Nom d’objet | Nom de compteur |
|:--|:--|
| Logical Disk | % Free Inodes |
| Logical Disk | % Free Space |
| Logical Disk | % Used Inodes |
| Logical Disk | % Used Space |
| Logical Disk | Nb d’octets de lecture de disque/s  |
| Logical Disk | Nb d’opérations de lectures de disque/s  |
| Logical Disk | Disk Transfers/sec |
| Logical Disk | Nb d’octets d’écriture de disque/s |
| Logical Disk | Nb d’opération d’écriture de disque/s |
| Logical Disk | Free Megabytes |
| Logical Disk | Logical Disk Bytes/sec |
| Mémoire | % Available Memory |
| Mémoire | % Available Swap Space |
| Mémoire | % Used Memory |
| Mémoire | % Used Swap Space |
| Mémoire | Available MBytes Memory |
| Mémoire | Available MBytes Swap |
| Mémoire | Page Reads/sec |
| Mémoire | Page Writes/sec |
| Mémoire | Pages/sec |
| Mémoire | Used MBytes Swap Space |
| Mémoire | Used Memory MBytes |
| Réseau | Total Bytes Transmitted |
| Réseau | Total Bytes Received |
| Réseau | Total Bytes |
| Réseau | Total Packets Transmitted |
| Réseau | Total Packets Received |
| Réseau | Total Rx Errors |
| Réseau | Total Tx Errors |
| Réseau | Total Collisions |
| Physical Disk | Avg. Disk sec/Read |
| Physical Disk | Avg. Disk sec/Transfer |
| Physical Disk | Avg. Disk sec/Write |
| Physical Disk | Physical Disk Bytes/sec |
| Process | Pct Privileged Time |
| Process | Pct User Time |
| Process | Used Memory kBytes |
| Process | Virtual Shared Memory |
| Processeur | % DPC Time |
| Processeur | % Idle Time |
| Processeur | % Interrupt Time |
| Processeur | % IO Wait Time |
| Processeur | % Nice Time |
| Processeur | % Privileged Time |
| Processeur | % temps processeur |
| Processeur | % User Time |
| System | Free Physical Memory |
| System | Free Space in Paging Files |
| System | Free Virtual Memory |
| System | Processus |
| System | Size Stored In Paging Files |
| System | Uptime |
| System | Utilisateurs |


Voici la configuration par défaut de hello pour les mesures de performances.

    <source>
      type oms_omi
      object_name "Physical Disk"
      instance_regex ".*"
      counter_name_regex ".*"
      interval 5m
    </source>

    <source>
      type oms_omi
      object_name "Logical Disk"
      instance_regex ".*
      counter_name_regex ".*"
      interval 5m
    </source>

    <source>
      type oms_omi
      object_name "Processor"
      instance_regex ".*
      counter_name_regex ".*"
      interval 30s
    </source>

    <source>
      type oms_omi
      object_name "Memory"
      instance_regex ".*"
      counter_name_regex ".*"
      interval 30s
    </source>

## <a name="data-collection"></a>Collecte des données
Log Analytics collecte tous les compteurs de performances spécifiés selon l’intervalle d’échantillonnage spécifié sur tous les agents où le compteur est installé.  les données de salutation ne sont pas agrégées, et les données brutes hello sont disponibles dans toutes les vues de recherche de journal pour la durée de hello spécifiée par votre abonnement OMS.

## <a name="performance-record-properties"></a>Propriétés des enregistrements de performances
Les enregistrements de performances ont un type de **Perf** et ont des propriétés de hello Bonjour tableau suivant.

| Propriété | Description |
|:--- |:--- |
| Ordinateur |Ordinateur qui hello événements ont été collecté à partir de. |
| CounterName |Nom du compteur de performance hello |
| CounterPath |Chemin d’accès complet du compteur hello sous forme de hello \\ \\ \<ordinateur >\\object(instance)\\compteur. |
| CounterValue |Valeur numérique du compteur de hello. |
| InstanceName |Nom d’instance hello.  Vide si aucune instance. |
| ObjectName |Nom de l’objet de performance hello |
| SourceSystem |Type de données de l’agent hello ont été collecté à partir de. <br><br>Ops Manager – Agent Windows, connexion directe ou SCOM <br> Linux – Tous les agents Linux  <br> AzureStorage – Diagnostics Azure |
| TimeGenerated |L’échantillonnage des données hello date et heure. |

## <a name="sizing-estimates"></a>Tailles estimées
 La collecte d’un compteur toutes les 10 secondes correspond environ à 1 Mo par jour et par instance.  Vous pouvez estimer les besoins en stockage hello d’un compteur particulier avec hello formule suivante.

    1 MB x (number of counters) x (number of agents) x (number of instances)

## <a name="log-searches-with-performance-records"></a>Recherches de journal avec des enregistrements de performances
Hello tableau suivant fournit des exemples de recherches de journal qui extrait des enregistrements de performances.

| Interroger | Description |
|:--- |:--- |
| Type=Perf |Toutes les données de performances |
| Type=Perf Computer="MonOrdinateur" |Toutes les données de performances d’un ordinateur particulier |
| Type=Perf CounterName="Taille de file d’attente du disque actuelle" |Toutes les données de performances d’un compteur particulier |
| Type=Perf (ObjectName=Processor) CounterName="% du temps processeur" InstanceName=_Total &#124; measure Avg(Average) as AVGCPU by Computer |Utilisation moyenne du processeur entre tous les ordinateurs |
| Type=Perf (CounterName="% de temps processeur") &#124; measure max(Max) by Computer |Utilisation maximale du processeur entre tous les ordinateurs |
| Type=Perf ObjectName=LogicalDisk CounterName="Taille de file d’attente du disque actuelle" Computer="NomMonOrdinateur" &#124; measure Avg(Average) by InstanceName |Longueur moyenne de file d’attente du disque actuelle dans toutes les instances de hello d’un ordinateur donné |
| Type=Perf CounterName="Transferts disque/s" &#124; measure percentile95(Average) by Computer |95e centile de transferts disque/s entre tous les ordinateurs |
| Type=Perf CounterName="% du temps processeur" InstanceName="_Total"  &#124; measure avg(CounterValue) by Computer Interval 1HOUR |Moyenne horaire d’utilisation du processeur sur tous les ordinateurs |
| Type=Perf Computer="Monordinateur" CounterName=%* InstanceName=_Total &#124; measure percentile70(CounterValue) by CounterName Interval 1HOUR |70e centile horaire de chaque compteur de pourcentage pour un ordinateur particulier |
| Type=Perf CounterName="% du temps processeur" InstanceName="_Total"  (Computer="MonOrdinateur") &#124; measure min(CounterValue), avg(CounterValue), percentile75(CounterValue), max(CounterValue) by Computer Interval 1HOUR |Moyenne horaire, minimum, maximum et 75e centile d’utilisation du processeur pour un ordinateur spécifique |
| Type=Perf ObjectName="MSSQL$INST2:Databases" InstanceName=master | Toutes les données de performances à partir des performances de base de données hello de l’objet de base de données master hello de hello nommé l’instance de SQL Server INST2.  

>[!NOTE]
> Si votre espace de travail a été mis à niveau toohello [Analytique de journal nouveau langage de requête](log-analytics-log-search-upgrade.md), puis hello ci-dessus requêtes modifierait toohello suivant.

> | Interroger | Description |
|:--- |:--- |
| Perf |Toutes les données de performances |
| Perf &#124; où l’ordinateur == « MyComputer » |Toutes les données de performances d’un ordinateur particulier |
| Perf &#124; où CounterName == « longueur de la file d’attente de disque actuelle » |Toutes les données de performances d’un compteur particulier |
| Perf &#124; où ObjectName == « Processeur », CounterName == « % du temps processeur » et InstanceName == « _Total » &#124; résumer AVGCPU = avg(moyenne) par ordinateur |Utilisation moyenne du processeur entre tous les ordinateurs |
| Perf &#124; où CounterName == « % du temps processeur » &#124; résumer AggregatedValue = max(Max) par ordinateur |Utilisation maximale du processeur entre tous les ordinateurs |
| Perf &#124; où ObjectName == « LogicalDisk », CounterName == « longueur de la file d’attente de disque actuelle » et l’ordinateur == « MyComputerName » &#124; résumer AggregatedValue = avg(moyenne) par InstanceName |Longueur moyenne de file d’attente du disque actuelle dans toutes les instances de hello d’un ordinateur donné |
| Perf &#124; où CounterName == « DiskTransfers/sec » &#124; résumer AggregatedValue = centile(moyenne, 95) par ordinateur |95e centile de transferts disque/s entre tous les ordinateurs |
| Perf &#124; où CounterName == « % du temps processeur » et InstanceName == « _Total » &#124; résumer AggregatedValue = avg(CounterValue) par emplacement (TimeGenerated, 1 h), ordinateur |Moyenne horaire d’utilisation du processeur sur tous les ordinateurs |
| Perf &#124; où l’ordinateur == « MyComputer », CounterName startswith_cs « % » et InstanceName == « _Total » &#124; résumer AggregatedValue = centile(CounterValue, 70) par emplacement (TimeGenerated, 1 h), CounterName | 70e centile horaire de chaque compteur de pourcentage pour un ordinateur particulier |
| Perf &#124; où CounterName == « % du temps processeur », InstanceName == « _Total » et l’ordinateur == « MyComputer » &#124; résumer [« min(CounterValue) »] = min(CounterValue), [« avg(CounterValue) »] = avg(CounterValue), [« percentile75(CounterValue) »] = centile (CounterValue, 75), [« max(CounterValue) »] = max(CounterValue) par emplacement (TimeGenerated, 1 h), ordinateur |Moyenne horaire, minimum, maximum et 75e centile d’utilisation du processeur pour un ordinateur spécifique |
| Perf &#124; où ObjectName == « MSSQL$ INST2 : bases de données » et InstanceName == « maître » | Toutes les données de performances à partir des performances de base de données hello de l’objet de base de données master hello de hello nommé l’instance de SQL Server INST2.  

## <a name="viewing-performance-data"></a>Affichage des données de performances
Lorsque vous exécutez une recherche de journal pour les données de performances, hello **liste** s’affiche par défaut.  les données de salutation tooview dans un graphique, cliquez sur **métriques**.  Pour une vue graphique détaillée, cliquez sur hello  **+**  compteur tooa suivant.  

![Vue Mesures réduite](media/log-analytics-data-sources-performance-counters/metricscollapsed.png)

données de performances tooaggregate dans une recherche de journal, consultez [agrégation métrique de la demande et de visualisation dans OMS](http://blogs.technet.microsoft.com/msoms/2016/02/26/on-demand-metric-aggregation-and-visualization-in-oms/).


## <a name="next-steps"></a>Étapes suivantes
* [Collectez des compteurs de performances à partir d’applications Linux](log-analytics-data-sources-linux-applications.md), y compris Apache HTTP Server et MySQL.
* En savoir plus sur [recherche de journal](log-analytics-log-searches.md) tooanalyze les données de salutation collectées à partir de sources de données et les solutions possibles.  
* Exporter les données collectées trop[Power BI](log-analytics-powerbi.md) pour l’analyse et des visualisations supplémentaires.
