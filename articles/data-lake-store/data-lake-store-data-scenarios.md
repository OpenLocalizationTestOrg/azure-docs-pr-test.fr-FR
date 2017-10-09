---
title: "scénarios aaaData Data Lake Store | Documents Microsoft"
description: "Comprendre hello différents scénarios et outils à l’aide des données peuvent ingérée, traitées, téléchargées et visualisées dans un magasin Data Lake Store"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 37409a71-a563-4bb7-bc46-2cbd426a2ece
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: caaa3979b8a2532089778c3e3db3c711714d3c42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-data-lake-store-for-big-data-requirements"></a>Utilisation d’Azure Data Lake Store pour les données volumineuses
Il existe quatre étapes principales dans traitement des données Big Data :

* Réception de grandes quantités de données dans un magasin de données, en temps réel ou par lots
* Le traitement des données de hello
* Téléchargement des données de hello
* Visualisation des données de hello

Dans cet article, nous examinons ces étapes avec respect tooAzure Data Lake Store toounderstand hello options et outils disponible toomeet vos besoins de données volumineuses.

## <a name="ingest-data-into-data-lake-store"></a>Réception de données dans Data Lake Store
Cette section met en évidence hello différentes sources de données et hello différentes façons dans lequel ces données peuvent être transférées à un compte Data Lake Store.

![Réception de données dans Data Lake Store](./media/data-lake-store-data-scenarios/ingest-data.png "Réception de données dans Data Lake Store")

### <a name="ad-hoc-data"></a>Données ad hoc
Ceci représente les petits jeux de données qui sont utilisés pour créer un prototype d’une application de Big Data. Il existe différentes façons de réception ad hoc des données en fonction de la source de hello de données de hello.

| source de données | Réception avec |
| --- | --- |
| Ordinateur local |<ul> <li>[Portail Azure](/data-lake-store-get-started-portal.md)</li> <li>[Azure PowerShell](data-lake-store-get-started-powershell.md)</li> <li>[Interface CLI 2.0 inter-plateforme Azure](data-lake-store-get-started-cli-2.0.md)</li> <li>[Utilisation de Data Lake Tools pour Visual Studio](../data-lake-analytics/data-lake-analytics-data-lake-tools-get-started.md) </li></ul> |
| Azure Storage Blob |<ul> <li>[Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md)</li> <li>[l’outil AdlCopy](data-lake-store-copy-data-azure-storage-blob.md)</li><li>[DistCp en cours d’exécution sur un cluster HDInsight](data-lake-store-copy-data-wasb-distcp.md)</li> </ul> |

### <a name="streamed-data"></a>Flux de données
Ceci représente les données qui peuvent être générées par diverses sources, telles que des applications, des appareils, des capteurs, etc. Ces données peuvent être reçues dans un Data Lake Store par des outils divers. Ces outils sont généralement capturer et à traiter les données hello sur une base d’événement-événement dans en temps réel et puis écrire les événements hello par lots dans Data Lake Store afin qu’ils peuvent être traités davantage.

Voici les outils que vous pouvez utiliser :

* [Analytique de flux de données Azure](../stream-analytics/stream-analytics-data-lake-output.md) -événements ingérés aux concentrateurs d’événements peuvent être écrits tooAzure Data Lake à l’aide d’une sortie d’Azure Data Lake Store.
* [Azure HDInsight Storm](../hdinsight/hdinsight-storm-write-data-lake-store.md) -vous pouvez écrire des données directement tooData Lake Store à partir de hello cluster Storm.
* [EventProcessorHost](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md) – vous pouvez recevoir des événements de concentrateurs d’événements et puis réécrire tooData Lake Store à l’aide de hello [Data Lake Store .NET SDK](data-lake-store-get-started-net-sdk.md).

### <a name="relational-data"></a>Données relationnelles
Les bases de données relationnelles peuvent également être utilisées comme sources des données. Sur une période donnée, les bases de données relationnelles collectent de grandes quantités de données qui peuvent fournir des informations clés si elles sont traitées via un pipeline de Big Data. Vous pouvez utiliser hello suivant outils toomove ces données dans Data Lake Store.

* [Apache Sqoop](data-lake-store-data-transfer-sql-sqoop.md)
* [Azure Data Factory](../data-factory/data-factory-data-movement-activities.md)

### <a name="web-server-log-data-upload-using-custom-applications"></a>Données de journal de serveur web (téléchargement à l’aide d’applications personnalisées)
Ce type de jeu de données est spécifiquement appelé, car l’analyse des données de journal de serveur web est un cas d’usage courant pour les applications de données volumineuses et nécessite des volumes importants de toobe des fichiers journaux téléchargement toohello Data Lake Store. Vous pouvez utiliser des hello suivant outils toowrite tooupload de vos propres scripts ou applications ces données.

