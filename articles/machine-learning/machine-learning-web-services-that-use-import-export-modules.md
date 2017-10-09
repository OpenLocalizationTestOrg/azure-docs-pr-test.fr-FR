---
title: "aaaUsing importer/exporter des données dans les services web Azure Machine Learning | Documents Microsoft"
description: "Découvrez comment toouse hello toosend de modules de données d’importation et exportation de données et recevoir des données d’un service web."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: 3a7ac351-ebd3-43a1-8c5d-18223903d08e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 176380259b15cb338ede61c7f28ba2296b35dd52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-azure-ml-web-services-that-use-data-import-and-data-export-modules"></a><span data-ttu-id="6227f-103">Déploiement de services web Azure ML utilisant les modules d’importation et d’exportation des données</span><span class="sxs-lookup"><span data-stu-id="6227f-103">Deploying Azure ML web services that use Data Import and Data Export modules</span></span>

<span data-ttu-id="6227f-104">Lorsque vous créez une expérience prédictive, vous ajoutez généralement une entrée et une sortie de service web.</span><span class="sxs-lookup"><span data-stu-id="6227f-104">When you create a predictive experiment, you typically add a web service input and output.</span></span> <span data-ttu-id="6227f-105">Lorsque vous déployez expérience de hello, consommateurs peuvent envoyer et recevoir des données de service web de hello via hello entrées et sorties.</span><span class="sxs-lookup"><span data-stu-id="6227f-105">When you deploy hello experiment, consumers can send and receive data from hello web service through hello inputs and outputs.</span></span> <span data-ttu-id="6227f-106">Pour certaines applications, les données d’un consommateur peuvent être disponibles à partir d’un flux de données ou figurer déjà dans une source de données externe tels que le stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="6227f-106">For some applications, a consumer's data may be available from a data feed or already reside in an external data source such as Azure Blob storage.</span></span> <span data-ttu-id="6227f-107">Dans ces cas, elles n’ont pas besoin de lire ni d’écrire les données en utilisant des entrées et sorties de service web.</span><span class="sxs-lookup"><span data-stu-id="6227f-107">In these cases, they do not need read and write data using web service inputs and outputs.</span></span> <span data-ttu-id="6227f-108">Au lieu de cela, ils peuvent utilisent des données de tooread hello Service de l’exécution de lot (BES) à partir de la source de données hello à l’aide d’un module d’importation de données et écrire hello score résultats tooa emplacement de données différentes à l’aide d’un module d’exporter des données.</span><span class="sxs-lookup"><span data-stu-id="6227f-108">They can, instead, use hello Batch Execution Service (BES) tooread data from hello data source using an Import Data module and write hello scoring results tooa different data location using an Export Data module.</span></span>

<span data-ttu-id="6227f-109">Hello importer des données et des modules de données d’exportation, peut lire et écrire des données toovarious fournissent des emplacements, par exemple, une URL Web via HTTP, une requête Hive, une base de données SQL Azure, stockage de Table Azure, le stockage Blob Azure, un flux de données ou une base de données SQL locale.</span><span class="sxs-lookup"><span data-stu-id="6227f-109">hello Import Data and Export data modules, can read from and write toovarious data locations such as a Web URL via HTTP, a Hive Query, an Azure SQL database, Azure Table storage, Azure Blob storage, a Data Feed provide, or an on-premises SQL database.</span></span>

<span data-ttu-id="6227f-110">Cette rubrique utilise hello « exemple 5 : Evaluate Train, Test, pour la Classification binaire : jeu de données adulte « exemple et suppose hello le jeu de données a déjà été chargé dans une table SQL Azure nommée censusdata.</span><span class="sxs-lookup"><span data-stu-id="6227f-110">This topic uses hello "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" sample and assumes hello dataset has already been loaded into an Azure SQL table named censusdata.</span></span>

