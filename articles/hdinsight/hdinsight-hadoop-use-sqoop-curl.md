---
title: aaaUse Hadoop Sqoop avec Curl dans HDInsight - Azure | Documents Microsoft
description: "Découvrez comment tooremotely soumettre Sqoop tooHDInsight de travaux à l’aide de Curl."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 39798321-78ca-428c-bcfe-322e49af4059
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: d9c09a6704ab6c5f48be50ed6d6314ec406df8ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-sqoop-jobs-with-hadoop-in-hdinsight-with-curl"></a>Exécution de travaux Sqoop avec Hadoop dans HDInsight via Curl
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

Découvrez comment de cluster toouse Curl toorun Sqoop travaux sur un Hadoop dans HDInsight.

Curl est utilisé toodemonstrate comment vous pouvez interagir avec HDInsight à l’aide de toorun de demandes HTTP brut, analyse et récupérer les résultats de hello de Sqoop travaux. Cela fonctionne à l’aide de hello WebHCat API REST (anciennement Templeton) fournie par votre cluster HDInsight.

> [!NOTE]
> Si vous êtes déjà familiarisé avec l’utilisation de serveurs de Hadoop basé sur Linux, mais sont tooHDInsight nouvelle, consultez [plus d’informations sur l’utilisation de HDInsight sur Linux](hdinsight-hadoop-linux-information.md).
> 
> 

## <a name="prerequisites"></a>Composants requis
toocomplete hello étapes décrites dans cet article, vous devez suivant de hello :

