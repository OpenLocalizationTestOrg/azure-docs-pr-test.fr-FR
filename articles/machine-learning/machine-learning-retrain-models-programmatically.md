---
title: "aaaRetrain apprentissage des modèles par programme | Documents Microsoft"
description: "Découvrez comment tooprogrammatically recycler un modèle et mise à jour hello web service toouse hello qui vient d’être formé dans Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: 7ae4f977-e6bf-4d04-9dde-28a66ce7b664
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: raymondl;garye;v-donglo
ms.openlocfilehash: edbb64c08f7d9edf3c76e23e0cc7e14c0125d697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-machine-learning-models-programmatically"></a><span data-ttu-id="942ab-103">Reformation des modèles Machine Learning par programme</span><span class="sxs-lookup"><span data-stu-id="942ab-103">Retrain Machine Learning models programmatically</span></span>
<span data-ttu-id="942ab-104">Dans cette procédure pas à pas, vous allez apprendre comment tooprogrammatically recycler un Service Web Azure Machine Learning à l’aide de c# et hello service d’exécution de lot Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="942ab-104">In this walkthrough, you will learn how tooprogrammatically retrain an Azure Machine Learning Web Service using C# and hello Machine Learning Batch Execution service.</span></span>

<span data-ttu-id="942ab-105">Une fois que vous avez reformés modèle de hello, hello suivant les procédures pas à pas montrent comment tooupdate hello modèle dans votre service web prédictif :</span><span class="sxs-lookup"><span data-stu-id="942ab-105">Once you have retrained hello model, hello following walkthroughs show how tooupdate hello model in your predictive web service:</span></span>

