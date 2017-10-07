---
title: "aaaUse Kit de développement .NET pour les travaux du Gestionnaire de données de Microsoft Azure StorSimple | Documents Microsoft"
description: "Découvrez comment les travaux de toouse .NET SDK toolaunch StorSimple Data Manager (version préliminaire privée)"
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
ms.openlocfilehash: b07fe64369574c994fd28d42786aa02dca435ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-net-sdk-tooinitiate-data-transformation-private-preview"></a><span data-ttu-id="76ed4-103">Utilisez hello .net SDK tooinitiate transformation des données (aperçu privé)</span><span class="sxs-lookup"><span data-stu-id="76ed4-103">Use hello .Net SDK tooinitiate data transformation (Private Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="76ed4-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="76ed4-104">Overview</span></span>

<span data-ttu-id="76ed4-105">Cet article explique comment vous pouvez utiliser la fonctionnalité de transformation de données hello dans hello StorSimple Data Manager service tootransform données de l’appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="76ed4-105">This article explains how you can use hello data transformation feature within hello StorSimple Data Manager service tootransform StorSimple device data.</span></span> <span data-ttu-id="76ed4-106">Hello données transformées sont ensuite utilisées par d’autres services Azure dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="76ed4-106">hello transformed data is then consumed by other Azure services in hello cloud.</span></span> <span data-ttu-id="76ed4-107">l’article Hello a également un toohelp de procédure pas à pas créer un tooinitiate d’application exemple .NET console une tâche de transformation de données et ensuite effectuer le suivi d’achèvement.</span><span class="sxs-lookup"><span data-stu-id="76ed4-107">hello article also has a walkthrough toohelp create a sample .NET console application tooinitiate a data transformation job and then track it for completion.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="76ed4-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="76ed4-108">Prerequisites</span></span>

