---
title: "Reformation des modèles Machine Learning par programme | Microsoft Docs"
description: "Apprenez à reformer un modèle par programme et à mettre à jour le service Web pour utiliser le modèle reformé dans Azure Machine Learning."
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
ms.openlocfilehash: cf7a39e14a935d0d0e0df07e66a8f37480ec9687
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="retrain-machine-learning-models-programmatically"></a><span data-ttu-id="5173b-103">Reformation des modèles Machine Learning par programme</span><span class="sxs-lookup"><span data-stu-id="5173b-103">Retrain Machine Learning models programmatically</span></span>
<span data-ttu-id="5173b-104">Cette procédure pas à pas explique comment reformer par programmation un service web Azure Machine Learning en utilisant C# et le service d’exécution de lot Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="5173b-104">In this walkthrough, you will learn how to programmatically retrain an Azure Machine Learning Web Service using C# and the Machine Learning Batch Execution service.</span></span>

<span data-ttu-id="5173b-105">Une fois le modèle reformé, les procédures pas à pas suivantes montrent comment le mettre à jour dans votre service web prédictif :</span><span class="sxs-lookup"><span data-stu-id="5173b-105">Once you have retrained the model, the following walkthroughs show how to update the model in your predictive web service:</span></span>

* <span data-ttu-id="5173b-106">Si vous avez déployé un service web classique dans le portail des services web Azure Machine Learning, consultez [Reformer un service web classique](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="5173b-106">If you deployed a Classic web service in the Machine Learning Web Services portal, see [Retrain a Classic web service](machine-learning-retrain-a-classic-web-service.md).</span></span> 
* <span data-ttu-id="5173b-107">Si vous avez déployé un nouveau service web, consultez [Reformer un nouveau service web à l’aide des applets de commande de gestion Machine Learning](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="5173b-107">If you deployed a New web service, see [Retrain a New web service using the Machine Learning Management cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<span data-ttu-id="5173b-108">Pour une présentation du processus de reformation, voir [Reformer un modèle Machine Learning](machine-learning-retrain-machine-learning-model.md).</span><span class="sxs-lookup"><span data-stu-id="5173b-108">For an overview of the retraining process, see [Retrain a Machine Learning Model](machine-learning-retrain-machine-learning-model.md).</span></span>

<span data-ttu-id="5173b-109">Si vous voulez commencer avec votre service web Azure Resource Manager existant, consultez [Reformer un service web prédictif existant](machine-learning-retrain-existing-resource-manager-based-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="5173b-109">If you want to start with your existing New Azure Resource Manager based web service, see [Retrain an existing Predictive web service](machine-learning-retrain-existing-resource-manager-based-web-service.md).</span></span>

## <a name="create-a-training-experiment"></a><span data-ttu-id="5173b-110">Créez une expérience d'apprentissage</span><span class="sxs-lookup"><span data-stu-id="5173b-110">Create a training experiment</span></span>
<span data-ttu-id="5173b-111">Pour cet exemple, vous allez utiliser « Sample 5 : Train, Test, Evaluate for Binary Classification : Adult Dataset » dans les exemples Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="5173b-111">For this example, you will use "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" from the Microsoft Azure Machine Learning samples.</span></span> 

<span data-ttu-id="5173b-112">Pour créer l’expérience :</span><span class="sxs-lookup"><span data-stu-id="5173b-112">To create the experiment:</span></span>

1. <span data-ttu-id="5173b-113">Connectez-vous à Microsoft Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="5173b-113">Sign into to Microsoft Azure Machine Learning Studio.</span></span> 
2. <span data-ttu-id="5173b-114">En bas à droite du tableau de bord, cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="5173b-114">On the bottom right corner of the dashboard, click **New**.</span></span>
3. <span data-ttu-id="5173b-115">Parmi les exemples Microsoft, sélectionnez l’exemple 5.</span><span class="sxs-lookup"><span data-stu-id="5173b-115">From the Microsoft Samples, select Sample 5.</span></span>
4. <span data-ttu-id="5173b-116">Pour renommer l’expérience, en haut du canevas de l’expérience, sélectionnez le nom de l’expérience « Sample 5 : Train, Test, Evaluate for Binary Classification : Adult Dataset ».</span><span class="sxs-lookup"><span data-stu-id="5173b-116">To rename the experiment, at the top of the experiment canvas, select the experiment name "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset".</span></span>
5. <span data-ttu-id="5173b-117">Tapez Modèle de recensement.</span><span class="sxs-lookup"><span data-stu-id="5173b-117">Type Census Model.</span></span>
6. <span data-ttu-id="5173b-118">En bas de la zone de dessin de l’expérience, cliquez sur **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="5173b-118">At the bottom of the experiment canvas, click **Run**.</span></span>
7. <span data-ttu-id="5173b-119">Cliquez sur **Configurer le service web**, puis sélectionnez **Reformation du service web**.</span><span class="sxs-lookup"><span data-stu-id="5173b-119">Click **Set Up web service** and select **Retraining web service**.</span></span> 

<span data-ttu-id="5173b-120">L’exemple suivant illustre l’expérience initiale.</span><span class="sxs-lookup"><span data-stu-id="5173b-120">The following shows the initial experiment.</span></span>
   
   ![Expérience initiale.][2]


## <a name="create-a-predictive-experiment-and-publish-as-a-web-service"></a><span data-ttu-id="5173b-122">Créer une expérience prédictive et la publier comme service web</span><span class="sxs-lookup"><span data-stu-id="5173b-122">Create a predictive experiment and publish as a web service</span></span>
<span data-ttu-id="5173b-123">Ensuite, vous créez une expérience prédictive.</span><span class="sxs-lookup"><span data-stu-id="5173b-123">Next you create a Predicative Experiment.</span></span>

1. <span data-ttu-id="5173b-124">En bas du canevas de l’expérience, cliquez sur **Configurer le service web**, puis sélectionnez **Service web prédictif**.</span><span class="sxs-lookup"><span data-stu-id="5173b-124">At the bottom of the experiment canvas, click **Set Up Web Service** and select **Predictive Web Service**.</span></span> <span data-ttu-id="5173b-125">Le modèle est enregistré sous forme d’un modèle formé, et des modules d’entrée et de sortie du service web sont ajoutés.</span><span class="sxs-lookup"><span data-stu-id="5173b-125">This saves the model as a Trained Model and adds web service Input and Output modules.</span></span> 
2. <span data-ttu-id="5173b-126">Cliquez sur **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="5173b-126">Click **Run**.</span></span> 
3. <span data-ttu-id="5173b-127">Une fois l’exécution de l’expérience terminée, cliquez sur **Déployer le service web [classique]** ou **Déployer le service web [nouveau]**.</span><span class="sxs-lookup"><span data-stu-id="5173b-127">After the experiment has finished running, click **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span></span>

> [!NOTE] 
> <span data-ttu-id="5173b-128">Pour déployer un nouveau service web, vous devez disposer d’autorisations suffisantes dans l’abonnement dans lequel déployer le service web.</span><span class="sxs-lookup"><span data-stu-id="5173b-128">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="5173b-129">Pour en savoir plus, consultez la rubrique [Gérer un service web à l’aide du portail des services web Azure Machine Learning](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="5173b-129">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

## <a name="deploy-the-training-experiment-as-a-training-web-service"></a><span data-ttu-id="5173b-130">Déployer l’expérience de formation comme service web de formation</span><span class="sxs-lookup"><span data-stu-id="5173b-130">Deploy the training experiment as a Training web service</span></span>
<span data-ttu-id="5173b-131">Pour reformer le modèle, vous devez déployer l’expérience de formation que vous avez créée comme service web de reformation.</span><span class="sxs-lookup"><span data-stu-id="5173b-131">To retrain the trained model, you must deploy the training experiment that you created as a Retraining web service.</span></span> <span data-ttu-id="5173b-132">Ce service web a besoin d’un module *Sortie du service web* connecté au module *[Former le modèle][train-model]* afin de pouvoir produire de nouveaux modèles formés.</span><span class="sxs-lookup"><span data-stu-id="5173b-132">This web service needs a *Web Service Output* module connected to the *[Train Model][train-model]* module, to be able to produce new trained models.</span></span>

1. <span data-ttu-id="5173b-133">Pour revenir à l’expérience d’apprentissage, cliquez sur l’icône Expériences dans le volet gauche, puis sur l’expérience nommée Modèle de recensement.</span><span class="sxs-lookup"><span data-stu-id="5173b-133">To return to the training experiment, click the Experiments icon in the left pane, then click the experiment named Census Model.</span></span>  
2. <span data-ttu-id="5173b-134">Dans la zone de recherche des éléments d’expérience, tapez Service web.</span><span class="sxs-lookup"><span data-stu-id="5173b-134">In the Search Experiment Items search box, type web service.</span></span> 
3. <span data-ttu-id="5173b-135">Faites glisser un module *Entrée du service web* dans le canevas de l’expérience et connectez sa sortie au module *Nettoyer les données manquantes*.</span><span class="sxs-lookup"><span data-stu-id="5173b-135">Drag a *Web Service Input* module onto the experiment canvas and connect its output to the *Clean Missing Data* module.</span></span>  <span data-ttu-id="5173b-136">Cela garantit que vos données de reformation sont traitées de la même manière que vos données de formation d’origine.</span><span class="sxs-lookup"><span data-stu-id="5173b-136">This ensures that your retraining data is processed the same way as your original training data.</span></span>
4. <span data-ttu-id="5173b-137">Faites glisser deux modules *Sortie du service web* sur le canevas de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="5173b-137">Drag two *web service Output* modules onto the experiment canvas.</span></span> <span data-ttu-id="5173b-138">Connectez la sortie du module *Former le modèle* à l’un des modules, et la sortie du module *Évaluer le modèle* à l’autre.</span><span class="sxs-lookup"><span data-stu-id="5173b-138">Connect the output of the *Train Model* module to one and the output of the *Evaluate Model* module to the other.</span></span> <span data-ttu-id="5173b-139">La sortie du service web pour **Former le modèle** nous fournit le nouveau modèle formé.</span><span class="sxs-lookup"><span data-stu-id="5173b-139">The web service output for **Train Model** gives us the new trained model.</span></span> <span data-ttu-id="5173b-140">La sortie attachée au module **Évaluer le modèle** retourne la sortie de celui-ci, c’est-à-dire les résultats des performances.</span><span class="sxs-lookup"><span data-stu-id="5173b-140">The output attached to **Evaluate Model** returns that module’s output, which is the performance results.</span></span>
5. <span data-ttu-id="5173b-141">Cliquez sur **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="5173b-141">Click **Run**.</span></span> 

<span data-ttu-id="5173b-142">Ensuite, vous devez déployer l’expérience de formation comme service web qui produit un modèle formé et les résultats d’évaluation du modèle.</span><span class="sxs-lookup"><span data-stu-id="5173b-142">Next you must deploy the training experiment as a web service that produces a trained model and model evaluation results.</span></span> <span data-ttu-id="5173b-143">La procédure diffère selon que vous utilisez un service web classique ou un nouveau service web.</span><span class="sxs-lookup"><span data-stu-id="5173b-143">To accomplish this, your next set of actions are dependent on whether you are working with a Classic web service or a New web service.</span></span>  

<span data-ttu-id="5173b-144">**Service web classique**</span><span class="sxs-lookup"><span data-stu-id="5173b-144">**Classic web service**</span></span>

<span data-ttu-id="5173b-145">En bas du canevas de l’expérience, cliquez sur **Configurer le service web**, puis sélectionnez **Service web [classique]**.</span><span class="sxs-lookup"><span data-stu-id="5173b-145">At the bottom of the experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [Classic]**.</span></span> <span data-ttu-id="5173b-146">Le **Tableau de bord** du service web s’affiche avec la clé API et la page d’aide d’API pour l’exécution par lots.</span><span class="sxs-lookup"><span data-stu-id="5173b-146">The Web Service **Dashboard** is displayed with the API Key and the API help page for Batch Execution.</span></span> <span data-ttu-id="5173b-147">Seule la méthode d’exécution par lots peut être utilisée pour créer des modèles entraînés.</span><span class="sxs-lookup"><span data-stu-id="5173b-147">Only the Batch Execution method can be used for creating Trained Models.</span></span>

<span data-ttu-id="5173b-148">**Nouveau service web**</span><span class="sxs-lookup"><span data-stu-id="5173b-148">**New web service**</span></span>

<span data-ttu-id="5173b-149">En bas du canevas de l’expérience, cliquez sur **Configurer le service web**, puis sélectionnez **Déployer le service web [nouveau]**.</span><span class="sxs-lookup"><span data-stu-id="5173b-149">At the bottom of the experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="5173b-150">Le portail de services web Azure Machine Learning s’ouvre sur la page Déployer le service web.</span><span class="sxs-lookup"><span data-stu-id="5173b-150">The Web Service Azure Machine Learning Web Services portal opens to the Deploy web service page.</span></span> <span data-ttu-id="5173b-151">Tapez un nom pour votre service web, choisissez un plan de paiement, puis cliquez sur **Déployer**.</span><span class="sxs-lookup"><span data-stu-id="5173b-151">Type a name for your web service and choose a payment plan, then click **Deploy**.</span></span> <span data-ttu-id="5173b-152">Seule la méthode d’exécution par lot peut être utilisée pour créer des modèles formés.</span><span class="sxs-lookup"><span data-stu-id="5173b-152">Only the Batch Execution method can be used for creating Trained Models</span></span>

<span data-ttu-id="5173b-153">Dans les deux cas, une fois l’exécution de l’expérience terminée, le flux de travail doit ressembler à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="5173b-153">In either case, after experiment has completed running, the resulting workflow should look as follows:</span></span>

![Flux de travail produit après l’exécution.][4]



## <a name="retrain-the-model-with-new-data-using-bes"></a><span data-ttu-id="5173b-155">Effectuer à nouveau l’apprentissage du modèle avec de nouvelles données à l’aide de BES</span><span class="sxs-lookup"><span data-stu-id="5173b-155">Retrain the model with new data using BES</span></span>
<span data-ttu-id="5173b-156">Pour cet exemple, vous utilisez le langage C# pour créer l’application de reformation.</span><span class="sxs-lookup"><span data-stu-id="5173b-156">For this example, you are using C# to create the retraining application.</span></span> <span data-ttu-id="5173b-157">Pour accomplir cette tâche, vous pouvez également utiliser l’exemple de code Python ou R.</span><span class="sxs-lookup"><span data-stu-id="5173b-157">You can also use the Python or R sample code to accomplish this task.</span></span>

<span data-ttu-id="5173b-158">Pour appeler les API Retraining :</span><span class="sxs-lookup"><span data-stu-id="5173b-158">To call the Retraining APIs:</span></span>

1. <span data-ttu-id="5173b-159">Créez une application console en C# dans Visual Studio : **Nouveau** > **Projet** > **Visual C#** > **Bureau classique Windows** > **Application console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="5173b-159">Create a C# console application in Visual Studio: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
2. <span data-ttu-id="5173b-160">Connectez-vous au portail de services web Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="5173b-160">Sign in to the Machine Learning Web Service portal.</span></span>
3. <span data-ttu-id="5173b-161">Si vous utilisez un service web classique, cliquez sur **Services web classiques**.</span><span class="sxs-lookup"><span data-stu-id="5173b-161">If you are working with a Classic web service, click **Classic Web Services**.</span></span>
   1. <span data-ttu-id="5173b-162">Cliquez sur le service web utilisé.</span><span class="sxs-lookup"><span data-stu-id="5173b-162">Click the web service you are working with.</span></span>
   2. <span data-ttu-id="5173b-163">Cliquez sur le point de terminaison par défaut.</span><span class="sxs-lookup"><span data-stu-id="5173b-163">Click the default endpoint.</span></span>
   3. <span data-ttu-id="5173b-164">Cliquez sur **Consommer**.</span><span class="sxs-lookup"><span data-stu-id="5173b-164">Click **Consume**.</span></span>
   4. <span data-ttu-id="5173b-165">En bas de la page **Utiliser**, dans la section **Exemple de code**, cliquez sur **Lot**.</span><span class="sxs-lookup"><span data-stu-id="5173b-165">At the bottom of the **Consume** page, in the **Sample Code** section, click **Batch**.</span></span>
   5. <span data-ttu-id="5173b-166">Passez à l’étape 5 de cette procédure.</span><span class="sxs-lookup"><span data-stu-id="5173b-166">Continue to step 5 of this procedure.</span></span>
4. <span data-ttu-id="5173b-167">Si vous utilisez un nouveau service web, cliquez sur **Services web**.</span><span class="sxs-lookup"><span data-stu-id="5173b-167">If you are working with a New web service, click **Web Services**.</span></span>
   1. <span data-ttu-id="5173b-168">Cliquez sur le service web utilisé.</span><span class="sxs-lookup"><span data-stu-id="5173b-168">Click the web service you are working with.</span></span>
   2. <span data-ttu-id="5173b-169">Cliquez sur **Consommer**.</span><span class="sxs-lookup"><span data-stu-id="5173b-169">Click **Consume**.</span></span>
   3. <span data-ttu-id="5173b-170">En bas de la page Utiliser, dans la section **Exemple de code**, cliquez sur **Lot**.</span><span class="sxs-lookup"><span data-stu-id="5173b-170">At the bottom of the Consume page, in the **Sample Code** section, click **Batch**.</span></span>
5. <span data-ttu-id="5173b-171">Copiez l’exemple de code C# pour l’exécution par lot et collez-le dans le fichier Program.cs en veillant à ne pas modifier l’espace de noms.</span><span class="sxs-lookup"><span data-stu-id="5173b-171">Copy the sample C# code for batch execution and paste it into the Program.cs file, making sure the namespace remains intact.</span></span>

<span data-ttu-id="5173b-172">Ajoutez le package NuGet Microsoft.AspNet.WebApi.Client comme indiqué dans les commentaires.</span><span class="sxs-lookup"><span data-stu-id="5173b-172">Add the Nuget package Microsoft.AspNet.WebApi.Client as specified in the comments.</span></span> <span data-ttu-id="5173b-173">Pour ajouter une référence à Microsoft.WindowsAzure.Storage.dll, il se peut que vous deviez au préalable installer la bibliothèque cliente pour les services de stockage Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="5173b-173">To add the reference to Microsoft.WindowsAzure.Storage.dll, you might first need to install the client library for Microsoft Azure storage services.</span></span> <span data-ttu-id="5173b-174">Pour plus d’informations, consultez [cette page](https://www.nuget.org/packages/WindowsAzure.Storage).</span><span class="sxs-lookup"><span data-stu-id="5173b-174">For more information, see [Windows Storage Services](https://www.nuget.org/packages/WindowsAzure.Storage).</span></span>

### <a name="update-the-apikey-declaration"></a><span data-ttu-id="5173b-175">Mettre à jour la déclaration apiKey</span><span class="sxs-lookup"><span data-stu-id="5173b-175">Update the apikey declaration</span></span>
<span data-ttu-id="5173b-176">Localisez la déclaration **apiKey** .</span><span class="sxs-lookup"><span data-stu-id="5173b-176">Locate the **apikey** declaration.</span></span>

    const string apiKey = "abc123"; // Replace this with the API key for the web service

<span data-ttu-id="5173b-177">Dans la section des **informations de base sur la consommation** de la page **Utiliser**, recherchez la clé primaire et copiez-la dans la déclaration **apiKey**.</span><span class="sxs-lookup"><span data-stu-id="5173b-177">In the **Basic consumption info** section of the **Consume** page, locate the primary key and copy it to the **apikey** declaration.</span></span>

### <a name="update-the-azure-storage-information"></a><span data-ttu-id="5173b-178">Mettre à jour les informations Azure Storage</span><span class="sxs-lookup"><span data-stu-id="5173b-178">Update the Azure Storage information</span></span>
<span data-ttu-id="5173b-179">L’exemple de code BES charge un fichier à partir d’un lecteur local (par exemple, « C:\temp\CensusInput.csv ») vers Azure Storage, le traite et réécrit les résultats dans Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="5173b-179">The BES sample code uploads a file from a local drive (For example "C:\temp\CensusIpnput.csv") to Azure Storage, processes it, and writes the results back to Azure Storage.</span></span>  

<span data-ttu-id="5173b-180">Pour réaliser cette tâche, vous devez récupérer les informations de nom de compte, de clé et de conteneur de stockage pour votre compte de stockage depuis le portail Azure Classic et mettre à jour les valeurs correspondantes dans le code.</span><span class="sxs-lookup"><span data-stu-id="5173b-180">To accomplish this task, you must retrieve the Storage account name, key, and container information for your Storage account from the classic Azure portal and the update corresponding values in the code.</span></span> 

1. <span data-ttu-id="5173b-181">Connectez-vous au portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="5173b-181">Sign in to the classic Azure portal.</span></span>
2. <span data-ttu-id="5173b-182">Dans la colonne de navigation de gauche, cliquez sur **Stockage**.</span><span class="sxs-lookup"><span data-stu-id="5173b-182">In the left navigation column, click **Storage**.</span></span>
3. <span data-ttu-id="5173b-183">Dans la liste des comptes de stockage, sélectionnez-en un pour stocker le modèle reformé.</span><span class="sxs-lookup"><span data-stu-id="5173b-183">From the list of storage accounts, select one to store the retrained model.</span></span>
4. <span data-ttu-id="5173b-184">En bas de la page, cliquez sur **Gérer les clés d’accès**.</span><span class="sxs-lookup"><span data-stu-id="5173b-184">At the bottom of the page, click **Manage Access Keys**.</span></span>
5. <span data-ttu-id="5173b-185">Copiez et enregistrez la **clé d’accès primaire** , puis fermez la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="5173b-185">Copy and save the **Primary Access Key** and close the dialog.</span></span> 
6. <span data-ttu-id="5173b-186">En haut de la page, cliquez sur **Conteneurs**.</span><span class="sxs-lookup"><span data-stu-id="5173b-186">At the top of the page, click **Containers**.</span></span>
7. <span data-ttu-id="5173b-187">Sélectionnez un conteneur existant ou créez-en un et enregistrez le nom.</span><span class="sxs-lookup"><span data-stu-id="5173b-187">Select an existing container or create a new one and save the name.</span></span>

<span data-ttu-id="5173b-188">Localisez les déclarations *StorageAccountName*, *StorageAccountKey* et *StorageContainerName*, et mettez à jour les valeurs que vous avez enregistrées à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5173b-188">Locate the *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations and update the values you saved from the Azure portal.</span></span>

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure Storage Account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage Key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage Container name

<span data-ttu-id="5173b-189">Vous devez également vous assurer que le fichier d’entrée est disponible à l’emplacement spécifié dans le code.</span><span class="sxs-lookup"><span data-stu-id="5173b-189">You also must ensure the input file is available at the location you specify in the code.</span></span> 

### <a name="specify-the-output-location"></a><span data-ttu-id="5173b-190">Spécifier l’emplacement de sortie</span><span class="sxs-lookup"><span data-stu-id="5173b-190">Specify the output location</span></span>
<span data-ttu-id="5173b-191">Lorsque vous spécifiez l’emplacement de sortie dans la charge utile des demandes, l’extension du fichier spécifiée dans *RelativeLocation* doit avoir pour valeur ilearner.</span><span class="sxs-lookup"><span data-stu-id="5173b-191">When specifying the output location in the Request Payload, the extension of the file specified in *RelativeLocation* must be specified as ilearner.</span></span> 

<span data-ttu-id="5173b-192">Voir l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="5173b-192">See the following example:</span></span>

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with the location you would like to use for your output file, and valid file extension (usually .csv for scoring results, or .ilearner for trained models)*/
            }
        },

> [!NOTE]
> <span data-ttu-id="5173b-193">Le nom de vos emplacements de sortie peut être différent de ceux de cette procédure pas à pas, selon l’ordre dans lequel vous avez ajouté les modules de sortie du service web.</span><span class="sxs-lookup"><span data-stu-id="5173b-193">The names of your output locations may be different from the ones in this walkthrough based on the order in which you added the web service output modules.</span></span> <span data-ttu-id="5173b-194">Étant donné que vous avez défini cette expérience de formation avec deux sorties, les résultats incluent les informations d’emplacement de stockage des deux.</span><span class="sxs-lookup"><span data-stu-id="5173b-194">Since you set up this training experiment with two outputs, the results include storage location information for both of them.</span></span>  
> 
> 

![Sortie du nouvel apprentissage.][6]

<span data-ttu-id="5173b-196">Diagramme 4 : Sortie du nouvel apprentissage.</span><span class="sxs-lookup"><span data-stu-id="5173b-196">Diagram 4: Retraining output.</span></span>

## <a name="evaluate-the-retraining-results"></a><span data-ttu-id="5173b-197">Évaluer les résultats du nouvel apprentissage</span><span class="sxs-lookup"><span data-stu-id="5173b-197">Evaluate the Retraining Results</span></span>
<span data-ttu-id="5173b-198">Lorsque vous exécutez l’application, la sortie inclut le jeton SAP et l’URL nécessaires pour accéder aux résultats de l’évaluation.</span><span class="sxs-lookup"><span data-stu-id="5173b-198">When you run the application, the output includes the URL and SAS token necessary to access the evaluation results.</span></span>

<span data-ttu-id="5173b-199">Vous pouvez consulter les résultats des performances du modèle de nouveau entraîné en combinant *BaseLocation*, *RelativeLocation* et *SasBlobToken* dans les résultats de sortie de *output2* (comme le montre l’image de sortie de la reformation précédente), puis en collant l’URL complète dans la barre d’adresses du navigateur.</span><span class="sxs-lookup"><span data-stu-id="5173b-199">You can see the performance results of the retrained model by combining the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results for *output2* (as shown in the preceding retraining output image) and pasting the complete URL in the browser address bar.</span></span>  

<span data-ttu-id="5173b-200">Examinez les résultats pour déterminer si le modèle de nouveau entraîné est suffisamment performant pour remplacer le modèle existant.</span><span class="sxs-lookup"><span data-stu-id="5173b-200">Examine the results to determine whether the newly trained model performs well enough to replace the existing one.</span></span>

<span data-ttu-id="5173b-201">Copiez les éléments *BaseLocation*, *RelativeLocation* et *SasBlobToken* des résultats de sortie. Vous allez les utiliser pendant le processus de reformation.</span><span class="sxs-lookup"><span data-stu-id="5173b-201">Copy the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results, you will use them during the retraining process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5173b-202">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5173b-202">Next steps</span></span>
<span data-ttu-id="5173b-203">Si vous avez déployé le service web prédictif en cliquant sur **Déployer un service web [classique]**, consultez [Reformer un service web classique](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="5173b-203">If you deployed the predictive web service by clicking **Deploy Web Service [Classic]**, see [Retrain a Classic web service](machine-learning-retrain-a-classic-web-service.md).</span></span>

<span data-ttu-id="5173b-204">Si vous avez déployé le service web prédictif en cliquant sur **Déployer un service web [nouveau]**, consultez [Reformer un nouveau service web à l’aide des applets de commande de gestion Machine Learning](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="5173b-204">If you deployed the predictive web service by clicking **Deploy Web Service [New]**, see [Retrain a New web service using the Machine Learning Management cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<!-- Retrain a New web service using the Machine Learning Management REST API -->


[1]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE01.png
[2]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE02.png
[3]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE03.png
[4]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE04.png
[5]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE05.png
[6]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE06.png
[7]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE07.png


<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
