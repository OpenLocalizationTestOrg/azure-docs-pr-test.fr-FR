---
title: "aaaRetrain existant prédictive de service web | Documents Microsoft"
description: "Découvrez comment tooretrain un modèle et mise à jour hello web service toouse hello qui vient d’être formé dans Azure Machine Learning."
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
ms.openlocfilehash: fb0760d0a2adc34fc5f3df1ae41bdac075f91bf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-an-existing-predictive-web-service"></a><span data-ttu-id="a5fde-103">Reformer un service web prédictif existant</span><span class="sxs-lookup"><span data-stu-id="a5fde-103">Retrain an existing predictive web service</span></span>
<span data-ttu-id="a5fde-104">Ce document décrit hello recyclage de processus pour hello scénario :</span><span class="sxs-lookup"><span data-stu-id="a5fde-104">This document describes hello retraining process for hello following scenario:</span></span>

* <span data-ttu-id="a5fde-105">Vous avez une expérience de formation et une expérience de prévision que vous avez déployées en tant que service web mis en œuvre.</span><span class="sxs-lookup"><span data-stu-id="a5fde-105">You have a training experiment and a predictive experiment that you have deployed as an operationalized web service.</span></span>
* <span data-ttu-id="a5fde-106">Vous avez des nouvelles données que vous souhaitez votre tooperform toouse du service web prédictif son calcul de score.</span><span class="sxs-lookup"><span data-stu-id="a5fde-106">You have new data that you want your predictive web service toouse tooperform its scoring.</span></span>

