---
title: "Surveiller les clusters Hadoop dans HDInsight à l’aide de l’API Ambari - Azure | Microsoft Docs"
description: "Utilisez les API Apache Ambari pour la création, la gestion et la surveillance des clusters Hadoop. Les outils intuitifs pour opérateurs et les API masquent la complexité de Hadoop."
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
ms.openlocfilehash: b6fc2098027690eb76b69b1427f0e9541b8a7a69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-hadoop-clusters-in-hdinsight-using-the-ambari-api"></a>Surveillance des clusters Hadoop dans HDInsight à l'aide des API Ambari
Découvrez comment surveiller les clusters HDInsight à l’aide des API Ambari.

> [!NOTE]
> Les informations contenues dans cet article sont adaptées principalement aux clusters HDInsight basés sur Windows, qui fournissent une version en lecture seule de l’API REST Ambari. Pour les clusters basés sur Linux, consultez la page [Gestion des clusters HDInsight à l’aide d’Ambari](hdinsight-hadoop-manage-ambari.md).
> 
> 

## <a name="what-is-ambari"></a>Présentation d'Ambari
[Apache Ambari][ambari-home] est destiné à l’approvisionnement, à la gestion et à la surveillance des clusters Apache Hadoop. Il comprend une collection intuitive d'outils d'opérateurs et un solide jeu d'API qui masque la complexité de Hadoop, en simplifiant le fonctionnement des clusters. Pour plus d’informations sur les API, consultez la page [Référence des API Ambari][ambari-api-reference]. 

HDInsight prend actuellement en charge la fonctionnalité de surveillance Ambari uniquement. La version 1.0 de l’API Ambari est prise en charge par les clusters HDInsight versions 2.1 et 3.0. Cet article présente l’accès aux API Ambari sur les versions de clusters HDInsight 3.1 et 2.1. La différence principale entre les deux est que certains des composants ont changé avec l'introduction des nouvelles fonctionnalités (telles que le serveur d'historique des tâches). 

**Configuration requise**

Avant de commencer ce didacticiel, vous devez disposer des éléments suivants :

* **Un poste de travail sur lequel est installé Azure PowerShell**.
* [cURL][curl] est facultatif. Pour l’installer, consultez [Versions et téléchargements de cURL][curl-download].
  
  > [!NOTE]
  > Lorsque vous utilisez la commande cURL sous Windows, remplacez les guillemets simples par des guillemets doubles pour exprimer la valeur des options.
  > 
  > 
* Un **cluster Azure HDInsight**. Pour obtenir des instructions sur l’approvisionnement des clusters, consultez la rubrique [Prise en main de HDInsight][hdinsight-get-started] ou [Approvisionnement de clusters HDInsight][hdinsight-provision]. Vous aurez besoin des données suivantes pour suivre ce didacticiel :
  
  | Propriété du cluster | Nom de la variable Azure PowerShell | Valeur | Description |
  | --- | --- | --- | --- |
  |   Nom du cluster HDInsight |$clusterName | |Nom de votre cluster HDInsight |
  |   Nom d'utilisateur du cluster |$clusterUsername | |Nom d’utilisateur du cluster spécifié lors de la création du cluster. |
  |   Mot de passe du cluster |$clusterPassword | |Mot de passe utilisateur du cluster |

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]


## <a name="jump-start"></a>Lancer rapidement
Il existe plusieurs façons d'utiliser Ambari pour surveiller les clusters HDInsight.

**Utilisation d'Azure PowerShell**

Le script Azure PowerShell suivant permet d’obtenir les informations de suivi des tâches MapReduce *dans un cluster HDInsight 3.5.*  La différence principale réside dans le fait que nous allons extraire ces détails à partir du service YARN (plutôt que Map Reduce).

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName/services/YARN/components/RESOURCEMANAGER"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'yarn.queueMetrics'

Le script PowerShell suivant permet d’obtenir les informations de suivi des tâches MapReduce *dans un cluster HDInsight 2.1* :

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443/ambari"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName.azurehdinsight.net/services/mapreduce/components/jobtracker"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'mapred.JobTracker'

La sortie est la suivante :

![Sortie du jobtracker][img-jobtracker-output]

**Utilisation de curl**

L’exemple suivant permet d’obtenir des informations de cluster à l’aide de cURL :

    curl -u <username>:<password> -k https://<ClusterName>.azurehdinsight.net:443/ambari/api/v1/clusters/<ClusterName>.azurehdinsight.net

La sortie est la suivante :

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

**Pour la version du 8/10/2014**:

Lors de l’utilisation du point de terminaison Ambari, « https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname} », le champ *host_name* renvoie le nom de domaine complet du nœud au lieu du nom d’hôte. Avant la version du 8/10/2014, cet exemple renvoyait simplement «**headnode0**». Après la version du 8/10/2014, vous obtenez le nom de domaine complet «**headnode0.{ClusterDNS}.azurehdinsight.net**», comme illustré dans l’exemple précédent. Cette modification était nécessaire pour permettre les scénarios dans lesquels plusieurs types de cluster tels que HBase et Hadoop sont déployés dans un réseau virtuel (VNET). Cela se produit, par exemple, lors de l'utilisation de HBase en tant que plateforme principale pour Hadoop.

## <a name="ambari-monitoring-apis"></a>API de surveillance Ambari
Le tableau suivant répertorie certains des appels d'API de surveillance Ambari les plus connus. Pour plus d’informations sur l’API, consultez la page [Référence des API Ambari][ambari-api-reference].

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
Vous avez appris à utiliser les appels d'API de surveillance Ambari. Pour plus d'informations, consultez les rubriques suivantes :

* [Gestion des clusters HDInsight à l’aide du portail Azure][hdinsight-admin-portal]
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
