---
title: "Reformer un service web prédictif | Microsoft Docs"
description: "Apprenez à reformer un modèle et à mettre à jour le service web pour utiliser le modèle reformé dans Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: cc4c26a2-5672-4255-a767-cfd971e46775
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: v-donglo
ms.openlocfilehash: bdc994daf441d397157f8e6cbcf84d72584927f0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="retrain-an-existing-predictive-web-service"></a><span data-ttu-id="33702-103">Reformer un service web prédictif existant</span><span class="sxs-lookup"><span data-stu-id="33702-103">Retrain an existing predictive web service</span></span>
<span data-ttu-id="33702-104">Ce document décrit le processus de reformation pour le scénario suivant :</span><span class="sxs-lookup"><span data-stu-id="33702-104">This document describes the retraining process for the following scenario:</span></span>

* <span data-ttu-id="33702-105">Vous avez une expérience de formation et une expérience de prévision que vous avez déployées en tant que service web mis en œuvre.</span><span class="sxs-lookup"><span data-stu-id="33702-105">You have a training experiment and a predictive experiment that you have deployed as an operationalized web service.</span></span>
* <span data-ttu-id="33702-106">Vous disposez de nouvelles données et souhaitez que votre service web prédictif les utilise pour produire des scores.</span><span class="sxs-lookup"><span data-stu-id="33702-106">You have new data that you want your predictive web service to use to perform its scoring.</span></span>