* [Interface CLI 2.0 inter-plateforme Azure](data-lake-store-get-started-cli-2.0.md)
* [Azure PowerShell](data-lake-store-get-started-powershell.md)
* [Kit de développement logiciel (SDK) .NET Azure Data Lake Store](data-lake-store-get-started-net-sdk.md)
* [Azure Data Factory](../data-factory/data-factory-data-movement-activities.md)

Pour télécharger les données de journal de serveur web et également pour le téléchargement des autres types de données (par exemple, les données d’éléments social), il est une bonne approche toowrite vos propres scripts personnalisées et d’applications, car elle vous donne hello flexibilité tooinclude vos données de composant dans le cadre de téléchargement de votre application de données plus volumineuse. Dans certains cas, ce code peut prendre hello forme un script ou d’un utilitaire de ligne de commande simple. Dans d’autres cas, code de hello peut être utilisé toointegrate big le traitement des données dans une application métier ou de la solution.

### <a name="data-associated-with-azure-hdinsight-clusters"></a>Données associées aux clusters Azure HDInsight
La plupart des types de clusters HDInsight (Hadoop, HBase, Storm) prend en charge Data Lake Store comme référentiel de stockage des données. Les clusters HDInsight accèdent aux données à partir des objets blob d’Azure Storage (WASB). Pour de meilleures performances, vous pouvez copier des données de la hello de WASB dans un compte Data Lake Store associé hello cluster. Vous pouvez utiliser hello outils toocopy hello données suivantes.

* [Apache DistCp](data-lake-store-copy-data-wasb-distcp.md)
* [AdlCopy Service](data-lake-store-copy-data-azure-storage-blob.md)
* [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md)

### <a name="data-stored-in-on-premises-or-iaas-hadoop-clusters"></a>Données stockées localement ou dans des clusters IaaS Hadoop
De grandes quantités de données peuvent être stockées dans des clusters Hadoop existants, localement sur les ordinateurs à l’aide de HDFS. les clusters Hadoop Hello est peut-être dans un déploiement sur site ou est peut-être dans un cluster IaaS dans Azure. Il peut être exigences toocopy ce données tooAzure Data Lake Store une approche uniques ou de manière périodique. Il existe plusieurs options que vous pouvez l’utiliser tooachieve. Voici une liste d’alternatives et hello associés compromis.

