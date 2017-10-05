---
title: "Prise en main des métadonnées OpenAPI dans Azure Functions | Microsoft Docs"
description: "Prise en main de la prise en charge d’OpenAPI dans Azure Functions"
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 03/23/2017
ms.author: alkarche
ms.openlocfilehash: 9b861aacf31e17866293732dc2323f56014c1877
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="creating-openapi-20-swagger-metadata-for-a-function-app-preview"></a><span data-ttu-id="58c48-103">Création de métadonnées OpenAPI 2.0 (Swagger) pour une Function App (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="58c48-103">Creating OpenAPI 2.0 (Swagger) Metadata for a Function App (Preview)</span></span>

<span data-ttu-id="58c48-104">Ce document vous guide pas à pas dans la création d’une définition OpenAPI pour une API simple hébergée sur Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="58c48-104">This document guides you through the step by step process of creating an OpenAPI Definition for a simple API hosted on Azure Functions.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

### <a name="what-is-openapi-swagger"></a><span data-ttu-id="58c48-105">Qu’est-ce qu’OpenAPI (Swagger) ?</span><span class="sxs-lookup"><span data-stu-id="58c48-105">What is OpenAPI (Swagger)?</span></span>
<span data-ttu-id="58c48-106">[Métadonnées Swagger](http://swagger.io/) est un fichier qui définit les fonctionnalités et les modes de fonctionnement de votre API et permet à une fonction qui héberge une API REST d’être utilisée par une grande variété d’autres logiciels.</span><span class="sxs-lookup"><span data-stu-id="58c48-106">[Swagger Metadata](http://swagger.io/) is a file that defines the functionality and operating modes of your API, and allows a function hosting a REST API to be consumed by a wide variety of other software.</span></span> <span data-ttu-id="58c48-107">Les offres Microsoft telles que PowerApps et [API Apps](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), ainsi que des outils de développeurs tiers tels que [Postman](https://www.getpostman.com/docs/importing_swagger) et [de nombreux autres packages](http://swagger.io/tools/) permettent à votre API d’être utilisée avec une définition Swagger.</span><span class="sxs-lookup"><span data-stu-id="58c48-107">Microsoft offerings like PowerApps and [API Apps](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), as well as 3rd party developer tooling like [Postman](https://www.getpostman.com/docs/importing_swagger) and [many more packages](http://swagger.io/tools/) all allow your API to be consumed with a Swagger definition.</span></span>

## <span data-ttu-id="58c48-108"><a name="prepare-function"></a>Création d’une fonction avec une API simple</span><span class="sxs-lookup"><span data-stu-id="58c48-108"><a name="prepare-function"></a>Creating a Function with a simple API</span></span>
  <span data-ttu-id="58c48-109">Pour créer une définition OpenAPI, nous devons tout d’abord créer une fonction avec une API simple.</span><span class="sxs-lookup"><span data-stu-id="58c48-109">To create an OpenAPI definition, we first need to create a Function with a simple API.</span></span> <span data-ttu-id="58c48-110">Si vous disposez déjà d’une API hébergée sur une Function App, vous pouvez passer directement à la section suivante</span><span class="sxs-lookup"><span data-stu-id="58c48-110">If you already have an API hosted on a Function App, you can skip straight to the next section</span></span>
1. <span data-ttu-id="58c48-111">Créez une nouvelle Function App.</span><span class="sxs-lookup"><span data-stu-id="58c48-111">Create a new Function App.</span></span>
    1. <span data-ttu-id="58c48-112">[Portail Azure](https://portal.azure.com) > `+ New` > Recherchez « Function App »</span><span class="sxs-lookup"><span data-stu-id="58c48-112">[Azure portal](https://portal.azure.com) > `+ New` > Search for "Function App"</span></span>
1. <span data-ttu-id="58c48-113">Créer une nouvelle fonction de déclencheur HTTP à l’intérieur de votre nouvelle Function App</span><span class="sxs-lookup"><span data-stu-id="58c48-113">Create a new HTTP trigger function inside your new Function App</span></span>
    1. <span data-ttu-id="58c48-114">Votre fonction est préremplie avec du code définissant une API REST très simple.</span><span class="sxs-lookup"><span data-stu-id="58c48-114">Your function is pre-populated with code defining a very simple REST API.</span></span>
    1. <span data-ttu-id="58c48-115">N’importe quelle chaîne transmise à la fonction en tant que paramètre de requête ou dans le corps est retournée en tant que « Bonjour {entrée} »</span><span class="sxs-lookup"><span data-stu-id="58c48-115">Any string passed to the Function as a query parameter or in the body is returned as "Hello {input}"</span></span>
1. <span data-ttu-id="58c48-116">Accédez à l’onglet `Integrate` de votre nouvelle fonction de déclencheur HTTP</span><span class="sxs-lookup"><span data-stu-id="58c48-116">Go to the `Integrate` tab of your new HTTP Trigger function</span></span>
    1. <span data-ttu-id="58c48-117">Basculer `Allowed HTTP methods` sur `Selected methods`</span><span class="sxs-lookup"><span data-stu-id="58c48-117">Toggle `Allowed HTTP methods` to `Selected methods`</span></span>
    1. <span data-ttu-id="58c48-118">Dans `Selected HTTP methods`, désactivez chaque verbe sauf POST.</span><span class="sxs-lookup"><span data-stu-id="58c48-118">In `Selected HTTP methods` uncheck every verb except POST.</span></span>
    <span data-ttu-id="58c48-119">![Méthodes HTTP sélectionnées](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)</span><span class="sxs-lookup"><span data-stu-id="58c48-119">![Selected HTTP Methods](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)</span></span>
    1. <span data-ttu-id="58c48-120">Cette étape simplifiera votre définition d’API.</span><span class="sxs-lookup"><span data-stu-id="58c48-120">This step will simplify your API definition later on.</span></span>

## <span data-ttu-id="58c48-121"><a name="enable"></a>Activation de la prise en charge de la définition d’API</span><span class="sxs-lookup"><span data-stu-id="58c48-121"><a name="enable"></a>Enabling API Definition Support</span></span>
1. <span data-ttu-id="58c48-122">Accédez à `your function name`  >  `Platform Features`  >  `API Definition` 
 ![onglet Définition](./media/functions-api-definition-getting-started/definitiontab.png)</span><span class="sxs-lookup"><span data-stu-id="58c48-122">Navigate to `your function name` > `Platform Features` > `API Definition`
![Definition Tab](./media/functions-api-definition-getting-started/definitiontab.png)</span></span>
1. <span data-ttu-id="58c48-123">Paramétrez `API Definition Source` sur `Function (preview)`</span><span class="sxs-lookup"><span data-stu-id="58c48-123">Set `API Definition Source` to `Function (preview)`</span></span>
    1. <span data-ttu-id="58c48-124">Cette étape active une suite d’options OpenAPI pour votre Function App, notamment un point de terminaison pour héberger un fichier OpenAPI à partir du domaine de votre Function App, une copie en ligne de l’[éditeur OpenAPI](http://editor.swagger.io) et un générateur de définition de démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="58c48-124">This step enables a suite of OpenAPI options for your Function App, including an endpoint to host an OpenAPI file from your Function App's domain, an inline copy of the [OpenAPI Editor](http://editor.swagger.io), and a quickstart definition generator.</span></span>
<span data-ttu-id="58c48-125">![Définition activée](./media/functions-api-definition-getting-started/enabledefinition.png)</span><span class="sxs-lookup"><span data-stu-id="58c48-125">![Enabled Definition](./media/functions-api-definition-getting-started/enabledefinition.png)</span></span>

## <span data-ttu-id="58c48-126"><a name="create-definition"></a>Création de votre définition d’API à partir d’un modèle</span><span class="sxs-lookup"><span data-stu-id="58c48-126"><a name="create-definition"></a>Creating your API Definition from a template</span></span>
1. <span data-ttu-id="58c48-127">Cliquez sur `Generate API Definition template`</span><span class="sxs-lookup"><span data-stu-id="58c48-127">Click `Generate API Definition template`</span></span>
    1. <span data-ttu-id="58c48-128">Cette étape analyse votre Function App pour trouver des fonctions de déclencheur HTTP et utilise les informations contenues dans functions.json pour générer un document OpenAPI.</span><span class="sxs-lookup"><span data-stu-id="58c48-128">This step scans your Function App for HTTP Trigger functions and uses the info in functions.json to generate an OpenAPI document.</span></span>
1. <span data-ttu-id="58c48-129">Ajouter un objet d’opération à `paths: /api/yourfunctionroute post:`</span><span class="sxs-lookup"><span data-stu-id="58c48-129">Add an operation object to `paths: /api/yourfunctionroute post:`</span></span>
    1. <span data-ttu-id="58c48-130">Le document OpenAPI de démarrage rapide est un plan d’un document OpenAPI complet. Elle nécessite davantage de métadonnées pour être une définition OpenAPI complète, telles que des objets d’opération et des modèles de réponse.</span><span class="sxs-lookup"><span data-stu-id="58c48-130">The quickstart OpenAPI document is an outline of a full OpenAPI doc. It requires more metadata to be a full OpenAPI definition, such as operation objects and response templates.</span></span>
    1. <span data-ttu-id="58c48-131">L’exemple d’objet d’opération ci-dessous dispose d’une section production/consommation remplie, d’un objet de paramètre et d’un objet de réponse.</span><span class="sxs-lookup"><span data-stu-id="58c48-131">The sample operation object below has a filled out produces/consumes section, a parameter object, and a response object.</span></span>
    
    ```yaml
      post:
        operationId: /api/yourfunctionroute/post
        consumes: [application/json]
        produces: [application/json]
        parameters:
          - name: name
            in: body
            description: Your name
            x-ms-summary: Your name
            required: true
            schema:
              type: object
              properties:
                name:
                  type: string
        description: >-
          Replace with Operation Object
          #http://swagger.io/specification/#operationObject
        responses:
          '200':
            description: A Greeting
            x-ms-summary: Your name
            schema:
              type: string
        security:
          - apikeyQuery: []
    ```
    
    > [!NOTE]
    >  <span data-ttu-id="58c48-132">x-ms-summary fournit un nom d’affichage dans Logic Apps, Flow et PowerApps.</span><span class="sxs-lookup"><span data-stu-id="58c48-132">x-ms-summary provides a display name in Logic Apps, Flow, and PowerApps.</span></span>
    >
    > <span data-ttu-id="58c48-133">Consultez la section [Personnaliser votre définition Swagger pour PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="58c48-133">Check out [customize your Swagger definition for PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) to learn more.</span></span>

1. <span data-ttu-id="58c48-134">Cliquez sur `save` pour enregistrer vos modifications ![Ajout d’une définition de modèle](./media/functions-api-definition-getting-started/addingtemplate.png)</span><span class="sxs-lookup"><span data-stu-id="58c48-134">Click `save` to save your changes ![Adding Template Definition](./media/functions-api-definition-getting-started/addingtemplate.png)</span></span>

## <span data-ttu-id="58c48-135"><a name="use-definition"></a>Utilisation de votre définition d’API</span><span class="sxs-lookup"><span data-stu-id="58c48-135"><a name="use-definition"></a>Using Your API Definition</span></span>
1. <span data-ttu-id="58c48-136">Copiez-collez votre `API definition URL` dans un nouvel onglet de navigateur pour afficher votre document OpenAPI brut.</span><span class="sxs-lookup"><span data-stu-id="58c48-136">Copy your `API definition URL` and paste it into a new browser tab to view your raw OpenAPI document.</span></span>
1. <span data-ttu-id="58c48-137">Vous pouvez importer votre document OpenAPI dans un nombre illimité d’outils de test et l’intégration via cette URL.</span><span class="sxs-lookup"><span data-stu-id="58c48-137">You can import your OpenAPI document to any number of tools for testing and integration using that URL.</span></span>
    1. <span data-ttu-id="58c48-138">De nombreuses ressources Azure peuvent importer automatiquement votre document OpenAPI à l’aide de l’URL de définition d’API qui est enregistrée dans vos paramètres d’application de fonction.</span><span class="sxs-lookup"><span data-stu-id="58c48-138">Many Azure resources are able to automatically import your OpenAPI doc using the API Definition URL that is saved in your Function application settings.</span></span> <span data-ttu-id="58c48-139">Dans le cadre de la source de définition d’API `Function`, nous mettons à jour cette URL pour vous.</span><span class="sxs-lookup"><span data-stu-id="58c48-139">As a part of the `Function` API definition source, we update that url for you.</span></span>


## <span data-ttu-id="58c48-140"><a name="test-definition"></a>Utilisation de l’interface utilisateur Swagger pour tester votre définition d’API</span><span class="sxs-lookup"><span data-stu-id="58c48-140"><a name="test-definition"></a>Using the Swagger UI to test your API definition</span></span>
<span data-ttu-id="58c48-141">Des outils de test sont intégrés à l’affichage interface utilisateur de l’éditeur de définition d’API intégré.</span><span class="sxs-lookup"><span data-stu-id="58c48-141">There are testing tools built in to the UI view of the imbedded API definition editor.</span></span> <span data-ttu-id="58c48-142">Ajoutez votre clé d’API, puis utilisez le bouton `Try this operation` sous chaque méthode.</span><span class="sxs-lookup"><span data-stu-id="58c48-142">Add your API key, and then use the `Try this operation` button under each method.</span></span> <span data-ttu-id="58c48-143">L’outil utilisera votre définition d’API pour mettre en forme les demandes et les réponses de réussite indiqueront que la définition est correcte.</span><span class="sxs-lookup"><span data-stu-id="58c48-143">The tool will use your API Definition to format the requests and successful responses will indicate that your definition is correct.</span></span>

### <a name="steps"></a><span data-ttu-id="58c48-144">Étapes :</span><span class="sxs-lookup"><span data-stu-id="58c48-144">Steps:</span></span>

1. <span data-ttu-id="58c48-145">Copier votre clé d’API de fonction</span><span class="sxs-lookup"><span data-stu-id="58c48-145">Copy your function API key</span></span>
    1. <span data-ttu-id="58c48-146">Vous trouverez la clé d’API dans votre fonction de déclenchement HTTP sous `function name` > `Keys` > `Function Keys` 
   ![touche de fonction](./media/functions-api-definition-getting-started/functionkey.png)</span><span class="sxs-lookup"><span data-stu-id="58c48-146">The API key can be found in your HTTP Trigger Function under `function name` > `Keys` > `Function Keys`
![Function key](./media/functions-api-definition-getting-started/functionkey.png)</span></span>
1. <span data-ttu-id="58c48-147">Accédez à la page `API Definition`.</span><span class="sxs-lookup"><span data-stu-id="58c48-147">Navigate to the `API Definition` page.</span></span>
    1. <span data-ttu-id="58c48-148">Cliquez sur `Authenticate` et ajoutez votre clé d’API de fonction à l’objet de sécurité en haut.</span><span class="sxs-lookup"><span data-stu-id="58c48-148">Click `Authenticate` and add your Function API key to the security object at the top.</span></span>
  <span data-ttu-id="58c48-149">![Clé OpenAPI](./media/functions-api-definition-getting-started/definitionTest auth.png)</span><span class="sxs-lookup"><span data-stu-id="58c48-149">![OpenAPI key](./media/functions-api-definition-getting-started/definitionTest auth.png)</span></span>
1. <span data-ttu-id="58c48-150">sélectionnez `/api/yourfunctionroute` > `POST`</span><span class="sxs-lookup"><span data-stu-id="58c48-150">select `/api/yourfunctionroute` > `POST`</span></span>
1. <span data-ttu-id="58c48-151">Cliquez sur `Try it out` et entrez un nom pour le test</span><span class="sxs-lookup"><span data-stu-id="58c48-151">Click `Try it out` and enter a name to test</span></span>
1. <span data-ttu-id="58c48-152">Vous devriez voir un résultat RÉUSSITE sous `Pretty`
![Test de définition d’API](./media/functions-api-definition-getting-started/definitionTest.png)</span><span class="sxs-lookup"><span data-stu-id="58c48-152">You should see a SUCCESS result under `Pretty`
![API Definition test](./media/functions-api-definition-getting-started/definitionTest.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="58c48-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="58c48-153">Next steps</span></span>
* [<span data-ttu-id="58c48-154">Définition OpenAPI dans Vue d’ensemble de Functions</span><span class="sxs-lookup"><span data-stu-id="58c48-154">OpenAPI Definition in Functions Overview</span></span>](functions-api-definition.md)
  * <span data-ttu-id="58c48-155">Lisez la documentation complète pour plus d’informations sur la prise en charge d’OpenAPI.</span><span class="sxs-lookup"><span data-stu-id="58c48-155">Read the full documentation for more info on OpenAPI support.</span></span>
* [<span data-ttu-id="58c48-156">Informations de référence pour les développeurs sur Azure Functions</span><span class="sxs-lookup"><span data-stu-id="58c48-156">Azure Functions developer reference</span></span>](functions-reference.md)  
  * <span data-ttu-id="58c48-157">Référence du programmeur pour le codage de fonctions et la définition de déclencheurs et de liaisons.</span><span class="sxs-lookup"><span data-stu-id="58c48-157">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="58c48-158">Référentiel GitHub Azure Functions</span><span class="sxs-lookup"><span data-stu-id="58c48-158">Azure Functions GitHub repository</span></span>](https://github.com/Azure/Azure-Functions/)
  * <span data-ttu-id="58c48-159">Consultez le GitHub Functions pour nous donner votre avis sur la version préliminaire du support de définition d’API !</span><span class="sxs-lookup"><span data-stu-id="58c48-159">Check out the Functions GitHub to give us feedback on the API definition support preview!</span></span> <span data-ttu-id="58c48-160">Créez un ticket GitHub pour les mises à jour que vous souhaitez.</span><span class="sxs-lookup"><span data-stu-id="58c48-160">Make a GitHub issue for anything you'd like to see updated.</span></span>
