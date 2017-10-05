---
title: "Utiliser le kit SDK .NET pour les travaux Microsoft Azure StorSimple Data Manager | Microsoft Docs"
description: "Découvrez comment utiliser le Kit SDK .NET pour lancer les travaux StorSimple Data Manager (version préliminaire privée)"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: 44d243a034b20b99faf284c8615e470bc6f9d020
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="use-the-net-sdk-to-initiate-data-transformation-private-preview"></a><span data-ttu-id="594f1-103">Utiliser le kit SDK .NET pour initier la transformation des données (préversion privée)</span><span class="sxs-lookup"><span data-stu-id="594f1-103">Use the .Net SDK to initiate data transformation (Private Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="594f1-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="594f1-104">Overview</span></span>

<span data-ttu-id="594f1-105">Cet article vous explique comment utiliser la fonctionnalité de transformation des données au sein du service StorSimple Data Manager afin de transformer les données de l’appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="594f1-105">This article explains how you can use the data transformation feature within the StorSimple Data Manager service to transform StorSimple device data.</span></span> <span data-ttu-id="594f1-106">Les données transformées sont ensuite utilisées par d’autres services Azure dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="594f1-106">The transformed data is then consumed by other Azure services in the cloud.</span></span> <span data-ttu-id="594f1-107">L’article comporte également une procédure pas à pas pour créer un exemple d’application console .NET pour initier un travail de transformation de données et effectuer son suivi.</span><span class="sxs-lookup"><span data-stu-id="594f1-107">The article also has a walkthrough to help create a sample .NET console application to initiate a data transformation job and then track it for completion.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="594f1-108">Prérequis</span><span class="sxs-lookup"><span data-stu-id="594f1-108">Prerequisites</span></span>

<span data-ttu-id="594f1-109">Avant de commencer, assurez-vous de satisfaire les exigences suivantes :</span><span class="sxs-lookup"><span data-stu-id="594f1-109">Before you begin, ensure that you have:</span></span>
*   <span data-ttu-id="594f1-110">Un système avec Visual Studio 2012, 2013, 2015 ou 2017 installé.</span><span class="sxs-lookup"><span data-stu-id="594f1-110">A system with Visual Studio 2012, 2013, 2015, or 2017 installed.</span></span>
*   <span data-ttu-id="594f1-111">Azure Powershell installé.</span><span class="sxs-lookup"><span data-stu-id="594f1-111">Azure Powershell installed.</span></span> <span data-ttu-id="594f1-112">[Téléchargez Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="594f1-112">[Download Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
*   <span data-ttu-id="594f1-113">Les paramètres de configuration pour initialiser le travail de transformation des données (les instructions pour obtenir ces paramètres sont disponibles ici).</span><span class="sxs-lookup"><span data-stu-id="594f1-113">Configuration settings to initialize the Data Transformation job (instructions to obtain these settings are included here).</span></span>
*   <span data-ttu-id="594f1-114">Une définition de travail qui a été configurée correctement dans une ressource de données hybride dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="594f1-114">A job definition that has been correctly configured in a Hybrid Data Resource within a Resource Group.</span></span>
*   <span data-ttu-id="594f1-115">Toutes les DLL requises.</span><span class="sxs-lookup"><span data-stu-id="594f1-115">All the required dlls.</span></span> <span data-ttu-id="594f1-116">Téléchargez ces DLL à partir du [dépôt GitHub](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls).</span><span class="sxs-lookup"><span data-stu-id="594f1-116">Download these dlls from the [GitHub repository](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls).</span></span>
*   <span data-ttu-id="594f1-117">`Get-ConfigurationParams.ps1` Le [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) du dépôt GitHub.</span><span class="sxs-lookup"><span data-stu-id="594f1-117">`Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) from the github repository.</span></span>

## <a name="step-by-step"></a><span data-ttu-id="594f1-118">Procédure pas à pas</span><span class="sxs-lookup"><span data-stu-id="594f1-118">Step-by-step</span></span>

<span data-ttu-id="594f1-119">Procédez comme suit pour utiliser .NET pour lancer un travail de transformation de données.</span><span class="sxs-lookup"><span data-stu-id="594f1-119">Perform the following steps to use .NET to launch a data transformation job.</span></span>

1. <span data-ttu-id="594f1-120">Pour récupérer les paramètres de configuration, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="594f1-120">To retrieve the configuration parameters, do the following steps:</span></span>
    1. <span data-ttu-id="594f1-121">Téléchargez l’élément `Get-ConfigurationParams.ps1` à partir du script du dépôt GitHub, dans l’emplacement `C:\DataTransformation`.</span><span class="sxs-lookup"><span data-stu-id="594f1-121">Download the `Get-ConfigurationParams.ps1` from the github repository script in `C:\DataTransformation` location.</span></span>
    1. <span data-ttu-id="594f1-122">Exécutez le script `Get-ConfigurationParams.ps1` à partir du dépôt GitHub.</span><span class="sxs-lookup"><span data-stu-id="594f1-122">Run the `Get-ConfigurationParams.ps1` script from the github repository.</span></span> <span data-ttu-id="594f1-123">Tapez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="594f1-123">Type the following command:</span></span>

        ```
        C:\DataTransformation\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```
        <span data-ttu-id="594f1-124">Vous pouvez saisir les valeurs de votre choix pour les éléments ActiveDirectoryKey et AppName.</span><span class="sxs-lookup"><span data-stu-id="594f1-124">You can pass in any values for the ActiveDirectoryKey and AppName.</span></span>


2. <span data-ttu-id="594f1-125">Ce script génère les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="594f1-125">This script outputs the following values:</span></span>
    * <span data-ttu-id="594f1-126">ID client</span><span class="sxs-lookup"><span data-stu-id="594f1-126">Client ID</span></span>
    * <span data-ttu-id="594f1-127">ID client</span><span class="sxs-lookup"><span data-stu-id="594f1-127">Tenant ID</span></span>
    * <span data-ttu-id="594f1-128">Clé Active Directory (identique à celle entrée ci-dessus)</span><span class="sxs-lookup"><span data-stu-id="594f1-128">Active Directory key (same as the one entered above)</span></span>
    * <span data-ttu-id="594f1-129">Identifiant d’abonnement</span><span class="sxs-lookup"><span data-stu-id="594f1-129">Subscription ID</span></span>

3. <span data-ttu-id="594f1-130">À l'aide de Visual Studio 2012, 2013 ou 2015, créez une application console Visual C# .NET.</span><span class="sxs-lookup"><span data-stu-id="594f1-130">Using Visual Studio 2012, 2013 or 2015, create a C# .NET console application.</span></span>

    1. <span data-ttu-id="594f1-131">Lancez **Visual Studio 2012/2013/2015**.</span><span class="sxs-lookup"><span data-stu-id="594f1-131">Launch **Visual Studio 2012/2013/2015**.</span></span>
    1. <span data-ttu-id="594f1-132">Cliquez sur **Fichier**, pointez le curseur de la souris sur **Nouveau**, puis cliquez sur **Projet**.</span><span class="sxs-lookup"><span data-stu-id="594f1-132">Click **File**, point to **New**, and click **Project**.</span></span>
    2. <span data-ttu-id="594f1-133">Développez **Modèles**, puis sélectionnez **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="594f1-133">Expand **Templates**, and select **Visual C#**.</span></span>
    3. <span data-ttu-id="594f1-134">Sélectionnez **Application console** dans la liste des types de projet située sur la droite.</span><span class="sxs-lookup"><span data-stu-id="594f1-134">Select **Console Application** from the list of project types on the right.</span></span>
    4. <span data-ttu-id="594f1-135">Saisissez **DataTransformationApp** pour le **Nom**.</span><span class="sxs-lookup"><span data-stu-id="594f1-135">Enter **DataTransformationApp** for the **Name**.</span></span>
    5. <span data-ttu-id="594f1-136">Sélectionnez **C:\DataTransformation** pour l’**Emplacement**.</span><span class="sxs-lookup"><span data-stu-id="594f1-136">Select **C:\DataTransformation** for the **Location**.</span></span>
    6. <span data-ttu-id="594f1-137">Cliquez sur **OK** pour créer le projet.</span><span class="sxs-lookup"><span data-stu-id="594f1-137">Click **OK** to create the project.</span></span>

4.  <span data-ttu-id="594f1-138">Maintenant, ajoutez l’ensemble des DLL présentes dans le dossier [dédié](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) en tant que **Références**dans le projet que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="594f1-138">Now, add all DLLs present in the [dlls](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) folder as **References** in the project that you created.</span></span> <span data-ttu-id="594f1-139">Pour télécharger les fichiers DLL, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="594f1-139">To download the dll files, do the following:</span></span>

    1. <span data-ttu-id="594f1-140">Dans Visual Studio, accédez à **Affichage > Explorateur de solutions**.</span><span class="sxs-lookup"><span data-stu-id="594f1-140">In Visual Studio, go to **View > Solution Explorer**.</span></span>
    1. <span data-ttu-id="594f1-141">Cliquez sur la flèche à gauche du projet de l’application de transformation des données.</span><span class="sxs-lookup"><span data-stu-id="594f1-141">Click the arrow to the left of Data Transformation App project.</span></span> <span data-ttu-id="594f1-142">Cliquez sur **Références**, puis cliquez avec le bouton droit sur **Ajouter une référence**.</span><span class="sxs-lookup"><span data-stu-id="594f1-142">Click **References** and then right-click to **Add Reference**.</span></span>
    2. <span data-ttu-id="594f1-143">Accédez à l’emplacement du dossier des packages, sélectionnez l’ensemble des DLL, puis cliquez sur **Ajouter** et sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="594f1-143">Browse to the location of the packages folder, select all the DLLs and click **Add**, and then click **OK**.</span></span>

5. <span data-ttu-id="594f1-144">Ajoutez les instructions **using** suivantes au fichier source (Program.cs) dans le projet.</span><span class="sxs-lookup"><span data-stu-id="594f1-144">Add the following **using** statements to the source file (Program.cs) in the project.</span></span>

    ```
    using System;
    using System.Collections.Generic;
    using System.Threading;
    using Microsoft.Azure.Management.HybridData.Models;
    using Microsoft.Internal.Dms.DmsWebJob;
    using Microsoft.Internal.Dms.DmsWebJob.Contracts;
    ```


6. <span data-ttu-id="594f1-145">Le code suivant initialise l’instance du travail de transformation de données.</span><span class="sxs-lookup"><span data-stu-id="594f1-145">The following code initializes the data transformation job instance.</span></span> <span data-ttu-id="594f1-146">Add this in the **Méthode Main**.</span><span class="sxs-lookup"><span data-stu-id="594f1-146">Add this in the **Main method**.</span></span> <span data-ttu-id="594f1-147">Remplacez les valeurs des paramètres de configuration obtenues précédemment.</span><span class="sxs-lookup"><span data-stu-id="594f1-147">Replace the values of configuration parameters as obtained earlier.</span></span> <span data-ttu-id="594f1-148">Insérez les valeurs de **Nom du groupe de ressources** et **Nom de la ressource de données hybride**.</span><span class="sxs-lookup"><span data-stu-id="594f1-148">Plug in the values of **Resource Group Name** and **Hybrid Data Resource name**.</span></span> <span data-ttu-id="594f1-149">Le **Nom du groupe de ressources**est celui qui héberge la ressource de données hybride sur laquelle a été configurée la définition de travail.</span><span class="sxs-lookup"><span data-stu-id="594f1-149">The **Resource Group Name** is the one that hosts the Hybrid Data Resource on which the job definition was configured.</span></span>

    ```
    // Setup the configuration parameters.
    var configParams = new ConfigurationParams
    {
        ClientId = "client-id",
        TenantId = "tenant-id",
        ActiveDirectoryKey = "active-directory-key",
        SubscriptionId = "subscription-id",
        ResourceGroupName = "resource-group-name",
        ResourceName = "resource-name"
    };

    // Initialize the Data Transformation Job instance.
    DataTransformationJob dataTransformationJob = new DataTransformationJob(configParams);

    ```

7. <span data-ttu-id="594f1-150">Spécifiez les paramètres avec lesquels exécuter la définition de travail</span><span class="sxs-lookup"><span data-stu-id="594f1-150">Specify the parameters with which the job definition needs to be run</span></span>

    ```
    string jobDefinitionName = "job-definition-name";

    DataTransformationInput dataTransformationInput = dataTransformationJob.GetJobDefinitionParameters(jobDefinitionName);

    ```

    <span data-ttu-id="594f1-151">(OU)</span><span class="sxs-lookup"><span data-stu-id="594f1-151">(OR)</span></span>

    <span data-ttu-id="594f1-152">Si vous souhaitez modifier les paramètres de définition de travail durant l’exécution, ajoutez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="594f1-152">If you want to change the job definition parameters during run time, then add the following code:</span></span>

    ```
    string jobDefinitionName = "job-definition-name";
    // Must start with a '\'
    var rootDirectories = new List<string> {@"\root"};

    // Name of the volume on the StorSimple device.
    var volumeNames = new List<string> {"volume-name"};

    var dataTransformationInput = new DataTransformationInput
    {
        // If you require the latest existing backup to be picked else use TakeNow to trigger a new backup.
        BackupChoice = BackupChoice.UseExistingLatest.ToString(),
        // Name of the StorSimple device.
        DeviceName = "device-name",
        // Name of the container in Azure storage where the files will be placed after execution.
        ContainerName = "container-name",
        // File name filter (search pattern) to be applied on files under the root directory. * - Match all files.
        FileNameFilter = "*",
        // List of root directories.
        RootDirectories = rootDirectories,
        // Name of the volume on StorSimple device on which the relevant data is present. 
        VolumeNames = volumeNames
    };
    
    ```

8. <span data-ttu-id="594f1-153">Après l’initialisation, ajoutez le code suivant pour déclencher un travail de transformation de données sur la définition de travail.</span><span class="sxs-lookup"><span data-stu-id="594f1-153">After the initialization, add the following code to trigger a data transformation job on the job definition.</span></span> <span data-ttu-id="594f1-154">Insérez le **Job Definition Name** (Nom de définition de travail).</span><span class="sxs-lookup"><span data-stu-id="594f1-154">Plug in the appropriate **Job Definition Name**.</span></span>

    ```
    // Trigger a job, retrieve the jobId and the retry interval for polling.
    int retryAfter;
    string jobId = dataTransformationJob.RunJobAsync(jobDefinitionName, 
    dataTransformationInput, out retryAfter);

    ```

9. <span data-ttu-id="594f1-155">Ce travail charge les fichiers correspondants présents sous le répertoire racine du volume StorSimple sur le conteneur spécifié.</span><span class="sxs-lookup"><span data-stu-id="594f1-155">This job uploads the matched files present under the root directory on the StorSimple volume to the specified container.</span></span> <span data-ttu-id="594f1-156">Lorsqu’un fichier est chargé, un message est déposé dans la file d’attente (dans le compte de stockage du conteneur), avec le nom de la définition de travail.</span><span class="sxs-lookup"><span data-stu-id="594f1-156">When a file is uploaded, a message is dropped in the queue (in the same storage account as the container) with the same name as the job definition.</span></span> <span data-ttu-id="594f1-157">Ce message peut être utilisé comme un déclencheur pour initier le traitement ultérieur du fichier.</span><span class="sxs-lookup"><span data-stu-id="594f1-157">This message can be used as a trigger to initiate any further processing of the file.</span></span>

10. <span data-ttu-id="594f1-158">Une fois le travail déclenché, ajoutez le code suivant afin de suivre son exécution.</span><span class="sxs-lookup"><span data-stu-id="594f1-158">Once the job has been triggered, add the following code to track the job for completion.</span></span>

    ```
    Job jobDetails = null;

    // Poll the job.
    do
    {
        jobDetails = dataTransformationJob.GetJob(jobDefinitionName, jobId);

        // Wait before polling for the status again.
        Thread.Sleep(TimeSpan.FromSeconds(retryAfter));

    } while (jobDetails.Status == JobStatus.InProgress);

    // Completion status of the job.
    Console.WriteLine("JobStatus: {0}", jobDetails.Status);
    
    // To hold the console before exiting.
    Console.Read();

    ```


## <a name="next-steps"></a><span data-ttu-id="594f1-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="594f1-159">Next steps</span></span>

<span data-ttu-id="594f1-160">[Utilisez l’interface utilisateur de StorSimple Data Manager pour transformer vos données](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="594f1-160">[Use StorSimple Data Manager UI to transform your data](storsimple-data-manager-ui.md).</span></span>
