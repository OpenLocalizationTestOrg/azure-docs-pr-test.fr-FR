---
title: "aaaCreate votre première fonction dans Azure à l’aide de Visual Studio | Documents Microsoft"
description: "Créer et publier un tooAzure de fonction HTTP déclenchée simple à l’aide des fonctions de Windows Azure Tools pour Visual Studio."
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
editor: 
tags: 
keywords: "azure functions, functions, traitement des événements, calcul, architecture sans serveur"
ms.assetid: 82db1177-2295-4e39-bd42-763f6082e796
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 07/05/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 851e5b98dcc2da00334620896a0ea31f566589f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-using-visual-studio"></a><span data-ttu-id="9fee5-104">Créer votre première fonction à l’aide de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9fee5-104">Create your first function using Visual Studio</span></span>

<span data-ttu-id="9fee5-105">Les fonctions Azure vous permet d’exécuter votre code dans un environnement sans serveur sans avoir toofirst créer une machine virtuelle ou publier une application web.</span><span class="sxs-lookup"><span data-stu-id="9fee5-105">Azure Functions lets you execute your code in a serverless environment without having toofirst create a VM or publish a web application.</span></span>

<span data-ttu-id="9fee5-106">Dans cette rubrique, vous découvrez comment toouse hello tools de Visual Studio 2017 pour toocreate des fonctions d’Azure et tester localement une fonction de « hello world ».</span><span class="sxs-lookup"><span data-stu-id="9fee5-106">In this topic, you learn how toouse hello Visual Studio 2017 tools for Azure Functions toocreate and test a "hello world" function locally.</span></span> <span data-ttu-id="9fee5-107">Vous allez ensuite publier tooAzure de code de fonction hello.</span><span class="sxs-lookup"><span data-stu-id="9fee5-107">You will then publish hello function code tooAzure.</span></span> <span data-ttu-id="9fee5-108">Ces outils sont disponibles dans le cadre de la charge de travail de développement Azure dans Visual Studio 2017 version 15.3 hello, ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="9fee5-108">These tools are available as part of hello Azure development workload in Visual Studio 2017 version 15.3, or a later version.</span></span>

![Code Azure Functions dans un projet Visual Studio](./media/functions-create-your-first-function-visual-studio/functions-vstools-intro.png)

## <a name="prerequisites"></a><span data-ttu-id="9fee5-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9fee5-110">Prerequisites</span></span>

<span data-ttu-id="9fee5-111">toocomplete ce didacticiel, installer :</span><span class="sxs-lookup"><span data-stu-id="9fee5-111">toocomplete this tutorial, install:</span></span>

* <span data-ttu-id="9fee5-112">[Visual Studio 2017 version 15.3](https://www.visualstudio.com/vs/preview/), y compris hello **le développement Azure** la charge de travail.</span><span class="sxs-lookup"><span data-stu-id="9fee5-112">[Visual Studio 2017 version 15.3](https://www.visualstudio.com/vs/preview/), including hello **Azure development** workload.</span></span>

    ![Installer Visual Studio 2017 avec une charge de travail de développement Azure hello](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)
    
    >[!NOTE]  
    <span data-ttu-id="9fee5-114">Une fois que vous installez ou mettez à niveau tooVisual Studio 2017 version 15.3, vous devrez peut-être outils de hello Visual Studio 2017 toomanually mises à jour pour les fonctions d’Azure.</span><span class="sxs-lookup"><span data-stu-id="9fee5-114">After you install or upgrade tooVisual Studio 2017 version 15.3, you might also need toomanually update hello Visual Studio 2017 tools for Azure Functions.</span></span> <span data-ttu-id="9fee5-115">Vous pouvez mettre à jour des outils hello hello **outils** menu sous **Extensions et mises à jour...**   >  **Mises à jour** > **Visual Studio Marketplace** > **outils des travaux Web et des fonctions Azure**  >  **Mise à jour**.</span><span class="sxs-lookup"><span data-stu-id="9fee5-115">You can update hello tools from hello **Tools** menu under **Extensions and Updates...** > **Updates** > **Visual Studio Marketplace** > **Azure Functions and Web Jobs Tools** > **Update**.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] 