<span data-ttu-id="76ed4-109">Avant de commencer, assurez-vous de satisfaire les exigences suivantes :</span><span class="sxs-lookup"><span data-stu-id="76ed4-109">Before you begin, ensure that you have:</span></span>
*   <span data-ttu-id="76ed4-110">Un système avec Visual Studio 2012, 2013, 2015 ou 2017 installé.</span><span class="sxs-lookup"><span data-stu-id="76ed4-110">A system with Visual Studio 2012, 2013, 2015, or 2017 installed.</span></span>
*   <span data-ttu-id="76ed4-111">Azure Powershell installé.</span><span class="sxs-lookup"><span data-stu-id="76ed4-111">Azure Powershell installed.</span></span> <span data-ttu-id="76ed4-112">[Téléchargez Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="76ed4-112">[Download Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
*   <span data-ttu-id="76ed4-113">Configuration travail paramètres de tooinitialize hello Transformation de données (instructions tooobtain ces paramètres sont inclus ici).</span><span class="sxs-lookup"><span data-stu-id="76ed4-113">Configuration settings tooinitialize hello Data Transformation job (instructions tooobtain these settings are included here).</span></span>
*   <span data-ttu-id="76ed4-114">Une définition de travail qui a été configurée correctement dans une ressource de données hybride dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="76ed4-114">A job definition that has been correctly configured in a Hybrid Data Resource within a Resource Group.</span></span>
*   <span data-ttu-id="76ed4-115">Toutes les DLL hello requis.</span><span class="sxs-lookup"><span data-stu-id="76ed4-115">All hello required dlls.</span></span> <span data-ttu-id="76ed4-116">Téléchargez ces DLL à partir de hello [référentiel GitHub](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls).</span><span class="sxs-lookup"><span data-stu-id="76ed4-116">Download these dlls from hello [GitHub repository](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls).</span></span>
*   <span data-ttu-id="76ed4-117">`Get-ConfigurationParams.ps1`[script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) à partir du référentiel github de hello.</span><span class="sxs-lookup"><span data-stu-id="76ed4-117">`Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) from hello github repository.</span></span>

## <a name="step-by-step"></a><span data-ttu-id="76ed4-118">Procédure pas à pas</span><span class="sxs-lookup"><span data-stu-id="76ed4-118">Step-by-step</span></span>

<span data-ttu-id="76ed4-119">Effectuer hello suivant les étapes toouse .NET toolaunch une tâche de transformation de données.</span><span class="sxs-lookup"><span data-stu-id="76ed4-119">Perform hello following steps toouse .NET toolaunch a data transformation job.</span></span>

1. <span data-ttu-id="76ed4-120">paramètres de configuration tooretrieve hello, procédez comme hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="76ed4-120">tooretrieve hello configuration parameters, do hello following steps:</span></span>
    1. <span data-ttu-id="76ed4-121">Télécharger hello `Get-ConfigurationParams.ps1` de script de référentiel github hello dans `C:\DataTransformation` emplacement.</span><span class="sxs-lookup"><span data-stu-id="76ed4-121">Download hello `Get-ConfigurationParams.ps1` from hello github repository script in `C:\DataTransformation` location.</span></span>
    1. <span data-ttu-id="76ed4-122">Exécutez hello `Get-ConfigurationParams.ps1` script à partir du référentiel github de hello.</span><span class="sxs-lookup"><span data-stu-id="76ed4-122">Run hello `Get-ConfigurationParams.ps1` script from hello github repository.</span></span> <span data-ttu-id="76ed4-123">Tapez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="76ed4-123">Type hello following command:</span></span>

        ```
        C:\DataTransformation\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```
        <span data-ttu-id="76ed4-124">Vous pouvez passer dans toutes les valeurs de hello ActiveDirectoryKey et AppName.</span><span class="sxs-lookup"><span data-stu-id="76ed4-124">You can pass in any values for hello ActiveDirectoryKey and AppName.</span></span>


2. <span data-ttu-id="76ed4-125">Ce script génère hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="76ed4-125">This script outputs hello following values:</span></span>
    * <span data-ttu-id="76ed4-126">ID client</span><span class="sxs-lookup"><span data-stu-id="76ed4-126">Client ID</span></span>
    * <span data-ttu-id="76ed4-127">ID client</span><span class="sxs-lookup"><span data-stu-id="76ed4-127">Tenant ID</span></span>
    * <span data-ttu-id="76ed4-128">Clé Active Directory (identique à une entrée ci-dessus hello)</span><span class="sxs-lookup"><span data-stu-id="76ed4-128">Active Directory key (same as hello one entered above)</span></span>
    * <span data-ttu-id="76ed4-129">Identifiant d’abonnement</span><span class="sxs-lookup"><span data-stu-id="76ed4-129">Subscription ID</span></span>

3. <span data-ttu-id="76ed4-130">À l'aide de Visual Studio 2012, 2013 ou 2015, créez une application console Visual C# .NET.</span><span class="sxs-lookup"><span data-stu-id="76ed4-130">Using Visual Studio 2012, 2013 or 2015, create a C# .NET console application.</span></span>

    1. <span data-ttu-id="76ed4-131">Lancez **Visual Studio 2012/2013/2015**.</span><span class="sxs-lookup"><span data-stu-id="76ed4-131">Launch **Visual Studio 2012/2013/2015**.</span></span>
    1. <span data-ttu-id="76ed4-132">Cliquez sur **fichier**, pointez trop**nouveau**, puis cliquez sur **projet**.</span><span class="sxs-lookup"><span data-stu-id="76ed4-132">Click **File**, point too**New**, and click **Project**.</span></span>
    2. <span data-ttu-id="76ed4-133">Développez **Modèles**, puis sélectionnez **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="76ed4-133">Expand **Templates**, and select **Visual C#**.</span></span>
    3. <span data-ttu-id="76ed4-134">Sélectionnez **Application Console** à partir de la liste hello des types de projets sur hello droite.</span><span class="sxs-lookup"><span data-stu-id="76ed4-134">Select **Console Application** from hello list of project types on hello right.</span></span>
    4. <span data-ttu-id="76ed4-135">Entrez **DataTransformationApp** pour hello **nom**.</span><span class="sxs-lookup"><span data-stu-id="76ed4-135">Enter **DataTransformationApp** for hello **Name**.</span></span>
    5. <span data-ttu-id="76ed4-136">Sélectionnez **C:\DataTransformation** pour hello **emplacement**.</span><span class="sxs-lookup"><span data-stu-id="76ed4-136">Select **C:\DataTransformation** for hello **Location**.</span></span>
    6. <span data-ttu-id="76ed4-137">Cliquez sur **OK** projet hello de toocreate.</span><span class="sxs-lookup"><span data-stu-id="76ed4-137">Click **OK** toocreate hello project.</span></span>

4.  <span data-ttu-id="76ed4-138">Maintenant, ajoutez toutes les DLL présents Bonjour [DLL](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) dossier en tant que **références** dans le projet hello que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="76ed4-138">Now, add all DLLs present in hello [dlls](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) folder as **References** in hello project that you created.</span></span> <span data-ttu-id="76ed4-139">les fichiers dll toodownload hello, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="76ed4-139">toodownload hello dll files, do hello following:</span></span>

    1. <span data-ttu-id="76ed4-140">Dans Visual Studio, accédez trop**vue > Explorateur de solutions**.</span><span class="sxs-lookup"><span data-stu-id="76ed4-140">In Visual Studio, go too**View > Solution Explorer**.</span></span>
    1. <span data-ttu-id="76ed4-141">Cliquez sur hello flèche toohello gauche de projet d’application de Transformation de données.</span><span class="sxs-lookup"><span data-stu-id="76ed4-141">Click hello arrow toohello left of Data Transformation App project.</span></span> <span data-ttu-id="76ed4-142">Cliquez sur **références** , cliquez sur trop**ajouter une référence**.</span><span class="sxs-lookup"><span data-stu-id="76ed4-142">Click **References** and then right-click too**Add Reference**.</span></span>
    2. <span data-ttu-id="76ed4-143">Rechercher l’emplacement de toohello du dossier de packages hello, toutes les DLL hello, puis cliquez sur **ajouter**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="76ed4-143">Browse toohello location of hello packages folder, select all hello DLLs and click **Add**, and then click **OK**.</span></span>

5. <span data-ttu-id="76ed4-144">Ajoutez hello suivant **à l’aide de** instructions toohello source fichier (Program.cs) hello projet.</span><span class="sxs-lookup"><span data-stu-id="76ed4-144">Add hello following **using** statements toohello source file (Program.cs) in hello project.</span></span>

    ```
    using System;
    using System.Collections.Generic;
    using System.Threading;
    using Microsoft.Azure.Management.HybridData.Models;
    using Microsoft.Internal.Dms.DmsWebJob;
    using Microsoft.Internal.Dms.DmsWebJob.Contracts;
    ```


6. <span data-ttu-id="76ed4-145">Hello suivant code initialise l’instance de tâche de transformation de données hello.</span><span class="sxs-lookup"><span data-stu-id="76ed4-145">hello following code initializes hello data transformation job instance.</span></span> <span data-ttu-id="76ed4-146">Ce complément hello **méthode Main**.</span><span class="sxs-lookup"><span data-stu-id="76ed4-146">Add this in hello **Main method**.</span></span> <span data-ttu-id="76ed4-147">Remplacez les valeurs hello des paramètres de configuration tel qu’obtenu précédemment.</span><span class="sxs-lookup"><span data-stu-id="76ed4-147">Replace hello values of configuration parameters as obtained earlier.</span></span> <span data-ttu-id="76ed4-148">Les valeurs hello de plug-in **nom de groupe de ressources** et **nom de la ressource de données hybride**.</span><span class="sxs-lookup"><span data-stu-id="76ed4-148">Plug in hello values of **Resource Group Name** and **Hybrid Data Resource name**.</span></span> <span data-ttu-id="76ed4-149">Hello **nom de groupe de ressources** hello n’est celui qui héberge la ressource de données hybride hello sur quel hello définition de la tâche a été configurée.</span><span class="sxs-lookup"><span data-stu-id="76ed4-149">hello **Resource Group Name** is hello one that hosts hello Hybrid Data Resource on which hello job definition was configured.</span></span>

    ```
    // Setup hello configuration parameters.
    var configParams = new ConfigurationParams
    {
        ClientId = "client-id",
        TenantId = "tenant-id",
        ActiveDirectoryKey = "active-directory-key",
        SubscriptionId = "subscription-id",
        ResourceGroupName = "resource-group-name",
        ResourceName = "resource-name"
    };

    // Initialize hello Data Transformation Job instance.
    DataTransformationJob dataTransformationJob = new DataTransformationJob(configParams);

    ```

7. <span data-ttu-id="76ed4-150">Spécifiez hello quels hello définition du travail doit être toobe des paramètres d’exécution</span><span class="sxs-lookup"><span data-stu-id="76ed4-150">Specify hello parameters with which hello job definition needs toobe run</span></span>

    ```
    string jobDefinitionName = "job-definition-name";

    DataTransformationInput dataTransformationInput = dataTransformationJob.GetJobDefinitionParameters(jobDefinitionName);

    ```

    <span data-ttu-id="76ed4-151">(OU)</span><span class="sxs-lookup"><span data-stu-id="76ed4-151">(OR)</span></span>

    <span data-ttu-id="76ed4-152">Si vous souhaitez que les paramètres de définition du travail toochange hello pendant l’exécution, puis ajoutez hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="76ed4-152">If you want toochange hello job definition parameters during run time, then add hello following code:</span></span>

    ```
    string jobDefinitionName = "job-definition-name";
    // Must start with a '\'
    var rootDirectories = new List<string> {@"\root"};

    // Name of hello volume on hello StorSimple device.
    var volumeNames = new List<string> {"volume-name"};

    var dataTransformationInput = new DataTransformationInput
    {
        // If you require hello latest existing backup toobe picked else use TakeNow tootrigger a new backup.
        BackupChoice = BackupChoice.UseExistingLatest.ToString(),
        // Name of hello StorSimple device.
        DeviceName = "device-name",
        // Name of hello container in Azure storage where hello files will be placed after execution.
        ContainerName = "container-name",
        // File name filter (search pattern) toobe applied on files under hello root directory. * - Match all files.
        FileNameFilter = "*",
        // List of root directories.
        RootDirectories = rootDirectories,
        // Name of hello volume on StorSimple device on which hello relevant data is present. 
        VolumeNames = volumeNames
    };
    
    ```

8. <span data-ttu-id="76ed4-153">Après l’initialisation de hello, ajoutez hello suivant code tootrigger une tâche de transformation de données sur la définition de la tâche hello.</span><span class="sxs-lookup"><span data-stu-id="76ed4-153">After hello initialization, add hello following code tootrigger a data transformation job on hello job definition.</span></span> <span data-ttu-id="76ed4-154">Plug-in hello approprié **nom de définition de la tâche**.</span><span class="sxs-lookup"><span data-stu-id="76ed4-154">Plug in hello appropriate **Job Definition Name**.</span></span>

    ```
    // Trigger a job, retrieve hello jobId and hello retry interval for polling.
    int retryAfter;
    string jobId = dataTransformationJob.RunJobAsync(jobDefinitionName, 
    dataTransformationInput, out retryAfter);

    ```

9. <span data-ttu-id="76ed4-155">Cette tâche télécharge les fichiers de hello mis en correspondance présents dans le répertoire racine de hello sur le conteneur spécifié du toohello volume StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="76ed4-155">This job uploads hello matched files present under hello root directory on hello StorSimple volume toohello specified container.</span></span> <span data-ttu-id="76ed4-156">Quand un fichier est chargé, un message est déposé dans la file d’attente hello (Bonjour même compte de stockage en tant que conteneur de hello) avec hello même nom en tant que définition de la tâche hello.</span><span class="sxs-lookup"><span data-stu-id="76ed4-156">When a file is uploaded, a message is dropped in hello queue (in hello same storage account as hello container) with hello same name as hello job definition.</span></span> <span data-ttu-id="76ed4-157">Ce message peut être utilisé comme un tooinitiate déclencheur tout le traitement de fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="76ed4-157">This message can be used as a trigger tooinitiate any further processing of hello file.</span></span>

10. <span data-ttu-id="76ed4-158">Une fois la tâche de hello a été déclenchée, ajoutez hello suivant le travail de hello tootrack code d’achèvement.</span><span class="sxs-lookup"><span data-stu-id="76ed4-158">Once hello job has been triggered, add hello following code tootrack hello job for completion.</span></span>

    ```
    Job jobDetails = null;

    // Poll hello job.
    do
    {
        jobDetails = dataTransformationJob.GetJob(jobDefinitionName, jobId);

        // Wait before polling for hello status again.
        Thread.Sleep(TimeSpan.FromSeconds(retryAfter));

    } while (jobDetails.Status == JobStatus.InProgress);

    // Completion status of hello job.
    Console.WriteLine("JobStatus: {0}", jobDetails.Status);
    
    // toohold hello console before exiting.
    Console.Read();

    ```


## <a name="next-steps"></a><span data-ttu-id="76ed4-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="76ed4-159">Next steps</span></span>

<span data-ttu-id="76ed4-160">[Utilisez l’interface utilisateur de gestionnaire de données StorSimple tootransform vos données](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="76ed4-160">[Use StorSimple Data Manager UI tootransform your data](storsimple-data-manager-ui.md).</span></span>
