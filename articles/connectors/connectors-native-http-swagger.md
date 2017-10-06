---
title: points de terminaison REST aaaCall avec HTTP + Swagger connecteur pour Azure Logic Apps | Documents Microsoft
description: "Connecter les points de terminaison tooREST à partir d’applications logique via Swagger hello HTTP + Swagger connecteur"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: eccfd87c-c5fe-4cf7-b564-9752775fd667
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: baaa57689ff41fcd052f9d86086e36619ddec46e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-http--swagger-action"></a><span data-ttu-id="26fb1-103">Prise en main Bonjour HTTP + Swagger action</span><span class="sxs-lookup"><span data-stu-id="26fb1-103">Get started with hello HTTP + Swagger action</span></span>

<span data-ttu-id="26fb1-104">Vous pouvez créer un point de terminaison REST de tooany connecteur de première classe via un [Swagger document](https://swagger.io) lorsque vous utilisez Bonjour HTTP + Swagger action dans votre workflow d’application logique.</span><span class="sxs-lookup"><span data-stu-id="26fb1-104">You can create a first-class connector tooany REST endpoint through a [Swagger document](https://swagger.io) when you use hello HTTP + Swagger action in your logic app workflow.</span></span> <span data-ttu-id="26fb1-105">Vous pouvez également étendre logique applications toocall n’importe quel point de terminaison REST avec une expérience de concepteur d’application logique de première classe.</span><span class="sxs-lookup"><span data-stu-id="26fb1-105">You can also extend logic apps toocall any REST endpoint with a first-class Logic App Designer experience.</span></span>

<span data-ttu-id="26fb1-106">toolearn toocreate des applications de logique avec les connecteurs, voir [créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="26fb1-106">toolearn how toocreate logic apps with connectors, see [Create a new logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-http--swagger-as-a-trigger-or-an-action"></a><span data-ttu-id="26fb1-107">Utiliser HTTP + Swagger comme un déclencheur ou d’une action</span><span class="sxs-lookup"><span data-stu-id="26fb1-107">Use HTTP + Swagger as a trigger or an action</span></span>

<span data-ttu-id="26fb1-108">Bonjour HTTP + travail trigger et action de Swagger hello même hello [action HTTP](connectors-native-http.md) mais aussi fournir une meilleure expérience dans le Concepteur d’application logique en exposant la structure de hello API et les sorties de hello [Swagger métadonnées](https://swagger.io) .</span><span class="sxs-lookup"><span data-stu-id="26fb1-108">hello HTTP + Swagger trigger and action work hello same as hello [HTTP action](connectors-native-http.md) but provide a better experience in Logic App Designer by exposing hello API structure and outputs from hello [Swagger metadata](https://swagger.io).</span></span> <span data-ttu-id="26fb1-109">Vous pouvez également utiliser Bonjour HTTP + Swagger connecteur comme un déclencheur.</span><span class="sxs-lookup"><span data-stu-id="26fb1-109">You can also use hello HTTP + Swagger connector as a trigger.</span></span> <span data-ttu-id="26fb1-110">Si vous voulez tooimplement un déclencheur d’interrogation, procèdent d’interrogation de hello qui est décrit dans [créer personnalisé API toocall autres API, les services et les systèmes à partir d’applications de logique](../logic-apps/logic-apps-create-api-app.md#polling-triggers).</span><span class="sxs-lookup"><span data-stu-id="26fb1-110">If you want tooimplement a polling trigger, follow hello polling pattern that's described in [Create custom APIs toocall other APIs, services, and systems from logic apps](../logic-apps/logic-apps-create-api-app.md#polling-triggers).</span></span>

<span data-ttu-id="26fb1-111">En savoir plus sur les [déclencheurs et actions de l’application logique](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="26fb1-111">Learn more about [logic app triggers and actions](connectors-overview.md).</span></span>

<span data-ttu-id="26fb1-112">Voici un exemple de comment toouse hello HTTP + Swagger opération en tant qu’action dans un flux de travail dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="26fb1-112">Here's an example of how toouse hello HTTP + Swagger operation as an action in a workflow in a logic app.</span></span>

1. <span data-ttu-id="26fb1-113">Sélectionnez hello **nouvelle étape** bouton.</span><span class="sxs-lookup"><span data-stu-id="26fb1-113">Select hello **New Step** button.</span></span>
2. <span data-ttu-id="26fb1-114">Sélectionnez **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="26fb1-114">Select **Add an action**.</span></span>
3. <span data-ttu-id="26fb1-115">Dans la zone de recherche action hello, tapez **swagger** hello de toolist HTTP + Swagger action.</span><span class="sxs-lookup"><span data-stu-id="26fb1-115">In hello action search box, type **swagger** toolist hello HTTP + Swagger action.</span></span>
   
    ![Sélectionnez une action HTTP + Swagger](./media/connectors-native-http-swagger/using-action-1.png)
4. <span data-ttu-id="26fb1-117">Tapez l’URL hello pour un document de Swagger :</span><span class="sxs-lookup"><span data-stu-id="26fb1-117">Type hello URL for a Swagger document:</span></span>
   
   * <span data-ttu-id="26fb1-118">toowork de hello Concepteur d’application logique, hello URL doit être un point de terminaison HTTPS et disposer CORS.</span><span class="sxs-lookup"><span data-stu-id="26fb1-118">toowork from hello Logic App Designer, hello URL must be an HTTPS endpoint and have CORS enabled.</span></span>
   * <span data-ttu-id="26fb1-119">Si le document de Swagger hello ne répond pas à cette exigence, vous pouvez utiliser [le stockage Azure avec CORS activé](#hosting-swagger-from-storage) document de hello toostore.</span><span class="sxs-lookup"><span data-stu-id="26fb1-119">If hello Swagger document doesn't meet this requirement, you can use [Azure Storage with CORS enabled](#hosting-swagger-from-storage) toostore hello document.</span></span>
5. <span data-ttu-id="26fb1-120">Cliquez sur **suivant** tooread et rendu à partir de Swagger document hello.</span><span class="sxs-lookup"><span data-stu-id="26fb1-120">Click **Next** tooread and render from hello Swagger document.</span></span>
6. <span data-ttu-id="26fb1-121">Ajoutez tous les paramètres qui sont requis pour l’appel de hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="26fb1-121">Add in any parameters that are required for hello HTTP call.</span></span>
   
    ![Exécuter l’action HTTP](./media/connectors-native-http-swagger/using-action-2.png)
7. <span data-ttu-id="26fb1-123">toosave et publier votre application logique, cliquez sur **enregistrer** sur la barre d’outils.</span><span class="sxs-lookup"><span data-stu-id="26fb1-123">toosave and publish your logic app, click **Save** on designer toolbar.</span></span>

### <a name="host-swagger-from-azure-storage"></a><span data-ttu-id="26fb1-124">Héberger un document Swagger à partir d'Azure Storage</span><span class="sxs-lookup"><span data-stu-id="26fb1-124">Host Swagger from Azure Storage</span></span>
<span data-ttu-id="26fb1-125">Vous souhaiterez peut-être tooreference un document de Swagger qui n’est pas hébergé, ou qui ne répond pas aux exigences de sécurité et de cross-origin de hello pour le concepteur hello.</span><span class="sxs-lookup"><span data-stu-id="26fb1-125">You might want tooreference a Swagger document that's not hosted, or that doesn't meet hello security and cross-origin requirements for hello designer.</span></span> <span data-ttu-id="26fb1-126">tooresolve ce problème, vous pouvez stocker des documents de Swagger hello dans le stockage Azure et activer CORS tooreference hello document.</span><span class="sxs-lookup"><span data-stu-id="26fb1-126">tooresolve this issue, you can store hello Swagger document in Azure Storage and enable CORS tooreference hello document.</span></span>  

<span data-ttu-id="26fb1-127">Voici hello étapes toocreate, configurer et stocker les documents de Swagger dans le stockage Azure :</span><span class="sxs-lookup"><span data-stu-id="26fb1-127">Here are hello steps toocreate, configure, and store Swagger documents in Azure Storage:</span></span>

1. <span data-ttu-id="26fb1-128">[Créez un compte de stockage Azure avec un stockage d'objets blob Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="26fb1-128">[Create an Azure storage account with Azure Blob storage](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="26fb1-129">tooperform cette étape, définir des autorisations trop**accès Public**.</span><span class="sxs-lookup"><span data-stu-id="26fb1-129">tooperform this step, set permissions too**Public Access**.</span></span>

2. <span data-ttu-id="26fb1-130">Activer l’objet blob de hello CORS.</span><span class="sxs-lookup"><span data-stu-id="26fb1-130">Enable CORS on hello blob.</span></span> 

   <span data-ttu-id="26fb1-131">tooautomatically configurer ce paramètre, vous pouvez utiliser [ce script PowerShell](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).</span><span class="sxs-lookup"><span data-stu-id="26fb1-131">tooautomatically configure this setting, you can use [this PowerShell script](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).</span></span>

3. <span data-ttu-id="26fb1-132">Télécharger l’objet blob de hello Swagger fichier toohello.</span><span class="sxs-lookup"><span data-stu-id="26fb1-132">Upload hello Swagger file toohello blob.</span></span> 

   <span data-ttu-id="26fb1-133">Vous pouvez effectuer cette étape à partir de hello [portail Azure](https://portal.azure.com) ou à partir d’un outil tel que [Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="26fb1-133">You can perform this step from hello [Azure portal](https://portal.azure.com) or from a tool like [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

4. <span data-ttu-id="26fb1-134">Faire référence à un document de toohello lien HTTPS dans le stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="26fb1-134">Reference an HTTPS link toohello document in Azure Blob storage.</span></span> 

   <span data-ttu-id="26fb1-135">lien de Hello utilise ce format :</span><span class="sxs-lookup"><span data-stu-id="26fb1-135">hello link uses this format:</span></span>

   `https://*storageAccountName*.blob.core.windows.net/*container*/*filename*`

## <a name="technical-details"></a><span data-ttu-id="26fb1-136">Détails techniques</span><span class="sxs-lookup"><span data-stu-id="26fb1-136">Technical details</span></span>
<span data-ttu-id="26fb1-137">Voici les détails de hello pour hello déclencheurs et les actions que cette HTTP + Swagger connecteur prend en charge.</span><span class="sxs-lookup"><span data-stu-id="26fb1-137">Following are hello details for hello triggers and actions that this HTTP + Swagger connector supports.</span></span>

## <a name="http--swagger-triggers"></a><span data-ttu-id="26fb1-138">Déclencheurs HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="26fb1-138">HTTP + Swagger triggers</span></span>
<span data-ttu-id="26fb1-139">Un déclencheur est un événement qui peut être utilisé toostart hello flux de travail qui est défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="26fb1-139">A trigger is an event that can be used toostart hello workflow that's defined in a logic app.</span></span> [<span data-ttu-id="26fb1-140">En savoir plus sur les déclencheurs.</span><span class="sxs-lookup"><span data-stu-id="26fb1-140">Learn more about triggers.</span></span>](connectors-overview.md) <span data-ttu-id="26fb1-141">Hello HTTP + Swagger connecteur a un déclencheur.</span><span class="sxs-lookup"><span data-stu-id="26fb1-141">hello HTTP + Swagger connector has one trigger.</span></span>

| <span data-ttu-id="26fb1-142">Déclencheur</span><span class="sxs-lookup"><span data-stu-id="26fb1-142">Trigger</span></span> | <span data-ttu-id="26fb1-143">Description</span><span class="sxs-lookup"><span data-stu-id="26fb1-143">Description</span></span> |
| --- | --- |
| <span data-ttu-id="26fb1-144">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="26fb1-144">HTTP + Swagger</span></span> |<span data-ttu-id="26fb1-145">Effectuer un appel HTTP et retournent le contenu de la réponse hello</span><span class="sxs-lookup"><span data-stu-id="26fb1-145">Make an HTTP call and return hello response content</span></span> |

## <a name="http--swagger-actions"></a><span data-ttu-id="26fb1-146">Actions HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="26fb1-146">HTTP + Swagger actions</span></span>
<span data-ttu-id="26fb1-147">Une action est une opération est effectuée par le flux de travail hello défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="26fb1-147">An action is an operation that's carried out by hello workflow that's defined in a logic app.</span></span> [<span data-ttu-id="26fb1-148">En savoir plus sur les actions.</span><span class="sxs-lookup"><span data-stu-id="26fb1-148">Learn more about actions.</span></span>](connectors-overview.md) <span data-ttu-id="26fb1-149">Hello HTTP + Swagger connecteur a une seule action possible.</span><span class="sxs-lookup"><span data-stu-id="26fb1-149">hello HTTP + Swagger connector has one possible action.</span></span>

| <span data-ttu-id="26fb1-150">Action</span><span class="sxs-lookup"><span data-stu-id="26fb1-150">Action</span></span> | <span data-ttu-id="26fb1-151">Description</span><span class="sxs-lookup"><span data-stu-id="26fb1-151">Description</span></span> |
| --- | --- |
| <span data-ttu-id="26fb1-152">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="26fb1-152">HTTP + Swagger</span></span> |<span data-ttu-id="26fb1-153">Effectuer un appel HTTP et retournent le contenu de la réponse hello</span><span class="sxs-lookup"><span data-stu-id="26fb1-153">Make an HTTP call and return hello response content</span></span> |

### <a name="action-details"></a><span data-ttu-id="26fb1-154">Détails de l’action</span><span class="sxs-lookup"><span data-stu-id="26fb1-154">Action details</span></span>
<span data-ttu-id="26fb1-155">Hello HTTP + Swagger connecteur est fourni avec une seule action possible.</span><span class="sxs-lookup"><span data-stu-id="26fb1-155">hello HTTP + Swagger connector comes with one possible action.</span></span> <span data-ttu-id="26fb1-156">Voici quelques informations sur chacune des actions de hello, des champs d’entrée obligatoires et facultatifs et hello correspondant détails de sortie qui sont associés à leur utilisation.</span><span class="sxs-lookup"><span data-stu-id="26fb1-156">Following is information about each of hello actions, their required and optional input fields, and hello corresponding output details that are associated with their usage.</span></span>

#### <a name="http--swagger"></a><span data-ttu-id="26fb1-157">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="26fb1-157">HTTP + Swagger</span></span>
<span data-ttu-id="26fb1-158">Faites une demande HTTP sortante avec assistance des métadonnées Swagger.</span><span class="sxs-lookup"><span data-stu-id="26fb1-158">Make an HTTP outbound request with assistance of Swagger metadata.</span></span>
<span data-ttu-id="26fb1-159">Un astérisque (*) signifie un champ obligatoire.</span><span class="sxs-lookup"><span data-stu-id="26fb1-159">An asterisk (*) means a required field.</span></span>

| <span data-ttu-id="26fb1-160">Nom complet</span><span class="sxs-lookup"><span data-stu-id="26fb1-160">Display name</span></span> | <span data-ttu-id="26fb1-161">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="26fb1-161">Property name</span></span> | <span data-ttu-id="26fb1-162">Description</span><span class="sxs-lookup"><span data-stu-id="26fb1-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="26fb1-163">Method (Méthode)*</span><span class="sxs-lookup"><span data-stu-id="26fb1-163">Method*</span></span> |<span data-ttu-id="26fb1-164">method</span><span class="sxs-lookup"><span data-stu-id="26fb1-164">method</span></span> |<span data-ttu-id="26fb1-165">Toouse du verbe HTTP.</span><span class="sxs-lookup"><span data-stu-id="26fb1-165">HTTP verb toouse.</span></span> |
| <span data-ttu-id="26fb1-166">URI*</span><span class="sxs-lookup"><span data-stu-id="26fb1-166">URI*</span></span> |<span data-ttu-id="26fb1-167">URI</span><span class="sxs-lookup"><span data-stu-id="26fb1-167">uri</span></span> |<span data-ttu-id="26fb1-168">URI de demande de hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="26fb1-168">URI for hello HTTP request.</span></span> |
| <span data-ttu-id="26fb1-169">headers</span><span class="sxs-lookup"><span data-stu-id="26fb1-169">Headers</span></span> |<span data-ttu-id="26fb1-170">headers</span><span class="sxs-lookup"><span data-stu-id="26fb1-170">headers</span></span> |<span data-ttu-id="26fb1-171">Un objet JSON de tooinclude des en-têtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="26fb1-171">A JSON object of HTTP headers tooinclude.</span></span> |
| <span data-ttu-id="26fb1-172">Corps</span><span class="sxs-lookup"><span data-stu-id="26fb1-172">Body</span></span> |<span data-ttu-id="26fb1-173">body</span><span class="sxs-lookup"><span data-stu-id="26fb1-173">body</span></span> |<span data-ttu-id="26fb1-174">Hello corps de la demande HTTP.</span><span class="sxs-lookup"><span data-stu-id="26fb1-174">hello HTTP request body.</span></span> |
| <span data-ttu-id="26fb1-175">Authentification</span><span class="sxs-lookup"><span data-stu-id="26fb1-175">Authentication</span></span> |<span data-ttu-id="26fb1-176">authentication</span><span class="sxs-lookup"><span data-stu-id="26fb1-176">authentication</span></span> |<span data-ttu-id="26fb1-177">Toouse d’authentification pour la demande.</span><span class="sxs-lookup"><span data-stu-id="26fb1-177">Authentication toouse for request.</span></span> <span data-ttu-id="26fb1-178">Pour plus d’informations, consultez hello [connecteur HTTP](connectors-native-http.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="26fb1-178">For more information, see hello [HTTP connector](connectors-native-http.md#authentication).</span></span> |

<span data-ttu-id="26fb1-179">**Détails des résultats**</span><span class="sxs-lookup"><span data-stu-id="26fb1-179">**Output details**</span></span>

<span data-ttu-id="26fb1-180">Réponse HTTP</span><span class="sxs-lookup"><span data-stu-id="26fb1-180">HTTP response</span></span>

| <span data-ttu-id="26fb1-181">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="26fb1-181">Property Name</span></span> | <span data-ttu-id="26fb1-182">Type de données</span><span class="sxs-lookup"><span data-stu-id="26fb1-182">Data type</span></span> | <span data-ttu-id="26fb1-183">Description</span><span class="sxs-lookup"><span data-stu-id="26fb1-183">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="26fb1-184">headers</span><span class="sxs-lookup"><span data-stu-id="26fb1-184">Headers</span></span> |<span data-ttu-id="26fb1-185">objet</span><span class="sxs-lookup"><span data-stu-id="26fb1-185">object</span></span> |<span data-ttu-id="26fb1-186">En-têtes de réponse</span><span class="sxs-lookup"><span data-stu-id="26fb1-186">Response headers</span></span> |
| <span data-ttu-id="26fb1-187">Corps</span><span class="sxs-lookup"><span data-stu-id="26fb1-187">Body</span></span> |<span data-ttu-id="26fb1-188">objet</span><span class="sxs-lookup"><span data-stu-id="26fb1-188">object</span></span> |<span data-ttu-id="26fb1-189">Objet Réponse</span><span class="sxs-lookup"><span data-stu-id="26fb1-189">Response object</span></span> |
| <span data-ttu-id="26fb1-190">Code d’état</span><span class="sxs-lookup"><span data-stu-id="26fb1-190">Status Code</span></span> |<span data-ttu-id="26fb1-191">int</span><span class="sxs-lookup"><span data-stu-id="26fb1-191">int</span></span> |<span data-ttu-id="26fb1-192">Code d'état HTTP</span><span class="sxs-lookup"><span data-stu-id="26fb1-192">HTTP status code</span></span> |

### <a name="http-responses"></a><span data-ttu-id="26fb1-193">Réponses HTTP</span><span class="sxs-lookup"><span data-stu-id="26fb1-193">HTTP responses</span></span>
<span data-ttu-id="26fb1-194">Lorsque vous élaborez des appels toovarious actions, vous pouvez obtenir certaines réponses.</span><span class="sxs-lookup"><span data-stu-id="26fb1-194">When making calls toovarious actions, you might get certain responses.</span></span> <span data-ttu-id="26fb1-195">La table ci-dessous indique les réponses correspondantes et leurs descriptions.</span><span class="sxs-lookup"><span data-stu-id="26fb1-195">Following is a table that outlines corresponding responses and descriptions.</span></span>

| <span data-ttu-id="26fb1-196">Name</span><span class="sxs-lookup"><span data-stu-id="26fb1-196">Name</span></span> | <span data-ttu-id="26fb1-197">Description</span><span class="sxs-lookup"><span data-stu-id="26fb1-197">Description</span></span> |
| --- | --- |
| <span data-ttu-id="26fb1-198">200</span><span class="sxs-lookup"><span data-stu-id="26fb1-198">200</span></span> |<span data-ttu-id="26fb1-199">OK</span><span class="sxs-lookup"><span data-stu-id="26fb1-199">OK</span></span> |
| <span data-ttu-id="26fb1-200">202</span><span class="sxs-lookup"><span data-stu-id="26fb1-200">202</span></span> |<span data-ttu-id="26fb1-201">Acceptée</span><span class="sxs-lookup"><span data-stu-id="26fb1-201">Accepted</span></span> |
| <span data-ttu-id="26fb1-202">400</span><span class="sxs-lookup"><span data-stu-id="26fb1-202">400</span></span> |<span data-ttu-id="26fb1-203">Demande incorrecte</span><span class="sxs-lookup"><span data-stu-id="26fb1-203">Bad request</span></span> |
| <span data-ttu-id="26fb1-204">401</span><span class="sxs-lookup"><span data-stu-id="26fb1-204">401</span></span> |<span data-ttu-id="26fb1-205">Non autorisé</span><span class="sxs-lookup"><span data-stu-id="26fb1-205">Unauthorized</span></span> |
| <span data-ttu-id="26fb1-206">403</span><span class="sxs-lookup"><span data-stu-id="26fb1-206">403</span></span> |<span data-ttu-id="26fb1-207">Interdit</span><span class="sxs-lookup"><span data-stu-id="26fb1-207">Forbidden</span></span> |
| <span data-ttu-id="26fb1-208">404</span><span class="sxs-lookup"><span data-stu-id="26fb1-208">404</span></span> |<span data-ttu-id="26fb1-209">Introuvable</span><span class="sxs-lookup"><span data-stu-id="26fb1-209">Not Found</span></span> |
| <span data-ttu-id="26fb1-210">500</span><span class="sxs-lookup"><span data-stu-id="26fb1-210">500</span></span> |<span data-ttu-id="26fb1-211">Erreur interne du serveur.</span><span class="sxs-lookup"><span data-stu-id="26fb1-211">Internal server error.</span></span> <span data-ttu-id="26fb1-212">Une erreur inconnue s’est produite.</span><span class="sxs-lookup"><span data-stu-id="26fb1-212">Unknown error occurred.</span></span> |

- - -
## <a name="next-steps"></a><span data-ttu-id="26fb1-213">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="26fb1-213">Next steps</span></span>

* [<span data-ttu-id="26fb1-214">Créer une application logique</span><span class="sxs-lookup"><span data-stu-id="26fb1-214">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="26fb1-215">Rechercher d’autres connecteurs</span><span class="sxs-lookup"><span data-stu-id="26fb1-215">Find other connectors</span></span>](apis-list.md)