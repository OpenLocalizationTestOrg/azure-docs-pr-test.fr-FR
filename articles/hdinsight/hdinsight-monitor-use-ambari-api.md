---
title: "aaaMonitor les clusters Hadoop dans HDInsight à l’aide de hello Ambari API - Azure | Documents Microsoft"
description: "Pour créer, gérer et surveiller les clusters Hadoop, utilisez hello Apache Ambari APIs. Opérateur intuitif outils et API masquer la complexité de hello de Hadoop."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
editor: cgronlun
manager: jhubbard
ms.assetid: 052135b3-d497-4acc-92ff-71cee49356ff
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: d61a8aae5ddfcd7d44f2e4cc899e0a4da5e5fdcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-hadoop-clusters-in-hdinsight-using-hello-ambari-api"></a>Analyser les clusters Hadoop dans HDInsight à l’aide de hello Ambari API
Découvrez comment les clusters à l’aide de Ambari APIs toomonitor HDInsight.

> [!NOTE]
> informations Hello dans cet article sont principalement pour les clusters HDInsight de basés sur Windows, qui fournissent une version en lecture seule de hello Ambari REST API. Pour les clusters basés sur Linux, consultez la page [Gestion des clusters HDInsight à l’aide d’Ambari](hdinsight-hadoop-manage-ambari.md).
> 
> 

## <a name="what-is-ambari"></a>Présentation d'Ambari
[Apache Ambari][ambari-home] est destiné à l’approvisionnement, à la gestion et à la surveillance des clusters Apache Hadoop. Elle inclut une collection d’outils de l’opérateur d’intuitive et un ensemble complet d’API qui masquent la complexité hello de Hadoop, ce qui simplifie le fonctionnement de hello de clusters. Pour plus d’informations sur les API de hello, consultez [référence de l’API Ambari][ambari-api-reference]. 

HDInsight prend actuellement en charge uniquement hello Ambari fonctionnalité d’analyse. La version 1.0 de l’API Ambari est prise en charge par les clusters HDInsight versions 2.1 et 3.0. Cet article présente l’accès aux API Ambari sur les versions de clusters HDInsight 3.1 et 2.1. Hello principale différence entre hello deux est que certains composants de hello ont changé avec l’introduction de hello de nouvelles fonctionnalités (telles que le serveur de l’historique des travaux de hello). 

**Configuration requise**

Avant de commencer ce didacticiel, vous devez disposer des éléments suivants de hello :

* **Un poste de travail sur lequel est installé Azure PowerShell**.
* [cURL][curl] est facultatif. tooinstall, consultez [cURL téléchargements et mises en production][curl-download].
  
  > [!NOTE]
  > Quand utiliser hello cURL commande dans Windows, utilisez des guillemets doubles au lieu des guillemets simples pour les valeurs d’option hello.
  > 
  > 
* Un **cluster Azure HDInsight**. Pour obtenir des instructions sur l’approvisionnement des clusters, consultez la rubrique [Prise en main de HDInsight][hdinsight-get-started] ou [Approvisionnement de clusters HDInsight][hdinsight-provision]. Vous devez hello suivant toogo données didacticiel de hello :
  
  | Propriété du cluster | Nom de la variable Azure PowerShell | Valeur | Description |
  | --- | --- | --- | --- |
  |   Nom du cluster HDInsight |$clusterName | |nom de Hello de votre cluster HDInsight. |
  |   Nom d'utilisateur du cluster |$clusterUsername | |Nom d’utilisateur de cluster spécifiée lors de la création de cluster de hello. |
  |   Mot de passe du cluster |$clusterPassword | |Mot de passe utilisateur du cluster |

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]


## <a name="jump-start"></a>Lancer rapidement
Il existe plusieurs façons de clusters de HDInsight toomonitor toouse Ambari.

**Utilisation d'Azure PowerShell**

Bonjour Azure PowerShell script suivant obtient des informations de suivi de travail de MapReduce hello *dans un cluster HDInsight 3.5.*  Hello principale différence est que nous extraire ces informations à partir de service des fils hello (plutôt que MapReduce).

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName/services/YARN/components/RESOURCEMANAGER"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'yarn.queueMetrics'

Hello PowerShell script suivant obtient des informations de suivi de travail de MapReduce hello *dans un cluster HDInsight 2.1*:

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443/ambari"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName.azurehdinsight.net/services/mapreduce/components/jobtracker"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'mapred.JobTracker'

sortie de Hello est :

![Sortie du jobtracker][img-jobtracker-output]

