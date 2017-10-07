---
title: aaaAzure Data Factory - exemples
description: "Fournit des détails sur les exemples fournis avec hello service Azure Data Factory."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: c0538b90-2695-4c4c-a6c8-82f59111f4ab
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: aa1c15eca21b34b7bcc64358b685d7606baaf691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---samples"></a>Azure Data Factory - Exemples
## <a name="samples-on-github"></a>Exemples sur GitHub
Hello [GitHub Azure-DataFactory référentiel](https://github.com/azure/azure-datafactory) contient plusieurs exemples pour vous aider à rapidement avec le service Azure Data Factory d’accélération (ou) modifier les scripts de hello et l’utiliser dans une application propre. dossier de Samples\JSON Hello contient des extraits de code JSON pour les scénarios courants.

| Exemple | Description |
|:--- |:--- |
| [Procédure pas à pas Azure Data Factory](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFWalkthrough) |Cet exemple fournit une procédure pas à pas de bout en bout pour le traitement des fichiers journaux à l’aide des données de tooturn Azure Data Factory à partir des fichiers journaux dans tooinsights. <br/><br/>Dans cette procédure pas à pas, pipeline de Data Factory hello collecte des journaux de l’exemple, processus et enrichit hello les données de journaux avec les données de référence et transforme hello données tooevaluate hello l’efficacité d’une campagne marketing qui a été récemment lancée. |
| [Exemples JSON](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON) |Cet exemple fournit des exemples JSON pour des scénarios courants. |
| [Exemple de téléchargeur de données HTTP](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample) |Cet exemple présente téléchargement de données à partir d’un tooAzure de point de terminaison HTTP stockage d’objets Blob à l’aide d’activité .NET personnalisée. |
| [Exemple d’activité .NET entre AppDomains](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) |Cet exemple vous permet de tooauthor une activité .NET personnalisée qui n’est pas contraint de versions tooassembly utilisées hello ADF (par exemple, WindowsAzure.Storage v4.3.0, Newtonsoft.Json v6.0.x, etc.). |
| [Exécuter un script R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample) |Cet exemple inclut l’activité personnalisée hello fabrique de données qui peut être utilisé tooinvoke RScript.exe. Cet exemple fonctionne uniquement avec votre propre cluster HDInsight (et non celui à la demande) sur lequel est déjà installé le script R. |
| [Appeler des travaux Spark sur un cluster HDInsight Hadoop](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/Spark) |Cet exemple montre comment toouse MapReduce activité tooinvoke un programme Spark. programme de spark Hello copie uniquement les données à partir d’un tooanother de conteneur d’objets Blob Azure. |
| [Analyse de Twitter à l’aide d’une activité de notation par lot d’Azure Machine Learning](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-AzureMLBatchScoringActivity) |Cet exemple montre comment toouse AzureMLBatchScoringActivity tooinvoke une Azure Machine Learning modèle qui effectue l’analyse de sentiments twitter, de calcul de score, etc. de prédiction. |
| [Analyse de Twitter à l’aide d’une activité personnalisée](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-CustomC%23Activity) |Cet exemple montre comment toouse un tooinvoke d’activité .NET personnalisé un modèle Azure Machine Learning qui effectue twitter analyse des sentiments, de calcul de score, etc. de prédiction. |
| [Pipelines paramétrés pour Azure Machine Learning](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ParameterizedPipelinesForAzureML/) |exemple Hello fournit un bout à bout c# code toodeploy N pipelines pour calculer les scores et recyclage chacun avec un paramètre autre région où la liste des régions hello provient d’un fichier parameters.txt, qui est inclus avec cet exemple. |
| [Actualisation des données de référence pour les travaux Azure Stream Analytics](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ReferenceDataRefreshForASAJobs) |Cet exemple montre comment l’actualisation des données de référence sur une planification toouse Azure Data Factory et Azure flux Analytique toorun ensemble hello requêtes hello de données et le programme d’installation de référence. |
| [Pipeline hybride avec une instance locale d’Hadoop Hortonworks](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HybridPipelineWithOnPremisesHortonworksHadoop) |exemple Hello utilise un cluster Hadoop de local comme cible de calcul pour l’exécution de travaux dans la fabrique de données comme vous devez ajouter les autres cibles de calcul comme un HDInsight en fonction de cluster Hadoop dans le cloud. |
| [Outil de conversion JSON](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSONConversionTool) |Cet outil vous permet de tooconvert JSON à partir de la version antérieure too2015-07-01-preview toolatest ou 2015-07-01-preview (par défaut). |
| [Exemple de fichier d’entrée U-SQL](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/U-SQL%20Sample%20Input%20File) |Il s’agit d’un exemple de fichier utilisé par une activité U-SQL. |
| [Supprimer le fichier blob](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity) | Cet exemple présente un fichier c# qui peut être utilisé dans le cadre de la définition d’application .net activité toodelete des fichiers personnalisés à partir de la source de hello emplacement d’objets Blob Azure une fois que les fichiers hello ont été copiés.|

## <a name="azure-resource-manager-templates"></a>Modèles Microsoft Azure Resource Manager
Vous pouvez trouver hello suivant des modèles Azure Resource Manager de fabrique de données sur GitHub.

| Modèle | Description |
| --- | --- |
| [Copier à partir du stockage d’objets Blob Azure tooAzure base de données SQL](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy) |Déploiement de ce modèle crée une fabrique de données Azure avec un pipeline que copie des données à partir de hello spécifié de base de données SQL Azure blob Azure storage toohello |
| [Copier à partir de Salesforce tooAzure stockage d’objets Blob](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy) |Déploiement de ce modèle de crée une fabrique de données Azure avec un pipeline que copie des données à partir de hello spécifié le stockage d’objets blob Azure Salesforce compte toohello. |
| [Transformer les données en exécutant le script Hive sur un cluster Azure HDInsight](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation) |Déploiement de ce modèle de crée une fabrique de données Azure avec un pipeline qui transforme les données en exécutant le script Hive d’exemple hello sur un cluster Azure HDInsight Hadoop. |

## <a name="samples-in-azure-portal"></a>Exemples dans le portail Azure
Vous pouvez utiliser hello **exemple pipelines** vignette sur la page d’accueil hello de vos pipelines de données fabrique toodeploy exemple et les entités associées (groupes de données et services liés) dans tooyour data factory.

1. Créez une fabrique de données ou ouvrez une fabrique de données existante. Consultez [copier les données de stockage d’objets Blob tooSQL de base de données à l’aide de la fabrique de données](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour les étapes toocreate une fabrique de données.
2. Bonjour **DATA FACTORY** Panneau de fabrique de données hello, cliquez sur hello **exemple pipelines** vignette.

    ![Vignette Exemples de pipelines](./media/data-factory-samples/SamplePipelinesTile.png)
3. Bonjour **exemple pipelines** panneau, cliquez sur hello **exemple** que vous souhaitez toodeploy.

    ![Panneau Exemples de pipelines](./media/data-factory-samples/SampleTile.png)
4. Spécifiez les paramètres de configuration de l’exemple hello. Par exemple, votre clé de compte et votre nom de compte de stockage Azure, le nom du serveur SQL Azure, la base de données, l’ID d’utilisateur, le mot de passe, etc.

    ![Panneau Exemple](./media/data-factory-samples/SampleBlade.png)
5. Une fois que vous avez terminé avec la spécification des paramètres de configuration hello, cliquez sur **créer** toocreate/déployer hello exemple pipelines et utilisés par les pipelines hello services/tables liées.
6. Vous consultez État hello de déploiement sur la vignette d’exemple hello vous avez cliqué précédemment sur hello **exemple pipelines** panneau.

    ![état du déploiement](./media/data-factory-samples/DeploymentStatus.png)
7. Lorsque vous consultez hello **déploiement a réussi** message sur la vignette hello pour exemple hello, fermer hello **exemple pipelines** panneau.  
8. Sur **DATA FACTORY** panneau, vous voyez que les services liés, les jeux de données et les pipelines sont ajoutés fabrique de données tooyour.  

    ![Panneau Data Factory](./media/data-factory-samples/DataFactoryBladeAfter.png)

## <a name="samples-in-visual-studio"></a>Exemples dans Visual Studio
### <a name="prerequisites"></a>Composants requis
Vous devez disposer de hello installé sur votre ordinateur :

* Visual Studio 2013 ou Visual Studio 2015
* Téléchargez le Kit de développement logiciel (SDK) Azure pour Visual Studio 2013 ou Visual Studio 2015. Accédez trop[Page de téléchargement Azure](https://azure.microsoft.com/downloads/) et cliquez sur **VS 2013** ou **VS 2015** Bonjour **.NET** section.
* Téléchargement du plug-in Azure Data Factory dernière hello pour Visual Studio : [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) ou [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005). Si vous utilisez Visual Studio 2013, vous pouvez également mettre à jour plug-in hello en procédant comme hello comme suit : cliquez sur hello, **outils** -> **Extensions et mises à jour**  ->  **En ligne** -> **galerie Visual Studio** -> **Microsoft Azure Data Factory Tools pour Visual Studio**  ->  **Mise à jour**.

### <a name="use-data-factory-templates"></a>Utilisation de modèles de fabrique de données
1. Cliquez sur **fichier** dans le menu de hello, pointez trop**nouveau**, puis cliquez sur **projet**.
2. Bonjour **nouveau projet** boîte de dialogue zone, hello comme suit :

   1. Sous **Modèles**, sélectionnez **DataFactory**.
   2. Sélectionnez **modèles de fabrique de données** dans le volet de droite hello.
   3. Entrez un **nom** pour le projet de hello.
   4. Sélectionnez un **emplacement** pour le projet de hello.
   5. Cliquez sur **OK**.

      ![Boîte de dialogue Nouveau projet](./media/data-factory-samples/vs-new-project-adf-templates.png)
3. Bonjour **modèles de fabrique de données** boîte de dialogue, exemple de modèle de hello select à partir de hello **modèles de cas d’usage** section, puis cliquez sur **suivant**. Hello étapes suivantes vous guident à l’aide de hello **client profilage** modèle. Étapes sont identiques pour hello d’autres exemples.

    ![Boîte de dialogue Modèles de fabrique de données](./media/data-factory-samples/vs-data-factory-templates-dialog.png)
4. Bonjour **Configuration de fabrique de données** boîte de dialogue, cliquez sur **suivant** sur hello **principes de base de données de fabrique** page.
5. Sur hello **fabrique de données de configuration** page, procédez comme hello comme suit :
   1. Sélectionnez **Créer une fabrique de données** . Vous pouvez également sélectionner **Utiliser une fabrique de données existante**.
   2. Entrez un **nom** de fabrique de données hello.
   3. Sélectionnez hello **abonnement Azure** dans lesquelles vous voulez toobe de fabrique de données hello créé.
   4. Sélectionnez hello **groupe de ressources** de fabrique de données hello.
   5. Sélectionnez hello **ouest des États-Unis**, **États-Unis**, ou **Europe du Nord** pour hello **région**.
   6. Cliquez sur **Suivant**.
6. Bonjour **configurer des magasins de données** , spécifiez un existant **base de données SQL Azure** et **compte de stockage Azure** (ou) créer la base de données/du stockage et cliquez sur Suivant.
7. Bonjour **configurer calcul** page, sélectionnez les valeurs par défaut, puis cliquez sur **suivant**.
8. Bonjour **Résumé** page, passez en revue tous les paramètres, puis cliquez sur **suivant**.
9. Bonjour **état du déploiement** page, attendez que le déploiement de hello est terminé, cliquez sur **Terminer**.
10. Cliquez sur le projet dans l’Explorateur de solutions de hello, puis cliquez sur **publier**.
11. Si vous voyez **connecter tooyour compte Microsoft** boîte de dialogue, entrez vos informations d’identification de compte hello qui dispose d’abonnement Azure, puis cliquez sur **connectez-vous**.
12. Vous devez voir hello suivant la boîte de dialogue :

    ![Boîte de dialogue Publier](./media/data-factory-build-your-first-pipeline-using-vs/publish.png)
13. Bonjour **fabrique de données de configuration** page, procédez comme hello comme suit :

    1. Confirmez l’option **Utiliser une fabrique de données existante** .
    2. Sélectionnez hello **fabrique de données** vous aviez sélectionnez lors de l’utilisation du modèle de hello.
    3. Cliquez sur **suivant** tooswitch toohello **publier des éléments** page. (Appuyez sur **onglet** toomove hors Bonjour nom champ tooif Bonjour **suivant** bouton est désactivé.)
14. Bonjour **publier des éléments** , vérifiez que tous les hello fabriques de données entités sont sélectionnées, puis cliquez sur **suivant** tooswitch toohello **Résumé** page.     
15. Passez en revue la synthèse de hello et cliquez sur **suivant** toostart Bonjour déploiement processus et vue Bonjour **état du déploiement**.
16. Bonjour **état du déploiement** page, vous devez voir État hello hello du processus de déploiement. Après le déploiement de hello, cliquez sur Terminer.

Consultez [générer votre première fabrique de données (Visual Studio)](data-factory-build-your-first-pipeline-using-vs.md) pour plus d’informations sur l’utilisation des entités de fabrique de données tooauthor Visual Studio et de leur publication tooAzure.          
