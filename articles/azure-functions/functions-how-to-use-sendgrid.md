---
title: "Guide d’utilisation de SendGrid dans Azure Functions | Microsoft Docs"
description: "Cet article décrit l’utilisation de SendGrid dans Azure Functions"
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 01/31/2017
ms.author: rachelap
ms.openlocfilehash: 05c9f4e4a4351219da68af8b702c25f21d7d4d02
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-sendgrid-in-azure-functions"></a><span data-ttu-id="d25ae-103">Guide d’utilisation de SendGrid dans Azure Functions</span><span class="sxs-lookup"><span data-stu-id="d25ae-103">How to use SendGrid in Azure Functions</span></span>

## <a name="sendgrid-overview"></a><span data-ttu-id="d25ae-104">Présentation de SendGrid</span><span class="sxs-lookup"><span data-stu-id="d25ae-104">SendGrid Overview</span></span>

<span data-ttu-id="d25ae-105">Azure Functions prend en charge les liaisons de SendGrid, afin de permettre à vos fonctions d’envoyer des messages électroniques avec quelques lignes de codes et un compte SendGrid.</span><span class="sxs-lookup"><span data-stu-id="d25ae-105">Azure Functions supports SendGrid output bindings to enable your functions to send email messages with a few lines of code and a SendGrid account.</span></span>

