---
title: "une fonction dans Azure déclenchée par le stockage d’objets Blob d’aaaCreate | Documents Microsoft"
description: "Utilisez les fonctions Azure toocreate une fonction sans serveur qui est appelée par les éléments ajoutés tooAzure stockage d’objets Blob."
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: d6bff41c-a624-40c1-bbc7-80590df29ded
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: acb7d29abb07a22da11d0e65d2ed54591f8e3f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-azure-blob-storage"></a>Créer une fonction déclenchée par un stockage Blob Azure

Découvrez comment toocreate une fonction déclenchée lorsque les fichiers sont téléchargés tooor mis à jour dans le stockage Blob Azure.

![Afficher le message dans les journaux hello.](./media/functions-create-storage-blob-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>Composants requis

+ Téléchargez et installez hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).
+ Un abonnement Azure. Si vous n’en avez pas, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Création d’une application Azure Function

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Function App créée avec succès.](./media/functions-create-first-azure-function/function-app-create-success.png)

Ensuite, créez une fonction dans hello une nouvelle application de fonction.

<a name="create-function"></a>

## <a name="create-a-blob-storage-triggered-function"></a>Créer une fonction déclenchée par le stockage Blob

1. Développez votre application de la fonction et cliquez sur hello  **+**  bouton ensuite trop**fonctions**. S’il s’agit de hello première fonction dans votre application de la fonction, sélectionnez **fonction personnalisée**. Cela affiche le jeu complet de hello des modèles de fonction.

    ![Page de démarrage rapide de fonctions Bonjour portail Azure](./media/functions-create-storage-blob-triggered-function/add-first-function.png)

2. Sélectionnez hello **BlobTrigger** modèle pour votre langue de votre choix, puis utiliser les paramètres comme spécifié dans la table de hello hello.

    ![Créer la fonction de stockage déclenchée de Blob de hello.](./media/functions-create-storage-blob-triggered-function/functions-create-blob-storage-trigger-portal.png)

    | Paramètre | Valeur suggérée | Description |
    |---|---|---|
    | **Chemin d’accès**   | mycontainer/{name}    | Emplacement du stockage Blob analysé. nom du fichier d’objet blob de hello Hello est passé dans la liaison de hello en hello _nom_ paramètre.  |
    | **Connexion au compte de stockage** | AzureWebJobStorage | Vous pouvez utiliser la connexion au compte de stockage hello est déjà utilisée par votre application de la fonction, ou créez-en un.  |
    | **Nommer votre fonction** | Unique dans votre Function App | Nom de cette fonction déclenchée par l’objet Blob. |

3. Cliquez sur **créer** toocreate votre fonction.

Ensuite, vous vous connectez compte de stockage Azure tooyour et que vous créez hello **mycontainer** conteneur.

## <a name="create-hello-container"></a>Créer un conteneur de hello

1. Dans votre fonction, cliquez sur **Intégrer**, développez **Documentation** et copiez le **Nom du compte** et la **Clé du compte**. Vous utilisez ces informations d’identification tooconnect toohello stockage compte. Si vous êtes déjà connecté votre compte de stockage, passez toostep 4.

    ![Obtenir des informations d’identification de connexion de compte de stockage hello.](./media/functions-create-storage-blob-triggered-function/functions-storage-account-connection.png)

1. Exécutez hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) outil, cliquez sur hello icône à gauche de hello de connexion, choisissez **utiliser un nom de compte de stockage et de la clé**, puis cliquez sur **suivant**.

    ![Exécuter l’outil Explorateur de compte de stockage de hello.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-1.png)

1. Entrez hello **nom de compte** et **clé de compte** à l’étape 1, cliquez sur **suivant** , puis **connexion**. 

    ![Entrez les informations d’identification du stockage hello et se connecter.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-2.png)

1. Développez le compte de stockage hello attaché, cliquez sur **conteneurs d’objets Blob**, cliquez sur **créer un conteneur blob**, type `mycontainer`, puis appuyez sur ENTRÉE.

    ![Créez une file d’attente de stockage.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-create-blob-container.png)

Maintenant que vous avez un conteneur d’objets blob, vous pouvez tester la fonction hello en téléchargeant un conteneur toohello de fichier.

## <a name="test-hello-function"></a>Fonction hello de test

1. Dans hello portail Azure, parcourir tooyour fonction développez hello **journaux** bas hello page de hello et assurez-vous que ce journal de diffusion en continu n’est pas suspendue.

1. Dans l’Explorateur de stockage, développez votre compte de stockage, **Conteneurs d’objets Blob** et **mycontainer**. Cliquez sur **Charger**, puis sur **Charger des fichiers...**.

    ![Télécharger un conteneur d’objets blob toohello fichier.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-upload-file-blob.png)

1. Bonjour **télécharger des fichiers** boîte de dialogue, cliquez sur hello **fichiers** champ. Rechercher le fichier tooa sur votre ordinateur local, tel qu’un fichier image, sélectionnez-le, puis cliquez sur **ouvrir** , puis **télécharger**.

1. Revenir en arrière tooyour fonction journaux et vérifiez que cet objet blob hello a été lu.

   ![Afficher le message dans les journaux hello.](./media/functions-create-storage-blob-triggered-function/functions-blob-storage-trigger-view-logs.png)

    >[!NOTE]
    > Lorsque votre application de la fonction s’exécute dans le plan de la consommation hello par défaut, il peut y avoir un délai de configuration tooseveral minutes entre hello blob qui est ajouté ou mis à jour et hello fonction soit déclenchée. Si vous exigez une faible latence pour vos fonctions déclenchées par des objets Blob, exécutez plutôt votre Function App dans un plan App Service.

## <a name="clean-up-resources"></a>Supprimer des ressources

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Étapes suivantes

Vous avez créé une fonction qui s’exécute lorsqu’un objet blob est ajouté tooor mis à jour dans le stockage Blob. 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Pour plus d’informations sur les déclencheurs de stockage Blob, consultez [Liaisons de stockage Blob Azure Functions](functions-bindings-storage-blob.md).
