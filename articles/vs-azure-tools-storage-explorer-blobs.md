---
title: "aaaManage des ressources de stockage d’objets Blob Azure avec l’Explorateur de stockage (version préliminaire) | Documents Microsoft"
description: "Gérer les conteneurs d’objets blob et les blobs Azure avec l’Explorateur de stockage (version préliminaire)"
services: storage
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 2f09e545-ec94-4d89-b96c-14783cc9d7a9
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 503dd061b205875da127378ab48e8d465800fc09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-blob-storage-resources-with-storage-explorer-preview"></a>Gérer les ressources Azure Blob Storage avec l’Explorateur de stockage (version préliminaire)
## <a name="overview"></a>Vue d'ensemble
[Stockage d’objets Blob Azure](storage/blobs/storage-dotnet-how-to-use-blobs.md) est un service destiné à stocker de grandes quantités de données non structurées, telles que les données texte ou binaire, qui sont accessibles à partir de n’importe où dans le monde hello via HTTP ou HTTPS.
Vous pouvez utiliser les données de tooexpose de stockage Blob publiquement toohello world ou les données d’application toostore en privé. Dans cet article, vous allez apprendre comment toowork de l’Explorateur de stockage (version préliminaire) toouse avec des conteneurs d’objets blob et les objets BLOB.

## <a name="prerequisites"></a>Composants requis
toocomplete hello étapes décrites dans cet article, vous allez hello éléments suivants sont nécessaires :

