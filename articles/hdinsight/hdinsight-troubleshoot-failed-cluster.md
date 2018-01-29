---
title: "Résoudre les problèmes d’un cluster HDInsight défaillant ou lent - Azure HDInsight | Microsoft Docs"
description: "Diagnostiquer et résoudre les problèmes d’un cluster HDInsight défaillant ou lent."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: ashishthaps
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2018
ms.author: ashishth
ms.openlocfilehash: 59382931d4b5478888238760b268af7f962a10b5
ms.sourcegitcommit: 48fce90a4ec357d2fb89183141610789003993d2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/12/2018
---
# <a name="troubleshoot-a-slow-or-failing-hdinsight-cluster"></a>Résoudre les problèmes d’un cluster HDInsight défaillant ou lent

En cas de ralentissement d’un cluster HDInsight ou d’échec du cluster avec un code d’erreur, vous disposez de plusieurs options de dépannage. Si l’exécution de vos travaux prend plus de temps que prévu ou si vous constatez généralement des temps de réponse assez longs, il est possible que ces problèmes soient imputables à des défaillances en amont à de votre cluster (par exemple, les services sur lesquels s’exécute le cluster). Mais une mise à l’échelle insuffisante est la cause la plus courante de ces ralentissements. Lorsque vous créez un nouveau cluster HDInsight, sélectionnez les [tailles de machine virtuelle](hdinsight-component-versioning.md#default-node-configuration-and-virtual-machine-sizes-for-clusters) appropriées.

Pour diagnostiquer un cluster lent ou défaillant, essayez de recueillir des informations sur tous les aspects de l’environnement, notamment les services Azure associés, la configuration du cluster ou encore les informations relatives à l’exécution du travail. Pour diagnostiquer les problèmes, le mieux est d’essayer de reproduire l’état d’erreur sur un autre cluster.

* Étape 1 : recueillir des données sur le problème
* Étape 2 : valider l’environnement du cluster HDInsight 
* Étape 3 : contrôler l’état d’intégrité de votre cluster
* Étape 4 : examiner la pile et les versions de l’environnement
* Étape 5 : examiner les fichiers journaux du cluster
* Étape 6 : vérifier les paramètres de configuration
* Étape 7 : reproduire la défaillance sur un autre cluster 

## <a name="step-1-gather-data-about-the-issue"></a>Étape 1 : recueillir des données sur le problème

HDInsight fournit de nombreux outils que vous pouvez utiliser pour identifier et résoudre les problèmes liés aux clusters. Les étapes suivantes vous guident tout au long de l’utilisation de ces outils et vous fournissent des suggestions pour localiser le problème.

### <a name="identify-the-problem"></a>Identifier le problème

Pour vous aider à identifier le problème, posez-vous les questions suivantes :

* Que devait-il normalement se passer ? Que s’est-il passé en réalité ?
* Quelle a été la durée d’exécution du processus ? Pendant combien de temps aurait-il dû s’exécuter ?
* Mes tâches se sont-elles toujours exécutées lentement sur ce cluster ? Leur exécution était-elle plus rapide sur un autre cluster ?
* À quel moment ce problème est-il initialement apparu ? À quelle fréquence s’est-il ensuite produit ?
* Ai-je modifié quelque chose dans la configuration de mon cluster ?

### <a name="cluster-details"></a>Détails du cluster

Voici quelques informations importantes à propos du cluster :

* Nom du cluster.
* Région du cluster : vérifiez les [pannes dans la région](https://azure.microsoft.com/status/).
* Type et version du cluster HDInsight.
* Type et nombre d’instances HDInsight spécifiés pour les nœuds de tête et de travail.

Le portail Azure peut fournir les informations suivantes :

![Informations relatives au portail Azure HDInsight](./media/hdinsight-troubleshoot-failed-cluster/portal.png)

Vous pouvez aussi utiliser l’interface Azure CLI :

```
    azure hdinsight cluster list
    azure hdinsight cluster show <ClusterName>
```

Une autre option consiste à utiliser PowerShell. Pour en savoir plus, consultez [Gestion des clusters Hadoop dans HDInsight au moyen d’Azure PowerShell](hdinsight-administer-use-powershell.md).

## <a name="step-2-validate-the-hdinsight-cluster-environment"></a>Étape 2 : valider l’environnement du cluster HDInsight

Chaque cluster HDInsight s’appuie sur divers services Azure ainsi que sur des logiciels open source tels que Apache HBase et Apache Spark. Les clusters HDInsight peuvent également appeler d’autres services Azure, comme les réseaux virtuels Azure.  Une défaillance de cluster peut être liée soit à l’un des services en cours d’exécution sur votre cluster, soit à un service externe.  Un changement de configuration d’un service de cluster peut également provoquer une défaillance du cluster.

### <a name="service-details"></a>Détails du service

* Vérifiez les versions de bibliothèques open source
* Recherchez les [interruptions de service Azure](https://azure.microsoft.com/status/) 
* Recherchez les limites d’utilisation des services Azure 
* Vérifiez la configuration de sous-réseau du réseau virtuel Azure 

### <a name="view-cluster-configuration-settings-with-the-ambari-ui"></a>Vérifier les paramètres de configuration du cluster avec l’interface utilisateur Ambari

Apache Ambari assure la gestion et la surveillance d’un cluster HDInsight grâce à une interface utilisateur web et à une API REST. Ambari est inclus sur les clusters HDInsight sous Linux. Sélectionnez le volet **Tableau de bord du cluster** sur la page HDInsight du portail Azure.  Sélectionnez le volet **Tableau de bord du cluster HDInsight** pour ouvrir l’interface utilisateur Ambari, puis entrez les informations d’identification utilisée pour vous connecter au cluster.  

![Interface utilisateur Ambari](./media/hdinsight-troubleshoot-failed-cluster/ambari-ui.png)

Pour ouvrir une liste de vues du service, sélectionnez **Vues Ambari** sur la page du portail Azure.  Cette liste varie selon les bibliothèques installées. Elle peut contenir par exemple YARN Queue Manager, Hive View et Tez View.  Sélectionnez le lien d’un service pour afficher des informations sur la configuration et le service.

#### <a name="check-for-azure-service-outages"></a>Rechercher les interruptions de service Azure

HDInsight s’appuie sur plusieurs services Azure. Il exécute des serveurs virtuels dans Azure HDInsight, stocke des données et des scripts sur le stockage Blob Azure ou sur Azure DataLake Store, et indexe des fichiers journaux dans le stockage Azure Table. Bien que rares, les perturbation de ces services peuvent entraîner des problèmes dans HDInsight. Si votre cluster subit des ralentissements ou défaillances inattendus, consultez le [Tableau de bord d’état Azure](https://azure.microsoft.com/status/). L’état de chaque service est indiqué par région. Vérifiez la région de votre cluster, mais également les régions de tous les services associés.

#### <a name="check-azure-service-usage-limits"></a>Rechercher les limites d’utilisation des services Azure

Si vous démarrez un cluster volumineux ou si vous avez lancé simultanément un grand nombre de clusters, un cluster peut échouer si vous avez dépassé une limite de service Azure. Les limites de service varient selon votre abonnement Azure. Pour plus d’informations, consultez [Abonnement Azure et limites, quotas et contraintes de service](https://docs.microsoft.com/azure/azure-subscription-service-limits).
Vous pouvez demander à Microsoft d’augmenter le nombre de ressources HDInsight disponibles (par exemple, les cœurs de machines virtuelles et les instances de machines virtuelles) en soumettant une [demande d’augmentation des quotas de processeurs virtuels pour Resource Manager](https://docs.microsoft.com/azure/azure-supportability/resource-manager-core-quotas-request).

#### <a name="check-the-release-version"></a>Vérifier la version

Comparez la version de votre cluster à la dernière version de HDInsight. Chaque version de HDInsight inclut des améliorations, par exemple de nouvelles applications ou fonctionnalités, des correctifs et des corrections de bogues. Il est possible que le problème que rencontre votre cluster a été résolu dans la dernière version. Si possible, exécutez à nouveau votre cluster en utilisant la dernière version de HDInsight et des bibliothèques associées tels que Apache HBase, Apache Spark ou autre.

#### <a name="restart-your-cluster-services"></a>Redémarrer vos services de cluster

Si votre cluster subit des ralentissements, pensez à redémarrer vos services via l’interface utilisateur Ambari ou l’interface Azure CLI. Le cluster peut rencontrer des erreurs transitoires, auquel cas un redémarrage offre le moyen le plus rapide pour stabiliser votre environnement et éventuellement en améliorer les performances.

## <a name="step-3-view-your-clusters-health"></a>Étape 3 : contrôler l’état d’intégrité de votre cluster

Les clusters HDInsight sont composées de différents types de nœuds en cours d’exécution sur des instances de machine virtuelle. Chaque nœud peut être analysé pour identifier des problèmes de ressources insuffisantes, des problèmes de connectivité réseau et d’autres problèmes susceptibles de ralentir le cluster. Chaque cluster contient deux nœuds principaux et la plupart des types de cluster comportent à la fois des nœuds de travail et des nœuds de périphérie. 

<!-- For a description of the various nodes each cluster type uses, see [HDInsight Architecture](hdinsight-architecture.md). -->

Les sections suivantes vous expliquent comment vérifier l’intégrité de chaque nœud et du cluster global.

### <a name="get-a-snapshot-of-the-cluster-health-using-the-ambari-ui-dashboard"></a>Obtenir un instantané de l’intégrité du cluster à l’aide du tableau de bord de l’interface utilisateur Ambari

Le [tableau de bord de l’interface utilisateur Ambari](#view-cluster-configuration-settings-with-the-ambari-ui) (`https://<clustername>.azurehdinsight.net`) fournit une vue d’ensemble de l’intégrité du cluster (temps de fonctionnement, utilisation de la mémoire, du réseau et du processeur, utilisation du disque HDFS, etc.). Utilisez la section Hôtes d’Ambari pour afficher les ressources au niveau d’un hôte. Vous pouvez également arrêter et redémarrer les services.

### <a name="check-your-webhcat-service"></a>Vérifier votre service WebHCat

Il arrive souvent que les travaux Hive, Pig ou Sqoop échouent en raison d’une défaillance du service [WebHCat](hdinsight-hadoop-templeton-webhcat-debug-errors.md) (ou *Templeton*). WebHCat est une interface REST qui permet d’exécuter un travail à distance, tel que Hive, Pig, Scoop et MapReduce. WebHCat convertit les demandes de soumission de travail en applications YARN et retourne un état dérivé de l’état de l’application YARN.  Les sections suivantes décrivent les codes d’état HTTP WebHCat courants.

#### <a name="badgateway-502-status-code"></a>BadGateway (code d’état 502)

Ce message générique est généré par les nœuds de la passerelle et représente le code d’état d’échec le plus courant. Il peut être imputé à un arrêt du service WebHCat sur le nœud principal actif. Pour vérifier cette possibilité, utilisez la commande CURL suivante :

```bash
$ curl -u admin:{HTTP PASSWD} https://{CLUSTERNAME}.azurehdinsight.net/templeton/v1/status?user.name=admin
```

Ambari affiche une alerte indiquant les hôtes sur lesquels le service WebHCat est arrêté. Vous pouvez tenter de rétablir le service WebHCat en redémarrant le service sur son hôte.

![Redémarrer le serveur WebHCat](./media/hdinsight-troubleshoot-failed-cluster/restart-webhcat.png)

Si un serveur WebHCat ne répond toujours pas, consultez le journal des opérations pour vérifier les messages d’échec. Pour plus d’informations, vérifiez les fichiers `stderr` et `stdout` référencés sur le nœud.

#### <a name="webhcat-times-out"></a>Délai d’expiration de WebHCat

Une passerelle HDInsight renvoie `502 BadGateway` lorsque les réponses dépassent un délai de deux minutes. WebHCat interroge les services YARN pour connaître l’état des travaux. Si YARN met plus de deux minutes à répondre, cette demande peut expirer.

Dans ce cas, consultez les journaux suivants dans le répertoire `/var/log/webhcat` :

* **webhcat.log** est le journal log4j sur lequel le serveur écrit des fichiers journaux
* **webhcat-console.log** est le stdout du serveur au démarrage
* **webhcat-console-error.log** est le stderr du processus serveur

> [!NOTE]
> Chaque `webhcat.log` est renouvelé tous les jours, ce qui génère des fichiers nommés `webhcat.log.YYYY-MM-DD`. Sélectionnez le fichier correspondant à l’intervalle de temps que vous examinez.

Les sections suivantes décrivent les causes possibles de l’expiration des délais d’attente WebHCat.

##### <a name="webhcat-level-timeout"></a>Délai d’expiration au niveau de WebHCat

Lorsque WebHCat est chargé et que plus de 10 sockets sont ouverts, il met davantage de temps à établir de nouvelles connexions de socket, ce qui peut entraîner un délai d’attente. Pour répertorier les connexions réseau vers et depuis WebHCat, utilisez `netstat` sur le nœud principal actif actuel :

```bash
$ netstat | grep 30111
```

30111 est le port qu’écoute WebHCat. Le nombre de sockets ouverts doit être inférieur à 10.

Si aucun socket n’est ouvert, la commande précédente ne produit aucun résultat. Pour vérifier si Templeton est activé et à l’écoute sur le port 30111, utilisez :

```bash
$ netstat -l | grep 30111
```

##### <a name="yarn-level-timeout"></a>Délai d’expiration au niveau de YARN

Templeton appelle YARN pour exécuter des travaux, et la communication entre Templeton et YARN peut entraîner un délai d’attente.

Au niveau de YARN, il existe deux types de délais d’expiration :

1. L’envoi d’un travail YARN peut durer suffisamment longtemps pour provoquer l’expiration du délai d’attente.

    Si vous ouvrez le fichier journal `/var/log/webhcat/webhcat.log` et que vous recherchez un « travail en file d’attente », vous pouvez voir plusieurs entrées associées à une durée d’exécution trop longue (> 2 000 ms), où les entrées indiquent une augmentation des temps d’attente.

    La durée des travaux en file d’attente continue d’augmenter car la vitesse à laquelle les nouveaux travaux sont envoyés est supérieure à la fréquence d’exécution des anciens travaux. Une fois que la mémoire de YARN est utilisée à 100 %, la *file d’attente joblauncher* ne peut plus emprunter de capacité à la *file d’attente par défaut*. Par conséquent, la file d’attente joblauncher ne peut plus accepter de nouveaux travaux. Ce comportement peut provoquer un allongement des temps d’attente et provoquer une erreur de délai d’expiration, qui est généralement suivie de nombreuses autres erreurs du même type.

    L’illustration suivante montre la file d’attente joblauncher à un taux d’utilisation de 714,4 %. Ce taux est acceptable tant qu’il reste de la capacité disponible à emprunter à la file d’attente par défaut. Toutefois, lorsque le cluster est entièrement utilisé et que la mémoire YARN a atteint 100 % de sa capacité, les nouveaux travaux doivent attendre, ce qui finit par provoquer une expiration des délais d’attente.

    ![File d’attente Joblauncher](./media/hdinsight-troubleshoot-failed-cluster/joblauncher-queue.png)

    Il existe deux façons de résoudre ce problème : vous pouvez soit réduire la vitesse d’envoi de nouveaux travaux, soit relever la vitesse de la consommation des anciens travaux en augmentant la capacité du cluster.

2. Le traitement YARN peut prendre beaucoup de temps, ce qui peut entraîner des délais d’attente.

    * Répertorier tous les travaux : ce type d’appel prend beaucoup de temps. Cet appel énumère les applications à partir de YARN ResourceManager et, pour chaque application exécutée, récupère l’état auprès de YARN JobHistoryServer. Cet appel peut expirer si le nombre de travaux atteint une valeur importante.

    * Répertorier les travaux de plus de sept jours : HDInsight YARN JobHistoryServer est configuré pour conserver les informations relatives aux travaux exécutés pendant une durée de sept jours (valeur `mapreduce.jobhistory.max-age-ms`). Une tentative d’énumération des travaux supprimés conduit à l’expiration du délai d’attente.

Pour diagnostiquer ces problèmes :

    1. Déterminez l’intervalle de temps UTC pour résoudre les problèmes
    2. Sélectionnez le ou les fichier(s) `webhcat.log` appropriés
    3. Recherchez des messages d’avertissement et d’erreur pendant cette période

#### <a name="other-webhcat-failures"></a>Autres défaillances de WebHCat

1. Code d’état HTTP 500

    Lorsque WebHCat renvoie un code d’état 500, le message d’erreur contient généralement des détails relatifs à l’échec. Sinon, examinez `webhcat.log` pour rechercher d’éventuels messages d’avertissement et d’erreur.

2. Échecs des travaux

    Il peut arriver que les interactions avec WebHCat réussissent, mais que les travaux échouent.

    Templeton récupère la sortie de la console de travail en tant que `stderr` dans `statusdir`, ce qui est souvent utile pour le dépannage. `stderr` contient l’identifiant d’application YARN de la requête réelle.

## <a name="step-4-review-the-environment-stack-and-versions"></a>Étape 4 : examiner la pile et les versions de l’environnement

La page **Pile et version** de l’interface utilisateur Ambari fournit des informations sur la configuration des services du cluster et sur l’historique de version des services.  Des versions incorrectes de la bibliothèque de services Hadoop peuvent être une cause de défaillance du cluster.  Dans l’interface utilisateur Ambari, sélectionnez le menu **Admin**, puis **Piles et versions**.  Sélectionnez l’onglet **Versions** sur la page pour afficher des informations sur la version du service :

![Pile et versions](./media/hdinsight-troubleshoot-failed-cluster/stack-versions.png)

## <a name="step-5-examine-the-log-files"></a>Étape 5 : examiner les fichiers journaux

De nombreux types de fichiers journaux sont générés à partir des nombreux services et composants qui composent un cluster HDInsight. Les [fichiers journaux WebHCat](#check-your-webhcat-service) ont été décrits précédemment. Il existe d’autres fichiers journaux utiles que vous pouvez examiner pour réduire les problèmes liés à votre cluster, comme décrit ci-dessous.

![Exemple de fichier journal HDInsight](./media/hdinsight-troubleshoot-failed-cluster/logs.png)

* Les clusters HDInsight sont constitués de plusieurs nœuds, dont la plupart sont chargés d’exécuter les travaux soumis. Les travaux s’exécutent simultanément, mais les fichiers journaux peuvent uniquement afficher des résultats de façon linéaire. HDInsight exécute de nouvelles tâches, en mettant d’abord fin à celles qui ne parviennent pas à s’exécuter. Tous ces activités sont consignées dans les fichiers `stderr` et `syslog`.

* Les fichiers journaux d’actions de script indiquent les erreurs ou les changements de configuration inattendus pendant le processus de création de votre cluster.

* Les journaux d’étape Hadoop identifient les travaux Hadoop lancés dans le cadre d’une étape contenant des erreurs.

### <a name="check-the-script-action-logs"></a>Vérifier les journaux d’actions de script

Les [actions de script](hdinsight-hadoop-customize-cluster-linux.md) HDInsight exécutent des scripts sur le cluster manuellement ou à l’intervalle spécifié. Par exemple, des actions de script peuvent être utilisées pour installer des logiciels supplémentaires sur le cluster ou pour modifier les paramètres de configuration à partir des valeurs par défaut. La vérification des journaux d’actions de script peut donnent une idée des erreurs qui se sont produites pendant l’installation et la configuration du cluster.  Vous pouvez consulter l’état d’une action de script en sélectionnant le bouton **ops** dans l’interface utilisateur Ambari, ou en accédant aux journaux à partir du compte de stockage par défaut.

Les journaux d’actions de script se trouvent dans le répertoire `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.

### <a name="view-hdinsight-logs-using-ambari-quick-links"></a>Afficher les journaux HDInsight à l’aide des liens rapides d’Ambari

L’interface utilisateur HDInsight Ambari comprend un certain nombre de sections **Liens rapides**.  Pour accéder aux liens vers les journaux d’un service donné de votre cluster HDInsight, ouvrez l’interface utilisateur Ambari de votre cluster, puis sélectionnez le lien du service dans la liste située à gauche. Sélectionnez la liste déroulante **Liens rapides**, puis le nœud HDInsight qui vous intéresse, et sélectionnez le lien vers le journal correspondant.

Par exemple, pour les journaux HDFS :

![Liens rapides Ambari vers des fichiers journaux](./media/hdinsight-troubleshoot-failed-cluster/quick-links.png)

### <a name="view-hadoop-generated-log-files"></a>Afficher les fichiers journaux générés par Hadoop

Un cluster HDInsight génère des fichiers journaux qui sont écrits dans les tables Azure et dans le stockage Blob Azure. YARN crée ses propres journaux d’exécution. Pour plus d’informations, consultez la rubrique [Gérer les journaux pour un cluster HDInsight](hdinsight-log-management.md#access-the-hadoop-log-files).

### <a name="review-heap-dumps"></a>Examiner les dumps de tas

Les dumps de tas contiennent un instantané de la mémoire de l’application, y compris les valeurs des variables à ce moment précis, ce qui peut être utile pour diagnostiquer des problèmes qui se produisent lors de l’exécution. Pour plus d’informations, consultez l’article [Activer les dumps de tas pour les services Hadoop sur HDInsight sur Linux](hdinsight-hadoop-collect-debug-heap-dump-linux.md).

## <a name="step-6-check-configuration-settings"></a>Étape 6 : vérifier les paramètres de configuration

Les clusters HDInsight sont préconfigurés avec les paramètres par défaut pour les services connexes, tels que Hadoop, Hive, HBase, etc. Selon le type de cluster, sa configuration matérielle, son nombre de nœuds, les types de travaux que vous exécutez et les données sur lesquelles vous travaillez (ainsi que la manière dont ces données sont traitées), vous devrez peut-être optimiser votre configuration.

<!-- For detailed instructions on optimizing performance configurations for most scenarios, see [Changing configurations with Ambari](hdinsight-changing-configs-via-ambari.md). When using Spark, see [Optimizing Spark jobs for performance](spark/apache-spark-perf.md).  -->

## <a name="step-7-reproduce-the-failure-on-a-different-cluster"></a>Étape 7 : reproduire la défaillance sur un autre cluster

Pour aider à diagnostiquer l’origine d’une erreur de cluster, démarrez un nouveau cluster avec la même configuration, puis soumettez de nouveau une à une les étapes du travail qui a échoué. Vérifiez les résultats de chaque étape avant de traiter l’étape suivante. Cette méthode vous donne la possibilité de corriger et de réexécuter une seule étape ayant échoué. Cette méthode présente également l’avantage de charger vos données d’entrée une seule fois.

1. Créez un nouveau cluster de test avec la même configuration que le cluster défaillant.
2. Envoyez la première étape du travail vers le cluster de test.
3. Une fois le traitement de l’étape terminé, recherchez les erreurs dans les fichiers journaux d’étapes. Connectez-vous au nœud principal du cluster de test et consultez les fichiers journaux qui s’y trouvent. Les fichiers journaux d’étapes apparaissent uniquement si l’étape s’exécute pendant un certain temps, se termine ou échoue.
4. Si la première étape a réussi, exécutez l’étape suivante. En cas d’erreurs, examinez l’erreur dans les fichiers journaux. S’il s’agit d’une erreur de code, corrigez-la et exécutez de nouveau l’étape. 
5. Continuez ainsi jusqu’à ce que toutes les étapes s’exécutent sans erreur.
6. Une fois le débogage du cluster de test terminé, supprimez-le.

## <a name="next-steps"></a>étapes suivantes

* [Gérer des clusters HDInsight à l’aide de l’interface utilisateur Web d’Ambari](hdinsight-hadoop-manage-ambari.md)
* [Analyse des journaux HDInsight](hdinsight-debug-jobs.md)
* [Accéder aux journaux des applications YARN dans HDInsight sous Linux](hdinsight-hadoop-access-yarn-app-logs-linux.md)
* [Activer les dumps de tas pour les services Hadoop sur HDInsight sur Linux](hdinsight-hadoop-collect-debug-heap-dump-linux.md)
* [Problèmes connus du cluster Apache Spark sur Azure HDInsight](hdinsight-apache-spark-known-issues.md)
