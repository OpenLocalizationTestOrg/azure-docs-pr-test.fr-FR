---
title: les clusters avec Data Lake Store aaaUse hello toocreate portail Azure Azure HDInsight | Documents Microsoft
description: Utiliser hello toocreate portail Azure et utiliser des clusters HDInsight avec Azure Data Lake Store
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: a8c45a83-a8e3-4227-8b02-1bc1e1de6767
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: nitinme
ms.openlocfilehash: f23113d444a3c5a01894dba29f75f3621b2d16bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-by-using-hello-azure-portal"></a>Créer des clusters HDInsight avec Data Lake Store à l’aide de hello portail Azure
> [!div class="op_single_selector"]
> * [Utilisez hello portail Azure](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [Utiliser PowerShell (pour le stockage par défaut)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [Utiliser PowerShell (pour le stockage supplémentaire)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Utiliser Resource Manager](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

Découvrez comment toouse hello toocreate portail Azure un cluster HDInsight avec un compte Azure Data Lake Store en tant que stockage par défaut de hello ou un stockage supplémentaire. Bien que le stockage supplémentaire est facultatif pour un cluster HDInsight, il est recommandé de toostore vos données d’entreprise dans les comptes de stockage supplémentaires hello.

## <a name="prerequisites"></a>Composants requis
Avant de commencer ce didacticiel, assurez-vous que vous avez répondu hello suivant les exigences :

* **Un abonnement Azure**. Accédez trop[version d’évaluation gratuite de Azure d’obtenir](https://azure.microsoft.com/pricing/free-trial/).
* **Un compte Azure Data Lake Store**. Suivez les instructions hello [prise en main Azure Data Lake Store à l’aide de hello Azure portal](data-lake-store-get-started-portal.md). Vous devez également créer un dossier racine sur le compte de hello.  Dans ce didacticiel, un dossier racine appelé __/clusters__ est utilisé.
* **Un principal de service Azure Active Directory**. Ce didacticiel fournit des instructions sur la façon de toocreate un principal de service dans Azure Active Directory (Azure AD). Toutefois, de le toocreate un principal de service, vous devez être un administrateur Azure AD. Si vous êtes un administrateur, vous pouvez ignorer cette condition préalable et poursuivre le didacticiel de hello.

    >[!NOTE]
    >Vous pouvez créer un principal de service uniquement si vous être administrateur Azure AD. Votre administrateur Azure AD doit créer un principal de service. Vous pouvez ensuite créer un cluster HDInsight avec Data Lake Store. En outre, le principal du service hello doit être créée avec un certificat, comme décrit dans [créer un principal de service avec certificat](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).
    >

## <a name="create-an-hdinsight-cluster"></a>Création d'un cluster HDInsight

Dans cette section, vous créez un cluster HDInsight avec des comptes Data Lake Store en tant que valeur par défaut hello hello supplémentaires. Cet article traite uniquement la partie hello de la configuration de comptes Data Lake Store.  Pour les informations de la création de cluster général hello et des procédures, consultez [Hadoop de créer des clusters dans HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).

### <a name="create-a-cluster-with-data-lake-store-as-default-storage"></a>Création d’un cluster avec Data Lake Store en tant que stockage par défaut

**toocreate un HDInsight cluster avec un Data Lake Store en tant que compte de stockage par défaut hello**

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Suivez [créer des clusters](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md#create-clusters) pour des informations générales hello sur la création de clusters HDInsight.
3. Sur hello **stockage** panneau, sous **type de stockage principal**, sélectionnez **Data Lake Store**, puis entrez hello informations suivantes :

    ![Cluster tooHDInsight principal de service ajouter](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.adls.storage.png "ajouter service tooHDInsight principal de cluster")

    - **Sélectionner un compte Data Lake Store** : sélectionnez un compte Data Lake Store existant. Un compte Data Lake Store existant est requis.  Consultez les [Conditions préalables](#prereuisites).
    - **Chemin d’accès racine**: entrez un chemin d’accès où les fichiers spécifiques à un cluster hello sont toobe stockée. Sur la capture d’écran de hello, il est __/clusters/myhdiadlcluster/__, dans quel hello __/clusters__ dossier doit exister, et crée hello Portal *myhdicluster* dossier.  Hello *myhdicluster* est le nom du cluster hello.
    - **Accès de Data Lake Store**: configurer l’accès entre le compte Data Lake Store de hello et du cluster HDInsight. Pour obtenir des instructions, consultez [Configurer l’accès aux données Data Lake Store](#configure-data-lake-store-access).
    - **Comptes de stockage supplémentaires**: comptes d’ajouter des comptes de stockage Azure en tant que stockage supplémentaire pour le cluster de hello. Magasins de LAC de données supplémentaires tooadd est effectué en attribuant des autorisations de cluster hello sur les données de plusieurs comptes Data Lake Store lors de la configuration d’un compte Data Lake Store en tant que type de stockage principal hello. Consultez [Configurer l’accès à Data Lake Store](#configure-data-lake-store-access).

4. Sur hello **l’accès Data Lake Store**, cliquez sur **sélectionnez**, puis continuez la création du cluster, comme décrit dans [Hadoop de créer des clusters dans HDInsight](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md).


### <a name="create-a-cluster-with-data-lake-store-as-additional-storage"></a>Création d’un cluster avec Data Lake Store en tant que stockage supplémentaire

Hello instructions suivantes créer un cluster HDInsight avec un compte de stockage Azure en tant que stockage par défaut de hello et d’un compte Data Lake Store en tant qu’un stockage supplémentaire.
**toocreate un HDInsight cluster avec un Data Lake Store en tant que compte de stockage par défaut hello**

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Suivez [créer des clusters](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md#create-clusters) pour des informations générales hello sur la création de clusters HDInsight.
3. Sur hello **stockage** panneau, sous **type de stockage principal**, sélectionnez **Azure Storage**, puis entrez hello informations suivantes :

    ![Cluster tooHDInsight principal de service ajouter](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.png "ajouter service tooHDInsight principal de cluster")

    - **Méthode de sélection**: utilisez une des options suivantes de hello :

        * toospecify un compte de stockage qui fait partie de votre abonnement Azure, sélectionnez **Mes abonnements**, puis sélectionnez le compte de stockage hello.
        * toospecify un compte de stockage qui se trouve en dehors de votre abonnement Azure, sélectionnez **clé d’accès**, puis fournissez les informations de hello pour hello en dehors du compte de stockage.

    - **Conteneur par défaut**: utiliser hello valeur par défaut ou spécifier votre propre nom.

    - Les comptes de stockage supplémentaires : ajouter plusieurs comptes de stockage Azure en tant qu’espace de stockage supplémentaire hello.
    - Accès de Data Lake Store : configurer l’accès entre le compte Data Lake Store de hello et du cluster HDInsight. Pour obtenir des instructions, consultez [Configurer l’accès aux données Data Lake Store](#configure-data-lake-store-access).

## <a name="configure-data-lake-store-access"></a>Configurer l’accès aux données Data Lake Store 

Dans cette section, vous configurez l’accès à Data Lake Store à partir des clusters HDInsight au moyen d’un principal du service Azure Active Directory. 

### <a name="specify-a-service-principal"></a>Spécifier un principal du service

À partir de hello portail Azure, vous pouvez utiliser un principal de service existant ou créez-en un.

**toocreate un principal de service à partir de hello portail Azure**

1. Cliquez sur **l’accès Data Lake Store** à partir du Panneau de magasin hello.
2. Sur hello **l’accès Data Lake Store** panneau, cliquez sur **nouvel**.
3. Cliquez sur **Principal du Service**, puis suivez les instructions de hello toocreate un principal de service.
4. Télécharger le certificat de hello si vous décidez de toouse à nouveau dans hello futures. Téléchargement du certificat de hello est utile que si vous souhaitez toouse hello même service principal lorsque vous créez des clusters HDInsight supplémentaires.

    ![Cluster tooHDInsight principal de service ajouter](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.2.png "ajouter service tooHDInsight principal de cluster")

4. Cliquez sur **accès** accès au dossier de tooconfigure hello.  Reportez-vous à [Configurer les autorisations des fichiers](#configure-file-permissions).


**toouse un service existant principal à partir de hello portail Azure**

1. Cliquez sur **Accès à Data Lake Store**.
1. Sur hello **l’accès Data Lake Store** panneau, cliquez sur **existant**.
2. Cliquez sur **Principal du service**, puis sélectionnez un principal du service. 
3. Télécharger hello certificat (fichier .pfx) qui est associé à votre principal de service sélectionné, puis entrez le mot de passe du certificat hello.

    ![Cluster tooHDInsight principal de service ajouter](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.5.png "ajouter service tooHDInsight principal de cluster")

4. Cliquez sur **accès** accès au dossier de tooconfigure hello.  Reportez-vous à [Configurer les autorisations des fichiers](#configure-file-permissions).


### <a name="configure-file-permissions"></a>Configurer les autorisations des fichiers

Hello configure sont différentes selon que le compte de hello est utilisée en tant que stockage par défaut de hello ou un compte de stockage supplémentaire :

- Utilisation en tant que stockage par défaut

    - autorisation au niveau racine de hello Hello compte Data Lake Store
    - autorisation au niveau racine de hello Hello stockage du cluster HDInsight. Par exemple, hello __/clusters__ dossier utilisé précédemment dans le didacticiel de hello.
- Utilisation en tant que stockage supplémentaire

    - Autorisation dossiers hello où vous avez besoin d’accès au fichier.

**autorisation tooassign à hello au niveau racine de compte Data Lake Store**

1. Sur hello **l’accès Data Lake Store** panneau, cliquez sur **accès**. Hello **sélectionner les autorisations de fichier** panneau est ouvert. Il répertorie tous les comptes Data Lake Store hello votre abonnement.
2. Placez le curseur (ne cliquez pas sur) souris hello sur nom hello Hello compte Data Lake Store toomake hello case visible, puis sélectionnez hello case à cocher.

    ![Cluster tooHDInsight principal de service ajouter](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3.png "ajouter service tooHDInsight principal de cluster")

  Par défaut, __READ__, __WRITE__ ET __EXECUTE__ sont tous sélectionnés.

3. Cliquez sur **sélectionnez** bas hello de page de hello.
4. Cliquez sur **exécuter** tooassign autorisation.
5. Cliquez sur **Done**.

**autorisation tooassign à hello au niveau racine de cluster HDInsight**

1. Sur hello **l’accès Data Lake Store** panneau, cliquez sur **accès**. Hello **sélectionner les autorisations de fichier** panneau est ouvert. Il répertorie tous les comptes Data Lake Store hello votre abonnement.
1. À partir de hello **sélectionner les autorisations de fichier** panneau, cliquez sur hello Data Lake Store nom tooshow son contenu.
2. Sélectionnez la racine de stockage du cluster HDInsight hello en sélectionnant la case à cocher hello sur gauche hello du dossier de hello. En fonction de capture d’écran de toohello précédemment, est de racine de stockage du cluster hello __/clusters__ dossier que vous avez spécifié lors de la sélection hello Data Lake Store en tant que stockage de la valeur par défaut.
3. Définir les autorisations de hello sur le dossier de hello.  Par défaut, les autorisations en lecture, écriture et exécution sont toutes sélectionnées.
4. Cliquez sur **sélectionnez** bas hello de page de hello.
5. Cliquez sur **Exécuter**.
6. Cliquez sur **Done**.

Si vous utilisez Data Lake Store en tant que stockage supplémentaire, vous devez attribuer autorisation uniquement pour les dossiers de hello que vous souhaitez tooaccess à partir du cluster HDInsight de hello. Par exemple, dans la capture d’écran de hello ci-dessous, vous procurez aux accès uniquement trop**hdiaddonstorage** dossier dans un compte Data Lake Store.

![Affecter le service de cluster principal autorisations toohello HDInsight](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3-1.png "le cluster HDInsight toohello affecter service principal d’autorisations")


## <a name="verify-cluster-set-up"></a>Vérification de la configuration de cluster

Après l’installation de cluster hello, dans Panneau de cluster hello, vérifiez vos résultats en effectuant l’une ou les deux hello comme suit :

* tooverify hello stockage associé pour le cluster de hello est compte Data Lake Store hello que vous avez spécifié, puis cliquez sur **comptes de stockage** dans le volet gauche de hello.

    ![Cluster tooHDInsight principal de service ajouter](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6-1.png "ajouter service tooHDInsight principal de cluster")

* tooverify qui hello principal du service est correctement associé au cluster HDInsight de hello, cliquez sur **l’accès Data Lake Store** dans le volet gauche de hello.

    ![Cluster tooHDInsight principal de service ajouter](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6.png "ajouter service tooHDInsight principal de cluster")


## <a name="examples"></a>Exemples

Après que vous avez configuré cluster hello avec Data Lake Store en tant que votre stockage, consultez les exemples de toothese de comment toouse HDInsight cluster données hello tooanalyze qui sont stockées dans Data Lake Store.

### <a name="run-a-hive-query-against-data-in-a-data-lake-store-as-primary-storage"></a>Exécuter une requête Hive sur des données stockées dans Data Lake Store (comme stockage principal)

toorun une requête Hive, utiliser l’interface de vues hello Hive dans le portail de Ambari hello. Pour savoir comment toouse Ambari ruche vues, consultez [hello d’utiliser la ruche de vue avec Hadoop dans HDInsight](../hdinsight/hdinsight-hadoop-use-hive-ambari-view.md).

Lorsque vous travaillez avec des données dans un magasin Data Lake Store, il existe quelques chaînes toochange.

Si vous utilisez, par exemple, hello cluster que vous avez créé avec Data Lake Store comme stockage principal, les données de toohello hello chemin d’accès sont : *adl : / / < data_lake_store_account_name > /azuredatalakestore.net/path/to/file*. Un toocreate de requête Hive une table à partir d’exemples de données qui sont stockés dans hello compte Data Lake Store ressemble à hello après l’instruction :

    CREATE EXTERNAL TABLE websitelog (str string) LOCATION 'adl://hdiadlsstorage.azuredatalakestore.net/clusters/myhdiadlcluster/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/'

Descriptions :
* `adl://hdiadlstorage.azuredatalakestore.net/`est la racine hello hello compte Data Lake Store.
* `/clusters/myhdiadlcluster`est la racine hello des données de cluster hello que vous avez spécifié lors de la création du cluster de hello.
* `/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/`est l’emplacement hello du fichier d’exemple hello que vous avez utilisé dans la requête de hello.

### <a name="run-a-hive-query-against-data-in-a-data-lake-store-as-additional-storage"></a>Exécuter une requête Hive sur des données dans Data Lake Store (comme stockage supplémentaire)

Si le cluster hello que vous avez créé utilise le stockage d’objets Blob en tant que stockage par défaut, les données d’exemple hello ne sont pas contenues dans hello compte Azure Data Lake Store qui est utilisé comme espace de stockage supplémentaire. Dans ce cas, tout d’abord transférer les données de salutation de toohello de stockage d’objets Blob Data Lake Store, puis exécutez des requêtes de hello comme indiqué dans le précédent exemple de hello.

Pour plus d’informations sur la façon dont toocopy depuis le stockage Blob tooa Data Lake du magasin de données, consultez hello suivant des articles :

* [Utiliser des données de toocopy Distcp entre les objets BLOB de stockage Azure et Data Lake Store](data-lake-store-copy-data-wasb-distcp.md)
* [Utiliser des données de toocopy AdlCopy depuis le stockage Azure BLOB tooData Lake Store](data-lake-store-copy-data-azure-storage-blob.md)

### <a name="use-data-lake-store-with-a-spark-cluster"></a>Utiliser Data Lake Store avec un cluster Spark
Vous pouvez utiliser les travaux du Spark toorun un cluster Spark sur les données stockées dans un Data Lake Store. Pour plus d’informations, consultez [données de tooanalyze du cluster utilisez HDInsight Spark dans Data Lake Store](../hdinsight/hdinsight-apache-spark-use-with-data-lake-store.md).


### <a name="use-data-lake-store-in-a-storm-topology"></a>Utiliser Data Lake Store dans une topologie Storm
Vous pouvez utiliser les données de toowrite hello Data Lake Store à partir d’une topologie Storm. Pour obtenir des instructions sur la façon de tooachieve ce scénario, consultez [utilisez Azure Data Lake Store avec Apache Storm hdinsight](../hdinsight/hdinsight-storm-write-data-lake-store.md).

## <a name="see-also"></a>Voir aussi
* [PowerShell : Créer un toouse du cluster HDInsight Data Lake Store](data-lake-store-hdinsight-hadoop-use-powershell.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
