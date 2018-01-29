---
title: "Comparer les versions 1 et 2 d’Azure Data Factory | Microsoft Docs"
description: Cet article compare Azure Data Factory V1 et Azure Data Factory V2.
services: data-factory
documentationcenter: 
author: kromerm
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/24/2018
ms.author: makromer
ms.openlocfilehash: 83065e6cacd784a3914cfac3ff2552a712688366
ms.sourcegitcommit: 79683e67911c3ab14bcae668f7551e57f3095425
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2018
---
# <a name="compare-azure-data-factory-v1-and-v2"></a>Comparer les versions V1 et V2 d’Azure Data Factory
Cet article compare la version V2 à la version V1 d’Azure Data Factory. Pour une présentation de V1, consultez [Présentation d’Azure Data Factory](v1/data-factory-introduction.md). Pour une présentation de V2, consultez [Présentation d’Azure Data Factory (V2 - préversion)](introduction.md).

## <a name="feature-comparison"></a>Comparaison des fonctionnalités
Le tableau suivant compare les fonctionnalités de V1 et V2. 

| Fonctionnalité | version 1 | version 2 | 
| ------- | --------- | --------- | 
| Groupes de données | Une vue de données nommée qui fait référence aux données que vous souhaitez utiliser dans vos activités en tant qu’entrées et sorties. Les jeux de données identifient les données dans différents magasins de données, par exemple des tables, des fichiers, des dossiers et des documents. Par exemple, un jeu de données d’objets blob Azure spécifie le conteneur et le dossier du stockage Blob Azure à partir duquel l’activité doit lire les données.<br/><br/>**Disponibilité** définit le modèle de découpage de fenêtre de traitement du jeu de données (par exemple, horaire, journalier, etc.). | Les jeux de données sont les mêmes dans V2. Toutefois, vous n’avez pas besoin de définir de planifications de **disponibilité** pour les jeux de données. Vous pouvez définir une ressource de déclencheur qui permet de planifier des pipelines à partir d’un paradigme de planificateur d’horloge. Pour plus d’informations, consultez [Déclencheurs](concepts-pipeline-execution-triggers.md#triggers) et [Jeux de données](concepts-datasets-linked-services.md). | 
| Services liés | Les services liés ressemblent à des chaînes de connexion. Ils définissent les informations de connexion nécessaires à Data Factory pour se connecter à des ressources externes. | Les services liés sont identiques à ceux de Data Factory V1, mais avec une nouvelle propriété **connectVia** qui permet d’utiliser l’environnement Compute de runtime d’intégration de Data Factory V2. Pour plus d’informations, consultez [Runtimes d’intégration dans Azure Data Factory](concepts-integration-runtime.md) et [Propriétés de service lié pour le stockage Blob Azure](connector-azure-blob-storage.md#linked-service-properties). |
| Pipelines | Une fabrique de données peut avoir un ou plusieurs pipelines. Un pipeline constitue un regroupement logique d’activités qui exécutent ensemble une tâche. Vous utilisez startTime, endTime et isPaused pour planifier et exécuter des pipelines. | Les pipelines sont des groupes d’activités qui sont effectuées sur les données. Toutefois, la planification des activités dans le pipeline a été divisée en nouvelles ressources de déclencheur. Vous pouvez davantage considérer les pipelines de Data Factory V2 comme des « unités de workflow » que vous planifiez séparément via des déclencheurs. <br/><br/>Les pipelines n’ont pas de « fenêtres » d’exécution dans Data Factory V2. Les concepts startTime, endTime et isPaused de Data Factory V1 ne sont plus présents dans Data Factory V2. Pour plus d’informations, consultez [Exécution de pipelines et déclencheurs](concepts-pipeline-execution-triggers.md) et [Pipelines et activités](concepts-pipelines-activities.md). |
| Activités | Les activités définissent les actions à effectuer sur vos données dans un pipeline. Le déplacement des données (activité de copie) et des activités de transformation des données (tels que Hive, Pig et MapReduce) sont pris en charge. | Dans Data Factory V2, les activités sont toujours des actions définies dans un pipeline. V2 introduit de nouvelles [activités de flux de contrôle](concepts-pipelines-activities.md#control-activities). Vous utilisez ces activités dans un flux de contrôle (bouclage et création de branche). Le déplacement des données et les activités de transformation des données qui étaient prises en charge dans V1 le sont également dans V2. Vous pouvez définir des activités de transformation sans utiliser de jeux de données dans V2. |
| Déplacement de données hybrides et répartition des activités | Maintenant appelée Runtime d’intégration, la [passerelle de gestion des données](v1/data-factory-data-management-gateway.md) prenait en charge le déplacement de données entre un emplacement local et un cloud.| La passerelle de gestion des données est maintenant appelée un runtime d’intégration autohébergé. Il offre la même fonctionnalité que dans V1. <br/><br/> Le runtime d’intégration Azure-SSIS dans V2 prend également en charge le déploiement et l’exécution de packages SQL Server Integration Services (SSIS) dans le cloud. Pour plus d’informations, consultez [Runtime d’intégration dans Azure Data Factory](concepts-integration-runtime.md).|
| parameters | N/D | Les paramètres sont des paires clé/valeur de paramètres de configuration en lecture seule qui sont définis dans des pipelines. Vous pouvez transmettre des arguments pour les paramètres lorsque vous exécutez manuellement le pipeline. Si vous utilisez un déclencheur Scheduler, le déclencheur peut également transmettre des valeurs pour les paramètres. Les activités contenues dans le pipeline utilisent les valeurs des paramètres.  |
| Expressions | Data Factory V1 vous permet d’utiliser des fonctions et des variables système dans des requêtes de sélection de données et des propriétés d’activité/de jeu de données. | Dans Data Factory V2, vous pouvez utiliser des expressions n’importe où dans une valeur de chaîne JSON. Pour plus d’informations, consultez [Expressions et fonctions dans V2](control-flow-expression-language-functions.md).|
| Exécutions de pipeline | N/D | Une seule instance d’exécution d’un pipeline. Par exemple, vous disposez d’un pipeline qui s’exécute à 8 h, 9 h et 10 h. Il y aura trois exécutions du pipeline différentes. Chaque exécution de pipeline possède un ID d’exécution de pipeline unique. L’ID d’exécution de pipeline est un GUID qui identifie de façon unique cette exécution de pipeline spécifique. Les exécutions de pipeline sont généralement instanciées en transmettant des arguments aux paramètres définis dans les pipelines. |
| Exécutions d’activités | N/D | Une instance d’une exécution d’activité dans un pipeline. | 
| Exécutions de déclencheur | N/D | Une instance d’une exécution de déclencheur. Pour plus d’informations, consultez [Déclencheurs](concepts-pipeline-execution-triggers.md). |
| Planification | La planification est basée sur les heures de début/fin du pipeline et sur la disponibilité du jeu de données. | Le déclencheur Scheduler ou l’exécution via un planificateur externe. Pour plus d’informations, consultez l’article [Exécution de pipelines et déclencheurs](concepts-pipeline-execution-triggers.md). |

Les sections qui suivent fournissent des informations supplémentaires sur les fonctionnalités de V2. 

## <a name="control-flow"></a>Flux de contrôle  
Pour prendre en charge différents flux d’intégration et modèles dans l’entrepôt de données moderne, Data Factory V2 a mis en œuvre un nouveau modèle flexible de pipeline de données qui n’est plus lié à des données de série chronologique. Quelques flux courants qui n’étaient pas possibles auparavant sont désormais activés. Ils sont décrits dans les sections suivantes.   

### <a name="chaining-activities"></a>Chaînage des activités
Dans V1, vous deviez configurer la sortie d’une activité en tant qu’entrée d’une autre activité pour les chaîner. Dans V2, vous pouvez chaîner des activités dans une séquence au sein d’un pipeline. Vous pouvez utiliser la propriété **dependsOn** dans une définition d’activité pour la chaîner à une activité en amont. Pour plus d’informations et obtenir un exemple, consultez [Pipelines et activités](concepts-pipelines-activities.md#multiple-activities-in-a-pipeline) et [Création d’une branche et chaînage des activités](tutorial-control-flow.md). 

### <a name="branching-activities"></a>Création d’une branche d’activités
Dans V2, vous pouvez désormais créer une branche d’activités au sein d’un pipeline. L’[activité If-condition](control-flow-if-condition-activity.md) fournit les mêmes fonctionnalités qu’une instruction `if` dans les langages de programmation. La condition évalue un ensemble d’activités si l’expression retourne `true` et un autre ensemble d’activités si elle retourne `false`. Pour obtenir un exemple de création d’une branche d’activités, consultez le didacticiel [Création d’une branche et chaînage des activités](tutorial-control-flow.md).

### <a name="parameters"></a>parameters 
Vous pouvez définir les paramètres au niveau du pipeline et transmettre des arguments pendant que vous appelez le pipeline à la demande ou à partir d’un déclencheur. Les activités peuvent consommer les arguments transmis au pipeline. Pour plus d’informations, consultez [Pipelines et déclencheurs](concepts-pipeline-execution-triggers.md). 

### <a name="custom-state-passing"></a>Transmission d’un état personnalisé
Les sorties de l’activité, notamment l’état, peuvent être consommées par une activité ultérieure du pipeline. Par exemple, dans la définition JSON d’une activité, vous pouvez accéder à la sortie de l’activité précédente à l’aide de la syntaxe suivante : `@activity('NameofPreviousActivity').output.value`. Grâce à cette fonctionnalité, vous pouvez créer des workflows dans lesquels des valeurs peuvent transmettre des activités.

### <a name="looping-containers"></a>Bouclage des conteneurs
L’[activité ForEach](control-flow-for-each-activity.md) définit un flux de contrôle répétitif dans votre pipeline. Elle effectue une itération sur une collection et exécute des activités spécifiées dans une boucle. L’implémentation en boucle de cette activité est semblable à la structure d’exécution en boucle de Foreach dans les langages de programmation. 

L’activité [Until](control-flow-until-activity.md) fournit les mêmes fonctionnalités qu’une structure de boucle do-until dans les langages de programmation. Elle exécute un ensemble d’activités dans une boucle jusqu’à ce que la condition associée à l’activité retourne la valeur `true`. Vous pouvez spécifier une valeur de délai d’attente pour l’activité Until dans Data Factory.  

### <a name="trigger-based-flows"></a>Flux basés sur déclencheur
Les pipelines peuvent être déclenchés à la demande ou selon une durée chronométrée. L’article [Pipelines et déclencheurs](concepts-pipeline-execution-triggers.md) contient des informations détaillées sur les déclencheurs. 

### <a name="invoking-a-pipeline-from-another-pipeline"></a>Appel d’un pipeline à partir d’un autre pipeline
L’[activité d’exécution du pipeline](control-flow-execute-pipeline-activity.md) permet à un pipeline Data Factory d’appeler un autre pipeline.

### <a name="delta-flows"></a>Flux delta
Un cas d’utilisation typique dans des modèles ETL correspond aux « charges delta », dans lesquelles seules les données ayant changé depuis la dernière itération d’un pipeline sont chargées. De nouvelles fonctionnalités de V2 comme [l’activité de recherche](control-flow-lookup-activity.md), la planification flexible et le flux de contrôle permettent d’appliquer naturellement ce cas d’utilisation. Pour un didacticiel avec des instructions détaillées, consultez [Didacticiel : copie incrémentielle](tutorial-incremental-copy-powershell.md).

### <a name="other-control-flow-activities"></a>Autres activités de flux de contrôle
D’autres activités de flux de contrôle prises en charge par Data Factory V2 sont indiquées ci-dessous. 

Activité de contrôle | DESCRIPTION
---------------- | -----------
[Activité ForEach](control-flow-for-each-activity.md) | Définit un flux de contrôle répétitif dans votre pipeline. Elle permet d’effectuer une itération sur une collection et exécute des activités spécifiées dans une boucle. L’implémentation en boucle de cette activité est semblable à la structure d’exécution en boucle de Foreach dans les langages de programmation.
[Activité Web](control-flow-web-activity.md) | Appelle un point de terminaison REST personnalisé à partir d’un pipeline Data Factory. Vous pouvez transmettre des jeux de données et des services liés que l’activité peut utiliser et auxquels elle peut accéder. 
[Activité de recherche](control-flow-lookup-activity.md) | Lit ou recherche une valeur de nom d’enregistrement ou de table à partir de n’importe quelle source externe. Cette sortie peut être référencée par des activités complémentaires. 
[Activité d’obtention des métadonnées](control-flow-get-metadata-activity.md) | Récupère les métadonnées des données dans Azure Data Factory. 
[Activité d’attente](control-flow-wait-activity.md) | Suspend le pipeline pour une période spécifiée.

## <a name="deploy-ssis-packages-to-azure"></a>Déployer des packages SSIS vers Azure 
Utilisez Azure SSIS si vous souhaitez déplacer vos charges de travail SSIS dans le cloud, créer une fabrique de données V2 et approvisionner un runtime d’intégration Azure-SSIS.

Le runtime d’intégration Azure-SSIS est un cluster entièrement géré de machines virtuelles Azure (nœuds) dédiées à l’exécution de vos packages SSIS dans le cloud. Une fois que vous avez approvisionné le runtime d’intégration Azure-SSIS, vous pouvez utiliser les mêmes outils que ceux utilisés pour déployer des packages SSIS dans un environnement SSIS local. 

Par exemple, vous pouvez utiliser SQL Server Data Tools (SSDT) ou SQL Server Management Studio (SSMS) pour déployer des packages SSIS sur ce runtime dans Azure. Pour obtenir des instructions pas à pas, consultez le didacticiel [Déployer des packages SQL Server Integration Services vers Azure](tutorial-deploy-ssis-packages-azure.md). 

## <a name="flexible-scheduling"></a>Planification flexible
Dans Data Factory V2, vous n’avez pas besoin de définir de planifications de disponibilité de jeu de données. Vous pouvez définir une ressource de déclencheur qui permet de planifier des pipelines à partir d’un paradigme de planificateur d’horloge. Vous pouvez également transmettre des paramètres à des pipelines à partir d’un déclencheur pour une planification flexible et un modèle d’exécution. 

Les pipelines n’ont pas de « fenêtres » d’exécution dans Data Factory V2. Les concepts startTime, endTime et isPaused de Data Factory V1 n’existent plus dans Data Factory V2. Pour plus d’informations sur la façon de créer et de planifier un pipeline dans Data Factory V2, consultez [Exécution du pipeline et déclencheurs](concepts-pipeline-execution-triggers.md).

## <a name="support-for-more-data-stores"></a>Prise en charge d’autres magasins de données
V2 prend en charge la copie de données dans et à partir de plus de magasins de données que V1. Pour obtenir la liste des magasins de données pris en charge, consultez les articles suivants :

- [V1 - Magasins de données pris en charge](v1/data-factory-data-movement-activities.md#supported-data-stores-and-formats)
- [V2 - Magasins de données pris en charge](copy-activity-overview.md#supported-data-stores-and-formats)

## <a name="support-for-on-demand-spark-cluster"></a>Prise en charge du cluster Spark à la demande
V2 prend en charge la création d’un cluster Azure HDInsight Spark à la demande. Pour créer un cluster Spark à la demande, spécifiez le type de cluster Spark dans votre définition de service lié HDInsight à la demande. Vous pouvez ensuite configurer l’activité Spark dans votre pipeline pour utiliser ce service lié. 

Lors de l’exécution, lorsque l’activité est exécutée, le service Data Factory crée automatiquement le cluster Spark pour vous. Pour plus d’informations, consultez les articles suivants :

- [Activité Spark dans V2](transform-data-using-spark.md)
- [Service lié à la demande Azure HDInsight](compute-linked-services.md#azure-hdinsight-on-demand-linked-service)

## <a name="custom-activities"></a>Activités personnalisées
Dans V1, vous implémentez le code de l’activité DotNet (personnalisée) en créant un projet de bibliothèque de classes .NET avec une classe qui implémente la méthode Execute de l’interface IDotNetActivity. Votre code personnalisé doit donc être écrit dans le .NET Framework 4.5.2 et être exécuté sur des nœuds de pool Azure Batch basés sur Windows. 

Dans une activité personnalisée V2, vous n’êtes pas obligé d’implémenter une interface .NET. Vous pouvez exécuter directement des commandes et des scripts, et exécuter votre propre code compilé comme un exécutable. 

Pour plus d’informations, consultez [Différence entre une activité personnalisée dans V1 et V2](transform-data-using-dotnet-custom-activity.md#difference-between-custom-activity-in-azure-data-factory-v2-and-custom-dotnet-activity-in-azure-data-factory-v1).

## <a name="sdks"></a>Kits de développement logiciel (SDK)
 Data Factory V2 fournit un ensemble plus riche de Kits de développement logiciel (DSK) qui peuvent être utilisés pour créer, gérer et surveiller des pipelines.

- **SDK .NET** : le SDK .NET est mis à jour pour V2.

- **PowerShell** : les applets de commande PowerShell sont mises à jour pour V2. Les cmdlets V2 ont **DataFactoryV2** dans le nom, par exemple : Get-AzureRmDataFactoryV2. 

- **SDK Python** : ce SDK est une nouveauté de V2.

- **API REST** : l’API REST est mise à jour pour V2. 

Les Kits de développement logiciel (SDK) mis à jour pour V2 ne sont pas compatibles avec les clients V1. 

## <a name="authoring-experience"></a>Expérience de création

| &nbsp; | V2 | V1 |
| ------ | -- | -- | 
| Portail Azure | [Oui](quickstart-create-data-factory-portal.md) | [Oui](data-factory-build-your-first-pipeline-using-editor.md) |
| Azure PowerShell | [Oui](quickstart-create-data-factory-powershell.md) | [Oui](data-factory-build-your-first-pipeline-using-powershell.md) |
| Kit de développement logiciel (SDK) .NET | [Oui](quickstart-create-data-factory-dot-net.md) | [Oui](data-factory-build-your-first-pipeline-using-vs.md) |
| de l’API REST | [Oui](quickstart-create-data-factory-rest-api.md) | [Oui](data-factory-build-your-first-pipeline-using-rest-api.md) |
| Kit de développement logiciel (SDK) Python | [Oui](quickstart-create-data-factory-python.md) | Non  |
| Modèle Resource Manager | [Oui](quickstart-create-data-factory-resource-manager-template.md) | [Oui](data-factory-build-your-first-pipeline-using-arm.md) | 


## <a name="monitoring-experience"></a>Expérience de surveillance
Dans V2, vous pouvez également surveiller les fabriques de données à l’aide d’[Azure Monitor](monitor-using-azure-monitor.md). Les nouvelles applets de commande PowerShell prennent en charge la surveillance des [runtimes d’intégration](monitor-integration-runtime.md). V1 et V2 prennent toutes deux en charge la surveillance visuelle à l’aide d’une application de surveillance pouvant être lancée depuis le portail Azure.


## <a name="next-steps"></a>étapes suivantes
Découvrez comment créer une fabrique de données en suivant les instructions détaillées fournies dans les démarrages rapides suivants : [PowerShell](quickstart-create-data-factory-powershell.md), [.NET](quickstart-create-data-factory-dot-net.md), [Python](quickstart-create-data-factory-python.md), [API REST](quickstart-create-data-factory-rest-api.md). 
