---
title: aaaHow toouse SendGrid dans les fonctions de Azure | Documents Microsoft
description: "Montre comment toouse SendGrid dans les fonctions d’Azure"
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
ms.openlocfilehash: a0ffdae04e5924c773d2d26427626fc1f570f7ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-sendgrid-in-azure-functions"></a><span data-ttu-id="2876f-103">Comment toouse SendGrid dans les fonctions d’Azure</span><span class="sxs-lookup"><span data-stu-id="2876f-103">How toouse SendGrid in Azure Functions</span></span>

## <a name="sendgrid-overview"></a><span data-ttu-id="2876f-104">Présentation de SendGrid</span><span class="sxs-lookup"><span data-stu-id="2876f-104">SendGrid Overview</span></span>

<span data-ttu-id="2876f-105">Prend en charge des fonctions Azure SendGrid sortie liaisons tooenable vos messages de messagerie fonctions toosend avec quelques lignes de code et un compte SendGrid.</span><span class="sxs-lookup"><span data-stu-id="2876f-105">Azure Functions supports SendGrid output bindings tooenable your functions toosend email messages with a few lines of code and a SendGrid account.</span></span>

<span data-ttu-id="2876f-106">toouse hello des API SendGrid dans une fonction d’Azure, vous devez avoir un [compte SendGrid](http://SendGrid.com).</span><span class="sxs-lookup"><span data-stu-id="2876f-106">toouse hello SendGrid API in an Azure Function, you must have a [SendGrid account](http://SendGrid.com).</span></span> <span data-ttu-id="2876f-107">En outre, vous devez disposer d’une clé d’API SendGrid.</span><span class="sxs-lookup"><span data-stu-id="2876f-107">Additionally, you must have a SendGrid API Key.</span></span> <span data-ttu-id="2876f-108">Connectez-vous à tooyour compte SendGrid, puis cliquez sur **paramètres** puis **clé API** toogenerate une API clé.</span><span class="sxs-lookup"><span data-stu-id="2876f-108">Log in tooyour SendGrid account and click **Settings** then **API Key** toogenerate an API key.</span></span> <span data-ttu-id="2876f-109">Gardez cette clé sous la main, car vous l’utiliserez dans une étape à venir.</span><span class="sxs-lookup"><span data-stu-id="2876f-109">Keep this key available as you use it in an upcoming step.</span></span>

<span data-ttu-id="2876f-110">Vous êtes maintenant prêt toocreate une application de la fonction d’Azure.</span><span class="sxs-lookup"><span data-stu-id="2876f-110">You are now ready toocreate an Azure Function app.</span></span>

## <a name="create-an-azure-function-app"></a><span data-ttu-id="2876f-111">Création d’une application Azure Function</span><span class="sxs-lookup"><span data-stu-id="2876f-111">Create an Azure Function app</span></span> 

<span data-ttu-id="2876f-112">Les applications Azure Function sont des conteneurs pour une ou plusieurs fonctions Azure.</span><span class="sxs-lookup"><span data-stu-id="2876f-112">Azure Function Apps are containers for one or more Azure functions.</span></span> <span data-ttu-id="2876f-113">Les fonctions Azure sont exactement cela : des fonctions.</span><span class="sxs-lookup"><span data-stu-id="2876f-113">Azure functions are just that - a function.</span></span> <span data-ttu-id="2876f-114">Chaque fonction Azure est liée tooone déclencheur, qui est un événement qui provoque hello fonction toorun.</span><span class="sxs-lookup"><span data-stu-id="2876f-114">Each Azure function is tied tooone trigger, which is an event that causes hello function toorun.</span></span>
<span data-ttu-id="2876f-115">Chaque fonction peut contenir un nombre quelconque de liaisons d’entrée ou de sortie.</span><span class="sxs-lookup"><span data-stu-id="2876f-115">Each function can contain any number of input or output bindings.</span></span> <span data-ttu-id="2876f-116">Les liaisons sont des services que vous pouvez utiliser dans une fonction.</span><span class="sxs-lookup"><span data-stu-id="2876f-116">Bindings are services that you can use in a function.</span></span> <span data-ttu-id="2876f-117">SendGrid est une sortie liaison vous pouvez utiliser toosend e-mail.</span><span class="sxs-lookup"><span data-stu-id="2876f-117">SendGrid is an output binding you can use toosend email.</span></span> 

1. <span data-ttu-id="2876f-118">Connectez-vous à toohello portail Azure et [créer une application de la fonction Azure](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) ou ouvrir une application existante de la fonction.</span><span class="sxs-lookup"><span data-stu-id="2876f-118">Log in toohello Azure portal and [create an Azure Function App](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) or open an existing Function app.</span></span> 
2. <span data-ttu-id="2876f-119">Créez une fonction Azure.</span><span class="sxs-lookup"><span data-stu-id="2876f-119">Create an Azure function.</span></span> <span data-ttu-id="2876f-120">tookeep il simple, choisissez un déclencheur manuel et c#.</span><span class="sxs-lookup"><span data-stu-id="2876f-120">tookeep it simple, choose a manual trigger and C#.</span></span> 

 ![Création d’une fonction Azure](./media/functions-how-to-use-sendgrid/functions-new-function-manual-trigger-page.png)

## <a name="configure-sendgrid-for-use-in-an-azure-function-app"></a><span data-ttu-id="2876f-122">Configuration de SendGrid pour une utilisation dans une application Azure Function</span><span class="sxs-lookup"><span data-stu-id="2876f-122">Configure SendGrid for use in an Azure Function app</span></span>

<span data-ttu-id="2876f-123">Vous devez stocker votre clé d’API SendGrid comme un toouse de paramètre d’application dans une fonction.</span><span class="sxs-lookup"><span data-stu-id="2876f-123">You must store your SendGrid API Key as an app setting toouse it in a function.</span></span> <span data-ttu-id="2876f-124">champ de ApiKey Hello n’est pas votre clé API SendGrid réel, mais une application de paramètre, vous définissez et qui représente votre clé API réel.</span><span class="sxs-lookup"><span data-stu-id="2876f-124">hello ApiKey field is not your actual SendGrid API key, but an app setting you define that represents your actual API key.</span></span> <span data-ttu-id="2876f-125">Votre clé est stockée de cette façon à des fins de sécurité, car elle est séparée de tout code et tous fichiers qui peuvent être consultés avec le contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="2876f-125">Storing your key this way is for security, since it is separate from any code or files that might be checked into source code control.</span></span>

- <span data-ttu-id="2876f-126">Créez une clé **AppSettings** dans les **Paramètres de l’application** de votre application de fonction.</span><span class="sxs-lookup"><span data-stu-id="2876f-126">Create an **AppSettings** key in your function app's **Application Settings**.</span></span>

 ![Création d’une fonction Azure](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-api-key-app-settings.png)

## <a name="configure-sendgrid-output-bindings"></a><span data-ttu-id="2876f-128">Configuration des liaisons de sortie SendGrid</span><span class="sxs-lookup"><span data-stu-id="2876f-128">Configure SendGrid output bindings</span></span>

<span data-ttu-id="2876f-129">SendGrid est disponible en tant que liaison de sortie de fonction Azure.</span><span class="sxs-lookup"><span data-stu-id="2876f-129">SendGrid is available as an Azure function output binding.</span></span> <span data-ttu-id="2876f-130">liaison de sortie toocreate un SendGrid :</span><span class="sxs-lookup"><span data-stu-id="2876f-130">toocreate a SendGrid output binding:</span></span>

1. <span data-ttu-id="2876f-131">Accédez toohello **intégrer** onglet de la fonction hello Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2876f-131">Go toohello **Integrate** tab of hello function in hello Azure portal.</span></span>
2. <span data-ttu-id="2876f-132">Cliquez sur **nouvelle sortie** toocreate un SendGrid liaison de sortie.</span><span class="sxs-lookup"><span data-stu-id="2876f-132">Click **New Output** toocreate a SendGrid output binding.</span></span>
3. <span data-ttu-id="2876f-133">Renseignez hello **clé API** et **nom de paramètre de Message** propriétés.</span><span class="sxs-lookup"><span data-stu-id="2876f-133">Fill in hello **API Key** and **Message parameter name** properties.</span></span> <span data-ttu-id="2876f-134">Si vous le souhaitez, vous pouvez entrer hello maintenant les autres propriétés, ou à la place de leur code.</span><span class="sxs-lookup"><span data-stu-id="2876f-134">If you want, you can enter hello other properties now, or code them instead.</span></span> <span data-ttu-id="2876f-135">Ces paramètres peuvent être utilisés comme valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="2876f-135">These settings can be used as defaults.</span></span>

 ![Configuration des liaisons de sortie SendGrid](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-output-bindings.png)

<span data-ttu-id="2876f-137">Ajout d’une fonction de tooa liaison crée un fichier appelé **function.json** dans le dossier de votre fonction.</span><span class="sxs-lookup"><span data-stu-id="2876f-137">Adding a binding tooa function creates a file called **function.json** in your function's folder.</span></span> <span data-ttu-id="2876f-138">Ce fichier contient tous les hello les mêmes informations que vous voyez dans hello la fonction Azure **intégrer** onglet, mais dans Json de format.</span><span class="sxs-lookup"><span data-stu-id="2876f-138">This file contains all hello same information that you see in hello Azure function's **Integrate** tab, but in Json format.</span></span> <span data-ttu-id="2876f-139">Hello du paramètre **ApiKey**, **message**, et **de** champs créent hello suivant entrées Bonjour **function.json** fichier :</span><span class="sxs-lookup"><span data-stu-id="2876f-139">Setting hello **ApiKey**, **message**, and **from** fields create hello following entries in hello **function.json** file:</span></span> 

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

<span data-ttu-id="2876f-140">Si vous préférez, vous pouvez modifier ce fichier vous-même directement.</span><span class="sxs-lookup"><span data-stu-id="2876f-140">If you prefer, you may modify this file yourself directly.</span></span>

<span data-ttu-id="2876f-141">Maintenant que vous avez créé et configuré les hello application de la fonction et la fonction, vous pouvez écrire un message électronique toosend de code hello.</span><span class="sxs-lookup"><span data-stu-id="2876f-141">Now that you have created and configured hello Function App and function, you can write hello code toosend an email.</span></span>

## <a name="write-code-that-creates-and-sends-email"></a><span data-ttu-id="2876f-142">Écriture du code qui crée et envoie un message électronique</span><span class="sxs-lookup"><span data-stu-id="2876f-142">Write code that creates and sends email</span></span>

<span data-ttu-id="2876f-143">Hello API SendGrid contient toutes les commandes de hello vous devez toocreate et envoyez un courrier électronique.</span><span class="sxs-lookup"><span data-stu-id="2876f-143">hello SendGrid API contains all hello commands you need toocreate and send an email.</span></span>  

- <span data-ttu-id="2876f-144">Remplacez le code hello fonction hello avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="2876f-144">Replace hello code in hello function with hello following code:</span></span>

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
    // change tooemail of recipient
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

<span data-ttu-id="2876f-145">Avis hello première ligne contient hello ```#r``` directive qui référence l’assembly SendGrid de hello.</span><span class="sxs-lookup"><span data-stu-id="2876f-145">Notice hello first line contains hello ```#r``` directive that references hello SendGrid assembly.</span></span> <span data-ttu-id="2876f-146">Après cela, vous pouvez utiliser un ```using``` instruction toomore accéder facilement aux objets hello dans cet espace de noms.</span><span class="sxs-lookup"><span data-stu-id="2876f-146">After that, you can use a ```using``` statement toomore easily access hello objects in that namespace.</span></span> <span data-ttu-id="2876f-147">Dans le code hello, créer des instances de ```Mail```, ```Personalization```, et ```Content``` objets hello API SendGrid à partir de rédiger un message électronique de hello.</span><span class="sxs-lookup"><span data-stu-id="2876f-147">In hello code, create instances of ```Mail```, ```Personalization```, and ```Content``` objects from hello SendGrid API that compose hello email.</span></span> <span data-ttu-id="2876f-148">Lorsque vous renvoyez le message de type hello, SendGrid effectue sa remise.</span><span class="sxs-lookup"><span data-stu-id="2876f-148">When you return hello message, SendGrid delivers it.</span></span> 

<span data-ttu-id="2876f-149">Hello signature de la fonction contient également un supplémentaire, le paramètre de type out ```Mail``` nommé ```message```.</span><span class="sxs-lookup"><span data-stu-id="2876f-149">hello function's signature also contains an extra out parameter of type ```Mail``` named ```message```.</span></span> <span data-ttu-id="2876f-150">Les liaisons d’entrée et de sortie s’expriment elles-mêmes en tant que paramètres de fonction dans le code.</span><span class="sxs-lookup"><span data-stu-id="2876f-150">Both input and output bindings express themselves as function parameters in code.</span></span> 

2. <span data-ttu-id="2876f-151">Testez votre code en cliquant sur **Test** et en entrant un message en hello **corps de la demande** champ, puis en cliquant sur hello **exécuter** bouton.</span><span class="sxs-lookup"><span data-stu-id="2876f-151">Test your code by clicking **Test** and entering a message into hello **Request body** field, then clicking hello **Run** button.</span></span>

 ![Test de votre code](./media/functions-how-to-use-sendgrid/functions-develop-test-sendgrid.png)

3. <span data-ttu-id="2876f-153">Vérifiez tooverify par courrier électronique que SendGrid envoyées par courrier électronique hello.</span><span class="sxs-lookup"><span data-stu-id="2876f-153">Check email tooverify that SendGrid sent hello email.</span></span> <span data-ttu-id="2876f-154">Il doit atteindre l’adresse toohello dans le code hello à l’étape 1 et contient le message de type hello de hello **corps de la demande**.</span><span class="sxs-lookup"><span data-stu-id="2876f-154">It should go toohello address in hello code from step 1, and contain hello message from hello **Request body**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2876f-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2876f-155">Next steps</span></span>
<span data-ttu-id="2876f-156">Cet article a montré comment toouse hello SendGrid service toocreate et envoyer un courrier électronique.</span><span class="sxs-lookup"><span data-stu-id="2876f-156">This article has demonstrated how toouse hello SendGrid service toocreate and send email.</span></span> <span data-ttu-id="2876f-157">toolearn savoir plus sur l’utilisation de fonctions de Azure dans vos applications, consultez hello rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="2876f-157">toolearn more about using Azure Functions in your apps, see hello following topics:</span></span> 

- <span data-ttu-id="2876f-158">[Meilleures pratiques pour les fonctions Azure](functions-best-practices.md) répertorie certains meilleures toouse de pratiques lors de la création de fonctions d’Azure.</span><span class="sxs-lookup"><span data-stu-id="2876f-158">[Best practices for Azure Functions](functions-best-practices.md) Lists some best practices toouse when creating Azure Functions.</span></span>

- <span data-ttu-id="2876f-159">[Référence du développeur Azure Functions](functions-reference.md) Référence du programmeur pour le codage de fonctions et la définition de déclencheurs et de liaisons.</span><span class="sxs-lookup"><span data-stu-id="2876f-159">[Azure Functions developer reference](functions-reference.md) Programmer reference for coding functions and defining triggers and bindings.</span></span>

- <span data-ttu-id="2876f-160">Le didacticiel [Test d’Azure Functions](functions-test-a-function.md) décrit plusieurs outils et techniques permettant de tester vos fonctions.</span><span class="sxs-lookup"><span data-stu-id="2876f-160">[Testing Azure Functions](functions-test-a-function.md) Describes various tools and techniques for testing your functions.</span></span>