---
title: "aaaApache structurées Spark diffusion en continu avec Kafka - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment toouse Apache Spark diffusion en continu (DStream) tooget données dans ou hors d’Apache Kafka. Dans cet exemple, vous diffusez des données à l’aide d’un bloc-notes Jupyter à partir de Spark sur HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/09/2017
ms.author: larryfr
ms.openlocfilehash: 0837e8fc5ea314e644daed029d596feeb2b02c68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-spark-structured-streaming-with-kafka-preview-on-hdinsight"></a>Utiliser Spark Structured Streaming avec Kafka (préversion) sur HDInsight

Découvrez comment toouse Spark structurée de diffusion en continu des données de tooread de Kafka Apache sur Azure HDInsight.

Spark Structured Streaming est un moteur de traitement de flux basé sur Spark SQL. Il permet de que vous calculs de diffusion en continu tooexpress hello identique au calcul du lot sur les données statiques. Pour plus d’informations sur la diffusion en continu structuré, consultez hello [structurées de diffusion en continu Guide de programmation [Alpha]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) sur le site Apache.org.

> [!IMPORTANT]
> Cet exemple utilise Spark 2.1 sur HDInsight 3.6. Structured Streaming est considéré comme __alpha__ sur Spark 2.1.
>
> étapes Hello dans ce document créent un groupe de ressources Azure qui contient à la fois un Spark sur HDInsight et un Kafka sur le cluster HDInsight. Ces clusters sont situés dans un réseau virtuel Azure, ce qui permet de hello toodirectly de cluster Spark communiquent avec hello cluster de Kafka.
>
> Lorsque vous avez terminé les étapes hello dans ce document, n’oubliez pas de frais supplémentaires de toodelete hello clusters tooavoid.

## <a name="create-hello-clusters"></a>Créer des clusters de hello

Kafka Apache sur HDInsight ne fournit pas d’accès toohello Kafka courtiers sur hello internet public. Tout ce qui tooKafka doit se trouver dans des entretiens hello même réseau virtuel Azure en tant que nœuds hello dans hello cluster de Kafka. Pour cet exemple, hello Kafka et les clusters Spark se trouvent dans un réseau virtuel Azure. Hello diagramme suivant illustre le flux de communication entre les clusters hello :