## <a name="create-hello-training-experiment"></a><span data-ttu-id="6227f-111">Créer l’expérience de formation hello</span><span class="sxs-lookup"><span data-stu-id="6227f-111">Create hello training experiment</span></span>
<span data-ttu-id="6227f-112">Lorsque vous ouvrez hello « exemple 5 : Evaluate Train, Test, pour la Classification binaire : jeu de données adulte « exemple de jeu de données utilise hello exemple adulte Classification binaire revenu de recensement.</span><span class="sxs-lookup"><span data-stu-id="6227f-112">When you open hello "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" sample it uses hello sample Adult Census Income Binary Classification dataset.</span></span> <span data-ttu-id="6227f-113">Et expérience hello dans la zone de dessin hello ressemblera similaire toohello suivant l’image :</span><span class="sxs-lookup"><span data-stu-id="6227f-113">And hello experiment in hello canvas will look similar toohello following image:</span></span>

![Configuration initiale de l’expérience de hello.](./media/machine-learning-web-services-that-use-import-export-modules/initial-look-of-experiment.png)

<span data-ttu-id="6227f-115">données de salutation tooread à partir de la table de SQL Azure hello :</span><span class="sxs-lookup"><span data-stu-id="6227f-115">tooread hello data from hello Azure SQL table:</span></span>

1. <span data-ttu-id="6227f-116">Suppression du module de dataset hello.</span><span class="sxs-lookup"><span data-stu-id="6227f-116">Delete hello dataset module.</span></span>
2. <span data-ttu-id="6227f-117">Dans la zone de recherche de composants hello, tapez l’importation.</span><span class="sxs-lookup"><span data-stu-id="6227f-117">In hello components search box, type import.</span></span>
3. <span data-ttu-id="6227f-118">À partir de la liste des résultats hello, ajoutez un *importer des données* module toohello expérimenter la zone de dessin.</span><span class="sxs-lookup"><span data-stu-id="6227f-118">From hello results list, add an *Import Data* module toohello experiment canvas.</span></span>
4. <span data-ttu-id="6227f-119">Connectez la sortie de hello *importer des données* entrée hello de module de hello *Clean Missing Data* module.</span><span class="sxs-lookup"><span data-stu-id="6227f-119">Connect output of hello *Import Data* module hello input of hello *Clean Missing Data* module.</span></span>
5. <span data-ttu-id="6227f-120">Dans le volet Propriétés, sélectionnez **base de données SQL Azure** Bonjour **Source de données** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="6227f-120">In properties pane, select **Azure SQL Database** in hello **Data Source** dropdown.</span></span>
6. <span data-ttu-id="6227f-121">Bonjour **nom du serveur de base de données**, **nom de la base de données**, **nom d’utilisateur**, et **mot de passe** , saisissez les informations appropriées pour hello votre base de données.</span><span class="sxs-lookup"><span data-stu-id="6227f-121">In hello **Database server name**, **Database name**, **User name**, and **Password** fields, enter hello appropriate information for your database.</span></span>
7. <span data-ttu-id="6227f-122">Dans le champ de requête de base de données hello, entrez hello suivant la requête.</span><span class="sxs-lookup"><span data-stu-id="6227f-122">In hello Database query field, enter hello following query.</span></span>
   
     <span data-ttu-id="6227f-123">select [age],</span><span class="sxs-lookup"><span data-stu-id="6227f-123">select [age],</span></span>
   
        [workclass],
        [fnlwgt],
        [education],
        [education-num],
        [marital-status],
        [occupation],
        [relationship],
        [race],
        [sex],
        [capital-gain],
        [capital-loss],
        [hours-per-week],
        [native-country],
        [income]
     <span data-ttu-id="6227f-124">from dbo.censusdata;</span><span class="sxs-lookup"><span data-stu-id="6227f-124">from dbo.censusdata;</span></span>
8. <span data-ttu-id="6227f-125">Au bas de hello du canevas de l’expérience hello, cliquez sur **exécuter**.</span><span class="sxs-lookup"><span data-stu-id="6227f-125">At hello bottom of hello experiment canvas, click **Run**.</span></span>

## <a name="create-hello-predictive-experiment"></a><span data-ttu-id="6227f-126">Créer l’expérience de prédictive hello</span><span class="sxs-lookup"><span data-stu-id="6227f-126">Create hello predictive experiment</span></span>
<span data-ttu-id="6227f-127">Ensuite, vous configurez les expérience prédictive hello à partir duquel vous déployez votre service web.</span><span class="sxs-lookup"><span data-stu-id="6227f-127">Next you set up hello predictive experiment from which you deploy your web service.</span></span>