> [!NOTE] 
> <span data-ttu-id="33702-107">Pour déployer un nouveau service web, vous devez disposer d’autorisations suffisantes dans l’abonnement dans lequel déployer le service web.</span><span class="sxs-lookup"><span data-stu-id="33702-107">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="33702-108">Pour en savoir plus, consultez la rubrique [Gérer un service web à l’aide du portail des services web Azure Machine Learning](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="33702-108">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="33702-109">En partant de vos expériences et de votre service web existants, vous devez procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="33702-109">Starting with your existing web service and experiments, you need to follow these steps:</span></span>

1. <span data-ttu-id="33702-110">Mettez le modèle à niveau.</span><span class="sxs-lookup"><span data-stu-id="33702-110">Update the model.</span></span>
   1. <span data-ttu-id="33702-111">Modifiez votre expérience de formation de façon à autoriser les entrées et sorties du service web.</span><span class="sxs-lookup"><span data-stu-id="33702-111">Modify your training experiment to allow for web service inputs and outputs.</span></span>
   2. <span data-ttu-id="33702-112">Déployez l’expérience de formation en tant que service web de reformation.</span><span class="sxs-lookup"><span data-stu-id="33702-112">Deploy the training experiment as a retraining web service.</span></span>
   3. <span data-ttu-id="33702-113">Utilisez le Service d’exécution de lots (BES, Batch Execution Service) de l’expérience de formation pour reformer le modèle.</span><span class="sxs-lookup"><span data-stu-id="33702-113">Use the training experiment's Batch Execution Service (BES) to retrain the model.</span></span>
2. <span data-ttu-id="33702-114">Utilisez les applets de commande PowerShell d’Azure Machine Learning pour mettre à jour l’expérience prédictive.</span><span class="sxs-lookup"><span data-stu-id="33702-114">Use the Azure Machine Learning PowerShell cmdlets to update the predictive experiment.</span></span>
   1. <span data-ttu-id="33702-115">Connectez-vous à votre compte Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="33702-115">Sign in to your Azure Resource Manager account.</span></span>
   2. <span data-ttu-id="33702-116">Obtenez la définition du service web.</span><span class="sxs-lookup"><span data-stu-id="33702-116">Get the web service definition.</span></span>
   3. <span data-ttu-id="33702-117">Exportez la définition du service web en tant que JSON.</span><span class="sxs-lookup"><span data-stu-id="33702-117">Export the web service definition as JSON.</span></span>
   4. <span data-ttu-id="33702-118">Mettez à jour la référence sur l’objet blob ilearner dans le JSON.</span><span class="sxs-lookup"><span data-stu-id="33702-118">Update the reference to the ilearner blob in the JSON.</span></span>
   5. <span data-ttu-id="33702-119">Importez le JSON dans une définition de service web.</span><span class="sxs-lookup"><span data-stu-id="33702-119">Import the JSON into a web service definition.</span></span>
   6. <span data-ttu-id="33702-120">Mettez à jour le service web avec la nouvelle définition de service web.</span><span class="sxs-lookup"><span data-stu-id="33702-120">Update the web service with a new web service definition.</span></span>

## <a name="deploy-the-training-experiment"></a><span data-ttu-id="33702-121">Déployer l’expérience de formation</span><span class="sxs-lookup"><span data-stu-id="33702-121">Deploy the training experiment</span></span>
<span data-ttu-id="33702-122">Pour déployer l’expérience de formation en tant que service web de reformation, vous devez ajouter les entrées et sorties du service web au modèle.</span><span class="sxs-lookup"><span data-stu-id="33702-122">To deploy the training experiment as a retraining web service, you must add web service inputs and outputs to the model.</span></span> <span data-ttu-id="33702-123">En connectant un module de *Sortie du service web* au module *[Former le modèle][train-model]* de l’expérience, vous permettez à l’expérience de formation de générer un nouveau modèle formé que vous pouvez utiliser dans votre expérience prédictive.</span><span class="sxs-lookup"><span data-stu-id="33702-123">By connecting a *Web Service Output* module to the experiment's *[Train Model][train-model]* module, you enable the training experiment to produce a new trained model that you can use in your predictive experiment.</span></span> <span data-ttu-id="33702-124">Si vous avez un module *Évaluer le modèle*, vous pouvez également attacher la sortie du service web pour obtenir les résultats d’évaluation en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="33702-124">If you have an *Evaluate Model* module, you can also attach web service output to get the evaluation results as output.</span></span>

<span data-ttu-id="33702-125">Pour mettre à jour votre expérience de formation :</span><span class="sxs-lookup"><span data-stu-id="33702-125">To update your training experiment:</span></span>

1. <span data-ttu-id="33702-126">Connectez un module d’*Entrée du service web* à votre entrée de données (par exemple, un module *Nettoyer les données manquantes*).</span><span class="sxs-lookup"><span data-stu-id="33702-126">Connect a *Web Service Input* module to your data input (for example, a *Clean Missing Data* module).</span></span> <span data-ttu-id="33702-127">En règle générale, vous souhaitez vous assurer que vos données d’entrée sont traitées de la même manière que vos données de formation d’origine.</span><span class="sxs-lookup"><span data-stu-id="33702-127">Typically, you want to ensure that your input data is processed in the same way as your original training data.</span></span>
2. <span data-ttu-id="33702-128">Connectez un module de *Sortie du service web* à la sortie de votre module *Former le modèle*.</span><span class="sxs-lookup"><span data-stu-id="33702-128">Connect a *Web Service Output* module to the output of your *Train Model* module.</span></span>
3. <span data-ttu-id="33702-129">Si vous avez un module *Évaluer le modèle* et souhaitez sortir les résultats d’évaluation, connectez un module de *Sortie du service web* à la sortie de votre module *Évaluer le modèle*.</span><span class="sxs-lookup"><span data-stu-id="33702-129">If you have an *Evaluate Model* module and you want to output the evaluation results, connect a *Web Service Output* module to the output of your *Evaluate Model* module.</span></span>

<span data-ttu-id="33702-130">Exécutez votre expérience.</span><span class="sxs-lookup"><span data-stu-id="33702-130">Run your experiment.</span></span>

<span data-ttu-id="33702-131">Ensuite, vous devez déployer l’expérience de formation en tant que service web qui produit un modèle formé et les résultats d’évaluation du modèle.</span><span class="sxs-lookup"><span data-stu-id="33702-131">Next, you must deploy the training experiment as a web service that produces a trained model and model evaluation results.</span></span>  

<span data-ttu-id="33702-132">En bas du canevas de l’expérience, cliquez sur **Configurer le service web**, puis sélectionnez **Déployer le service web [nouveau]**.</span><span class="sxs-lookup"><span data-stu-id="33702-132">At the bottom of the experiment canvas, click **Set Up Web Service**, and then select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="33702-133">Le portail des services web Azure Machine Learning s’ouvre sur la page **Déployer le service web**.</span><span class="sxs-lookup"><span data-stu-id="33702-133">The Azure Machine Learning Web Services portal opens to the **Deploy Web Service** page.</span></span> <span data-ttu-id="33702-134">Tapez un nom pour votre service web, choisissez un plan de paiement, puis cliquez sur **Déployer**.</span><span class="sxs-lookup"><span data-stu-id="33702-134">Type a name for your web service, choose a payment plan, and then click **Deploy**.</span></span> <span data-ttu-id="33702-135">Vous pouvez utiliser la méthode Exécution par lot uniquement pour créer des modèles formés.</span><span class="sxs-lookup"><span data-stu-id="33702-135">You can only use the Batch Execution method for creating trained models.</span></span>

## <a name="retrain-the-model-with-new-data-by-using-bes"></a><span data-ttu-id="33702-136">Reformer le modèle avec les nouvelles données en utilisant le BES</span><span class="sxs-lookup"><span data-stu-id="33702-136">Retrain the model with new data by using BES</span></span>
<span data-ttu-id="33702-137">Pour cet exemple, nous utilisons le langage C# pour créer l’application de reformation.</span><span class="sxs-lookup"><span data-stu-id="33702-137">For this example, we're using C# to create the retraining application.</span></span> <span data-ttu-id="33702-138">Pour accomplir cette tâche, vous pouvez également utiliser un code Python ou R.</span><span class="sxs-lookup"><span data-stu-id="33702-138">You can also use Python or R sample code to accomplish this task.</span></span>

<span data-ttu-id="33702-139">Pour appeler les API de reformation :</span><span class="sxs-lookup"><span data-stu-id="33702-139">To call the retraining APIs:</span></span>

1. <span data-ttu-id="33702-140">Créez une application console en C# dans Visual Studio : **Nouveau** > **Projet** > **Visual C#** > **Bureau classique Windows** > **Application console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="33702-140">Create a C# console application in Visual Studio: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
2. <span data-ttu-id="33702-141">Connectez-vous au portail des services web Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="33702-141">Sign in to the Machine Learning Web Services portal.</span></span>
3. <span data-ttu-id="33702-142">Cliquez sur le service web que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="33702-142">Click the web service that you're working with.</span></span>
4. <span data-ttu-id="33702-143">Cliquez sur **Consommer**.</span><span class="sxs-lookup"><span data-stu-id="33702-143">Click **Consume**.</span></span>
5. <span data-ttu-id="33702-144">En bas de la page **Utiliser**, dans la section **Exemple de code**, cliquez sur **Lot**.</span><span class="sxs-lookup"><span data-stu-id="33702-144">At the bottom of the **Consume** page, in the **Sample Code** section, click **Batch**.</span></span>
6. <span data-ttu-id="33702-145">Copiez l’exemple de code C# pour l’exécution par lot et collez-le dans le fichier Program.cs.</span><span class="sxs-lookup"><span data-stu-id="33702-145">Copy the sample C# code for batch execution and paste it into the Program.cs file.</span></span> <span data-ttu-id="33702-146">Assurez-vous que l’espace de noms reste intact.</span><span class="sxs-lookup"><span data-stu-id="33702-146">Make sure that the namespace remains intact.</span></span>

<span data-ttu-id="33702-147">Ajoutez le package NuGet Microsoft.AspNet.WebApi.Client comme indiqué dans les commentaires.</span><span class="sxs-lookup"><span data-stu-id="33702-147">Add the NuGet package Microsoft.AspNet.WebApi.Client, as specified in the comments.</span></span> <span data-ttu-id="33702-148">Pour ajouter la référence à Microsoft.WindowsAzure.Storage.dll, il se peut que vous deviez au préalable installer la [bibliothèque cliente pour les services de Stockage Azure](https://www.nuget.org/packages/WindowsAzure.Storage).</span><span class="sxs-lookup"><span data-stu-id="33702-148">To add the reference to Microsoft.WindowsAzure.Storage.dll, you might first need to install the [client library for Azure Storage services](https://www.nuget.org/packages/WindowsAzure.Storage).</span></span>

<span data-ttu-id="33702-149">La capture d’écran suivante montre la page **Consommer** du portail des services web Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="33702-149">The following screenshot shows the **Consume** page in the Azure Machine Learning Web Services portal.</span></span>

![Page Consommer][1]

### <a name="update-the-apikey-declaration"></a><span data-ttu-id="33702-151">Mettre à jour la déclaration apiKey</span><span class="sxs-lookup"><span data-stu-id="33702-151">Update the apikey declaration</span></span>
<span data-ttu-id="33702-152">Localisez la déclaration **apikey**:</span><span class="sxs-lookup"><span data-stu-id="33702-152">Locate the **apikey** declaration:</span></span>

    const string apiKey = "abc123"; // Replace this with the API key for the web service

<span data-ttu-id="33702-153">Dans la section des **informations de base sur la consommation** de la page **Utiliser**, recherchez la clé primaire et copiez-la dans la déclaration **apiKey**.</span><span class="sxs-lookup"><span data-stu-id="33702-153">In the **Basic consumption info** section of the **Consume** page, locate the primary key and copy it to the **apikey** declaration.</span></span>

### <a name="update-the-azure-storage-information"></a><span data-ttu-id="33702-154">Mettre à jour les informations Azure Storage</span><span class="sxs-lookup"><span data-stu-id="33702-154">Update the Azure Storage information</span></span>
<span data-ttu-id="33702-155">L’exemple de code BES charge un fichier à partir d’un lecteur local (par exemple, « C:\temp\CensusInput.csv ») vers le Stockage Azure, le traite, réécrit les résultats dans le Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="33702-155">The BES sample code uploads a file from a local drive (for example, "C:\temp\CensusIpnput.csv") to Azure Storage, processes it, and writes the results back to Azure Storage.</span></span>  

<span data-ttu-id="33702-156">Pour mettre à jour les informations du Stockage Azure, vous devez récupérer les informations de nom, de clé et de conteneur pour votre compte de stockage à partir du portail Azure Classic, puis mettre à jour les valeurs correspondantes dans le code. Après exécution de votre expérience, le flux de travail obtenu doit être similaire à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="33702-156">To update the Azure Storage information, you must retrieve the storage account name, key, and container information for your storage account from the Azure classic portal, and then update the correspondi After running your experiment, the resulting workflow should be similar to the following:</span></span>

![Flux de travail obtenu après l’exécution][4]<span data-ttu-id="33702-158">valeurs ng dans le code </span><span class="sxs-lookup"><span data-stu-id="33702-158">ng values in the code.</span></span>

1. <span data-ttu-id="33702-159">Connectez-vous à la version classique du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="33702-159">Sign in to the Azure classic portal.</span></span>
2. <span data-ttu-id="33702-160">Dans la colonne de navigation de gauche, cliquez sur **Stockage**.</span><span class="sxs-lookup"><span data-stu-id="33702-160">In the left navigation column, click **Storage**.</span></span>
3. <span data-ttu-id="33702-161">Dans la liste des comptes de stockage, sélectionnez-en un pour stocker le modèle reformé.</span><span class="sxs-lookup"><span data-stu-id="33702-161">From the list of storage accounts, select one to store the retrained model.</span></span>
4. <span data-ttu-id="33702-162">En bas de la page, cliquez sur **Gérer les clés d’accès**.</span><span class="sxs-lookup"><span data-stu-id="33702-162">At the bottom of the page, click **Manage Access Keys**.</span></span>
5. <span data-ttu-id="33702-163">Copiez et enregistrez la **clé d’accès primaire** , puis fermez la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="33702-163">Copy and save the **Primary Access Key** and close the dialog.</span></span>
6. <span data-ttu-id="33702-164">En haut de la page, cliquez sur **Conteneurs**.</span><span class="sxs-lookup"><span data-stu-id="33702-164">At the top of the page, click **Containers**.</span></span>
7. <span data-ttu-id="33702-165">Sélectionnez un conteneur existant ou créez-en un et enregistrez le nom.</span><span class="sxs-lookup"><span data-stu-id="33702-165">Select an existing container, or create a new one and save the name.</span></span>

<span data-ttu-id="33702-166">Localisez les déclarations *StorageAccountName*, *StorageAccountKey* et *StorageContainerName*, puis mettez à jour les valeurs que vous avez enregistrées à partir du portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="33702-166">Locate the *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations, and update the values that you saved from the classic portal.</span></span>

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure storage account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage container name

<span data-ttu-id="33702-167">Vous devez également vous assurer que le fichier d’entrée est disponible à l’emplacement spécifié dans le code.</span><span class="sxs-lookup"><span data-stu-id="33702-167">You also must ensure that the input file is available at the location that you specify in the code.</span></span>

### <a name="specify-the-output-location"></a><span data-ttu-id="33702-168">Spécifier l’emplacement de sortie</span><span class="sxs-lookup"><span data-stu-id="33702-168">Specify the output location</span></span>
<span data-ttu-id="33702-169">Lorsque vous spécifiez l’emplacement de sortie dans la Charge utile des demandes, l’extension du fichier spécifiée dans *RelativeLocation* doit être spécifiée en tant que valeur `ilearner`.</span><span class="sxs-lookup"><span data-stu-id="33702-169">When you specify the output location in the Request Payload, the extension of the file that is specified in *RelativeLocation* must be specified as `ilearner`.</span></span> <span data-ttu-id="33702-170">Voir l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="33702-170">See the following example:</span></span>

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with the location you want to use for your output file and a valid file extension (usually .csv for scoring results or .ilearner for trained models)*/
            }
        },

