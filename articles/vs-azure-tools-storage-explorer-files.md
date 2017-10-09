---
title: "aaaUsing Explorateur de stockage (version préliminaire) avec le stockage de fichiers Azure | Documents Microsoft"
description: "Découvrez comment savoir comment toowork de l’Explorateur de stockage (version préliminaire) toouse avec fichier de partage et de fichiers."
services: storage
documentationcenter: na
author: cawaMS
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/09/2017
ms.author: cawa
ms.openlocfilehash: 98eb3cde711ae3dbfdb6ffaec23ae24f822370e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-storage-explorer-preview-with-azure-file-storage"></a>Utilisation de l’Explorateur de stockage (version préliminaire) avec Azure Stockage Fichier

Le stockage est un service qui offre le fichier partages dans hello cloud à l’aide de fichiers Azure hello protocole Server Message Block (SMB) standard. Les protocoles SMB 2.1 et SMB 3.0 sont pris en charge. Avec le stockage de fichiers Azure, vous pouvez migrer des applications héritées qui s’appuient sur tooAzure de partages de fichiers rapidement et sans réécritures coûteux. Vous pouvez utiliser les données de tooexpose de stockage de fichier publiquement toohello world ou les données d’application toostore en privé. Dans cet article, vous allez apprendre comment toowork de l’Explorateur de stockage (version préliminaire) toouse avec fichier de partage et de fichiers.

## <a name="prerequisites"></a>Composants requis

toocomplete hello étapes décrites dans cet article, vous allez hello éléments suivants sont nécessaires :