1. <span data-ttu-id="6227f-128">Au bas de hello du canevas de l’expérience hello, cliquez sur **configurer le Service Web** et sélectionnez **Service Web prédictive [recommandé]**.</span><span class="sxs-lookup"><span data-stu-id="6227f-128">At hello bottom of hello experiment canvas, click **Set Up Web Service** and select **Predictive Web Service [Recommended]**.</span></span>
2. <span data-ttu-id="6227f-129">Supprimer hello *entrée du Service Web* et *des modules de sortie du Service Web* à partir de l’expérience de prédictive hello.</span><span class="sxs-lookup"><span data-stu-id="6227f-129">Remove hello *Web Service Input* and *Web Service Output modules* from hello predictive experiment.</span></span> 
3. <span data-ttu-id="6227f-130">Dans la zone de recherche de composants hello, tapez l’exportation.</span><span class="sxs-lookup"><span data-stu-id="6227f-130">In hello components search box, type export.</span></span>
4. <span data-ttu-id="6227f-131">À partir de la liste des résultats hello, ajoutez un *exporter les données* module toohello expérimenter la zone de dessin.</span><span class="sxs-lookup"><span data-stu-id="6227f-131">From hello results list, add an *Export Data* module toohello experiment canvas.</span></span>
5. <span data-ttu-id="6227f-132">Connectez la sortie de hello *Score Model* entrée hello de module de hello *exporter les données* module.</span><span class="sxs-lookup"><span data-stu-id="6227f-132">Connect output of hello *Score Model* module hello input of hello *Export Data* module.</span></span> 
6. <span data-ttu-id="6227f-133">Dans le volet Propriétés, sélectionnez **base de données SQL Azure** dans la liste déroulante destination de données hello.</span><span class="sxs-lookup"><span data-stu-id="6227f-133">In properties pane, select **Azure SQL Database** in hello data destination dropdown.</span></span>
7. <span data-ttu-id="6227f-134">Bonjour **nom du serveur de base de données**, **nom de la base de données**, **le nom de compte d’utilisateur Server**, et **mot de passe utilisateur serveur** , saisissez Hello les informations appropriées pour votre base de données.</span><span class="sxs-lookup"><span data-stu-id="6227f-134">In hello **Database server name**, **Database name**, **Server user account name**, and **Server user account password** fields, enter hello appropriate information for your database.</span></span>
8. <span data-ttu-id="6227f-135">Bonjour **liste des toobe colonnes enregistrée séparées par des virgules** , tapez Scored Labels.</span><span class="sxs-lookup"><span data-stu-id="6227f-135">In hello **Comma separated list of columns toobe saved** field, type Scored Labels.</span></span>
9. <span data-ttu-id="6227f-136">Bonjour **champ de nom de table de données**, tapez dbo. ScoredLabels.</span><span class="sxs-lookup"><span data-stu-id="6227f-136">In hello **Data table name field**, type dbo.ScoredLabels.</span></span> <span data-ttu-id="6227f-137">Si la table de hello n’existe pas, il est créé lors de l’expérience de hello est exécutée ou service web de hello est appelé.</span><span class="sxs-lookup"><span data-stu-id="6227f-137">If hello table does not exist, it is created when hello experiment is run or hello web service is called.</span></span>
10. <span data-ttu-id="6227f-138">Bonjour **liste des colonnes de table de données séparées par des virgules** champ, tapez ScoredLabels.</span><span class="sxs-lookup"><span data-stu-id="6227f-138">In hello **Comma separated list of datatable columns** field, type ScoredLabels.</span></span>