<span data-ttu-id="33702-171">Voici un exemple de sortie de reformation : ![Sortie de reformation][6]</span><span class="sxs-lookup"><span data-stu-id="33702-171">The following is an example of retraining output: ![Retraining output][6]</span></span>

## <a name="evaluate-the-retraining-results"></a><span data-ttu-id="33702-172">Évaluer les résultats de la reformation</span><span class="sxs-lookup"><span data-stu-id="33702-172">Evaluate the retraining results</span></span>
<span data-ttu-id="33702-173">Lorsque vous exécutez l’application, la sortie inclut l’URL et le jeton de signature d’accès partagé (SAP) nécessaires pour accéder aux résultats de l’évaluation.</span><span class="sxs-lookup"><span data-stu-id="33702-173">When you run the application, the output includes the URL and shared access signatures token that are necessary to access the evaluation results.</span></span>

<span data-ttu-id="33702-174">Vous pouvez consulter les résultats des performances du modèle reformé en combinant les éléments *BaseLocation*, *RelativeLocation* et *SasBlobToken* dans les résultats de sortie de *output2* (comme le montre l’image de sortie de reformation précédente), puis en collant l’URL complète dans la barre d’adresses du navigateur.</span><span class="sxs-lookup"><span data-stu-id="33702-174">You can see the performance results of the retrained model by combining the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results for *output2* (as shown in the preceding retraining output image) and pasting the complete URL into the browser address bar.</span></span>  