> [!NOTE] 
> <span data-ttu-id="a5fde-107">toodeploy un nouveau service web, vous devez disposer des autorisations suffisantes dans hello abonnement toowhich vous déployez le service web de hello.</span><span class="sxs-lookup"><span data-stu-id="a5fde-107">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="a5fde-108">Pour plus d’informations, consultez [gérer un service Web à l’aide du portail de Services Web de Azure Machine Learning hello](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="a5fde-108">For more information see, [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="a5fde-109">À partir de votre service web existant et les expériences, vous devez toofollow comme suit :</span><span class="sxs-lookup"><span data-stu-id="a5fde-109">Starting with your existing web service and experiments, you need toofollow these steps:</span></span>

1. <span data-ttu-id="a5fde-110">Modèle de mise à jour hello.</span><span class="sxs-lookup"><span data-stu-id="a5fde-110">Update hello model.</span></span>
   1. <span data-ttu-id="a5fde-111">Modifiez votre tooallow d’expérience d’apprentissage pour web service entrées et sorties.</span><span class="sxs-lookup"><span data-stu-id="a5fde-111">Modify your training experiment tooallow for web service inputs and outputs.</span></span>
   2. <span data-ttu-id="a5fde-112">Déployer l’expérience de formation hello comme un service web reconversion.</span><span class="sxs-lookup"><span data-stu-id="a5fde-112">Deploy hello training experiment as a retraining web service.</span></span>
   3. <span data-ttu-id="a5fde-113">Utilisez modèle de hello tooretrain d’expérience de formation hello Service de l’exécution de lot (BES).</span><span class="sxs-lookup"><span data-stu-id="a5fde-113">Use hello training experiment's Batch Execution Service (BES) tooretrain hello model.</span></span>
2. <span data-ttu-id="a5fde-114">Utilisez expérience prédictive hello du tooupdate applets de commande hello Azure Machine Learning PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a5fde-114">Use hello Azure Machine Learning PowerShell cmdlets tooupdate hello predictive experiment.</span></span>
   1. <span data-ttu-id="a5fde-115">Connectez-vous tooyour compte de gestionnaire de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="a5fde-115">Sign in tooyour Azure Resource Manager account.</span></span>
   2. <span data-ttu-id="a5fde-116">Obtenir la définition du service web hello.</span><span class="sxs-lookup"><span data-stu-id="a5fde-116">Get hello web service definition.</span></span>
   3. <span data-ttu-id="a5fde-117">Exporter la définition du service web hello au format JSON.</span><span class="sxs-lookup"><span data-stu-id="a5fde-117">Export hello web service definition as JSON.</span></span>
   4. <span data-ttu-id="a5fde-118">Mise à jour hello toohello ilearner objet blob de référence Bonjour JSON.</span><span class="sxs-lookup"><span data-stu-id="a5fde-118">Update hello reference toohello ilearner blob in hello JSON.</span></span>
   5. <span data-ttu-id="a5fde-119">Importer hello JSON dans une définition de service web.</span><span class="sxs-lookup"><span data-stu-id="a5fde-119">Import hello JSON into a web service definition.</span></span>
   6. <span data-ttu-id="a5fde-120">Mettre à jour le service web de hello avec une nouvelle définition de service web.</span><span class="sxs-lookup"><span data-stu-id="a5fde-120">Update hello web service with a new web service definition.</span></span>

## <a name="deploy-hello-training-experiment"></a><span data-ttu-id="a5fde-121">Déployer l’expérience de formation hello</span><span class="sxs-lookup"><span data-stu-id="a5fde-121">Deploy hello training experiment</span></span>
<span data-ttu-id="a5fde-122">toodeploy hello l’expérience d’apprentissage comme un service web reconversion, vous devez ajouter des entrées et sorties toohello modèle de service web.</span><span class="sxs-lookup"><span data-stu-id="a5fde-122">toodeploy hello training experiment as a retraining web service, you must add web service inputs and outputs toohello model.</span></span> <span data-ttu-id="a5fde-123">En connectant un *sortie du Service Web* d’expérience module toohello  *[Train Model] [ train-model]*  module, vous activez hello expérience d’apprentissage tooproduce un nouveau modèle formé que vous pouvez utiliser dans votre expérience prédictive.</span><span class="sxs-lookup"><span data-stu-id="a5fde-123">By connecting a *Web Service Output* module toohello experiment's *[Train Model][train-model]* module, you enable hello training experiment tooproduce a new trained model that you can use in your predictive experiment.</span></span> <span data-ttu-id="a5fde-124">Si vous avez un *modèle Evaluate* module, vous pouvez également attacher des résultats de l’évaluation web service sortie tooget hello en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="a5fde-124">If you have an *Evaluate Model* module, you can also attach web service output tooget hello evaluation results as output.</span></span>

<span data-ttu-id="a5fde-125">tooupdate votre expérience d’apprentissage :</span><span class="sxs-lookup"><span data-stu-id="a5fde-125">tooupdate your training experiment:</span></span>

1. <span data-ttu-id="a5fde-126">Connecter un *Web Service d’entrée* données tooyour du module d’entrée (par exemple, un *Clean Missing Data* module).</span><span class="sxs-lookup"><span data-stu-id="a5fde-126">Connect a *Web Service Input* module tooyour data input (for example, a *Clean Missing Data* module).</span></span> <span data-ttu-id="a5fde-127">En règle générale, vous souhaitez tooensure vos données d’entrée sont traitées dans hello la même façon que vos données d’apprentissage d’origine.</span><span class="sxs-lookup"><span data-stu-id="a5fde-127">Typically, you want tooensure that your input data is processed in hello same way as your original training data.</span></span>
2. <span data-ttu-id="a5fde-128">Connecter un *sortie du Service Web* sortie toohello de module de votre *Train Model* module.</span><span class="sxs-lookup"><span data-stu-id="a5fde-128">Connect a *Web Service Output* module toohello output of your *Train Model* module.</span></span>
3. <span data-ttu-id="a5fde-129">Si vous avez un *modèle Evaluate* module et que vous souhaitez obtenir des résultats d’évaluation toooutput hello, connectez-vous une *sortie du Service Web* sortie toohello de module de votre *modèle Evaluate* module.</span><span class="sxs-lookup"><span data-stu-id="a5fde-129">If you have an *Evaluate Model* module and you want toooutput hello evaluation results, connect a *Web Service Output* module toohello output of your *Evaluate Model* module.</span></span>

<span data-ttu-id="a5fde-130">Exécutez votre expérience.</span><span class="sxs-lookup"><span data-stu-id="a5fde-130">Run your experiment.</span></span>

<span data-ttu-id="a5fde-131">Ensuite, vous devez déployer l’expérience de formation hello comme un service web qui génère un modèle et les résultats d’évaluation du modèle.</span><span class="sxs-lookup"><span data-stu-id="a5fde-131">Next, you must deploy hello training experiment as a web service that produces a trained model and model evaluation results.</span></span>  

<span data-ttu-id="a5fde-132">Au bas de hello du canevas de l’expérience hello, cliquez sur **configurer le Service Web**, puis sélectionnez **déployer le Service Web [nouveau]**.</span><span class="sxs-lookup"><span data-stu-id="a5fde-132">At hello bottom of hello experiment canvas, click **Set Up Web Service**, and then select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="a5fde-133">portail de Services Web de Azure Machine Learning Hello ouvre toohello **déployer le Service Web** page.</span><span class="sxs-lookup"><span data-stu-id="a5fde-133">hello Azure Machine Learning Web Services portal opens toohello **Deploy Web Service** page.</span></span> <span data-ttu-id="a5fde-134">Tapez un nom pour votre service web, choisissez un plan de paiement, puis cliquez sur **Déployer**.</span><span class="sxs-lookup"><span data-stu-id="a5fde-134">Type a name for your web service, choose a payment plan, and then click **Deploy**.</span></span> <span data-ttu-id="a5fde-135">Vous pouvez uniquement utiliser la méthode de l’exécution par lots de hello pour la création de modèles formés.</span><span class="sxs-lookup"><span data-stu-id="a5fde-135">You can only use hello Batch Execution method for creating trained models.</span></span>

## <a name="retrain-hello-model-with-new-data-by-using-bes"></a><span data-ttu-id="a5fde-136">Recycler un modèle hello avec de nouvelles données à l’aide de BES</span><span class="sxs-lookup"><span data-stu-id="a5fde-136">Retrain hello model with new data by using BES</span></span>
<span data-ttu-id="a5fde-137">Pour cet exemple, nous utilisons hello toocreate c# recyclage d’application.</span><span class="sxs-lookup"><span data-stu-id="a5fde-137">For this example, we're using C# toocreate hello retraining application.</span></span> <span data-ttu-id="a5fde-138">Vous pouvez également utiliser Python ou R tooaccomplish de code d’exemple à cette tâche.</span><span class="sxs-lookup"><span data-stu-id="a5fde-138">You can also use Python or R sample code tooaccomplish this task.</span></span>

<span data-ttu-id="a5fde-139">hello toocall réapprentissage API :</span><span class="sxs-lookup"><span data-stu-id="a5fde-139">toocall hello retraining APIs:</span></span>

1. <span data-ttu-id="a5fde-140">Créez une application console en C# dans Visual Studio : **Nouveau** > **Projet** > **Visual C#** > **Bureau classique Windows** > **Application console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="a5fde-140">Create a C# console application in Visual Studio: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
2. <span data-ttu-id="a5fde-141">Se connecter toohello portail de Services Web de Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="a5fde-141">Sign in toohello Machine Learning Web Services portal.</span></span>
3. <span data-ttu-id="a5fde-142">Cliquez sur hello web service avec lequel vous travaillez.</span><span class="sxs-lookup"><span data-stu-id="a5fde-142">Click hello web service that you're working with.</span></span>
4. <span data-ttu-id="a5fde-143">Cliquez sur **Consommer**.</span><span class="sxs-lookup"><span data-stu-id="a5fde-143">Click **Consume**.</span></span>
5. <span data-ttu-id="a5fde-144">En bas de hello Hello **consommer** page hello **exemple de Code** , cliquez sur **lot**.</span><span class="sxs-lookup"><span data-stu-id="a5fde-144">At hello bottom of hello **Consume** page, in hello **Sample Code** section, click **Batch**.</span></span>
6. <span data-ttu-id="a5fde-145">Copier le code c# exemple hello pour l’exécution du lot et collez-le dans le fichier Program.cs de hello.</span><span class="sxs-lookup"><span data-stu-id="a5fde-145">Copy hello sample C# code for batch execution and paste it into hello Program.cs file.</span></span> <span data-ttu-id="a5fde-146">Assurez-vous que cet espace de noms hello reste intacte.</span><span class="sxs-lookup"><span data-stu-id="a5fde-146">Make sure that hello namespace remains intact.</span></span>

<span data-ttu-id="a5fde-147">Ajouter le package de NuGet hello Microsoft.AspNet.WebApi.Client, comme indiqué dans les commentaires de hello.</span><span class="sxs-lookup"><span data-stu-id="a5fde-147">Add hello NuGet package Microsoft.AspNet.WebApi.Client, as specified in hello comments.</span></span> <span data-ttu-id="a5fde-148">tooadd hello référence tooMicrosoft.WindowsAzure.Storage.dll, vous devrez peut-être tout d’abord tooinstall hello [bibliothèque cliente pour les services de stockage Azure](https://www.nuget.org/packages/WindowsAzure.Storage).</span><span class="sxs-lookup"><span data-stu-id="a5fde-148">tooadd hello reference tooMicrosoft.WindowsAzure.Storage.dll, you might first need tooinstall hello [client library for Azure Storage services](https://www.nuget.org/packages/WindowsAzure.Storage).</span></span>

<span data-ttu-id="a5fde-149">capture d’écran suivante Hello affiche hello **consommer** page du portail de Services Web de Azure Machine Learning hello.</span><span class="sxs-lookup"><span data-stu-id="a5fde-149">hello following screenshot shows hello **Consume** page in hello Azure Machine Learning Web Services portal.</span></span>

![Page Consommer][1]

### <a name="update-hello-apikey-declaration"></a><span data-ttu-id="a5fde-151">Mise à jour hello apikey déclaration</span><span class="sxs-lookup"><span data-stu-id="a5fde-151">Update hello apikey declaration</span></span>
<span data-ttu-id="a5fde-152">Recherchez hello **apikey** déclaration :</span><span class="sxs-lookup"><span data-stu-id="a5fde-152">Locate hello **apikey** declaration:</span></span>

    const string apiKey = "abc123"; // Replace this with hello API key for hello web service

<span data-ttu-id="a5fde-153">Bonjour **les informations de base de la consommation** section Hello **consommer** page, recherchez la clé primaire de hello et copiez-le toohello **apikey** déclaration.</span><span class="sxs-lookup"><span data-stu-id="a5fde-153">In hello **Basic consumption info** section of hello **Consume** page, locate hello primary key and copy it toohello **apikey** declaration.</span></span>

### <a name="update-hello-azure-storage-information"></a><span data-ttu-id="a5fde-154">Mettre à jour les informations de stockage Azure hello</span><span class="sxs-lookup"><span data-stu-id="a5fde-154">Update hello Azure Storage information</span></span>
<span data-ttu-id="a5fde-155">Hello, exemple de code BES télécharge un fichier à partir d’un stockage de tooAzure disque local (par exemple, « C:\temp\CensusIpnput.csv »), la traite et écrit hello résultats tooAzure arrière stockage.</span><span class="sxs-lookup"><span data-stu-id="a5fde-155">hello BES sample code uploads a file from a local drive (for example, "C:\temp\CensusIpnput.csv") tooAzure Storage, processes it, and writes hello results back tooAzure Storage.</span></span>  

<span data-ttu-id="a5fde-156">informations de stockage Azure tooupdate hello, vous devez récupérer un compte de stockage hello nom, clé et un conteneur des informations de votre compte de stockage à partir de hello portail Azure classic, puis correspondi hello de mise à jour après l’exécution de votre expérience, hello résultant flux de travail sont similaires toohello suivants :</span><span class="sxs-lookup"><span data-stu-id="a5fde-156">tooupdate hello Azure Storage information, you must retrieve hello storage account name, key, and container information for your storage account from hello Azure classic portal, and then update hello correspondi After running your experiment, hello resulting workflow should be similar toohello following:</span></span>

![Flux de travail obtenu après l’exécution][4]<span data-ttu-id="a5fde-158">valeurs NG dans le code hello.</span><span class="sxs-lookup"><span data-stu-id="a5fde-158">ng values in hello code.</span></span>

1. <span data-ttu-id="a5fde-159">Se connecter toohello portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="a5fde-159">Sign in toohello Azure classic portal.</span></span>
2. <span data-ttu-id="a5fde-160">Dans la colonne du volet de navigation gauche hello, cliquez sur **stockage**.</span><span class="sxs-lookup"><span data-stu-id="a5fde-160">In hello left navigation column, click **Storage**.</span></span>
3. <span data-ttu-id="a5fde-161">À partir de la liste de hello des comptes de stockage, sélectionnez un toostore hello reformés modèle.</span><span class="sxs-lookup"><span data-stu-id="a5fde-161">From hello list of storage accounts, select one toostore hello retrained model.</span></span>
4. <span data-ttu-id="a5fde-162">Au bas de hello de page de hello, cliquez sur **gérer les clés d’accès**.</span><span class="sxs-lookup"><span data-stu-id="a5fde-162">At hello bottom of hello page, click **Manage Access Keys**.</span></span>
5. <span data-ttu-id="a5fde-163">Copiez et enregistrez hello **clé d’accès primaire** et hello fermer la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a5fde-163">Copy and save hello **Primary Access Key** and close hello dialog.</span></span>
6. <span data-ttu-id="a5fde-164">En hello haut hello, cliquez sur **conteneurs**.</span><span class="sxs-lookup"><span data-stu-id="a5fde-164">At hello top of hello page, click **Containers**.</span></span>
7. <span data-ttu-id="a5fde-165">Sélectionnez un conteneur existant, ou créez-en un nouveau et enregistrer le nom de hello.</span><span class="sxs-lookup"><span data-stu-id="a5fde-165">Select an existing container, or create a new one and save hello name.</span></span>

<span data-ttu-id="a5fde-166">Recherchez hello *StorageAccountName*, *StorageAccountKey*, et *StorageContainerName* déclarations et les valeurs hello mise à jour que vous avez enregistré à partir du portail classique de hello .</span><span class="sxs-lookup"><span data-stu-id="a5fde-166">Locate hello *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations, and update hello values that you saved from hello classic portal.</span></span>

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure storage account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage container name

<span data-ttu-id="a5fde-167">Vous devez également vérifier que ce fichier d’entrée hello est disponible à l’emplacement de hello que vous spécifiez dans le code hello.</span><span class="sxs-lookup"><span data-stu-id="a5fde-167">You also must ensure that hello input file is available at hello location that you specify in hello code.</span></span>

### <a name="specify-hello-output-location"></a><span data-ttu-id="a5fde-168">Spécifiez l’emplacement de sortie hello</span><span class="sxs-lookup"><span data-stu-id="a5fde-168">Specify hello output location</span></span>
<span data-ttu-id="a5fde-169">Lorsque vous spécifiez l’emplacement de sortie hello Bonjour charge utile de demander, hello extension du fichier hello qui est spécifié dans *RelativeLocation* doit être spécifié en tant que `ilearner`.</span><span class="sxs-lookup"><span data-stu-id="a5fde-169">When you specify hello output location in hello Request Payload, hello extension of hello file that is specified in *RelativeLocation* must be specified as `ilearner`.</span></span> <span data-ttu-id="a5fde-170">Consultez hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="a5fde-170">See hello following example:</span></span>

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with hello location you want toouse for your output file and a valid file extension (usually .csv for scoring results or .ilearner for trained models)*/
            }
        },

<span data-ttu-id="a5fde-171">Hello Voici un exemple de sortie de recyclage : ![réapprentissage de sortie][6]</span><span class="sxs-lookup"><span data-stu-id="a5fde-171">hello following is an example of retraining output: ![Retraining output][6]</span></span>

## <a name="evaluate-hello-retraining-results"></a><span data-ttu-id="a5fde-172">Évaluer hello réapprentissage des résultats</span><span class="sxs-lookup"><span data-stu-id="a5fde-172">Evaluate hello retraining results</span></span>
<span data-ttu-id="a5fde-173">Lorsque vous exécutez des application hello, sortie de hello inclut hello URL et le jeton de signatures d’accès partagé sont des résultats de l’évaluation hello tooaccess nécessaire.</span><span class="sxs-lookup"><span data-stu-id="a5fde-173">When you run hello application, hello output includes hello URL and shared access signatures token that are necessary tooaccess hello evaluation results.</span></span>

<span data-ttu-id="a5fde-174">Vous pouvez voir les résultats des performances du modèle de hello reformé hello en combinant hello *BaseLocation*, *RelativeLocation*, et *SasBlobToken* à partir des résultats de sortie hello pour *output2* (comme indiqué dans hello précédent réapprentissage d’image de sortie) et de coller des URL complète de hello dans la barre d’adresse du navigateur hello.</span><span class="sxs-lookup"><span data-stu-id="a5fde-174">You can see hello performance results of hello retrained model by combining hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from hello output results for *output2* (as shown in hello preceding retraining output image) and pasting hello complete URL into hello browser address bar.</span></span>  

<span data-ttu-id="a5fde-175">Examinez hello résultats toodetermine si qui vient d’être formé hello effectue également assez hello tooreplace existant à un.</span><span class="sxs-lookup"><span data-stu-id="a5fde-175">Examine hello results toodetermine whether hello newly trained model performs well enough tooreplace hello existing one.</span></span>

<span data-ttu-id="a5fde-176">Hello de copie *BaseLocation*, *RelativeLocation*, et *SasBlobToken* à partir des résultats de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="a5fde-176">Copy hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from hello output results.</span></span>

## <a name="retrain-hello-web-service"></a><span data-ttu-id="a5fde-177">Recycler le service web de hello</span><span class="sxs-lookup"><span data-stu-id="a5fde-177">Retrain hello web service</span></span>
<span data-ttu-id="a5fde-178">Lorsque vous recycler un nouveau service web, vous mettez à jour hello web prédictif service définition tooreference hello nouveau modèle formé.</span><span class="sxs-lookup"><span data-stu-id="a5fde-178">When you retrain a new web service, you update hello predictive web service definition tooreference hello new trained model.</span></span> <span data-ttu-id="a5fde-179">définition du service web Hello est une représentation interne du modèle formé de hello du service web de hello et n’est pas directement modifiable.</span><span class="sxs-lookup"><span data-stu-id="a5fde-179">hello web service definition is an internal representation of hello trained model of hello web service and is not directly modifiable.</span></span> <span data-ttu-id="a5fde-180">Assurez-vous que la récupération de définition du service web hello pour votre expérience prédictive et pas votre expérience d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="a5fde-180">Make sure that you are retrieving hello web service definition for your predictive experiment and not your training experiment.</span></span>

## <a name="sign-in-tooazure-resource-manager"></a><span data-ttu-id="a5fde-181">Connectez-vous à tooAzure le Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="a5fde-181">Sign in tooAzure Resource Manager</span></span>
<span data-ttu-id="a5fde-182">Vous devez vous connecter tooyour compte Azure à partir de dans un environnement de hello PowerShell à l’aide de hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="a5fde-182">You must first sign in tooyour Azure account from within hello PowerShell environment by using hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

## <a name="get-hello-web-service-definition-object"></a><span data-ttu-id="a5fde-183">Obtenir l’objet de définition de Service Web hello</span><span class="sxs-lookup"><span data-stu-id="a5fde-183">Get hello Web Service Definition object</span></span>
<span data-ttu-id="a5fde-184">Ensuite, obtenez objet de définition de Service Web hello en appelant hello [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="a5fde-184">Next, get hello Web Service Definition object by calling hello [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

<span data-ttu-id="a5fde-185">nom de groupe ressource toodetermine hello d’un service web existant, exécutez hello applet de commande Get-AzureRmMlWebService sans aucun service web de paramètres toodisplay hello dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="a5fde-185">toodetermine hello resource group name of an existing web service, run hello Get-AzureRmMlWebService cmdlet without any parameters toodisplay hello web services in your subscription.</span></span> <span data-ttu-id="a5fde-186">Recherchez le service web de hello et observez son ID de service web.</span><span class="sxs-lookup"><span data-stu-id="a5fde-186">Locate hello web service, and then look at its web service ID.</span></span> <span data-ttu-id="a5fde-187">nom Hello hello du groupe de ressources est hello quatrième élément de hello ID, juste après hello *resourceGroups* élément.</span><span class="sxs-lookup"><span data-stu-id="a5fde-187">hello name of hello resource group is hello fourth element in hello ID, just after hello *resourceGroups* element.</span></span> <span data-ttu-id="a5fde-188">Dans l’exemple suivant de hello, nom de groupe de ressources hello est par défaut-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="a5fde-188">In hello following example, hello resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

<span data-ttu-id="a5fde-189">Vous pouvez également toodetermine hello nom groupe de ressources d’un service web, connectez-vous au portail de Services Web de Azure Machine Learning toohello.</span><span class="sxs-lookup"><span data-stu-id="a5fde-189">Alternatively, toodetermine hello resource group name of an existing web service, sign in toohello Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="a5fde-190">Sélectionnez le service web de hello.</span><span class="sxs-lookup"><span data-stu-id="a5fde-190">Select hello web service.</span></span> <span data-ttu-id="a5fde-191">nom de groupe de ressources Hello est hello cinquième élément de hello les URL du service web de hello, juste après hello *resourceGroups* élément.</span><span class="sxs-lookup"><span data-stu-id="a5fde-191">hello resource group name is hello fifth element of hello URL of hello web service, just after hello *resourceGroups* element.</span></span> <span data-ttu-id="a5fde-192">Dans l’exemple suivant de hello, nom de groupe de ressources hello est par défaut-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="a5fde-192">In hello following example, hello resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-hello-web-service-definition-object-as-json"></a><span data-ttu-id="a5fde-193">Exporter l’objet de définition de Service Web hello au format JSON</span><span class="sxs-lookup"><span data-stu-id="a5fde-193">Export hello Web Service Definition object as JSON</span></span>
<span data-ttu-id="a5fde-194">définition de hello toomodify Hello de toouse hello formé formé qui vient d’être le modèle, vous devez d’abord utiliser hello [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) tooexport de l’applet de commande qu’il les fichier tooa au format JSON.</span><span class="sxs-lookup"><span data-stu-id="a5fde-194">toomodify hello definition of hello trained model toouse hello newly trained model, you must first use hello [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet tooexport it tooa JSON-format file.</span></span>

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-hello-reference-toohello-ilearner-blob"></a><span data-ttu-id="a5fde-195">Objet blob de mise à jour hello référence toohello ilearner</span><span class="sxs-lookup"><span data-stu-id="a5fde-195">Update hello reference toohello ilearner blob</span></span>
<span data-ttu-id="a5fde-196">Dans les ressources hello, recherchez hello [modèle formé], mise à jour hello *uri* valeur Bonjour *locationInfo* nœud avec hello URI d’objet blob de hello ilearner.</span><span class="sxs-lookup"><span data-stu-id="a5fde-196">In hello assets, locate hello [trained model], update hello *uri* value in hello *locationInfo* node with hello URI of hello ilearner blob.</span></span> <span data-ttu-id="a5fde-197">URI Hello est généré en combinant hello *BaseLocation* et hello *RelativeLocation* à partir de la sortie hello Hello appel de reconversion BES.</span><span class="sxs-lookup"><span data-stu-id="a5fde-197">hello URI is generated by combining hello *BaseLocation* and hello *RelativeLocation* from hello output of hello BES retraining call.</span></span>

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

## <a name="import-hello-json-into-a-web-service-definition-object"></a><span data-ttu-id="a5fde-198">Importez des hello JSON dans un objet de définition de Service Web</span><span class="sxs-lookup"><span data-stu-id="a5fde-198">Import hello JSON into a Web Service Definition object</span></span>
<span data-ttu-id="a5fde-199">Vous devez utiliser hello [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) applet de commande tooconvert hello modifié le fichier JSON dans un objet de définition de Service Web que vous pouvez utiliser expérience de predicative tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="a5fde-199">You must use hello [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert hello modified JSON file back into a Web Service Definition object that you can use tooupdate hello predicative experiment.</span></span>

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-hello-web-service"></a><span data-ttu-id="a5fde-200">Mettre à jour hello web service</span><span class="sxs-lookup"><span data-stu-id="a5fde-200">Update hello web service</span></span>
<span data-ttu-id="a5fde-201">Enfin, utilisez hello [AzureRmMlWebService de mise à jour](https://msdn.microsoft.com/library/azure/mt767922.aspx) tooupdate de l’applet de commande hello expérience prédictive.</span><span class="sxs-lookup"><span data-stu-id="a5fde-201">Finally, use hello [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate hello predictive experiment.</span></span>

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

[1]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-consume-page.png
[4]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE04.png
[6]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE06.png

<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
