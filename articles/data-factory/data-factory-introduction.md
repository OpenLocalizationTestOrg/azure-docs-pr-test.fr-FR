---
title: "aaaIntroduction tooData fabrique, un service d’intégration de données | Documents Microsoft"
description: "Découvrez Azure Data Factory : un service d’intégration de données cloud qui gère et automatise le déplacement et la transformation des données."
keywords: "intégration de données, intégration de données cloud, description d’azure data factory"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: cec68cb5-ca0d-473b-8ae8-35de949a009e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 4cc30515315efc938951057743ff8eb3701214ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-data-factory"></a>Introduction tooAzure Data Factory 
## <a name="what-is-azure-data-factory"></a>qu'est-ce qu'Azure Data Factory ?
Dans le monde hello de données volumineuses, comment sont données existantes exploitées dans business ? Il est possible tooenrich les données générées dans le cloud de hello à l’aide de données de référence provenant de sources de données locales ou d’autres sources de données disparates ? Par exemple, une société de jeux collecte de journaux produites par les jeux dans le cloud de hello. Il veut tooanalyze ces observations journaux toogain toocustomer Préférences, les données démographiques, comportement de l’utilisation des possibilités croisées et la vente incitative de tooidentify etc., développer le nouveau champ croissance de l’activité toodrive fonctionnalités et fournir une meilleure expérience toocustomers. 

tooanalyze ces journaux, la société de hello a besoin de données de référence toouse hello telles que les informations du client, informations sur les jeux, les informations de campagne qui se trouve dans une banque de données locale de marketing. Par conséquent, la société de hello souhaite tooingest des données de journal à partir du magasin de données cloud hello et les données de référence à partir de la banque de données locale hello. Ensuite, traitement des données à l’aide de Hadoop Bonjour hello cloud (Azure HDInsight) et publier des résultats hello du magasin de données dans un entrepôt de données cloud comme Azure SQL Data Warehouse ou des données locales telles que SQL Server. Il veut toorun de ce flux de travail une fois par semaine qu’une seule fois. 

Ce qui est nécessaire est une plateforme qui permet à un flux de travail d’acquisition des données de locaux et cloud des magasins de données et les données de transformation ou de processus à l’aide des services de calcul existantes telles que Hadoop et publier hello résultats tooan local hello entreprise toocreate ou le magasin de données de cloud pour tooconsume d’applications BI. 

![Présentation de Data Factory](media/data-factory-introduction/what-is-azure-data-factory.png) 

Azure Data Factory est plateforme hello pour ce genre de scénarios. Il s’agit d’un **service d’intégration de données basés sur le cloud qui vous permet de toocreate flux de travail pilotés par les données dans le cloud hello pour orchestrer et automatiser le déplacement des données et transformation des données**. À l’aide d’Azure Data Factory, vous pouvez créer et planifier piloté par les données des flux de travail (appelé pipelines) qui peut réception des données à partir de différents magasins de données, processus/transformer les données de salutation à l’aide des services de calcul tels que Azure HDInsight Hadoop, Spark, Azure Data Lake Analytique et Azure Machine Learning et stocke les données toodata comme Azure SQL Data Warehouse pour tooconsume d’applications business intelligence (BI) de sortie de publication.  

Il s’agit plus d’une plateforme d’extraction et de chargement (EL) puis de transformation et chargement (TL) qu’une plateforme d’extraction, de transformation-et de chargement (ETL) traditionnelle. transformations Hello qui sont effectuées sont tootransform/traitement des données à l’aide des services de calcul plutôt que de transformations tooperform comme hello celles permettant d’ajouter des colonnes, en comptant le nombre de lignes, le tri des données, etc. dérivées. 

Actuellement, les données hello sont utilisées et produites par le flux de travail sont dans Azure Data Factory, **en tranches de temps des données** (horaire, quotidienne, hebdomadaire, etc..). Par exemple, un pipeline peut lire des données d’entrée, traiter des données et générer des données de sortie une fois par jour. Vous ne pouvez également exécuter un flux de travail qu’une seule fois.  
  

## <a name="how-does-it-work"></a>Comment cela fonctionne-t-il ? 
Généralement, les pipelines Hello (flux de travail pilotés par les données) dans Azure Data Factory effectuent hello trois comme suit :

![Trois étapes d’Azure Data Factory](media/data-factory-introduction/three-information-production-stages.png)

### <a name="connect-and-collect"></a>Se connecter et collecter
Les entreprises disposent de données de divers types situées dans des sources diverses. sources de hello requis tooconnect tooall de données est Hello première étape dans la création d’un système de production d’information et traitement, telles que les services SaaS, les services web, FTP, les partages de fichiers et déplacer l’emplacement en fonction des besoins de tooa centralisée des données hello pour suivantes lors du traitement.

Sans la fabrique de données, les entreprises doivent construire des composants de déplacement des données personnalisées ou d’écriture des services personnalisés toointegrate ces sources de données et le traitement. Il est coûteux et dur toointegrate maintenir ces systèmes et il lui manque souvent hello entreprise autorise surveillance et les alertes et les contrôles hello un service entièrement géré offre.

