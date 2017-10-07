---
title: "aaaManage des clusters de Hadoop basé sur Windows à l’aide de HDInsight hello portail Azure | Documents Microsoft"
description: "Découvrez comment tooadminister HDInsight Service. Créer un cluster HDInsight, console JavaScript interactive de hello ouvert et la console de commande Hadoop hello ouvert."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 9295a988-bd88-453a-8c8b-55fa103bf39c
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: a237726b0e37a08005ce22e96581739e93edb050
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-windows-based-hadoop-clusters-in-hdinsight-by-using-hello-azure-portal"></a>Gérer les clusters HDInsight Hadoop basé sur Windows à l’aide de hello portail Azure

À l’aide de hello [portail Azure][azure-portal], vous pouvez créer des clusters de Hadoop basé sur Windows dans Azure HDInsight, modifiez le mot de passe utilisateur Hadoop et activer le protocole RDP (Remote Desktop) et le rendre accessible hello Hadoop console de commande sur le cluster de hello.

informations Hello dans cet article s’applique uniquement à basée sur les tooWindow des clusters HDInsight. Pour plus d’informations sur la gestion des clusters basés sur Linux, consultez [Hadoop de gérer les clusters dans HDInsight à l’aide de hello Azure portal](hdinsight-administer-use-portal-linux.md).

> [!IMPORTANT]
> Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).


## <a name="prerequisites"></a>Composants requis

Avant de commencer cet article, vous devez disposer de hello :

