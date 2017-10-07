---
title: code aaaCustom pour Azure Logic Apps avec des fonctions de Azure | Documents Microsoft
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
ms.openlocfilehash: 18b3821ed7e434feb568b9b96e9a5a2189dba3bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-and-run-custom-code-for-logic-apps-through-azure-functions"></a><span data-ttu-id="b5b72-103">Ajout et exécution d’un code personnalisé pour des applications logiques avec Azure Functions</span><span class="sxs-lookup"><span data-stu-id="b5b72-103">Add and run custom code for logic apps through Azure Functions</span></span>

<span data-ttu-id="b5b72-104">extraits de code personnalisés toorun de c# ou node.js dans les applications de la logique, vous pouvez créer des fonctions personnalisées au moyen de fonctions de Azure.</span><span class="sxs-lookup"><span data-stu-id="b5b72-104">toorun custom snippets of C# or node.js in logic apps, you can create custom functions through Azure Functions.</span></span> 
<span data-ttu-id="b5b72-105">[Azure Functions](../azure-functions/functions-overview.md) assure le calcul sans serveur dans Microsoft Azure, et est utile pour effectuer ces tâches :</span><span class="sxs-lookup"><span data-stu-id="b5b72-105">[Azure Functions](../azure-functions/functions-overview.md) offers server-free computing in Microsoft Azure and are useful for performing these tasks:</span></span>

* <span data-ttu-id="b5b72-106">Mise en forme avancée ou calcul de champs dans les applications logiques</span><span class="sxs-lookup"><span data-stu-id="b5b72-106">Advanced formatting or compute of fields in logic apps</span></span>
* <span data-ttu-id="b5b72-107">Effectuez les calculs dans un workflow.</span><span class="sxs-lookup"><span data-stu-id="b5b72-107">Perform calculations in a workflow.</span></span>
* <span data-ttu-id="b5b72-108">Étendre les fonctionnalités de l’application hello logique avec des fonctions qui sont prises en charge en c# ou node.js</span><span class="sxs-lookup"><span data-stu-id="b5b72-108">Extend hello logic app functionality with functions that are supported in C# or node.js</span></span>

## <a name="create-custom-functions-for-your-logic-apps"></a><span data-ttu-id="b5b72-109">Création de fonctions personnalisées pour vos applications logiques</span><span class="sxs-lookup"><span data-stu-id="b5b72-109">Create custom functions for your logic apps</span></span>

<span data-ttu-id="b5b72-110">Nous vous recommandons de créer une fonction dans le portail Azure fonctions hello, à partir de hello **Webhook générique - nœud** ou **Webhook - générique c#** modèles.</span><span class="sxs-lookup"><span data-stu-id="b5b72-110">We recommend that you create a function in hello Azure Functions portal, from hello **Generic Webhook - Node** or **Generic Webhook - C#** templates.</span></span> <span data-ttu-id="b5b72-111">résultat de Hello crée un rempli automatiquement un modèle qui accepte `application/json` à partir d’une application logique.</span><span class="sxs-lookup"><span data-stu-id="b5b72-111">hello result creates an auto-populated a template that accepts `application/json` from a logic app.</span></span> <span data-ttu-id="b5b72-112">Les fonctions que vous créez à partir de ces modèles sont détectées automatiquement et s’affichent dans hello de concepteur d’application logique sous **fonctions Azure dans ma région.**</span><span class="sxs-lookup"><span data-stu-id="b5b72-112">Functions that you create from these templates are automatically detected and appear in hello Logic App Designer under **Azure Functions in my region.**</span></span>

<span data-ttu-id="b5b72-113">Bonjour portail Azure, sur hello **intégrer** volet de votre fonction, votre modèle doit montrer que **Mode** défini trop**Webhook** et **Webhook type** est défini trop**JSON générique**.</span><span class="sxs-lookup"><span data-stu-id="b5b72-113">In hello Azure portal, on hello **Integrate** pane for your function, your template should show that **Mode** set too**Webhook** and **Webhook type** is set too**Generic JSON**.</span></span> 