## <a name="create-an-azure-functions-project-in-visual-studio"></a><span data-ttu-id="9fee5-116">Créer un projet Azure Functions dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9fee5-116">Create an Azure Functions project in Visual Studio</span></span>

[!INCLUDE [Create a project using hello Azure Functions template](../../includes/functions-vstools-create.md)]

<span data-ttu-id="9fee5-117">Maintenant que vous avez créé le projet de hello, vous pouvez créer votre première fonction.</span><span class="sxs-lookup"><span data-stu-id="9fee5-117">Now that you have created hello project, you can create your first function.</span></span>

## <a name="create-hello-function"></a><span data-ttu-id="9fee5-118">Créer la fonction hello</span><span class="sxs-lookup"><span data-stu-id="9fee5-118">Create hello function</span></span>

1. <span data-ttu-id="9fee5-119">Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur le nœud de projet et sélectionnez **Ajouter** > **Nouvel élément**.</span><span class="sxs-lookup"><span data-stu-id="9fee5-119">In **Solution Explorer**, right-click on your project node and select **Add** > **New Item**.</span></span> <span data-ttu-id="9fee5-120">Sélectionnez **Azure Function** et cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="9fee5-120">Select **Azure Function** and click **Add**.</span></span>

2. <span data-ttu-id="9fee5-121">Sélectionnez **HttpTrigger**, tapez un **nom de fonction**, sélectionnez **Anonyme** pour les **Droits d’accès**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="9fee5-121">Select **HttpTrigger**, type a **Function Name**, select **Anonymous** for **Access Rights**, and click **Create**.</span></span> <span data-ttu-id="9fee5-122">fonction Hello créée est accessible par une requête HTTP à partir de n’importe quel client.</span><span class="sxs-lookup"><span data-stu-id="9fee5-122">hello function created is accessed by an HTTP request from any client.</span></span> 

    ![Créer une fonction Azure](./media/functions-create-your-first-function-visual-studio/functions-vstools-add-new-function-2.png)

    <span data-ttu-id="9fee5-124">Un fichier de code est ajouté le projet tooyour qui contient une classe qui implémente votre code de fonction.</span><span class="sxs-lookup"><span data-stu-id="9fee5-124">A code file is added tooyour project that contains a class that implements your function code.</span></span> <span data-ttu-id="9fee5-125">Ce code est basé sur un modèle, qui reçoit une valeur de nom, puis la renvoie.</span><span class="sxs-lookup"><span data-stu-id="9fee5-125">This code is based on a template, which receives a name value and echos it back.</span></span> <span data-ttu-id="9fee5-126">Hello **FunctionName** attribut définit le nom hello de votre fonction.</span><span class="sxs-lookup"><span data-stu-id="9fee5-126">hello **FunctionName** attribute sets hello name of your function.</span></span> <span data-ttu-id="9fee5-127">Hello **HttpTrigger** attribut indique le message de type hello qui déclenche la fonction hello.</span><span class="sxs-lookup"><span data-stu-id="9fee5-127">hello **HttpTrigger** attribute indicates hello message that triggers hello function.</span></span> 

    ![Fichier du code de fonction](./media/functions-create-your-first-function-visual-studio/functions-code-page.png)

<span data-ttu-id="9fee5-129">Maintenant que vous avez créé une fonction HTTP déclenchée, vous pouvez la tester sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="9fee5-129">Now that you have created an HTTP-triggered function, you can test it on your local computer.</span></span>

## <a name="test-hello-function-locally"></a><span data-ttu-id="9fee5-130">Tester la fonction hello localement</span><span class="sxs-lookup"><span data-stu-id="9fee5-130">Test hello function locally</span></span>