<span data-ttu-id="33702-175">Examinez les résultats pour déterminer si le modèle de nouveau entraîné est suffisamment performant pour remplacer le modèle existant.</span><span class="sxs-lookup"><span data-stu-id="33702-175">Examine the results to determine whether the newly trained model performs well enough to replace the existing one.</span></span>

<span data-ttu-id="33702-176">Copiez les éléments *BaseLocation*, *RelativeLocation* et *SasBlobToken* des résultats de sortie.</span><span class="sxs-lookup"><span data-stu-id="33702-176">Copy the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results.</span></span>

## <a name="retrain-the-web-service"></a><span data-ttu-id="33702-177">Reformer le service web</span><span class="sxs-lookup"><span data-stu-id="33702-177">Retrain the web service</span></span>
<span data-ttu-id="33702-178">Lorsque vous reformez un nouveau service web, vous mettez à jour la définition de service web prédictif pour référencer le nouveau modèle formé.</span><span class="sxs-lookup"><span data-stu-id="33702-178">When you retrain a new web service, you update the predictive web service definition to reference the new trained model.</span></span> <span data-ttu-id="33702-179">La définition du service web est une représentation interne du modèle formé du service web, qui n’est pas directement modifiable.</span><span class="sxs-lookup"><span data-stu-id="33702-179">The web service definition is an internal representation of the trained model of the web service and is not directly modifiable.</span></span> <span data-ttu-id="33702-180">Vérifiez que vous récupérez la définition du service web pour votre expérience prédictive et non pour votre expérience de formation.</span><span class="sxs-lookup"><span data-stu-id="33702-180">Make sure that you are retrieving the web service definition for your predictive experiment and not your training experiment.</span></span>

