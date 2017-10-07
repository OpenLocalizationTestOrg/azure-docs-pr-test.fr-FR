---
title: "chemin d’accès des blob aaaChange à partir de la valeur par défaut hello | Documents Microsoft"
description: "Apprenez comment tooset d’Azure fonctionner toorename un chemin d’accès du fichier blob (aperçu privé)"
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
ms.date: 03/16/2017
ms.author: vidarmsft
ms.openlocfilehash: 2c414603514223c701ab1a3bd0b81ee18f1af666
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="change-a-blob-path-from-hello-default-path-private-preview"></a><span data-ttu-id="3a2e3-103">Modifier un chemin d’accès de l’objet blob à partir du chemin d’accès par défaut de hello (aperçu privé)</span><span class="sxs-lookup"><span data-stu-id="3a2e3-103">Change a blob path from hello default path (private preview)</span></span>

<span data-ttu-id="3a2e3-104">Cet article décrit comment tooset d’Azure fonction toorename un chemin de fichier blob par défaut.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-104">This article describes how tooset up an Azure function toorename a default blob file path.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3a2e3-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="3a2e3-105">Prerequisites</span></span>

<span data-ttu-id="3a2e3-106">Vérifiez que vous disposez d’une définition de travail qui a été configurée correctement dans une ressource de données hybride dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-106">Ensure that you have a job definition that has been correctly configured in a hybrid data resource within a resource group.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="3a2e3-107">Création d’une fonction Azure</span><span class="sxs-lookup"><span data-stu-id="3a2e3-107">Create an Azure function</span></span>

<span data-ttu-id="3a2e3-108">toocreate une fonction d’Azure, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="3a2e3-108">toocreate an Azure function, do hello following:</span></span>