<span data-ttu-id="9fee5-131">Azure Functions Core Tools vous permet d’exécuter un projet Azure Functions sur votre ordinateur de développement local.</span><span class="sxs-lookup"><span data-stu-id="9fee5-131">Azure Functions Core Tools lets you run Azure Functions project on your local development computer.</span></span> <span data-ttu-id="9fee5-132">Vous êtes invité à tooinstall ces outils hello la première fois que vous démarrez une fonction à partir de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9fee5-132">You are prompted tooinstall these tools hello first time you start a function from Visual Studio.</span></span>  

1. <span data-ttu-id="9fee5-133">tootest votre fonction, appuyez sur F5.</span><span class="sxs-lookup"><span data-stu-id="9fee5-133">tootest your function, press F5.</span></span> <span data-ttu-id="9fee5-134">Si vous y êtes invité, accepter la demande hello toodownload de Visual Studio et installez les outils de base des fonctions Azure (CLI).</span><span class="sxs-lookup"><span data-stu-id="9fee5-134">If prompted, accept hello request from Visual Studio toodownload and install Azure Functions Core (CLI) tools.</span></span>  <span data-ttu-id="9fee5-135">Vous devez également tooenable une exception de pare-feu afin que les outils hello peuvent traiter les requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="9fee5-135">You may also need tooenable a firewall exception so that hello tools can handle HTTP requests.</span></span>

2. <span data-ttu-id="9fee5-136">Copier l’URL de votre fonction de l’exécution de fonctions d’Azure hello hello de sortie.</span><span class="sxs-lookup"><span data-stu-id="9fee5-136">Copy hello URL of your function from hello Azure Functions runtime output.</span></span>  

    ![Azure runtime local](./media/functions-create-your-first-function-visual-studio/functions-vstools-f5.png)

3. <span data-ttu-id="9fee5-138">Collez l’URL hello pour la requête HTTP de hello dans la barre d’adresse de votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="9fee5-138">Paste hello URL for hello HTTP request into your browser's address bar.</span></span> <span data-ttu-id="9fee5-139">Ajouter la chaîne de requête hello `&name=<yourname>` toothis URL et l’exécution de la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="9fee5-139">Append hello query string `&name=<yourname>` toothis URL and execute hello request.</span></span> <span data-ttu-id="9fee5-140">les Voici Hello réponse de hello dans hello navigateur toohello local une demande GET retournée par la fonction hello :</span><span class="sxs-lookup"><span data-stu-id="9fee5-140">hello following shows hello response in hello browser toohello local GET request returned by hello function:</span></span> 

    ![Réponse de localhost de fonction dans le navigateur de hello](./media/functions-create-your-first-function-visual-studio/functions-test-local-browser.png)

4. <span data-ttu-id="9fee5-142">toostop de débogage, cliquez sur hello **arrêter** bouton de barre d’outils de Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="9fee5-142">toostop debugging, click hello **Stop** button on hello Visual Studio toolbar.</span></span>

<span data-ttu-id="9fee5-143">Après avoir vérifié que la fonction hello s’exécute correctement sur votre ordinateur local, il est temps toopublish hello projet tooAzure.</span><span class="sxs-lookup"><span data-stu-id="9fee5-143">After you have verified that hello function runs correctly on your local computer, it's time toopublish hello project tooAzure.</span></span>

## <a name="publish-hello-project-tooazure"></a><span data-ttu-id="9fee5-144">Publier hello projet tooAzure</span><span class="sxs-lookup"><span data-stu-id="9fee5-144">Publish hello project tooAzure</span></span>

<span data-ttu-id="9fee5-145">Vous devez disposer d’une application de fonction dans votre abonnement Azure avant de pouvoir publier votre projet.</span><span class="sxs-lookup"><span data-stu-id="9fee5-145">You must have a function app in your Azure subscription before you can publish your project.</span></span> <span data-ttu-id="9fee5-146">Vous pouvez créer une application de fonction directement à partir de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9fee5-146">You can create a function app right from Visual Studio.</span></span>

[!INCLUDE [Publish hello project tooAzure](../../includes/functions-vstools-publish.md)]

