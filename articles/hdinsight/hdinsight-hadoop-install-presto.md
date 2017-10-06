---
title: les clusters Presto sur Azure HDInsight Linux aaaInstall | Documents Microsoft
description: "Découvrez comment tooinstall Presto et Airpal sur basés sur Linux HDInsight Hadoop les clusters à l’aide des Actions de Script."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/17/2017
ms.author: nitinme
ms.openlocfilehash: 5d54d0efc3e5fdc6f5a8d3a94ad2f61d16df24c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-presto-on-hdinsight-hadoop-clusters"></a>Installer et utiliser Presto sur des clusters Hadoop HDInsight

Dans cette rubrique, vous découvrez comment tooinstall Presto sur HDInsight Hadoop clusters en utilisant l’Action de Script. Vous apprendrez également comment tooinstall Airpal sur un cluster HDInsight appliqués aux existant.

> [!IMPORTANT]
> Hello étapes décrites dans ce document nécessitent une **cluster HDInsight 3.5 Hadoop** qui utilise Linux. Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez la page [Versions de HDInsight](hdinsight-component-versioning.md).

## <a name="what-is-presto"></a>Qu’est-ce que Presto ?
[Presto](https://prestodb.io/overview.html) est un moteur de requête SQL rapide distribué pour les Big Data. Presto convient à l’exécution interactive de requêtes de pétaoctets de données. Pour plus d’informations sur les composants de hello Presto et comment ils fonctionnent ensemble, consultez [concepts Presto](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst).

> [!WARNING]
> Les composants fournis avec le cluster HDInsight de hello sont entièrement gérés et permet de tooisolate et résoudre les problèmes connexes toothese composants de Support technique de Microsoft.
> 
> Les composants personnalisés, tels que Presto, réception efforcera toohelp vous toofurther hello de dépannage. Cela peut entraîner hello de résoudre ou demandant que vous tooengage les canaux disponibles pour hello ouvrir technologies source où se trouve une grande expérience pour cette technologie. Vous pouvez, par exemple, utiliser de nombreux sites de communauté, comme le [forum MSDN sur HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). En outre, les projets Apache ont des sites de projet sur [http://apache.org](http://apache.org). Par exemple : [Hadoop](http://hadoop.apache.org/).
> 
> 


## <a name="install-presto-using-script-action"></a>Installer Presto à l’aide d’une action de script

Cette section explique comment toouse hello exemple de script lors de la création d’un nouveau cluster à l’aide de hello portail Azure. 

1. Démarrer l’approvisionnement d’un cluster à l’aide des étapes hello dans [clusters basés sur Linux de fourniture de HDInsight](hdinsight-hadoop-create-linux-clusters-portal.md). Vérifiez que vous créez le cluster hello à l’aide de hello **personnalisé** flux de création de cluster. Vous devez vous assurer que vous créez le cluster hello répond aux hello suivant les exigences.

    a. Ce doit être un cluster Hadoop créé avec la version 3.5 de HDInsight.

    b. Elle doit utiliser le stockage Azure en tant que banque de données hello. À l’aide de tour sur un cluster qui utilise Azure Data Lake Store comme option de stockage hello n’est pas encore pris en charge. 

    ![Créer un cluster HDInsight à l’aide d’options personnalisées](./media/hdinsight-hadoop-install-presto/hdinsight-install-custom.png)

2. Sur hello **paramètres avancés** panneau, sélectionnez **Actions de Script**et fournissent des informations de hello ci-dessous :
   
   * **NOM**: entrez un nom convivial pour l’action de script hello.
   * **URI de script bash** : `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`
   * **HEAD**: cochez cette option.
   * **WORKER** : cochez cette option
   * **ZOOKEEPER** : décochez cette case
   * **PARAMETERS**: laissez ce champ vide.


3. En bas de hello Hello **Actions de Script** panneau, cliquez sur hello **sélectionnez** configuration hello toosave du bouton. Enfin, cliquez sur hello **sélectionnez** bouton bas hello hello **paramètres avancés** informations de configuration de panneau toosave hello.

4. Continuer la mise en service de cluster de hello comme décrit dans [clusters basés sur Linux de fourniture de HDInsight](hdinsight-hadoop-create-linux-clusters-portal.md).

    > [!NOTE]
    > Azure PowerShell, hello CLI d’Azure, hello HDInsight .NET SDK ou modèles Azure Resource Manager peuvent également être utilisés tooapply les actions de script. Vous pouvez également appliquer tooalready d’actions de script clusters en cours d’exécution. Pour plus d’informations, consultez la page [Personnaliser des clusters HDInsight à l’aide d’une action de script](hdinsight-hadoop-customize-cluster-linux.md).
    > 
    > 

## <a name="use-presto-with-hdinsight"></a>Utiliser Presto avec HDInsight

Effectuer hello suivant les étapes toouse Presto dans un cluster HDInsight après avoir installé à l’aide des étapes hello décrites ci-dessus.

1. Connecter le cluster HDInsight de toohello à l’aide de SSH :
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).
     

2. Démarrer l’interpréteur de commandes Presto hello à l’aide de hello commande suivante.
   
        presto --schema default

3. Exécutez une requête sur un exemple de table, comme **hivesampletable**, disponible sur tous les clusters HDInsight par défaut.
   
        select count (*) from hivesampletable;
   
    Par défaut, les connecteurs [Hive](https://prestodb.io/docs/current/connector/hive.html) et [TPCH](https://prestodb.io/docs/current/connector/tpch.html) pour Presto sont déjà configurés. Connecteur de la ruche étant toouse configuré hello-installation ruche par défaut, toutes les tables hello à partir de la ruche seront automatiquement visibles dans Presto.

    Pour obtenir une description détaillée de la manière d’utiliser Presto, consultez la [documentation Presto](https://prestodb.io/docs/current/index.html).

## <a name="use-airpal-with-presto"></a>Utiliser Airpal avec Presto

[Airpal](https://github.com/airbnb/airpal#airpal) est une interface de requête web open source pour Presto. Pour plus d’informations sur Airpal, consultez la [documentation Airpal](https://github.com/airbnb/airpal#airpal).

Dans cette section, nous abordons les étapes hello trop**installer Airpal sur hello edgenode** d’un cluster HDInsight Hadoop, qui possède déjà Presto installé. Cela garantit que l’interface de requête web qui Airpal hello est disponible via hello Internet.

1. À l’aide de SSH, se connecter à nœud de toohello principal du cluster HDInsight hello qui a installé appliqués aux :
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Une fois que vous êtes connecté, exécutez hello commande suivante.

        sudo slider registry  --name presto1 --getexp presto 
   
    Vous devez voir une sortie semblable à hello suivante :

        {
            "coordinator_address" : [ {
                "value" : "10.0.0.12:9090",
                "level" : "application",
                "updatedTime" : "Mon Apr 03 20:13:41 UTC 2017"
        } ]

3. À partir de la sortie de hello, notez la valeur hello hello **valeur** propriété. Vous en aurez besoin lors de l’installation Airpal sur hello cluster edgenode. À partir de la sortie de hello ci-dessus, la valeur hello dont vous avez besoin est **10.0.0.12:9090**.

4. Utiliser un modèle hello  **[ici](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)**  toocreate un HDInsight edgenode de cluster et fournir des valeurs de hello comme indiqué dans hello suivant capture d’écran.

    ![HDInsight installe Airpal sur un cluster Presto](./media/hdinsight-hadoop-install-presto/hdinsight-install-airpal.png)

5. Cliquez sur **Achat**.

6. Une fois les modifications de hello appliqué toohello configuration du cluster, vous pouvez accéder à l’interface web hello Airpal à l’aide de hello comme suit.

    a. Dans le panneau de cluster hello, cliquez sur **Applications**.

    ![HDInsight lance Airpal sur un cluster Presto](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal.png)

    b. À partir de hello **installé des applications** panneau, cliquez sur **Portal** contre airpal.

    ![HDInsight lance Airpal sur un cluster Presto](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal-1.png)

    c. Lorsque vous y êtes invité, entrez des informations d’identification d’admin hello que vous avez spécifié lors de la création du cluster HDInsight Hadoop de hello.

## <a name="customize-a-presto-installation-on-hdinsight-cluster"></a>Personnaliser une installation Presto sur un cluster HDInsight

Une fois que vous avez installé Presto sur un cluster HDInsight Hadoop, vous pouvez personnaliser hello installation toomake modifications telles que les paramètres de mémoire mise à jour, modifier les connecteurs, etc.. Hello suivant les étapes toodo donc d’effectuer.

1. À l’aide de SSH, se connecter à nœud de toohello principal du cluster HDInsight hello qui a installé appliqués aux :
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Apportez les modifications de configuration dans le fichier de hello `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`. Pour en savoir plus sur la configuration de Presto, consultez la page [Presto configuration for YARN-based clusters](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html) (Configuration de Presto pour des clusters sous Yarn).

3. Arrêter et supprimer l’instance en cours d’exécution en cours de hello de Presto.

        sudo slider stop presto1 --force
        sudo slider destroy presto1 --force

4. Démarrer une nouvelle instance de Presto avec une personnalisation hello.

       sudo slider create presto1 --template /var/lib/presto/presto-hdinsight-master/appConfig-default.json --resources /var/lib/presto/presto-hdinsight-master/resources-default.json

5. Attendez que toobe instance hello nouveau prêt et notez l’adresse du coordinateur presto.


       sudo slider registry --name presto1 --getexp presto

## <a name="generate-benchmark-data-for-hdinsight-clusters-that-run-presto"></a>Générer des données de point de référence pour les clusters HDInsight qui exécutent Presto

TPC-DS est hello standard pour mesurer les performances de hello de nombreux systèmes de prise en charge de décision, y compris les systèmes de données volumineuses. Vous pouvez utiliser appliqués aux données de toogenerate clusters HDInsight et évaluer le compare avec vos propres données de test d’évaluation de HDInsight. Vous pourrez trouver plus d’informations [ici](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).



## <a name="see-also"></a>Voir aussi
* [Installer et utiliser Hue sur les clusters HDInsight](hdinsight-hadoop-hue-linux.md). La teinte représente une interface utilisateur web qui permet de facilement toocreate, exécuter et enregistrer des travaux Pig et Hive, également en tant que parcourir du stockage par défaut pour votre cluster HDInsight hello.

* [Installation de Giraph sur des clusters HDInsight](hdinsight-hadoop-giraph-install-linux.md). Utilisez tooinstall de personnalisation de cluster que giraph sur HDInsight Hadoop de clusters. Giraph vous permet de graphique tooperform traitement à l’aide de Hadoop et peut être utilisé avec Azure HDInsight.

* [Installation de Solr sur des clusters HDInsight](hdinsight-hadoop-solr-install-linux.md). Utilisez tooinstall de personnalisation de cluster que solr sur HDInsight Hadoop de clusters. Solr vous permet de tooperform les opérations de recherche puissante sur les données stockées.

[hdinsight-install-r]: hdinsight-hadoop-r-scripts-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