* Un cluster Hadoop sur HDInsight (Linux ou Windows)
* [Curl](http://curl.haxx.se/)
* [jq](http://stedolan.github.io/jq/)

## <a name="submit-sqoop-jobs-by-using-curl"></a>Envoi de travaux Sqoop avec Curl
> [!NOTE]
> Lorsque vous utilisez Curl ou toute autre communication reste avec WebHCat, vous devez vous authentifier les demandes hello en fournissant le nom d’utilisateur hello et mot de passe administrateur de cluster HDInsight hello. Vous devez également utiliser le nom du cluster hello comme partie d’identificateur de ressource uniforme (URI) de hello utilisé serveur toohello de toosend hello demandes.
> 
> Pour les commandes hello dans cette section, remplacez **nom d’utilisateur** avec cluster de toohello tooauthenticate hello utilisateur, puis remplacez **mot de passe** avec mot de passe hello hello compte d’utilisateur. Remplacez **CLUSTERNAME** avec nom hello de votre cluster.
> 
> API REST Hello est sécurisé via [l’authentification de base](http://en.wikipedia.org/wiki/Basic_access_authentication). Vous devez toujours effectuer des requêtes en utilisant HTTP sécurisée (HTTPS) toohelp vous assurer que vos informations d’identification sont envoyées en toute sécurité toohello server.
> 
> 

1. À partir d’une ligne de commande, utilisez hello suivant tooverify de commande que vous pouvez vous connecter à tooyour HDInsight cluster :
   
        curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
   
    Vous devez recevoir une suivant toohello similaire de réponse :
   
        {"status":"ok","version":"v1"}
   
    paramètres de Hello utilisés dans cette commande sont les suivantes :
   
   * **-u** -nom d’utilisateur hello et le mot de passe de demande de hello tooauthenticate utilisé.
   * **-G** : indique qu’il s’agit d’une demande GET.
     
     Bonjour à partir de l’URL de hello, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, sera hello identique pour toutes les demandes. chemin d’accès de Hello, **/Status**, indique cette demande hello est tooreturn état WebHCat (également appelé Templeton) pour le serveur de hello. 
2. Utilisez hello suivant toosubmit un travail sqoop :

        curl -u USERNAME:PASSWORD -d user.name=USERNAME -d command="export --connect jdbc:sqlserver://SQLDATABASESERVERNAME.database.windows.net;user=USERNAME@SQLDATABASESERVERNAME;password=PASSWORD;database=SQLDATABASENAME --table log4jlogs --export-dir /tutorials/usesqoop/data --input-fields-terminated-by \0x20 -m 1" -d statusdir="wasb:///example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/sqoop

    paramètres de Hello utilisés dans cette commande sont les suivantes :

    * **-d** - depuis `-G` n’est pas utilisé, demande de hello par défaut est la méthode POST de toohello. `-d`Spécifie les valeurs de données hello qui sont envoyés avec la demande de hello.

        * **User.nom** -utilisateur hello qui commande hello est en cours d’exécution.

        * **commande** -hello Sqoop commande tooexecute.

        * **statusdir** -répertoire hello hello l’état de cette tâche sera écrit dans.

    Cette commande doit retourner un ID de tâche qui peut être l’état de hello toocheck utilisés du travail de hello.

        {"id":"job_1415651640909_0026"}

1. état de hello toocheck du travail hello, hello utilisez commande suivante. Remplacez **JOBID** avec la valeur hello retourné à l’étape précédente de hello. Par exemple, si hello retourner la valeur était `{"id":"job_1415651640909_0026"}`, puis **JOBID** serait `job_1415651640909_0026`.
   
        curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
   
    Si le travail de hello terminée, hello état n’aura pas **SUCCEEDED**.
   
   > [!NOTE]
   > Cette demande Curl retourne un document JavaScript Objet Notation (JSON) avec des informations sur la tâche de hello ; jq sert tooretrieve hello uniquement la valeur d’état.
   > 
   > 
2. Une fois que l’état hello du travail de hello a changé trop**SUCCEEDED**, vous pouvez récupérer les résultats de hello du travail de hello à partir du stockage d’objets Blob Azure. Hello `statusdir` passés avec la requête de hello contient l’emplacement hello hello du fichier de sortie ; dans ce cas, **wasb : / / exemple/curl**. Cette adresse stocke la sortie hello du travail de hello Bonjour **exemple/curl** répertoire sur le conteneur de stockage hello par défaut utilisé par votre cluster HDInsight.
   
    Vous pouvez répertorier et télécharger ces fichiers à l’aide de hello [CLI d’Azure](../cli-install-nodejs.md). Par exemple, fichiers toolist **exemple/curl**, utilisez hello de commande suivante :
   
        azure storage blob list <container-name> example/curl
   
    toodownload un fichier, utilisez hello qui suit :
   
        azure storage blob download <container-name> <blob-name> <destination-file>
   
   > [!NOTE]
   > Vous devez spécifier soit le nom de compte de stockage hello qui contient l’objet blob de hello à l’aide de hello `-a` et `-k` paramètres, ou ensemble hello **AZURE\_stockage\_compte** et **AZURE\_stockage\_accès\_clé** variables d’environnement. Consultez <a href="hdinsight-upload-data.md" target="_blank" pour plus d'informations.
   > 
   > 

## <a name="limitations"></a>Limites
* L’exportation en bloc - basés sur Linux avec un HDInsight, hello Sqoop connecteur utilisé tooexport données tooMicrosoft SQL Server ou base de données SQL Azure ne prend actuellement pas en charge les insertions en bloc.
* Le traitement par lot - Hdinsight basés sur Linux, lorsque vous utilisez hello `-batch` commutateur lorsque vous effectuez des insertions, Sqoop effectue plusieurs insertions au lieu de traitement par lot des opérations d’insertion hello.

## <a name="summary"></a>Résumé
Comme illustré dans ce document, vous pouvez utiliser un toorun de demande HTTP brut, analyse et afficher les résultats des travaux de Sqoop hello sur votre cluster HDInsight.

Pour plus d’informations sur l’interface REST de hello utilisée dans cet article, consultez hello <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">guide de l’API REST de Sqoop</a>.

## <a name="next-steps"></a>Étapes suivantes
Pour obtenir des informations générales sur Hive avec HDInsight :

* [Utilisation de Sqoop avec Hadoop dans HDInsight](hdinsight-use-sqoop.md)

Pour plus d’informations sur d’autres méthodes de travail avec Hadoop sur HDInsight :

* [Utilisation de Hive avec Hadoop sur HDInsight](hdinsight-use-hive.md)
* [Utilisation de Pig avec Hadoop sur HDInsight](hdinsight-use-pig.md)
* [Utilisation de MapReduce avec Hadoop sur HDInsight](hdinsight-use-mapreduce.md)

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


