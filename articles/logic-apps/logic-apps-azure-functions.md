---
title: "Code personnalisé pour Azure Logic Apps avec Azure Functions | Microsoft Docs"
description: "Création et exécution d’un code personnalisé pour Azure Logic Apps avec Azure Functions"
services: logic-apps,functions
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 18442c87b049200fac5ed41cc7034ba7a848b8d3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="add-and-run-custom-code-for-logic-apps-through-azure-functions"></a><span data-ttu-id="d3062-103">Ajout et exécution d’un code personnalisé pour des applications logiques avec Azure Functions</span><span class="sxs-lookup"><span data-stu-id="d3062-103">Add and run custom code for logic apps through Azure Functions</span></span>

<span data-ttu-id="d3062-104">Pour exécuter des extraits de code personnalisés de C# ou node.js dans des applications logiques, vous pouvez créer des fonctions personnalisées par le biais d’Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="d3062-104">To run custom snippets of C# or node.js in logic apps, you can create custom functions through Azure Functions.</span></span> 
<span data-ttu-id="d3062-105">[Azure Functions](../azure-functions/functions-overview.md) assure le calcul sans serveur dans Microsoft Azure, et est utile pour effectuer ces tâches :</span><span class="sxs-lookup"><span data-stu-id="d3062-105">[Azure Functions](../azure-functions/functions-overview.md) offers server-free computing in Microsoft Azure and are useful for performing these tasks:</span></span>

* <span data-ttu-id="d3062-106">Mise en forme avancée ou calcul de champs dans les applications logiques</span><span class="sxs-lookup"><span data-stu-id="d3062-106">Advanced formatting or compute of fields in logic apps</span></span>
* <span data-ttu-id="d3062-107">Effectuez les calculs dans un workflow.</span><span class="sxs-lookup"><span data-stu-id="d3062-107">Perform calculations in a workflow.</span></span>
* <span data-ttu-id="d3062-108">Extension des fonctionnalités des applications logiques avec des fonctions prises en charge dans C# ou node.js</span><span class="sxs-lookup"><span data-stu-id="d3062-108">Extend the logic app functionality with functions that are supported in C# or node.js</span></span>

## <a name="create-custom-functions-for-your-logic-apps"></a><span data-ttu-id="d3062-109">Création de fonctions personnalisées pour vos applications logiques</span><span class="sxs-lookup"><span data-stu-id="d3062-109">Create custom functions for your logic apps</span></span>

<span data-ttu-id="d3062-110">Nous vous recommandons de créer une fonction dans le portail Azure Functions à partir des modèles **Generic Webhook - Node (Webhook générique - Nœud)** ou **Generic Webhook - C# (Webhook générique - C#)**.</span><span class="sxs-lookup"><span data-stu-id="d3062-110">We recommend that you create a function in the Azure Functions portal, from the **Generic Webhook - Node** or **Generic Webhook - C#** templates.</span></span> <span data-ttu-id="d3062-111">Ce résultat crée automatiquement un modèle qui accepte `application/json` à partir d’une application logique.</span><span class="sxs-lookup"><span data-stu-id="d3062-111">The result creates an auto-populated a template that accepts `application/json` from a logic app.</span></span> <span data-ttu-id="d3062-112">Les fonctions que vous créez à partir de ces modèles sont automatiquement détectées et s’affichent dans le concepteur d’applications logiques sous **Azure Functions in my region**</span><span class="sxs-lookup"><span data-stu-id="d3062-112">Functions that you create from these templates are automatically detected and appear in the Logic App Designer under **Azure Functions in my region.**</span></span>

<span data-ttu-id="d3062-113">Dans le portail Azure, dans le volet **Intégrer** de votre fonction, votre modèle doit montrer que **Mode** a la valeur **Webhook** et que **Type de webhook** est défini sur **JSON générique**.</span><span class="sxs-lookup"><span data-stu-id="d3062-113">In the Azure portal, on the **Integrate** pane for your function, your template should show that **Mode** set to **Webhook** and **Webhook type** is set to **Generic JSON**.</span></span> 

