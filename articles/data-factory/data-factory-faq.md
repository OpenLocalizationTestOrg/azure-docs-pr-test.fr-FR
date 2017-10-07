---
title: aaaAzure Data Factory - Forum aux Questions
description: Forum aux Questions sur Azure Data Factory.
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 532dec5a-7261-4770-8f54-bfe527918058
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 78289fb4b6e15d74772af6c71ec25c7d2ca1a0bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---frequently-asked-questions"></a>Azure Data Factory - Forum aux Questions
## <a name="general-questions"></a>Questions générales
### <a name="what-is-azure-data-factory"></a>qu'est-ce qu'Azure Data Factory ?
Fabrique de données est basé sur un cloud service de l’intégration de données **automatise le déplacement de hello et la transformation des données**. Tout comme une fabrique qui s’exécute équipement tootake les matières premières et de leur transformation en produits finis, Data Factory orchestre des services existants qui collectent des données brutes et transforment en informations de prêt à l’emploi.

Fabrique de données vous permet de données de toomove de flux de travail pilotés par les données toocreate entre à la fois localement et les magasins de données cloud ainsi que processus/transformer des données à l’aide des services de calcul tels que Azure HDInsight et Analytique de LAC de données Azure. Après avoir créé un pipeline qui effectue l’action hello dont vous avez besoin, vous pouvez la planifier toorun régulièrement (horaire, quotidienne, hebdomadaire, etc.).   

Pour plus d’informations, consultez [Vue d’ensemble et concepts clés](data-factory-introduction.md).

### <a name="where-can-i-find-pricing-details-for-azure-data-factory"></a>où puis-je trouver des informations de tarification pour Azure Data Factory ?
Consultez [page de tarification de la fabrique de données] [ adf-pricing-details] pour hello tarification pour hello Azure Data Factory.  

