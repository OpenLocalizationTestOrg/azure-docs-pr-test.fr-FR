---
title: "aaaGet a démarré avec un exemple de HBase sur HDInsight - Azure | Documents Microsoft"
description: "Suivez cette toostart d’exemple Apache HBase à l’aide de hadoop dans HDInsight. Créer des tables à partir du shell HBase de hello et les interroger à l’aide de la ruche."
keywords: commande hbase, exemple hbase
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 4d6a2658-6b19-4268-95ee-822890f5a33a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 43419780142b320b16180a2b1f25020dee2f7a11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-an-apache-hbase-example-in-hdinsight"></a>Prise en main d’un exemple Apache HBase dans HDInsight

Découvrez comment créer des tables de HBase toocreate un cluster HBase dans HDInsight, et interroger des tables à l’aide de ruche. Pour obtenir des informations générales sur HBase, voir [Vue d’ensemble de HDInsight HBase][hdinsight-hbase-overview].

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="prerequisites"></a>Composants requis
Avant de commencer la tentative de cet exemple HBase, vous devez disposer de hello éléments suivants :

* **Un abonnement Azure**. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* [Secure Shell(SSH)](hdinsight-hadoop-linux-use-ssh-unix.md). 
* [curl](http://curl.haxx.se/download.html).

## <a name="create-hbase-cluster"></a>Créer un cluster HBase
Hello procédure suivante utilise une toocreate de modèle Azure Resource Manager un version 3.4 HBase de basés sur Linux cluster et hello dépendants compte par défaut le stockage Azure. paramètres de hello toounderstand utilisés dans la procédure de hello et d’autres méthodes de création de cluster, consultez [Hadoop basé sur Linux de créer des clusters dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

1. Cliquez sur hello suit image tooopen hello template Bonjour portail Azure. modèle de Hello se trouve dans un conteneur d’objets blob publics. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-tutorial-get-started-linux/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. À partir de hello **les déploiement personnalisé** panneau, entrez hello valeurs suivantes :
   
   * **Abonnement**: sélectionnez votre abonnement Azure est utilisé toocreate hello cluster.
   * **Groupe de ressources** : créez un groupe Azure Resource Manager ou utilisez un groupe existant.
   * **Emplacement**: spécifiez l’emplacement hello hello du groupe de ressources. 
   * **ClusterName**: entrez un nom pour le cluster de HBase hello.
   * **Nom de connexion et mot de passe de cluster**: nom de connexion par défaut hello est **admin**.
   * **Mot de passe et le nom d’utilisateur SSH**: nom d’utilisateur par défaut de hello est **sshuser**.  Vous pouvez le renommer.
     
     Tous les autres paramètres sont facultatifs.  
     
     Chaque cluster possède une dépendance de compte Stockage Azure. Après avoir supprimé un cluster, les données de salutation conservent dans le compte de stockage hello. nom du compte de stockage Hello cluster par défaut est le nom de cluster hello avec « store » ajouté. Il est codé en dur dans la section de variables de modèle hello.
3. Sélectionnez **J’accepte les conditions susmentionnées générales toohello**, puis cliquez sur **bon**. Il prend environ 20 minutes toocreate un cluster.

> [!NOTE]
> Après la suppression d’un cluster HBase, vous pouvez créer un autre cluster HBase à l’aide de hello même conteneur d’objets blob par défaut. nouveau cluster de Hello récupère les tables de HBase hello créées hello cluster d’origine. des incohérences tooavoid, nous vous conseillons de désactiver les tables HBase hello avant de supprimer le cluster de hello.
> 
> 

## <a name="create-tables-and-insert-data"></a>Créer des tables et insérer des données
Vous pouvez utiliser SSH tooconnect tooHBase clusters et utilisent des tables de HBase Shell toocreate HBase, insérer des données et interroger des données. Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

Pour la plupart des personnes, les données apparaissent sous forme de hello :

![Données tabulaires HBase HDInsight][img-hbase-sample-data-tabular]

Dans HBase (il s’agit d’une implémentation de BigTable), hello même données ressemble à :

![Données bigtable HBase HDInsight][img-hbase-sample-data-bigtable]


**toouse hello shell HBase**

1. À partir de SSH, exécutez hello HBase commande suivante :
   
    ```bash
    hbase shell
    ```

2. Créez une HBase contenant deux familles de colonne :

    ```hbaseshell   
    create 'Contacts', 'Personal', 'Office'
    list
    ```
3. Insérez des données :
    
    ```hbaseshell   
    put 'Contacts', '1000', 'Personal:Name', 'John Dole'
    put 'Contacts', '1000', 'Personal:Phone', '1-425-000-0001'
    put 'Contacts', '1000', 'Office:Phone', '1-425-000-0002'
    put 'Contacts', '1000', 'Office:Address', '1111 San Gabriel Dr.'
    scan 'Contacts'
    ```
   
    ![Interpréteur de commandes HBase Hadoop HDInsight][img-hbase-shell]
4. Récupérez une seule ligne :
   
    ```hbaseshell
    get 'Contacts', '1000'
    ```
   
    Vous devez voir hello mêmes résultats comme à l’aide de la commande d’analyse hello, car il y a qu’une seule ligne.
   
    Pour plus d’informations sur le schéma de la table HBase hello, consultez [Introduction tooHBase conception de schéma][hbase-schema]. Pour obtenir plus de commandes HBase, consultez le [Guide de référence Apache HBase][hbase-quick-start].
5. Sortie hello shell
   
    ```hbaseshell
    exit
    ```

**toobulk charger des données dans la table HBase de contacts hello**

HBase propose plusieurs méthodes pour charger des données dans des tables.  Pour en savoir plus, consultez la rubrique [Chargement en bloc](http://hbase.apache.org/book.html#arch.bulk.load).

Vous trouverez un exemple de fichier de données dans un conteneur de blobs public, *wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*.  contenu Hello hello du fichier de données est :

    8396    Calvin Raji      230-555-0191    230-555-0191    5415 San Gabriel Dr.
    16600   Karen Wu         646-555-0113    230-555-0192    9265 La Paz
    4324    Karl Xie         508-555-0163    230-555-0193    4912 La Vuelta
    16891   Jonn Jackson     674-555-0110    230-555-0194    40 Ellis St.
    3273    Miguel Miller    397-555-0155    230-555-0195    6696 Anchor Drive
    3588    Osa Agbonile     592-555-0152    230-555-0196    1873 Lion Circle
    10272   Julia Lee        870-555-0110    230-555-0197    3148 Rose Street
    4868    Jose Hayes       599-555-0171    230-555-0198    793 Crawford Street
    4761    Caleb Alexander  670-555-0141    230-555-0199    4775 Kentucky Dr.
    16443   Terry Chander    998-555-0171    230-555-0200    771 Northridge Drive

Vous pouvez éventuellement créer un fichier texte et télécharger le compte de stockage propre fichier tooyour de hello. Pour obtenir des instructions de hello, consultez [télécharger des données pour les travaux Hadoop dans HDInsight][hdinsight-upload-data].

> [!NOTE]
> Cette procédure utilise la table de Contacts HBase hello que vous avez créé dans la dernière procédure de hello.
> 

1. À partir de SSH, exécutez hello suivant commande tootransform hello tooStoreFiles du fichier de données et stocker à un chemin d’accès relatif spécifié par Dimporttsv.bulk.output.  Si vous êtes dans le HBase Shell, utilisez tooexit de commande exit hello.

    ```bash   
    hbase org.apache.hadoop.hbase.mapreduce.ImportTsv -Dimporttsv.columns="HBASE_ROW_KEY,Personal:Name,Personal:Phone,Office:Phone,Office:Address" -Dimporttsv.bulk.output="/example/data/storeDataFileOutput" Contacts wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt
    ```

2. Exécutez hello suivant des données de commande tooupload hello à partir de la table HBase à toohello /example/data/storeDataFileOutput :
   
    ```bash
    hbase org.apache.hadoop.hbase.mapreduce.LoadIncrementalHFiles /example/data/storeDataFileOutput Contacts
    ```

3. Vous pouvez ouvrir hello shell HBase et utiliser le contenu de la table hello analyse commande toolist hello.

## <a name="use-hive-tooquery-hbase"></a>Utiliser la ruche tooquery HBase

Vous pouvez interroger les données des tables HBase à l’aide de Hive. Dans cette section, vous créez une table Hive qui mappe la table HBase à toohello et utilise les données de salutation tooquery dans votre table HBase.

1. Ouvrez **PuTTY**et vous connecter toohello cluster.  Consultez les instructions hello dans la procédure précédente de hello.
2. À partir de la session SSH hello, utilisez hello suivant commande toostart Beeline :

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    Pour plus d’informations sur Beeline, consultez [Utilisation de Hive avec Hadoop dans HDInsight via Beeline](hdinsight-hadoop-use-hive-beeline.md).
       
3. Exécutez hello suivant HiveQL script toocreate une table Hive qui mappe la table HBase à toohello. Assurez-vous que vous avez créé la table d’exemple hello mentionné plus haut dans ce didacticiel à l’aide de shell HBase de hello avant d’exécuter cette instruction.

    ```hiveql   
    CREATE EXTERNAL TABLE hbasecontacts(rowkey STRING, name STRING, homephone STRING, officephone STRING, officeaddress STRING)
    STORED BY 'org.apache.hadoop.hive.hbase.HBaseStorageHandler'
    WITH SERDEPROPERTIES ('hbase.columns.mapping' = ':key,Personal:Name,Personal:Phone,Office:Phone,Office:Address')
    TBLPROPERTIES ('hbase.table.name' = 'Contacts');
    ```

4. Exécutez hello HiveQL script tooquery hello données dans la table HBase à hello suivantes :

    ```hiveql   
    SELECT count(rowkey) FROM hbasecontacts;
    ```

## <a name="use-hbase-rest-apis-using-curl"></a>Utilisation des API REST HBase à l’aide de Curl

API REST Hello est sécurisé via [l’authentification de base](http://en.wikipedia.org/wiki/Basic_access_authentication). Vous sont toujours effectuer des demandes à l’aide de HTTP sécurisée (HTTPS) toohelp vous assurer que vos informations d’identification sont envoyées en toute sécurité toohello server.

2. Utilisez hello commande toolist hello existant HBase tables suivantes :

    ```bash
    curl -u <UserName>:<Password> \
    -G https://<ClusterName>.azurehdinsight.net/hbaserest/
    ```

3. Utilisez hello suivant commande toocreate une nouvelle table HBase avec les familles de deux colonnes :

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/schema" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"@name\":\"Contact1\",\"ColumnSchema\":[{\"name\":\"Personal\"},{\"name\":\"Office\"}]}" \
    -v
    ```

    schéma de Hello est fournie au format JSon de hello.
4. Utilisez hello suivant de commande tooinsert des données :

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/false-row-key" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"Row\":[{\"key\":\"MTAwMA==\",\"Cell\": [{\"column\":\"UGVyc29uYWw6TmFtZQ==\", \"$\":\"Sm9obiBEb2xl\"}]}]}" \
    -v
    ```
   
    Vous devez en base64 encoder les valeurs hello spécifiés dans le commutateur -d de hello. Dans l’exemple de hello :
   
   * MTAwMA==: 1000
   * UGVyc29uYWw6TmFtZQ==: Personal:Name
   * Sm9obiBEb2xl: John Dole
     
     [clé de ligne false](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single) vous permet de tooinsert plusieurs valeurs (par lot).
5. Utilisez hello suivant commande tooget une ligne :
   
    ```bash 
    curl -u <UserName>:<Password> \
    -X GET "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/1000" \
    -H "Accept: application/json" \
    -v
    ```

Pour plus d’informations sur HBase Rest, voir le [Guide de référence Apache HBase](https://hbase.apache.org/book.html#_rest).

> [!NOTE]
> Thrift n’est pas pris en charge par HBase dans HDInsight.
>
> Lorsque vous utilisez Curl ou toute autre communication reste avec WebHCat, vous devez vous authentifier les demandes hello en fournissant le nom d’utilisateur hello et mot de passe administrateur de cluster HDInsight hello. Vous devez également utiliser le nom du cluster hello comme partie d’identificateur de ressource uniforme (URI) de hello utilisé serveur toohello de toosend hello demandes :
> 
>   
>        curl -u <UserName>:<Password> \
>        -G https://<ClusterName>.azurehdinsight.net/templeton/v1/status
>   
>    Vous devez recevoir un toohello similaire de réponse suivant la réponse :
>   
>        {"status":"ok","version":"v1"}
   


## <a name="check-cluster-status"></a>Vérification du statut du cluster
HBase dans HDInsight est livré avec une interface utilisateur web pour la surveillance des clusters. À l’aide de l’interface utilisateur Web de hello, vous pouvez demander des statistiques ou des informations sur les régions.

**tooaccess hello HBase Master UI**

1. L’authentification à hello hello Ambari Web UI à https://&lt;nomcluster >. azurehdinsight.net.
2. Cliquez sur **HBase** à partir du menu de gauche hello.
3. Cliquez sur **liens rapides** hello haut de page hello, point toohello active soigneur nœud lien et puis cliquez sur **HBase Master UI**.  l’interface utilisateur de Hello est ouvert dans un autre onglet de navigateur :

  ![Interface utilisateur principale HDInsight HBase](./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hmaster-ui.png)

  Hello HBase Master UI contient hello les sections suivantes :

  - serveurs de région
  - serveurs de sauvegarde
  - tables
  - tâches
  - attributs logiciels

## <a name="delete-hello-cluster"></a>Supprimer le cluster de hello
des incohérences tooavoid, nous vous conseillons de désactiver les tables HBase hello avant de supprimer le cluster de hello.

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>Résolution des problèmes

Si vous rencontrez des problèmes lors de la création de clusters HDInsight, reportez-vous aux [exigences de contrôle d’accès](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Étapes suivantes
Dans cet article, vous avez appris comment toocreate un cluster HBase et comment afficher et les tables toocreate hello données dans ces tables à partir de hello shell HBase. Vous avez également appris comment toouse une ruche des requêtes sur les données dans les tables HBase et comment toouse hello HBase c# API REST toocreate une table HBase et récupérer des données à partir de la table de hello.

toolearn, voir :

* [Vue d’ensemble de HDInsight HBase][hdinsight-hbase-overview] : HBase est une base de données NoSQL open source Apache basée sur Hadoop qui fournit un accès aléatoire et une forte cohérence pour de grandes quantités de données non structurées et semi-structurées.

[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hbase-reference]: http://hbase.apache.org/book.html#importtsv
[hbase-schema]: http://0b4af6cdc2f0c5998459-c0245c5c937c5dedcca3f1764ecc9b2f.r43.cf2.rackcdn.com/9353-login1210_khurana.pdf
[hbase-quick-start]: http://hbase.apache.org/book.html#quickstart





[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-versions]: hdinsight-component-versioning.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-portal]: https://portal.azure.com/
[azure-create-storageaccount]: http://azure.microsoft.com/documentation/articles/storage-create-storage-account/

[img-hdinsight-hbase-cluster-quick-create]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-quick-create.png
[img-hdinsight-hbase-hive-editor]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hive-editor.png
[img-hdinsight-hbase-file-browser]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-file-browser.png
[img-hbase-shell]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-shell.png
[img-hbase-sample-data-tabular]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-tabular.png
[img-hbase-sample-data-bigtable]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-bigtable.png