Avec la fabrique de données, vous pouvez utiliser hello activité de copie dans un pipeline de données toomove des données à la fois en local et cloud source données magasins tooa centralisation données magasin dans le cloud hello pour une analyse plus approfondie. Par exemple, vous pouvez collecter donnée hello Azure Data Lake Store et transformation plus tard à l’aide d’un service de calcul Analytique de LAC de données Azure. Vous pouvez aussi collecter des données dans un stockage Blob Azure, puis les transformer à l’aide d’un cluster Azure HDInsight Hadoop.

### <a name="transform-and-enrich"></a>Transformer et enrichir
Une fois que les données sont présentes dans un magasin de données centralisé dans le cloud de hello, que vous souhaitiez hello collectée données toobe traité ou transformées à l’aide des services de calcul tels que HDInsight Hadoop, Spark, Analytique lac de données et d’apprentissage. Vous souhaitez que des données de production transformée de tooreliably sur un environnements de production toofeed planification contrôlé et facile à gérer avec des données approuvées. 

### <a name="publish"></a>Publier 
Remettre les données transformées à partir du cloud de hello sources tooon local tel que SQL Server, ou conserver dans votre cloud des sources de stockage pour la consommation par décisionnel (BI) et les outils analytique et d’autres applications.

## <a name="key-components"></a>Composants clés
Un abonnement Azure peut contenir une ou plusieurs instances Azure Data Factory (ou fabriques de données). Azure Data Factory est composé de quatre composants clés qui coopèrent de plateforme de hello tooprovide sur lequel vous pouvez composer des flux de travail pilotés par les données avec les étapes toomove et transformer des données. 

### <a name="pipeline"></a>Pipeline
Une fabrique de données peut avoir un ou plusieurs pipelines. Un pipeline est un groupe d’activités. Ensemble, les activités hello dans un pipeline d’effectuent une tâche. Par exemple, un pipeline peut contenir un groupe d’activités qui reçoit des données à partir d’un objet blob Azure et puis exécutez une requête Hive sur les données de salutation toopartition un cluster HDInsight. Grâce à Hello cette est que ce pipeline hello vous permet des activités hello toomanage en tant qu’ensemble au lieu de chacune d’elles individuellement. Par exemple, vous pouvez déployer et planifier le pipeline hello, au lieu des activités hello indépendamment. 

### <a name="activity"></a>Activité
Un pipeline peut contenir une ou plusieurs activités. Activités définissent hello actions tooperform sur vos données. Par exemple, vous pouvez utiliser un copie activité toocopy de données à partir du magasin de données tooanother de données d’un magasin. De même, vous pouvez utiliser une activité Hive, qui s’exécute une requête Hive sur un tootransform de cluster Azure HDInsight ou analyser vos données. Data Factory prend en charge deux types d’activités : les activités de déplacement des données et les activités de transformation des données.

### <a name="data-movement-activities"></a>Activités de déplacement des données
Activité de copie dans la fabrique de données copie des données à partir d’un magasin de données de source données magasin tooa récepteur. Fabrique de données prend en charge hello suivant des magasins de données. Données à partir de n’importe quelle source peuvent être écrites tooany récepteur. Cliquez sur un toolearn de magasin de données comment tooand de données toocopy de ce magasin.

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

Pour plus d’informations, consultez l’article [Activités de déplacement des données](data-factory-data-movement-activities.md).

### <a name="data-transformation-activities"></a>Activités de transformation des données
[!INCLUDE [data-factory-transformation-activities](../../includes/data-factory-transformation-activities.md)]

Pour plus d’informations, consultez l’article [Activités de déplacement des données](data-factory-data-transformation-activities.md).

### <a name="custom-net-activities"></a>Activités .NET personnalisées
Si vous avez besoin des données toomove/à partir d’un magasin de données que l’activité de copie ne prend en charge, ou transformer des données à l’aide de votre propre logique, créez un **activité .NET personnalisée**. Pour plus d’informations sur la création et l’utilisation d’une activité personnalisée, consultez [Utilisation des activités personnalisées dans un pipeline Azure Data Factory](data-factory-use-custom-activities.md).

### <a name="datasets"></a>Groupes de données
Une activité accepte ou non des jeux de données en tant qu’entrées et produit un ou plusieurs jeux de données en tant que sorties. Jeux de données représente des structures de données dans les magasins de données hello, pointent simplement ou de référencent hello données toouse dans vos activités en tant qu’entrée ni sortie. Par exemple, un jeu de données d’objets Blob Azure Spécifie le conteneur d’objets blob hello et le dossier de stockage d’objets Blob Azure hello à partir de quels hello pipeline doit lire les données de hello. Ou bien, un jeu de données SQL Azure Table spécifie les données de sortie salutation table toowhich hello sont écrit par activité hello. 