### <a name="how-do-i-get-started-with-azure-data-factory"></a>comment prendre en main Azure Data Factory ?
* Pour une vue d’ensemble d’Azure Data Factory, consultez [Introduction tooAzure Data Factory](data-factory-introduction.md).
* Pour obtenir un didacticiel sur la façon de trop**les données de copie/déplacement** à l’aide de l’activité de copie, consultez [copier les données de stockage d’objets Blob Azure tooAzure base de données SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
* Pour obtenir un didacticiel sur la façon de trop**transformer des données** à l’aide d’activité de la ruche HDInsight. Consultez [Traiter des données en exécutant un script Hive sur un cluster Hadoop](data-factory-build-your-first-pipeline.md)

### <a name="what-is-hello-data-factorys-region-availability"></a>Quelle est la disponibilité de la région de la fabrique de données hello ?
Data Factory est disponible dans les régions **Ouest des États-Unis** et **Europe du Nord**. calcul de Hello et services de stockage utilisés par les fabriques de données peuvent être dans d’autres régions. Consultez [Régions prises en charge](data-factory-introduction.md#supported-regions).

### <a name="what-are-hello-limits-on-number-of-data-factoriespipelinesactivitiesdatasets"></a>Quelles sont les limites de hello sur le nombre de fabriques de données/pipelines/activités/datasets ?
Consultez **limites de fabrique de données Azure** section Hello [abonnement Azure et limites de Service, Quotas et contraintes](../azure-subscription-service-limits.md#data-factory-limits) l’article.

### <a name="what-is-hello-authoringdeveloper-experience-with-azure-data-factory-service"></a>Nouveautés d’expérience de création/développeur hello avec le service Azure Data Factory ?
Vous pouvez créer/créer des fabriques de données à l’aide d’une des hello suivant outils/kits de développement logiciel :

* **Portail Azure** panneaux de Data Factory hello Bonjour Azure portal fournit interface utilisateur élaborée pour vous toocreate données fabriques ad lié services. Hello **éditeur Data Factory**, qui fait également partie du portail de hello, vous permet de tooeasily créer des services liés, les tables, les jeux de données et les pipelines en spécifiant des définitions de JSON pour ces artefacts. Consultez [générer votre première pipeline de données à l’aide du portail Azure](data-factory-build-your-first-pipeline-using-editor.md) pour un exemple d’utilisation hello / l’Éditeur du portail toocreate et déployer une fabrique de données.
* **Visual Studio** vous pouvez utiliser Visual Studio toocreate une fabrique de données Azure. Pour plus d’informations, consultez [Créer votre premier pipeline de données à l’aide de Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) .
* **Azure PowerShell** : consultez [Créer et surveiller Azure Data Factory à l’aide d’Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md) pour obtenir un didacticiel/une procédure pas à pas pour créer une fabrique de données à l’aide de PowerShell. Consultez [Informations de référence sur les applets de commande Data Factory][adf-powershell-reference] dans la bibliothèque MSDN pour obtenir une documentation complète sur les applets de commande Data Factory.
* **Bibliothèque de classes .NET** Vous pouvez créer par programmation des fabriques de données à l'aide du Kit de développement logiciel (SDK) Data Factory .NET. Consultez [Créer, surveiller et gérer des fabriques de données à l'aide du Kit de développement logiciel (SDK) .NET](data-factory-create-data-factories-programmatically.md) pour découvrir comment créer une fabrique de données à l'aide du Kit de développement logiciel (SDK) .NET. Consultez [Informations de référence sur la bibliothèque de classes Data Factory][msdn-class-library-reference] pour obtenir une documentation complète sur le Kit de développement logiciel (SDK) Data Factory .NET.
* **API REST** vous pouvez également utiliser hello API REST exposées par toocreate de service Azure Data Factory hello et déployer des fabriques de données. Consultez [Informations de référence sur l’API REST Data Factory][msdn-rest-api-reference] pour obtenir une documentation complète de l’API REST Data Factory.
* **Modèle Azure Resource Manager** Consultez [Didacticiel : concevoir votre première fabrique de données Azure à l’aide du modèle Azure Resource Manager](data-factory-build-your-first-pipeline-using-arm.md) pour plus d’informations.

### <a name="can-i-rename-a-data-factory"></a>Puis-je renommer une fabrique de données ?
Non. Comme d’autres ressources Azure, les nom de hello d’une fabrique de données Azure ne peut pas être modifié.

### <a name="can-i-move-a-data-factory-from-one-azure-subscription-tooanother"></a>Puis-je déplacer une fabrique de données à partir d’un abonnement Azure tooanother ?
Oui. Hello d’utilisation **déplacer** bouton sur le panneau de fabrique de données, comme indiqué dans hello suivant schéma :

![Déplacer la fabrique de données](media/data-factory-faq/move-data-factory.png)

### <a name="what-are-hello-compute-environments-supported-by-data-factory"></a>Quelles sont les environnements de calcul hello pris en charge par la fabrique de données ?
Hello tableau suivant fournit une liste des environnements de calcul pris en charge par les activités de fabrique de données et hello pouvant s’exécuter sur ces derniers.

| Environnement de calcul | activités |
| --- | --- |
| [Cluster HDInsight à la demande](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) ou [votre propre cluster HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) |[DotNet](data-factory-use-custom-activities.md), [Hive](data-factory-hive-activity.md), [Pig](data-factory-pig-activity.md), [MapReduce](data-factory-map-reduce.md), [Diffusion en continu Hadoop](data-factory-hadoop-streaming-activity.md) |
| [Azure Batch](data-factory-compute-linked-services.md#azure-batch-linked-service) |[DotNet](data-factory-use-custom-activities.md) |
| [Azure Machine Learning](data-factory-compute-linked-services.md#azure-machine-learning-linked-service) |[Activités Machine Learning : exécution de lot et mise à jour de ressource](data-factory-azure-ml-batch-execution-activity.md) |
| [Service Analytique Azure Data Lake](data-factory-compute-linked-services.md#azure-data-lake-analytics-linked-service) |[Langage U-SQL du service Analytique Data Lake](data-factory-usql-activity.md) |
| [Azure SQL](data-factory-compute-linked-services.md#azure-sql-linked-service), [Azure SQL Data Warehouse](data-factory-compute-linked-services.md#azure-sql-data-warehouse-linked-service), [SQL Server](data-factory-compute-linked-services.md#sql-server-linked-service) |[Procédure stockée](data-factory-stored-proc-activity.md) |

### <a name="how-does-azure-data-factory-compare-with-sql-server-integration-services-ssis"></a>Comparaison d’Azure Data Factory avec SQL Server Integration Services (SSIS) 
Consultez hello [vs d’Azure Data Factory. et SSIS](http://www.sqlbits.com/Sessions/Event15/Azure_Data_Factory_vs_SSIS) faite par un de nos MVP (Most Valued Professional), Reza Rad. Certaines des modifications récentes de hello dans la fabrique de données peut ne pas figurer dans le jeu de diapositives hello. Nous ajoutons en permanence plusieurs fonctionnalités tooAzure Data Factory. Nous ajoutons en permanence plusieurs fonctionnalités tooAzure Data Factory. Nous s’intégrer ces mises à jour dans la comparaison hello de technologies d’intégration de données à partir de Microsoft un peu plus tard cette année.   

## <a name="activities---faq"></a>Activités - Forum Aux Questions
### <a name="what-are-hello-different-types-of-activities-you-can-use-in-a-data-factory-pipeline"></a>Quelles sont les hello différents types d’activités que vous pouvez utiliser dans un pipeline de fabrique de données ?
* [Activités de déplacement des données](data-factory-data-movement-activities.md) toomove données.
* [Activités de Transformation des données](data-factory-data-transformation-activities.md) tooprocess/transformer des données.

### <a name="when-does-an-activity-run"></a>Quand une activité s'exécute-t-elle ?
Hello **disponibilité** hello de paramètre de configuration de sortie détermine de table de données lorsque l’activité hello est exécutée. Si des jeux de données d’entrée est spécifiées, activité hello vérifie si toutes les dépendances de données d’entrée hello sont satisfaites (autrement dit, **prêt** état) avant l’exécution.

## <a name="copy-activity---faq"></a>Activité de copie - Forum Aux Questions
### <a name="is-it-better-toohave-a-pipeline-with-multiple-activities-or-a-separate-pipeline-for-each-activity"></a>Il est mieux toohave un pipeline avec plusieurs activités ou un pipeline distinct pour chaque activité ?
Pipelines sont censés toobundle des activités connexes. Si les datasets hello qui les relient ne sont pas consommés par toute autre activité en dehors du pipeline de hello, vous pouvez conserver les activités hello dans un pipeline. De cette manière, vous devez pas période active du pipeline toochain afin qu’ils s’alignent sur eux. En outre, hello l’intégrité des données dans les tables hello toohello interne pipeline est mieux préservé lors de la mise à jour du pipeline de hello. Mise à jour du pipeline essentiellement arrête toutes les activités de hello dans le pipeline de hello, les supprime et crée les à nouveau. À partir de la création du point de vue, il peut également être des flux de hello toosee plus facilement des données au sein de hello liée activités dans JSON d’un fichier pour le pipeline de hello.

### <a name="what-are-hello-supported-data-stores"></a>Quelles sont les hello prise en charge des magasins de données ?
Activité de copie dans la fabrique de données copie des données à partir d’un magasin de données de source données magasin tooa récepteur. Fabrique de données prend en charge hello suivant des magasins de données. Données à partir de n’importe quelle source peuvent être écrites tooany récepteur. Cliquez sur un toolearn de magasin de données comment tooand de données toocopy de ce magasin.

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> Stocke des données avec * peut être local ou sur Azure IaaS et vous obligent tooinstall [passerelle de gestion des données](data-factory-data-management-gateway.md) sur un ordinateur de IaaS Azure/le local.

### <a name="what-are-hello-supported-file-formats"></a>Quelles sont les hello pris en charge les formats de fichier ?
[!INCLUDE [data-factory-file-format](../../includes/data-factory-file-format.md)]

### <a name="where-is-hello-copy-operation-performed"></a>Où l’opération de copie hello est effectuée ?
Consultez la section relative au [déplacement des données disponibles à l’échelle mondiale](data-factory-data-movement-activities.md#global) pour plus d’informations. En bref, lorsqu’une banque de données locale est impliquée, opération de copie hello est effectuée par hello passerelle de gestion des données dans votre environnement local. Et, lorsque le déplacement des données de hello est entre deux magasins de cloud, opération de copie de hello est effectuée dans hello région emplacement le plus proche toohello récepteur Bonjour même geography.

## <a name="hdinsight-activity---faq"></a>Activité de HDInsight - Forum Aux Questions
### <a name="what-regions-are-supported-by-hdinsight"></a>Quelles sont les régions prises en charge par HDInsight ?
Consultez hello section disponibilité géographique dans l’article suivant de hello : ou [tarification HDInsight][hdinsight-supported-regions].

### <a name="what-region-is-used-by-an-on-demand-hdinsight-cluster"></a>quelle est la région utilisée par un cluster HDInsight à la demande ?
Bonjour à la demande HDInsight cluster est créé dans hello même région où le stockage hello toobe utilisé avec hello cluster spécifié existe.    

### <a name="how-tooassociate-additional-storage-accounts-tooyour-hdinsight-cluster"></a>Comment les comptes de stockage supplémentaire de tooassociate tooyour HDInsight cluster ?
Si vous utilisez votre propre HDInsight Cluster (BYOC - mettre de votre propre Cluster), consultez hello rubriques suivantes :

* [Utilisation d’un cluster HDInsight avec des comptes de stockage et des metastores secondaires][hdinsight-alternate-storage]
* [Utilisation de comptes de stockage supplémentaires avec Hive HDInsight][hdinsight-alternate-storage-2]

Si vous utilisez un cluster à la demande qui est créé par le service Data Factory de hello, spécifiez les comptes de stockage supplémentaires pour hello HDInsight le service lié afin que le service de fabrique de données hello de les inscrire à votre place. Bonjour définition JSON pour le service lié à la demande de hello, utilisez **additionalLinkedServiceNames** comptes de stockage de remplacement de propriété toospecify comme indiqué dans hello suivant extrait de code JSON :

```JSON
{
    "name": "MyHDInsightOnDemandLinkedService",
    "properties":
    {
        "type": "HDInsightOnDemandLinkedService",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "LinkedService-SampleData",
            "additionalLinkedServiceNames": [ "otherLinkedServiceName1", "otherLinkedServiceName2" ]
        }
    }
}
```
Dans l’exemple hello ci-dessus, otherLinkedServiceName1 et otherLinkedServiceName2 représentent les services liés dont les définitions contiennent des informations d’identification que hello des comptes de stockage de remplacement tooaccess HDInsight cluster besoins.

## <a name="slices---faq"></a>Tranches - Forum Aux Questions
### <a name="why-are-my-input-slices-not-in-ready-state"></a>Pourquoi mes tranches d’entrée ne sont-elles pas à l’état Prêt ?
Une erreur courante n’affecte pas **externe** propriété trop**true** sur hello dataset d’entrée lorsque les données d’entrée hello est la fabrique de données externe toohello (ne pas produit par la fabrique de données hello).

Dans l’exemple suivant de hello, vous ne devez tooset **externe** tootrue sur **dataset1**.  

**DataFactory1** Pipeline 1 : dataset1 -&gt; activity1 -&gt; dataset2 -&gt; activity2 -&gt; dataset3 Pipeline 2 : dataset3-&gt; activity3 -&gt; dataset4

Si vous avez un autre fabrique de données avec un pipeline qui prend dataset4 (généré par le pipeline 2 dans la fabrique de données 1), marquez dataset4 comme un jeu de données externe, car le jeu de données hello est généré par une fabrique de données différentes (DataFactory1, pas DataFactory2).  

**DataFactory2**    
Pipeline 1 : dataset4->activity4->dataset5

Si la propriété external de hello est définie correctement, vérifiez si les données d’entrée hello existent à l’emplacement de hello spécifié dans la définition du dataset d’entrée hello.

### <a name="how-toorun-a-slice-at-another-time-than-midnight-when-hello-slice-is-being-produced-daily"></a>Comment toorun un secteur à un autre moment à minuit si le secteur de hello est en cours produit tous les jours ?
Hello d’utilisation **offset** propriété toospecify hello heure à laquelle hello tranche toobe généré. Pour plus d’informations sur cette propriété, consultez la section [Disponibilité du jeu de données](data-factory-create-datasets.md#dataset-availability) . Voici un exemple rapide :

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
Début des tranches quotidiennes à **6 h 00** au lieu de minuit par défaut de hello.     

### <a name="how-can-i-rerun-a-slice"></a>Comment puis-je réexécuter une tranche ?
Vous pouvez réexécuter une tranche dans un des hello suivant façons :

* Utilisez surveiller et gérer une application toorerun une fenêtre d’activité ou la tranche. Pour obtenir des instructions, consultez [Réexécuter les fenêtres d’activité sélectionnées](data-factory-monitor-manage-app.md#perform-batch-actions) .   
* Cliquez sur **exécuter** dans la barre de commandes de hello en hello **tranche de données** Panneau de la tranche de hello Bonjour portail Azure.
* Exécutez **Set-AzureRmDataFactorySliceStatus** applet de commande avec l’état défini trop**attente** de la tranche de hello.   

    ```PowerShell
    Set-AzureRmDataFactorySliceStatus -Status Waiting -ResourceGroupName $ResourceGroup -DataFactoryName $df -TableName $table -StartDateTime "02/26/2015 19:00:00" -EndDateTime "02/26/2015 20:00:00"
    ```
Consultez [Set-AzureRmDataFactorySliceStatus] [ set-azure-datafactory-slice-status] pour plus d’informations sur l’applet de commande hello.

### <a name="how-long-did-it-take-tooprocess-a-slice"></a>La durée pendant laquelle elle a duré tooprocess une tranche ?
Utiliser l’Explorateur de fenêtre d’activité dans tooknow moniteur & application de gérer la durée pendant laquelle elle a duré tooprocess une tranche de données. Pour plus d’informations, consultez [Explorateur de fenêtres d’activité](data-factory-monitor-manage-app.md#activity-window-explorer) .

Vous pouvez également effectuer hello suivant Bonjour portail Azure :  

1. Cliquez sur **Datasets** vignette sur hello **DATA FACTORY** Panneau de votre fabrique de données.
2. Cliquez sur le jeu de données spécifique hello sur hello **Datasets** panneau.
3. Tranche hello SELECT qui vous intéressez dans hello **tranches récentes** liste hello **TABLE** panneau.
4. Cliquez sur Exécuter à partir de hello : activité hello **activité** liste hello **tranche de données** panneau.
5. Cliquez sur **propriétés** vignette sur hello **détails de l’activité exécuter** panneau.
6. Vous devez voir hello **durée** champ avec une valeur. Cette valeur est la durée de hello la tranche de hello tooprocess.   

### <a name="how-toostop-a-running-slice"></a>Comment toostop une tranche en cours d’exécution ?
Si vous avez besoin de pipeline de hello toostop à partir de l’exécution, vous pouvez utiliser [Suspend-AzureRmDataFactoryPipeline](/powershell/module/azurerm.datafactories/suspend-azurermdatafactorypipeline) applet de commande. Actuellement, la suspension du pipeline de hello n’arrête pas les exécutions de tranche hello qui sont en cours d’exécution. Une fois que les exécutions en cours hello terminer, aucune coupe n’est récupéré.

Si vous voulez vraiment toostop toutes les exécutions de hello immédiatement, hello uniquement de façon serait toodelete hello pipeline et recréez-le. Si vous choisissez de pipeline de hello toodelete, il est inutile toodelete tables et les services liés utilisés par le pipeline de hello.

[create-factory-using-dotnet-sdk]: data-factory-create-data-factories-programmatically.md
[msdn-class-library-reference]: /dotnet/api/microsoft.azure.management.datafactories.models
[msdn-rest-api-reference]: /rest/api/datafactory/

[adf-powershell-reference]: /powershell/resourcemanager/azurerm.datafactories/v2.3.0/azurerm.datafactories
[azure-portal]: http://portal.azure.com
[set-azure-datafactory-slice-status]: /powershell/resourcemanager/azurerm.datafactories/v2.3.0/set-azurermdatafactoryslicestatus

[adf-pricing-details]: http://go.microsoft.com/fwlink/?LinkId=517777
[hdinsight-supported-regions]: http://azure.microsoft.com/pricing/details/hdinsight/
[hdinsight-alternate-storage]: http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx
[hdinsight-alternate-storage-2]: http://blogs.msdn.com/b/cindygross/archive/2014/05/05/use-additional-storage-accounts-with-hdinsight-hive.aspx
