---
title: "Modifier le chemin d’accès d’objet blob par défaut | Microsoft Docs"
description: "Découvrez comment configurer une fonction Azure pour renommer un chemin d’accès de fichier d’objet blob (version préliminaire privée)"
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
ms.openlocfilehash: 057d4d7370207859617eb63238bf425bfa6d3e16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="change-a-blob-path-from-the-default-path-private-preview"></a><span data-ttu-id="74fb9-103">Modifier le chemin d’accès d’objet blob par défaut (version préliminaire privée)</span><span class="sxs-lookup"><span data-stu-id="74fb9-103">Change a blob path from the default path (private preview)</span></span>

<span data-ttu-id="74fb9-104">Cet article décrit comment configurer une fonction Azure pour renommer un chemin d’accès de fichier d’objet blob par défaut.</span><span class="sxs-lookup"><span data-stu-id="74fb9-104">This article describes how to set up an Azure function to rename a default blob file path.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="74fb9-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="74fb9-105">Prerequisites</span></span>

<span data-ttu-id="74fb9-106">Vérifiez que vous disposez d’une définition de travail qui a été configurée correctement dans une ressource de données hybride dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="74fb9-106">Ensure that you have a job definition that has been correctly configured in a hybrid data resource within a resource group.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="74fb9-107">Création d’une fonction Azure</span><span class="sxs-lookup"><span data-stu-id="74fb9-107">Create an Azure function</span></span>

<span data-ttu-id="74fb9-108">Pour créer une fonction Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="74fb9-108">To create an Azure function, do the following:</span></span>

