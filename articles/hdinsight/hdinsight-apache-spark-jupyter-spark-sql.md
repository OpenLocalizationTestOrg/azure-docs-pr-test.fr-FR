---
title: "cluster d’aaaCreate un Apache Spark dans Azure HDInsight | Documents Microsoft"
description: "Démarrage rapide de HDInsight Spark sur comment toocreate un Apache Spark dans HDInsight de cluster."
keywords: "démarrage rapide spark,spark interactif,requête interactive,hdinsight spark,azure spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 91f41e6a-d463-4eb4-83ef-7bbb1f4556cc
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 002f71b3cd4fb315d4a556cebc9263026515ec4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-spark-cluster-in-azure-hdinsight"></a>Créer un cluster Apache Spark dans Azure HDInsight

Dans cet article, vous découvrez comment toocreate un Apache Spark cluster dans Azure HDInsight. Pour en savoir plus sur le service Spark sur HDInsight, consultez [Vue d’ensemble : Apache Spark sur Azure HDInsight](hdinsight-apache-spark-overview.md).

   ![Diagramme de démarrage rapide qui décrit les étapes toocreate un cluster Apache Spark sur Azure HDInsight](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "quickstart Spark à l’aide d’Apache Spark dans HDInsight. Étapes illustrées : création d’un cluster ; exécution d’une requête interactive Spark")

## <a name="prerequisites"></a>Composants requis

