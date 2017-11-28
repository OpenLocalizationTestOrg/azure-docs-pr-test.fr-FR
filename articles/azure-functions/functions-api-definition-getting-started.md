---
title: "aaaGetting démarré avec OpenAPI Metadata dans les fonctions Azure | Documents Microsoft"
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
ms.openlocfilehash: fee3464c9a0a11b6d3891ccd0e9c5343d6bedcad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-openapi-20-swagger-metadata-for-a-function-app-preview"></a><span data-ttu-id="b43d8-103">Création de métadonnées OpenAPI 2.0 (Swagger) pour une Function App (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="b43d8-103">Creating OpenAPI 2.0 (Swagger) Metadata for a Function App (Preview)</span></span>

<span data-ttu-id="b43d8-104">Ce document vous guide tout au long des processus d’étape par étape de hello de création d’une définition de OpenAPI pour une API simple hébergée sur les fonctions d’Azure.</span><span class="sxs-lookup"><span data-stu-id="b43d8-104">This document guides you through hello step by step process of creating an OpenAPI Definition for a simple API hosted on Azure Functions.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

### <a name="what-is-openapi-swagger"></a><span data-ttu-id="b43d8-105">Qu’est-ce qu’OpenAPI (Swagger) ?</span><span class="sxs-lookup"><span data-stu-id="b43d8-105">What is OpenAPI (Swagger)?</span></span>
<span data-ttu-id="b43d8-106">[Métadonnées de swagger](http://swagger.io/) est un fichier qui définit les fonctionnalités de hello et modes de votre API de fonctionnement et permet à une fonction qui héberge un toobe de l’API REST utilisée par un grand nombre d’autres logiciels.</span><span class="sxs-lookup"><span data-stu-id="b43d8-106">[Swagger Metadata](http://swagger.io/) is a file that defines hello functionality and operating modes of your API, and allows a function hosting a REST API toobe consumed by a wide variety of other software.</span></span> <span data-ttu-id="b43d8-107">Offres Microsoft telles que PowerApps et [applications API](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), ainsi que de 3 développeur tiers tels que des outils [Postman](https://www.getpostman.com/docs/importing_swagger) et [de nombreux packages plus](http://swagger.io/tools/) tous les autoriser votre toobe API consommée avec un Définition swagger.</span><span class="sxs-lookup"><span data-stu-id="b43d8-107">Microsoft offerings like PowerApps and [API Apps](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), as well as 3rd party developer tooling like [Postman](https://www.getpostman.com/docs/importing_swagger) and [many more packages](http://swagger.io/tools/) all allow your API toobe consumed with a Swagger definition.</span></span>

## <span data-ttu-id="b43d8-108"><a name="prepare-function"></a>Création d’une fonction avec une API simple</span><span class="sxs-lookup"><span data-stu-id="b43d8-108"><a name="prepare-function"></a>Creating a Function with a simple API</span></span>
  <span data-ttu-id="b43d8-109">toocreate une définition OpenAPI, nous devons tout d’abord toocreate une fonction avec une API simple.</span><span class="sxs-lookup"><span data-stu-id="b43d8-109">toocreate an OpenAPI definition, we first need toocreate a Function with a simple API.</span></span> <span data-ttu-id="b43d8-110">Si vous avez déjà une API hébergée sur une application de la fonction, vous pouvez ignorer la section suivante de droite toohello</span><span class="sxs-lookup"><span data-stu-id="b43d8-110">If you already have an API hosted on a Function App, you can skip straight toohello next section</span></span>
1. <span data-ttu-id="b43d8-111">Créez une nouvelle Function App.</span><span class="sxs-lookup"><span data-stu-id="b43d8-111">Create a new Function App.</span></span>
    1. <span data-ttu-id="b43d8-112">[Portail Azure](https://portal.azure.com) > `+ New` &gt; Recherchez « Function App »</span><span class="sxs-lookup"><span data-stu-id="b43d8-112">[Azure portal](https://portal.azure.com) > `+ New` > Search for "Function App"</span></span>
1. <span data-ttu-id="b43d8-113">Créer une nouvelle fonction de déclencheur HTTP à l’intérieur de votre nouvelle Function App</span><span class="sxs-lookup"><span data-stu-id="b43d8-113">Create a new HTTP trigger function inside your new Function App</span></span>
    1. <span data-ttu-id="b43d8-114">Votre fonction est préremplie avec du code définissant une API REST très simple.</span><span class="sxs-lookup"><span data-stu-id="b43d8-114">Your function is pre-populated with code defining a very simple REST API.</span></span>
    1. <span data-ttu-id="b43d8-115">N’importe quelle chaîne passée toohello fonction comme paramètre de requête ou dans le corps de hello est retourné en tant que « Hello {entrée} »</span><span class="sxs-lookup"><span data-stu-id="b43d8-115">Any string passed toohello Function as a query parameter or in hello body is returned as "Hello {input}"</span></span>
1. <span data-ttu-id="b43d8-116">Accédez toohello `Integrate` onglet de votre nouvelle fonction de déclencheur de HTTP</span><span class="sxs-lookup"><span data-stu-id="b43d8-116">Go toohello `Integrate` tab of your new HTTP Trigger function</span></span>
    1. <span data-ttu-id="b43d8-117">Activer/désactiver `Allowed HTTP methods` trop`Selected methods`</span><span class="sxs-lookup"><span data-stu-id="b43d8-117">Toggle `Allowed HTTP methods` too`Selected methods`</span></span>
    1. <span data-ttu-id="b43d8-118">Dans `Selected HTTP methods`, désactivez chaque verbe sauf POST.</span><span class="sxs-lookup"><span data-stu-id="b43d8-118">In `Selected HTTP methods` uncheck every verb except POST.</span></span>
    <span data-ttu-id="b43d8-119">![Méthodes HTTP sélectionnées](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)</span><span class="sxs-lookup"><span data-stu-id="b43d8-119">![Selected HTTP Methods](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)</span></span>
    1. <span data-ttu-id="b43d8-120">Cette étape simplifiera votre définition d’API.</span><span class="sxs-lookup"><span data-stu-id="b43d8-120">This step will simplify your API definition later on.</span></span>

## <span data-ttu-id="b43d8-121"><a name="enable"></a>Activation de la prise en charge de la définition d’API</span><span class="sxs-lookup"><span data-stu-id="b43d8-121"><a name="enable"></a>Enabling API Definition Support</span></span>
1. <span data-ttu-id="b43d8-122">Accédez trop`your function name` > `Platform Features` > `API Definition`
![onglet Définition](./media/functions-api-definition-getting-started/definitiontab.png)</span><span class="sxs-lookup"><span data-stu-id="b43d8-122">Navigate too`your function name` > `Platform Features` > `API Definition`
![Definition Tab](./media/functions-api-definition-getting-started/definitiontab.png)</span></span>
1. <span data-ttu-id="b43d8-123">Définissez `API Definition Source` trop`Function (preview)`</span><span class="sxs-lookup"><span data-stu-id="b43d8-123">Set `API Definition Source` too`Function (preview)`</span></span>
    1. <span data-ttu-id="b43d8-124">Cette étape permet à une suite d’options OpenAPI pour votre application de la fonction, y compris un point de terminaison de toohost un fichier OpenAPI à partir du domaine de votre application de fonction, une copie de la ligne de hello [OpenAPI éditeur](http://editor.swagger.io)et un générateur de définition de démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="b43d8-124">This step enables a suite of OpenAPI options for your Function App, including an endpoint toohost an OpenAPI file from your Function App's domain, an inline copy of hello [OpenAPI Editor](http://editor.swagger.io), and a quickstart definition generator.</span></span>
<span data-ttu-id="b43d8-125">![Définition activée](./media/functions-api-definition-getting-started/enabledefinition.png)</span><span class="sxs-lookup"><span data-stu-id="b43d8-125">![Enabled Definition](./media/functions-api-definition-getting-started/enabledefinition.png)</span></span>

## <span data-ttu-id="b43d8-126"><a name="create-definition"></a>Création de votre définition d’API à partir d’un modèle</span><span class="sxs-lookup"><span data-stu-id="b43d8-126"><a name="create-definition"></a>Creating your API Definition from a template</span></span>
1. <span data-ttu-id="b43d8-127">Cliquez sur `Generate API Definition template`</span><span class="sxs-lookup"><span data-stu-id="b43d8-127">Click `Generate API Definition template`</span></span>
    1. <span data-ttu-id="b43d8-128">Cette étape analyse votre application de la fonction pour les fonctions de déclencheur de HTTP et utilise les informations de hello dans functions.json toogenerate un document OpenAPI.</span><span class="sxs-lookup"><span data-stu-id="b43d8-128">This step scans your Function App for HTTP Trigger functions and uses hello info in functions.json toogenerate an OpenAPI document.</span></span>
1. <span data-ttu-id="b43d8-129">Ajouter un objet de l’opération trop`paths: /api/yourfunctionroute post:`</span><span class="sxs-lookup"><span data-stu-id="b43d8-129">Add an operation object too`paths: /api/yourfunctionroute post:`</span></span>
    1. <span data-ttu-id="b43d8-130">document de OpenAPI de démarrage rapide de Hello est un plan d’un document OpenAPI complète. Il requiert plusieurs métadonnées toobe une définition complète de OpenAPI, tels que les objets d’opération et les modèles de réponse.</span><span class="sxs-lookup"><span data-stu-id="b43d8-130">hello quickstart OpenAPI document is an outline of a full OpenAPI doc. It requires more metadata toobe a full OpenAPI definition, such as operation objects and response templates.</span></span>
    1. <span data-ttu-id="b43d8-131">objet d’opération exemple Hello ci-dessous est remplie produit/consomme une section, un objet de paramètre et un objet de réponse.</span><span class="sxs-lookup"><span data-stu-id="b43d8-131">hello sample operation object below has a filled out produces/consumes section, a parameter object, and a response object.</span></span>
    
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
    >  <span data-ttu-id="b43d8-132">x-ms-summary fournit un nom d’affichage dans Logic Apps, Flow et PowerApps.</span><span class="sxs-lookup"><span data-stu-id="b43d8-132">x-ms-summary provides a display name in Logic Apps, Flow, and PowerApps.</span></span>
    >
    > <span data-ttu-id="b43d8-133">Extraire [personnaliser votre définition Swagger pour PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) toolearn plus.</span><span class="sxs-lookup"><span data-stu-id="b43d8-133">Check out [customize your Swagger definition for PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) toolearn more.</span></span>

1. <span data-ttu-id="b43d8-134">Cliquez sur `save` toosave vos modifications ![Ajout d’une définition de modèle](./media/functions-api-definition-getting-started/addingtemplate.png)</span><span class="sxs-lookup"><span data-stu-id="b43d8-134">Click `save` toosave your changes ![Adding Template Definition](./media/functions-api-definition-getting-started/addingtemplate.png)</span></span>

## <span data-ttu-id="b43d8-135"><a name="use-definition"></a>Utilisation de votre définition d’API</span><span class="sxs-lookup"><span data-stu-id="b43d8-135"><a name="use-definition"></a>Using Your API Definition</span></span>
1. <span data-ttu-id="b43d8-136">Copiez votre `API definition URL` et collez-le dans un nouveau tooview d’onglet navigateur votre document OpenAPI brut.</span><span class="sxs-lookup"><span data-stu-id="b43d8-136">Copy your `API definition URL` and paste it into a new browser tab tooview your raw OpenAPI document.</span></span>
1. <span data-ttu-id="b43d8-137">Vous pouvez importer votre numéro tooany OpenAPI des outils de test et l’intégration à l’aide de cette URL.</span><span class="sxs-lookup"><span data-stu-id="b43d8-137">You can import your OpenAPI document tooany number of tools for testing and integration using that URL.</span></span>
    1. <span data-ttu-id="b43d8-138">Nombre de ressources Azure est tooautomatically en mesure des importer à l’aide de votre document OpenAPI hello URL de définition d’API qui est enregistré dans les paramètres de votre application (fonction).</span><span class="sxs-lookup"><span data-stu-id="b43d8-138">Many Azure resources are able tooautomatically import your OpenAPI doc using hello API Definition URL that is saved in your Function application settings.</span></span> <span data-ttu-id="b43d8-139">Dans le cadre de hello `Function` source de définition d’API, nous mettre à jour cette url pour vous.</span><span class="sxs-lookup"><span data-stu-id="b43d8-139">As a part of hello `Function` API definition source, we update that url for you.</span></span>


## <span data-ttu-id="b43d8-140"><a name="test-definition"></a>À l’aide de tootest de l’interface utilisateur de Swagger hello votre définition de l’API</span><span class="sxs-lookup"><span data-stu-id="b43d8-140"><a name="test-definition"></a>Using hello Swagger UI tootest your API definition</span></span>
<span data-ttu-id="b43d8-141">Testez outils intégrés dans la vue de l’interface utilisateur toohello de l’éditeur de définition d’API hello incorporé.</span><span class="sxs-lookup"><span data-stu-id="b43d8-141">There are testing tools built in toohello UI view of hello imbedded API definition editor.</span></span> <span data-ttu-id="b43d8-142">Ajoutez votre clé API et l’utiliser hello `Try this operation` sous chaque méthode.</span><span class="sxs-lookup"><span data-stu-id="b43d8-142">Add your API key, and then use hello `Try this operation` button under each method.</span></span> <span data-ttu-id="b43d8-143">Hello outil utilise vos demandes de hello tooformat définition d’API et des réponses réussies indique que votre définition est correcte.</span><span class="sxs-lookup"><span data-stu-id="b43d8-143">hello tool will use your API Definition tooformat hello requests and successful responses will indicate that your definition is correct.</span></span>

### <a name="steps"></a><span data-ttu-id="b43d8-144">Étapes :</span><span class="sxs-lookup"><span data-stu-id="b43d8-144">Steps:</span></span>

1. <span data-ttu-id="b43d8-145">Copier votre clé d’API de fonction</span><span class="sxs-lookup"><span data-stu-id="b43d8-145">Copy your function API key</span></span>
    1. <span data-ttu-id="b43d8-146">Hello API clé se trouve dans votre fonction de déclenchement HTTP sous `function name` > `Keys` > `Function Keys` 
   ![touche de fonction](./media/functions-api-definition-getting-started/functionkey.png)</span><span class="sxs-lookup"><span data-stu-id="b43d8-146">hello API key can be found in your HTTP Trigger Function under `function name` > `Keys` > `Function Keys`
![Function key](./media/functions-api-definition-getting-started/functionkey.png)</span></span>
1. <span data-ttu-id="b43d8-147">Accédez toohello `API Definition` page.</span><span class="sxs-lookup"><span data-stu-id="b43d8-147">Navigate toohello `API Definition` page.</span></span>
    1. <span data-ttu-id="b43d8-148">Cliquez sur `Authenticate` et ajoutez votre objet de sécurité clé toohello fonction API haut hello.</span><span class="sxs-lookup"><span data-stu-id="b43d8-148">Click `Authenticate` and add your Function API key toohello security object at hello top.</span></span>
  <span data-ttu-id="b43d8-149">![Clé OpenAPI](./media/functions-api-definition-getting-started/definitionTest auth.png)</span><span class="sxs-lookup"><span data-stu-id="b43d8-149">![OpenAPI key](./media/functions-api-definition-getting-started/definitionTest auth.png)</span></span>
1. <span data-ttu-id="b43d8-150">sélectionnez `/api/yourfunctionroute` > `POST`</span><span class="sxs-lookup"><span data-stu-id="b43d8-150">select `/api/yourfunctionroute` > `POST`</span></span>
1. <span data-ttu-id="b43d8-151">Cliquez sur `Try it out` et entrez un nom tootest</span><span class="sxs-lookup"><span data-stu-id="b43d8-151">Click `Try it out` and enter a name tootest</span></span>
1. <span data-ttu-id="b43d8-152">Vous devriez voir un résultat RÉUSSITE sous `Pretty`
![Test de définition d’API](./media/functions-api-definition-getting-started/definitionTest.png)</span><span class="sxs-lookup"><span data-stu-id="b43d8-152">You should see a SUCCESS result under `Pretty`
![API Definition test](./media/functions-api-definition-getting-started/definitionTest.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="b43d8-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b43d8-153">Next steps</span></span>
* [<span data-ttu-id="b43d8-154">Définition OpenAPI dans Vue d’ensemble de Functions</span><span class="sxs-lookup"><span data-stu-id="b43d8-154">OpenAPI Definition in Functions Overview</span></span>](functions-api-definition.md)
  * <span data-ttu-id="b43d8-155">Lire la documentation complète de hello pour plus d’informations sur la prise en charge OpenAPI.</span><span class="sxs-lookup"><span data-stu-id="b43d8-155">Read hello full documentation for more info on OpenAPI support.</span></span>
* [<span data-ttu-id="b43d8-156">Référence du développeur Azure Functions</span><span class="sxs-lookup"><span data-stu-id="b43d8-156">Azure Functions developer reference</span></span>](functions-reference.md)  
  * <span data-ttu-id="b43d8-157">Référence du programmeur pour le codage de fonctions et la définition de déclencheurs et de liaisons.</span><span class="sxs-lookup"><span data-stu-id="b43d8-157">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="b43d8-158">Référentiel GitHub Azure Functions</span><span class="sxs-lookup"><span data-stu-id="b43d8-158">Azure Functions GitHub repository</span></span>](https://github.com/Azure/Azure-Functions/)
  * <span data-ttu-id="b43d8-159">Découvrez hello fonctions GitHub toogive nous des commentaires sur la version préliminaire de hello API définition prise en charge.</span><span class="sxs-lookup"><span data-stu-id="b43d8-159">Check out hello Functions GitHub toogive us feedback on hello API definition support preview!</span></span> <span data-ttu-id="b43d8-160">Créer un problème GitHub pour ce que vous voulez toosee mis à jour.</span><span class="sxs-lookup"><span data-stu-id="b43d8-160">Make a GitHub issue for anything you'd like toosee updated.</span></span>
