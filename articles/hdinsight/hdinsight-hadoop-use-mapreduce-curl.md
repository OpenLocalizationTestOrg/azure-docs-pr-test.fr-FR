---
title: aaaUse MapReduce et Curl avec Hadoop dans HDInsight - Azure | Documents Microsoft
description: "Découvrez comment tooremotely exécuter les tâches MapReduce avec Hadoop dans HDInsight à l’aide de Curl."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: bc6daf37-fcdc-467a-a8a8-6fb2f0f773d1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 16920205bacf9699f88090568099e0508a172b3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-rest"></a>Exécution des tâches MapReduce avec Hadoop sur HDInsight avec REST

Découvrez comment toouse hello WebHCat REST API toorun MapReduce travaux sur un Hadoop sur le cluster HDInsight. Curl est utilisé toodemonstrate comment vous pouvez interagir avec HDInsight à l’aide de travaux de MapReduce toorun de demandes HTTP bruts.

> [!NOTE]
> Si vous êtes déjà familiarisé avec l’utilisation de serveurs de Hadoop basé sur Linux, mais sont de nouveau tooHDInsight, consultez hello [ce dont vous avez besoin tooknow sur basés sur Linux de Hadoop dans HDInsight](hdinsight-hadoop-linux-information.md) document.


## <a id="prereq"></a>Configuration requise

* Un cluster Hadoop sur HDInsight
* [Curl](http://curl.haxx.se/)
* [jq](http://stedolan.github.io/jq/)

## <a id="curl"></a>Exécution de tâches MapReduce à l'aide de Curl

> [!NOTE]
> Lorsque vous utilisez Curl ou toute autre communication reste avec WebHCat, vous devez vous authentifier les demandes hello en fournissant le mot de passe et le nom d’utilisateur administrateur hello HDInsight cluster. Vous devez utiliser le nom du cluster hello dans le cadre de hello URI qui est utilisé toosend hello demandes toohello serveur.
>
> Pour les commandes hello dans cette section, remplacez **nom d’utilisateur** avec cluster de hello utilisateur tooauthenticate toohello, et **mot de passe** avec mot de passe hello hello compte d’utilisateur. Remplacez **CLUSTERNAME** avec nom hello de votre cluster.
>
> API REST Hello est sécurisé à l’aide de [l’authentification d’accès de base](http://en.wikipedia.org/wiki/Basic_access_authentication). Vous devez toujours effectuer des requêtes en utilisant tooensure HTTPS que vos informations d’identification sont envoyées en toute sécurité toohello server.


1. À partir d’une ligne de commande, utilisez hello suivant tooverify de commande que vous pouvez vous connecter à tooyour HDInsight cluster :

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    Vous devez recevoir un toohello similaire de réponse suivant JSON :

        {"status":"ok","version":"v1"}

    paramètres de Hello utilisés dans cette commande sont les suivantes :

   * **-u**: indique le nom d’utilisateur hello et le mot de passe utilisé demande de hello tooauthenticate
   * **-G**: indique que cette opération est une requête GET

     Bonjour à partir de hello URI, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, est hello identique pour toutes les demandes.

2. toosubmit une tâche MapReduce, utilisez hello de commande suivante :

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d jar=/example/jars/hadoop-mapreduce-examples.jar -d class=wordcount -d arg=/example/data/gutenberg/davinci.txt -d arg=/example/data/CurlOut https://CLUSTERNAME.azurehdinsight.net/templeton/v1/mapreduce/jar
    ```

    fin de Hello Hello URI/mapreduce/jar () indique WebHCat que cette demande démarre une tâche MapReduce à partir d’une classe dans un fichier jar. paramètres de Hello utilisés dans cette commande sont les suivantes :

   * **-d**: `-G` n’est pas utilisé, afin de la demande de hello par défaut est la méthode POST de toohello. `-d`Spécifie les valeurs de données hello qui sont envoyés avec la demande de hello.
    * **User.nom**: utilisateur hello qui commande hello est en cours d’exécution
    * **JAR**: emplacement hello du fichier jar hello qui contient la classe toobe a exécuté.
    * **classe**: hello de classe qui contient la logique hello MapReduce
    * **arg**: hello arguments toobe passé toohello MapReduce travail. Dans ce cas, le répertoire de fichiers et de hello texte qui sont utilisés pour la sortie de hello d’entrée hello

     Cette commande doit retourner un ID de tâche qui peut être l’état de hello toocheck utilisés du travail de hello :

       {"id":"job_1415651640909_0026"}

3. état de hello toocheck du travail hello, hello utilisez commande suivante :

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    Remplacez hello **JOBID** avec la valeur hello retourné à l’étape précédente de hello. Par exemple, si hello retourner la valeur était `{"id":"job_1415651640909_0026"}`, puis les hello JOBID serait `job_1415651640909_0026`.

    Si le travail de hello est terminée, état de hello retournée est `SUCCEEDED`.

   > [!NOTE]
   > Cette demande Curl retourne un document JSON avec des informations sur la tâche de hello. Jq sert tooretrieve hello uniquement la valeur d’état.

4. Lorsque état hello du travail de hello est devenue trop`SUCCEEDED`, vous pouvez récupérer les résultats de hello du travail de hello à partir du stockage d’objets Blob Azure. Hello `statusdir` paramètre est passé avec la requête de hello contient l’emplacement hello hello du fichier de sortie. Dans cet exemple, emplacement de hello est `/example/curl`. Cette adresse stocke sortie hello du travail de hello dans le stockage de valeur par défaut de clusters hello à `/example/curl`.

Vous pouvez répertorier et télécharger ces fichiers à l’aide de hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli). Pour plus d’informations sur l’utilisation des objets BLOB à partir de hello CLI d’Azure, consultez hello [Using hello Azure CLI 2.0 avec le stockage Azure](../storage/common/storage-azure-cli.md#create-and-manage-blobs) document.

## <a id="nextsteps"></a>Étapes suivantes

Pour obtenir des informations générales sur les tâches MapReduce dans HDInsight :

* [Utilisation de MapReduce avec Hadoop sur HDInsight](hdinsight-use-mapreduce.md)

Pour plus d’informations sur d’autres méthodes de travail avec Hadoop sur HDInsight :

* [Utilisation de Hive avec Hadoop sur HDInsight](hdinsight-use-hive.md)
* [Utilisation de Pig avec Hadoop sur HDInsight](hdinsight-use-pig.md)

Pour plus d’informations sur l’interface REST hello qui est utilisé dans cet article, consultez hello [WebHCat référence](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).