<span data-ttu-id="d25ae-106">Pour utiliser l’API SendGrid dans une fonction d’Azure, vous devez avoir un [compte SendGrid](http://SendGrid.com).</span><span class="sxs-lookup"><span data-stu-id="d25ae-106">To use the SendGrid API in an Azure Function, you must have a [SendGrid account](http://SendGrid.com).</span></span> <span data-ttu-id="d25ae-107">En outre, vous devez disposer d’une clé d’API SendGrid.</span><span class="sxs-lookup"><span data-stu-id="d25ae-107">Additionally, you must have a SendGrid API Key.</span></span> <span data-ttu-id="d25ae-108">Connectez-vous à votre compte SendGrid et cliquez sur **Paramètres** puis **Clé API** pour générer une clé API.</span><span class="sxs-lookup"><span data-stu-id="d25ae-108">Log in to your SendGrid account and click **Settings** then **API Key** to generate an API key.</span></span> <span data-ttu-id="d25ae-109">Gardez cette clé sous la main, car vous l’utiliserez dans une étape à venir.</span><span class="sxs-lookup"><span data-stu-id="d25ae-109">Keep this key available as you use it in an upcoming step.</span></span>

<span data-ttu-id="d25ae-110">Vous êtes maintenant prêt à créer une application Azure Function.</span><span class="sxs-lookup"><span data-stu-id="d25ae-110">You are now ready to create an Azure Function app.</span></span>

## <a name="create-an-azure-function-app"></a><span data-ttu-id="d25ae-111">Création d’une application Azure Function</span><span class="sxs-lookup"><span data-stu-id="d25ae-111">Create an Azure Function app</span></span> 

<span data-ttu-id="d25ae-112">Les applications Azure Function sont des conteneurs pour une ou plusieurs fonctions Azure.</span><span class="sxs-lookup"><span data-stu-id="d25ae-112">Azure Function Apps are containers for one or more Azure functions.</span></span> <span data-ttu-id="d25ae-113">Les fonctions Azure sont exactement cela : des fonctions.</span><span class="sxs-lookup"><span data-stu-id="d25ae-113">Azure functions are just that - a function.</span></span> <span data-ttu-id="d25ae-114">Chaque fonction Azure est liée à un déclencheur, qui est un événement qui lance la fonction.</span><span class="sxs-lookup"><span data-stu-id="d25ae-114">Each Azure function is tied to one trigger, which is an event that causes the function to run.</span></span>
<span data-ttu-id="d25ae-115">Chaque fonction peut contenir un nombre quelconque de liaisons d’entrée ou de sortie.</span><span class="sxs-lookup"><span data-stu-id="d25ae-115">Each function can contain any number of input or output bindings.</span></span> <span data-ttu-id="d25ae-116">Les liaisons sont des services que vous pouvez utiliser dans une fonction.</span><span class="sxs-lookup"><span data-stu-id="d25ae-116">Bindings are services that you can use in a function.</span></span> <span data-ttu-id="d25ae-117">SendGrid est une liaison de sortie que vous pouvez utiliser pour envoyer des messages électroniques.</span><span class="sxs-lookup"><span data-stu-id="d25ae-117">SendGrid is an output binding you can use to send email.</span></span> 

1. <span data-ttu-id="d25ae-118">Connectez-vous au portail Azure et [créez une Azure Function App](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) ou ouvrez-en une existante.</span><span class="sxs-lookup"><span data-stu-id="d25ae-118">Log in to the Azure portal and [create an Azure Function App](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) or open an existing Function app.</span></span> 
2. <span data-ttu-id="d25ae-119">Créez une fonction Azure.</span><span class="sxs-lookup"><span data-stu-id="d25ae-119">Create an Azure function.</span></span> <span data-ttu-id="d25ae-120">Pour faire simple, choisissez un déclencheur manuel et C#.</span><span class="sxs-lookup"><span data-stu-id="d25ae-120">To keep it simple, choose a manual trigger and C#.</span></span> 

 ![Création d’une fonction Azure](./media/functions-how-to-use-sendgrid/functions-new-function-manual-trigger-page.png)

## <a name="configure-sendgrid-for-use-in-an-azure-function-app"></a><span data-ttu-id="d25ae-122">Configuration de SendGrid pour une utilisation dans une application Azure Function</span><span class="sxs-lookup"><span data-stu-id="d25ae-122">Configure SendGrid for use in an Azure Function app</span></span>

<span data-ttu-id="d25ae-123">Vous devez stocker votre clé d’API SendGrid comme paramètre d’application pour l’utiliser dans une fonction.</span><span class="sxs-lookup"><span data-stu-id="d25ae-123">You must store your SendGrid API Key as an app setting to use it in a function.</span></span> <span data-ttu-id="d25ae-124">Le champ ApiKey n’est pas votre clé d’API SendGrid réelle, mais un paramètre d’application que vous définissez et qui représente votre clé d’API réelle.</span><span class="sxs-lookup"><span data-stu-id="d25ae-124">The ApiKey field is not your actual SendGrid API key, but an app setting you define that represents your actual API key.</span></span> <span data-ttu-id="d25ae-125">Votre clé est stockée de cette façon à des fins de sécurité, car elle est séparée de tout code et tous fichiers qui peuvent être consultés avec le contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="d25ae-125">Storing your key this way is for security, since it is separate from any code or files that might be checked into source code control.</span></span>

- <span data-ttu-id="d25ae-126">Créez une clé **AppSettings** dans les **Paramètres de l’application** de votre application de fonction.</span><span class="sxs-lookup"><span data-stu-id="d25ae-126">Create an **AppSettings** key in your function app's **Application Settings**.</span></span>

 ![Création d’une fonction Azure](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-api-key-app-settings.png)

## <a name="configure-sendgrid-output-bindings"></a><span data-ttu-id="d25ae-128">Configuration des liaisons de sortie SendGrid</span><span class="sxs-lookup"><span data-stu-id="d25ae-128">Configure SendGrid output bindings</span></span>

<span data-ttu-id="d25ae-129">SendGrid est disponible en tant que liaison de sortie de fonction Azure.</span><span class="sxs-lookup"><span data-stu-id="d25ae-129">SendGrid is available as an Azure function output binding.</span></span> <span data-ttu-id="d25ae-130">Pour créer une liaison de sortie SendGrid :</span><span class="sxs-lookup"><span data-stu-id="d25ae-130">To create a SendGrid output binding:</span></span>

1. <span data-ttu-id="d25ae-131">Accédez à l’onglet **Intégrer** de la fonction dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d25ae-131">Go to the **Integrate** tab of the function in the Azure portal.</span></span>
2. <span data-ttu-id="d25ae-132">Cliquez sur **Nouvelle sortie** pour créer une liaison de sortie SendGrid.</span><span class="sxs-lookup"><span data-stu-id="d25ae-132">Click **New Output** to create a SendGrid output binding.</span></span>
3. <span data-ttu-id="d25ae-133">Renseignez les propriétés **Clé API** et **Nom du paramètre de message**.</span><span class="sxs-lookup"><span data-stu-id="d25ae-133">Fill in the **API Key** and **Message parameter name** properties.</span></span> <span data-ttu-id="d25ae-134">Si vous le souhaitez, vous pouvez entrer d’autres propriétés maintenant, ou les coder à la place.</span><span class="sxs-lookup"><span data-stu-id="d25ae-134">If you want, you can enter the other properties now, or code them instead.</span></span> <span data-ttu-id="d25ae-135">Ces paramètres peuvent être utilisés comme valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="d25ae-135">These settings can be used as defaults.</span></span>

 ![Configuration des liaisons de sortie SendGrid](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-output-bindings.png)

<span data-ttu-id="d25ae-137">L’ajout d’une liaison à une fonction crée un fichier appelé **function.json** dans le dossier de votre fonction.</span><span class="sxs-lookup"><span data-stu-id="d25ae-137">Adding a binding to a function creates a file called **function.json** in your function's folder.</span></span> <span data-ttu-id="d25ae-138">Ce fichier contient les mêmes informations que celles que vous voyez dans l’onglet **Intégrer** de la fonction Azure, mais au format Json.</span><span class="sxs-lookup"><span data-stu-id="d25ae-138">This file contains all the same information that you see in the Azure function's **Integrate** tab, but in Json format.</span></span> <span data-ttu-id="d25ae-139">Le réglage des champs **clé API**, **message**, et **de** crée les entrées suivantes dans le fichier **function.json** :</span><span class="sxs-lookup"><span data-stu-id="d25ae-139">Setting the **ApiKey**, **message**, and **from** fields create the following entries in the **function.json** file:</span></span> 

```json
{
  "bindings": [    
    {
      "type": "sendGrid",
      "name": "message",
      "apiKey": "SendGridKey",
      "direction": "out",
      "from": "azure@contoso.com"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="d25ae-140">Si vous préférez, vous pouvez modifier ce fichier vous-même directement.</span><span class="sxs-lookup"><span data-stu-id="d25ae-140">If you prefer, you may modify this file yourself directly.</span></span>

<span data-ttu-id="d25ae-141">Maintenant que vous avez créé et configuré Function App et la fonction, vous pouvez écrire le code pour envoyer un message électronique.</span><span class="sxs-lookup"><span data-stu-id="d25ae-141">Now that you have created and configured the Function App and function, you can write the code to send an email.</span></span>

## <a name="write-code-that-creates-and-sends-email"></a><span data-ttu-id="d25ae-142">Écriture du code qui crée et envoie un message électronique</span><span class="sxs-lookup"><span data-stu-id="d25ae-142">Write code that creates and sends email</span></span>

<span data-ttu-id="d25ae-143">L’API SendGrid contient toutes les commandes dont vous avez besoin pour créer et envoyer un message électronique.</span><span class="sxs-lookup"><span data-stu-id="d25ae-143">The SendGrid API contains all the commands you need to create and send an email.</span></span>  

- <span data-ttu-id="d25ae-144">Remplacez le code dans la fonction par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="d25ae-144">Replace the code in the function with the following code:</span></span>

```cs
#r "SendGrid"
using System;
using SendGrid.Helpers.Mail;

public static void Run(TraceWriter log, string input, out Mail message)
{
    message = new Mail
    {        
        Subject = "Azure news"          
    };

    var personalization = new Personalization();
    // change to email of recipient
    personalization.AddTo(new Email("MoreEmailPlease@contoso.com"));   

    Content content = new Content
    {
        Type = "text/plain",
        Value = input
    };
    message.AddContent(content);
    message.AddPersonalization(personalization);
}
```

<span data-ttu-id="d25ae-145">Notez que la première ligne contient la directive ```#r``` qui fait référence à l’assembly SendGrid.</span><span class="sxs-lookup"><span data-stu-id="d25ae-145">Notice the first line contains the ```#r``` directive that references the SendGrid assembly.</span></span> <span data-ttu-id="d25ae-146">Après cela, vous pouvez utiliser une instruction ```using``` pour accéder plus facilement aux objets dans cet espace de noms.</span><span class="sxs-lookup"><span data-stu-id="d25ae-146">After that, you can use a ```using``` statement to more easily access the objects in that namespace.</span></span> <span data-ttu-id="d25ae-147">Dans le code, créez des instances des objets ```Mail```, ```Personalization``` et ```Content``` qui composent le message électronique à partir de l’API SendGrid.</span><span class="sxs-lookup"><span data-stu-id="d25ae-147">In the code, create instances of ```Mail```, ```Personalization```, and ```Content``` objects from the SendGrid API that compose the email.</span></span> <span data-ttu-id="d25ae-148">Lorsque vous renvoyez le message, SendGrid le livre.</span><span class="sxs-lookup"><span data-stu-id="d25ae-148">When you return the message, SendGrid delivers it.</span></span> 

<span data-ttu-id="d25ae-149">La signature de la fonction contient également un paramètre de sortie supplémentaire de type ```Mail``` nommé ```message```.</span><span class="sxs-lookup"><span data-stu-id="d25ae-149">The function's signature also contains an extra out parameter of type ```Mail``` named ```message```.</span></span> <span data-ttu-id="d25ae-150">Les liaisons d’entrée et de sortie s’expriment elles-mêmes en tant que paramètres de fonction dans le code.</span><span class="sxs-lookup"><span data-stu-id="d25ae-150">Both input and output bindings express themselves as function parameters in code.</span></span> 

2. <span data-ttu-id="d25ae-151">Testez votre code en cliquant sur **Test** et en entrant un message dans le champ **Corps de la requête**, puis en cliquant sur le bouton **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="d25ae-151">Test your code by clicking **Test** and entering a message into the **Request body** field, then clicking the **Run** button.</span></span>

 ![Test de votre code](./media/functions-how-to-use-sendgrid/functions-develop-test-sendgrid.png)

3. <span data-ttu-id="d25ae-153">Consultez votre messagerie électronique pour vérifier que SendGrid a envoyé le message électronique.</span><span class="sxs-lookup"><span data-stu-id="d25ae-153">Check email to verify that SendGrid sent the email.</span></span> <span data-ttu-id="d25ae-154">Il devrait être livré à l’adresse dans le code de l’étape 1 et contenir le message du **Corps de la requête**.</span><span class="sxs-lookup"><span data-stu-id="d25ae-154">It should go to the address in the code from step 1, and contain the message from the **Request body**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d25ae-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d25ae-155">Next steps</span></span>
<span data-ttu-id="d25ae-156">Cet article a montré comment utiliser le service SendGrid pour créer et envoyer du courrier électronique.</span><span class="sxs-lookup"><span data-stu-id="d25ae-156">This article has demonstrated how to use the SendGrid service to create and send email.</span></span> <span data-ttu-id="d25ae-157">Pour plus d’informations sur l’utilisation d’Azure Functions dans vos applications, consultez les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="d25ae-157">To learn more about using Azure Functions in your apps, see the following topics:</span></span> 

- <span data-ttu-id="d25ae-158">[Meilleures pratiques pour Azure Functions](functions-best-practices.md) répertorie les meilleures pratiques à utiliser lors de la création de fonctions d’Azure.</span><span class="sxs-lookup"><span data-stu-id="d25ae-158">[Best practices for Azure Functions](functions-best-practices.md) Lists some best practices to use when creating Azure Functions.</span></span>

- <span data-ttu-id="d25ae-159">[Référence du développeur Azure Functions](functions-reference.md) Référence du programmeur pour le codage de fonctions et la définition de déclencheurs et de liaisons.</span><span class="sxs-lookup"><span data-stu-id="d25ae-159">[Azure Functions developer reference](functions-reference.md) Programmer reference for coding functions and defining triggers and bindings.</span></span>

- <span data-ttu-id="d25ae-160">Le didacticiel [Test d’Azure Functions](functions-test-a-function.md) décrit plusieurs outils et techniques permettant de tester vos fonctions.</span><span class="sxs-lookup"><span data-stu-id="d25ae-160">[Testing Azure Functions](functions-test-a-function.md) Describes various tools and techniques for testing your functions.</span></span>