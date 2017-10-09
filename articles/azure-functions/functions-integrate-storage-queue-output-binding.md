---
title: "une fonction dans Azure déclenché par des messages de la file d’attente d’aaaCreate | Documents Microsoft"
description: "Utilisez les fonctions Azure toocreate une fonction sans serveur qui est appelée par une les messages soumis file d’attente de stockage Azure tooan."
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 0b609bc0-c264-4092-8e3e-0784dcc23b5d
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/17/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 44db90fa80bf77e31bf53dddabd7136de5800b11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-messages-tooan-azure-storage-queue-using-functions"></a>Ajouter la file d’attente de messages tooan stockage Azure à l’aide de fonctions

Dans les fonctions d’Azure, les liaisons d’entrée et de sortie fournissent une données de service de façon déclarative tooconnect tooexternal à partir de votre fonction. Dans cette rubrique, découvrez comment tooupdate une fonction existante en ajoutant une sortie de liaison qui envoie des messages stockage de file d’attente tooAzure.  

![Afficher le message dans les journaux hello.](./media/functions-integrate-storage-queue-output-binding/functions-integrate-storage-binding-in-portal.png)

## <a name="prerequisites"></a>Composants requis 

[!INCLUDE [Previous topics](../../includes/functions-quickstart-previous-topics.md)]

* Installer hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).

## <a name="add-binding"></a>Ajoutez une liaison de sortie
 
1. Développez à la fois votre application de fonction et votre fonction.

2. Cliquez sur **Intégrer** et **+ Nouvelle sortie**, puis choisissez **Stockage File d’attente Azure** et **Sélectionner**.
    
    ![Ajouter une fonction de file d’attente stockage sortie liaison tooa Bonjour portail Azure.](./media/functions-integrate-storage-queue-output-binding/function-add-queue-storage-output-binding.png)

3. Utiliser les paramètres de hello comme spécifié dans la table de hello : 

    ![Ajouter une fonction de file d’attente stockage sortie liaison tooa Bonjour portail Azure.](./media/functions-integrate-storage-queue-output-binding/function-add-queue-storage-output-binding-2.png)

    | Paramètre      |  Valeur suggérée   | Description                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | **Nom de la file d’attente**   | éléments myqueue    | nom Hello Hello file d’attente tooconnect tooin votre compte de stockage. |
    | **Connexion au compte de stockage** | AzureWebJobStorage | Vous pouvez utiliser la connexion au compte de stockage hello est déjà utilisée par votre application de la fonction, ou créez-en un.  |
    | **Nom de message de paramètre** | outputQueueItem | nom Hello hello liaison de paramètre de sortie. | 

4. Cliquez sur **enregistrer** liaison de hello tooadd.
 
Maintenant que vous avez définie une liaison de sortie, vous devez tooupdate hello code toouse hello liaison tooadd messages tooa file d’attente.  

## <a name="update-hello-function-code"></a>Mettre à jour le code de la fonction hello

1. Sélectionnez votre code de fonction hello fonction toodisplay dans l’éditeur de hello. 

2. Pour une fonction c#, mise à jour de votre définition de fonction comme suit tooadd hello **outputQueueItem** paramètre de liaison de stockage. Ignorez cette étape pour une fonction JavaScript.

    ```cs   
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, 
        ICollector<string> outputQueueItem, TraceWriter log)
    {
        ....
    }
    ```

3. Ajoutez hello suivant fonction toohello de code juste avant le retour de méthode hello. Utilisez hello approprié extrait de code pour la langue hello de votre fonction.

    ```javascript
    context.bindings.outputQueueItem = "Name passed toohello function: " + 
                (req.query.name || req.body.name);
    ```

    ```cs
    outputQueueItem.Add("Name passed toohello function: " + name);     
    ```

4. Sélectionnez **enregistrer** toosave modifications.

valeur de Hello passé le déclencheur HTTP toohello est incluse dans une file d’attente de message toohello ajouté.
 
## <a name="test-hello-function"></a>Fonction hello de test 

1. Après avoir enregistrement les modifications de code hello, sélectionnez **exécuter**. 

    ![Ajouter une fonction de file d’attente stockage sortie liaison tooa Bonjour portail Azure.](./media/functions-integrate-storage-queue-output-binding/functions-test-run-function.png)

2. Vérifiez toomake de journaux hello assurer que la fonction hello a réussi. Une nouvelle file d’attente nommée **outqueue** est créé dans votre compte de stockage par hello fonctions runtime lors de la liaison de sortie hello est utilisée pour la première fois.

Ensuite, vous pouvez vous connecter tooyour stockage compte tooverify hello nouvelle file d’attente et vous avez ajouté tooit message de type hello. 

## <a name="connect-toohello-queue"></a>Se connecter à la file d’attente de toohello

Skip hello trois premières étapes si vous avez déjà installé l’Explorateur de stockage et le compte de stockage tooyour elle est connectée.    

1. Dans votre fonction, choisissez **intégrer** et hello nouvelle **stockage de file d’attente Azure** liaison de sortie, puis développez **Documentation**. Copiez le **Nom de compte** et la **Clé de compte**. Vous utilisez ces informations d’identification tooconnect toohello stockage compte.
 
    ![Obtenir des informations d’identification de connexion de compte de stockage hello.](./media/functions-integrate-storage-queue-output-binding/function-get-storage-account-credentials.png)

2. Exécutez hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) outil, sélectionnez hello icône à gauche de hello de connexion, choisissez **utiliser un nom de compte de stockage et de la clé**, puis sélectionnez **suivant**.

    ![Exécuter l’outil Explorateur de compte de stockage de hello.](./media/functions-integrate-storage-queue-output-binding/functions-storage-manager-connect-1.png)
    
3. Hello de coller **nom de compte** et **clé de compte** à l’étape 1 dans les champs correspondants, puis sélectionnez **suivant**, et **connexion**. 
  
    ![Collez les informations d’identification du stockage hello et se connecter.](./media/functions-integrate-storage-queue-output-binding/functions-storage-manager-connect-2.png)

4. Développez le compte de stockage hello attaché, **les files d’attente** et vérifiez qu’une file d’attente appelé **myqueue-éléments** existe. Vous devez également voir un message déjà dans la file d’attente hello.  
 
    ![Créez une file d’attente de stockage.](./media/functions-integrate-storage-queue-output-binding/function-queue-storage-output-view-queue.png)
 

## <a name="clean-up-resources"></a>Supprimer des ressources

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Étapes suivantes

Vous avez ajouté une fonction existante de tooan de liaison de sortie. 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Pour plus d’informations sur le stockage de tooQueue de liaison, consultez [liaisons de file d’attente de stockage de fonctions Azure](functions-bindings-storage-queue.md). 



