---
title: environnements aaaCompute pris en charge par Azure Data Factory | Documents Microsoft
description: "En savoir plus sur les environnements de calcul que vous pouvez utiliser dans Azure Data Factory pipelines (par exemple, Azure HDInsight) tootransform ou traitent des données."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 6877a7e8-1a58-4cfb-bbd3-252ac72e4145
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 07/25/2017
ms.author: shlo
ms.openlocfilehash: aba7d7de695bc1c7d475f1e741ee3b3e884151c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="compute-environments-supported-by-azure-data-factory"></a>Environnements de calcul pris en charge par Azure Data Factory
Cet article explique les environnements de calcul différents que vous pouvez utiliser tooprocess ou transformer des données. Il fournit également des détails sur les différentes configurations (demand et apportez votre propre) pris en charge par la fabrique de données lors de la configuration de liaison ces fabrique de données Azure compute environnements tooan de services liés.

Hello tableau suivant fournit une liste des environnements de calcul pris en charge par les activités de fabrique de données et hello pouvant s’exécuter sur ces derniers. 

| Environnement de calcul | activités |
| --- | --- |
| [Cluster HDInsight à la demande](#azure-hdinsight-on-demand-linked-service) ou [votre propre cluster HDInsight](#azure-hdinsight-linked-service) |[DotNet](data-factory-use-custom-activities.md), [Hive](data-factory-hive-activity.md), [Pig](data-factory-pig-activity.md), [MapReduce](data-factory-map-reduce.md), [Diffusion en continu Hadoop](data-factory-hadoop-streaming-activity.md) |
| [Azure Batch](#azure-batch-linked-service) |[DotNet](data-factory-use-custom-activities.md) |
| [Azure Machine Learning](#azure-machine-learning-linked-service) |[Activités Machine Learning : exécution de lot et mise à jour de ressource](data-factory-azure-ml-batch-execution-activity.md) |
| [Service Analytique Azure Data Lake](#azure-data-lake-analytics-linked-service) |[Langage U-SQL du service Analytique Data Lake](data-factory-usql-activity.md) |
| [Azure SQL](#azure-sql-linked-service), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-linked-service), [SQL Server](#sql-server-linked-service) |[Procédure stockée](data-factory-stored-proc-activity.md) |

## <a name="supported-hdinsight-versions-in-azure-data-factory"></a>Versions de HDInsight prises en charge dans Azure Data Factory
Azure HDInsight prend en charge plusieurs versions de cluster Hadoop qui peuvent être déployées à tout moment. Chaque choix version crée une version spécifique de distribution de hello Hortonworks Data Platform (HDP) et un ensemble de composants qui sont contenues dans cette distribution. Microsoft est mise à jour de liste hello versions prises en charge des derniers Hadoop HDInsight tooprovide composants écosystème et des correctifs. Hello 3.2 de HDInsight est déconseillée à compter du 1er avril 2017. Pour plus d’informations, voir [Versions de HDInsight prises en charge](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions).

Ceci influe sur les fabriques de données Azure Data Factory existantes, où des activités sont en cours d’exécution sur des clusters HDInsight 3.2. Nous vous recommandons d’indications de hello toofollow utilisateurs Bonjour suivant la section tooupdate hello fabriques de données concernés :

### <a name="for-linked-services-pointing-tooyour-own-hdinsight-clusters"></a>Pour les Services liés pointant vers les clusters HDInsight propres tooyour
* **Les Services liés HDInsight pointant tooyour propre HDInsight 3.2 ou en dessous de clusters :**

  Azure Data Factory prend en charge la soumission tooyour travaux HDInsight propre clusters trop de HDI 3.1[hello plus récentes prises en charge HDInsight version](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions). Toutefois, vous ne pouvez plus créer HDInsight 3.2 cluster après le 1er avril 2017 selon la stratégie d’amortissement hello documentée dans [HDInsight versions prises en charge](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions).  

  **Recommandations :** 
  * Effectuer des tests tooensure hello compatibilité Hello activités qui font référence à ce service lié trop[hello plus récentes prises en charge HDInsight version](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) avec les informations documentées dans [disponibles avec les composants Hadoop différentes versions de HDInsight](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) et [Hortonworks notes de publication associés aux versions de HDInsight](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions).
  * Mise à niveau de votre cluster HDInsight 3.2 trop[hello plus récentes prises en charge HDInsight version](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) tooget hello derniers composants écosystème de Hadoop et des correctifs. 

* **Les Services liés HDInsight pointant tooyour propre HDInsight 3.3 ou au-dessus de clusters :**

  Azure Data Factory prend en charge la soumission tooyour travaux HDInsight propre clusters trop de HDI 3.1[hello plus récentes prises en charge HDInsight version](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions). 
  
  **Recommandations :** 
  * Aucune action n’est requise du point de vue de Data Factory. Toutefois, si vous utilisez une version antérieure de HDInsight, nous vous recommandons la mise à niveau trop[hello plus récentes prises en charge HDInsight version](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) tooget hello derniers composants écosystème de Hadoop et des correctifs.

### <a name="for-hdinsight-on-demand-linked-services"></a>Pour les services liés à la demande HDInsight
* **La version 3.2 ou antérieure est spécifiée dans la définition JSON des services liés à la demande HDInsight :**
  
  Azure Data Factory prend en charge la création de clusters HDInsight à la demande en version 3.3 ou ultérieure à partir du **15/05/2017**. Et, à la fin de hello de prise en charge pour 3.2 de HDInsight à la demande existante services liés est trop étendue**15/07/2017**.  

  **Recommandations :** 
  * Effectuer des tests tooensure hello compatibilité Hello activités qui font référence à ce service lié trop [hello plus récentes prises en charge HDInsight version](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) avec les informations documentées dans [disponibles avec les composants Hadoop différentes versions de HDInsight](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) et [Hortonworks notes de publication associés aux versions de HDInsight](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions).
  * Avant de **15/07/2017**, mettre à jour de la propriété Version hello dans la définition JSON de Service lié à la demande HDI trop[hello plus récentes prises en charge HDInsight version](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) tooget hello derniers Hadoop écosystème composants et correctifs. Pour la définition JSON détaillée, consultez toohello [exemple de Service lié d’Azure HDInsight à la demande](#azure-hdinsight-on-demand-linked-service). 

* **Version non spécifiée dans les services liés HDInsight à la demande :**
  
  Azure Data Factory prend en charge la création de clusters HDInsight à la demande en version 3.3 ou ultérieure à partir du **15/05/2017**. Et fin hello tooexisting sur demande 3.2 HDInsight lié des services de support est trop étendue**15/07/2017**. 

  Avant de **15/07/2017**, si ce champ est vide, les valeurs par défaut de hello pour la version et les propriétés d’osType : 

  | Propriété | Valeur par défaut | Requis |
  | --- | --- | --- |
  Version   | HDI 3.1 pour un cluster Windows et HDI 3.2 pour un cluster Linux.| Non
  osType | valeur par défaut Hello est Windows | Non

  Après avoir **15/07/2017**, si ce champ est vide, les valeurs par défaut de hello pour la version et les propriétés d’osType :

  | Propriété | Valeur par défaut | Requis |
  | --- | --- | --- |
  Version   | HDI 3.3 pour un cluster Windows et HDI 3.5 pour un cluster Linux.    | Non
  osType | valeur par défaut Hello est Linux   | Non

  **Recommandations :** 
  * Avant de **15/07/2017**, effectuer des tests tooensure hello compatibilité Hello activités qui font référence à ce service lié trop[hello plus récentes prises en charge HDInsight version](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) avec les informations documentées dans [composants Hadoop disponibles avec différentes versions de HDInsight](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) et [Hortonworks notes de publication associés aux versions de HDInsight](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions).  
  * Après avoir **15/07/2017**, assurez-vous que vous spécifiez explicitement les valeurs osType et version si vous souhaitez que les paramètres par défaut de hello toooverride. 

>[!Note]
>Actuellement, Azure Data Factory ne prend pas en charge les clusters HDInsight avec Azure Data Lake Store comme magasin principal. Utilisez Stockage Azure comme magasin principal pour les clusters HDInsight. 
>  
>  

## <a name="on-demand-compute-environment"></a>Environnement de calcul à la demande
Dans ce type de configuration, environnement hello est entièrement gérée par le service d’Azure Data Factory hello. Il est automatiquement créé par hello service Data Factory avant un travail est soumis tooprocess données et supprimé lorsque hello tâche est terminée. Vous pouvez créer un service lié pour un environnement de calcul de la demande de hello, configurer et contrôler les paramètres de niveau de granularité pour l’exécution du travail, gestion du cluster et actions d’amorçage.

> [!NOTE]
> configuration de la demande de Hello est actuellement pris en charge uniquement pour les clusters Azure HDInsight.
> 
> 

## <a name="azure-hdinsight-on-demand-linked-service"></a>Service lié à la demande Azure HDInsight
Hello service Azure Data Factory peut créer automatiquement un données de tooprocess cluster basé sur Windows/Linux à la demande HDInsight. cluster de Hello est créé dans la même région que le compte de stockage hello (propriété linkedServiceName Bonjour JSON) associée au cluster de hello de hello. compte de stockage Hello doit être un compte de stockage Azure de standard à usage général. 

Notez les éléments suivants de hello **important** points sur HDInsight de la demande de service lié :

* Vous ne voyez pas à la demande hello cluster HDInsight créé dans votre abonnement Azure. Hello service Azure Data Factory gère le cluster de HDInsight hello à la demande à votre place.
* Hello journaux pour les travaux qui est exécutés sur un HDInsight à la demande de cluster copiés toohello compte de stockage associé au cluster HDInsight de hello. Vous pouvez accéder à ces journaux à partir de hello portail Azure Bonjour **détails de l’activité exécuter** panneau. Pour plus de détails, consultez l'article [Surveiller et gérer les pipelines](data-factory-monitor-manage-pipelines.md) .
* Vous payez uniquement pour les temps de hello lorsque le cluster HDInsight de hello est active et les tâches en cours d’exécution.

> [!IMPORTANT]
> L’opération prend généralement **20 minutes** ou tooprovision plus d’un Azure HDInsight de cluster à la demande.
> 
> 

### <a name="example"></a>Exemple
Hello suivant JSON définit un service lié HDInsight à la demande sur Linux. Hello service Data Factory crée automatiquement un **basés sur Linux** cluster HDInsight lors du traitement d’une tranche de données. 

```json
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "AzureStorageLinkedService"
        }
    }
}
```

toouse un cluster HDInsight de basés sur Windows, définissez **osType** trop**windows** ou n’utilisez pas de propriété de hello comme valeur par défaut de hello est : windows.  

> [!IMPORTANT]
> Hello HDInsight cluster crée un **conteneur par défaut** dans le stockage blob hello spécifié dans hello JSON (**linkedServiceName**). HDInsight ne supprime pas ce conteneur lorsque le cluster de hello est supprimé. Ce comportement est normal. Service lié HDInsight à la demande un cluster HDInsight est créé chaque fois qu’une tranche doit toobe traité sauf s’il existe un cluster dynamique existant (**timeToLive**) et est supprimé quand le traitement de hello est effectué. 
> 
> Comme un nombre croissant de tranches sont traitées, vous voyez un grand nombre de conteneurs dans votre stockage d’objets blob Azure. Si vous ne devez pas les pour la résolution des problèmes de travaux de hello, vous souhaiterez peut-être toodelete les coûts de stockage tooreduce hello. les noms de ces conteneurs Hello suivent un modèle : `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`. Utiliser des outils tels que [Explorateur de stockage Microsoft](http://storageexplorer.com/) stockage d’objets blob des conteneurs de toodelete dans votre Azure.
> 
> 

### <a name="properties"></a>Propriétés
| Propriété | Description | Requis |
| --- | --- | --- |
| type |propriété de type Hello doit être définie trop**HDInsightOnDemand**. |Oui |
| clusterSize |Nombre de nœuds de données des collaborateurs de cluster de hello. cluster HDInsight de Hello est créé avec 2 nœuds principal, ainsi que le nombre de hello de nœuds de travail que vous spécifiez pour cette propriété. les nœuds de Hello sont de taille D3 standard qui a 4 cœurs, pour un cluster de nœuds 4 worker prend 24 cœurs (4\*4 = 16 cœurs pour les nœuds de travail, ainsi que 2\*4 = 8 cœurs pour les nœuds principal). Consultez [Hadoop basé sur Linux de créer des clusters dans HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) pour plus d’informations sur la couche de hello D3 standard. |Oui |
| timetolive |Hello autorisé de temps d’inactivité pour le cluster de HDInsight hello à la demande. Spécifie la durée pendant laquelle hello à la demande HDInsight cluster reste actif après l’achèvement d’une activité à exécuter s’il en existe aucune autre tâche active dans le cluster de hello.<br/><br/>Par exemple, si une activité exécuter prend 6 minutes et la propriété timetolive est défini à too5 minutes, hello reste de cluster actif pendant 5 minutes après hello 6 minutes du traitement d’exécution de l’activité hello. Si l’exécution à une autre activité est exécutée avec la fenêtre de 6 minutes hello, il est traité par hello même cluster.<br/><br/>Création d’un cluster de HDInsight à la demande est une opération coûteuse (Impossible de prendre un certain temps), par conséquent, utilisez ce paramètre d’une fabrique de données de performances tooimprove nécessaires en réutilisant un cluster de HDInsight à la demande.<br/><br/>Si vous définissez la propriété timetolive valeur too0, cluster de hello est supprimé dès que l’exécution de l’activité hello se termine. Alors que, si vous définissez une valeur élevée, le cluster de hello peut rester inactif inutilement entraîne des coûts élevés. Par conséquent, il est important que valeur hello approprié selon vos besoins.<br/><br/>Si la valeur de la propriété timetolive hello est configuré correctement, plusieurs pipelines peuvent partager instance hello du cluster de HDInsight hello à la demande.  |Oui |
| version |Version du cluster HDInsight de hello. valeur par défaut de Hello est 3.1 pour le cluster Windows et 3.2 de cluster Linux. |Non |
| linkedServiceName | Toobe de service lié de stockage Azure utilisé par le cluster à la demande de hello pour le stockage et le traitement des données. Hello cluster HDInsight est créé dans hello même région que ce compte de stockage Azure.<p>Actuellement, vous ne peut pas créer un cluster HDInsight à la demande qui utilise une Azure Data Lake Store en tant que stockage de hello. Si vous souhaitez que les données de résultat hello toostore de HDInsight de traitement dans un Azure Data Lake Store, utilisez un activité de copie toocopy hello des données de toohello de stockage d’objets Blob Azure hello Azure Data Lake Store. </p>  | Oui |
| additionalLinkedServiceNames |Spécifie les comptes de stockage supplémentaires pour hello HDInsight le service lié afin que le service de fabrique de données hello de les inscrire à votre place. Ces comptes de stockage doivent être Bonjour même région que le cluster HDInsight hello, qui est créé dans hello même région que le compte de stockage hello spécifié par linkedServiceName. |Non |
| osType |Type de système d'exploitation. Les valeurs autorisées sont Windows (par défaut) et Linux. |Non |
| hcatalogLinkedServiceName |nom de Hello de lié SQL Azure service point toohello HCatalog base de données. cluster de HDInsight Hello à la demande est créée à l’aide de la base de données SQL Azure hello en tant que le magasin de métadonnées hello. |Non |

#### <a name="additionallinkedservicenames-json-example"></a>Exemple JSON additionalLinkedServiceNames

```json
"additionalLinkedServiceNames": [
    "otherLinkedServiceName1",
    "otherLinkedServiceName2"
  ]
```

### <a name="advanced-properties"></a>Propriétés avancées
Vous pouvez également spécifier hello hello granularité de la configuration du cluster de HDInsight à la demande hello propriétés suivantes.

| Propriété | Description | Requis |
|:--- |:--- |:--- |
| coreConfiguration |Spécifie les paramètres de configuration principale hello (comme dans core-site.XML) pour hello HDInsight cluster toobe est créé. |Non |
| hBaseConfiguration |Spécifie les paramètres de configuration hello HBase (hbase-site.XML) pour le cluster HDInsight de hello. |Non |
| hdfsConfiguration |Spécifie les paramètres de configuration hello HDFS (hdfs-site.XML) pour le cluster HDInsight de hello. |Non |
| hiveConfiguration |Spécifie les paramètres de configuration hello hive (hive-site.XML) pour le cluster HDInsight de hello. |Non |
| mapReduceConfiguration |Spécifie les paramètres de configuration hello MapReduce (mapred-site.XML) pour le cluster HDInsight de hello. |Non |
| oozieConfiguration |Spécifie les paramètres de configuration hello Oozie (oozie-site.XML) pour le cluster HDInsight de hello. |Non |
| stormConfiguration |Spécifie les paramètres de configuration hello Storm (storm-site.XML) pour le cluster HDInsight de hello. |Non |
| yarnConfiguration |Spécifie les paramètres de configuration hello Yarn (yarn-site.XML) pour le cluster HDInsight de hello. |Non |

#### <a name="example--on-demand-hdinsight-cluster-configuration-with-advanced-properties"></a>Exemple : configuration de cluster HDInsight à la demande avec les propriétés avancées

```json
{
  "name": " HDInsightOnDemandLinkedService",
  "properties": {
    "type": "HDInsightOnDemand",
    "typeProperties": {
      "clusterSize": 16,
      "timeToLive": "01:30:00",
      "linkedServiceName": "adfods1",
      "coreConfiguration": {
        "templeton.mapper.memory.mb": "5000"
      },
      "hiveConfiguration": {
        "templeton.mapper.memory.mb": "5000"
      },
      "mapReduceConfiguration": {
        "mapreduce.reduce.java.opts": "-Xmx4000m",
        "mapreduce.map.java.opts": "-Xmx4000m",
        "mapreduce.map.memory.mb": "5000",
        "mapreduce.reduce.memory.mb": "5000",
        "mapreduce.job.reduce.slowstart.completedmaps": "0.8"
      },
      "yarnConfiguration": {
        "yarn.app.mapreduce.am.resource.mb": "5000",
        "mapreduce.map.memory.mb": "5000"
      },
      "additionalLinkedServiceNames": [
        "datafeeds",
        "adobedatafeed"
      ]
    }
  }
}
```

### <a name="node-sizes"></a>Tailles de nœuds
Vous pouvez spécifier les tailles de hello de noeuds head, les données et soigneur à l’aide des propriétés suivantes de hello : 

| Propriété | Description | Requis |
|:--- |:--- |:--- |
| headNodeSize |Spécifie la taille de hello du nœud principal de hello. la valeur par défaut Hello est : D3 standard. Consultez hello **spécifier les tailles de nœud** pour plus d’informations. |Non |
| dataNodeSize |Spécifie la taille de hello du nœud de données hello. la valeur par défaut Hello est : D3 standard. |Non |
| zookeeperNodeSize |Spécifie la taille de hello du nœud de gardien de Zoo hello. la valeur par défaut Hello est : D3 standard. |Non |

#### <a name="specifying-node-sizes"></a>Spécification des tailles de nœud
Consultez hello [tailles des Machines virtuelles](../virtual-machines/linux/sizes.md) article pour les valeurs de chaîne que vous devez toospecify pour les propriétés hello mentionnées dans la section précédente de hello. les valeurs de Hello doivent tooconform toohello **applets de commande et API** référencée dans l’article de hello. Comme vous pouvez le voir dans l’article de hello, le nœud de données hello de (par défaut) de grande taille a 7 Go de mémoire, ce qui n’est peut-être pas suffisante pour votre scénario. 

Si vous souhaitez toocreate D4 dimensionné nœuds principal et les nœuds de travail, spécifiez **Standard_D4** en tant que valeur hello pour les propriétés headNodeSize et dataNodeSize. 

```json
"headNodeSize": "Standard_D4",    
"dataNodeSize": "Standard_D4",
```

Si vous spécifiez une valeur incorrecte pour ces propriétés, vous pouvez recevoir des éléments suivants de hello **erreur :** n’a pas pu toocreate cluster. Exception : Cluster de hello toocomplete Impossible de l’opération de création. Operation failed with code ’400’. (L’opération a échoué avec le code « 400 ».) Cluster left behind state: 'Error'. Message: 'PreClusterCreationValidationFailure'. Lorsque vous recevez cette erreur, assurez-vous que vous utilisez hello **applet de commande et API** nom de table hello Bonjour [tailles des Machines virtuelles](../virtual-machines/linux/sizes.md) l’article.  

## <a name="bring-your-own-compute-environment"></a>Apportez votre propre environnement de calcul
Dans ce type de configuration, les utilisateurs peuvent inscrire un environnement de calcul existant en tant que service lié dans Data Factory. environnement Hello est gérée par l’utilisateur de hello et hello service Data Factory utilise les activités tooexecute hello.

Ce type de configuration est prise en charge pour les environnements de calcul suivant de hello :

* Azure HDInsight
* Azure Batch
* Azure Machine Learning
* Service Analytique Azure Data Lake
* Azure SQL DB, Azure SQL DW, SQL Server

## <a name="azure-hdinsight-linked-service"></a>Service lié Azure HDInsight
Vous pouvez créer un tooregister de service lié HDInsight Azure à votre propre cluster HDInsight avec la fabrique de données.

### <a name="example"></a>Exemple

```json
{
  "name": "HDInsightLinkedService",
  "properties": {
    "type": "HDInsight",
    "typeProperties": {
      "clusterUri": " https://<hdinsightclustername>.azurehdinsight.net/",
      "userName": "admin",
      "password": "<password>",
      "linkedServiceName": "MyHDInsightStoragelinkedService"
    }
  }
}
```

### <a name="properties"></a>Propriétés
| Propriété | Description | Requis |
| --- | --- | --- |
| type |propriété de type Hello doit être définie trop**HDInsight**. |Oui |
| clusterUri |Hello URI du cluster HDInsight de hello. |Oui |
| username |Spécifier le nom hello de hello utilisateur toobe utilisé cluster HDInsight existant de tooconnect tooan. |Oui |
| password |Spécifiez le mot de passe de compte d’utilisateur hello. |Oui |
| linkedServiceName | Nom du service lié Azure Storage qui fait référence le stockage d’objets blob Azure toohello de hello utilisé par hello cluster HDInsight. <p>Actuellement, vous ne pouvez pas spécifier un service lié Azure Data Lake Store pour cette propriété. Si le cluster HDInsight de hello a accès toohello Data Lake Store, vous pouvez accéder aux données Bonjour Azure Data Lake Store à partir de scripts Hive/Pig. </p>  |Oui |

## <a name="azure-batch-linked-service"></a>Service lié Azure Batch
Un pool de traitement par lots de la fabrique de données tooa de machines virtuelles (VM), vous pouvez créer un tooregister de service lié Azure Batch. Vous pouvez exécuter des activités personnalisées .NET à l'aide d'Azure Batch ou Azure HDInsight.

Consultez les rubriques suivantes si vous êtes de nouveau service de traitement par lots tooAzure :

* [Principes de base Azure Batch](../batch/batch-technical-overview.md) pour une vue d’ensemble de hello service Azure Batch.
* [Nouveau-AzureBatchAccount](https://msdn.microsoft.com/library/mt125880.aspx) toocreate de l’applet de commande un compte Azure Batch (ou) [portail Azure](../batch/batch-account-create-portal.md) compte de traitement par lots Azure hello toocreate à l’aide du portail Azure. Consultez [à l’aide de PowerShell toomanage du compte Azure Batch](http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx) rubrique pour obtenir des instructions détaillées sur l’utilisation d’applet de commande hello.
* [Nouveau-AzureBatchPool](https://msdn.microsoft.com/library/mt125936.aspx) toocreate de l’applet de commande un pool Azure Batch.

### <a name="example"></a>Exemple

```json
{
  "name": "AzureBatchLinkedService",
  "properties": {
    "type": "AzureBatch",
    "typeProperties": {
      "accountName": "<Azure Batch account name>",
      "accessKey": "<Azure Batch account key>",
      "poolName": "<Azure Batch pool name>",
      "linkedServiceName": "<Specify associated storage linked service reference here>"
    }
  }
}
```

Ajoutez «**.\< nom de la région\>**» toohello nom de votre compte batch hello **accountName** propriété. Exemple :

```json
"accountName": "mybatchaccount.eastus"
```

Une autre option est point de terminaison tooprovide hello batchUri comme indiqué dans hello suivant l’exemple :

```json
"accountName": "adfteam",
"batchUri": "https://eastus.batch.azure.com",
```

### <a name="properties"></a>Propriétés
| Propriété | Description | Requis |
| --- | --- | --- |
| type |propriété de type Hello doit être définie trop**AzureBatch**. |Oui |
| accountName |Nom du compte Azure Batch de hello. |Oui |
| accessKey |Clé d’accès pour hello compte Azure Batch. |Oui |
| poolName |Nom du pool hello d’ordinateurs virtuels. |Oui |
| linkedServiceName |Nom de hello service lié Azure Storage associé à ce service lié Azure Batch. Ce service lié est utilisé pour organiser des fichiers requis d’activité de hello toorun et le stockage des journaux de l’exécution d’activité hello. |Oui |

## <a name="azure-machine-learning-linked-service"></a>Service lié Microsoft Azure Machine Learning
Vous créez un tooregister de service lié Azure Machine Learning un lot d’apprentissage fabrique de données de point de terminaison tooa de calcul de score.

### <a name="example"></a>Exemple

```json
{
  "name": "AzureMLLinkedService",
  "properties": {
    "type": "AzureML",
    "typeProperties": {
      "mlEndpoint": "https://[batch scoring endpoint]/jobs",
      "apiKey": "<apikey>"
    }
  }
}
```

### <a name="properties"></a>Propriétés
| Propriété | Description | Requis |
| --- | --- | --- |
| Type |propriété de type Hello doit indiquer : **AzureML**. |Oui |
| mlEndpoint |lot Hello URL de calcul de score. |Oui |
| apiKey |Hello publiée API du modèle d’espace de travail. |Oui |

## <a name="azure-data-lake-analytics-linked-service"></a>Service lié Analytique Azure Data Lake
Vous créez un **Analytique de LAC de données Azure** lié service toolink une Analytique de LAC de données Azure compute service tooan Azure data factory. Hello activité Data Lake Analytique U-SQL dans le pipeline de hello fait référence toothis lié service. 

Hello tableau suivant fournit des descriptions pour hello propriétés génériques utilisées dans hello définition JSON. Vous pouvez ensuite choisir entre une authentification par principal de service et par informations d’identification utilisateur.

| Propriété | Description | Requis |
| --- | --- | --- |
| **type** |propriété de type Hello doit indiquer : **AzureDataLakeAnalytics**. |Oui |
| **accountName** |Nom du compte du service Analytique Azure Data Lake. |Oui |
| **dataLakeAnalyticsUri** |URI du service Analytique Azure Data Lake. |Non |
| **subscriptionId** |ID d’abonnement Azure |Non (si non spécifié, abonnement Hello fabrique de données est utilisée). |
| **resourceGroupName** |Nom du groupe de ressources Azure |Non (si non spécifié, groupe de ressources de hello fabrique de données est utilisée). |

### <a name="service-principal-authentication-recommended"></a>Authentification d’un principal du service (recommandée)
authentification principale du service toouse, inscrire une entité de l’application dans Azure Active Directory (Azure AD) et accordez à elle hello accéder à tooData Lake Store. Consultez la page [Authentification de service à service](../data-lake-store/data-lake-store-authenticate-using-active-directory.md) pour des instructions détaillées. Prenez note de hello après les valeurs que vous pouvez utiliser toodefine hello de service lié :
* ID de l'application
* Clé de l'application 
* ID client

Utilisez l’authentification principale du service en spécifiant hello propriétés suivantes :

| Propriété | Description | Requis |
|:--- |:--- |:--- |
| **servicePrincipalId** | Spécifiez l’ID client de. l’application hello | Oui |
| **servicePrincipalKey** | Spécifiez la clé de l’application hello. | Oui |
| **client** | Spécifiez les informations de locataire hello (ID client ou le nom de domaine) dans lequel réside votre application. Vous pouvez le récupérer par pointage de souris hello dans le coin supérieur droit de hello Hello portail Azure. | Oui |

**Exemple : authentification du principal de service**
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

### <a name="user-credential-authentication"></a>Authentification des informations d’identification utilisateur
Vous pouvez également utiliser authentification des informations d’identification utilisateur pour l’Analytique lac de données en spécifiant les propriétés suivantes de hello :

| Propriété | Description | Requis |
|:--- |:--- |:--- |
| **authorization** | Cliquez sur hello **Authorize** bouton Bonjour éditeur Data Factory et entrez vos informations d’identification qui affecte le propriété toothis URL hello générées automatiquement d’autorisation. | Oui |
| **sessionId** | ID de session OAuth à partir de la session de d’autorisation OAuth hello. Chaque ID de session est unique et ne peut être utilisé qu’une seule fois. Ce paramètre est automatiquement généré lorsque vous utilisez hello éditeur Data Factory. | Oui |

**Exemple : authentification des informations d’identification utilisateur**
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>", 
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

#### <a name="token-expiration"></a>Expiration du jeton
Hello code d’autorisation généré à l’aide de hello **Authorize** bouton expire après un certain temps. Consultez hello tableau suivant pour les délais d’expiration de hello pour différents types de comptes d’utilisateur. Hello message d’erreur suivant peut s’afficher lorsque hello authentification **expiration du jeton**: erreur de l’opération des informations d’identification : invalid_grant - AADSTS70002 : erreur de validation des informations d’identification. AADSTS70008 : hello fourni octroi d’accès est expiré ou révoqué. Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21-09-31Z ».

| Type d’utilisateur | Expire après |
|:--- |:--- |
| Comptes d’utilisateurs NON gérés par Azure Active Directory (@hotmail.com, @live.com, etc.) |12 heures |
| Comptes d’utilisateurs gérés par Azure Active Directory (AAD) |exécution de 14 jours après la dernière tranche de hello. <br/><br/>90 jours, si une tranche basée sur un service lié OAuth est exécutée au moins une fois tous les 14 jours. |

tooavoid/résoudre cette erreur, autorisez à nouveau à l’aide de hello **Authorize** bouton lorsque hello **expiration du jeton** et redéployez hello lié service. Vous pouvez également générer par programmation des valeurs pour les propriétés **sessionId** et **authorization** à l’aide du code suivant :

```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```

Consultez [AzureDataLakeStoreLinkedService classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), et [AuthorizationSessionGetResponse classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) pour plus d’informations sur les classes de fabrique de données hello utilisées dans le code hello. Ajoutez une référence à : Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll pour hello WindowsFormsWebAuthenticationDialog classe. 

## <a name="azure-sql-linked-service"></a>Service lié Azure SQL
Vous créez un service lié SQL Azure et l’utiliser avec hello [activité de procédure stockée](data-factory-stored-proc-activity.md) tooinvoke une procédure stockée à partir d’un pipeline de fabrique de données. Pour plus d’informations sur ce service lié, consultez la page [Connecteur SQL Azure](data-factory-azure-sql-connector.md#linked-service-properties) .

## <a name="azure-sql-data-warehouse-linked-service"></a>Service lié Azure SQL Data Warehouse
Vous créez un service Azure SQL Data Warehouse lié et l’utiliser avec hello [activité de procédure stockée](data-factory-stored-proc-activity.md) tooinvoke une procédure stockée à partir d’un pipeline de fabrique de données. Pour plus d’informations sur ce service lié, consultez la page [Connecteur Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) .

## <a name="sql-server-linked-service"></a>Service SQL Server lié
Vous créez un service lié SQL Server et l’utiliser avec hello [activité de procédure stockée](data-factory-stored-proc-activity.md) tooinvoke une procédure stockée à partir d’un pipeline de fabrique de données. Pour plus d’informations sur ce service lié, consultez la page [Connecteur SQL Server](data-factory-sqlserver-connector.md#linked-service-properties) .