| Approche | Détails | Avantages | Considérations |
| --- | --- | --- | --- |
| Utiliser des données toocopy de fabrique de données Azure (ADF) directement à partir de Hadoop clusters tooAzure Data Lake Store |[ADF prend en charge HDFS comme source de données](../data-factory/data-factory-hdfs-connector.md) |ADF offre une prise en charge immédiate de HDFS ainsi qu’une gestion et une surveillance de bout en bout de premier ordre |Nécessite la passerelle de gestion des données toobe déployés localement ou dans un cluster IaaS de hello |
| Exportez les données depuis Hadoop sous forme de fichiers. Copiez ensuite hello fichiers tooAzure Data Lake Store à l’aide du mécanisme approprié. |Vous pouvez copier à l’aide de fichiers tooAzure Data Lake Store : <ul><li>[Azure PowerShell pour système d'exploitation Windows](data-lake-store-get-started-powershell.md)</li><li>[Interface CLI 2.0 inter-plateforme Azure pour système d’exploitation non Windows](data-lake-store-get-started-cli-2.0.md)</li><li>Application personnalisée utilisant n’importe quel SDK Data Lake Store</li></ul> |Tooget rapide a démarré. Permet des téléchargements personnalisés |Processus en plusieurs étapes qui implique différentes technologies. Gestion et surveillance augmentera toobe une vérification sur la nature de hello personnalisé étant donné des outils de hello |
| Utiliser des données de toocopy Distcp à partir de Hadoop tooAzure stockage. Copier les données à partir d’Azure Storage tooData Lake Store à l’aide du mécanisme approprié. |Vous pouvez copier des données à partir d’Azure Storage tooData Lake Store à l’aide de : <ul><li>[Azure Data Factory](../data-factory/data-factory-data-movement-activities.md)</li><li>[l’outil AdlCopy](data-lake-store-copy-data-azure-storage-blob.md)</li><li>[pache DistCp en cours d’exécution sur des clusters HDInsight](data-lake-store-copy-data-wasb-distcp.md)</li></ul> |Vous pouvez utiliser des outils open source. |Processus en plusieurs étapes qui implique différentes technologies |

### <a name="really-large-datasets"></a>Jeux de données très volumineux
Pour le téléchargement des jeux de données qui vont dans plusieurs téraoctets, à l’aide de méthodes hello décrites ci-dessus peut parfois être lente et coûteuse. Dans ce cas, vous pouvez utiliser les options de hello ci-dessous.

* **Utilisation d’Azure ExpressRoute**. Azure ExpressRoute vous permet de créer des connexions privées entre les infrastructures et les centres de données Azure dans votre environnement local. Ceci constitue une option fiable pour le transfert de grandes quantités de données. Pour plus d’informations, consultez la [Documentation Azure ExpressRoute](../expressroute/expressroute-introduction.md).
* **Téléchargement « hors connexion » des données**. Si l’utilisation d’Azure ExpressRoute n’est pas possible pour une raison quelconque, vous pouvez utiliser [service Azure Import/Export](../storage/common/storage-import-export-service.md) tooship des lecteurs de disque dur avec votre centre de données Azure tooan données. Vos données sont des objets BLOB de stockage tooAzure téléchargé premier. Vous pouvez ensuite utiliser [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md) ou [AdlCopy outil](data-lake-store-copy-data-azure-storage-blob.md) toocopy des données à partir d’objets BLOB de stockage Azure tooData Lake Store.

  > [!NOTE]
  > Alors que l’aide de hello service Import/Export, tailles des fichiers hello sur hello center de disques que vous expédiez tooAzure données ne doivent pas être supérieures à 195 go.
  >
  >

## <a name="process-data-stored-in-data-lake-store"></a>Traitement des données stockées dans Data Lake Store
Une fois que les données de salutation sont disponibles dans Data Lake Store vous pouvez exécuter analysis sur que les données à l’aide de hello pris en charge les applications de données volumineuses. Actuellement, vous pouvez utiliser des tâches d’analyse des données toorun Azure HDInsight et Analytique de LAC de données Azure sur les données de hello stockées dans Data Lake Store.

![Analyse des données dans Data Lake Store](./media/data-lake-store-data-scenarios/analyze-data.png "Analyse des données dans Data Lake Store")

Vous pouvez examiner hello exemple suivant.

* [Créer un cluster HDInsight avec Data Lake Store comme stockage.](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Utiliser Azure Data Lake Analytics avec Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)

## <a name="download-data-from-data-lake-store"></a>Téléchargement de données à partir de Data Lake Store
Vous pourrez également souhaitez toodownload ou déplacer des données à partir d’Azure Data Lake Store pour les scénarios tels que :

* Déplacer les données tooother référentiels toointerface avec vos pipelines de traitement des données existantes. Par exemple, vous pourriez toomove des données à partir de Data Lake Store tooAzure base de données SQL ou SQL Server locale.
* Télécharger l’ordinateur local de données tooyour pour le traitement dans des environnements IDE lors de la création de prototypes d’application.

![Sortie des données à partir de Data Lake Store](./media/data-lake-store-data-scenarios/egress-data.png "Sortie des données à partir de Data Lake Store")

Dans ce cas, vous pouvez utiliser une des options suivantes de hello :

* [Apache Sqoop](data-lake-store-data-transfer-sql-sqoop.md)
* [Azure Data Factory](../data-factory/data-factory-data-movement-activities.md)
* [Apache DistCp](data-lake-store-copy-data-wasb-distcp.md)

Vous pouvez également utiliser hello suivant les méthodes toowrite vos propres données de toodownload/application de script à partir de Data Lake Store.

* [Interface CLI 2.0 inter-plateforme Azure](data-lake-store-get-started-cli-2.0.md)
* [Azure PowerShell](data-lake-store-get-started-powershell.md)
* [Kit de développement logiciel (SDK) .NET Azure Data Lake Store](data-lake-store-get-started-net-sdk.md)

## <a name="visualize-data-in-data-lake-store"></a>Visualisation des données dans Data Lake Store
Vous pouvez utiliser un mélange de représentations visuelles de services toocreate des données stockées dans Data Lake Store.

![Visualisation des données dans Data Lake Store](./media/data-lake-store-data-scenarios/visualize-data.png "Visualisation des données dans Data Lake Store")

* Vous pouvez démarrer à l’aide de [données toomove de Azure Data Factory à partir de Data Lake Store tooAzure SQL Data Warehouse](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats)
* Après cela, vous pouvez [intégrer Power BI avec Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-integrate-power-bi.md) toocreate la représentation visuelle des données de hello.