<span data-ttu-id="6227f-139">Lorsque vous écrivez une application que les appels hello service web final, vous souhaiterez toospecify une table de requête ou la destination d’entrée différente au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="6227f-139">When you write an application that calls hello final web service, you may want toospecify a different input query or destination table at run time.</span></span> <span data-ttu-id="6227f-140">tooconfigure ces entrées et sorties, utilisez Bonjour paramètres de Service Web fonctionnalité tooset Bonjour *importer des données* module *source de données* propriété et hello *exporter les données* mode propriété de destination de données.</span><span class="sxs-lookup"><span data-stu-id="6227f-140">tooconfigure these inputs and outputs, use hello Web Service Parameters feature tooset hello *Import Data* module *Data source* property and hello *Export Data* mode data destination property.</span></span>  <span data-ttu-id="6227f-141">Pour plus d’informations sur les paramètres de Service Web, consultez hello [entrée de paramètres de Service Web AzureML](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/) sur hello Cortana Intelligence et Machine Learning Blog.</span><span class="sxs-lookup"><span data-stu-id="6227f-141">For more information on Web Service Parameters, see hello [AzureML Web Service Parameters entry](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/) on hello Cortana Intelligence and Machine Learning Blog.</span></span>

<span data-ttu-id="6227f-142">hello tooconfigure paramètres de Service Web pour la requête d’importation hello et la table de destination hello :</span><span class="sxs-lookup"><span data-stu-id="6227f-142">tooconfigure hello Web Service Parameters for hello import query and hello destination table:</span></span>

1. <span data-ttu-id="6227f-143">Dans le volet de propriétés hello pour hello *importer des données* module, cliquez sur icône de hello en hello haut à droite de hello **requête de base de données** champ, puis sélectionnez **définir en tant que paramètre de service web**.</span><span class="sxs-lookup"><span data-stu-id="6227f-143">In hello properties pane for hello *Import Data* module, click hello icon at hello top right of hello **Database query** field and select **Set as web service parameter**.</span></span>
2. <span data-ttu-id="6227f-144">Dans le volet de propriétés hello pour hello *exporter les données* module, cliquez sur icône de hello en hello haut à droite de hello **nom de table de données** champ, puis sélectionnez **définir en tant que paramètre de service web**.</span><span class="sxs-lookup"><span data-stu-id="6227f-144">In hello properties pane for hello *Export Data* module, click hello icon at hello top right of hello **Data table name** field and select **Set as web service parameter**.</span></span>
3. <span data-ttu-id="6227f-145">En bas de hello Hello *exporter les données* volet de propriétés du module, Bonjour **paramètres de Service Web** section, cliquez sur requête de base de données et renommer la requête.</span><span class="sxs-lookup"><span data-stu-id="6227f-145">At hello bottom of hello *Export Data* module properties pane, in hello **Web Service Parameters** section, click Database query and rename it Query.</span></span>
4. <span data-ttu-id="6227f-146">Cliquez sur le champ **Nom de la table de données** et renommez-le **Table**.</span><span class="sxs-lookup"><span data-stu-id="6227f-146">Click **Data table name** and rename it **Table**.</span></span>

<span data-ttu-id="6227f-147">Lorsque vous avez terminé, votre expérience doit ressembler similaire toohello suivant l’image :</span><span class="sxs-lookup"><span data-stu-id="6227f-147">When you are done, your experiment should look similar toohello following image:</span></span>

![Aspect final de l’expérience.](./media/machine-learning-web-services-that-use-import-export-modules/experiment-with-import-data-added.png)

<span data-ttu-id="6227f-149">Vous pouvez à présent déployer hello expérience comme un service web.</span><span class="sxs-lookup"><span data-stu-id="6227f-149">Now you can deploy hello experiment as a web service.</span></span>

## <a name="deploy-hello-web-service"></a><span data-ttu-id="6227f-150">Déployer le service web de hello</span><span class="sxs-lookup"><span data-stu-id="6227f-150">Deploy hello web service</span></span>
<span data-ttu-id="6227f-151">Vous pouvez déployer tooeither un service web classique ou nouveau.</span><span class="sxs-lookup"><span data-stu-id="6227f-151">You can deploy tooeither a Classic or New web service.</span></span>

### <a name="deploy-a-classic-web-service"></a><span data-ttu-id="6227f-152">Déployer comme un service web classique</span><span class="sxs-lookup"><span data-stu-id="6227f-152">Deploy a Classic Web Service</span></span>
<span data-ttu-id="6227f-153">toodeploy comme un Service Web classique et créer une application tooconsume il :</span><span class="sxs-lookup"><span data-stu-id="6227f-153">toodeploy as a Classic Web Service and create an application tooconsume it:</span></span>