### <a name="linked-services"></a>Services liés
Services liés ressemblent aux chaînes de connexion, qui définissent les informations de connexion hello requises pour les ressources de tooexternal tooconnect Data Factory. Considérer cette façon : un service lié définit la source de données toohello hello connexion et un jeu de données représente la structure hello de données de hello. Par exemple, un service lié Azure Storage Spécifie le compte Azure Storage toohello connexion chaîne tooconnect. Et un jeu de données d’objets Blob Azure Spécifie le conteneur d’objets blob hello et dossier hello qui contient les données de salutation.   

Data Factory fait appel aux services liés pour deux raisons :

* toorepresent un **magasin de données** , y compris, mais non limité à, un ordinateur local SQL Server, base de données Oracle, partage de fichiers ou un compte de stockage d’objets Blob Azure. Consultez hello [les activités de déplacement des données](#data-movement-activities) section pour obtenir la liste des magasins de données pris en charge.
* toorepresent un **ressources de calcul** qui peut héberger l’exécution de hello d’une activité. Par exemple, hello HDInsightHive activité s’exécute sur un cluster HDInsight Hadoop. Pour obtenir la liste des environnements de calcul pris en charge, consultez la section [Activités de transformation des données](#data-transformation-activities).

### <a name="relationship-between-data-factory-entities"></a>Relation entre des entités Data Factory
![Diagramme : Data Factory, un service d’intégration de données cloud - Concepts clés](./media/data-factory-introduction/data-integration-service-key-concepts.png)
**Figure 2.** Relations entre jeu de données, activité, pipeline et service lié

## <a name="supported-regions"></a>Régions prises en charge
Actuellement, vous pouvez créer des fabriques de données Bonjour **ouest des États-Unis**, **États-Unis**, et **Europe du Nord** régions. Toutefois, une fabrique de données peut accéder à des magasins de données et dans d’autres données relatives aux régions Azure toomove entre les magasins de données, les services de calcul ou des données de processus à l’aide des services de calcul.

Azure Data Factory ne permet pas en soi de stocker des données. Vous permet de créer des flux de travail pilotés par les données tooorchestrate les mouvements de données entre [prise en charge des magasins de données](#data-movement-activities) et le traitement des données à l’aide [les services de calcul](#data-transformation-activities) dans d’autres régions ou dans un site local environnement. Il vous permet également de trop[surveiller et gérer des flux de travail](data-factory-monitor-manage-pipelines.md) à la fois par programme et les mécanismes de l’interface utilisateur.

Bien que la fabrique de données est uniquement disponible dans **ouest des États-Unis**, **États-Unis**, et **Europe du Nord** régions, service hello mise sous tension le déplacement des données de hello dans la fabrique de données est disponible [globalement](data-factory-data-movement-activities.md#global) dans plusieurs régions. Si un magasin de données se trouve derrière un pare-feu, puis un [passerelle de gestion des données](data-factory-move-data-between-onprem-and-cloud.md) installé dans votre environnement local déplace les données hello à la place.

Supposons que vos environnements de calcul (cluster Azure HDInsight et Azure Machine Learning, par exemple) s’exécutent hors de la région Europe de l’ouest. Vous pouvez créer et utiliser une instance d’Azure Data Factory en Europe du Nord et utiliser les travaux tooschedule sur vos environnements de calcul en Europe de l’ouest. Il prend quelques millisecondes pour la tâche de Data Factory tootrigger hello sur votre environnement de calcul mais heure hello pour l’exécution du travail de hello sur votre environnement informatique ne change pas.

## <a name="get-started-with-creating-a-pipeline"></a>Prise en main de la création d’un pipeline
Vous pouvez utiliser un de ces outils ou les pipelines de données API toocreate dans Azure Data Factory : 

- Portail Azure
- Visual Studio
- PowerShell
- API .NET
- API REST
- Modèle Azure Resource Manager. 

toolearn comment toobuild les fabriques de données avec des données de pipeline, suivez les instructions détaillées dans hello suivant didacticiels :

| Didacticiel | Description |
| --- | --- |
| [Déplacer des données entre deux magasins de données cloud](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) |Dans ce didacticiel, vous créez une fabrique de données avec un pipeline qui **déplace les données** à partir de la base de données tooSQL de stockage Blob. |
| [Transformer des données à l’aide du cluster Hadoop](data-factory-build-your-first-pipeline.md) |Dans ce didacticiel, vous devez générer votre première fabrique de données Azure avec un pipeline de données qui **traite les données** en exécutant le script Hive sur un cluster Azure HDInsight (Hadoop). |
| [Déplacer des données entre une banque de données locale et une banque de données cloud à l’aide de la passerelle de gestion des données](data-factory-move-data-between-onprem-and-cloud.md) |Dans ce didacticiel, vous générez une fabrique de données avec un pipeline **déplace les données** d’une **local** tooan de base de données SQL Server blob Azure. Dans le cadre de la procédure pas à pas hello, vous installez et configurez hello passerelle de gestion des données sur votre ordinateur. |
