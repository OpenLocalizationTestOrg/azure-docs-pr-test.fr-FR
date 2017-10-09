---
title: "une fonction dans Azure déclenché par des messages de la file d’attente d’aaaCreate | Documents Microsoft"
description: "Utilisez les fonctions Azure toocreate une fonction sans serveur qui est appelée par une les messages soumis file d’attente de stockage Azure tooan."
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 361da2a4-15d1-4903-bdc4-cc4b27fc3ff4
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: e9501ed336b502eaeee3fa62ec4ae085c76de0ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-azure-queue-storage"></a>Créer une fonction déclenchée par une file d’attente de stockage Azure

Découvrez comment toocreate une fonction déclenchée lorsque les messages sont soumis la file d’attente de stockage Azure tooan.

![Afficher le message dans les journaux hello.](./media/functions-create-storage-queue-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>Composants requis

- Téléchargez et installez hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).

- Un abonnement Azure. Si vous n’en avez pas, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Création d’une application Azure Function

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Function App créée avec succès.](./media/functions-create-first-azure-function/function-app-create-success.png)

Ensuite, créez une fonction dans hello une nouvelle application de fonction.

<a name="create-function"></a>

## <a name="create-a-queue-triggered-function"></a>Créer une fonction déclenchée par une file d’attente

1. Développez votre application de la fonction et cliquez sur hello  **+**  bouton ensuite trop**fonctions**. S’il s’agit de hello première fonction dans votre application de la fonction, sélectionnez **fonction personnalisée**. Cela affiche le jeu complet de hello des modèles de fonction.

    ![Page de démarrage rapide de fonctions Bonjour portail Azure](./media/functions-create-storage-queue-triggered-function/add-first-function.png)

2. Sélectionnez hello **QueueTrigger** modèle pour votre langue de votre choix, puis utiliser les paramètres comme spécifié dans la table de hello hello.

    ![Créer la fonction de file d’attente déclenchée stockage hello.](./media/functions-create-storage-queue-triggered-function/functions-create-queue-storage-trigger-portal.png)
    
    | Paramètre | Valeur suggérée | Description |
    |---|---|---|
    | **Nom de la file d’attente**   | éléments myqueue    | Nom de hello file d’attente tooconnect tooin votre compte de stockage. |
    | **Connexion au compte de stockage** | AzureWebJobStorage | Vous pouvez utiliser la connexion au compte de stockage hello est déjà utilisée par votre application de la fonction, ou créez-en un.  |
    | **Nommer votre fonction** | Unique dans votre Function App | Nom de cette fonction déclenchée par la file d’attente. |

3. Cliquez sur **créer** toocreate votre fonction.

Ensuite, vous vous connectez compte de stockage Azure tooyour et que vous créez hello **myqueue-éléments** file d’attente de stockage.

## <a name="create-hello-queue"></a>Créer la file d’attente hello

1. Dans votre fonction, cliquez sur **Intégrer**, développez **Documentation** et copiez le **Nom du compte** et la **Clé du compte**. Vous utilisez ces informations d’identification tooconnect toohello stockage compte. Si vous êtes déjà connecté votre compte de stockage, passez toostep 4.

    ![Obtenir des informations d’identification de connexion de compte de stockage hello.](./media/functions-create-storage-queue-triggered-function/functions-storage-account-connection.png)v

1. Exécutez hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) outil, cliquez sur hello icône à gauche de hello de connexion, choisissez **utiliser un nom de compte de stockage et de la clé**, puis cliquez sur **suivant**.

    ![Exécuter l’outil Explorateur de compte de stockage de hello.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-1.png)

1. Entrez hello **nom de compte** et **clé de compte** à l’étape 1, cliquez sur **suivant** , puis **connexion**.

    ![Entrez les informations d’identification du stockage hello et se connecter.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-2.png)

1. Développez le compte de stockage hello attaché, cliquez sur **les files d’attente**, cliquez sur **Create queue**, type `myqueue-items`, puis appuyez sur ENTRÉE.

    ![Créez une file d’attente de stockage.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-create-queue.png)

Maintenant que vous avez une file d’attente de stockage, vous pouvez tester la fonction hello en ajoutant une file d’attente de message toohello.

## <a name="test-hello-function"></a>Fonction hello de test

1. Dans hello portail Azure, parcourir tooyour fonction développez hello **journaux** bas hello page de hello et assurez-vous que ce journal de diffusion en continu n’est pas suspendue.

1. Dans l’Explorateur de stockage, développez votre compte de stockage, **Files d’attente**, et **myqueue-items**, puis cliquez sur **Ajouter message**.

    ![Ajouter une file d’attente de message toohello.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-add-message.png)

1. Saisissez le message « Hello World ! » dans **Texte du message** et cliquez sur **OK**.

1. Attendez quelques secondes, puis revenir en arrière tooyour fonction journaux et vérifiez que ce nouveau message de salutation a été lu à partir de la file d’attente hello.

    ![Afficher le message dans les journaux hello.](./media/functions-create-storage-queue-triggered-function/functions-queue-storage-trigger-view-logs.png)

1. Dans l’Explorateur de stockage, cliquez sur **Actualiser** et vérifiez que ce message de type hello a été traité et n’est plus dans la file d’attente hello.

## <a name="clean-up-resources"></a>Supprimer des ressources

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Étapes suivantes

Vous avez créé une fonction qui s’exécute lorsqu’un message est ajouté de file d’attente de stockage tooa.

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Pour en savoir plus sur les déclencheurs de stockage en file d’attente, consultez la page [Liaisons de file d’attente de stockage Azure Functions](functions-bindings-storage-queue.md).