1. <span data-ttu-id="6227f-154">Bas hello du canevas de l’expérience hello, cliquez sur Exécuter.</span><span class="sxs-lookup"><span data-stu-id="6227f-154">At hello bottom of hello experiment canvas, click Run.</span></span>
2. <span data-ttu-id="6227f-155">Hello exécuter a terminé, cliquez sur **déployer le Service Web** et sélectionnez **déployer le Service Web [standard]**.</span><span class="sxs-lookup"><span data-stu-id="6227f-155">When hello run has completed, click **Deploy Web Service** and select **Deploy Web Service [Classic]**.</span></span>
3. <span data-ttu-id="6227f-156">Tableau de bord de service web hello, recherchez votre clé API.</span><span class="sxs-lookup"><span data-stu-id="6227f-156">On hello web service dashboard, locate your API key.</span></span> <span data-ttu-id="6227f-157">Copier et l’enregistrer toouse plus tard.</span><span class="sxs-lookup"><span data-stu-id="6227f-157">Copy and save it toouse later.</span></span>
4. <span data-ttu-id="6227f-158">Bonjour **le point de terminaison par défaut** , cliquez sur hello **l’exécution par lots** hello tooopen de lien Page d’aide API.</span><span class="sxs-lookup"><span data-stu-id="6227f-158">In hello **Default Endpoint** table, click hello **Batch Execution** link tooopen hello API Help Page.</span></span>
5. <span data-ttu-id="6227f-159">Créez une application console en C# dans Visual Studio : **Nouveau** > **Projet** > **Visual C#** > **Bureau classique Windows** > **Application console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="6227f-159">In Visual Studio, create a C# console application: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
6. <span data-ttu-id="6227f-160">Sur la Page d’aide de l’API de hello, recherche hello **exemple de Code** section bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="6227f-160">On hello API Help Page, find hello **Sample Code** section at hello bottom of hello page.</span></span>
7. <span data-ttu-id="6227f-161">Copiez et collez hello, exemple de code c# dans votre fichier Program.cs et de supprimer le stockage d’objets blob toohello toutes les références.</span><span class="sxs-lookup"><span data-stu-id="6227f-161">Copy and paste hello C# sample code into your Program.cs file, and remove all references toohello blob storage.</span></span>
8. <span data-ttu-id="6227f-162">Mettre à jour la valeur hello hello *apiKey* variable avec clé hello API enregistré précédemment.</span><span class="sxs-lookup"><span data-stu-id="6227f-162">Update hello value of hello *apiKey* variable with hello API key saved earlier.</span></span>
9. <span data-ttu-id="6227f-163">Recherchez hello demande déclaration et la mise à jour hello valeurs des paramètres de Service Web qui sont passés toohello *importer des données* et *exporter les données* modules.</span><span class="sxs-lookup"><span data-stu-id="6227f-163">Locate hello request declaration and update hello values of Web Service Parameters that are passed toohello *Import Data* and *Export Data* modules.</span></span> <span data-ttu-id="6227f-164">Dans ce cas, vous utilisez la requête d’origine de hello, mais définissez un nouveau nom de table.</span><span class="sxs-lookup"><span data-stu-id="6227f-164">In this case, you use hello original query, but define a new table name.</span></span>
   
        var request = new BatchExecutionRequest() 
        {           
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable2" },
            }
        };
10. <span data-ttu-id="6227f-165">Exécutez l’application hello.</span><span class="sxs-lookup"><span data-stu-id="6227f-165">Run hello application.</span></span> 

<span data-ttu-id="6227f-166">À la fin de hello exécuter, une nouvelle table est ajoutée contenant hello score des résultats de la base de données toohello.</span><span class="sxs-lookup"><span data-stu-id="6227f-166">On completion of hello run, a new table is added toohello database containing hello scoring results.</span></span>

### <a name="deploy-a-new-web-service"></a><span data-ttu-id="6227f-167">Déployer comme un nouveau service web</span><span class="sxs-lookup"><span data-stu-id="6227f-167">Deploy a New Web Service</span></span>

