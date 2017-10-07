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
# <a name="change-a-blob-path-from-hello-default-path-private-preview"></a>Modifier un chemin d’accès de l’objet blob à partir du chemin d’accès par défaut de hello (aperçu privé)

Cet article décrit comment tooset d’Azure fonction toorename un chemin de fichier blob par défaut. 

## <a name="prerequisites"></a>Composants requis

Vérifiez que vous disposez d’une définition de travail qui a été configurée correctement dans une ressource de données hybride dans un groupe de ressources.

## <a name="create-an-azure-function"></a>Création d’une fonction Azure

toocreate une fonction d’Azure, procédez comme hello suivant :

1. Accédez toohello [portail Azure](http://portal.azure.com/).

2. Haut hello du volet gauche de hello, cliquez sur **nouveau**. 

3. Bonjour **recherche** , tapez **application de la fonction**, puis appuyez sur ENTRÉE.

    ![Tapez « Fonction App » dans la zone de recherche hello](./media/storsimple-data-manager-change-default-blob-path/goto-function-app-resource.png)

4. Bonjour **résultats** , cliquez sur **fonction application**.

    ![Sélectionnez la ressource application hello fonction dans la liste des résultats hello](./media/storsimple-data-manager-change-default-blob-path/select-function-app-resource.png)

    Hello **fonction application** fenêtre s’ouvre.

5. Cliquez sur **Créer**.

    ![bouton « Créer » une fenêtre Hello application de fonction](./media/storsimple-data-manager-change-default-blob-path/create-new-function-app.png)

6. Sur hello **fonction application** Panneau de configuration, procédez comme hello suivant :

    a. Bonjour **nom de l’application** boîte, nom d’application de type hello.
    
    b. Bonjour **abonnement** zone, entrez un nom hello d’abonnement de hello.

    c. Sous **groupe de ressources**, cliquez sur **nouvel**et puis hello nom du type de groupe de ressources hello.

    d. Bonjour **Plan d’hébergement** , tapez **consommation Plan**.

    e. Bonjour **emplacement** boîte de type hello emplacement.

    f. Sous **Compte de stockage**, sélectionnez un compte de stockage existant ou créez un nouveau compte de stockage. Un compte de stockage est utilisé en interne pour la fonction hello.

    ![Entrer les données de configuration de la nouvelle application Function App](./media/storsimple-data-manager-change-default-blob-path/enter-new-funcion-app-data.png)

7. Cliquez sur **Créer**.  
    application de fonction Hello est créée.

8. Dans le volet gauche de hello, cliquez sur **davantage de services**et puis hello suivant :
    
    a. Bonjour **filtre** , tapez **des services d’application**.
    
    b. Cliquez sur **App Services**. 

    ![Lien « Plus services » dans le volet gauche de hello](./media/storsimple-data-manager-change-default-blob-path/more-services.png)

9. Dans la liste de hello des services d’application, cliquez sur nom hello hello fonction app.  
    Ouvre la page de l’application Hello (fonction).

10. Dans le volet gauche de hello, cliquez sur **nouvelle fonction**et puis hello suivant : 

    a. Bonjour **langage** liste, sélectionnez **c#**.
    
    b. Dans le tableau de hello des vignettes de modèle, sélectionnez **QueueTrigger-CSharp**.

    c. Bonjour **nom de votre fonction** , tapez un nom pour la fonction.

    d. Bonjour **nom de la file d’attente** , tapez votre nom de définition de tâche de transformation de données.

    e. Sous **connexion au compte de stockage**, cliquez sur **nouveau**, puis sélectionnez le compte hello qui correspond la tâche de transformation de données toohello.  
        Prenez note du nom de connexion hello. nom de Hello est requis plus loin dans hello fonction Azure.

       ![Créer une fonction C#](./media/storsimple-data-manager-change-default-blob-path/create-new-csharp-function.png)

    f. Cliquez sur **Créer**.  
    Hello **fonction** fenêtre s’ouvre.

11. Bonjour **fonction** fenêtre, exécutez _.csx_ de fichiers, puis hello suivant :

    a. Collez hello suivant de code :

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

    b. Remplacez la valeur **STORAGE_CONNECTIONNAME** de la ligne 11 par la connexion à votre compte de stockage (point de référence 8c).

    c. À hello gauche en haut, cliquez sur **enregistrer**.

    ![Enregistrer la fonction](./media/storsimple-data-manager-change-default-blob-path/save-function.png)

12. toocomplete hello (fonction), ajoutez un fichier de plus de manière hello suivante :

    a. Cliquez sur **Afficher les fichiers**.

       ![lien de « Afficher les fichiers » Hello](./media/storsimple-data-manager-change-default-blob-path/view-files.png)

    b. Cliquez sur **Add**.
    
    c. Saisissez **project.json** et appuyez sur Entrée.
    
    d. Bonjour **project.json** file, collez hello suivant de code :

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

    e. Cliquez sur **Enregistrer**.

Vous avez créé une fonction Azure. Cette fonction est déclenchée chaque fois qu’un nouvel objet blob est généré par la tâche de transformation de données hello.

## <a name="next-steps"></a>Étapes suivantes

[Utilisez l’interface utilisateur de gestionnaire de données StorSimple tootransform vos données](storsimple-data-manager-ui.md)