## <a name="test-your-function-in-azure"></a><span data-ttu-id="9fee5-147">Tester votre fonction dans Azure</span><span class="sxs-lookup"><span data-stu-id="9fee5-147">Test your function in Azure</span></span>

1. <span data-ttu-id="9fee5-148">URL de base hello copie de l’application de fonction hello à partir de la page de profil de publication hello.</span><span class="sxs-lookup"><span data-stu-id="9fee5-148">Copy hello base URL of hello function app from hello Publish profile page.</span></span> <span data-ttu-id="9fee5-149">Remplacez hello `localhost:port` partie de l’URL de hello utilisée lors du test de fonction hello localement avec la nouvelle URL de base hello.</span><span class="sxs-lookup"><span data-stu-id="9fee5-149">Replace hello `localhost:port` portion of hello URL you used when testing hello function locally with hello new base URL.</span></span> <span data-ttu-id="9fee5-150">Comme précédemment, vérifiez que chaîne de requête hello tooappend `&name=<yourname>` toothis URL et l’exécution de la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="9fee5-150">As before, make sure tooappend hello query string `&name=<yourname>` toothis URL and execute hello request.</span></span>

    <span data-ttu-id="9fee5-151">URL de Hello qui appelle votre HTTP déclenchée présente de fonction comme suit :</span><span class="sxs-lookup"><span data-stu-id="9fee5-151">hello URL that calls your HTTP triggered function looks like this:</span></span>

        http://<functionappname>.azurewebsites.net/api/<functionname>?name=<yourname> 

2. <span data-ttu-id="9fee5-152">Collez cette nouvelle URL de demande de hello HTTP dans la barre d’adresse de votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="9fee5-152">Paste this new URL for hello HTTP request into your browser's address bar.</span></span> <span data-ttu-id="9fee5-153">les Voici Hello réponse de hello dans hello navigateur toohello à distance une demande GET retourné par la fonction hello :</span><span class="sxs-lookup"><span data-stu-id="9fee5-153">hello following shows hello response in hello browser toohello remote GET request returned by hello function:</span></span> 

    ![Réponse de fonction dans le navigateur de hello](./media/functions-create-your-first-function-visual-studio/functions-test-remote-browser.png)
 
## <a name="next-steps"></a><span data-ttu-id="9fee5-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9fee5-155">Next steps</span></span>

<span data-ttu-id="9fee5-156">Vous avez utilisé l’application de fonction toocreate C# de Visual Studio avec une fonction HTTP déclenchée simple.</span><span class="sxs-lookup"><span data-stu-id="9fee5-156">You have used Visual Studio toocreate a C# function app with a simple HTTP triggered function.</span></span> 

+ <span data-ttu-id="9fee5-157">toolearn comment tooconfigure toosupport de votre projet autres types de déclencheurs et les liaisons, consultez hello [projet hello de configurer pour le développement local](functions-develop-vs.md#configure-the-project-for-local-development) section [Azure fonctions Tools pour Visual Studio](functions-develop-vs.md).</span><span class="sxs-lookup"><span data-stu-id="9fee5-157">toolearn how tooconfigure your project toosupport other types of triggers and bindings, see hello [Configure hello project for local development](functions-develop-vs.md#configure-the-project-for-local-development) section in [Azure Functions Tools for Visual Studio](functions-develop-vs.md).</span></span>
+ <span data-ttu-id="9fee5-158">toolearn en savoir plus sur le test local et de débogage à l’aide des outils de base Azure fonctions hello, consultez [Code et test, les fonctions Azure localement](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="9fee5-158">toolearn more about local testing and debugging using hello Azure Functions Core Tools, see [Code and test Azure Functions locally](functions-run-local.md).</span></span> 
+ <span data-ttu-id="9fee5-159">toolearn plus sur le développement des fonctions en tant que bibliothèques de classes .NET, consultez [des bibliothèques de classes à l’aide de .NET avec des fonctions d’Azure](functions-dotnet-class-library.md).</span><span class="sxs-lookup"><span data-stu-id="9fee5-159">toolearn more about developing functions as .NET class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span> 

