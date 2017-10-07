---
title: "les clusters aaaManage Hadoop dans HDInsight à l’aide du portail Azure | Documents Microsoft"
description: "Découvrez comment toocreate et gérer des clusters HDInsight à l’aide de hello portail Azure."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5a76f897-02e8-4437-8f2b-4fb12225854a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: jgao
ms.openlocfilehash: c242d43d4ccea7cf1e7be19c3f3d7ed3c4f50918
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-hello-azure-portal"></a>Gérer les clusters Hadoop dans HDInsight à l’aide de hello portail Azure
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

À l’aide de hello [portail Azure][azure-portal], vous pouvez gérer les clusters Hadoop dans HDInsight de Azure. Utilisez le sélecteur de tabulation hello pour plus d’informations sur la gestion des clusters Hadoop dans HDInsight à l’aide d’autres outils.

**Configuration requise**

Avant de commencer cet article, vous devez disposer de hello éléments suivants :

* **Un abonnement Azure**. Consultez la rubrique [Obtenir une version d'évaluation gratuite d'Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

## <a name="open-hello-portal"></a>Portail de hello ouvert
1. Connectez-vous trop[https://portal.azure.com](https://portal.azure.com).
2. Une fois que vous ouvrez hello portail, vous pouvez :

   * Cliquez sur **nouveau** à partir de hello menu gauche toocreate un nouveau cluster :

       ![bouton nouveau cluster HDInsight](./media/hdinsight-administer-use-portal-linux/azure-portal-new-button.png)
   * Cliquez sur **Clusters HDInsight** de hello toolist de menu de gauche hello clusters existants

       ![bouton de cluster HDinsight du portail Azure](./media/hdinsight-administer-use-portal-linux/azure-portal-hdinsight-button.png)

       Si vous ne voyez pas de cluster HDInsight, cliquez sur **davantage de services** sur hello en bas de la liste de hello, puis cliquez sur **clusters HDInsight** sous hello **Intelligence + Analytique** section.


## <a name="create-clusters"></a>Créer des clusters
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

HDInsight fonctionne avec un large éventail de composants Hadoop. Pour hello la liste des composants hello qui ont été vérifiés et pris en charge, consultez [quelle version de Hadoop est dans Azure HDInsight](hdinsight-component-versioning.md). Pour des informations sur la création du cluster général hello, consultez [Hadoop de créer des clusters dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

### <a name="access-control-requirements"></a>Exigences de contrôle d’accès

Vous devez spécifier un abonnement Azure lorsque vous créez un cluster HDInsight. Ce cluster peut être créé dans un groupe de ressources Azure ou un groupe de ressources existant. Vous pouvez utiliser hello suivant les étapes tooverify vos autorisations pour créer des clusters HDInsight :

- toouse un groupe de ressources existant.

    1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
    2. Cliquez sur **groupes de ressources** hello menu gauche toolist hello groupes de ressources.
    3. Cliquez sur le groupe de ressources hello toouse souhaité pour la création de votre cluster HDInsight.
    4. Cliquez sur **(IAM) de contrôle d’accès**et vérifiez que vous (ou un groupe auquel vous appartenez) ont au moins hello groupe de ressources de collaborateur accès toohello.

- toocreate un groupe de ressources

    1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
    2. Cliquez sur **abonnement** à partir du menu de gauche hello. Il présente une icône en forme de clé jaune. Vous devriez voir une liste d’abonnements.
    3. Cliquez sur abonnement hello que vous utilisez des clusters de toocreate. 
    4. Cliquez sur **Mes autorisations**.  Il montre votre [rôle](../active-directory/role-based-access-control-what-is.md#built-in-roles) lors de l’abonnement de hello. Vous devez avoir au moins cluster HDInsight de collaborateur accès toocreate.

Si vous recevez l’erreur de NoRegisteredProviderFound hello ou hello MissingSubscriptionRegistration, consultez [résoudre les erreurs courantes de déploiement Azure avec Azure Resource Manager](../azure-resource-manager/resource-manager-common-deployment-errors.md).

## <a name="list-and-show-clusters"></a>Énumération et affichage des clusters
1. Connectez-vous trop[https://portal.azure.com](https://portal.azure.com).
2. Cliquez sur **Clusters HDInsight** de hello toolist de menu de gauche hello clusters existants.
3. Cliquez sur le nom du cluster hello. Si la liste de cluster hello est longue, vous pouvez utiliser le filtre en haut de hello de page de hello.
4. Cliquez sur un cluster à partir de la page Vue d’ensemble de hello liste toosee hello :

    ![essentials du cluster HDInsight du portail Azure](./media/hdinsight-administer-use-portal-linux/hdinsight-essentials.png)

    * **Tableau de bord**: ouvre hello cluster tableau de bord, qui est Ambari Web pour les clusters basés sur Linux.
    * **Secure Shell**: cluster affiche hello instructions tooconnect toohello à l’aide de la connexion de Secure Shell (SSH).
    * **L’échelle du Cluster**: vous permet de nombre de hello toochange de nœuds de travail pour ce cluster.
    * **Supprimer**: cluster hello de suppressions.
    * **Journaux d’activité** : affiche et interroge les journaux d’activité.
    * **Contrôle d’accès (IAM)** : utilise les attributions de rôle.  Consultez [utiliser les ressources de rôle affectations toomanage accès tooyour abonnement Azure](../active-directory/role-based-access-control-configure.md).
    * **Balises**: permet de vous tooset clé/valeur paires toodefine une classification personnalisée de vos services cloud. Vous pouvez par exemple créer une clé nommée **projet**, puis utiliser une valeur commune pour tous les services associés à un projet spécifique.
    * **Diagnostiquer et résoudre les problèmes** : affiche les informations de dépannage.
    * **Verrouille**: ajouter le verrou tooprevent hello cluster est modifié ou supprimé.
    * **Script d’automatisation**: modèle d’Azure Resource Manager hello affichage et d’exportation pour le cluster de hello. Actuellement, vous pouvez uniquement exporter compte de stockage Azure dépendants hello. Consultez [Création de clusters Hadoop basés sur Linux dans HDInsight à l’aide de modèles Azure Resource Manager](hdinsight-hadoop-create-linux-clusters-arm-templates.md).
    * **Démarrage rapide** : affiche des informations qui vous aident à prendre en main HDInsight.
    * **Outils pour HDInsight** : informations d’aide pour les outils associés à HDInsight.
    * **Connexion de cluster**: afficher les informations de connexion de cluster hello.
    * **L’utilisation des cœurs abonnement**: affichage hello cœurs utilisées et disponibles pour votre abonnement.
    * **L’échelle du Cluster**: augmentation et diminution hello le nombre de nœuds worker du cluster. Consultez [Mettre à l’échelle des clusters](hdinsight-administer-use-management-portal.md#scale-clusters).
    * **Secure Shell**: cluster affiche hello instructions tooconnect toohello à l’aide de la connexion de Secure Shell (SSH). Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).
    * **Partenaire HDInsight**: Ajout/Suppression de hello partenaire HDInsight actuel.
    * **Magasin de métadonnées externe**: afficher les magasins de métadonnées Hive et Oozie hello. magasin de métadonnées Hello peut être configuré uniquement pendant le processus de création de cluster hello. Consultez [Utiliser un metastore Hive/Oozie](hdinsight-hadoop-provision-linux-clusters.md#use-hiveoozie-metastore).
    * **Actions de script**: exécutez Bash des scripts sur le cluster de hello. Consultez [Personnalisation de clusters HDInsight basés sur Linux à l’aide d’une action de script](hdinsight-hadoop-customize-cluster-linux.md).
    * **Applications** : permet d’ajouter/supprimer des applications HDInsight.  Consultez [Installer des applications HDInsight personnalisées](hdinsight-apps-install-custom-applications.md).
    * **Propriétés**: afficher les propriétés du cluster hello.
    * **Comptes de stockage**: afficher les comptes de stockage hello et les clés de hello. comptes de stockage Hello sont configurés au cours du processus de création de cluster hello.
    * **Identité AAS de cluster**:
    * **Nouvelle demande de support**: vous permet de toocreate un ticket de support avec prise en charge de Microsoft.
    
6. Cliquez sur **Propriétés**:

    propriétés de Hello sont :

   * **Nom d’hôte**: nom du Cluster.
   * **URL de cluster**. URL de Hello pour l’interface hello Ambari web.
   * **État**: inclut Abandonné, Accepté, ClusterStorageProvisioned, AzureVMConfiguration, HDInsightConfiguration, En fonctionnement, En cours d’exécution, Erreur, En cours de suppression, Supprimé, TimedOut, DeleteQueued, DeleteTimedOut, DeleteError, PatchQueued, CertRolloverQueued, ResizeQueued, ClusterCustomization
   * **Région**: emplacement Azure. Pour obtenir la liste des emplacements Azure pris en charge, consultez hello **région** zone de liste déroulante sur [tarification HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).
   * **Date de création**.
   * **Système d’exploitation** : **Windows** ou **Linux**.
   * **Type**: Hadoop, Hbase, Storm, Spark.
   * **Version**. Voir [Versions HDInsight](hdinsight-component-versioning.md)
   * **Abonnement**: nom de l’abonnement.
   * **Source de données par défaut**: hello du système de fichiers du cluster par défaut.
   * **Taille des nœuds de Worker**.
   * **Taille du nœud principal**.

## <a name="delete-clusters"></a>Suppression des clusters
La suppression d’un cluster ne supprime pas de compte de stockage par défaut hello ou des comptes de stockage. Vous pouvez recréer les cluster hello à l’aide de hello les mêmes comptes de stockage et hello même magasin de métadonnées. Il est recommandé de toouse un conteneur d’objets Blob par défaut lorsque vous recréez le cluster de hello.

1. Connectez-vous à toohello [Portal][azure-portal].
2. Cliquez sur **Clusters HDInsight** à partir du menu de gauche hello. Si vous ne voyez pas **Clusters HDInsight**, cliquez d’abord sur **Plus de services**.
3. Cliquez sur le cluster hello que vous souhaitez toodelete.
4. Cliquez sur **supprimer** du menu du haut hello, puis suivez les instructions hello.

Voir aussi [Pause/arrêt de clusters](#pauseshut-down-clusters).

## <a name="add-additional-storage-accounts"></a>Ajouter des comptes de stockage

Vous pouvez ajouter des comptes de stockage Azure et des comptes Azure Data Lake Store supplémentaires après la création d’un cluster. Pour plus d’informations, consultez [ajouter tooHDInsight des comptes de stockage supplémentaire](./hdinsight-hadoop-add-storage.md).

## <a name="scale-clusters"></a>Mise à l’échelle des clusters
cluster Hello fonctionnalité de mise à l’échelle permet un nombre de hello toochange de nœuds de travail utilisé par un cluster qui s’exécute dans Azure HDInsight sans avoir toore-créer le cluster de hello.

> [!NOTE]
> Seuls les clusters ayant la version 3.1.3 de HDInsight ou une version ultérieure sont pris en charge. Si vous ne savez pas de version hello de votre cluster, vous pouvez vérifier la page de propriétés hello.  Voir [Énumération et affichage des clusters](#list-and-show-clusters).
>
>

impact Hello modifiant nombre hello de nœuds de données pour chaque type de cluster pris en charge par HDInsight :

* Hadoop

    Vous pouvez augmenter de façon transparente nombre hello de nœuds de travail dans un cluster Hadoop qui est en cours d’exécution sans impact sur toutes les tâches en attente ou en cours d’exécution. Nouvelles tâches peuvent également être soumises pendant que l’opération de hello est en cours. Échecs dans une opération de mise à l’échelle sont correctement gérés afin que hello cluster est toujours conservé dans un état fonctionnel.

    Lorsqu’un cluster Hadoop est réduite en réduisant le nombre de hello de nœuds de données, certains services hello dans un cluster de hello sont redémarrés. Ce comportement provoque en cours d’exécution et en attente de toofail de travaux à l’achèvement de hello Hello opération de mise à l’échelle. Vous pouvez, toutefois, renvoyer des tâches de hello une fois l’opération hello est terminée.
* HBase

    Vous pouvez accéder en toute transparence ajouter ou supprimer le cluster de nœuds tooyour HBase pendant son exécution. Serveurs régionaux sont équilibrés automatiquement après quelques minutes d’achèvement hello opération de mise à l’échelle. Toutefois, vous pouvez équilibrer manuellement les serveurs régionaux hello en vous connectant à un nœud principal de toohello du cluster et hello en cours d’exécution suivant des commandes dans une fenêtre d’invite de commandes :

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer

    Pour plus d’informations sur l’utilisation du shell HBase de hello, consultez]
* Storm

    Vous pouvez accéder en toute transparence ajouter ou supprimer le cluster de données nœuds tooyour Storm pendant son exécution. Mais après la réussite de l’opération de mise à l’échelle de hello, vous devrez topologie de hello toorebalance.

    Cela peut se faire de deux façons à l’aide de :

  * l'interface utilisateur Web de Storm
  * l’outil d’interface de ligne de commande (CLI)

    Consultez toohello [documentation d’Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) pour plus d’informations.

    interface utilisateur web de Storm Hello est disponible sur le cluster HDInsight de hello :

    ![Rééquilibrage de mise à l’échelle HDInsight Storm](./media/hdinsight-administer-use-portal-linux/hdinsight-portal-scale-cluster-storm-rebalance.png)

    Voici un exemple comment toouse hello CLI commande topologie de Storm toorebalance hello :

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

**clusters tooscale**

1. Connectez-vous à toohello [Portal][azure-portal].
2. Cliquez sur **Clusters HDInsight** à partir du menu de gauche hello.
3. Cliquez sur le cluster de hello souhaité tooscale.
3. Cliquez sur **Mettre à jour le cluster**.
4. Entrez une valeur dans le champ **Nombre de nœuds de travail**. Hello hello nombre limite de nœuds de cluster varie selon les abonnements Azure. Vous pouvez contacter facturation limite de hello tooincrease prise en charge.  informations sur les coûts Hello reflètent hello apportées nombre toohello de nœuds.

    ![HDInsight hadoop hbase storm spark mise à l’échelle](./media/hdinsight-administer-use-portal-linux/hdinsight-portal-scale-cluster.png)

## <a name="pauseshut-down-clusters"></a>Pause/arrêt de clusters

La plupart des travaux Hadoop sont les traitements par lots exécutés occasionnellement seulement. Pour la plupart des clusters Hadoop, il existe de grandes périodes de temps que le cluster hello n’est pas utilisé pour le traitement. Avec HDInsight, vos données sont stockées Azure Storage, pour que vous puissiez supprimer un cluster en toute sécurité s’il n’est pas en cours d’utilisation.
Vous devez également payer pour un cluster HDInsight, même lorsque vous ne l’utilisez pas. Étant donné que les frais de hello pour le cluster de hello sont autant de fois plus de frais hello pour le stockage, il est judicieux économique toodelete clusters lorsqu’ils ne sont pas en cours d’utilisation.

Il existe de nombreuses façons, vous pouvez programmer hello :

* Utilisateur d’Azure Data Factory. Pour créer des services liés HDInsight à la demande, consultez la section [Création de clusters Hadoop à la demande basés sur Linux dans HDInsight avec Azure Data Factory](hdinsight-hadoop-create-linux-clusters-adf.md) .
* Utilisation d’Azure PowerShell  Voir [Analyse des données sur les retards de vol](hdinsight-analyze-flight-delay-data.md).
* Utiliser l’interface de ligne de commande Microsoft Azure Voir [Gestion des clusters HDInsight à l’aide de l’interface de ligne de commande Azure](hdinsight-administer-use-command-line.md).
* Utilisation du kit de développement logiciel .NET. Voir [Envoyer des tâches Hadoop](hdinsight-submit-hadoop-jobs-programmatically.md).

Pourquoi les informations de tarification, consultez [tarification HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/). toodelete un cluster à partir de hello portail, consultez [supprimer des clusters](#delete-clusters)


## <a name="upgrade-clusters"></a>Mettre à niveau des clusters

Consultez [version plus récente de mise à niveau de HDInsight cluster tooa](./hdinsight-upgrade-cluster.md).

## <a name="change-passwords"></a>Modifier les mots de passe
Un cluster HDInsight peut disposer de deux comptes d'utilisateur. Hello compte utilisateur de cluster HDInsight (aussi appelé) Compte d’utilisateur HTTP) et hello SSH compte d’utilisateur sont créés au cours du processus de création de hello. Vous pouvez utiliser hello Ambari web UI toochange hello cluster compte nom d’utilisateur et mot de passe et script actions toochange hello compte d’utilisateur SSH

### <a name="change-hello-cluster-user-password"></a>Modification de mot de passe hello cluster utilisateur
Vous pouvez utiliser hello l’interface utilisateur de Ambari Web toochange hello Cluster mot de passe utilisateur. toolog dans tooAmbari, vous devez utiliser un mot de passe et nom d’utilisateur de cluster existant hello.

> [!NOTE]
> Mot de passe utilisateur (admin) de cluster hello modification risque de script actions exécutées sur cet toofail de cluster. Si vous disposez de toutes les actions de script persistantes qui ciblent des nœuds de travail, ces scripts peuvent échouer lorsque vous ajoutez le cluster de toohello nœuds via des opérations de redimensionnement. Pour plus d’informations sur les actions de script, consultez la section [Personnaliser des clusters HDInsight à l’aide d’actions de script](hdinsight-hadoop-customize-cluster-linux.md).
>
>

1. Connectez-vous à l’aide de l’interface utilisateur de Ambari Web toohello hello des informations d’identification du cluster HDInsight. nom d’utilisateur par défaut de Hello est **admin**. hello URL est **https://&lt;nom du Cluster HDInsight > azurehdinsight.net**.
2. Cliquez sur **Admin** à partir du menu du haut hello, puis cliquez sur « Gérer Ambari ».
3. Dans le menu de gauche hello, cliquez sur **utilisateurs**.
4. Cliquez sur **Admin**.
5. Cliquez sur **Modifier le mot de passe**.

Ambari puis passe hello sur tous les nœuds de cluster de hello.

### <a name="change-hello-ssh-user-password"></a>Modification de mot de passe hello SSH utilisateur
1. À l’aide d’un éditeur de texte, enregistrez hello après le texte dans un fichier nommé **changepassword.sh**.

   > [!IMPORTANT]
   > Vous devez utiliser un éditeur qui utilise le saut de ligne en tant que la fin de ligne hello. Si l’éditeur hello utilise CRLF, puis hello script ne fonctionne pas.
   >
   >

        #! /bin/bash
        USER=$1
        PASS=$2

        usermod --password $(echo $PASS | openssl passwd -1 -stdin) $USER
2. Téléchargez hello tooa emplacement de stockage qui sont accessibles à partir de HDInsight à l’aide d’une adresse HTTP ou HTTPS. Par exemple, un magasin de fichiers public tel que le stockage d’objets blob Azure ou OneDrive. Enregistrez-le hello URI (adresse HTTP ou HTTPS) toohello, car cet URI est nécessaire à l’étape suivante de hello.
3. À partir de hello portail Azure, cliquez sur **Clusters HDInsight**.
4. Cliquez sur votre cluster HDInsight.
4. Cliquez sur **Actions de script**.
4. À partir de hello **Actions de Script** panneau, sélectionnez **soumettre un nouveau**. Hello lorsque **envoyer l’action de script** panneau s’affiche, entrez hello informations suivantes :

   | Champ | Valeur |
   | --- | --- |
   | Nom |Modifier le mot de passe SSH |
   | URI de script bash |fichier Hello URI toohello changepassword.sh |
   | Nœuds (En-tête, Collaborateur, Nimbus, Superviseur, Zookeeper, etc.) |✓ pour tous les types de nœuds répertoriés |
   | Paramètres |Entrez le nom d’utilisateur SSH hello, puis le nouveau mot de passe hello. Il doit y avoir un espace entre le nom d’utilisateur hello et un mot de passe hello. |
   | Conservez cette action de script... |Laissez ce champ non coché. |
5. Sélectionnez **créer** script de hello tooapply. Une fois le script de hello terminée, vous êtes en mesure de tooconnect toohello cluster est à l’aide de SSH avec le nouveau mot de passe hello.

## <a name="grantrevoke-access"></a>Octroyer/Révoquer l’accès
Clusters HDInsight ont hello suivant (tous ces services ont des points de terminaison RESTful) des services web HTTP :

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

Par défaut, l'accès à ces services est octroyé. Vous pouvez révoquer ou octroyer hello l’accès à l’aide [CLI d’Azure](hdinsight-administer-use-command-line.md#enabledisable-http-access-for-a-cluster) et [Azure PowerShell](hdinsight-administer-use-powershell.md#grantrevoke-access).

## <a name="find-hello-subscription-id"></a>Rechercher l’ID d’abonnement hello

**toofind votre ID d’abonnement Azure**

1. Connectez-vous à toohello [Portal][azure-portal].
2. Cliquez sur **Abonnements**. Chaque abonnement a un nom et un ID.

Chaque cluster est liée tooan abonnement Azure. Hello d’abonnement ID est indiqué sur le cluster de hello **essentielles** vignette. Voir [Énumération et affichage des clusters](#list-and-show-clusters).

## <a name="find-hello-resource-group"></a>Recherchez le groupe de ressources hello
En mode de gestionnaire de ressources Azure hello, chaque cluster HDInsight est créé avec un groupe Azure Resource Manager. groupe de gestionnaire de ressources de Hello un cluster appartient tooappears dans :

* liste de cluster Hello a un **groupe de ressources** colonne.
* Mosaïque **Essential** du cluster.  

Voir [Énumération et affichage des clusters](#list-and-show-clusters).

## <a name="find-hello-default-storage-account"></a>Recherchez le compte de stockage par défaut hello
Chaque cluster HDInsight dispose d’un compte de stockage par défaut. Hello compte de stockage par défaut et ses clés pour un cluster apparaît sous **comptes de stockage**. Voir [Énumération et affichage des clusters](#list-and-show-clusters).

## <a name="run-hive-queries"></a>Exécuter des requêtes Hive
Vous ne pouvez pas exécuter les tâche Hive directement à partir de hello portail Azure, mais vous pouvez utiliser hello Hive la vue sur l’interface utilisateur de Ambari Web.

**requêtes de ruche toorun à l’aide de la vue de la ruche Ambari**

1. Connectez-vous à l’aide de l’interface utilisateur de Ambari Web toohello hello des informations d’identification du cluster HDInsight. nom d’utilisateur par défaut de Hello est **admin**. hello URL est **https://&lt;nom du Cluster HDInsight > azurehdinsight.net**.
2. Ouvrir la vue de la ruche comme indiqué dans hello suivant capture d’écran :  

    ![Affichage Hive dans HDInsight](./media/hdinsight-administer-use-portal-linux/hdinsight-hive-view.png)
3. Cliquez sur **requête** à partir du menu du haut hello.
4. Entrez une requête Hive dans l’**éditeur de requête**, puis cliquez sur **Exécuter**.

## <a name="monitor-jobs"></a>Surveiller des travaux
Consultez [HDInsight de gérer des clusters à l’aide de hello l’interface utilisateur de Ambari Web](hdinsight-hadoop-manage-ambari.md#monitoring).

## <a name="browse-files"></a>Parcourir les fichiers
À l’aide de hello portail Azure, vous pouvez parcourir le contenu du conteneur par défaut de hello hello.

1. Connectez-vous trop[https://portal.azure.com](https://portal.azure.com).
2. Cliquez sur **Clusters HDInsight** de hello toolist de menu de gauche hello clusters existants.
3. Cliquez sur le nom du cluster hello. Si la liste de cluster hello est longue, vous pouvez utiliser le filtre en haut de hello de page de hello.
4. Cliquez sur **comptes de stockage** à partir du menu de gauche hello cluster.
5. Cliquez sur un compte de stockage.
7. Cliquez sur hello **BLOB** vignette.
8. Cliquez sur le nom du conteneur par défaut hello.

## <a name="monitor-cluster-usage"></a>Surveiller l’utilisation du cluster
Hello **utilisation** section du Panneau de cluster HDInsight hello affiche des informations sur le nombre hello d’abonnement disponibles tooyour de cœurs pour une utilisation avec HDInsight, ainsi que nombre de hello de cœurs toothis cluster et comment elles sont allouées alloué pour les nœuds hello dans ce cluster. Voir [Énumération et affichage des clusters](#list-and-show-clusters).

> [!IMPORTANT]
> services de hello toomonitor fournie par hello cluster HDInsight, vous devez utiliser Ambari Web hello Ambari REST API. Pour plus d’informations sur l’utilisation d’Ambari, voir [Gestion des clusters HDInsight à l’aide d’Ambari](hdinsight-hadoop-manage-ambari.md)
>
>

## <a name="connect-tooa-cluster"></a>Se connecter tooa cluster

* [Utilisation de Hive avec HDInsight](hdinsight-hadoop-use-hive-ambari-view.md)
* [Utiliser SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)

## <a name="next-steps"></a>Étapes suivantes
Dans cet article, vous avez découvert certaines fonctions d’administration de base. toolearn, voir hello suivant des articles :

* [Administration de HDInsight à l’aide d’Azure PowerShell](hdinsight-administer-use-powershell.md)
* [Administration de HDInsight à l’aide de l’interface de ligne de commande Azure](hdinsight-administer-use-command-line.md)
* [Création de clusters HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
* [Utilisation d'Hive dans HDInsight](hdinsight-use-hive.md)
* [Utilisation de Pig dans HDInsight](hdinsight-use-pig.md)
* [Utilisation de Sqoop dans HDInsight](hdinsight-use-sqoop.md)
* [Prise en main d’Azure HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Version de Hadoop dans Azure HDInsight](hdinsight-component-versioning.md)

[azure-portal]: https://portal.azure.com
[image-hadoopcommandline]: ./media/hdinsight-administer-use-portal-linux/hdinsight-hadoop-command-line.png "Ligne de commande Hadoop"