* **Un abonnement Azure**. Avant de commencer ce didacticiel, vous devez disposer d’un abonnement Azure. Voir [Créez votre compte Azure gratuit](https://azure.microsoft.com/free).

## <a name="create-hdinsight-spark-cluster"></a>Créer un cluster HDInsight Spark

Dans cette section, vous créez un cluster HDInsight Spark à l’aide d’un [modèle Azure Resource Manager](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/). Pour obtenir d’autres méthodes de création de cluster, consultez [Création de clusters HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

1. Cliquez sur hello suit image tooopen hello template Bonjour portail Azure.         

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-spark-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apache-spark-jupyter-spark-sql/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. Entrez hello valeurs suivantes :

    ![Créer un cluster HDInsight Spark à l’aide d’un modèle Azure Resource Manager](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Créer un cluster Spark dans HDInsight à l’aide d’un modèle Azure Resource Manager")

    * **Abonnement** : sélectionnez votre abonnement Azure pour ce cluster.
    * **Groupe de ressources** : créez un groupe de ressources ou sélectionnez un groupe existant. Groupe de ressources est utilisé toomanage ressources Azure pour vos projets.
    * **Emplacement**: sélectionnez un emplacement pour le groupe de ressources hello. modèle de Hello utilise cet emplacement pour la création de cluster de hello ainsi que pour stockage de cluster par défaut hello.
    * **ClusterName**: entrez un nom pour le cluster HDInsight de hello que vous souhaitez toocreate.
    * **Version de Spark**: sélectionnez **2.0** en tant que version hello que vous souhaitez tooinstall sur le cluster de hello.
    * **Nom de connexion et mot de passe de cluster**: nom de connexion hello par défaut est Admin.
    * **Nom d’utilisateur et mot de passe SSH**.

   Notez ces valeurs.  Vous avez besoin plus tard dans le didacticiel de hello.

3. Sélectionnez **J’accepte les conditions susmentionnées générales toohello**, sélectionnez **code confidentiel toodashboard**, puis cliquez sur **bon**. Vous pouvez voir une nouvelle vignette intitulée Envoi du déploiement pour Déploiement de modèle. Il prend le cluster de hello toocreate environ 20 minutes.

Si vous rencontrez un problème avec la création de clusters HDInsight, il peut être que vous n’avez pas toodo des autorisations appropriées hello ainsi. Consultez la page [À propos des noms d’espaces de contrôle d’accès](hdinsight-administer-use-portal-linux.md#create-clusters) pour plus d’informations.

> [!NOTE]
> Cet article crée un cluster Spark utilise [stockage en cluster objets BLOB de stockage Azure en tant que hello](hdinsight-hadoop-use-blob-storage.md). Vous pouvez également créer un cluster Spark qui utilise [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) comme stockage par défaut de hello. Pour plus d’informations, voir [Créer un cluster HDInsight avec Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).
>
>

## <a name="run-a-hive-query-using-spark-sql"></a>Exécuter une requête Hive à l’aide de Spark SQL

Lorsque vous utilisez un bloc-notes jupyter configuré pour votre cluster HDInsight Spark, vous obtenez une présélection `sqlContext` que vous pouvez utiliser les requêtes Hive toorun à l’aide de Spark SQL. Dans cette section, vous apprendrez comment toostart un bloc-notes jupyter, puis exécutez une requête Hive base.

1. Ouvrez hello [portail Azure](https://portal.azure.com/).

2. Si vous avez choisi de tableau de bord toohello toopin hello cluster, cliquez sur hello en mosaïque de cluster à partir du Panneau de cluster hello du tableau de bord toolaunch hello.

    Si vous ne pas épinglez hello cluster toohello du tableau de bord, à partir du volet de gauche hello, cliquez sur **clusters HDInsight**, puis cliquez sur cluster hello vous avez créé.

3. À partir de **Liens rapides**, cliquez sur **Tableaux de bord de Cluster**, puis sur **Bloc-notes Jupyter**. Si vous y êtes invité, entrez les informations d’identification du admin de hello pour le cluster de hello.

   ![Ouvrez Notebook bloc-notes toorun interactive Spark requête SQL](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "la requête interactive Spark SQL Notebook ouvrir Bloc-notes toorun")

   > [!NOTE]
   > Vous pouvez également accéder bloc-notes jupyter de hello pour votre cluster en hello ouverture suivante d’URL dans votre navigateur. Remplacez **CLUSTERNAME** avec nom hello de votre cluster :
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. Créez un bloc-notes. Cliquez sur **Nouveau**, puis sur **PySpark**.

   ![Créer une requête de Spark SQL interactive Notebook bloc-notes toorun](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "créer une requête de Spark SQL Notebook bloc-notes toorun interactive")

   Un nouvel ordinateur portable est créé et ouvert avec le nom hello Untitled(Untitled.pynb).

4. Cliquez sur le nom du bloc-notes hello haut hello et entrez un nom convivial, si vous le souhaitez.

    ![Fournissez un nom pour hello Jupter bloc-notes toorun Spark requêtes interactif de](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "fournir un nom pour hello Jupter bloc-notes toorun interactive Spark requête à partir de")

5.  Suit hello de coller le code dans une cellule vide, puis appuyez sur **MAJ + ENTRÉE** code hello de toorun. Dans le code hello ci-dessous `%%sql` (magique de sql appelée hello) indique hello de toouse bloc-notes Notebook présélection `sqlContext` requête Hive de hello toorun. requête de Hello récupère hello 10 premières lignes d’une table Hive (**hivesampletable**) qui est disponible par défaut sur tous les clusters HDInsight.

        %%sql
        SELECT * FROM hivesampletable LIMIT 10

    ![Requête Hive dans HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "Requête Hive dans HDInsight Spark")

    Pour plus d’informations sur hello `%%sql` magique et hello présélection des contextes, consultez [noyaux Notebook disponibles pour un cluster HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).

    > [!NOTE]
    > Chaque fois que vous exécutez une requête dans le bloc-notes, le titre de la fenêtre de navigateur web affiche un **(occupé)** état, ainsi que le titre du bloc-notes hello. Vous voyez également un toohello suivant cercle plein **PySpark** texte dans l’angle supérieur droit de hello. Une fois le travail de hello est terminé, il modifie tooa les cercle vide.
    >
    >
    
6. écran Hello doit actualiser le résultat de la requête tooshow hello.

    ![Sortie de requête Hive dans HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "Sortie de requête Hive dans HDInsight Spark")

7. Arrêt des ressources de cluster hello hello bloc-notes toorelease une fois que vous avez terminé d’exécuter l’application hello. toodo donc de hello **fichier** cliquez sur le menu d’un ordinateur portable hello, **fermer et s’arrêter**.

8. Si vous envisagez d’étapes de hello toocomplete à une date ultérieure, assurez-vous que vous supprimez le cluster HDInsight de hello que vous avez créé dans cet article. 

    [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-step"></a>Étape suivante 

Dans cet article, vous avez appris comment toocreate un HDInsight Spark cluster et exécutez une base Spark SQL de requête. Avance toohello toolearn de l’article suivant comment toouse un HDInsight Spark cluster toorun des requêtes interactives sur les exemples de données.

> [!div class="nextstepaction"]
>[Exécuter des requêtes interactives sur un cluster HDInsight Spark](hdinsight-apache-spark-load-data-run-query.md)