* **Un abonnement Azure**. Consultez la rubrique [Obtenir une version d'évaluation gratuite d'Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Compte de stockage Azure** -HDInsight un cluster utilise un conteneur de stockage d’objets Blob Azure en tant que système de fichiers par défaut hello. Pour plus d’informations sur l’expérience transparente offerte par le stockage d’objets blob Azure avec les clusters HDInsight, consultez la rubrique [Utilisation du stockage d’objets blob Azure avec HDInsight](hdinsight-hadoop-use-blob-storage.md). Pour plus d’informations sur la création d’un compte de stockage Azure, consultez [comment tooCreate un compte de stockage](../storage/common/storage-create-storage-account.md).

## <a name="open-hello-portal"></a>Ouvrez hello portail
1. Connectez-vous trop[https://portal.azure.com](https://portal.azure.com).
2. Une fois que vous ouvrez hello portail, vous pouvez :

   * Cliquez sur **nouveau** à partir de hello menu gauche toocreate un nouveau cluster :

       ![bouton nouveau cluster HDInsight](./media/hdinsight-administer-use-management-portal/azure-portal-new-button.png)
   * Cliquez sur **Clusters HDInsight** à partir du menu de gauche hello.

       ![bouton de cluster HDinsight du portail Azure](./media/hdinsight-administer-use-management-portal/azure-portal-hdinsight-button.png)

     Si **HDInsight** ne s’affichent dans le menu de gauche hello, cliquez sur **Parcourir**.

     ![bouton de cluster Parcourir du portail Azure](./media/hdinsight-administer-use-management-portal/azure-portal-browse-button.png)

## <a name="create-clusters"></a>Créer des clusters
Pour des instructions de création de hello à l’aide de hello portail, consultez [HDInsight de créer des clusters](hdinsight-hadoop-provision-linux-clusters.md).

HDInsight fonctionne avec un large éventail de composants Hadoop. Pour hello la liste des composants hello qui ont été vérifiés et pris en charge, consultez [quelle version de Hadoop est dans Azure HDInsight](hdinsight-component-versioning.md). Vous pouvez personnaliser HDInsight à l’aide d’une des options suivantes de hello :

* Utilisez Action de Script toorun des scripts personnalisés qui peuvent personnaliser un cluster de tooeither modifier la configuration de cluster ou installer des composants personnalisés tels que Giraph ou Solr. Pour plus d’informations, consultez la page [Personnalisation d’un cluster HDInsight à l’aide d’une d’action de script](hdinsight-hadoop-customize-cluster.md).
* Utiliser des paramètres de personnalisation de cluster hello dans hello Kit de développement logiciel HDInsight .NET ou Azure PowerShell lors de la création du cluster. Ces modifications de configuration sont conservées puis via la durée de vie hello du cluster de hello et ne sont pas affectées par reimages de nœud de cluster qui exécute périodiquement une plateforme Azure pour la maintenance. Pour plus d’informations sur l’utilisation de paramètres de personnalisation de cluster hello, consultez [HDInsight de créer des clusters](hdinsight-hadoop-provision-linux-clusters.md).
* Certains composants Java natifs, telles que Mahout et en cascade, peuvent être exécutés sur le cluster de hello en tant que fichiers JAR. Ces fichiers JAR peuvent être distribuée tooAzure stockage d’objets Blob et soumis tooHDInsight clusters via des mécanismes de soumission de travail Hadoop. Pour plus d’informations, consultez la rubrique [Envoi de tâches Hadoop par programme](hdinsight-submit-hadoop-jobs-programmatically.md).

  > [!NOTE]
  > Si vous rencontrez des problèmes de déploiement de clusters de tooHDInsight fichiers JAR ou appeler des fichiers JAR sur les clusters HDInsight, contactez [Support technique de Microsoft](https://azure.microsoft.com/support/options/).
  >
  > Cascading n'est pas pris en charge par HDInsight et ne peut pas bénéficier du support Microsoft. Pour les listes de composants pris en charge, consultez [quelles sont les nouveautés dans les versions de cluster hello fournies par HDInsight](hdinsight-component-versioning.md).
  >
  >

Installation de logiciels personnalisés sur le cluster hello à l’aide de connexion Bureau à distance n’est pas prise en charge. Évitez de stocker des fichiers sur des lecteurs hello de nœud principal de hello, car elles seront perdues si vous avez besoin de toore-créer des clusters de hello. Il est recommandé de stocker les fichiers sur le stockage d’objets blob Azure. Le stockage d'objets blob est permanent.

## <a name="list-and-show-clusters"></a>Énumération et affichage des clusters
1. Connectez-vous trop[https://portal.azure.com](https://portal.azure.com).
2. Cliquez sur **Clusters HDInsight** à partir du menu de gauche hello.
3. Cliquez sur le nom du cluster hello. Si la liste de cluster hello est longue, vous pouvez utiliser le filtre en haut de hello de page de hello.
4. Double-cliquez sur un cluster à partir des détails de hello liste tooshow hello.

    **Menu et essentials**:

    ![essentials du cluster HDInsight du portail Azure](./media/hdinsight-administer-use-management-portal/hdinsight-essentials.png)

   * menu de hello toocustomize, avec le bouton droit n’importe où sur le menu de hello, puis cliquez sur **personnaliser**.
   * **Paramètres** et **tous les paramètres**: hello d’affiche **paramètres** panneau pour le cluster hello, qui vous permet de tooaccess configuration des informations détaillées sur le cluster de hello.
   * **Tableau de bord**, **tableau de bord de Cluster** et **URL : il s’agit de toutes les méthodes tooaccess hello cluster tableau de bord, qui est Ambari Web pour les clusters basés sur Linux. -**Shell sécurisé ** : Affiche le cluster de toohello hello instructions tooconnect à l’aide de la connexion de Secure Shell (SSH).
   * **L’échelle du Cluster**: vous permet de nombre de hello toochange de nœuds de travail pour ce cluster.
   * **Supprimer**: cluster hello de suppressions.
   * **Démarrage rapide** : affiche des informations qui vous aideront à prendre en main HDInsight.
   * ** Utilisateurs : Vous permet d’autorisations tooset *portail administration* de ce cluster pour d’autres utilisateurs sur votre abonnement Azure.

     > [!IMPORTANT]
     > Cela *uniquement* affecte les autorisations d’accès et cluster toothis Bonjour portail Azure, et n’a aucun effet sur qui peut se connecter le cluster HDInsight toohello tooor envoyer les travaux.
     >
     >
   * **Balises**: balises autoriser vous tooset clé/valeur paires toodefine une classification personnalisée de vos services cloud. Vous pouvez par exemple créer une clé nommée **projet**, puis utiliser une valeur commune pour tous les services associés à un projet spécifique.
   * **Vues de Ambari**: tooAmbari Web est liée.

     > [!IMPORTANT]
     > services de hello toomanage fournie par hello cluster HDInsight, vous devez utiliser Ambari Web hello Ambari REST API. Pour plus d’informations sur l’utilisation d’Ambari, consultez [Gestion des clusters HDInsight à l’aide d’Ambari](hdinsight-hadoop-manage-ambari.md).
     >
     >

     **Utilisation**:

     ![utilisation de cluster HDInsight du portail Azure](./media/hdinsight-administer-use-management-portal/hdinsight-portal-cluster-usage.png)
5. Cliquez sur **Settings**.

    ![utilisation de cluster HDInsight du portail Azure](./media/hdinsight-administer-use-management-portal/hdinsight.portal.cluster.settings.png)

   * **Propriétés**: afficher les propriétés du cluster hello.
   * **Identité AAS de cluster**:
   * **Les clés de stockage Azure**: afficher le compte de stockage par défaut hello et sa clé. compte de stockage Hello est configuration pendant le processus de création de cluster hello.
   * **Connexion de cluster**: modifier le nom d’utilisateur hello cluster HTTP et le mot de passe.
   * **Magasin de métadonnées externe**: afficher les magasins de métadonnées Hive et Oozie hello. magasin de métadonnées Hello peut être configuré uniquement pendant le processus de création de cluster hello.
   * **L’échelle du Cluster**: augmentation et diminution hello le nombre de nœuds worker du cluster.
   * **Bureau à distance**: activer et désactiver l’accès Bureau à distance (RDP) et configurer le nom d’utilisateur de hello RDP.  nom d’utilisateur RDP Hello doit être différent du nom d’utilisateur hello HTTP.
   * **Partenaire d’enregistrement**:

     > [!NOTE]
     > Ceci est une liste générique des paramètres disponibles. Ils ne sont pas tous présents pour tous les types de clusters.
     >
     >
6. Cliquez sur **Propriétés**:

    section des propriétés Hello indique hello qui suit :

   * **Nom d’hôte**: nom du Cluster.
   * **URL de cluster**.
   * **État**: inclut Abandonné, Accepté, ClusterStorageProvisioned, AzureVMConfiguration, HDInsightConfiguration, En fonctionnement, En cours d’exécution, Erreur, En cours de suppression, Supprimé, TimedOut, DeleteQueued, DeleteTimedOut, DeleteError, PatchQueued, CertRolloverQueued, ResizeQueued, ClusterCustomization
   * **Région**: emplacement Azure. Pour obtenir la liste des emplacements Azure pris en charge, consultez hello **région** zone de liste déroulante sur [tarification HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).
   * **Données créées**.
   * **Système d’exploitation** : **Windows** ou **Linux**.
   * **Type**: Hadoop, Hbase, Storm, Spark.
   * **Version**. Voir [Versions HDInsight](hdinsight-component-versioning.md)
   * **Abonnement**: nom de l’abonnement.
   * **ID d’abonnement**.
   * **Source de données principale**. compte de stockage Blob Azure Hello utilisé en tant que système de fichiers Hadoop hello par défaut.
   * **Niveau de tarification des nœuds de travail**.
   * **Niveau de tarification du nœud principal**.

## <a name="delete-clusters"></a>Suppression des clusters
Supprimer un cluster ne supprime pas le compte de stockage par défaut hello ou des comptes de stockage. Vous pouvez recréer les cluster hello à l’aide de hello les mêmes comptes de stockage et hello même magasin de métadonnées.

1. Connectez-vous à toohello [Portal][azure-portal].
2. Cliquez sur **parcourir tous les** à partir du menu de gauche hello, cliquez sur **Clusters HDInsight**, cliquez sur le nom de votre cluster.
3. Cliquez sur **supprimer** du menu du haut hello, puis suivez les instructions hello.

Voir aussi [Pause/arrêt de clusters](#pauseshut-down-clusters).

## <a name="scale-clusters"></a>Mise à l’échelle des clusters
cluster Hello fonctionnalité de mise à l’échelle permet un nombre de hello toochange de nœuds de travail utilisé par un cluster qui s’exécute dans Azure HDInsight sans avoir toore-créer le cluster de hello.

> [!NOTE]
> Seuls les clusters ayant la version 3.1.3 de HDInsight ou une version ultérieure sont pris en charge. Si vous ne savez pas de version hello de votre cluster, vous pouvez vérifier la page de propriétés hello.  Voir [Énumération et affichage des clusters](#list-and-show-clusters).
>
>

impact Hello modifiant nombre hello de nœuds de données pour chaque type de cluster pris en charge par HDInsight :

* Hadoop

    Vous pouvez augmenter de façon transparente nombre hello de nœuds de travail dans un cluster Hadoop qui est en cours d’exécution sans impact sur toutes les tâches en attente ou en cours d’exécution. Nouvelles tâches peuvent également être soumises pendant que l’opération de hello est en cours. Échecs dans une opération de mise à l’échelle sont correctement gérés afin que hello cluster est toujours conservé dans un état fonctionnel.

    Lorsqu’un cluster Hadoop est réduite en réduisant le nombre de hello de nœuds de données, certains services hello dans un cluster de hello sont redémarrés. Ainsi, en cours d’exécution et en attente de toofail de travaux à l’achèvement de hello Hello opération de mise à l’échelle. Vous pouvez, toutefois, renvoyer des tâches de hello une fois l’opération hello est terminée.
* HBase

    Vous pouvez accéder en toute transparence ajouter ou supprimer le cluster de nœuds tooyour HBase pendant son exécution. Serveurs régionaux sont équilibrés automatiquement après quelques minutes d’achèvement hello opération de mise à l’échelle. Toutefois, vous pouvez équilibrer manuellement les serveurs régionaux hello en vous connectant à un nœud principal de hello du cluster et hello en cours d’exécution suivant des commandes dans une fenêtre d’invite de commandes :

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer

    Pour plus d’informations sur l’utilisation du shell HBase de hello, consultez]
* Storm

    Vous pouvez accéder en toute transparence ajouter ou supprimer le cluster de données nœuds tooyour Storm pendant son exécution. Mais après la réussite de l’opération de mise à l’échelle de hello, vous devrez topologie de hello toorebalance.

    Cela peut se faire de deux façons à l’aide de :

  * l'interface utilisateur Web de Storm
  * l’outil d’interface de ligne de commande (CLI)

    Reportez-vous toohello [documentation d’Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) pour plus d’informations.

    interface utilisateur web de Storm Hello est disponible sur le cluster HDInsight de hello :

    ![HDInsight storm mise à l’échelle rééquilibrage](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)

    Voici un exemple comment toouse hello CLI commande topologie de Storm toorebalance hello :

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

**clusters tooscale**

1. Connectez-vous à toohello [Portal][azure-portal].
2. Cliquez sur **parcourir tous les** à partir du menu de gauche hello, cliquez sur **Clusters HDInsight**, cliquez sur le nom de votre cluster.
3. Cliquez sur **paramètres** dans le menu du haut hello, puis cliquez sur **échelle Cluster**.
4. Entrez une valeur dans le champ **Nombre de nœuds de travail**. Hello hello nombre limite de nœud de cluster varie selon les abonnements Azure. Vous pouvez contacter facturation limite de hello tooincrease prise en charge.  informations sur les coûts Hello reflétera hello apportées nombre toohello de nœuds.

    ![HDInsight Hadoop HBase Storm Spark mise à l’échelle](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

## <a name="pauseshut-down-clusters"></a>Pause/arrêt de clusters
La plupart des travaux Hadoop sont les traitements par lots exécutés occasionnellement seulement. Pour la plupart des clusters Hadoop, il existe de grandes périodes de temps que le cluster hello n’est pas utilisé pour le traitement. Avec HDInsight, vos données sont stockées Azure Storage, pour que vous puissiez supprimer un cluster en toute sécurité s’il n’est pas en cours d’utilisation.
Vous devez également payer pour un cluster HDInsight, même lorsque vous ne l’utilisez pas. Étant donné que les frais de hello pour le cluster de hello sont autant de fois plus de frais hello pour le stockage, il est judicieux économique toodelete clusters lorsqu’ils ne sont pas en cours d’utilisation.

Il existe de nombreuses façons, vous pouvez programmer hello :

* Utilisateur d’Azure Data Factory. Voir [Service lié Azure HDInsight](../data-factory/data-factory-compute-linked-services.md) et [Transformation et analyse en utilisant Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md) pour les services liés HDInsight à la demande et auto-définis.
* Utilisation d’Azure PowerShell  Voir [Analyse des données sur les retards de vol](hdinsight-analyze-flight-delay-data.md).
* Utiliser l’interface de ligne de commande Microsoft Azure Voir [Gestion des clusters HDInsight à l’aide de l’interface de ligne de commande Azure](hdinsight-administer-use-command-line.md).
* Utilisation du kit de développement logiciel .NET. Voir [Envoyer des tâches Hadoop](hdinsight-submit-hadoop-jobs-programmatically.md).

Pourquoi les informations de tarification, consultez [tarification HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/). toodelete un cluster à partir de hello portail, consultez [supprimer des clusters](#delete-clusters)

## <a name="change-cluster-username"></a>Modifier le nom d’utilisateur du cluster
Un cluster HDInsight peut disposer de deux comptes d'utilisateur. Hello compte utilisateur de cluster HDInsight est créé au cours du processus de création de hello. Vous pouvez également créer un compte d’utilisateur RDP pour accéder au cluster hello via RDP. Consultez la rubrique [Activation du Bureau à distance](#connect-to-hdinsight-clusters-by-using-rdp).

**mot de passe et le nom d’utilisateur cluster toochange hello HDInsight**

1. Connectez-vous à toohello [Portal][azure-portal].
2. Cliquez sur **parcourir tous les** à partir du menu de gauche hello, cliquez sur **Clusters HDInsight**, cliquez sur le nom de votre cluster.
3. Cliquez sur **paramètres** dans le menu du haut hello, puis cliquez sur **au Cluster**.
4. Si **au Cluster** a été activé, vous devez cliquer sur **désactiver**, puis cliquez sur **activer** que vous puissiez modifier le nom d’utilisateur hello et le mot de passe...
5. Hello de modification **nom de connexion de Cluster** et/ou hello **mot de passe de connexion Cluster**, puis cliquez sur **enregistrer**.

    ![HDInsight modifier cluster utilisateur nom d’utilisateur mot de passe utilisateur http](./media/hdinsight-administer-use-management-portal/hdinsight.portal.change.username.password.png)

## <a name="grantrevoke-access"></a>Octroyer/Révoquer l’accès
Clusters HDInsight ont hello suivant (tous ces services ont des points de terminaison RESTful) des services web HTTP :

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

Par défaut, l'accès à ces services est octroyé. Vous pouvez revoke ou octroyer l’accès de hello de hello portail Azure.

> [!NOTE]
> Par attribution/révocation de l’accès hello, vous allez réinitialiser le mot de passe et le nom d’utilisateur de cluster de hello.
>
>

**accès de services web toogrant/revoke HTTP**

1. Connectez-vous à toohello [Portal][azure-portal].
2. Cliquez sur **parcourir tous les** à partir du menu de gauche hello, cliquez sur **Clusters HDInsight**, cliquez sur le nom de votre cluster.
3. Cliquez sur **paramètres** dans le menu du haut hello, puis cliquez sur **au Cluster**.
4. Si **au Cluster** a été activé, vous devez cliquer sur **désactiver**, puis cliquez sur **activer** que vous puissiez modifier le nom d’utilisateur hello et le mot de passe...
5. Pour **nom d’utilisateur Cluster** et **mot de passe de connexion Cluster**, entrez de nouveau nom d’utilisateur hello et le mot de passe (respectivement) pour le cluster de hello.
6. Cliquez sur **ENREGISTRER**.

    ![HDInsight octroi suppression accès au service web http](./media/hdinsight-administer-use-management-portal/hdinsight.portal.change.username.password.png)

## <a name="find-hello-default-storage-account"></a>Recherchez le compte de stockage par défaut hello
Chaque cluster HDInsight dispose d’un compte de stockage par défaut. Hello compte de stockage par défaut et ses clés pour un cluster apparaît sous **paramètres**/**propriétés**/**clés de stockage Azure**. Voir [Énumération et affichage des clusters](#list-and-show-clusters).

## <a name="find-hello-resource-group"></a>Recherchez le groupe de ressources hello
En mode de gestionnaire de ressources Azure hello, chaque cluster HDInsight est créé avec un groupe de ressources Azure. groupe de ressources Azure Hello un cluster appartenant tooappears dans :

* liste de cluster Hello a un **groupe de ressources** colonne.
* Mosaïque **Essential** du cluster.  

Voir [Énumération et affichage des clusters](#list-and-show-clusters).

## <a name="open-hdinsight-query-console"></a>Ouvrir la console de requête HDInsight
Hello console de requête de HDInsight inclut hello suivant de fonctionnalités :

* **Éditeur Hive**: interface web GUI pour l’envoi de tâches Hive.  Consultez [exécuter la ruche de requêtes à l’aide de hello Console de requête](hdinsight-hadoop-use-hive-query-console.md).

    ![éditeur hive de portail HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight-hive-editor.png)
* **Historique des tâches**: surveillez les tâches Hadoop.  

    ![historique de travail de portail HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight-job-history.png)

    Cliquez sur **nom de la requête** tooshow détails de hello, y compris les propriétés du travail, **requête de travail**, et ** sortie des tâches. Vous pouvez également télécharger des requêtes de hello et hello sortie tooyour station de travail.
* **Explorateur de fichiers**: recherchez le compte de stockage par défaut hello et hello des comptes de stockage lié.

    ![parcourir l’explorateur de fichier de portail HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight-file-browser.png)

    Sur la capture d’écran de hello, hello  **<Account>**  type indique l’élément de hello est un compte de stockage Azure.  Cliquez sur les fichiers hello toobrowse hello compte nom.
* **Interface utilisateur Hadoop**.

    ![Interface utilisateur Hadoop du portail HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight-hadoop-ui.png)

    À partir de **Interface utilisateur Hadoop*, vous pouvez parcourir les fichiers et consulter les journaux.
* **Interface utilisateur Yarn**.

    ![Interface utilisateur YARN du portail HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight-yarn-ui.png)

## <a name="run-hive-queries"></a>Exécuter des requêtes Hive
travaux de ruche tooran à partir de hello portail, cliquez sur **éditeur Hive** Bonjour HDInsight requête de la console. Voir [Ouvrir la console de requête HDInsight](#open-hdinsight-query-console).

## <a name="monitor-jobs"></a>Surveiller des travaux
travaux toomonitor de hello portail, cliquez sur **l’historique des travaux** Bonjour HDInsight requête de la console. Voir [Ouvrir la console de requête HDInsight](#open-hdinsight-query-console).

## <a name="browse-files"></a>Parcourir les fichiers
toobrowse fichiers stockés dans le compte de stockage par défaut hello et hello des comptes de stockage lié, cliquez sur **Explorateur** Bonjour HDInsight requête de la console. Voir [Ouvrir la console de requête HDInsight](#open-hdinsight-query-console).

Vous pouvez également utiliser hello **parcourir le système de fichiers hello** utilitaire hello **Hadoop UI** dans la console hello HDInsight.  Voir [Ouvrir la console de requête HDInsight](#open-hdinsight-query-console).

## <a name="monitor-cluster-usage"></a>Surveiller l’utilisation du cluster
Hello **utilisation** section du Panneau de cluster HDInsight hello affiche des informations sur le nombre hello d’abonnement disponibles tooyour de cœurs pour une utilisation avec HDInsight, ainsi que nombre de hello de cœurs toothis cluster et comment elles sont allouées alloué pour les nœuds hello dans ce cluster. Voir [Énumération et affichage des clusters](#list-and-show-clusters).

> [!IMPORTANT]
> services de hello toomonitor fournie par hello cluster HDInsight, vous devez utiliser Ambari Web hello Ambari REST API. Pour plus d’informations sur l’utilisation d’Ambari, voir [Gestion des clusters HDInsight à l’aide d’Ambari](hdinsight-hadoop-manage-ambari.md)
>
>

## <a name="open-hadoop-ui"></a>Ouvrez l’interface utilisateur Hadoop
cluster de hello toomonitor, système de fichiers Parcourir hello et vérifiez les journaux, cliquez sur **Hadoop UI** Bonjour HDInsight requête de la console. Voir [Ouvrir la console de requête HDInsight](#open-hdinsight-query-console).

## <a name="open-yarn-ui"></a>Ouvrez l’interface utilisateur Yarn
toouse interface utilisateur de fils, cliquez sur **fils UI** Bonjour HDInsight requête de la console. Voir [Ouvrir la console de requête HDInsight](#open-hdinsight-query-console).

## <a name="connect-tooclusters-using-rdp"></a>Se connecter à l’aide du protocole RDP de tooclusters
informations d’identification Hello pour cluster hello que vous avez fourni lors de sa création donnent accès à des services de toohello sur le cluster de hello, mais pas toohello cluster via Bureau à distance. Vous pouvez activer l’accès Bureau à distance lorsque vous approvisionnez un cluster ou une fois l’approvisionnement effectué. Pour obtenir des instructions sur l’activation du Bureau à distance lors de la création hello, consultez [cluster HDInsight de créer](hdinsight-hadoop-provision-linux-clusters.md).

**tooenable Bureau à distance**

1. Connectez-vous à toohello [Portal][azure-portal].
2. Cliquez sur **parcourir tous les** à partir du menu de gauche hello, cliquez sur **Clusters HDInsight**, cliquez sur le nom de votre cluster.
3. Cliquez sur **paramètres** dans le menu du haut hello, puis cliquez sur **Bureau à distance**.
4. Renseignez les champs **Expiration**, **Nom d’utilisateur de bureau à distance** et **Mot de passe de bureau à distance**, puis cliquez sur **Activer**.

    ![HDInsight activer désactiver configurer Bureau à distance](./media/hdinsight-administer-use-management-portal/hdinsight.portal.remote.desktop.png)

    valeurs par défaut de Hello pour l’expiration est une semaine.

   > [!NOTE]
   > Vous pouvez également utiliser hello HDInsight .NET SDK tooenable Bureau à distance sur un cluster. Hello d’utilisation **EnableRdp** méthode sur l’objet de client HDInsight hello Bonjour suivant manière : **client. EnableRdp (clustername, emplacement, « rdpuser », « rdppassword », DateTime.Now.AddDays(6))**. De même, de le toodisable Bureau à distance sur le cluster de hello, vous pouvez utiliser **client. DisableRdp (clustername, emplacement)**. Pour plus d’informations sur ces méthodes, consultez la rubrique [Référence du Kit de développement logiciel (SDK) HDInsight .NET](http://go.microsoft.com/fwlink/?LinkId=529017). Cela s’applique uniquement aux clusters HDInsight fonctionnant sous Windows.
   >
   >

**cluster de tooa tooconnect au moyen de RDP**

1. Connectez-vous à toohello [Portal][azure-portal].
2. Cliquez sur **parcourir tous les** à partir du menu de gauche hello, cliquez sur **Clusters HDInsight**, cliquez sur le nom de votre cluster.
3. Cliquez sur **paramètres** dans le menu du haut hello, puis cliquez sur **Bureau à distance**.
4. Cliquez sur **Connect** et suivez les instructions de hello. Si la connexion est désactivée, vous devez d’abord l’activer. Veillez à l’aide du mot de passe et le nom d’utilisateur du Bureau à distance hello.  Vous ne pouvez pas utiliser les informations d’identification d’utilisateur de Cluster hello.

## <a name="open-hadoop-command-line"></a>Ouverture de la ligne de commande Hadoop
cluster de toohello tooconnect à l’aide de bureau à distance et la ligne de commande Hadoop utilisez hello, vous devez tout d’abord avoir activé le cluster de toohello d’accès Bureau à distance comme décrit dans la section précédente de hello.

**tooopen une ligne de commande Hadoop**

1. Connectez le cluster toohello à l’aide du Bureau à distance.
2. À partir du bureau de hello, double-cliquez sur **ligne de commande Hadoop**.

    ![HDI.HadoopCommandLine][image-hadoopcommandline]

    Pour plus d’informations sur les commandes Hadoop, consultez la rubrique [Référence aux commandes Hadoop](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-common/CommandsManual.html).

Dans la capture d’écran précédente hello, nom du dossier hello a numéro de version de Hadoop hello incorporé. numéro de version Hello peuvent choisir de hello en fonction des modifications des composants de Hadoop hello installé sur le cluster de hello. Vous pouvez utiliser les dossiers toothose toorefer Hadoop environnement variables. Par exemple :

    cd %hadoop_home%
    cd %hive_home%
    cd %hbase_home%
    cd %pig_home%
    cd %sqoop_home%
    cd %hcatalog_home%

## <a name="next-steps"></a>Étapes suivantes
Dans cet article, vous avez appris comment toocreate un cluster HDInsight à l’aide de hello Portal, et comment tooopen hello outil de ligne de commande Hadoop. toolearn, voir hello suivant des articles :

* [Administration de HDInsight à l’aide d’Azure PowerShell](hdinsight-administer-use-powershell.md)
* [Administration de HDInsight à l’aide de l’interface de ligne de commande Azure](hdinsight-administer-use-command-line.md)
* [Création de clusters HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
* [Envoi de tâches Hadoop par programme](hdinsight-submit-hadoop-jobs-programmatically.md)
* [Prise en main d’Azure HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Version de Hadoop dans Azure HDInsight](hdinsight-component-versioning.md)

[azure-portal]: https://portal.azure.com
[image-hadoopcommandline]: ./media/hdinsight-administer-use-management-portal/hdinsight-hadoop-command-line.png "Ligne de commande Hadoop"