<span data-ttu-id="b5b72-114">Les fonctions de Webhook accepter une demande et passez-la dans la méthode hello via un `data` variable.</span><span class="sxs-lookup"><span data-stu-id="b5b72-114">Webhook functions accept a request and pass it into hello method via a `data` variable.</span></span> <span data-ttu-id="b5b72-115">Vous pouvez accéder à des propriétés de hello de votre charge utile à l’aide de notation par points comme `data.function-name`.</span><span class="sxs-lookup"><span data-stu-id="b5b72-115">You can access hello properties of your payload by using dot notation like `data.function-name`.</span></span> <span data-ttu-id="b5b72-116">Par exemple, une fonction JavaScript simple qui convertit une valeur DateTime en une chaîne de date se présente comme hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="b5b72-116">For example, a simple JavaScript function that converts a DateTime value into a date string looks like hello following example:</span></span>

```
function start(req, res){
    var data = req.body;
    res = {
        body: data.date.ToDateString();
    }
}
```

## <a name="call-azure-functions-from-logic-apps"></a><span data-ttu-id="b5b72-117">Appeler Azure Functions à partir d’applications logiques</span><span class="sxs-lookup"><span data-stu-id="b5b72-117">Call Azure Functions from logic apps</span></span>

<span data-ttu-id="b5b72-118">conteneurs de hello toolist dans votre abonnement et la fonction hello select que vous souhaitez toocall, dans le Concepteur d’application logique, cliquez sur hello **Actions** , puis sélectionnez à partir de **fonctions Azure dans ma région**.</span><span class="sxs-lookup"><span data-stu-id="b5b72-118">toolist hello containers in your subscription and select hello function that you want toocall, in Logic App Designer, click hello **Actions** menu, and select from **Azure Functions in my Region**.</span></span>

<span data-ttu-id="b5b72-119">Après avoir sélectionné la fonction hello, vous êtes invité toospecify un objet de la charge utile d’entrée.</span><span class="sxs-lookup"><span data-stu-id="b5b72-119">After you select hello function, you are asked toospecify an input payload object.</span></span> <span data-ttu-id="b5b72-120">Cet objet est un message de type hello hello logique application envoie toohello fonction et doit être un objet JSON.</span><span class="sxs-lookup"><span data-stu-id="b5b72-120">This object is hello message that hello logic app sends toohello function and must be a JSON object.</span></span> <span data-ttu-id="b5b72-121">Par exemple, si vous souhaitez toopass Bonjour **de dernière modification** date à partir d’un déclencheur de Salesforce, charge utile de fonction hello peut se présenter à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="b5b72-121">For example, if you want toopass in hello **Last Modified** date from a Salesforce trigger, hello function payload might look like this example:</span></span>

![Date de dernière modification][1]

## <a name="trigger-logic-apps-from-a-function"></a><span data-ttu-id="b5b72-123">Déclencher des applications logiques à partir d’une fonction</span><span class="sxs-lookup"><span data-stu-id="b5b72-123">Trigger logic apps from a function</span></span>