1. <span data-ttu-id="3a2e3-109">Accédez toohello [portail Azure](http://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3a2e3-109">Go toohello [Azure portal](http://portal.azure.com/).</span></span>

2. <span data-ttu-id="3a2e3-110">Haut hello du volet gauche de hello, cliquez sur **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-110">At hello top of hello left pane, click **New**.</span></span> 

3. <span data-ttu-id="3a2e3-111">Bonjour **recherche** , tapez **application de la fonction**, puis appuyez sur ENTRÉE.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-111">In hello **Search** box, type **Function App**, and then press Enter.</span></span>

    ![Tapez « Fonction App » dans la zone de recherche hello](./media/storsimple-data-manager-change-default-blob-path/goto-function-app-resource.png)

4. <span data-ttu-id="3a2e3-113">Bonjour **résultats** , cliquez sur **fonction application**.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-113">In hello **Results** list, click **Function App**.</span></span>

    ![Sélectionnez la ressource application hello fonction dans la liste des résultats hello](./media/storsimple-data-manager-change-default-blob-path/select-function-app-resource.png)

    <span data-ttu-id="3a2e3-115">Hello **fonction application** fenêtre s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-115">hello **Function App** window opens.</span></span>

5. <span data-ttu-id="3a2e3-116">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-116">Click **Create**.</span></span>

    ![bouton « Créer » une fenêtre Hello application de fonction](./media/storsimple-data-manager-change-default-blob-path/create-new-function-app.png)

6. <span data-ttu-id="3a2e3-118">Sur hello **fonction application** Panneau de configuration, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="3a2e3-118">On hello **Function App** configuration blade, do hello following:</span></span>

    <span data-ttu-id="3a2e3-119">a.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-119">a.</span></span> <span data-ttu-id="3a2e3-120">Bonjour **nom de l’application** boîte, nom d’application de type hello.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-120">In hello **App name** box, type hello app name.</span></span>
    
    <span data-ttu-id="3a2e3-121">b.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-121">b.</span></span> <span data-ttu-id="3a2e3-122">Bonjour **abonnement** zone, entrez un nom hello d’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-122">In hello **Subscription** box, type hello name of hello subscription.</span></span>

    <span data-ttu-id="3a2e3-123">c.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-123">c.</span></span> <span data-ttu-id="3a2e3-124">Sous **groupe de ressources**, cliquez sur **nouvel**et puis hello nom du type de groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-124">Under **Resource Group**, click **Create new**, and then type hello name of hello resource group.</span></span>

    <span data-ttu-id="3a2e3-125">d.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-125">d.</span></span> <span data-ttu-id="3a2e3-126">Bonjour **Plan d’hébergement** , tapez **consommation Plan**.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-126">In hello **Hosting Plan** box, type **Consumption Plan**.</span></span>

    <span data-ttu-id="3a2e3-127">e.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-127">e.</span></span> <span data-ttu-id="3a2e3-128">Bonjour **emplacement** boîte de type hello emplacement.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-128">In hello **Location** box, type hello location.</span></span>

    <span data-ttu-id="3a2e3-129">f.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-129">f.</span></span> <span data-ttu-id="3a2e3-130">Sous **Compte de stockage**, sélectionnez un compte de stockage existant ou créez un nouveau compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-130">Under **Storage account**, select an existing storage account or create a new storage account.</span></span> <span data-ttu-id="3a2e3-131">Un compte de stockage est utilisé en interne pour la fonction hello.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-131">A storage account is used internally for hello function.</span></span>

    ![Entrer les données de configuration de la nouvelle application Function App](./media/storsimple-data-manager-change-default-blob-path/enter-new-funcion-app-data.png)

7. <span data-ttu-id="3a2e3-133">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-133">Click **Create**.</span></span>  
    <span data-ttu-id="3a2e3-134">application de fonction Hello est créée.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-134">hello function app is created.</span></span>

8. <span data-ttu-id="3a2e3-135">Dans le volet gauche de hello, cliquez sur **davantage de services**et puis hello suivant :</span><span class="sxs-lookup"><span data-stu-id="3a2e3-135">In hello left pane, click **More services**, and then do hello following:</span></span>
    
    <span data-ttu-id="3a2e3-136">a.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-136">a.</span></span> <span data-ttu-id="3a2e3-137">Bonjour **filtre** , tapez **des services d’application**.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-137">In hello **Filter** box, type **App services**.</span></span>
    
    <span data-ttu-id="3a2e3-138">b.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-138">b.</span></span> <span data-ttu-id="3a2e3-139">Cliquez sur **App Services**.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-139">Click **App Services**.</span></span> 

    ![Lien « Plus services » dans le volet gauche de hello](./media/storsimple-data-manager-change-default-blob-path/more-services.png)

9. <span data-ttu-id="3a2e3-141">Dans la liste de hello des services d’application, cliquez sur nom hello hello fonction app.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-141">In hello list of app services, click hello name of hello function app.</span></span>  
    <span data-ttu-id="3a2e3-142">Ouvre la page de l’application Hello (fonction).</span><span class="sxs-lookup"><span data-stu-id="3a2e3-142">hello function app page opens.</span></span>

10. <span data-ttu-id="3a2e3-143">Dans le volet gauche de hello, cliquez sur **nouvelle fonction**et puis hello suivant :</span><span class="sxs-lookup"><span data-stu-id="3a2e3-143">In hello left pane, click **New Function**, and then do hello following:</span></span> 

    <span data-ttu-id="3a2e3-144">a.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-144">a.</span></span> <span data-ttu-id="3a2e3-145">Bonjour **langage** liste, sélectionnez **c#**.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-145">In hello **Language** list, select **C#**.</span></span>
    
    <span data-ttu-id="3a2e3-146">b.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-146">b.</span></span> <span data-ttu-id="3a2e3-147">Dans le tableau de hello des vignettes de modèle, sélectionnez **QueueTrigger-CSharp**.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-147">In hello array of template tiles, select **QueueTrigger-CSharp**.</span></span>

    <span data-ttu-id="3a2e3-148">c.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-148">c.</span></span> <span data-ttu-id="3a2e3-149">Bonjour **nom de votre fonction** , tapez un nom pour la fonction.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-149">In hello **Name your function** box, type a name for your function.</span></span>

    <span data-ttu-id="3a2e3-150">d.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-150">d.</span></span> <span data-ttu-id="3a2e3-151">Bonjour **nom de la file d’attente** , tapez votre nom de définition de tâche de transformation de données.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-151">In hello **Queue name** box, type your data-transformation job definition name.</span></span>

    <span data-ttu-id="3a2e3-152">e.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-152">e.</span></span> <span data-ttu-id="3a2e3-153">Sous **connexion au compte de stockage**, cliquez sur **nouveau**, puis sélectionnez le compte hello qui correspond la tâche de transformation de données toohello.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-153">Under **Storage account connection**, click **new**, and then select hello account that corresponds toohello data-transformation job.</span></span>  
        <span data-ttu-id="3a2e3-154">Prenez note du nom de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-154">Make a note of hello connection name.</span></span> <span data-ttu-id="3a2e3-155">nom de Hello est requis plus loin dans hello fonction Azure.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-155">hello name is required later in hello Azure function.</span></span>

       ![Créer une fonction C#](./media/storsimple-data-manager-change-default-blob-path/create-new-csharp-function.png)

    <span data-ttu-id="3a2e3-157">f.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-157">f.</span></span> <span data-ttu-id="3a2e3-158">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-158">Click **Create**.</span></span>  
    <span data-ttu-id="3a2e3-159">Hello **fonction** fenêtre s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-159">hello **Function** window opens.</span></span>

11. <span data-ttu-id="3a2e3-160">Bonjour **fonction** fenêtre, exécutez _.csx_ de fichiers, puis hello suivant :</span><span class="sxs-lookup"><span data-stu-id="3a2e3-160">In hello **Function** window, run _.csx_ file, and then do hello following:</span></span>

    <span data-ttu-id="3a2e3-161">a.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-161">a.</span></span> <span data-ttu-id="3a2e3-162">Collez hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="3a2e3-162">Paste hello following code:</span></span>

    ```
    using System;
    using System.Configuration;
    using Microsoft.WindowsAzure.Storage.Blob;
    using Microsoft.WindowsAzure.Storage.Queue;
    using Microsoft.WindowsAzure.Storage;
    using System.Collections.Generic;
    using System.Linq;

    public static void Run(QueueItem myQueueItem, TraceWriter log)
    {
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConfigurationManager.AppSettings["STORAGE_CONNECTIONNAME"]);

        string storageAccUriEndswith = "windows.net/";
        string uri = myQueueItem.TargetLocation.Replace("%20", " ");
        log.Info($"Blob Uri: {uri}");

        // Remove storage account uri string
        uri = uri.Substring(uri.IndexOf(storageAccUriEndswith) + storageAccUriEndswith.Length);

        string containerName = uri.Substring(0, uri.IndexOf("/")); 

        // Remove container name string
        uri = uri.Substring(containerName.Length + 1);

        // Current blob path
        string blobName = uri; 

        string volumeName = uri.Substring(containerName.Length + 1);
        volumeName = uri.Substring(0, uri.IndexOf("/"));

        // Remove volume name string
        uri = uri.Substring(volumeName.Length + 1);

        string newContainerName = uri.Substring(0, uri.IndexOf("/")).ToLower();
        string newBlobName = uri.Substring(newContainerName.Length + 1);

        log.Info($"Container name: {containerName}");
        log.Info($"Volume name: {volumeName}");
        log.Info($"New container name: {newContainerName}");

        log.Info($"Blob name: {blobName}");
        log.Info($"New blob name: {newBlobName}");

        // Create hello blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

        // Container reference
        CloudBlobContainer container = blobClient.GetContainerReference(containerName);
        CloudBlobContainer newContainer = blobClient.GetContainerReference(newContainerName);
        newContainer.CreateIfNotExists();

        if(!container.Exists())
        {
            log.Info($"Container - {containerName} not exists");
            return;
        }

        if(!newContainer.Exists())
        {
            log.Info($"Container - {newContainerName} not exists");
            return;
        }

        CloudBlockBlob blob = container.GetBlockBlobReference(blobName);
        if (!blob.Exists())
        {
            // Skip toocopy hello blob toonew container, if source blob doesn't exist
            log.Info($"hello specified blob does not exist.");
            log.Info($"Blob Uri: {blob.Uri}");
            return;
        }

        CloudBlockBlob blobCopy = newContainer.GetBlockBlobReference(newBlobName);
        if (!blobCopy.Exists())
        {
            blobCopy.StartCopy(blob);
            // Delete old blob, after copy toonew container
            blob.DeleteIfExists();
            log.Info($"Blob file path renamed completed successfully");
        }
        else
        {
            log.Info($"Blob file path renamed already done");
            // Delete old blob, if already exists.
            blob.DeleteIfExists();
        }
    }

    public class QueueItem
    {
        public string SourceLocation {get;set;}
        public long SizeInBytes {get;set;}
        public string Status {get;set;}
        public string JobID {get;set;}
        public string TargetLocation {get; set;}
    }

    ```

    <span data-ttu-id="3a2e3-163">b.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-163">b.</span></span> <span data-ttu-id="3a2e3-164">Remplacez la valeur **STORAGE_CONNECTIONNAME** de la ligne 11 par la connexion à votre compte de stockage (point de référence 8c).</span><span class="sxs-lookup"><span data-stu-id="3a2e3-164">Replace **STORAGE_CONNECTIONNAME** on line 11 with your storage account connection (refer point 8c).</span></span>

    <span data-ttu-id="3a2e3-165">c.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-165">c.</span></span> <span data-ttu-id="3a2e3-166">À hello gauche en haut, cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-166">At hello top left, click **Save**.</span></span>

    ![Enregistrer la fonction](./media/storsimple-data-manager-change-default-blob-path/save-function.png)

12. <span data-ttu-id="3a2e3-168">toocomplete hello (fonction), ajoutez un fichier de plus de manière hello suivante :</span><span class="sxs-lookup"><span data-stu-id="3a2e3-168">toocomplete hello function, add one more file by doing hello following:</span></span>

    <span data-ttu-id="3a2e3-169">a.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-169">a.</span></span> <span data-ttu-id="3a2e3-170">Cliquez sur **Afficher les fichiers**.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-170">Click **View files**.</span></span>

       ![lien de « Afficher les fichiers » Hello](./media/storsimple-data-manager-change-default-blob-path/view-files.png)

    <span data-ttu-id="3a2e3-172">b.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-172">b.</span></span> <span data-ttu-id="3a2e3-173">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-173">Click **Add**.</span></span>
    
    <span data-ttu-id="3a2e3-174">c.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-174">c.</span></span> <span data-ttu-id="3a2e3-175">Saisissez **project.json** et appuyez sur Entrée.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-175">Type **project.json**, and then press Enter.</span></span>
    
    <span data-ttu-id="3a2e3-176">d.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-176">d.</span></span> <span data-ttu-id="3a2e3-177">Bonjour **project.json** file, collez hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="3a2e3-177">In hello **project.json** file, paste hello following code:</span></span>

    ```
    {
    "frameworks": {
        "net46":{
        "dependencies": {
            "windowsazure.storage": "8.1.1"
        }
        }
    }
    }

    ```

    <span data-ttu-id="3a2e3-178">e.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-178">e.</span></span> <span data-ttu-id="3a2e3-179">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-179">Click **Save**.</span></span>

<span data-ttu-id="3a2e3-180">Vous avez créé une fonction Azure.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-180">You have created an Azure function.</span></span> <span data-ttu-id="3a2e3-181">Cette fonction est déclenchée chaque fois qu’un nouvel objet blob est généré par la tâche de transformation de données hello.</span><span class="sxs-lookup"><span data-stu-id="3a2e3-181">This function is triggered each time a new blob is generated by hello data-transformation job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3a2e3-182">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3a2e3-182">Next steps</span></span>

[<span data-ttu-id="3a2e3-183">Utilisez l’interface utilisateur de gestionnaire de données StorSimple tootransform vos données</span><span class="sxs-lookup"><span data-stu-id="3a2e3-183">Use StorSimple Data Manager UI tootransform your data</span></span>](storsimple-data-manager-ui.md)
