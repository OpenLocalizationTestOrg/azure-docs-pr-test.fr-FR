---
title: aaaGet main Hadoop et Hive dans Azure HDInsight | Documents Microsoft
description: "Découvrez comment les clusters toocreate HDInsight et interroger des données avec la ruche."
keywords: "prise en main de hadoop,hadoop sur linux,démarrage rapide de hadoop,prise en main de hive,démarrage rapide de hive"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6a12ed4c-9d49-4990-abf5-0a79fdfca459
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: jgao
ms.openlocfilehash: 3d96d78121200ebda3626dd2c3885e3ddacd546d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="hadoop-tutorial-get-started-using-hadoop-in-hdinsight"></a>Didacticiel Hadoop : prise en main de Hadoop dans HDInsight

Découvrez comment toocreate [Hadoop](http://hadoop.apache.org/) clusters HDInsight et comment des travaux toorun Hive dans HDInsight. [Apache Hive](https://hive.apache.org/) est hello le composant les plus populaires dans l’écosystème de Hadoop hello. HDInsight est actuellement fournie avec [sept types de cluster](hdinsight-hadoop-introduction.md#overview). Chaque type de cluster prend en charge un ensemble de composants bien spécifiques. Tous les types de cluster prennent en charge Hive. Pour obtenir la liste des composants pris en charge dans HDInsight, consultez [quelles sont les nouveautés dans les versions de cluster Hadoop hello fournies par HDInsight ?](hdinsight-component-versioning.md)  

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="prerequisites"></a>Composants requis
Avant de commencer ce didacticiel, vous devez disposer des éléments suivants :

* **Abonnement Azure**: toocreate un compte d’essai un mois gratuit, parcourir trop[azure.microsoft.com/free](https://azure.microsoft.com/free).

## <a name="create-cluster"></a>Créer un cluster

La plupart des tâches Hadoop sont des tâches de traitements par lots. Vous créez un cluster, exécutez certaines tâches, puis supprimez le cluster de hello. Cette section vous permet de créer un cluster Hadoop dans HDInsight à l’aide d’un [modèle Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md). Aucune expérience avec le modèle Resource Manager n’est requise pour ce didacticiel. Pour d’autres méthodes de création de cluster et les propriétés hello utilisées dans ce didacticiel, consultez [HDInsight de créer des clusters](hdinsight-hadoop-provision-linux-clusters.md). Utilisez le sélecteur de hello haut hello de hello page toochoose vos options de création de cluster.

modèle de gestionnaire de ressources Hello utilisé dans ce didacticiel se trouve dans [GitHub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-password/). 

1. Cliquez sur hello suivant toosign image dans tooAzure et modèle du Gestionnaire de ressources ouvrir hello Bonjour portail Azure. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-ssh-password%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. Entrez ou sélectionnez hello valeurs suivantes :
   
    ![HDInsight Linux get a démarré le modèle de gestionnaire de ressources sur le portail](./media/hdinsight-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-arm-template-on-portal.png "cluster Hadoop de déployer à l’aide de HDInsigut hello portail Azure et un modèle de gestionnaire de groupe de ressources").
   
    * **Abonnement** : sélectionnez votre abonnement Azure.
    * **Groupe de ressources** : créez un groupe de ressources ou sélectionnez-en un.  Un groupe de ressources est un conteneur de composants Azure.  Dans ce cas, groupe de ressources hello contient le cluster HDInsight de hello et compte de stockage Azure hello dépendant. 
    * **Emplacement**: sélectionner un emplacement Azure où vous souhaitez toocreate votre cluster.  Choisissez un tooyou proche emplacement pour de meilleures performances. 
    * **Type du cluster** : pour les besoins de ce didacticiel, sélectionnez **hadoop**.
    * **Nom du cluster**: entrez un nom pour le cluster Hadoop de hello.
    * **Nom de connexion et mot de passe de cluster**: nom de connexion par défaut hello est **admin**.
    * **Mot de passe et le nom d’utilisateur SSH**: nom d’utilisateur par défaut de hello est **sshuser**.  Vous pouvez le renommer. 
     
    Certaines propriétés ont été codé en dur dans le modèle de hello.  Vous pouvez configurer ces valeurs à partir du modèle de hello.

    * **Emplacement**: hello emplacement du cluster de hello et même emplacement que le groupe de ressources hello hello hello partage de compte de stockage dépendant.
    * **Version de cluster** : 3.5
    * **Type de système d’exploitation** : Linux
    * **Nombre de nœuds de travail** : 2

     Chaque cluster possède une dépendance [compte de stockage Azure](hdinsight-hadoop-use-blob-storage.md) ou [compte Azure Data Lake](hdinsight-hadoop-use-data-lake-store.md). Il s’agit en tant que compte de stockage par défaut hello. Cluster HDInsight et son compte de stockage par défaut doivent coexister Bonjour même région Azure. Suppression de clusters ne supprime pas le compte de stockage hello. 
     
     Pour consulter une présentation de ces propriétés, voir [Création de clusters Hadoop basés sur Linux dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

3. Sélectionnez **J’accepte les conditions susmentionnées générales toohello** et **code confidentiel toodashboard**, puis cliquez sur **bon**. Vous devez voir une nouvelle vignette intitulée **déploiement d’un modèle de déploiement** sur le tableau de bord de portail hello. Cela prend environ environ 20 minutes toocreate un cluster. Une fois que le cluster de hello est créé, légende hello de vignette de hello est modifié toohello nom de groupe de ressources spécifié. Et le portail de hello ouvre automatiquement le groupe de ressources hello dans un nouveau panneau. Vous pouvez voir le cluster de hello et de stockage par défaut de hello répertoriés.
   
    ![Prise en main de HDInsight sous Linux - Groupe de ressources](./media/hdinsight-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-resource-group.png "Groupe de ressources de cluster Azure HDInsight").

4. Cliquez sur hello cluster nom tooopen hello cluster dans un nouveau panneau.

   ![Prise en main de HDInsight sous Linux - Paramètres du cluster](./media/hdinsight-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-cluster-settings.png "Propriétés de cluster HDInsight")


## <a name="run-hive-queries"></a>Exécuter des requêtes Hive
[Apache Hive](hdinsight-use-hive.md) est hello de composant les plus populaires utilisée dans HDInsight. Il existe de nombreuses façons toorun ruche travaux dans HDInsight. Dans ce didacticiel, vous utilisez hello vue Ambari Hive à partir du portail de hello. Pour d’autres méthodes d’envoi de tâches Hive, consultez la page [Utilisation de Hive et HiveQL avec Hadoop dans HDInsight pour l’analyse d’un exemple de fichier Apache log4j](hdinsight-use-hive.md).

1. À partir de la capture d’écran précédente hello, cliquez sur **tableau de bord de Cluster**, puis cliquez sur **tableau de bord de Cluster HDInsight**.  Vous pouvez également parcourir trop **https://&lt;nomcluster >. azurehdinsight.net**, où &lt;nomcluster > est le cluster hello vous avez créé dans hello précédente section tooopen Ambari.
2. Entrez le nom d’utilisateur de hello Hadoop et le mot de passe que vous avez spécifié dans la section précédente de hello. nom d’utilisateur par défaut de Hello est **admin**.
3. Ouvrez **affichage de la ruche** comme indiqué dans hello suivant capture d’écran :
   
    ![Sélection des vues Ambari](./media/hdinsight-hadoop-linux-tutorial-get-started/selecthiveview.png "Menu Affichage Hive dans HDInsight").
4. Bonjour **l’éditeur de requête** section de page hello, hello coller suivant les instructions HiveQL dans la feuille de calcul hello :
   
        SHOW TABLES;
   
   > [!NOTE]
   > Hive requiert l’utilisation d’un point-virgule.       
   > 
   > 
5. Cliquez sur **Exécuter**. A **résultats du processus de requête** section devant apparaître sous hello éditeur de requête et afficher des informations sur la tâche de hello. 
   
    Une fois la requête hello est terminée, hello **résultats du processus de requête** section affiche les résultats de hello de hello. Vous devriez voir une table appelée **hivesampletable**. Cet exemple de table Hive est fourni avec tous les clusters HDInsight de hello.
   
    ![Affichages Hive dans HDInsight](./media/hdinsight-hadoop-linux-tutorial-get-started/hiveview.png "Éditeur de requête de l’affichage Hive dans HDInsight").
6. Répétez les étapes 4 et hello toorun de l’étape 5 suivant la requête :
   
        SELECT * FROM hivesampletable;
   
   > [!TIP]
   > Hello de note **enregistrer les résultats** déroulante Bonjour supérieur gauche de hello **résultats du processus de requête** section ; vous pouvez utiliser cette résultats hello du téléchargement tooeither, ou les enregistrer tooHDInsight stockage dans un fichier CSV.
   > 
   > 
7. Cliquez sur **historique** tooget une liste des tâches de hello.

Une fois que vous avez terminé une tâche Hive, vous pouvez [exporter la base de données SQL hello résultats tooAzure ou de la base de données SQL Server](hdinsight-use-sqoop-mac-linux.md), vous pouvez également [visualiser les résultats de hello à l’aide d’Excel](hdinsight-connect-excel-power-query.md). Pour plus d’informations sur l’utilisation de Hive dans HDInsight, consultez [utilisez Hive et HiveQL avec Hadoop dans HDInsight tooanalyze un exemple de fichier log4j Apache](hdinsight-use-hive.md).

## <a name="clean-up-hello-tutorial"></a>Nettoyer le didacticiel de hello
Après avoir terminé le didacticiel de hello, vous souhaiterez cluster hello de toodelete. Avec HDInsight, vos données sont stockées Azure Storage, pour que vous puissiez supprimer un cluster en toute sécurité s’il n’est pas en cours d’utilisation. Vous devez également payer pour un cluster HDInsight, même lorsque vous ne l’utilisez pas. Étant donné que les frais de hello pour le cluster de hello sont autant de fois plus de frais hello pour le stockage, il est judicieux économique toodelete clusters lorsqu’ils ne sont pas en cours d’utilisation. 

> [!NOTE]
> À l’aide de [Azure Data Factory](hdinsight-hadoop-create-linux-clusters-adf.md), vous pouvez créer des clusters HDInsight à la demande et configurer une TimeToLive paramètre trop supprimer les clusters hello automatiquement. 
> 
> 

**toodelete hello hello et/ou de cluster par défaut compte de stockage**

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Tableau de bord de portail hello, cliquez sur mosaïque hello avec le nom de groupe de ressources hello que vous avez utilisé lors de la création de cluster de hello.
3. Cliquez sur **supprimer** hello panneau toodelete hello ressource groupe de ressources, qui contient le cluster de hello et compte de stockage par défaut hello ; ou cliquez sur le nom du cluster hello hello **ressources** vignette, puis cliquez sur **Supprimer** sur le panneau de cluster hello. Remarque la suppression du groupe de ressources hello supprime le compte de stockage hello. Si vous souhaitez que le compte de stockage tookeep hello, choisissez le cluster hello toodelete.

## <a name="troubleshoot"></a>Résolution des problèmes

Si vous rencontrez des problèmes lors de la création de clusters HDInsight, reportez-vous aux [exigences de contrôle d’accès](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous avez appris comment toocreate un HDInsight basés sur Linux à l’aide d’un modèle de gestionnaire de ressources de cluster et les requêtes Hive base tooperform.

toolearn en savoir plus sur l’analyse de données avec HDInsight, consultez hello suivant des articles :

* toolearn savoir plus sur l’utilisation de la ruche avec HDInsight, y compris le fonctionnement des requêtes tooperform Hive à partir de Visual Studio, consultez [utilisez Hive hdinsight][hdinsight-use-hive].
* toolearn sur Pig, un langage tootransform données, consultez [utilisez Pig hdinsight][hdinsight-use-pig].
* toolearn sur MapReduce, une façon dont les programmes toowrite qui traitent les données sur Hadoop, consultez [MapReduce utilisation hdinsight][hdinsight-use-mapreduce].
* toolearn sur l’utilisation des outils HDInsight de hello pour les données de tooanalyze de Visual Studio sur HDInsight, consultez [prise en main des outils de Visual Studio Hadoop pour HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).

Si vous êtes prêt toostart fonctionne avec vos propres données et que vous devez tooknow savoir plus sur HDInsight stocke les données ou comment les données de tooget dans HDInsight, voir hello :

* Pour plus d’informations sur la façon dont HDInsight utilise le stockage Azure, consultez la page [Use Azure Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md) (Utilisation du stockage Azure avec HDInsight).
* Pour plus d’informations sur la façon de tooupload tooHDInsight de données, consultez [télécharger des données tooHDInsight][hdinsight-upload-data].

Si vous souhaitez que toolearn plus d’informations sur la création ou de gestion d’un cluster HDInsight, consultez hello :

* toolearn sur la gestion de votre cluster HDInsight de basés sur Linux, consultez [HDInsight de gérer des clusters à l’aide de Ambari](hdinsight-hadoop-manage-ambari.md).
* toolearn savoir plus sur les options de hello vous pouvez sélectionner lors de la création d’un cluster HDInsight, consultez [création de HDInsight sur Linux à l’aide des options personnalisées](hdinsight-hadoop-provision-linux-clusters.md).
* Si vous êtes familiarisé avec Linux et Hadoop, mais tooknow spécificités Hadoop sur hello HDInsight, consultez [utilisation de HDInsight sur Linux](hdinsight-hadoop-linux-information.md). Cet article vous fournit les informations suivantes :
  
  * URL pour les services hébergés sur le cluster hello, telles que Ambari et WebHCat
  * emplacement des fichiers de Hadoop et des exemples sur le système de fichiers local hello de Hello
  * utilisation de Hello d’Azure Storage (WASB) au lieu de HDFS en tant que banque de données par défaut hello

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-provision]: hdinsight-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