<span data-ttu-id="b5b72-124">Vous pouvez déclencher une application logique dans une fonction.</span><span class="sxs-lookup"><span data-stu-id="b5b72-124">You can trigger a logic app from inside a function.</span></span> <span data-ttu-id="b5b72-125">Consultez [Applications logiques en tant que points de terminaison pouvant être appelés](logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="b5b72-125">See [Logic apps as callable endpoints](logic-apps-http-endpoint.md).</span></span> <span data-ttu-id="b5b72-126">Créer une application de la logique qui comporte un déclencheur manuel, puis à partir de votre fonction, générer une URL de déclenchement manuel toohello HTTP POST avec une charge utile hello qui que vous souhaitez envoyer toohello logique application.</span><span class="sxs-lookup"><span data-stu-id="b5b72-126">Create a logic app that has a manual trigger, then from inside your function, generate an HTTP POST toohello manual trigger URL with hello payload that you want sent toohello logic app.</span></span>

### <a name="create-a-function-from-logic-app-designer"></a><span data-ttu-id="b5b72-127">Création d’une fonction à partir du concepteur d’applications logiques</span><span class="sxs-lookup"><span data-stu-id="b5b72-127">Create a function from Logic App Designer</span></span>

<span data-ttu-id="b5b72-128">Vous pouvez également créer une fonction de webhook node.js à partir du concepteur hello.</span><span class="sxs-lookup"><span data-stu-id="b5b72-128">You can also create a node.js webhook function from hello designer.</span></span> <span data-ttu-id="b5b72-129">Tout d’abord, sélectionnez **Azure Functions in my Region** (Azure Functions dans ma région) et choisissez un conteneur pour votre fonction.</span><span class="sxs-lookup"><span data-stu-id="b5b72-129">First, select **Azure Functions in my Region,** and then choose a container for your function.</span></span> <span data-ttu-id="b5b72-130">Si vous n’avez pas encore un conteneur, vous devez toocreate une à partir de hello [portal de fonctions d’Azure](https://functions.azure.com/signin).</span><span class="sxs-lookup"><span data-stu-id="b5b72-130">If you don't yet have a container, you need toocreate one from hello [Azure Functions portal](https://functions.azure.com/signin).</span></span> <span data-ttu-id="b5b72-131">Sélectionnez ensuite **Créer**.</span><span class="sxs-lookup"><span data-stu-id="b5b72-131">Then select **Create New**.</span></span>  

<span data-ttu-id="b5b72-132">toogenerate un modèle basé sur les données de salutation que vous souhaitez toocompute, spécifiez l’objet de contexte hello que vous envisagez de toopass dans une fonction.</span><span class="sxs-lookup"><span data-stu-id="b5b72-132">toogenerate a template based on hello data that you want toocompute, specify hello context object that you plan toopass into a function.</span></span> <span data-ttu-id="b5b72-133">Cet objet doit être un objet JSON.</span><span class="sxs-lookup"><span data-stu-id="b5b72-133">This object must be a JSON object.</span></span> <span data-ttu-id="b5b72-134">Par exemple, si vous passez dans le contenu du fichier hello à partir d’une action de FTP, charge utile de contexte hello ressemble à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="b5b72-134">For example, if you pass in hello file content from an FTP action, hello context payload looks like this example:</span></span>

![Charge utile de contexte][2]

> [!NOTE]
> <span data-ttu-id="b5b72-136">Étant donné que cet objet n’a pas été converti en une chaîne, le contenu hello est ajouté directement charge utile JSON de toohello.</span><span class="sxs-lookup"><span data-stu-id="b5b72-136">Because this object wasn't cast as a string, hello content is added directly toohello JSON payload.</span></span> <span data-ttu-id="b5b72-137">Toutefois, une erreur se produit si l’objet de hello n’est pas un jeton JSON (autrement dit, une chaîne ou JSON/tableau d’objets).</span><span class="sxs-lookup"><span data-stu-id="b5b72-137">However, an error occurs if hello object is not a JSON token (that is, a string or a JSON object/array).</span></span> <span data-ttu-id="b5b72-138">objet de hello toocast sous forme de chaîne, ajouter des guillemets comme indiqué dans la première illustration de hello dans cet article.</span><span class="sxs-lookup"><span data-stu-id="b5b72-138">toocast hello object as a string, add quotes as shown in hello first illustration in this article.</span></span>
> 

<span data-ttu-id="b5b72-139">le Concepteur de Hello génère ensuite un modèle de fonction que vous pouvez créer en ligne.</span><span class="sxs-lookup"><span data-stu-id="b5b72-139">hello designer then generates a function template that you can create inline.</span></span> <span data-ttu-id="b5b72-140">Les variables sont créés au préalable en fonction de contexte hello que vous envisagez de toopass dans la fonction hello.</span><span class="sxs-lookup"><span data-stu-id="b5b72-140">Variables are pre-created based on hello context that you plan toopass into hello function.</span></span>

<!--Image references-->
[1]: ./media/logic-apps-azure-functions/callfunction.png
[2]: ./media/logic-apps-azure-functions/createfunction.png
