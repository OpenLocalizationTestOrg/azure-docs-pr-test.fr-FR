---
title: "Créer votre première fonction à l’aide du Portail Azure | Microsoft Docs"
description: "Apprenez à créer votre première fonction Azure pour une exécution sans serveur à l’aide du portail Azure."
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
ms.openlocfilehash: 3ec1f278f21d89782137625aff200f07f15fd9fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-function-in-the-azure-portal"></a><span data-ttu-id="be773-103">Créer votre première fonction à l’aide du Portail Azure</span><span class="sxs-lookup"><span data-stu-id="be773-103">Create your first function in the Azure portal</span></span>

<span data-ttu-id="be773-104">Azure Functions vous permet d’exécuter votre code dans un environnement sans serveur et sans avoir à créer une machine virtuelle ou à publier une application web au préalable.</span><span class="sxs-lookup"><span data-stu-id="be773-104">Azure Functions lets you execute your code in a serverless environment without having to first create a VM or publish a web application.</span></span> <span data-ttu-id="be773-105">Dans cette rubrique, vous allez découvrir comment utiliser Functions pour créer une fonction « hello world » dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="be773-105">In this topic, learn how to use Functions to create a "hello world" function in the Azure portal.</span></span>

![Créer une Function App dans le Portail Azure](./media/functions-create-first-azure-function/function-app-in-portal-editor.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="log-in-to-azure"></a><span data-ttu-id="be773-107">Connexion à Azure</span><span class="sxs-lookup"><span data-stu-id="be773-107">Log in to Azure</span></span>

<span data-ttu-id="be773-108">Connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="be773-108">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="be773-109">Créer une Function App</span><span class="sxs-lookup"><span data-stu-id="be773-109">Create a function app</span></span>

<span data-ttu-id="be773-110">Vous devez disposer d’une Function App pour héberger l’exécution de vos fonctions.</span><span class="sxs-lookup"><span data-stu-id="be773-110">You must have a function app to host the execution of your functions.</span></span> <span data-ttu-id="be773-111">Une Function App vous permet de regrouper les fonctions en une unité logique pour faciliter la gestion, le déploiement et le partage des ressources.</span><span class="sxs-lookup"><span data-stu-id="be773-111">A function app lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span></span> 

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

<span data-ttu-id="be773-112">Créez ensuite une fonction dans la nouvelle Function App.</span><span class="sxs-lookup"><span data-stu-id="be773-112">Next, you create a function in the new function app.</span></span>

## <span data-ttu-id="be773-113"><a name="create-function"></a>Créer une fonction déclenchée via HTTP</span><span class="sxs-lookup"><span data-stu-id="be773-113"><a name="create-function"></a>Create an HTTP triggered function</span></span>

1. <span data-ttu-id="be773-114">Développez votre nouvelle Function App, puis cliquez sur le bouton **+** en regard de **Fonctions**.</span><span class="sxs-lookup"><span data-stu-id="be773-114">Expand your new function app, then click the **+** button next to **Functions**.</span></span>

2.  <span data-ttu-id="be773-115">Sur la page **Commencez rapidement**, sélectionnez **WebHook + API**, **choisissez le langage** de votre fonction, puis cliquez sur **Créer cette fonction**.</span><span class="sxs-lookup"><span data-stu-id="be773-115">In the **Get started quickly** page, select **WebHook + API**, **Choose a language** for your function, and click **Create this function**.</span></span> 
   
    ![Démarrage rapide de fonctions dans le portail Azure.](./media/functions-create-first-azure-function/function-app-quickstart-node-webhook.png)

<span data-ttu-id="be773-117">Une fonction est créée dans le langage que vous avez choisi à l’aide du modèle de fonction déclenchée via HTTP.</span><span class="sxs-lookup"><span data-stu-id="be773-117">A function is created in your chosen language using the template for an HTTP triggered function.</span></span> <span data-ttu-id="be773-118">Vous pouvez exécuter la nouvelle fonction en envoyant une demande HTTP.</span><span class="sxs-lookup"><span data-stu-id="be773-118">You can run the new function by sending an HTTP request.</span></span>

## <a name="test-the-function"></a><span data-ttu-id="be773-119">Tester la fonction</span><span class="sxs-lookup"><span data-stu-id="be773-119">Test the function</span></span>

1. <span data-ttu-id="be773-120">Dans votre nouvelle fonction, cliquez sur **</> Obtenir l’URL de la fonction**, sélectionnez **par défaut (touche de fonction)**, puis cliquez sur **Copier**.</span><span class="sxs-lookup"><span data-stu-id="be773-120">In your new function, click **</> Get function URL**, select **default (Function key)**, and then click **Copy**.</span></span> 

    ![Copier l’URL de fonction à partir du portail Azure](./media/functions-create-first-azure-function/function-app-develop-tab-testing.png)

2. <span data-ttu-id="be773-122">Collez l’URL de fonction dans la barre d’adresse de votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="be773-122">Paste the function URL into your browser's address bar.</span></span> <span data-ttu-id="be773-123">Ajoutez la chaîne de requête `&name=<yourname>` à cette URL et appuyez sur la touche `Enter` de votre clavier pour exécuter la requête.</span><span class="sxs-lookup"><span data-stu-id="be773-123">Append the query string `&name=<yourname>` to this URL and press the `Enter` key on your keyboard to execute the request.</span></span> <span data-ttu-id="be773-124">Voici un exemple de la réponse retournée par la fonction dans le navigateur Edge :</span><span class="sxs-lookup"><span data-stu-id="be773-124">The following is an example of the response returned by the function in the Edge browser:</span></span>

    ![Réponse de la fonction dans le navigateur.](./media/functions-create-first-azure-function/function-app-browser-testing.png)

    <span data-ttu-id="be773-126">L’URL de demande inclut une clé qui est requise, par défaut, pour accéder à votre fonction sur HTTP.</span><span class="sxs-lookup"><span data-stu-id="be773-126">The request URL includes a key that is required, by default, to access your function over HTTP.</span></span>   

3. <span data-ttu-id="be773-127">Lorsque votre fonction s’exécute, des informations de suivi sont écrites dans les journaux.</span><span class="sxs-lookup"><span data-stu-id="be773-127">When your function runs, trace information is written to the logs.</span></span> <span data-ttu-id="be773-128">Pour afficher la sortie de suivi de l’exécution précédente, revenez à votre fonction dans le portail et cliquez sur la flèche vers le haut figurant en bas de l’écran pour développer **Journaux**.</span><span class="sxs-lookup"><span data-stu-id="be773-128">To see the trace output from the previous execution, return to your function in the portal and click the up arrow at the bottom of the screen to expand **Logs**.</span></span> 

   ![Affichage des journaux de fonction dans le portail Azure.](./media/functions-create-first-azure-function/function-view-logs.png)

## <a name="clean-up-resources"></a><span data-ttu-id="be773-130">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="be773-130">Clean up resources</span></span>

[!INCLUDE [Clean up resources](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="be773-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="be773-131">Next steps</span></span>

<span data-ttu-id="be773-132">Vous avez créé une Function App avec une simple fonction déclenchée via HTTP.</span><span class="sxs-lookup"><span data-stu-id="be773-132">You have created a function app with a simple HTTP triggered function.</span></span>  

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="be773-133">Pour plus d’informations, consultez [Liaisons HTTP et webhook Azure Functions](functions-bindings-http-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="be773-133">For more information, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span>



