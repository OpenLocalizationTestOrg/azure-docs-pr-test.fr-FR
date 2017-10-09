---
title: "aaaCreate votre première fonction à partir de hello portail Azure | Documents Microsoft"
description: "Découvrez comment toocreate votre première Azure de fonction pour l’utilisation de l’exécution sans serveur hello portail Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 96cf87b9-8db6-41a8-863a-abb828e3d06d
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/07/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 84283d7d4bc6015061946af4589f9a70ae61f36b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-in-hello-azure-portal"></a>Créer votre première fonction Bonjour portail Azure

Les fonctions Azure vous permet d’exécuter votre code dans un environnement sans serveur sans avoir toofirst créer une machine virtuelle ou publier une application web. Dans cette rubrique, découvrez comment toouse fonctionne toocreate une fonction de « hello world » dans hello portail Azure.

![Créer l’application de la fonction Bonjour portail Azure](./media/functions-create-first-azure-function/function-app-in-portal-editor.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="log-in-tooazure"></a>Connectez-vous à tooAzure

Connectez-vous à toohello [portail Azure](https://portal.azure.com/).

## <a name="create-a-function-app"></a>Créer une Function App

Vous devez disposer d’une application toohost hello exécution d’une fonction de vos fonctions. Une Function App vous permet de regrouper les fonctions en une unité logique pour faciliter la gestion, le déploiement et le partage des ressources. 

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

Ensuite, créez une fonction dans hello une nouvelle application de fonction.

## <a name="create-function"></a>Créer une fonction déclenchée via HTTP

1. Développez votre nouvelle application de la fonction, puis cliquez sur hello  **+**  bouton ensuite trop**fonctions**.

2.  Bonjour **mise en route rapide** page, sélectionnez **WebHook + API**, **choisir une langue** votre fonction, puis cliquez sur **créer cette fonction** . 
   
    ![Démarrage rapide de fonctions Bonjour portail Azure.](./media/functions-create-first-azure-function/function-app-quickstart-node-webhook.png)

Une fonction est créée dans la langue choisie à l’aide du modèle de hello pour une fonction HTTP déclenchée. Vous pouvez exécuter la fonction hello en envoyant une requête HTTP.

## <a name="test-hello-function"></a>Fonction hello de test

1. Dans votre nouvelle fonction, cliquez sur **</> Obtenir l’URL de la fonction**, sélectionnez **par défaut (touche de fonction)**, puis cliquez sur **Copier**. 

    ![Fonction hello copier l’URL de hello portail Azure](./media/functions-create-first-azure-function/function-app-develop-tab-testing.png)

2. Collez l’URL de fonction hello dans la barre d’adresse de votre navigateur. Ajouter la chaîne de requête hello `&name=<yourname>` hello d’URL, puis appuyez sur toothis `Enter` clés sur votre demande de hello tooexecute clavier. Hello Voici un exemple de réponse hello retourné par la fonction hello dans le navigateur Edge hello :

    ![Réponse de la fonction dans le navigateur de hello.](./media/functions-create-first-azure-function/function-app-browser-testing.png)

    demande Hello URL inclut une clé qui est requis, par défaut, tooaccess votre fonction via HTTP.   

3. Lorsque votre fonction s’exécute, les informations de trace sont écrite toohello journaux. sortie de trace hello toosee à partir de l’exécution précédente de hello, retourner tooyour fonction dans le portail de hello et cliquez sur hello flèche bas hello hello écran tooexpand **journaux**. 

   ![Fonctions visionneuse du journal Bonjour portail Azure.](./media/functions-create-first-azure-function/function-view-logs.png)

## <a name="clean-up-resources"></a>Supprimer des ressources

[!INCLUDE [Clean up resources](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Étapes suivantes

Vous avez créé une Function App avec une simple fonction déclenchée via HTTP.  

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Pour plus d’informations, consultez [Liaisons HTTP et webhook Azure Functions](functions-bindings-http-webhook.md).



