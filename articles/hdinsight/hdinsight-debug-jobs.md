---
title: "Déboguer Hadoop dans HDInsight : afficher les journaux et interpréter les messages d’erreur - Azure | Microsoft Docs"
description: "En savoir plus sur les messages d’erreur hello que peut s’afficher lors de l’administration à l’aide de PowerShell et les étapes à suivre toorecover de HDInsight."
services: hdinsight
tags: azure-portal
editor: cgronlun
manager: jhubbard
author: mumian
documentationcenter: 
ms.assetid: 7e6ceb0e-8be8-4911-bc80-20714030a3ad
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jgao
ms.openlocfilehash: 2f12a40e9dcac32ce2e11d66d60d8b3b212ecb53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-hdinsight-logs"></a>Analyse des journaux de HDInsight
Chaque cluster Hadoop dans Azure HDInsight dispose d’un compte de stockage Azure utilisé en tant que système de fichiers par défaut hello. compte de stockage Hello est désigné comme compte de stockage par défaut hello. Cluster utilise hello stockage de Table Azure et hello stockage d’objets Blob sur toostore de compte de stockage de valeur par défaut hello ses journaux.  toofind compte de stockage par défaut hello pour votre cluster, consultez [Hadoop de gérer des clusters dans HDInsight](hdinsight-administer-use-management-portal.md#find-the-default-storage-account). Hello journaux conservent Bonjour compte de stockage, même après la suppression de cluster de hello.

## <a name="logs-written-tooazure-tables"></a>Journaux écrits tooAzure Tables
Hello journaux écrits tooAzure Tables fournissent un niveau d’un aperçu de ce qui se passe avec un cluster HDInsight.

Lorsque vous créez un cluster HDInsight, 6 tables sont automatiquement créées pour les clusters dans le stockage de Table par défaut hello basés sur Linux :

* hdinsightagentlog
* syslog
* daemonlog
* hadoopservicelog
* ambariserverlog
* ambariagentlog

3 tables sont créées pour les clusters basés sur Windows :

* setuplog : journal des événements/des exceptions rencontrés lors de l’approvisionnement/la configuration des clusters HDInsight.
* hadoopinstalllog : le journal des événements ou des exceptions rencontrées lors de l’installation de Hadoop sur le cluster de hello. Cette table peut-être être utile pour résoudre les problèmes liés tooclusters créé avec des paramètres personnalisés.
* hadoopservicelog : journal des événements/des exceptions enregistrés par tous les services Hadoop. Cette table peut être utile pour déboguer les problèmes des échecs de toojob connexes sur les clusters HDInsight.

noms de fichiers de table Hello sont **u<ClusterName>DDMonYYYYatHHMMSSsss<TableName>**.

Ces tables contient hello champs qui suivent :

* ClusterDnsName
* ComponentName
* EventTimestamp
* Host
* MALoggingHash
* Message
* N
* PreciseTimeStamp
* Rôle
* RowIndex
* Locataire
* TIMESTAMP
* TraceLevel

### <a name="tools-for-accessing-hello-logs"></a>Outils pour accéder aux journaux de hello
Il existe de nombreux outils permettant d’accéder aux données de ces tables :

* Visual Studio
* Azure Storage Explorer
* Power Query pour Excel

#### <a name="use-power-query-for-excel"></a>Utiliser Power Query pour Excel
Power Query peut être installé à partir de [www.microsoft.com/en-us/download/details.aspx?id=39379](http://www.microsoft.com/en-us/download/details.aspx?id=39379). Consultez hello page de téléchargement de la configuration système requise du hello

**toouse Power Query tooopen et analyser le journal du service hello**

1. Ouvrez **Microsoft Excel**.
2. À partir de hello **Power Query** menu, cliquez sur **à partir de Azure**, puis cliquez sur **le stockage à partir de Microsoft Azure Table**.
   
    ![HDInsight Hadoop Excel PowerQuery ouvrir le stockage de tables Azure](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-using-excel-power-query-open.png)
3. Entrez le nom de compte de stockage hello. Cela peut être le nom court de hello ou de nom de domaine complet de hello.
4. Entrez la clé de compte de stockage hello. Une liste de tables doit s’afficher :
   
    ![Journaux HDInsight Hadoop stockés dans le stockage de tables Azure](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-table-names.png)
5. Table de hadoopservicelog avec le bouton hello Bonjour **Navigator** volet et sélectionnez **modifier**. 4 colonnes doivent s’afficher. Vous pouvez également supprimer hello **clé de Partition**, **clé de ligne**, et **Timestamp** les colonnes en les sélectionnant, puis en cliquant sur **supprimer les colonnes** Options de hello dans le ruban de hello.
6. Cliquez sur hello icône sur hello toochoose hello en colonnes souhaitées dans la feuille de calcul Excel hello tooimport de contenu. Pour cette démonstration, j’ai choisi les colonnes TraceLevel et ComponentName : elles peuvent me donner des informations de base sur les composants ayant rencontré des problèmes.
   
    ![Choisir les colonnes des journaux HDInsight Hadoop](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-using-excel-power-query-filter.png)
7. Cliquez sur **OK** tooimport les données de salutation.
8. Sélectionnez hello **TraceLevel**, rôle, et **ComponentName** colonnes, puis cliquez sur **Group By** contrôle dans le ruban de hello.
9. Cliquez sur **OK** dans la boîte de dialogue hello
10. Cliquez sur** Appliquer et fermer**.

Vous pouvez maintenant utiliser Excel toofilter et tri selon les besoins. Évidemment, vous souhaiterez tooinclude autres colonnes (par exemple, Message) dans toodrill d’ordre bas des problèmes lorsqu’ils se produisent, mais sélectionner et à grouper les colonnes hello décrites ci-dessus fournissent une image acceptable de ce qui se passe avec les services de Hadoop. Hello même idée peut être appliqué toohello setuplog et hadoopinstalllog.

#### <a name="use-visual-studio"></a>Utiliser Visual Studio
**toouse Visual Studio**

1. Ouvrez Visual Studio.
2. À partir de hello **vue** menu, cliquez sur **Cloud Explorer**. Ou cliquez simplement sur **CTRL+\, CTRL+X**.
3. Dans **Cloud Explorer**, sélectionnez **Types de ressources**.  Bonjour autre option disponible est **groupes de ressources**.
4. Développez **comptes de stockage**, hello compte de stockage par défaut pour votre cluster, puis **Tables**.
5. Double-cliquez sur **hadoopservicelog**.
6. Ajoutez un filtre. Par exemple :
   
        TraceLevel eq 'ERROR'
   
    ![Choisir les colonnes des journaux HDInsight Hadoop](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-visual-studio-filter.png)
   
    Pour plus d’informations sur la construction des filtres, consultez [construire des chaînes de filtrage pour hello Concepteur de tables](../vs-azure-tools-table-designer-construct-filter-strings.md).

## <a name="logs-written-tooazure-blob-storage"></a>Journaux écrit tooAzure stockage d’objets Blob
[Hello consigne les Tables écrites tooAzure](#log-written-to-azure-tables) fournissent un niveau d’un aperçu de ce qui se passe avec un cluster HDInsight. Toutefois, ces tables ne fournissent pas de journaux au niveau des tâches, qui peuvent être utiles pour explorer les problèmes lorsqu’ils se produisent. tooprovide ce niveau de détail, HDInsight sont des clusters suivant configuré de compte de stockage d’objets Blob toowrite tâche journaux tooyour pour une tâche qui est envoyée via Templeton. En pratique, cela signifie que les travaux soumis à l’aide des applets de commande de Microsoft Azure PowerShell hello ou hello API de soumission de travail .NET, pas les travaux soumis via RDP/ligne de commande toohello cluster d’accès. 

journaux de hello tooview, consultez [application d’accès fils de session basés sur Linux de HDInsight](hdinsight-hadoop-access-yarn-app-logs-linux.md).

Pour plus d’informations sur les journaux des applications, consultez la page [Simplifier la gestion et l’accès des journaux utilisateur dans YARN](http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/).

## <a name="view-cluster-health-and-job-logs"></a>Afficher les journaux de travail et d’état d’intégrité du cluster
### <a name="access-hadoop-ui"></a>Accéder à l’interface utilisateur Hadoop
À partir de hello portail Azure, cliquez sur une lame de cluster HDInsight cluster nom tooopen hello. Dans le panneau de cluster hello, cliquez sur **tableau de bord**.

![Tableau de bord du cluster](./media/hdinsight-debug-jobs/hdi-debug-launch-dashboard.png)

Lorsque vous y êtes invité, entrez les informations d’identification d’administrateur de cluster hello. Bonjour Console de requête qui s’ouvre, cliquez sur **Hadoop UI**.

![Démarrer l’interface utilisateur Hadoop](./media/hdinsight-debug-jobs/hdi-debug-launch-dashboard-hadoop-ui.png)

### <a name="access-hello-yarn-ui"></a>Hello d’accès fils UI
À partir de hello portail Azure, cliquez sur une lame de cluster HDInsight cluster nom tooopen hello. Dans le panneau de cluster hello, cliquez sur **tableau de bord**. Lorsque vous y êtes invité, entrez les informations d’identification d’administrateur de cluster hello. Bonjour Console de requête qui s’ouvre, cliquez sur **fils UI**.

Vous pouvez utiliser suivant de hello hello fils UI toodo :

* **Obtenir l’état du cluster**. Dans le volet gauche de hello, développez **Cluster**, puis cliquez sur **sur**. Ce présent cluster détails de l’état total alloué de la mémoire, cœurs utilisés, état du Gestionnaire de ressources de cluster hello, version, etc. de cluster.
  
    ![Tableau de bord du cluster](./media/hdinsight-debug-jobs/hdi-debug-yarn-cluster-state.png)
* **Obtenir l’état du nœud**. Dans le volet gauche de hello, développez **Cluster**, puis cliquez sur **nœuds**. Celle-ci répertorie tous les nœuds hello dans un cluster de hello, l’adresse HTTP de chaque nœud, nœud de ressources allouées tooeach, etc..
* **Surveiller l’état du travail**. Dans le volet gauche de hello, développez **Cluster**, puis cliquez sur **Applications** toolist tous hello travaux dans le cluster de hello. Si vous souhaitez toolook à des travaux dans un spécifique état (par exemple, nouveau, envoyé, en cours d’exécution, etc.), cliquez sur le lien approprié de hello sous **Applications**. Vous pouvez plus cliquer hello travail nom toofind plus d’informations sur la tâche hello ce type, notamment les sortie hello, journaux, etc..

### <a name="access-hello-hbase-ui"></a>Hello d’accès HBase UI
À partir de hello portail Azure, cliquez sur une lame de cluster HDInsight HBase cluster nom tooopen hello. Dans le panneau de cluster hello, cliquez sur **tableau de bord**. Lorsque vous y êtes invité, entrez les informations d’identification d’administrateur de cluster hello. Bonjour Console de requête qui s’ouvre, cliquez sur **HBase UI**.

## <a name="hdinsight-error-codes"></a>Codes d’erreur HDInsight
Hello les messages d’erreur détaillés dans cette section sont fournis aux utilisateurs de hello toohelp de Hadoop dans Azure HDInsight comprennent les conditions d’erreur possibles qu’ils peuvent rencontrer lors de l’administration de service hello à l’aide d’Azure PowerShell et tooadvise les étapes de hello toorecover à partir de l’erreur de hello qui peuvent être pris.

Certains de ces messages d’erreur peut également se produire dans hello portail Azure lorsqu’il est utilisé toomanage HDInsight clusters. Autres messages d’erreur que vous pouvez rencontrer, mais il existe moins précise, en raison de contraintes de toohello sur hello des actions de réparation possibles dans ce contexte. Autres messages d’erreur sont fournies dans les contextes de hello où l’atténuation de hello est évidente. 

### <a id="AtleastOneSqlMetastoreMustBeProvided"></a>AtleastOneSqlMetastoreMustBeProvided
* **Description**: fournissez les détails de base de données SQL Azure pour au moins un composant dans l’ordre toouse paramètres personnalisés des magasins de métadonnées Hive et Oozie.
* **Atténuation**: l’utilisateur hello doit toosupply une SQL Azure le magasin de métadonnées et de nouvelle tentative hello demande valide.  

### <a id="AzureRegionNotSupported"></a>AzureRegionNotSupported
* **Description**: impossible de créer un cluster dans la région *nom_région*. Utilisez une région HDInsight valide et relancez la requête.
* **Atténuation**: client doit créer la région de cluster hello qui les prend en charge actuellement : Asie du Sud-est, Europe de l’ouest, Europe du Nord, est des États-Unis ou ouest des États-Unis.  

### <a id="ClusterContainerRecordNotFound"></a>ClusterContainerRecordNotFound
* **Description**: hello serveur pas pu trouver hello a demandé l’enregistrement du cluster.  
* **Atténuation**: recommencez l’opération de hello.

### <a id="ClusterDnsNameInvalidReservedWord"></a>ClusterDnsNameInvalidReservedWord
* **Description**: le nom DNS du cluster *nom_DNS* est incorrect. Assurez-vous que le nom commence et se termine par un caractère alphanumérique et contient uniquement le caractère spécial '-'.  
* **Atténuation**: Assurez-vous que vous avez utilisé un nom DNS valide pour votre cluster qui commence et se termine par alphanumérique et ne contient aucun spéciale des caractères autres que les tirets hello '-', puis recommencez hello opération.

### <a id="ClusterNameUnavailable"></a>ClusterNameUnavailable
* **Description**: le nom de cluster *nom_cluster* n’est pas disponible. Choisissez un autre nom.  
* **Atténuation**: hello utilisateur doit spécifier un clustername est unique et ne pas existe et réessayez. Si les utilisateurs hello utilise hello Portal, hello l’interface utilisateur informe les si un nom de cluster est déjà utilisé au cours de hello créer des étapes.

### <a id="ClusterPasswordInvalid"></a>ClusterPasswordInvalid
* **Description** : le mot de passe de cluster n’est pas valide. Mot de passe doit comporter au moins 10 caractères et doit contenir au moins un chiffre, lettre majuscule, une lettre minuscule et un caractère spécial sans espaces et ne doit pas contenir de nom d’utilisateur de hello en tant que partie de celui-ci.  
* **Atténuation**: fournir un mot de passe de cluster valide et recommencez l’opération de hello.

### <a id="ClusterUserNameInvalid"></a>ClusterUserNameInvalid
* **Description**: le nom d’utilisateur du cluster est incorrect. Assurez-vous que le nom d'utilisateur ne contient pas de caractères spéciaux ni d'espaces.  
* **Atténuation**: fournissez un nom d’utilisateur de cluster valide et recommencez l’opération de hello.

### <a id="ClusterUserNameInvalidReservedWord"></a>ClusterUserNameInvalidReservedWord
* **Description**: le nom DNS du cluster *nom_DNS_cluster* est incorrect. Assurez-vous que le nom commence et se termine par un caractère alphanumérique et contient uniquement le caractère spécial '-'.  
* **Atténuation**: fournissez un nom d’utilisateur de cluster DNS valide et recommencez l’opération de hello.

### <a id="ContainerNameMisMatchWithDnsName"></a>ContainerNameMisMatchWithDnsName
* **Description**: nom de conteneur dans l’URI *yourcontainerURI* et le nom DNS *yourDnsName* dans la demande de corps doit être hello l’identique.  
* **Atténuation**: Assurez-vous que votre nom de conteneur et votre nom DNS sont de même hello et recommencez l’opération de hello.

### <a id="DataNodeDefinitionNotFound"></a>DataNodeDefinitionNotFound
* **Description**: configuration du cluster incorrecte. Impossible de toofind des définitions de nœud de données dans la taille du nœud.  
* **Atténuation**: recommencez l’opération de hello.

### <a id="DeploymentDeletionFailure"></a>DeploymentDeletionFailure
* **Description**: Échec de la suppression du déploiement pour hello Cluster  
* **Atténuation**: recommencez l’opération de suppression hello.

### <a id="DnsMappingNotFound"></a>DnsMappingNotFound
* **Description**: erreur de configuration du service. Informations de mappage DNS requises introuvables.  
* **Atténuation**: supprimez le cluster et recréez-en un.

### <a id="DuplicateClusterContainerRequest"></a>DuplicateClusterContainerRequest
* **Description**: tentative de duplication d’un conteneur de cluster. Il existe un enregistrement pour *nom_conteneur* , mais les valeurs Etag ne correspondent pas.
* **Atténuation**: fournissez un nom unique pour l’opération de création du conteneur de hello et hello de nouvelle tentative.

### <a id="DuplicateClusterInHostedService"></a>DuplicateClusterInHostedService
* **Description**: le service hébergé *nom_service_hébergé* contient déjà un cluster. Un service hébergé ne peut pas contenir plusieurs clusters.  
* **Atténuation**: service hébergé de cluster de hello hôte dans un autre.

### <a id="FailureToUpdateDeploymentStatus"></a>FailureToUpdateDeploymentStatus
* **Description**: serveur de hello n’a pas pu mettre à jour état hello du déploiement de cluster hello.  
* **Atténuation**: recommencez l’opération de hello. Si le problème se reproduit plusieurs fois, contactez CSS.

### <a id="HdiRestoreClusterAltered"></a>HdiRestoreClusterAltered
* **Description**: Le cluster *nom_cluster* a été supprimé dans le cadre de la maintenance. Recréez le cluster de hello.
* **Atténuation**: cluster de hello recréer.

### <a id="HeadNodeConfigNotFound"></a>HeadNodeConfigNotFound
* **Description**: configuration du cluster incorrecte. Configuration de nœud principal introuvable dans les tailles de nœud.
* **Atténuation**: recommencez l’opération de hello.

### <a id="HostedServiceCreationFailure"></a>HostedServiceCreationFailure
* **Description**: Impossible de toocreate le service hébergé *nameOfYourHostedService*. Relancez la requête.  
* **Atténuation**: demande de nouvelle tentative hello.

### <a id="HostedServiceHasProductionDeployment"></a>HostedServiceHasProductionDeployment
* **Description**: le service hébergé *nom_service_hébergé* a déjà un déploiement de production. Un service hébergé ne peut pas contenir plusieurs déploiements de production. Réessayez la demande hello avec un autre nom de cluster.
* **Atténuation**: utiliser un autre nom de cluster et de nouvelle tentative de demande de hello.

### <a id="HostedServiceNotFound"></a>HostedServiceNotFound
* **Description**: Service hébergé *nameOfYourHostedService* pour le cluster de hello est introuvable.  
* **Atténuation**: si le cluster de hello est en état d’erreur, supprimez-le et réessayez.

### <a id="HostedServiceWithNoDeployment"></a>HostedServiceWithNoDeployment
* **Description**: aucun déploiement n’est associé au service hébergé *nom_service_hébergé* .  
* **Atténuation**: si le cluster de hello est en état d’erreur, supprimez-le et réessayez.

### <a id="InsufficientResourcesCores"></a>InsufficientResourcesCores
* **Description**: hello SubscriptionId *yourSubscriptionId* n’a pas de cluster de gauche toocreate cœurs *yourClusterName*. Requis : *Ressources_requises*, disponible : *Ressources_disponibles*.  
* **Atténuation**: libérer des ressources dans votre abonnement ou augmenter l’abonnement aux ressources de hello toohello disponibles et essayez à nouveau de cluster de hello toocreate.

### <a id="InsufficientResourcesHostedServices"></a>InsufficientResourcesHostedServices
* **Description**: ID d’abonnement *yourSubscriptionId* n’a pas de quota pour un cluster le service hébergé toocreate *yourClusterName*.  
* **Atténuation**: libérer des ressources dans votre abonnement ou augmenter l’abonnement aux ressources de hello toohello disponibles et essayez à nouveau de cluster de hello toocreate.

### <a id="InternalErrorRetryRequest"></a>InternalErrorRetryRequest
* **Description**: serveur de hello a rencontré une erreur interne. Relancez la requête.  
* **Atténuation**: demande de nouvelle tentative hello.

### <a id="InvalidAzureStorageLocation"></a>InvalidAzureStorageLocation
* **Description**: l’emplacement d’Azure Storage *nom_région_données* n’est pas un emplacement correct. Assurez-vous que la région de hello est correcte et réessayez la demande.
* **Atténuation**: sélectionnez un emplacement de stockage qui prend en charge HDInsight, vérifiez que votre cluster est colocalisé et recommencez l’opération de hello.

### <a id="InvalidNodeSizeForDataNode"></a>InvalidNodeSizeForDataNode
* **Description**: la taille de la machine virtuelle est incorrecte pour les nœuds de données. Seule la taille « Machine virtuelle large » est prise en charge pour tous les nœuds de données.  
* **Atténuation**: spécifiez la taille du nœud hello pris en charge pour le nœud de données hello et recommencez l’opération de hello.

### <a id="InvalidNodeSizeForHeadNode"></a>InvalidNodeSizeForHeadNode
* **Description**: la taille de la machine virtuelle est incorrecte pour le nœud principal. Seule la taille « Machine virtuelle extra large » est prise en charge pour le nœud principal.  
* **Atténuation**: spécifiez la taille du nœud hello pris en charge pour le nœud principal de hello et recommencez l’opération de hello

### <a id="InvalidRightsForDeploymentDeletion"></a>InvalidRightsForDeploymentDeletion
* **Description**: ID d’abonnement *yourSubscriptionId* utilisé ne contient aucune opération de suppression autorisations tooexecute suffisant pour le cluster *yourClusterName*.  
* **Atténuation**: si le cluster de hello est en état d’erreur, supprimer et puis recommencez l’opération.  

### <a id="InvalidStorageAccountBlobContainerName"></a>InvalidStorageAccountBlobContainerName
* **Description**: le nom du conteneur d’objets blob du compte de stockage externe *nom_conteneur* est incorrect. Assurez-vous que le nom commence par une lettre et contient uniquement des lettres minuscules, des chiffres et des tirets.  
* **Atténuation**: spécifiez un nom de conteneur compte stockage valide et recommencez l’opération de hello.

### <a id="InvalidStorageAccountConfigurationSecretKey"></a>InvalidStorageAccountConfigurationSecretKey
* **Description**: Configuration pour le compte de stockage externe *yourStorageAccountName* est requis toohave détails de la clé secrètes toobe ensemble.  
* **Atténuation**: spécifiez une clé secrète valide pour le compte de stockage hello et recommencez l’opération de hello.

### <a id="InvalidVersionHeaderFormat"></a>InvalidVersionHeaderFormat
* **Description**: l’en-tête de version *entête_version* n’est pas au format correct : aaaa-mm-jj.  
* **Atténuation**: spécifiez un format valide pour l’en-tête de version hello et nouvelle tentative de demande de hello.

### <a id="MoreThanOneHeadNode"></a>MoreThanOneHeadNode
* **Description**: configuration du cluster incorrecte. Plusieurs configurations de nœud principal trouvées.  
* **Atténuation**: configuration de hello modifier afin que seul un nœud principal est spécifié.

### <a id="OperationTimedOutRetryRequest"></a>OperationTimedOutRetryRequest
* **Description**: opération de hello n’a pas pu être terminer dans hello autorisé de temps ou nombre maximal de tentatives hello tentative possible. Relancez la requête.  
* **Atténuation**: demande de nouvelle tentative hello.

### <a id="ParameterNullOrEmpty"></a>ParameterNullOrEmpty
* **Description**: le paramètre *nom_paramètre* ne peut pas être de type null ou vide.  
* **Atténuation**: spécifiez une valeur valide pour le paramètre hello.

### <a id="PreClusterCreationValidationFailure"></a>PreClusterCreationValidationFailure
* **Description**: un ou plusieurs des entrées de demande de création de cluster hello ne sont pas valide. Assurez-vous que les valeurs d’entrée hello sont corrects et réessayez la demande.  
* **Atténuation**: Assurez-vous que les valeurs d’entrée hello sont corrects et réessayez la demande.

### <a id="RegionCapabilityNotAvailable"></a>RegionCapabilityNotAvailable
* **Description** : capacité de région non disponible pour la région *nom_région* et l’ID d’abonnement *ID_abonnement*.  
* **Atténuation**: spécifiez une région qui prend en charge les clusters HDInsight. les régions Hello officiellement pris en charge sont : Asie du Sud-est, Europe de l’ouest, Europe du Nord, est des États-Unis ou ouest des États-Unis.

### <a id="StorageAccountNotColocated"></a>StorageAccountNotColocated
* **Description** : le compte de stockage *nom_compte_stockage* se trouve dans la région *nom_région_actuelle*. Il doit être identique à la région de cluster hello *yourClusterRegionName*.  
* **Atténuation**: spécifiez un compte de stockage dans hello même région que votre cluster ou si vos données sont déjà dans le compte de stockage hello, créez un nouveau cluster Bonjour même région que le compte de stockage existant hello. Si vous utilisez le portail de hello, hello UI est les informer de ce problème à l’avance.

### <a id="SubscriptionIdNotActive"></a>SubscriptionIdNotActive
* **Description**: l’ID d’abonnement *ID_abonnement* n’est pas actif.  
* **Atténuation**: réactivez votre abonnement ou obtenez un nouvel abonnement valide.

### <a id="SubscriptionIdNotFound"></a>SubscriptionIdNotFound
* **Description**: l’ID d’abonnement *ID_abonnement* est introuvable.  
* **Atténuation**: Vérifiez que votre ID d’abonnement est valide et recommencez l’opération de hello.

### <a id="UnableToResolveDNS"></a>UnableToResolveDNS
* **Description**: Impossible de tooresolve DNS *yourDnsUrl*. Vérifiez que hello complet URL de point de terminaison hello blob est effectuée.  
* **Atténuation**: fournissez une URL d’objet blob correcte. Hello URL doit être entièrement valide, y compris le démarrage avec *http://* et se terminant par *.com*.

### <a id="UnableToVerifyLocationOfResource"></a>UnableToVerifyLocationOfResource
* **Description**: emplacement tooverify Impossible de ressource *yourDnsUrl*. Vérifiez que hello complet URL de point de terminaison hello blob est effectuée.  
* **Atténuation**: fournissez une URL d’objet blob correcte. Hello URL doit être entièrement valide, y compris le démarrage avec *http://* et se terminant par *.com*.

### <a id="VersionCapabilityNotAvailable"></a>VersionCapabilityNotAvailable
* **Description** : capacité de version non disponible pour la version *version_spécifiée* et l’ID d’abonnement *ID_abonnement*.  
* **Atténuation**: choisissez une version qui n’est disponible et recommencez l’opération de hello.

### <a id="VersionNotSupported"></a>VersionNotSupported
* **Description**: la version *version_spécifiée* n’est pas prise en charge.
* **Atténuation**: choisir une version prise en charge et recommencez l’opération de hello.

### <a id="VersionNotSupportedInRegion"></a>VersionNotSupportedInRegion
* **Description** : la version *version_spécifiée* n’est pas disponible dans la région Azure *région_spécifiée*.  
* **Atténuation**: choisir une version prise en charge dans la région de hello spécifiée et recommencez l’opération de hello.

### <a id="WasbAccountConfigNotFound"></a>WasbAccountConfigNotFound
* **Description**: configuration du cluster incorrecte. Configuration de compte WASB requise introuvable dans les comptes externes.  
* **Atténuation**: Vérifiez que le compte de hello existe et qu’il est spécifié correctement dans l’opération de hello de configuration, puis réessayez.

## <a name="next-steps"></a>Étapes suivantes
* [Utilisez les vues Ambari toodebug Tez travaux sur HDInsight](hdinsight-debug-ambari-tez-view.md)
* [Activer les dumps de tas pour les services Hadoop sur HDInsight sur Linux](hdinsight-hadoop-collect-debug-heap-dump-linux.md)
* [Gérer des clusters HDInsight à l’aide de hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md)