> [!NOTE] 
> <span data-ttu-id="6227f-168">toodeploy un nouveau service web, vous devez disposer des autorisations suffisantes dans hello abonnement toowhich vous déployez le service web de hello.</span><span class="sxs-lookup"><span data-stu-id="6227f-168">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="6227f-169">Pour plus d’informations, consultez [gérer un service Web à l’aide du portail de Services Web de Azure Machine Learning hello](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="6227f-169">For more information, see [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="6227f-170">toodeploy comme un Service Web et de créer une application tooconsume il :</span><span class="sxs-lookup"><span data-stu-id="6227f-170">toodeploy as a New Web Service and create an application tooconsume it:</span></span>

1. <span data-ttu-id="6227f-171">Au bas de hello du canevas de l’expérience hello, cliquez sur **exécuter**.</span><span class="sxs-lookup"><span data-stu-id="6227f-171">At hello bottom of hello experiment canvas, click **Run**.</span></span>
2. <span data-ttu-id="6227f-172">Hello exécuter a terminé, cliquez sur **déployer le Service Web** et sélectionnez **déployer le Service Web [nouveau]**.</span><span class="sxs-lookup"><span data-stu-id="6227f-172">When hello run has completed, click **Deploy Web Service** and select **Deploy Web Service [New]**.</span></span>
3. <span data-ttu-id="6227f-173">Sur la page de déployer une expérience de hello, entrez un nom pour votre service web, sélectionnez un plan de tarification, puis cliquez sur **déployer**.</span><span class="sxs-lookup"><span data-stu-id="6227f-173">On hello Deploy Experiment page, enter a name for your web service, and select a pricing plan, then click **Deploy**.</span></span>
4. <span data-ttu-id="6227f-174">Sur hello **Quickstart** , cliquez sur **consommer**.</span><span class="sxs-lookup"><span data-stu-id="6227f-174">On hello **Quickstart** page, click **Consume**.</span></span>
5. <span data-ttu-id="6227f-175">Bonjour **exemple de Code** , cliquez sur **lot**.</span><span class="sxs-lookup"><span data-stu-id="6227f-175">In hello **Sample Code** section, click **Batch**.</span></span>
6. <span data-ttu-id="6227f-176">Créez une application console en C# dans Visual Studio : **Nouveau** > **Projet** > **Visual C#** > **Bureau classique Windows** > **Application console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="6227f-176">In Visual Studio, create a C# console application: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
7. <span data-ttu-id="6227f-177">Copiez et collez le code d’exemple hello c# dans votre fichier Program.cs.</span><span class="sxs-lookup"><span data-stu-id="6227f-177">Copy and paste hello C# sample code into your Program.cs file.</span></span>
8. <span data-ttu-id="6227f-178">Mettre à jour la valeur hello hello *apiKey* variable avec hello **clé primaire** situé dans hello **les informations de base de la consommation** section.</span><span class="sxs-lookup"><span data-stu-id="6227f-178">Update hello value of hello *apiKey* variable with hello **Primary Key** located in hello **Basic consumption info** section.</span></span>
9. <span data-ttu-id="6227f-179">Recherchez hello *scoreRequest* les valeurs hello déclaration et la mise à jour des paramètres de Service Web qui sont passés toohello *importer des données* et *exporter les données* modules.</span><span class="sxs-lookup"><span data-stu-id="6227f-179">Locate hello *scoreRequest* declaration and update hello values of Web Service Parameters that are passed toohello *Import Data* and *Export Data* modules.</span></span> <span data-ttu-id="6227f-180">Dans ce cas, vous utilisez la requête d’origine de hello, mais définissez un nouveau nom de table.</span><span class="sxs-lookup"><span data-stu-id="6227f-180">In this case, you use hello original query, but define a new table name.</span></span>
   
        var scoreRequest = new
        {       
            Inputs = new Dictionary<string, StringTable>()
            {
            },
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable3" },
            }
        };
10. <span data-ttu-id="6227f-181">Exécutez l’application hello.</span><span class="sxs-lookup"><span data-stu-id="6227f-181">Run hello application.</span></span> 