1. <span data-ttu-id="74fb9-109">Accédez au [portail Azure](http://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="74fb9-109">Go to the [Azure portal](http://portal.azure.com/).</span></span>

2. <span data-ttu-id="74fb9-110">En haut du panneau gauche, cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="74fb9-110">At the top of the left pane, click **New**.</span></span> 

3. <span data-ttu-id="74fb9-111">Dans la zone de **recherche**, saisissez **Function App**, puis appuyez sur Entrée.</span><span class="sxs-lookup"><span data-stu-id="74fb9-111">In the **Search** box, type **Function App**, and then press Enter.</span></span>

    ![Saisissez « Function App » dans la zone de recherche](./media/storsimple-data-manager-change-default-blob-path/goto-function-app-resource.png)

4. <span data-ttu-id="74fb9-113">Dans la liste **Résultats**, cliquez sur **Function App**.</span><span class="sxs-lookup"><span data-stu-id="74fb9-113">In the **Results** list, click **Function App**.</span></span>

    ![Sélectionnez la ressource Function App dans la liste des résultats](./media/storsimple-data-manager-change-default-blob-path/select-function-app-resource.png)

    <span data-ttu-id="74fb9-115">La fenêtre **Function App** s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="74fb9-115">The **Function App** window opens.</span></span>

5. <span data-ttu-id="74fb9-116">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="74fb9-116">Click **Create**.</span></span>

    ![Bouton « Créer » de la fenêtre Function App](./media/storsimple-data-manager-change-default-blob-path/create-new-function-app.png)

6. <span data-ttu-id="74fb9-118">Dans le panneau de configuration **Function App**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="74fb9-118">On the **Function App** configuration blade, do the following:</span></span>

    <span data-ttu-id="74fb9-119">a.</span><span class="sxs-lookup"><span data-stu-id="74fb9-119">a.</span></span> <span data-ttu-id="74fb9-120">Dans la zone **Nom de l’application**, saisissez le nom de l’application.</span><span class="sxs-lookup"><span data-stu-id="74fb9-120">In the **App name** box, type the app name.</span></span>
    
    <span data-ttu-id="74fb9-121">b.</span><span class="sxs-lookup"><span data-stu-id="74fb9-121">b.</span></span> <span data-ttu-id="74fb9-122">Dans la zone **Abonnement**, saisissez le nom de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="74fb9-122">In the **Subscription** box, type the name of the subscription.</span></span>

    <span data-ttu-id="74fb9-123">c.</span><span class="sxs-lookup"><span data-stu-id="74fb9-123">c.</span></span> <span data-ttu-id="74fb9-124">Sous **Groupe de ressources**, cliquez sur **Créer un nouveau** et saisissez le nom du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="74fb9-124">Under **Resource Group**, click **Create new**, and then type the name of the resource group.</span></span>

    <span data-ttu-id="74fb9-125">d.</span><span class="sxs-lookup"><span data-stu-id="74fb9-125">d.</span></span> <span data-ttu-id="74fb9-126">Dans la zone **Plan d’hébergement**, saisissez **Plan de consommation**.</span><span class="sxs-lookup"><span data-stu-id="74fb9-126">In the **Hosting Plan** box, type **Consumption Plan**.</span></span>

    <span data-ttu-id="74fb9-127">e.</span><span class="sxs-lookup"><span data-stu-id="74fb9-127">e.</span></span> <span data-ttu-id="74fb9-128">Dans la zone **Emplacement**, saisissez l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="74fb9-128">In the **Location** box, type the location.</span></span>

    <span data-ttu-id="74fb9-129">f.</span><span class="sxs-lookup"><span data-stu-id="74fb9-129">f.</span></span> <span data-ttu-id="74fb9-130">Sous **Compte de stockage**, sélectionnez un compte de stockage existant ou créez un nouveau compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="74fb9-130">Under **Storage account**, select an existing storage account or create a new storage account.</span></span> <span data-ttu-id="74fb9-131">Un compte de stockage est utilisé en interne pour la fonction.</span><span class="sxs-lookup"><span data-stu-id="74fb9-131">A storage account is used internally for the function.</span></span>

    ![Entrer les données de configuration de la nouvelle application Function App](./media/storsimple-data-manager-change-default-blob-path/enter-new-funcion-app-data.png)

7. <span data-ttu-id="74fb9-133">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="74fb9-133">Click **Create**.</span></span>  
    <span data-ttu-id="74fb9-134">L’application Function App est créée.</span><span class="sxs-lookup"><span data-stu-id="74fb9-134">The function app is created.</span></span>

8. <span data-ttu-id="74fb9-135">Dans le volet gauche, cliquez sur **Plus de services**, puis procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="74fb9-135">In the left pane, click **More services**, and then do the following:</span></span>
    
    <span data-ttu-id="74fb9-136">a.</span><span class="sxs-lookup"><span data-stu-id="74fb9-136">a.</span></span> <span data-ttu-id="74fb9-137">Dans la zone **Filtre**, saisissez **App Services**.</span><span class="sxs-lookup"><span data-stu-id="74fb9-137">In the **Filter** box, type **App services**.</span></span>
    
    <span data-ttu-id="74fb9-138">b.</span><span class="sxs-lookup"><span data-stu-id="74fb9-138">b.</span></span> <span data-ttu-id="74fb9-139">Cliquez sur **App Services**.</span><span class="sxs-lookup"><span data-stu-id="74fb9-139">Click **App Services**.</span></span> 

    ![Lien « Plus de services » dans le volet gauche](./media/storsimple-data-manager-change-default-blob-path/more-services.png)

9. <span data-ttu-id="74fb9-141">Dans la liste des services d’application, cliquez sur le nom de l’application Function App.</span><span class="sxs-lookup"><span data-stu-id="74fb9-141">In the list of app services, click the name of the function app.</span></span>  
    <span data-ttu-id="74fb9-142">La page de l’application Function App s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="74fb9-142">The function app page opens.</span></span>

10. <span data-ttu-id="74fb9-143">Dans le volet gauche, cliquez sur **Nouvelle fonction**, puis procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="74fb9-143">In the left pane, click **New Function**, and then do the following:</span></span> 

    <span data-ttu-id="74fb9-144">a.</span><span class="sxs-lookup"><span data-stu-id="74fb9-144">a.</span></span> <span data-ttu-id="74fb9-145">Dans la liste **Langage**, sélectionnez **C#**.</span><span class="sxs-lookup"><span data-stu-id="74fb9-145">In the **Language** list, select **C#**.</span></span>
    
    <span data-ttu-id="74fb9-146">b.</span><span class="sxs-lookup"><span data-stu-id="74fb9-146">b.</span></span> <span data-ttu-id="74fb9-147">Dans le tableau de vignettes de modèle, sélectionnez **QueueTrigger-CSharp**.</span><span class="sxs-lookup"><span data-stu-id="74fb9-147">In the array of template tiles, select **QueueTrigger-CSharp**.</span></span>

    <span data-ttu-id="74fb9-148">c.</span><span class="sxs-lookup"><span data-stu-id="74fb9-148">c.</span></span> <span data-ttu-id="74fb9-149">Dans la zone **Nommez votre fonction**, saisissez un nom pour la fonction.</span><span class="sxs-lookup"><span data-stu-id="74fb9-149">In the **Name your function** box, type a name for your function.</span></span>

    <span data-ttu-id="74fb9-150">d.</span><span class="sxs-lookup"><span data-stu-id="74fb9-150">d.</span></span> <span data-ttu-id="74fb9-151">Dans la zone **Nom de file d’attente**, saisissez le nom de la définition du travail de transformation des données.</span><span class="sxs-lookup"><span data-stu-id="74fb9-151">In the **Queue name** box, type your data-transformation job definition name.</span></span>

    <span data-ttu-id="74fb9-152">e.</span><span class="sxs-lookup"><span data-stu-id="74fb9-152">e.</span></span> <span data-ttu-id="74fb9-153">Sous **Connexion au compte de stockage**, cliquez sur **nouveau**, puis sélectionnez le compte correspondant au travail de transformation des données.</span><span class="sxs-lookup"><span data-stu-id="74fb9-153">Under **Storage account connection**, click **new**, and then select the account that corresponds to the data-transformation job.</span></span>  
        <span data-ttu-id="74fb9-154">Notez le nom de la connexion.</span><span class="sxs-lookup"><span data-stu-id="74fb9-154">Make a note of the connection name.</span></span> <span data-ttu-id="74fb9-155">Ce nom est requis plus loin dans la fonction Azure.</span><span class="sxs-lookup"><span data-stu-id="74fb9-155">The name is required later in the Azure function.</span></span>

       ![Créer une fonction C#](./media/storsimple-data-manager-change-default-blob-path/create-new-csharp-function.png)

    <span data-ttu-id="74fb9-157">f.</span><span class="sxs-lookup"><span data-stu-id="74fb9-157">f.</span></span> <span data-ttu-id="74fb9-158">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="74fb9-158">Click **Create**.</span></span>  
    <span data-ttu-id="74fb9-159">La fenêtre **Function** s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="74fb9-159">The **Function** window opens.</span></span>

11. <span data-ttu-id="74fb9-160">Dans la fenêtre **Function**, exécutez le fichier _.csx_, puis procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="74fb9-160">In the **Function** window, run _.csx_ file, and then do the following:</span></span>

    <span data-ttu-id="74fb9-161">a.</span><span class="sxs-lookup"><span data-stu-id="74fb9-161">a.</span></span> <span data-ttu-id="74fb9-162">Collez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="74fb9-162">Paste the following code:</span></span>

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

        // Create the blob client.
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
            // Skip to copy the blob to new container, if source blob doesn't exist
            log.Info($"The specified blob does not exist.");
            log.Info($"Blob Uri: {blob.Uri}");
            return;
        }

        CloudBlockBlob blobCopy = newContainer.GetBlockBlobReference(newBlobName);
        if (!blobCopy.Exists())
        {
            blobCopy.StartCopy(blob);
            // Delete old blob, after copy to new container
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

    <span data-ttu-id="74fb9-163">b.</span><span class="sxs-lookup"><span data-stu-id="74fb9-163">b.</span></span> <span data-ttu-id="74fb9-164">Remplacez la valeur **STORAGE_CONNECTIONNAME** de la ligne 11 par la connexion à votre compte de stockage (point de référence 8c).</span><span class="sxs-lookup"><span data-stu-id="74fb9-164">Replace **STORAGE_CONNECTIONNAME** on line 11 with your storage account connection (refer point 8c).</span></span>

    <span data-ttu-id="74fb9-165">c.</span><span class="sxs-lookup"><span data-stu-id="74fb9-165">c.</span></span> <span data-ttu-id="74fb9-166">Cliquez sur **Enregistrer** en haut à gauche.</span><span class="sxs-lookup"><span data-stu-id="74fb9-166">At the top left, click **Save**.</span></span>

    ![Enregistrer la fonction](./media/storsimple-data-manager-change-default-blob-path/save-function.png)

12. <span data-ttu-id="74fb9-168">Pour terminer la fonction, ajoutez un fichier de plus en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="74fb9-168">To complete the function, add one more file by doing the following:</span></span>

    <span data-ttu-id="74fb9-169">a.</span><span class="sxs-lookup"><span data-stu-id="74fb9-169">a.</span></span> <span data-ttu-id="74fb9-170">Cliquez sur **Afficher les fichiers**.</span><span class="sxs-lookup"><span data-stu-id="74fb9-170">Click **View files**.</span></span>

       ![Lien « Afficher les fichiers »](./media/storsimple-data-manager-change-default-blob-path/view-files.png)

    <span data-ttu-id="74fb9-172">b.</span><span class="sxs-lookup"><span data-stu-id="74fb9-172">b.</span></span> <span data-ttu-id="74fb9-173">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="74fb9-173">Click **Add**.</span></span>
    
    <span data-ttu-id="74fb9-174">c.</span><span class="sxs-lookup"><span data-stu-id="74fb9-174">c.</span></span> <span data-ttu-id="74fb9-175">Saisissez **project.json** et appuyez sur Entrée.</span><span class="sxs-lookup"><span data-stu-id="74fb9-175">Type **project.json**, and then press Enter.</span></span>
    
    <span data-ttu-id="74fb9-176">d.</span><span class="sxs-lookup"><span data-stu-id="74fb9-176">d.</span></span> <span data-ttu-id="74fb9-177">Collez le code suivant dans le fichier **project.json** :</span><span class="sxs-lookup"><span data-stu-id="74fb9-177">In the **project.json** file, paste the following code:</span></span>

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

    <span data-ttu-id="74fb9-178">e.</span><span class="sxs-lookup"><span data-stu-id="74fb9-178">e.</span></span> <span data-ttu-id="74fb9-179">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="74fb9-179">Click **Save**.</span></span>

<span data-ttu-id="74fb9-180">Vous avez créé une fonction Azure.</span><span class="sxs-lookup"><span data-stu-id="74fb9-180">You have created an Azure function.</span></span> <span data-ttu-id="74fb9-181">Cette fonction est déclenchée à chaque fois qu’un nouvel objet blob est généré par le travail de transformation des données.</span><span class="sxs-lookup"><span data-stu-id="74fb9-181">This function is triggered each time a new blob is generated by the data-transformation job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="74fb9-182">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="74fb9-182">Next steps</span></span>

[<span data-ttu-id="74fb9-183">Utilisez l’interface utilisateur de StorSimple Data Manager pour transformer vos données</span><span class="sxs-lookup"><span data-stu-id="74fb9-183">Use StorSimple Data Manager UI to transform your data</span></span>](storsimple-data-manager-ui.md)