<span data-ttu-id="d3062-114">Les fonctions de webhook acceptent une demande et la passent à la méthode par le biais d’une variable `data` .</span><span class="sxs-lookup"><span data-stu-id="d3062-114">Webhook functions accept a request and pass it into the method via a `data` variable.</span></span> <span data-ttu-id="d3062-115">Vous pouvez accéder aux propriétés de votre charge utile à l’aide d’une notation par points telle que `data.function-name`.</span><span class="sxs-lookup"><span data-stu-id="d3062-115">You can access the properties of your payload by using dot notation like `data.function-name`.</span></span> <span data-ttu-id="d3062-116">Par exemple, une fonction JavaScript simple qui convertit une valeur DateTime en une chaîne de date se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="d3062-116">For example, a simple JavaScript function that converts a DateTime value into a date string looks like the following example:</span></span>

```
function start(req, res){
    var data = req.body;
    res = {
        body: data.date.ToDateString();
    }
}
```

## <a name="call-azure-functions-from-logic-apps"></a><span data-ttu-id="d3062-117">Appeler Azure Functions à partir d’applications logiques</span><span class="sxs-lookup"><span data-stu-id="d3062-117">Call Azure Functions from logic apps</span></span>

<span data-ttu-id="d3062-118">Pour répertorier les conteneurs dans votre abonnement et sélectionner la fonction que vous souhaitez appeler, dans le concepteur d’applications logiques, cliquez sur le menu **Actions**, puis choisissez dans **Azure Functions in my Region (Fonctions Azure dans ma région)**.</span><span class="sxs-lookup"><span data-stu-id="d3062-118">To list the containers in your subscription and select the function that you want to call, in Logic App Designer, click the **Actions** menu, and select from **Azure Functions in my Region**.</span></span>

<span data-ttu-id="d3062-119">Après avoir sélectionné la fonction, il vous est demandé de spécifier un objet de charge utile d’entrée.</span><span class="sxs-lookup"><span data-stu-id="d3062-119">After you select the function, you are asked to specify an input payload object.</span></span> <span data-ttu-id="d3062-120">Cet objet représente le message qu’envoie l’application logique à la fonction et doit être un objet JSON.</span><span class="sxs-lookup"><span data-stu-id="d3062-120">This object is the message that the logic app sends to the function and must be a JSON object.</span></span> <span data-ttu-id="d3062-121">Par exemple, pour passer la **date de dernière modification** à partir d’un déclencheur Salesforce, la charge utile de la fonction peut ressembler à cet exemple :</span><span class="sxs-lookup"><span data-stu-id="d3062-121">For example, if you want to pass in the **Last Modified** date from a Salesforce trigger, the function payload might look like this example:</span></span>

![Date de dernière modification][1]

## <a name="trigger-logic-apps-from-a-function"></a><span data-ttu-id="d3062-123">Déclencher des applications logiques à partir d’une fonction</span><span class="sxs-lookup"><span data-stu-id="d3062-123">Trigger logic apps from a function</span></span>