## <a name="sign-in-to-azure-resource-manager"></a><span data-ttu-id="33702-181">Se connecter à Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="33702-181">Sign in to Azure Resource Manager</span></span>
<span data-ttu-id="33702-182">Vous devez tout d’abord vous connecter à votre compte Azure à partir de l’environnement PowerShell à l’aide de l’applet de commande [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx).</span><span class="sxs-lookup"><span data-stu-id="33702-182">You must first sign in to your Azure account from within the PowerShell environment by using the [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

## <a name="get-the-web-service-definition-object"></a><span data-ttu-id="33702-183">Obtenir l’objet Définition du service web</span><span class="sxs-lookup"><span data-stu-id="33702-183">Get the Web Service Definition object</span></span>
<span data-ttu-id="33702-184">Ensuite, obtenez l’objet Définition du service web en appelant l’applet de commande [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx).</span><span class="sxs-lookup"><span data-stu-id="33702-184">Next, get the Web Service Definition object by calling the [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

<span data-ttu-id="33702-185">Pour déterminer le nom du groupe de ressources d’un service web existant, exécutez l’applet de commande Get-AzureRmMlWebService sans paramètres pour afficher les services web dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="33702-185">To determine the resource group name of an existing web service, run the Get-AzureRmMlWebService cmdlet without any parameters to display the web services in your subscription.</span></span> <span data-ttu-id="33702-186">Recherchez le service web et examinez son ID de service web.</span><span class="sxs-lookup"><span data-stu-id="33702-186">Locate the web service, and then look at its web service ID.</span></span> <span data-ttu-id="33702-187">Le nom du groupe de ressources est le quatrième élément de l’ID, juste après l’élément *resourceGroups* .</span><span class="sxs-lookup"><span data-stu-id="33702-187">The name of the resource group is the fourth element in the ID, just after the *resourceGroups* element.</span></span> <span data-ttu-id="33702-188">Dans l’exemple suivant, le nom du groupe de ressources est Default-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="33702-188">In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

<span data-ttu-id="33702-189">Pour déterminer le nom du groupe de ressources d’un service web existant, vous pouvez également vous connecter au portail des services web Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="33702-189">Alternatively, to determine the resource group name of an existing web service, sign in to the Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="33702-190">Sélectionnez le service web.</span><span class="sxs-lookup"><span data-stu-id="33702-190">Select the web service.</span></span> <span data-ttu-id="33702-191">Le nom de groupe de ressources est le cinquième élément de l’URL du service web, juste après l’élément *resourceGroups* .</span><span class="sxs-lookup"><span data-stu-id="33702-191">The resource group name is the fifth element of the URL of the web service, just after the *resourceGroups* element.</span></span> <span data-ttu-id="33702-192">Dans l’exemple suivant, le nom du groupe de ressources est Default-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="33702-192">In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-the-web-service-definition-object-as-json"></a><span data-ttu-id="33702-193">Exporter l’objet Définition du service web en tant que JSON</span><span class="sxs-lookup"><span data-stu-id="33702-193">Export the Web Service Definition object as JSON</span></span>
<span data-ttu-id="33702-194">Pour modifier la définition du modèle formé de manière à utiliser le modèle nouvellement formé, vous devez d’abord utiliser l’applet de commande [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) pour l’exporter vers un fichier au format JSON.</span><span class="sxs-lookup"><span data-stu-id="33702-194">To modify the definition of the trained model to use the newly trained model, you must first use the [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet to export it to a JSON-format file.</span></span>

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-the-reference-to-the-ilearner-blob"></a><span data-ttu-id="33702-195">Mettre à jour la référence à l’objet blob ilearner</span><span class="sxs-lookup"><span data-stu-id="33702-195">Update the reference to the ilearner blob</span></span>
<span data-ttu-id="33702-196">Dans les ressources, recherchez le [modèle formé], mettez à jour la valeur *uri* dans le nœud *locationInfo* avec l’URI de l’objet blob ilearner.</span><span class="sxs-lookup"><span data-stu-id="33702-196">In the assets, locate the [trained model], update the *uri* value in the *locationInfo* node with the URI of the ilearner blob.</span></span> <span data-ttu-id="33702-197">L’URI est générée en combinant les valeurs *BaseLocation* et *RelativeLocation* de la sortie de l’appel de reformation BES.</span><span class="sxs-lookup"><span data-stu-id="33702-197">The URI is generated by combining the *BaseLocation* and the *RelativeLocation* from the output of the BES retraining call.</span></span>

     "asset3": {
        "name": "Retrain Sample [trained model]",
        "type": "Resource",
        "locationInfo": {
          "uri": "https://mltestaccount.blob.core.windows.net/azuremlassetscontainer/baca7bca650f46218633552c0bcbba0e.ilearner"
        },
        "outputPorts": {
          "Results dataset": {
            "type": "Dataset"
          }
        }
      },

## <a name="import-the-json-into-a-web-service-definition-object"></a><span data-ttu-id="33702-198">Importer le JSON dans un objet Définition du service web</span><span class="sxs-lookup"><span data-stu-id="33702-198">Import the JSON into a Web Service Definition object</span></span>
<span data-ttu-id="33702-199">Vous devez utiliser l’applet de commande [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) pour convertir le fichier JSON modifié en un objet Définition du service web que vous pouvez utiliser pour mettre à jour l’expérience prédictive.</span><span class="sxs-lookup"><span data-stu-id="33702-199">You must use the [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet to convert the modified JSON file back into a Web Service Definition object that you can use to update the predicative experiment.</span></span>

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-the-web-service"></a><span data-ttu-id="33702-200">Mise à jour du service web</span><span class="sxs-lookup"><span data-stu-id="33702-200">Update the web service</span></span>
<span data-ttu-id="33702-201">Enfin, utilisez l’applet de commande [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) pour mettre à jour l’expérience prédictive.</span><span class="sxs-lookup"><span data-stu-id="33702-201">Finally, use the [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet to update the predictive experiment.</span></span>

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

[1]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-consume-page.png
[4]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE04.png
[6]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE06.png

<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
