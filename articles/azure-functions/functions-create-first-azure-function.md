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
# <a name="create-your-first-function-in-hello-azure-portal"></a><span data-ttu-id="a1af9-103">Créer votre première fonction Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="a1af9-103">Create your first function in hello Azure portal</span></span>

<span data-ttu-id="a1af9-104">Les fonctions Azure vous permet d’exécuter votre code dans un environnement sans serveur sans avoir toofirst créer une machine virtuelle ou publier une application web.</span><span class="sxs-lookup"><span data-stu-id="a1af9-104">Azure Functions lets you execute your code in a serverless environment without having toofirst create a VM or publish a web application.</span></span> <span data-ttu-id="a1af9-105">Dans cette rubrique, découvrez comment toouse fonctionne toocreate une fonction de « hello world » dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a1af9-105">In this topic, learn how toouse Functions toocreate a "hello world" function in hello Azure portal.</span></span>

![Créer l’application de la fonction Bonjour portail Azure](./media/functions-create-first-azure-function/function-app-in-portal-editor.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="log-in-tooazure"></a><span data-ttu-id="a1af9-107">Connectez-vous à tooAzure</span><span class="sxs-lookup"><span data-stu-id="a1af9-107">Log in tooAzure</span></span>

<span data-ttu-id="a1af9-108">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a1af9-108">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="a1af9-109">Créer une Function App</span><span class="sxs-lookup"><span data-stu-id="a1af9-109">Create a function app</span></span>

<span data-ttu-id="a1af9-110">Vous devez disposer d’une application toohost hello exécution d’une fonction de vos fonctions.</span><span class="sxs-lookup"><span data-stu-id="a1af9-110">You must have a function app toohost hello execution of your functions.</span></span> <span data-ttu-id="a1af9-111">Une Function App vous permet de regrouper les fonctions en une unité logique pour faciliter la gestion, le déploiement et le partage des ressources.</span><span class="sxs-lookup"><span data-stu-id="a1af9-111">A function app lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span></span> 

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

<span data-ttu-id="a1af9-112">Ensuite, créez une fonction dans hello une nouvelle application de fonction.</span><span class="sxs-lookup"><span data-stu-id="a1af9-112">Next, you create a function in hello new function app.</span></span>

## <span data-ttu-id="a1af9-113"><a name="create-function"></a>Créer une fonction déclenchée via HTTP</span><span class="sxs-lookup"><span data-stu-id="a1af9-113"><a name="create-function"></a>Create an HTTP triggered function</span></span>

1. <span data-ttu-id="a1af9-114">Développez votre nouvelle application de la fonction, puis cliquez sur hello  **+**  bouton ensuite trop**fonctions**.</span><span class="sxs-lookup"><span data-stu-id="a1af9-114">Expand your new function app, then click hello **+** button next too**Functions**.</span></span>

2.  <span data-ttu-id="a1af9-115">Bonjour **mise en route rapide** page, sélectionnez **WebHook + API**, **choisir une langue** votre fonction, puis cliquez sur **créer cette fonction** .</span><span class="sxs-lookup"><span data-stu-id="a1af9-115">In hello **Get started quickly** page, select **WebHook + API**, **Choose a language** for your function, and click **Create this function**.</span></span> 
   
    ![Démarrage rapide de fonctions Bonjour portail Azure.](./media/functions-create-first-azure-function/function-app-quickstart-node-webhook.png)

<span data-ttu-id="a1af9-117">Une fonction est créée dans la langue choisie à l’aide du modèle de hello pour une fonction HTTP déclenchée.</span><span class="sxs-lookup"><span data-stu-id="a1af9-117">A function is created in your chosen language using hello template for an HTTP triggered function.</span></span> <span data-ttu-id="a1af9-118">Vous pouvez exécuter la fonction hello en envoyant une requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="a1af9-118">You can run hello new function by sending an HTTP request.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="a1af9-119">Fonction hello de test</span><span class="sxs-lookup"><span data-stu-id="a1af9-119">Test hello function</span></span>

1. <span data-ttu-id="a1af9-120">Dans votre nouvelle fonction, cliquez sur **</> Obtenir l’URL de la fonction**, sélectionnez **par défaut (touche de fonction)**, puis cliquez sur **Copier**.</span><span class="sxs-lookup"><span data-stu-id="a1af9-120">In your new function, click **</> Get function URL**, select **default (Function key)**, and then click **Copy**.</span></span> 

    ![Fonction hello copier l’URL de hello portail Azure](./media/functions-create-first-azure-function/function-app-develop-tab-testing.png)

2. <span data-ttu-id="a1af9-122">Collez l’URL de fonction hello dans la barre d’adresse de votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="a1af9-122">Paste hello function URL into your browser's address bar.</span></span> <span data-ttu-id="a1af9-123">Ajouter la chaîne de requête hello `&name=<yourname>` hello d’URL, puis appuyez sur toothis `Enter` clés sur votre demande de hello tooexecute clavier.</span><span class="sxs-lookup"><span data-stu-id="a1af9-123">Append hello query string `&name=<yourname>` toothis URL and press hello `Enter` key on your keyboard tooexecute hello request.</span></span> <span data-ttu-id="a1af9-124">Hello Voici un exemple de réponse hello retourné par la fonction hello dans le navigateur Edge hello :</span><span class="sxs-lookup"><span data-stu-id="a1af9-124">hello following is an example of hello response returned by hello function in hello Edge browser:</span></span>

    ![Réponse de la fonction dans le navigateur de hello.](./media/functions-create-first-azure-function/function-app-browser-testing.png)

    <span data-ttu-id="a1af9-126">demande Hello URL inclut une clé qui est requis, par défaut, tooaccess votre fonction via HTTP.</span><span class="sxs-lookup"><span data-stu-id="a1af9-126">hello request URL includes a key that is required, by default, tooaccess your function over HTTP.</span></span>   

3. <span data-ttu-id="a1af9-127">Lorsque votre fonction s’exécute, les informations de trace sont écrite toohello journaux.</span><span class="sxs-lookup"><span data-stu-id="a1af9-127">When your function runs, trace information is written toohello logs.</span></span> <span data-ttu-id="a1af9-128">sortie de trace hello toosee à partir de l’exécution précédente de hello, retourner tooyour fonction dans le portail de hello et cliquez sur hello flèche bas hello hello écran tooexpand **journaux**.</span><span class="sxs-lookup"><span data-stu-id="a1af9-128">toosee hello trace output from hello previous execution, return tooyour function in hello portal and click hello up arrow at hello bottom of hello screen tooexpand **Logs**.</span></span> 

   ![Fonctions visionneuse du journal Bonjour portail Azure.](./media/functions-create-first-azure-function/function-view-logs.png)

## <a name="clean-up-resources"></a><span data-ttu-id="a1af9-130">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="a1af9-130">Clean up resources</span></span>

[!INCLUDE [Clean up resources](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="a1af9-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a1af9-131">Next steps</span></span>

<span data-ttu-id="a1af9-132">Vous avez créé une Function App avec une simple fonction déclenchée via HTTP.</span><span class="sxs-lookup"><span data-stu-id="a1af9-132">You have created a function app with a simple HTTP triggered function.</span></span>  

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="a1af9-133">Pour plus d’informations, consultez [Liaisons HTTP et webhook Azure Functions](functions-bindings-http-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="a1af9-133">For more information, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span>