<span data-ttu-id="d3062-124">Vous pouvez déclencher une application logique dans une fonction.</span><span class="sxs-lookup"><span data-stu-id="d3062-124">You can trigger a logic app from inside a function.</span></span> <span data-ttu-id="d3062-125">Consultez [Applications logiques en tant que points de terminaison pouvant être appelés](logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="d3062-125">See [Logic apps as callable endpoints](logic-apps-http-endpoint.md).</span></span> <span data-ttu-id="d3062-126">Créez une application logique disposant d’un déclencheur manuel, puis, dans votre fonction, générez une requête HTTP POST vers l’URL du déclencheur manuel avec la charge utile que vous souhaitez envoyer à l’application logique.</span><span class="sxs-lookup"><span data-stu-id="d3062-126">Create a logic app that has a manual trigger, then from inside your function, generate an HTTP POST to the manual trigger URL with the payload that you want sent to the logic app.</span></span>

### <a name="create-a-function-from-logic-app-designer"></a><span data-ttu-id="d3062-127">Création d’une fonction à partir du concepteur d’applications logiques</span><span class="sxs-lookup"><span data-stu-id="d3062-127">Create a function from Logic App Designer</span></span>

<span data-ttu-id="d3062-128">Vous pouvez également créer une fonction de webhook node.js depuis le concepteur.</span><span class="sxs-lookup"><span data-stu-id="d3062-128">You can also create a node.js webhook function from the designer.</span></span> <span data-ttu-id="d3062-129">Tout d’abord, sélectionnez **Azure Functions in my Region** (Azure Functions dans ma région) et choisissez un conteneur pour votre fonction.</span><span class="sxs-lookup"><span data-stu-id="d3062-129">First, select **Azure Functions in my Region,** and then choose a container for your function.</span></span> <span data-ttu-id="d3062-130">Si vous n’avez pas encore de conteneur, vous devez en créer un à partir du [portail Azure Functions](https://functions.azure.com/signin).</span><span class="sxs-lookup"><span data-stu-id="d3062-130">If you don't yet have a container, you need to create one from the [Azure Functions portal](https://functions.azure.com/signin).</span></span> <span data-ttu-id="d3062-131">Sélectionnez ensuite **Créer**.</span><span class="sxs-lookup"><span data-stu-id="d3062-131">Then select **Create New**.</span></span>  

<span data-ttu-id="d3062-132">Pour générer un modèle basé sur les données que vous souhaitez calculer, spécifiez l’objet de contexte que vous envisagez de passer à une fonction.</span><span class="sxs-lookup"><span data-stu-id="d3062-132">To generate a template based on the data that you want to compute, specify the context object that you plan to pass into a function.</span></span> <span data-ttu-id="d3062-133">Cet objet doit être un objet JSON.</span><span class="sxs-lookup"><span data-stu-id="d3062-133">This object must be a JSON object.</span></span> <span data-ttu-id="d3062-134">Par exemple, si vous passez le contenu de fichier à partir d’une action FTP, la charge utile de contexte ressemblera à cet exemple :</span><span class="sxs-lookup"><span data-stu-id="d3062-134">For example, if you pass in the file content from an FTP action, the context payload looks like this example:</span></span>

![Charge utile de contexte][2]

> [!NOTE]
> <span data-ttu-id="d3062-136">Cet objet n’ayant pas été transformé en chaîne, le contenu est ajouté directement à la charge utile JSON.</span><span class="sxs-lookup"><span data-stu-id="d3062-136">Because this object wasn't cast as a string, the content is added directly to the JSON payload.</span></span> <span data-ttu-id="d3062-137">Cependant, cette opération provoque une erreur si l’objet n’est pas d’un jeton JSON (par exemple, une chaîne ou un objet/tableau JSON).</span><span class="sxs-lookup"><span data-stu-id="d3062-137">However, an error occurs if the object is not a JSON token (that is, a string or a JSON object/array).</span></span> <span data-ttu-id="d3062-138">Pour transformer cet objet en chaîne, ajoutez des guillemets comme indiqué dans la première illustration de cet article.</span><span class="sxs-lookup"><span data-stu-id="d3062-138">To cast the object as a string, add quotes as shown in the first illustration in this article.</span></span>
> 

<span data-ttu-id="d3062-139">Le concepteur génère ensuite un modèle de fonction que vous pouvez créer sous forme inline.</span><span class="sxs-lookup"><span data-stu-id="d3062-139">The designer then generates a function template that you can create inline.</span></span> <span data-ttu-id="d3062-140">Les variables sont créées préalablement en fonction du contexte que vous envisagez de passer à la fonction.</span><span class="sxs-lookup"><span data-stu-id="d3062-140">Variables are pre-created based on the context that you plan to pass into the function.</span></span>

<!--Image references-->
[1]: ./media/logic-apps-azure-functions/callfunction.png
[2]: ./media/logic-apps-azure-functions/createfunction.png