* [Télécharger et installer l’explorateur de stockage (version préliminaire)](http://www.storageexplorer.com)
* [Connexion de compte de stockage Azure tooa ou service](vs-azure-tools-storage-manage-with-storage-explorer.md#connect-to-a-storage-account-or-service)

## <a name="create-a-blob-container"></a>Création d’un conteneur d’objets blob
Tous les objets blob doivent résider dans un conteneur d’objets blob, c’est-à-dire un simple regroupement logique d’objets blob. Un compte peut contenir un nombre illimité de conteneurs, et chaque conteneur peut stocker un nombre illimité d’objets blob.

Hello étapes suivantes illustrent comment toocreate un conteneur d’objets blob dans l’Explorateur de stockage (version préliminaire).

1. Ouvrez l’Explorateur de stockage (version préliminaire).
2. Dans le volet gauche de hello, développez le compte de stockage hello dans lequel vous souhaitez le conteneur d’objets blob toocreate hello.
3. Avec le bouton droit **conteneurs d’objets Blob**et - dans le menu contextuel de hello - sélectionnez **créer un conteneur d’objets Blob**.

   ![Création de conteneurs d’objets blob - Menu contextuel][0]
4. Une zone de texte s’affichera sous hello **conteneurs d’objets Blob** dossier. Entrez le nom hello pour votre conteneur d’objets blob. Consultez hello [les règles d’affectation de noms de conteneur](storage/blobs/storage-dotnet-how-to-use-blobs.md#create-a-container) section pour obtenir la liste des règles et des restrictions sur les conteneurs d’objets blob d’affectation de noms.

   ![Création de conteneurs d’objets blob - Zone de texte][1]
5. Appuyez sur **entrée** fois le conteneur d’objets blob toocreate hello, ou **ÉCHAP** toocancel. Une fois le conteneur d’objets blob hello a été créé avec succès, il sera affiché sous hello **conteneurs d’objets Blob** dossier pour hello sélectionné compte de stockage.

   ![Conteneur d’objets blob créé][2]

## <a name="view-a-blob-containers-contents"></a>Affichage du contenu d’un conteneur d’objets blob
Les conteneurs d’objets blob contiennent des objets blob et des dossiers (qui peuvent eux-mêmes contenir des objets blob).

Hello étapes suivantes illustrent comment contenu de hello tooview d’un conteneur d’objets blob dans l’Explorateur de stockage (version préliminaire) :

1. Ouvrez l’Explorateur de stockage (version préliminaire).
2. Dans le volet gauche de hello, développez le compte de stockage hello contenant le conteneur d’objets blob hello tooview vous le souhaitez.
3. Développez du compte de stockage hello **conteneurs d’objets Blob**.
4. Conteneur d’objets blob avec le bouton hello vous le souhaitez tooview et - dans le menu contextuel de hello - sélectionnez **ouvrir l’éditeur de conteneur Blob**.
   Vous pouvez également double-cliquer sur le conteneur d’objets blob hello tooview vous le souhaitez.

   ![Ouvrir l’éditeur de conteneurs d’objets blob - Menu contextuel][19]
5. volet principal de Hello affiche le contenu du conteneur d’objets blob hello.

   ![Éditeur de conteneurs d’objets blob][3]

## <a name="delete-a-blob-container"></a>Suppression d’un conteneur d’objets blob
Vous pouvez facilement créer et supprimer des conteneurs d’objets blob selon vos besoins (toosee comment toodelete individuels des objets BLOB, consultez section toohello [gestion des objets BLOB dans un conteneur d’objets blob](#managing-blobs-in-a-blob-container).)

Hello étapes suivantes illustrent comment toodelete un conteneur d’objets blob dans l’Explorateur de stockage (version préliminaire) :

1. Ouvrez l’Explorateur de stockage (version préliminaire).
2. Dans le volet gauche de hello, développez le compte de stockage hello contenant le conteneur d’objets blob hello tooview vous le souhaitez.
3. Développez du compte de stockage hello **conteneurs d’objets Blob**.
4. Conteneur d’objets blob avec le bouton hello vous le souhaitez toodelete et - dans le menu contextuel de hello - sélectionnez **supprimer**.
   Vous pouvez également appuyer sur **supprimer** conteneur de toodelete hello blob actuellement sélectionné.

   ![Supprimer un conteneur d’objets blob - Menu contextuel][4]
5. Sélectionnez **Oui** boîte de dialogue de confirmation toohello.

   ![Supprimer un conteneur d’objets blob - Confirmation][5]

## <a name="copy-a-blob-container"></a>Copie d’un conteneur d’objets blob
Explorateur de stockage (version préliminaire) vous permet de toocopy un Presse-papiers toohello du conteneur blob et collez ensuite que le conteneur d’objets blob dans un autre compte de stockage. (toosee comment toocopy individuels des objets BLOB, consultez section toohello [gestion des objets BLOB dans un conteneur d’objets blob](#managing-blobs-in-a-blob-container).)

Hello suit illustre comment toocopy un conteneur d’objets blob à partir du stockage d’un compte tooanother.

1. Ouvrez l’Explorateur de stockage (version préliminaire).
2. Dans le volet gauche de hello, développez le compte de stockage hello contenant le conteneur d’objets blob hello toocopy vous le souhaitez.
3. Développez du compte de stockage hello **conteneurs d’objets Blob**.
4. Conteneur d’objets blob avec le bouton hello vous le souhaitez toocopy et - dans le menu contextuel de hello - sélectionnez **conteneur d’objets Blob copie**.

   ![Copier un conteneur d’objets blob - Menu contextuel][6]
5. Cliquez sur le compte de stockage cible « hello souhaitée » dans lequel vous le souhaitez conteneur d’objets blob toopaste hello et - dans le menu contextuel de hello - sélectionnez **conteneur d’objets Blob coller**.

   ![Coller un conteneur d’objets blob - Menu contextuel][7]

## <a name="get-hello-sas-for-a-blob-container"></a>Obtenir hello SAS pour un conteneur d’objets blob
A [signature d’accès partagé (SAS)](storage/common/storage-dotnet-shared-access-signature-part-1.md) fournit tooresources accès délégué dans votre compte de stockage.
Cela signifie que vous pouvez accorder à qu'un client limitée tooobjects autorisations dans votre compte de stockage pour une période de temps et avec un jeu spécifié d’autorisations, sans avoir à partager vos clés d’accès de compte.

Hello étapes suivantes illustrent comment toocreate un SAS pour un conteneur d’objets blob :

1. Ouvrez l’Explorateur de stockage (version préliminaire).
2. Dans le volet gauche de hello, développez le compte de stockage hello contenant le conteneur d’objets blob hello pour laquelle vous souhaitez tooget une SAP.
3. Développez du compte de stockage hello **conteneurs d’objets Blob**.
4. Cliquez sur le conteneur d’objets blob souhaité hello et - dans le menu contextuel de hello - sélectionnez **obtenir une Signature d’accès partagé**.

   ![Obtenir une signature d’accès partagé - Menu contextuel][8]
5. Bonjour **Signature d’accès partagé** boîte de dialogue, spécifiez la stratégie de hello, les dates de début et d’expiration, fuseau horaire et souhaité pour la ressource de hello des niveaux d’accès.

   ![Obtenir une signature d’accès partagé - Options][9]
6. Lorsque vous avez terminé de spécifier les options de SAS hello, sélectionnez **créer**.
7. Une seconde **Signature d’accès partagé** boîte de dialogue affichera alors que les listes hello conteneur d’objets blob, ainsi que les URL hello et requête que vous pouvez utiliser tooaccess hello ressource de stockage.
   Sélectionnez **copie** suivant toohello URL toocopy toohello Presse-papiers vous le souhaitez.

   ![Copier les URL de SAP][10]
8. Lorsque vous avez terminé, sélectionnez **Fermer**.

## <a name="manage-access-policies-for-a-blob-container"></a>Gestion des stratégies d’accès d’un conteneur d’objets blob
Hello étapes suivantes illustrent comment toomanage (ajouter et supprimer) pour un conteneur d’objets blob, les stratégies d’accès :

1. Ouvrez l’Explorateur de stockage (version préliminaire).
2. Dans le volet gauche de hello, développez le compte de stockage hello contenant le conteneur d’objets blob hello dont vous souhaitez toomanage les stratégies d’accès.
3. Développez du compte de stockage hello **conteneurs d’objets Blob**.
4. Sélectionnez le conteneur d’objets blob souhaité hello et - dans le menu contextuel de hello - sélectionnez **gérer les stratégies d’accès**.

   ![Gérer les stratégies d’accès - Menu contextuel][11]
5. Hello **des stratégies d’accès** boîte de dialogue répertorie les stratégies d’accès déjà créés pour le conteneur d’objet blob sélectionnés hello.

   ![Options de stratégie d’accès][12]        
6. Suivez ces étapes en fonction de la tâche de gestion de stratégie hello accès :

   * **Ajouter une nouvelle stratégie d’accès** : sélectionnez **Ajouter**. Une fois généré, hello **des stratégies d’accès** boîte de dialogue affiche hello nouvellement ajouté accéder à la stratégie (avec les paramètres par défaut).
   * **Modifier une stratégie d’accès** : apportez les modifications souhaitées, puis cliquez sur **Enregistrer**.
   * **Supprimer une stratégie d’accès** : sélectionnez **supprimer** suivant toohello accès stratégie tooremove.

## <a name="set-hello-public-access-level-for-a-blob-container"></a>Ensemble hello niveau d’accès Public pour un conteneur d’objets blob
Par défaut, chaque conteneur d’objets blob est défini trop « Aucun accès public ».

Hello étapes suivantes illustrent comment toospecify accès public au niveau d’un conteneur d’objets blob.

1. Ouvrez l’Explorateur de stockage (version préliminaire).
2. Dans le volet gauche de hello, développez le compte de stockage hello contenant le conteneur d’objets blob hello dont vous souhaitez toomanage les stratégies d’accès.
3. Développez du compte de stockage hello **conteneurs d’objets Blob**.
4. Sélectionnez le conteneur d’objets blob souhaité hello et - dans le menu contextuel de hello - sélectionnez **définie au niveau de l’accès Public**.

   ![Définir le niveau d’accès public - Menu contextuel][13]
5. Bonjour **définir le niveau de l’accès Public du conteneur** boîte de dialogue, spécifiez le niveau d’accès hello souhaité.

   ![Définir le niveau d’accès public - Options][14]
6. Sélectionnez **Appliquer**.

## <a name="managing-blobs-in-a-blob-container"></a>Gestion des objets blob dans un conteneur d’objets blob
Une fois que vous avez créé un conteneur d’objets blob, vous pouvez télécharger un conteneur d’objets blob toothat blob, télécharger un ordinateur local de blob tooyour, ouvrir un objet blob sur votre ordinateur local et bien plus encore.

Hello suit illustre comment toomanage hello des objets BLOB (et les dossiers) dans un conteneur d’objets blob.

1. Ouvrez l’Explorateur de stockage (version préliminaire).
2. Dans le volet gauche de hello, développez le compte de stockage hello contenant le conteneur d’objets blob hello toomanage vous le souhaitez.
3. Développez du compte de stockage hello **conteneurs d’objets Blob**.
4. Double-cliquez sur le conteneur d’objets blob hello tooview vous le souhaitez.
5. volet principal de Hello affiche le contenu du conteneur d’objets blob hello.

   ![Afficher le conteneur d’objets blob][3]
6. volet principal de Hello affiche le contenu du conteneur d’objets blob hello.
7. Suivez ces étapes en fonction de la tâche hello que vous souhaitez tooperform :

   * **Télécharger le conteneur d’objets blob tooa fichiers**

     1. Barre d’outils du volet hello principal, sélectionnez **télécharger**, puis **télécharger des fichiers** à partir du menu déroulant de hello.

        ![Télécharger des fichiers - Menu][15]
     2. Bonjour **télécharger des fichiers** boîte de dialogue, les points de suspension hello select (**...** ) situé à droite de hello Hello **fichiers** hello tooselect fichier (s) vous souhaitez tooupload de zone de texte.

        ![Télécharger des fichiers - Options][16]
     3. Spécifiez le type hello de **type d’objets Blob**. article de Hello [prise en main le stockage Blob Azure à l’aide de .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explique les différences de hello hello entre les différents types d’objet blob.
     4. Si vous le souhaitez, spécifiez un dossier cible dans lequel les fichiers sélectionnés hello seront téléchargés. Si le dossier cible de hello n’existe pas, il sera créé.
     5. Sélectionnez **Télécharger**.
   * **Télécharger un conteneur d’objets blob tooa dossier**

     1. Barre d’outils du volet hello principal, sélectionnez **télécharger**, puis **dossier de téléchargement** à partir du menu déroulant de hello.

        ![Télécharger un dossier - Menu][17]
     2. Bonjour **dossier de téléchargement** boîte de dialogue, les points de suspension hello select (**...** ) situé à droite de hello Hello **dossier** dossier hello dont vous souhaitez tooupload le contenu de texte boîte tooselect.

        ![Télécharger un dossier - Options][18]
     3. Spécifiez le type hello de **type d’objets Blob**. article de Hello [prise en main le stockage Blob Azure à l’aide de .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explique les différences de hello hello entre les différents types d’objet blob.
     4. Si vous le souhaitez, spécifiez un dossier cible dans le hello contenu du dossier sélectionné sera téléchargé. Si le dossier cible de hello n’existe pas, il sera créé.
     5. Sélectionnez **Télécharger**.
   * **Télécharger un ordinateur local de blob tooyour**

     1. Sélectionnez blob hello toodownload vous le souhaitez.
     2. Barre d’outils du volet hello principal, sélectionnez **télécharger**.
     3. Bonjour **spécifier où toosave hello téléchargé blob** boîte de dialogue, spécifiez hello emplacement blob hello téléchargé et hello nom que vous souhaitez toogive il.  
     4. Sélectionnez **Enregistrer**.
   * **Ouvrir un objet blob sur votre ordinateur local**

     1. Sélectionnez blob hello tooopen vous le souhaitez.
     2. Barre d’outils du volet hello principal, sélectionnez **ouvrir**.
     3. objet blob de Hello sera téléchargé et ouvert à l’aide d’application hello associée au type de fichier sous-jacent de l’objet blob de hello.
   * **Copier un Presse-papiers toohello de blob**

     1. Sélectionnez blob hello toocopy vous le souhaitez.
     2. Barre d’outils du volet hello principal, sélectionnez **copie**.
     3. Dans le volet gauche de hello, accédez tooanother conteneur d’objets blob, puis double-cliquez dessus tooview dans le volet principal de hello.
     4. Barre d’outils du volet hello principal, sélectionnez **coller** toocreate une copie de l’objet blob de hello.
   * **Supprimer un blob.**

     1. Sélectionnez blob hello toodelete vous le souhaitez.
     2. Barre d’outils du volet hello principal, sélectionnez **supprimer**.
     3. Sélectionnez **Oui** boîte de dialogue de confirmation toohello.

## <a name="next-steps"></a>Étapes suivantes
* Hello de vue [dernières notes de version de l’Explorateur de stockage (version préliminaire) et les vidéos](http://www.storageexplorer.com).
* Découvrez comment trop[créer des applications à l’aide d’objets BLOB Windows Azure, les tables, les files d’attente et les fichiers](https://azure.microsoft.com/documentation/services/storage/).

[0]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-create-context-menu.png
[1]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create.png
[2]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create-done.png
[3]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-editor.png
[4]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-context-menu.png
[5]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-confirmation.png
[6]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-copy-context-menu.png
[7]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-paste-context-menu.png
[8]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-context-menu.png
[9]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-options.png
[10]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-urls.png
[11]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-context-menu.png
[12]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-options.png
[13]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-context-menu.png
[14]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-options.png
[15]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-menu.png
[16]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-options.png
[17]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-menu.png
[18]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-options.png
[19]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-open-editor-context-menu.png
