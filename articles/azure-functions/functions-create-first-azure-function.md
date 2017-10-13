---
title: "Créer votre première fonction à l’aide du Portail Azure | Microsoft Docs"
description: "Apprenez à créer votre première fonction Azure pour une exécution sans serveur à l’aide du portail Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: cfowler
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
ms.custom: mvc, devcenter
ms.openlocfilehash: 2b73b8b1c5773b471c49394b0cceb3916afb9a70
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="create-your-first-function-in-the-azure-portal"></a>Créer votre première fonction à l’aide du Portail Azure

Azure Functions vous permet d’exécuter votre code dans un environnement sans serveur et sans avoir à créer une machine virtuelle ou à publier une application web au préalable. Dans cette rubrique, vous allez découvrir comment utiliser Functions pour créer une fonction « hello world » dans le portail Azure.

![Créer une Function App dans le Portail Azure](./media/functions-create-first-azure-function/function-app-in-portal-editor.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="log-in-to-azure"></a>Connexion à Azure

Connectez-vous au [portail Azure](https://portal.azure.com/).

## <a name="create-a-function-app"></a>Créer une Function App

Vous devez disposer d’une Function App pour héberger l’exécution de vos fonctions. Une Function App vous permet de regrouper les fonctions en une unité logique pour faciliter la gestion, le déploiement et le partage des ressources. 

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

Créez ensuite une fonction dans la nouvelle Function App.

## <a name="create-function"></a>Créer une fonction déclenchée via HTTP

1. Développez votre nouvelle Function App, puis cliquez sur le bouton **+** en regard de **Fonctions**.

2.  Sur la page **Commencez rapidement**, sélectionnez **WebHook + API**, **choisissez le langage** de votre fonction, puis cliquez sur **Créer cette fonction**. 
   
    ![Démarrage rapide de fonctions dans le portail Azure.](./media/functions-create-first-azure-function/function-app-quickstart-node-webhook.png)

Une fonction est créée dans le langage que vous avez choisi à l’aide du modèle de fonction déclenchée via HTTP. Vous pouvez exécuter la nouvelle fonction en envoyant une demande HTTP.

## <a name="test-the-function"></a>Tester la fonction

1. Dans votre nouvelle fonction, cliquez sur **</> Obtenir l’URL de la fonction**, sélectionnez **par défaut (touche de fonction)**, puis cliquez sur **Copier**. 

    ![Copier l’URL de fonction à partir du portail Azure](./media/functions-create-first-azure-function/function-app-develop-tab-testing.png)

2. Collez l’URL de fonction dans la barre d’adresse de votre navigateur. Ajoutez la chaîne de requête `&name=<yourname>` à cette URL et appuyez sur la touche `Enter` de votre clavier pour exécuter la requête. Voici un exemple de la réponse retournée par la fonction dans le navigateur Edge :

    ![Réponse de la fonction dans le navigateur.](./media/functions-create-first-azure-function/function-app-browser-testing.png)

    L’URL de demande inclut une clé qui est requise, par défaut, pour accéder à votre fonction sur HTTP.   

3. Lorsque votre fonction s’exécute, des informations de suivi sont écrites dans les journaux. Pour afficher la sortie de suivi de l’exécution précédente, revenez à votre fonction dans le portail et cliquez sur la flèche vers le haut figurant en bas de l’écran pour développer **Journaux**. 

   ![Affichage des journaux de fonction dans le portail Azure.](./media/functions-create-first-azure-function/function-view-logs.png)

## <a name="clean-up-resources"></a>Supprimer des ressources

[!INCLUDE [Clean up resources](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Étapes suivantes

Vous avez créé une Function App avec une simple fonction déclenchée via HTTP.  

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Pour plus d’informations, consultez [Liaisons HTTP et webhook Azure Functions](functions-bindings-http-webhook.md).