![Diagramme des clusters Spark et Kafka dans un réseau virtuel Azure](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> Hello service de Kafka est toocommunication limitée dans le réseau virtuel de hello. Autres services sur un cluster de hello, tels que SSH et Ambari, sont accessibles via hello internet. Pour plus d’informations sur les ports publics de hello disponibles avec HDInsight, consultez [Ports et URI utilisé par HDInsight](hdinsight-hadoop-port-settings-for-services.md).

Si vous pouvez créer un réseau virtuel Azure, Kafka et Spark clusters manuellement, il est plus facile toouse un modèle Azure Resource Manager. Toodeploy un réseau virtuel Azure, Kafka, les étapes suivantes de hello utilisation et Spark clusters tooyour abonnement Azure.

1. Utilisez hello suivant toosign bouton dans tooAzure et modèle ouvert hello Bonjour portail Azure.
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v4.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
    
    Hello modèle Azure Resource Manager se trouve dans **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.

    Ce modèle crée hello suivant des ressources :

    * Un cluster Kafka sur HDInsight 3.5.
    * Un cluster Spark sur HDInsight 3.6.
    * Un réseau virtuel Azure, qui contient des clusters HDInsight de hello.

    > [!IMPORTANT]
    > bloc-notes diffusion en continu structuré Hello utilisé dans cet exemple nécessite Spark sur HDInsight 3.6. Si vous utilisez une version antérieure de Spark sur HDInsight, vous recevez des erreurs lorsque vous utilisez le bloc-notes de hello.

2. Hello utilisation suivant des entrées d’information toopopulate hello de hello **les déploiement personnalisé** panneau :
   
    ![Déploiement HDInsight personnalisé](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * **Groupe de ressources** : créez un groupe de ressources ou sélectionnez-en un. Ce groupe contient un cluster HDInsight de hello.

    * **Emplacement**: sélectionnez un tooyou géographiquement fermer d’emplacement.

    * **Nom du Cluster de base**: cette valeur est utilisée comme nom de base hello pour les clusters de Spark et Kafka hello. Par exemple, si vous entrez **hdi**, cela crée un cluster Spark nommé spark-hdi__ et un cluster Kafka nommé **kafka-hdi**.

    * **Nom d’utilisateur de cluster**: nom d’utilisateur admin hello pour les clusters de Spark et Kafka hello.

    * **Mot de passe de connexion cluster**: hello mot de passe administrateur pour les clusters de Spark et Kafka hello.

    * **Nom d’utilisateur SSH**: hello toocreate d’utilisateur SSH pour les clusters de Spark et Kafka hello.

    * **Mot de passe SSH**: mot de passe de hello pour hello SSH pour les clusters de Spark et Kafka hello.

3. Hello de lecture **termes et Conditions**, puis sélectionnez **J’accepte les termes du contrat de toohello et conditions susmentionnées**.

4. Enfin, recherchez **code confidentiel toodashboard** , puis sélectionnez **bon**. Il prend environ 20 minutes toocreate les clusters hello.

Une fois que les ressources hello ont été créées, vous êtes panneau des ressources de groupe toohello redirigé.

![Panneau des ressources de groupe de réseau virtuel de hello et des clusters](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> Notez que les noms de hello des clusters HDInsight de hello sont **spark-BASENAME** et **kafka-BASENAME**, où BASENAME est nom hello toohello modèle fourni. Vous utilisez ces noms dans les étapes suivantes lors de la connexion toohello clusters.

## <a name="get-hello-kafka-brokers"></a>Obtenir hello Kafka courtiers

Hello code dans cet exemple connecte toohello Kafka hôtes Bonjour cluster de Kafka du service broker. toofind hello hôtes de service broker Kafka, utilisez hello PowerShell ou Bash l’exemple suivant :

```powershell
$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
$clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$brokerHosts = $respObj.host_components.HostRoles.host_name
($brokerHosts -join ":9092,") + ":9092"
```

```bash
curl -u admin:$PASSWORD -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")'
```

> [!NOTE]
> Cet exemple attend `$PASSWORD` toocontain hello mot de passe au cluster de hello, et `$CLUSTERNAME` nom de hello toocontain Hello cluster de Kafka.
>
> Cet exemple utilise hello [jq](https://stedolan.github.io/jq/) données tooparse utilitaire de document JSON de hello.

Hello est similaire toohello suivant texte de sortie :

`wn0-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn1-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn2-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn3-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092`

Enregistrez ces informations, car il est utilisé dans les sections suivantes de ce document de hello.

## <a name="get-hello-notebooks"></a>Obtenir les blocs-notes hello

code Hello pour exemple hello décrite dans ce document est disponible à l’adresse [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).

## <a name="upload-hello-notebooks"></a>Télécharger les blocs-notes hello

Utilisez hello étapes suivantes blocs-notes de hello tooupload de hello projet tooyour Spark sur le cluster HDInsight :

1. Dans votre navigateur web, connectez-vous toohello bloc-notes jupyter sur votre cluster Spark. Bonjour suivant URL, remplacez `CLUSTERNAME` par nom hello de votre cluster Kafka :

        https://CLUSTERNAME.azurehdinsight.net/jupyter

    Lorsque vous y êtes invité, entrez la connexion de cluster hello (admin) et le mot de passe utilisé lors de la création de cluster de hello.

2. À partir de hello coin supérieur droit de la page de hello, utilisez hello __télécharger__ hello tooupload de bouton __flux-Tweets-To_Kafka.ipynb__ toohello de fichiers. Sélectionnez __ouvrir__ téléchargement de hello toostart.

    ![Utilisez tooselect de bouton de téléchargement hello et télécharger un ordinateur portable](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-button.png)

    ![Sélectionnez le fichier de KafkaStreaming.ipynb hello](./media/hdinsight-apache-kafka-spark-structured-streaming/select-notebook.png)

3. Recherche hello __flux-Tweets-To_Kafka.ipynb__ entrée dans la liste hello de blocs-notes et sélectionnez __télécharger__ bouton à côté de lui.

    ![Téléchargement de hello utilisez bouton en regard de tooupload d’entrée hello KafkaStreaming.ipynb il serveur bloc-notes de toohello](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-notebook.png)

4. Répétez les étapes hello tooload de 1 à 3 __Spark-structuré-diffusion en continu-de-Kafka.ipynb__ bloc-notes.

## <a name="load-tweets-into-kafka"></a>Charger des tweets dans Kafka

Une fois que les fichiers hello ont été téléchargés, sélectionnez hello __flux-Tweets-To_Kafka.ipynb__ bloc-notes de hello tooopen entrée. Suivez les étapes de hello de hello bloc-notes tooload tweets dans Kafka.

## <a name="process-tweets-using-spark-structured-streaming"></a>Traiter des tweets à l’aide de Spark Structured Streaming

À partir de hello bloc-notes Jupyter page d’accueil, sélectionnez hello __Spark-structuré-diffusion en continu-de-Kafka.ipynb__ entrée. Suivez les étapes de hello de hello bloc-notes tooload tweets de Kafka à l’aide de Spark structurée de diffusion en continu.

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez appris comment toouse Spark structurées en continu, consultez hello suivant toolearn documents plus sur l’utilisation de Spark et Kafka :

* [Comment toouse au service de diffusion en continu (DStream) avec Kafka](hdinsight-apache-spark-with-kafka.md).
* [Prise en main du bloc-notes Jupyter et Spark sur HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md)