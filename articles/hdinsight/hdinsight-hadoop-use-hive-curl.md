---
title: aaaUse Hadoop Hive avec Curl dans HDInsight - Azure | Documents Microsoft
description: "Découvrez comment tooremotely submit Pig travaux tooHDInsight à l’aide de Curl."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6ce18163-63b5-4df6-9bb6-8fcbd4db05d8
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: e725829ad2adcf3540f44375e3e87b7cdaebd15e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-with-hadoop-in-hdinsight-using-rest"></a>Exécuter des requêtes Hive avec Hadoop dans HDInsight à l’aide de REST

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

Découvrez le fonctionnement des requêtes avec Hadoop toouse hello WebHCat REST API toorun Hive sur un cluster Azure HDInsight.

[Curl](http://curl.haxx.se/) est utilisé toodemonstrate comment vous pouvez interagir avec HDInsight à l’aide des requêtes HTTP bruts. Hello [jq](http://stedolan.github.io/jq/) utilitaire donnée utilisé tooprocess hello JSON retourné à partir de demandes REST.

> [!NOTE]
> Si vous êtes déjà familiarisé avec l’utilisation de serveurs de Hadoop basé sur Linux, mais sont tooHDInsight nouvelle, consultez hello [ce dont vous avez besoin tooknow sur Hadoop dans HDInsight de basés sur Linux](hdinsight-hadoop-linux-information.md) document.

## <a id="curl"></a>Exécuter des requêtes Hive

> [!NOTE]
> Lorsque vous utilisez cURL ou toute autre communication reste avec WebHCat, vous devez vous authentifier les demandes hello en fournissant le nom d’utilisateur hello et mot de passe administrateur de cluster HDInsight hello.
>
> Pour les commandes hello dans cette section, remplacez **nom d’utilisateur** avec cluster de toohello tooauthenticate hello utilisateur, puis remplacez **mot de passe** avec mot de passe hello hello compte d’utilisateur. Remplacez **CLUSTERNAME** avec nom hello de votre cluster.
>
> API REST Hello est sécurisé via [l’authentification de base](http://en.wikipedia.org/wiki/Basic_access_authentication). toohelp Assurez-vous que vos informations d’identification en toute sécurité envoyé toohello server, vérifiez systématiquement les demandes à l’aide de HTTP sécurisée (HTTPS).

1. À partir d’une ligne de commande, utilisez hello suivant tooverify de commande que vous pouvez vous connecter à tooyour HDInsight cluster :

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    Vous recevez un toohello similaire de réponse après le texte :

        {"status":"ok","version":"v1"}

    paramètres de Hello utilisés dans cette commande sont les suivantes :

   * **-u** -nom d’utilisateur hello et le mot de passe de demande de hello tooauthenticate utilisé.
   * **-G**: indique que la requête correspond à une opération GET.

     Bonjour à partir de l’URL de hello, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, est hello identique pour toutes les demandes. chemin d’accès de Hello, **/Status**, indique cette demande hello est tooreturn état WebHCat (également appelé Templeton) pour le serveur de hello. Vous pouvez également demander la version hello de ruche à l’aide de hello de commande suivante :

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/version/hive
    ```

     Cette requête retourne un toohello similaire de réponse après le texte :

       {"module":"hive","version":"0.13.0.2.1.6.0-2103"}

2. Hello utilisation suivant toocreate une table nommée **log4jLogs**:

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;DROP+TABLE+log4jLogs;CREATE+EXTERNAL+TABLE+log4jLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+ROW+FORMAT+DELIMITED+FIELDS+TERMINATED+BY+' '+STORED+AS+TEXTFILE+LOCATION+'/example/data/';SELECT+t4+AS+sev,COUNT(*)+AS+count+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log'+GROUP+BY+t4;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    Hello utilisés avec cette demande de paramètres suivants :

   * **-d** - depuis `-G` n’est pas utilisé, demande de hello par défaut est la méthode POST de toohello. `-d`Spécifie les valeurs de données hello qui sont envoyés avec la demande de hello.

     * **User.nom** -utilisateur hello qui commande hello est en cours d’exécution.
     * **Exécutez** -hello tooexecute d’instructions HiveQL.
     * **statusdir** -répertoire hello hello l’état de cette tâche est écrite dans.

     Ces instructions effectuent hello suivant des actions :
   * **DROP TABLE** -si hello table existe déjà, elle est supprimée.
   * **CREATE EXTERNAL TABLE** : crée une table « externe » dans Hive. Tables externes stockent uniquement la définition de table hello dans la ruche. les données de salutation reste dans l’emplacement d’origine de hello.

     > [!NOTE]
     > Tables externes doivent être utilisées lorsque vous attendez hello toobe de données sous-jacent mis à jour par une source externe. par exemple, par un processus de téléchargement de données automatisé ou une autre opération MapReduce.
     >
     > Suppression d’une table externe est **pas** supprimer les données de hello, uniquement la définition de table hello.

   * **FORMAT de ligne** - mise en forme les données de salutation. champs de Hello dans chaque journal sont séparés par un espace.
   * **EMPLACEMENT du fichier texte comme stockées** - emplacement de stockage des données de salutation (répertoire de données d’exemple hello) et qu’il est stocké sous forme de texte.
   * **Sélectionnez** -sélectionne un nombre de toutes les lignes où colonne **t4** contient la valeur de hello **[erreur]**. Cette instruction renvoie la valeur **3**, car trois lignes contiennent cette valeur.

     > [!NOTE]
     > Notez que les espaces hello entre les instructions HiveQL sont remplacés par hello `+` lorsqu’il est utilisé avec Curl de caractères. Les valeurs entre guillemets qui contiennent un espace, comme délimiteur de hello, ne doivent pas être remplacés par `+`.

   * **INPUT__FILE__NAME comme '% 25.log'** - cette instruction limites hello recherche tooonly utilisation de fichiers se terminant par. journal.

     > [!NOTE]
     > Hello `%25` étant formulaire codées URL de hello %, condition réelle de hello est `like '%.log'`. Hello % a URL toobe codée, comme il est traité comme un caractère spécial dans les URL.

     Cette commande doit retourner un ID de tâche qui peut être l’état de hello toocheck utilisés du travail de hello.

       {"id":"job_1415651640909_0026"}

3. état de hello toocheck du travail hello, hello utilisez commande suivante :

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    Remplacez **JOBID** avec la valeur hello retourné à l’étape précédente de hello. Par exemple, si hello retourner la valeur était `{"id":"job_1415651640909_0026"}`, puis **JOBID** serait `job_1415651640909_0026`.

    Si le travail de hello terminée, l’état hello est **SUCCEEDED**.

   > [!NOTE]
   > Cette demande Curl retourne un document JavaScript Objet Notation (JSON) avec des informations sur la tâche de hello. Jq sert tooretrieve hello uniquement la valeur d’état.

4. Une fois que l’état hello du travail de hello a changé trop**SUCCEEDED**, vous pouvez récupérer les résultats de hello du travail de hello à partir du stockage d’objets Blob Azure. Hello `statusdir` passés avec la requête de hello contient l’emplacement hello hello du fichier de sortie ; dans ce cas, **/exemple/curl**. Cette adresse stocke la sortie de hello Bonjour **exemple/curl** directory Bonjour clusters de stockage par défaut.

    Vous pouvez répertorier et télécharger ces fichiers à l’aide de hello [CLI d’Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli). Pour plus d’informations sur l’utilisation de hello CLI d’Azure avec le stockage Azure, consultez hello [utiliser Azure CLI 2.0 avec le stockage Azure](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) document.

5. Hello utilisation suivant les instructions toocreate une nouvelle table « interne » nommée **journaux d’erreurs de**:

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;CREATE+TABLE+IF+NOT+EXISTS+errorLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+STORED+AS+ORC;INSERT+OVERWRITE+TABLE+errorLogs+SELECT+t1,t2,t3,t4,t5,t6,t7+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log';SELECT+*+from+errorLogs;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    Ces instructions effectuent hello suivant des actions :

   * **CREATE TABLE IF NOT EXISTS** : crée une table, si elle n'existe pas déjà. Cette instruction crée une table interne, qui est stockée dans l’entrepôt de données Hive hello et entièrement gérée par ruche.

     > [!NOTE]
     > Contrairement aux tables externes, la suppression d’une table interne supprime également des données sous-jacentes hello.

   * **ORC de AS stockées** -stocke les données de hello dans format optimisé lignes en colonnes (ORC). ORC est un format particulièrement efficace et optimisé pour le stockage de données Hive.
   * **INSERT OVERWRITE ... Sélectionnez** -sélectionne des lignes à partir de hello **log4jLogs** table qui contiennent des **[erreur]**, puis insère hello des données dans hello **journaux d’erreurs de** table.
   * **Sélectionnez** -sélectionne toutes les lignes à partir de hello nouvelle **journaux d’erreurs de** table.

6. Utilisez l’ID de tâche hello a retourné l’état de hello toocheck du travail de hello. Une fois qu’elle a réussi, utilisez hello CLI d’Azure comme décrit précédemment toodownload et afficher les résultats de hello. sortie de Hello doit contenir trois lignes, qui contiennent toutes des **[erreur]**.

## <a id="nextsteps"></a>Étapes suivantes

Pour obtenir des informations générales sur Hive avec HDInsight :

* [Utilisation de Hive avec Hadoop sur HDInsight](hdinsight-use-hive.md)

Pour plus d’informations sur d’autres méthodes de travail avec Hadoop sur HDInsight :

* [Utilisation de Pig avec Hadoop sur HDInsight](hdinsight-use-pig.md)
* [Utilisation de MapReduce avec Hadoop sur HDInsight](hdinsight-use-mapreduce.md)

Si vous utilisez Tez avec Hive, consultez hello suivant des documents pour les informations de débogage :

* [Utilisez hello vue Ambari Tez sur HDInsight de basés sur Linux](hdinsight-debug-ambari-tez-view.md)

Pour plus d’informations sur hello API REST utilisé dans ce document, consultez hello [WebHCat référence](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) document.

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md




[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