* <span data-ttu-id="942ab-106">Si vous avez déployé un service web de classique dans le portail de Services Web de Machine Learning hello, consultez [recycler le service web standard](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="942ab-106">If you deployed a Classic web service in hello Machine Learning Web Services portal, see [Retrain a Classic web service](machine-learning-retrain-a-classic-web-service.md).</span></span> 
* <span data-ttu-id="942ab-107">Si vous avez déployé un service web, consultez [recycler un nouveau service web à l’aide des applets de commande hello Machine Learning Management](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="942ab-107">If you deployed a New web service, see [Retrain a New web service using hello Machine Learning Management cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<span data-ttu-id="942ab-108">Pour une vue d’ensemble de hello recyclage de processus, consultez [recycler un modèle d’apprentissage automatique](machine-learning-retrain-machine-learning-model.md).</span><span class="sxs-lookup"><span data-stu-id="942ab-108">For an overview of hello retraining process, see [Retrain a Machine Learning Model](machine-learning-retrain-machine-learning-model.md).</span></span>

<span data-ttu-id="942ab-109">Si vous souhaitez toostart avec votre nouveau gestionnaire de ressources Azure en fonction de service web, consultez [recycler un service web prédictif existant](machine-learning-retrain-existing-resource-manager-based-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="942ab-109">If you want toostart with your existing New Azure Resource Manager based web service, see [Retrain an existing Predictive web service](machine-learning-retrain-existing-resource-manager-based-web-service.md).</span></span>

## <a name="create-a-training-experiment"></a><span data-ttu-id="942ab-110">Créez une expérience d'apprentissage</span><span class="sxs-lookup"><span data-stu-id="942ab-110">Create a training experiment</span></span>
<span data-ttu-id="942ab-111">Pour cet exemple, vous allez utiliser « exemple 5 : Evaluate Train, Test, pour la Classification binaire : jeu de données adulte » à partir d’exemples de Microsoft Azure Machine Learning hello.</span><span class="sxs-lookup"><span data-stu-id="942ab-111">For this example, you will use "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" from hello Microsoft Azure Machine Learning samples.</span></span> 

<span data-ttu-id="942ab-112">expérience de hello toocreate :</span><span class="sxs-lookup"><span data-stu-id="942ab-112">toocreate hello experiment:</span></span>

1. <span data-ttu-id="942ab-113">Connectez-vous à tooMicrosoft Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="942ab-113">Sign into tooMicrosoft Azure Machine Learning Studio.</span></span> 
2. <span data-ttu-id="942ab-114">Dans hello coin inférieur droit du tableau de bord hello, cliquez sur **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="942ab-114">On hello bottom right corner of hello dashboard, click **New**.</span></span>
3. <span data-ttu-id="942ab-115">À partir de hello Microsoft Samples, sélectionnez exemple 5.</span><span class="sxs-lookup"><span data-stu-id="942ab-115">From hello Microsoft Samples, select Sample 5.</span></span>
4. <span data-ttu-id="942ab-116">l’expérience toorename hello, haut hello du canevas de l’expérience hello, sélectionnez le nom d’expérience de hello « exemple 5 : Evaluate Train, Test, pour la Classification binaire : jeu de données adulte ».</span><span class="sxs-lookup"><span data-stu-id="942ab-116">toorename hello experiment, at hello top of hello experiment canvas, select hello experiment name "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset".</span></span>
5. <span data-ttu-id="942ab-117">Tapez Modèle de recensement.</span><span class="sxs-lookup"><span data-stu-id="942ab-117">Type Census Model.</span></span>
6. <span data-ttu-id="942ab-118">Au bas de hello du canevas de l’expérience hello, cliquez sur **exécuter**.</span><span class="sxs-lookup"><span data-stu-id="942ab-118">At hello bottom of hello experiment canvas, click **Run**.</span></span>
7. <span data-ttu-id="942ab-119">Cliquez sur **Configurer le service web**, puis sélectionnez **Reformation du service web**.</span><span class="sxs-lookup"><span data-stu-id="942ab-119">Click **Set Up web service** and select **Retraining web service**.</span></span> 

<span data-ttu-id="942ab-120">Hello Voici expérience initiale de hello.</span><span class="sxs-lookup"><span data-stu-id="942ab-120">hello following shows hello initial experiment.</span></span>
   
   ![Expérience initiale.][2]


## <a name="create-a-predictive-experiment-and-publish-as-a-web-service"></a><span data-ttu-id="942ab-122">Créer une expérience prédictive et la publier comme service web</span><span class="sxs-lookup"><span data-stu-id="942ab-122">Create a predictive experiment and publish as a web service</span></span>
<span data-ttu-id="942ab-123">Ensuite, vous créez une expérience prédictive.</span><span class="sxs-lookup"><span data-stu-id="942ab-123">Next you create a Predicative Experiment.</span></span>

1. <span data-ttu-id="942ab-124">Au bas de hello du canevas de l’expérience hello, cliquez sur **configurer le Service Web** et sélectionnez **prédictive Service Web**.</span><span class="sxs-lookup"><span data-stu-id="942ab-124">At hello bottom of hello experiment canvas, click **Set Up Web Service** and select **Predictive Web Service**.</span></span> <span data-ttu-id="942ab-125">Cela enregistre le modèle de hello sous la forme d’un modèle formé et ajoute des modules d’entrée et de sortie du service web.</span><span class="sxs-lookup"><span data-stu-id="942ab-125">This saves hello model as a Trained Model and adds web service Input and Output modules.</span></span> 
2. <span data-ttu-id="942ab-126">Cliquez sur **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="942ab-126">Click **Run**.</span></span> 
3. <span data-ttu-id="942ab-127">Une fois l’expérience de hello est terminée, cliquez sur **déployer le Service Web [standard]** ou **déployer le Service Web [nouveau]**.</span><span class="sxs-lookup"><span data-stu-id="942ab-127">After hello experiment has finished running, click **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span></span>

> [!NOTE] 
> <span data-ttu-id="942ab-128">toodeploy un nouveau service web, vous devez disposer des autorisations suffisantes dans hello abonnement toowhich vous déployez le service web de hello.</span><span class="sxs-lookup"><span data-stu-id="942ab-128">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="942ab-129">Pour plus d’informations, consultez [gérer un service Web à l’aide du portail de Services Web de Azure Machine Learning hello](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="942ab-129">For more information see, [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

## <a name="deploy-hello-training-experiment-as-a-training-web-service"></a><span data-ttu-id="942ab-130">Déployer l’expérience de formation hello comme un service web de formation</span><span class="sxs-lookup"><span data-stu-id="942ab-130">Deploy hello training experiment as a Training web service</span></span>
<span data-ttu-id="942ab-131">modèle formé de hello tooretrain, vous devez déployer l’expérience de formation hello que vous avez créé en tant que Retraining web service.</span><span class="sxs-lookup"><span data-stu-id="942ab-131">tooretrain hello trained model, you must deploy hello training experiment that you created as a Retraining web service.</span></span> <span data-ttu-id="942ab-132">Ce service web a besoin d’un *sortie du Service Web* module connecté toohello  *[Train Model] [ train-model]*  module, tooproduce en mesure de toobe nouveau modèles formés.</span><span class="sxs-lookup"><span data-stu-id="942ab-132">This web service needs a *Web Service Output* module connected toohello *[Train Model][train-model]* module, toobe able tooproduce new trained models.</span></span>

1. <span data-ttu-id="942ab-133">expérience de formation tooreturn toohello, cliquez sur icône d’expériences hello dans le volet gauche de hello, puis expérience hello nommée modèle de recensement.</span><span class="sxs-lookup"><span data-stu-id="942ab-133">tooreturn toohello training experiment, click hello Experiments icon in hello left pane, then click hello experiment named Census Model.</span></span>  
2. <span data-ttu-id="942ab-134">Dans la zone de recherche de rechercher les éléments expérience hello, type de service web.</span><span class="sxs-lookup"><span data-stu-id="942ab-134">In hello Search Experiment Items search box, type web service.</span></span> 
3. <span data-ttu-id="942ab-135">Faites glisser un *entrée du Service Web* module sur hello faire des essais canevas et se connecter à sa sortie toohello *Clean Missing Data* module.</span><span class="sxs-lookup"><span data-stu-id="942ab-135">Drag a *Web Service Input* module onto hello experiment canvas and connect its output toohello *Clean Missing Data* module.</span></span>  <span data-ttu-id="942ab-136">Cela garantit que vos données reconversion sont traitées hello la même façon que vos données d’apprentissage d’origine.</span><span class="sxs-lookup"><span data-stu-id="942ab-136">This ensures that your retraining data is processed hello same way as your original training data.</span></span>
4. <span data-ttu-id="942ab-137">Faites glisser deux *sortie de service web* modules sur hello expérimenter la zone de dessin.</span><span class="sxs-lookup"><span data-stu-id="942ab-137">Drag two *web service Output* modules onto hello experiment canvas.</span></span> <span data-ttu-id="942ab-138">Connectez la sortie hello Hello *Train Model* module tooone hello sorties et de hello *modèle Evaluate* module toohello autres.</span><span class="sxs-lookup"><span data-stu-id="942ab-138">Connect hello output of hello *Train Model* module tooone and hello output of hello *Evaluate Model* module toohello other.</span></span> <span data-ttu-id="942ab-139">Hello la sortie du service web pour **Train Model** nous donne le modèle formé hello.</span><span class="sxs-lookup"><span data-stu-id="942ab-139">hello web service output for **Train Model** gives us hello new trained model.</span></span> <span data-ttu-id="942ab-140">Hello sortie jointe trop**modèle Evaluate** retourne ce module de sortie, ce qui est des résultats de performance hello.</span><span class="sxs-lookup"><span data-stu-id="942ab-140">hello output attached too**Evaluate Model** returns that module’s output, which is hello performance results.</span></span>
5. <span data-ttu-id="942ab-141">Cliquez sur **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="942ab-141">Click **Run**.</span></span> 

<span data-ttu-id="942ab-142">Ensuite, vous devez déployer expérience de formation hello comme un service web qui génère un modèle et les résultats d’évaluation du modèle.</span><span class="sxs-lookup"><span data-stu-id="942ab-142">Next you must deploy hello training experiment as a web service that produces a trained model and model evaluation results.</span></span> <span data-ttu-id="942ab-143">tooaccomplish cela, votre prochain ensemble d’actions varient selon que vous travaillez avec un service web de classique ou un service web.</span><span class="sxs-lookup"><span data-stu-id="942ab-143">tooaccomplish this, your next set of actions are dependent on whether you are working with a Classic web service or a New web service.</span></span>  

<span data-ttu-id="942ab-144">**Service web classique**</span><span class="sxs-lookup"><span data-stu-id="942ab-144">**Classic web service**</span></span>

<span data-ttu-id="942ab-145">Au bas de hello du canevas de l’expérience hello, cliquez sur **configurer le Service Web** et sélectionnez **déployer le Service Web [standard]**.</span><span class="sxs-lookup"><span data-stu-id="942ab-145">At hello bottom of hello experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [Classic]**.</span></span> <span data-ttu-id="942ab-146">Service Web de Hello **tableau de bord** s’affiche avec la page d’aide hello clé API et hello API pour l’exécution du lot.</span><span class="sxs-lookup"><span data-stu-id="942ab-146">hello Web Service **Dashboard** is displayed with hello API Key and hello API help page for Batch Execution.</span></span> <span data-ttu-id="942ab-147">Uniquement hello méthode d’exécution du traitement par lots peut servir pour la création de modèles formés.</span><span class="sxs-lookup"><span data-stu-id="942ab-147">Only hello Batch Execution method can be used for creating Trained Models.</span></span>

<span data-ttu-id="942ab-148">**Nouveau service web**</span><span class="sxs-lookup"><span data-stu-id="942ab-148">**New web service**</span></span>

<span data-ttu-id="942ab-149">Au bas de hello du canevas de l’expérience hello, cliquez sur **configurer le Service Web** et sélectionnez **déployer le Service Web [nouveau]**.</span><span class="sxs-lookup"><span data-stu-id="942ab-149">At hello bottom of hello experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="942ab-150">portail de Services Web de Web Service Azure Machine Learning Hello ouvre la page du service web toohello déployer.</span><span class="sxs-lookup"><span data-stu-id="942ab-150">hello Web Service Azure Machine Learning Web Services portal opens toohello Deploy web service page.</span></span> <span data-ttu-id="942ab-151">Tapez un nom pour votre service web, choisissez un plan de paiement, puis cliquez sur **Déployer**.</span><span class="sxs-lookup"><span data-stu-id="942ab-151">Type a name for your web service and choose a payment plan, then click **Deploy**.</span></span> <span data-ttu-id="942ab-152">Uniquement hello méthode d’exécution du traitement par lots peut être utilisé pour la création de modèles formés</span><span class="sxs-lookup"><span data-stu-id="942ab-152">Only hello Batch Execution method can be used for creating Trained Models</span></span>

<span data-ttu-id="942ab-153">Dans les deux cas, une fois que l’expérience exécution est terminée, flux de travail qui en résulte hello doit se présenter comme suit :</span><span class="sxs-lookup"><span data-stu-id="942ab-153">In either case, after experiment has completed running, hello resulting workflow should look as follows:</span></span>

![Flux de travail produit après l’exécution.][4]



## <a name="retrain-hello-model-with-new-data-using-bes"></a><span data-ttu-id="942ab-155">Recycler un modèle de hello avec de nouvelles données à l’aide de BES</span><span class="sxs-lookup"><span data-stu-id="942ab-155">Retrain hello model with new data using BES</span></span>
<span data-ttu-id="942ab-156">Pour cet exemple, vous utilisez c# toocreate hello recyclage d’application.</span><span class="sxs-lookup"><span data-stu-id="942ab-156">For this example, you are using C# toocreate hello retraining application.</span></span> <span data-ttu-id="942ab-157">Vous pouvez également utiliser hello Python ou R exemple code tooaccomplish cette tâche.</span><span class="sxs-lookup"><span data-stu-id="942ab-157">You can also use hello Python or R sample code tooaccomplish this task.</span></span>

<span data-ttu-id="942ab-158">toocall hello réapprentissage des API :</span><span class="sxs-lookup"><span data-stu-id="942ab-158">toocall hello Retraining APIs:</span></span>

1. <span data-ttu-id="942ab-159">Créez une application console en C# dans Visual Studio : **Nouveau** > **Projet** > **Visual C#** > **Bureau classique Windows** > **Application console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="942ab-159">Create a C# console application in Visual Studio: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
2. <span data-ttu-id="942ab-160">Se connecter toohello portail du Service Web de Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="942ab-160">Sign in toohello Machine Learning Web Service portal.</span></span>
3. <span data-ttu-id="942ab-161">Si vous utilisez un service web classique, cliquez sur **Services web classiques**.</span><span class="sxs-lookup"><span data-stu-id="942ab-161">If you are working with a Classic web service, click **Classic Web Services**.</span></span>
   1. <span data-ttu-id="942ab-162">Cliquez sur le service web de hello que vous travaillez.</span><span class="sxs-lookup"><span data-stu-id="942ab-162">Click hello web service you are working with.</span></span>
   2. <span data-ttu-id="942ab-163">Cliquez sur le point de terminaison par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="942ab-163">Click hello default endpoint.</span></span>
   3. <span data-ttu-id="942ab-164">Cliquez sur **Consommer**.</span><span class="sxs-lookup"><span data-stu-id="942ab-164">Click **Consume**.</span></span>
   4. <span data-ttu-id="942ab-165">En bas de hello Hello **consommer** page hello **exemple de Code** , cliquez sur **lot**.</span><span class="sxs-lookup"><span data-stu-id="942ab-165">At hello bottom of hello **Consume** page, in hello **Sample Code** section, click **Batch**.</span></span>
   5. <span data-ttu-id="942ab-166">Continuer toostep 5 de cette procédure.</span><span class="sxs-lookup"><span data-stu-id="942ab-166">Continue toostep 5 of this procedure.</span></span>
4. <span data-ttu-id="942ab-167">Si vous utilisez un nouveau service web, cliquez sur **Services web**.</span><span class="sxs-lookup"><span data-stu-id="942ab-167">If you are working with a New web service, click **Web Services**.</span></span>
   1. <span data-ttu-id="942ab-168">Cliquez sur le service web de hello que vous travaillez.</span><span class="sxs-lookup"><span data-stu-id="942ab-168">Click hello web service you are working with.</span></span>
   2. <span data-ttu-id="942ab-169">Cliquez sur **Consommer**.</span><span class="sxs-lookup"><span data-stu-id="942ab-169">Click **Consume**.</span></span>
   3. <span data-ttu-id="942ab-170">Au bas de hello de page de consommer de hello, Bonjour **exemple de Code** , cliquez sur **lot**.</span><span class="sxs-lookup"><span data-stu-id="942ab-170">At hello bottom of hello Consume page, in hello **Sample Code** section, click **Batch**.</span></span>
5. <span data-ttu-id="942ab-171">Copier le code c# exemple hello pour l’exécution du lot et collez-le dans le fichier Program.cs hello assurant l’espace de noms hello reste intacte.</span><span class="sxs-lookup"><span data-stu-id="942ab-171">Copy hello sample C# code for batch execution and paste it into hello Program.cs file, making sure hello namespace remains intact.</span></span>

<span data-ttu-id="942ab-172">Ajouter le package de Nuget hello Microsoft.AspNet.WebApi.Client comme indiqué dans les commentaires de hello.</span><span class="sxs-lookup"><span data-stu-id="942ab-172">Add hello Nuget package Microsoft.AspNet.WebApi.Client as specified in hello comments.</span></span> <span data-ttu-id="942ab-173">tooadd hello référence tooMicrosoft.WindowsAzure.Storage.dll, vous devrez peut-être tout d’abord bibliothèque cliente de tooinstall hello pour les services de stockage Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="942ab-173">tooadd hello reference tooMicrosoft.WindowsAzure.Storage.dll, you might first need tooinstall hello client library for Microsoft Azure storage services.</span></span> <span data-ttu-id="942ab-174">Pour plus d’informations, consultez [cette page](https://www.nuget.org/packages/WindowsAzure.Storage).</span><span class="sxs-lookup"><span data-stu-id="942ab-174">For more information, see [Windows Storage Services](https://www.nuget.org/packages/WindowsAzure.Storage).</span></span>

### <a name="update-hello-apikey-declaration"></a><span data-ttu-id="942ab-175">Mise à jour hello apikey déclaration</span><span class="sxs-lookup"><span data-stu-id="942ab-175">Update hello apikey declaration</span></span>
<span data-ttu-id="942ab-176">Recherchez hello **apikey** déclaration.</span><span class="sxs-lookup"><span data-stu-id="942ab-176">Locate hello **apikey** declaration.</span></span>

    const string apiKey = "abc123"; // Replace this with hello API key for hello web service

<span data-ttu-id="942ab-177">Bonjour **les informations de base de la consommation** section Hello **consommer** page, recherchez la clé primaire de hello et copiez-le toohello **apikey** déclaration.</span><span class="sxs-lookup"><span data-stu-id="942ab-177">In hello **Basic consumption info** section of hello **Consume** page, locate hello primary key and copy it toohello **apikey** declaration.</span></span>

### <a name="update-hello-azure-storage-information"></a><span data-ttu-id="942ab-178">Mettre à jour les informations de stockage Azure hello</span><span class="sxs-lookup"><span data-stu-id="942ab-178">Update hello Azure Storage information</span></span>
<span data-ttu-id="942ab-179">Hello, exemple de code BES télécharge un fichier à partir d’un stockage de tooAzure disque local (par exemple « C:\temp\CensusIpnput.csv »), la traite et écrit hello résultats tooAzure arrière stockage.</span><span class="sxs-lookup"><span data-stu-id="942ab-179">hello BES sample code uploads a file from a local drive (For example "C:\temp\CensusIpnput.csv") tooAzure Storage, processes it, and writes hello results back tooAzure Storage.</span></span>  

<span data-ttu-id="942ab-180">tooaccomplish cette tâche, vous devez récupérer hello informations compte de stockage nom, clé et un conteneur pour votre compte de stockage depuis le portail Azure classic de hello et mise à jour hello correspondant des valeurs dans le code hello.</span><span class="sxs-lookup"><span data-stu-id="942ab-180">tooaccomplish this task, you must retrieve hello Storage account name, key, and container information for your Storage account from hello classic Azure portal and hello update corresponding values in hello code.</span></span> 

1. <span data-ttu-id="942ab-181">Se connecter toohello de portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="942ab-181">Sign in toohello classic Azure portal.</span></span>
2. <span data-ttu-id="942ab-182">Dans la colonne du volet de navigation gauche hello, cliquez sur **stockage**.</span><span class="sxs-lookup"><span data-stu-id="942ab-182">In hello left navigation column, click **Storage**.</span></span>
3. <span data-ttu-id="942ab-183">À partir de la liste de hello des comptes de stockage, sélectionnez un toostore hello reformés modèle.</span><span class="sxs-lookup"><span data-stu-id="942ab-183">From hello list of storage accounts, select one toostore hello retrained model.</span></span>
4. <span data-ttu-id="942ab-184">Au bas de hello de page de hello, cliquez sur **gérer les clés d’accès**.</span><span class="sxs-lookup"><span data-stu-id="942ab-184">At hello bottom of hello page, click **Manage Access Keys**.</span></span>
5. <span data-ttu-id="942ab-185">Copiez et enregistrez hello **clé d’accès primaire** et hello fermer la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="942ab-185">Copy and save hello **Primary Access Key** and close hello dialog.</span></span> 
6. <span data-ttu-id="942ab-186">En hello haut hello, cliquez sur **conteneurs**.</span><span class="sxs-lookup"><span data-stu-id="942ab-186">At hello top of hello page, click **Containers**.</span></span>
7. <span data-ttu-id="942ab-187">Sélectionnez un conteneur existant ou créez-en un nouveau et enregistrer le nom de hello.</span><span class="sxs-lookup"><span data-stu-id="942ab-187">Select an existing container or create a new one and save hello name.</span></span>

<span data-ttu-id="942ab-188">Recherchez hello *StorageAccountName*, *StorageAccountKey*, et *StorageContainerName* déclarations et les valeurs hello de mise à jour vous avez enregistré à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="942ab-188">Locate hello *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations and update hello values you saved from hello Azure portal.</span></span>

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure Storage Account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage Key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage Container name

<span data-ttu-id="942ab-189">Vous devez également vérifier les fichiers d’entrée hello est disponible à l’emplacement hello que vous spécifiez dans le code hello.</span><span class="sxs-lookup"><span data-stu-id="942ab-189">You also must ensure hello input file is available at hello location you specify in hello code.</span></span> 

### <a name="specify-hello-output-location"></a><span data-ttu-id="942ab-190">Spécifiez l’emplacement de sortie hello</span><span class="sxs-lookup"><span data-stu-id="942ab-190">Specify hello output location</span></span>
<span data-ttu-id="942ab-191">Lorsque vous spécifiez l’emplacement de sortie hello Bonjour charge utile de demander, hello l’extension de fichier hello spécifié dans *RelativeLocation* doit être spécifié en tant qu’ilearner.</span><span class="sxs-lookup"><span data-stu-id="942ab-191">When specifying hello output location in hello Request Payload, hello extension of hello file specified in *RelativeLocation* must be specified as ilearner.</span></span> 

<span data-ttu-id="942ab-192">Consultez hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="942ab-192">See hello following example:</span></span>

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with hello location you would like toouse for your output file, and valid file extension (usually .csv for scoring results, or .ilearner for trained models)*/
            }
        },

> [!NOTE]
> <span data-ttu-id="942ab-193">les noms de Hello de vos emplacements de sortie peuvent être différents de hello dans cette procédure pas à pas selon l’ordre de hello dans lequel vous avez ajouté des modules de sortie du service web hello.</span><span class="sxs-lookup"><span data-stu-id="942ab-193">hello names of your output locations may be different from hello ones in this walkthrough based on hello order in which you added hello web service output modules.</span></span> <span data-ttu-id="942ab-194">Étant donné que vous définissez cette expérience d’apprentissage à deux sorties, les résultats de hello incluent des informations d’emplacement de stockage pour les deux.</span><span class="sxs-lookup"><span data-stu-id="942ab-194">Since you set up this training experiment with two outputs, hello results include storage location information for both of them.</span></span>  
> 
> 

![Sortie du nouvel apprentissage.][6]

<span data-ttu-id="942ab-196">Diagramme 4 : Sortie du nouvel apprentissage.</span><span class="sxs-lookup"><span data-stu-id="942ab-196">Diagram 4: Retraining output.</span></span>

## <a name="evaluate-hello-retraining-results"></a><span data-ttu-id="942ab-197">Évaluer les résultats de recyclage hello</span><span class="sxs-lookup"><span data-stu-id="942ab-197">Evaluate hello Retraining Results</span></span>
<span data-ttu-id="942ab-198">Lorsque vous exécutez des application hello, sortie de hello inclut les URL hello et tooaccess de nécessaires jeton SAS hello des résultats d’évaluation.</span><span class="sxs-lookup"><span data-stu-id="942ab-198">When you run hello application, hello output includes hello URL and SAS token necessary tooaccess hello evaluation results.</span></span>

<span data-ttu-id="942ab-199">Vous pouvez voir les résultats des performances du modèle de hello reformé hello en combinant hello *BaseLocation*, *RelativeLocation*, et *SasBlobToken* à partir des résultats de sortie hello pour *output2* (comme indiqué dans hello précédent réapprentissage d’image de sortie) et collez l’URL complète de hello dans la barre d’adresse du navigateur hello.</span><span class="sxs-lookup"><span data-stu-id="942ab-199">You can see hello performance results of hello retrained model by combining hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from hello output results for *output2* (as shown in hello preceding retraining output image) and pasting hello complete URL in hello browser address bar.</span></span>  

<span data-ttu-id="942ab-200">Examinez hello résultats toodetermine si qui vient d’être formé hello effectue également assez hello tooreplace existant à un.</span><span class="sxs-lookup"><span data-stu-id="942ab-200">Examine hello results toodetermine whether hello newly trained model performs well enough tooreplace hello existing one.</span></span>

<span data-ttu-id="942ab-201">Hello de copie *BaseLocation*, *RelativeLocation*, et *SasBlobToken* à partir des résultats de sortie hello, vous allez les utiliser au cours de hello recyclage de processus.</span><span class="sxs-lookup"><span data-stu-id="942ab-201">Copy hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from hello output results, you will use them during hello retraining process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="942ab-202">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="942ab-202">Next steps</span></span>
<span data-ttu-id="942ab-203">Si vous avez déployé le service web prédictif de hello en cliquant sur **déployer le Service Web [standard]**, consultez [recycler le service web standard](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="942ab-203">If you deployed hello predictive web service by clicking **Deploy Web Service [Classic]**, see [Retrain a Classic web service](machine-learning-retrain-a-classic-web-service.md).</span></span>

<span data-ttu-id="942ab-204">Si vous avez déployé le service web prédictif de hello en cliquant sur **déployer le Service Web [nouveau]**, consultez [recycler un nouveau service web à l’aide des applets de commande hello Machine Learning Management](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="942ab-204">If you deployed hello predictive web service by clicking **Deploy Web Service [New]**, see [Retrain a New web service using hello Machine Learning Management cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<!-- Retrain a New web service using hello Machine Learning Management REST API -->


[1]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE01.png
[2]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE02.png
[3]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE03.png
[4]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE04.png
[5]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE05.png
[6]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE06.png
[7]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE07.png


<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