- [Télécharger et installer l’explorateur de stockage (version préliminaire)](http://www.storageexplorer.com/)

- [Connexion de compte de stockage Azure tooa ou service](https://docs.microsoft.com//azure/vs-azure-tools-storage-manage-with-storage-explorer#connect-to-a-storage-account-or-service)

## <a name="create-a-file-share"></a>Créer un partage de fichiers

Tous les fichiers doivent résider dans un partage de fichiers, c’est-à-dire un simple regroupement logique de fichiers. Un compte peut contenir un nombre illimité de partages de fichiers, et chaque partage de fichiers peut stocker un nombre illimité de fichiers.

Hello suit illustre comment toocreate un partage de fichiers dans l’Explorateur de stockage (version préliminaire).

1. Ouvrez l’Explorateur de stockage (version préliminaire).

2. Dans le volet gauche de hello, développez le compte de stockage hello dans lequel vous souhaitez toocreate hello partage de fichiers

3. Avec le bouton droit **des partages de fichiers**et - dans le menu contextuel de hello - sélectionnez **créer un partage de fichier**.

    ![Créer un partage de fichiers](media/vs-azure-tools-storage-explorer-files/image1.png)

4. Une zone de texte s’affichera sous hello **des partages de fichiers** dossier. Entrez le nom hello pour le partage de fichiers. Consultez hello [partager des règles d’affectation de noms](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container) section pour obtenir la liste de règles et les restrictions d’affectation de noms des partages de fichiers.

    ![Partage de hello d’affectation de noms](media/vs-azure-tools-storage-explorer-files/image2.png)

5. Appuyez sur **entrée** lorsque toocreate terminé hello partage de fichiers, ou **ÉCHAP** toocancel. Une fois que le partage de fichiers hello a été créé avec succès, il sera affiché sous hello **des partages de fichiers** dossier pour hello sélectionné compte de stockage.

    ![nouveau partage de Hello](media/vs-azure-tools-storage-explorer-files/image3.png)

## <a name="view-a-file-shares-contents"></a>Afficher le contenu d’un partage de fichiers

Les partages de fichiers contiennent des fichiers et des dossiers (qui peuvent également contenir des fichiers).

Hello étapes suivantes illustrent comment partage du contenu de hello tooview d’un fichier dans l’Explorateur de stockage (version préliminaire) : +

1. Ouvrez l’Explorateur de stockage (version préliminaire).

2. Dans le volet gauche de hello, développez le compte de stockage hello contenant le partage de fichiers hello tooview vous le souhaitez.

3. Développez du compte de stockage hello **des partages de fichiers**.

4. Partage de fichiers avec le bouton hello vous le souhaitez tooview et - dans le menu contextuel de hello - sélectionnez **ouvrir**. Vous pouvez également double-cliquer sur le partage de fichiers hello tooview vous le souhaitez.

    ![Ouvrir le partage](media/vs-azure-tools-storage-explorer-files/image4.png)

5. volet principal de Hello affiche les contenu du partage de fichiers hello.
    
    ![contenu du partage de Hello](media/vs-azure-tools-storage-explorer-files/image5.png)

## <a name="delete-a-file-share"></a>Supprimer un partage de fichiers

Vous pouvez facilement créer et supprimer des partages de fichiers selon vos besoins. (toosee comment toodelete des fichiers individuels, consultez section toohello [la gestion des fichiers dans un partage de fichiers](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)

Hello suit illustre comment toodelete un partage de fichiers dans l’Explorateur de stockage (version préliminaire) :

1. Ouvrez l’Explorateur de stockage (version préliminaire).

2. Dans le volet gauche de hello, développez le compte de stockage hello contenant le partage de fichiers hello tooview vous le souhaitez.

3. Développez du compte de stockage hello **des partages de fichiers**.

4. Partage de fichiers avec le bouton hello vous le souhaitez toodelete et - dans le menu contextuel de hello - sélectionnez **supprimer**. Vous pouvez également appuyer sur **supprimer** partage de fichier actuellement sélectionné toodelete hello.

    ![Supprimer](media/vs-azure-tools-storage-explorer-files/image6.png)

5. Sélectionnez **Oui** boîte de dialogue de confirmation toohello.
    
    ![Boîte de dialogue de confirmation](media/vs-azure-tools-storage-explorer-files/image7.png)

## <a name="copy-a-file-share"></a>Copier un partage de fichiers

Explorateur de stockage (version préliminaire) vous permet de toocopy un Presse-papiers toohello du partage de fichier, puis collez ce partage de fichiers dans un autre compte de stockage. (toosee comment toocopy des fichiers individuels, consultez section toohello [la gestion des fichiers dans un partage de fichiers](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)

Hello suit illustre comment partager des toocopy un fichier à partir d’un tooanother de compte de stockage.

1. Ouvrez l’Explorateur de stockage (version préliminaire).

2. Dans le volet gauche de hello, développez le compte de stockage hello contenant le partage de fichiers hello toocopy vous le souhaitez.

3. Développez du compte de stockage hello **des partages de fichiers**.

4. Partage de fichiers avec le bouton hello vous le souhaitez toocopy et - dans le menu contextuel de hello - sélectionnez **de partage de fichiers copie**.

    ![Copier le partage de fichiers](media/vs-azure-tools-storage-explorer-files/image8.png)

5. Cliquez sur le compte de stockage cible « hello souhaitée » dans lequel vous le souhaitez partage de fichiers toopaste hello et - dans le menu contextuel de hello - sélectionnez **coller un partage de fichiers**.

    ![Coller le partage de fichiers](media/vs-azure-tools-storage-explorer-files/image9.png)

## <a name="get-hello-sas-for-a-file-share"></a>Obtenir hello SAS pour un partage de fichiers

A [signature d’accès partagé (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) fournit tooresources accès délégué dans votre compte de stockage. Cela signifie que vous pouvez accorder à qu'un client limitée tooobjects autorisations dans votre compte de stockage pour une période de temps et avec un jeu d’autorisations, spécifié sans avoir tooshare vos clés d’accès de compte.

Hello étapes suivantes illustrent comment toocreate partager un SAS pour un fichier : +

1. Ouvrez l’Explorateur de stockage (version préliminaire).

2. Dans le volet gauche de hello, développez le compte de stockage hello contenant le partage de fichiers hello pour laquelle vous souhaitez tooget une SAP.

3. Développez du compte de stockage hello **des partages de fichiers**.

4. Avec le bouton droit de partage de fichier souhaité hello et - dans le menu contextuel de hello - sélectionnez **obtenir une Signature d’accès partagé**.

    ![Obtenir une signature d’accès partagé](media/vs-azure-tools-storage-explorer-files/image10.png)

5. Bonjour **Signature d’accès partagé** boîte de dialogue, spécifiez la stratégie de hello, les dates de début et d’expiration, fuseau horaire et souhaité pour la ressource de hello des niveaux d’accès.

    ![Boîte de dialogue SAP](media/vs-azure-tools-storage-explorer-files/image11.png)

6. Lorsque vous avez terminé de spécifier les options de SAS hello, sélectionnez **créer**.

7. Une seconde **Signature d’accès partagé** boîte de dialogue affichera alors que les listes hello partage de fichiers, ainsi que les URL hello et requête que vous pouvez utiliser tooaccess hello ressource de stockage. Sélectionnez **copie** suivant toohello URL toocopy toohello Presse-papiers vous le souhaitez.
    
    ![Deuxième boîte de dialogue SAP](media/vs-azure-tools-storage-explorer-files/image12.png)

8. Lorsque vous avez terminé, sélectionnez **Fermer**.

## <a name="manage-access-policies-for-a-file-share"></a>Gérer les stratégies d’accès d’un partage de fichiers

Hello étapes suivantes illustrent comment toomanage (ajouter et supprimer) pour un partage de fichiers, les stratégies d’accès : +. les stratégies d’accès Hello est utilisée pour créer des URL de SAP par le biais duquel les personnes peuvent utiliser tooaccess hello ressource du fichier de stockage pendant une période de temps définie.

1. Ouvrez l’Explorateur de stockage (version préliminaire).

2. Dans le volet gauche de hello, développez le compte de stockage hello contenant le partage de fichiers hello dont vous souhaitez toomanage les stratégies d’accès.

3. Développez du compte de stockage hello **des partages de fichiers**.

4. Sélectionnez le partage de fichier souhaité hello et - dans le menu contextuel de hello - sélectionnez **gérer les stratégies d’accès**.

    ![Gérer les stratégies d’accès - Menu contextuel](media/vs-azure-tools-storage-explorer-files/image13.png)

5. Hello **des stratégies d’accès** boîte de dialogue répertorie les stratégies d’accès déjà créés pour le partage de fichier sélectionné hello.
    
    ![Stratégies d’accès](media/vs-azure-tools-storage-explorer-files/image14.png)

6. Suivez ces étapes en fonction de la tâche de gestion de stratégie hello accès :
    
    - **Ajouter une nouvelle stratégie d’accès** : sélectionnez **Ajouter**. Une fois généré, hello **des stratégies d’accès** boîte de dialogue affiche hello nouvellement ajouté accéder à la stratégie (avec les paramètres par défaut).

    - **Modifier une stratégie d’accès** : apportez les modifications souhaitées, puis cliquez sur **Enregistrer**.

    - **Supprimer une stratégie d’accès** : sélectionnez **supprimer** suivant toohello accès stratégie tooremove.

7. Créer une nouvelle URL de SAP à l’aide de hello la stratégie d’accès vous avez créé précédemment :
    
    ![Obtenir une SAP](media/vs-azure-tools-storage-explorer-files/image15.png)
    
    ![Propriétés et nom de la SAP](media/vs-azure-tools-storage-explorer-files/image16.png)

## <a name="managing-files-in-a-file-share"></a>Gestion des fichiers dans un partage de fichiers

Une fois que vous avez créé un partage de fichiers, vous pouvez télécharger un partage de fichiers toothat fichier, télécharger un ordinateur local tooyour de fichier, ouvrir un fichier sur votre ordinateur local et bien plus encore.

Hello étapes suivantes illustrent comment partagent des toomanage hello fichiers (et les dossiers) dans un fichier.

1.  Ouvrez l’Explorateur de stockage (version préliminaire).

2.  Dans le volet gauche de hello, développez le compte de stockage hello contenant le partage de fichiers hello toomanage vous le souhaitez.

3.  Développez du compte de stockage hello **des partages de fichiers**.

4.  Double-cliquez sur le partage de fichiers hello tooview vous le souhaitez.

5.  volet principal de Hello affiche les contenu du partage de fichiers hello.

    ![contenu du partage de Hello](media/vs-azure-tools-storage-explorer-files/image17.png)

6.  volet principal de Hello affiche les contenu du partage de fichiers hello.

7.  Suivez ces étapes en fonction de la tâche hello que vous souhaitez tooperform :

    - **Télécharger le partage de fichiers tooa de fichiers**

        a.  Barre d’outils du volet hello principal, sélectionnez **télécharger**, puis **télécharger des fichiers** à partir du menu déroulant de hello.

        ![Charger des fichiers](media/vs-azure-tools-storage-explorer-files/image18.png)
        
        b. Bonjour **télécharger des fichiers** boîte de dialogue, les points de suspension hello select (**...** ) situé à droite de hello Hello **fichiers** hello tooselect fichier (s) vous souhaitez tooupload de zone de texte.

        ![Ajout de fichiers](media/vs-azure-tools-storage-explorer-files/image19.png)

        c. Sélectionnez **Télécharger**.

    - **Télécharger un partage de fichiers tooa dossier**
        
        a. Barre d’outils du volet hello principal, sélectionnez **télécharger**, puis **dossier de téléchargement** à partir du menu déroulant de hello.

        ![Télécharger un dossier - Menu](media/vs-azure-tools-storage-explorer-files/image20.png)

        b. Bonjour **dossier de téléchargement** boîte de dialogue, les points de suspension hello select (**...** ) situé à droite de hello Hello **dossier** dossier hello dont vous souhaitez tooupload le contenu de texte boîte tooselect.

        c. Si vous le souhaitez, spécifiez un dossier cible dans le hello contenu du dossier sélectionné sera téléchargé. Si le dossier cible de hello n’existe pas, il sera créé.

        d. Sélectionnez **Télécharger**.

    - **Télécharger un ordinateur local tooyour de fichier**
        
        a. Sélectionnez le fichier hello toodownload.
        
        b. Barre d’outils du volet hello principal, sélectionnez **télécharger**.
        
        c. Bonjour **spécifier où toosave hello téléchargé le fichier** boîte de dialogue, spécifiez hello emplacement fichier hello téléchargé et hello nom que vous souhaitez toogive il.

        d. Sélectionnez **Enregistrer**.

    - **Ouvrir un fichier sur votre ordinateur local**
        
        a.  Sélectionnez le fichier hello tooopen.
        
        b.  Barre d’outils du volet hello principal, sélectionnez **ouvrir**.
        
        c.  fichier de Hello est téléchargé et ouverts à l’aide d’application hello associée au type de fichier du fichier hello sous-jacent.

    - **Copier un Presse-papiers toohello de fichier**

        a. Sélectionnez le fichier hello toocopy.

        b. Barre d’outils du volet hello principal, sélectionnez **copie**.

        c. Dans le volet gauche de hello, accédez de partage de fichiers tooanother, puis double-cliquez dessus tooview dans le volet principal de hello.

        d. Barre d’outils du volet hello principal, sélectionnez **coller** toocreate une copie du fichier de hello.

    - **Supprimer un fichier**

        a. Sélectionnez le fichier hello toodelete.

        b. Barre d’outils du volet hello principal, sélectionnez **supprimer**.

        c. Sélectionnez **Oui** boîte de dialogue de confirmation toohello.

## <a name="next-steps"></a>Étapes suivantes

- Hello de vue [dernières notes de version de l’Explorateur de stockage (version préliminaire) et les vidéos](http://www.storageexplorer.com/).

- Découvrez comment trop[créer des applications à l’aide d’objets BLOB Windows Azure, les tables, les files d’attente et les fichiers](https://azure.microsoft.com/documentation/services/storage/).
