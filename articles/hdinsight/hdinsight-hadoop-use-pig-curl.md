---
title: aaaUse Hadoop Pig reste dans HDInsight - Azure | Documents Microsoft
description: "Découvrez comment les travaux de Pig Latin toorun toouse reste sur un Hadoop cluster dans Azure HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: ed5e10d1-4f47-459c-a0d6-7ff967b468c4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 760139e3caad9103d8c9d34e7f548d476014b5ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-with-hadoop-on-hdinsight-by-using-rest"></a>Exécution de tâches Pig avec Hadoop sur HDInsight à l’aide de REST

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Découvrez comment des travaux en rendant le cluster Azure HDInsight REST demandes tooan toorun Pig Latin. Curl est utilisé toodemonstrate comment vous pouvez interagir avec HDInsight à l’aide de hello WebHCat REST API.

> [!NOTE]
> Si vous êtes déjà familiarisé avec l’utilisation de serveurs de Hadoop basé sur Linux, mais sont tooHDInsight nouvelle, consultez [conseils de HDInsight basés sur Linux](hdinsight-hadoop-linux-information.md).

## <a id="prereq"></a>Configuration requise

* Un cluster Azure HDInsight (Hadoop sur HDInsight) Windows ou Linux

  > [!IMPORTANT]
  > Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* [Curl](http://curl.haxx.se/)

* [jq](http://stedolan.github.io/jq/)

## <a id="curl"></a>Exécution de tâches Pig à l’aide de Curl

> [!NOTE]
> API REST Hello est sécurisé via [l’authentification d’accès de base](http://en.wikipedia.org/wiki/Basic_access_authentication). Toujours effectuer des demandes à l’aide de tooensure HTTP sécurisée (HTTPS) que vos informations d’identification sont envoyées en toute sécurité toohello server.
>
> Lorsque vous utilisez des commandes hello dans cette section, remplacez `USERNAME` avec cluster de toohello tooauthenticate hello utilisateur, puis remplacez `PASSWORD` avec mot de passe hello hello compte d’utilisateur. Remplacez `CLUSTERNAME` avec nom hello de votre cluster.
>


1. À partir d’une ligne de commande, utilisez hello suivant tooverify de commande que vous pouvez vous connecter à tooyour HDInsight cluster :

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    Vous devez recevoir hello suivant de réponse JSON :

        {"status":"ok","version":"v1"}

    paramètres de Hello utilisés dans cette commande sont les suivantes :

    * **-u**: nom d’utilisateur hello et le mot de passe utilisé demande de hello tooauthenticate
    * **-G** : indique que la requête correspond à une requête GET.

     Bonjour à partir de l’URL de hello, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, est hello identique pour toutes les demandes. chemin d’accès de Hello, **/Status**, indique cette demande hello est état hello tooreturn WebHCat (également appelé Templeton) pour le serveur de hello.

2. Utilisez hello suivant code toosubmit un cluster de toohello travail Pig Latin :

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="LOGS=LOAD+'/example/data/sample.log';LEVELS=foreach+LOGS+generate+REGEX_EXTRACT($0,'(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)',1)+as+LOGLEVEL;FILTEREDLEVELS=FILTER+LEVELS+by+LOGLEVEL+is+not+null;GROUPEDLEVELS=GROUP+FILTEREDLEVELS+by+LOGLEVEL;FREQUENCIES=foreach+GROUPEDLEVELS+generate+group+as+LOGLEVEL,COUNT(FILTEREDLEVELS.LOGLEVEL)+as+count;RESULT=order+FREQUENCIES+by+COUNT+desc;DUMP+RESULT;" -d statusdir="/example/pigcurl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/pig
    ```

    paramètres de Hello utilisés dans cette commande sont les suivantes :

    * **-d**: car `-G` n’est pas utilisé, demande de hello par défaut est la méthode POST de toohello. `-d`Spécifie les valeurs de données hello qui sont envoyés avec la demande de hello.

    * **User.nom**: utilisateur hello qui commande hello est en cours d’exécution
    * **Exécutez**: hello Pig Latin instructions tooexecute
    * **statusdir**: répertoire hello hello l’état de cette tâche est écrite dans

    > [!NOTE]
    > Notez que les espaces hello dans les instructions de Pig Latin sont remplacés par hello `+` lorsqu’il est utilisé avec Curl de caractères.

    Cette commande doit retourner un ID de tâche qui peut être un état de hello toocheck utilisé hello du travail de, par exemple :

        {"id":"job_1415651640909_0026"}

3. état de hello toocheck du travail hello, hello utilisez commande suivante

     ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

     Remplacez `JOBID` avec la valeur hello retourné à l’étape précédente de hello. Par exemple, si hello retourner la valeur était `{"id":"job_1415651640909_0026"}`, puis `JOBID` est `job_1415651640909_0026`.

    Si le travail de hello terminée, l’état hello est **SUCCEEDED**.

    > [!NOTE]
    > Cette demande Curl retourne une JavaScript Object Notation (JSON) document avec plus d’informations sur la tâche de hello et jq est tooretrieve utilisé hello uniquement la valeur d’état.

## <a id="results"></a>Affichage des résultats

Lorsque état hello du travail de hello est devenue trop**SUCCEEDED**, vous pouvez récupérer les résultats de hello du travail de hello. Hello `statusdir` passés avec la requête de hello contient l’emplacement hello hello du fichier de sortie ; dans ce cas, `/example/pigcurl`.

HDInsight peut utiliser le stockage Azure ou Azure Data Lake Store en tant que banque de données par défaut hello. Il existe différentes façons tooget données hello selon l’application que vous utilisez. Pour plus d’informations, consultez la section de stockage hello Hello [basés sur Linux de HDInsight informations](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) document.

## <a id="summary"></a>Résumé

Comme illustré dans ce document, vous pouvez utiliser un toorun de demande HTTP brut, d’analyse et d’afficher les résultats des travaux de Pig hello sur votre cluster HDInsight.

Pour plus d’informations sur l’interface REST de hello utilisée dans cet article, consultez hello [WebHCat référence](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).

## <a id="nextsteps"></a>Étapes suivantes

Pour obtenir des informations générales sur Pig dans HDInsight :

* [Utilisation de Pig avec Hadoop sur HDInsight](hdinsight-use-pig.md)

Pour plus d’informations sur d’autres méthodes de travail avec Hadoop sur HDInsight :

* [Utilisation de Hive avec Hadoop sur HDInsight](hdinsight-use-hive.md)
* [Utilisation de MapReduce avec Hadoop sur HDInsight](hdinsight-use-mapreduce.md)
