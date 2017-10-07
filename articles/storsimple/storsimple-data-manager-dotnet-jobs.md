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
# <a name="use-hello-net-sdk-tooinitiate-data-transformation-private-preview"></a>Utilisez hello .net SDK tooinitiate transformation des données (aperçu privé)

## <a name="overview"></a>Vue d'ensemble

Cet article explique comment vous pouvez utiliser la fonctionnalité de transformation de données hello dans hello StorSimple Data Manager service tootransform données de l’appareil StorSimple. Hello données transformées sont ensuite utilisées par d’autres services Azure dans le cloud de hello. l’article Hello a également un toohelp de procédure pas à pas créer un tooinitiate d’application exemple .NET console une tâche de transformation de données et ensuite effectuer le suivi d’achèvement.

## <a name="prerequisites"></a>Composants requis

Avant de commencer, assurez-vous de satisfaire les exigences suivantes :
*   Un système avec Visual Studio 2012, 2013, 2015 ou 2017 installé.
*   Azure Powershell installé. [Téléchargez Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).
*   Configuration travail paramètres de tooinitialize hello Transformation de données (instructions tooobtain ces paramètres sont inclus ici).
*   Une définition de travail qui a été configurée correctement dans une ressource de données hybride dans un groupe de ressources.
*   Toutes les DLL hello requis. Téléchargez ces DLL à partir de hello [référentiel GitHub](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls).
*   `Get-ConfigurationParams.ps1`[script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) à partir du référentiel github de hello.

## <a name="step-by-step"></a>Procédure pas à pas

Effectuer hello suivant les étapes toouse .NET toolaunch une tâche de transformation de données.

1. paramètres de configuration tooretrieve hello, procédez comme hello comme suit :
    1. Télécharger hello `Get-ConfigurationParams.ps1` de script de référentiel github hello dans `C:\DataTransformation` emplacement.
    1. Exécutez hello `Get-ConfigurationParams.ps1` script à partir du référentiel github de hello. Tapez hello de commande suivante :

        ```
        C:\DataTransformation\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```
        Vous pouvez passer dans toutes les valeurs de hello ActiveDirectoryKey et AppName.


2. Ce script génère hello valeurs suivantes :
    * ID client
    * ID client
    * Clé Active Directory (identique à une entrée ci-dessus hello)
    * Identifiant d’abonnement

3. À l'aide de Visual Studio 2012, 2013 ou 2015, créez une application console Visual C# .NET.

    1. Lancez **Visual Studio 2012/2013/2015**.
    1. Cliquez sur **fichier**, pointez trop**nouveau**, puis cliquez sur **projet**.
    2. Développez **Modèles**, puis sélectionnez **Visual C#**.
    3. Sélectionnez **Application Console** à partir de la liste hello des types de projets sur hello droite.
    4. Entrez **DataTransformationApp** pour hello **nom**.
    5. Sélectionnez **C:\DataTransformation** pour hello **emplacement**.
    6. Cliquez sur **OK** projet hello de toocreate.

4.  Maintenant, ajoutez toutes les DLL présents Bonjour [DLL](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) dossier en tant que **références** dans le projet hello que vous avez créé. les fichiers dll toodownload hello, procédez comme hello suivant :

    1. Dans Visual Studio, accédez trop**vue > Explorateur de solutions**.
    1. Cliquez sur hello flèche toohello gauche de projet d’application de Transformation de données. Cliquez sur **références** , cliquez sur trop**ajouter une référence**.
    2. Rechercher l’emplacement de toohello du dossier de packages hello, toutes les DLL hello, puis cliquez sur **ajouter**, puis cliquez sur **OK**.

5. Ajoutez hello suivant **à l’aide de** instructions toohello source fichier (Program.cs) hello projet.

    ```
    using System;
    using System.Collections.Generic;
    using System.Threading;
    using Microsoft.Azure.Management.HybridData.Models;
    using Microsoft.Internal.Dms.DmsWebJob;
    using Microsoft.Internal.Dms.DmsWebJob.Contracts;
    ```


6. Hello suivant code initialise l’instance de tâche de transformation de données hello. Ce complément hello **méthode Main**. Remplacez les valeurs hello des paramètres de configuration tel qu’obtenu précédemment. Les valeurs hello de plug-in **nom de groupe de ressources** et **nom de la ressource de données hybride**. Hello **nom de groupe de ressources** hello n’est celui qui héberge la ressource de données hybride hello sur quel hello définition de la tâche a été configurée.

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

7. Spécifiez hello quels hello définition du travail doit être toobe des paramètres d’exécution

    ```
    string jobDefinitionName = "job-definition-name";

    DataTransformationInput dataTransformationInput = dataTransformationJob.GetJobDefinitionParameters(jobDefinitionName);

    ```

    (OU)

    Si vous souhaitez que les paramètres de définition du travail toochange hello pendant l’exécution, puis ajoutez hello suivant de code :

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

8. Après l’initialisation de hello, ajoutez hello suivant code tootrigger une tâche de transformation de données sur la définition de la tâche hello. Plug-in hello approprié **nom de définition de la tâche**.

    ```
    // Trigger a job, retrieve hello jobId and hello retry interval for polling.
    int retryAfter;
    string jobId = dataTransformationJob.RunJobAsync(jobDefinitionName, 
    dataTransformationInput, out retryAfter);

    ```

9. Cette tâche télécharge les fichiers de hello mis en correspondance présents dans le répertoire racine de hello sur le conteneur spécifié du toohello volume StorSimple hello. Quand un fichier est chargé, un message est déposé dans la file d’attente hello (Bonjour même compte de stockage en tant que conteneur de hello) avec hello même nom en tant que définition de la tâche hello. Ce message peut être utilisé comme un tooinitiate déclencheur tout le traitement de fichier de hello.

10. Une fois la tâche de hello a été déclenchée, ajoutez hello suivant le travail de hello tootrack code d’achèvement.

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


## <a name="next-steps"></a>Étapes suivantes

[Utilisez l’interface utilisateur de gestionnaire de données StorSimple tootransform vos données](storsimple-data-manager-ui.md).