**Utilisation de curl**

Hello exemple suivant obtient les informations de cluster à l’aide de cURL :

    curl -u <username>:<password> -k https://<ClusterName>.azurehdinsight.net:443/ambari/api/v1/clusters/<ClusterName>.azurehdinsight.net

sortie de Hello est :

    {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/",
     "Clusters":{"cluster_name":"hdi0211v2.azurehdinsight.net","version":"2.1.3.0.432823"},
     "services"[
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/services/hdfs",
        "ServiceInfo":{"cluster_name":"hdi0211v2.azurehdinsight.net","service_name":"hdfs"}},
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/services/mapreduce",
        "ServiceInfo":{"cluster_name":"hdi0211v2.azurehdinsight.net","service_name":"mapreduce"}}],
     "hosts":[
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/hosts/headnode0",
        "Hosts":{"cluster_name":"hdi0211v2.azurehdinsight.net",
                 "host_name":"headnode0"}},
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/hosts/workernode0",
        "Hosts":{"cluster_name":"hdi0211v2.azurehdinsight.net",
                 "host_name":"headnode0.{ClusterDNS}.azurehdinsight.net"}}]}

**Pour cette version 8/10/2014 hello**:

Lorsque l’utilisation hello Ambari point de terminaison, « https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname} », hello *host_name* champ Retourne le nom de domaine complet (FQDN) hello du nœud hello au lieu du nom d’hôte hello. Avant la version de 8/10/2014 hello, cet exemple retourné simplement «**headnode0**». Après la mise en production de hello 8/10/2014, vous obtenez hello nom de domaine complet «**headnode0. {} ClusterDNS} .azurehdinsight .net**«, comme illustré dans l’exemple précédent de hello. Cette modification a été requis toofacilitate les scénarios où plusieurs types de cluster (par exemple, HBase et Hadoop) peuvent être déployées dans un réseau virtuel (VNET). Cela se produit, par exemple, lors de l'utilisation de HBase en tant que plateforme principale pour Hadoop.

## <a name="ambari-monitoring-apis"></a>API de surveillance Ambari
Hello tableau suivant répertorie certaines hello courants Ambari analyses d’appels d’API. Pour plus d’informations sur les API de hello, consultez [référence de l’API Ambari][ambari-api-reference].

| Appel d'API de surveillance | URI | Description |
| --- | --- | --- |
| Obtenir des clusters |`/api/v1/clusters` | |
| Obtenir des infos sur les clusters |`/api/v1/clusters/<ClusterName>.azurehdinsight.net` |clusters, services, hôtes |
| Obtenir des services |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services` |Les services incluent : hdfs, mapreduce |
| Obtenir des infos sur les services |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>` | |
| Obtenir des composants de service |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components` |HDFS: namenode, datanodeMapReduce: jobtracker; tasktracker |
| Obtenir des infos sur les composants |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components/<ComponentName>` |ServiceComponentInfo, host-components, mesures |
| Obtenir des hôtes |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts` |headnode0, workernode0 |
| Obtenir des infos sur les hôtes |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>` | |
| Obtenir des composants d'hôte |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components` |namenode, resourcemanager |
| Obtenir des informations sur les composants d'hôte |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components/<ComponentName>` |HostRoles, composant, hôte, mesure |
| Obtenir des configurations |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations` |Types de configurations : core-site, hdfs-site, mapred-site, hive-site |
| Obtenir des infos sur la configuration |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations?type=<ConfigType>&tag=<VersionName>` |Types de configurations : core-site, hdfs-site, mapred-site, hive-site |

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris toouse Ambari API d’analyse des appels. toolearn, voir :

* [Gérer les clusters HDInsight à l’aide de hello portail Azure][hdinsight-admin-portal]
* [Gestion des clusters HDInsight à l’aide d’Azure PowerShell][hdinsight-admin-powershell]
* [Gestion de clusters HDInsight à l’aide de l’interface de ligne de commande][hdinsight-admin-cli]
* [Documentation HDInsight][hdinsight-documentation]
* [Prise en main de HDInsight][hdinsight-get-started]

[ambari-home]: http://ambari.apache.org/
[ambari-api-reference]: https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[microsoft-hadoop-SDK]: http://hadoopsdk.codeplex.com/wikipage?title=Ambari%20Monitoring%20Client

[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-documentation]: https://docs.microsoft.com/azure/hdinsight/
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md

[img-jobtracker-output]: ./media/hdinsight-monitor-use-ambari-api/hdi.ambari.monitor.jobtracker.output.png
