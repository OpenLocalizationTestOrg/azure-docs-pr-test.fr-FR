---
title: "aaaCreate une API sans serveur à l’aide des fonctions de Azure | Documents Microsoft"
description: "Comment toocreate une API sans serveur à l’aide des fonctions d’Azure"
services: functions
author: mattchenderson
manager: erikre
ms.service: functions
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: tutorial
ms.date: 05/04/2017
ms.author: mahender
ms.custom: mvc
ms.openlocfilehash: 877e3b229d5477fc5fec594ccd284fb55d7f3c07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-serverless-api-using-azure-functions"></a><span data-ttu-id="cc7dd-103">Créer une API sans serveur à l’aide d’Azure Functions</span><span class="sxs-lookup"><span data-stu-id="cc7dd-103">Create a serverless API using Azure Functions</span></span>

<span data-ttu-id="cc7dd-104">Dans ce didacticiel, vous allez apprendre comment les fonctions Azure vous permet de toobuild des API hautement évolutives.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-104">In this tutorial you will learn how Azure Functions allows you toobuild highly-scalable APIs.</span></span> <span data-ttu-id="cc7dd-105">Fonctions Azure est fourni avec une collection intégrée HTTP et les liaisons qui rendent tooauthor facile à un point de terminaison dans une variété de langues, y compris Node.JS, c# et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-105">Azure Functions comes with a collection of built-in HTTP triggers and bindings which make it easy tooauthor an endpoint in a variety of languages, including Node.JS, C#, and more.</span></span> <span data-ttu-id="cc7dd-106">Dans ce didacticiel, vous allez personnaliser un HTTP déclencheur toohandle des actions spécifiques dans votre conception de l’API.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-106">In this tutorial, you will customize an HTTP trigger toohandle specific actions in your API design.</span></span> <span data-ttu-id="cc7dd-107">Vous allez également préparer le développement de votre API, l’intégration avec Proxys Azure Functions et la configuration d’API factices.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-107">You will also prepare for growing your API by integrating it with Azure Functions Proxies and setting up mock APIs.</span></span> <span data-ttu-id="cc7dd-108">Tout ceci s’effectue sur hello fonctions sans environnement de calcul, donc vous n’avez pas tooworry sur la mise à l’échelle des ressources, vous pouvez vous concentrer uniquement sur votre logique de l’API.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-108">All of this is accomplished on top of hello Functions serverless compute environment, so you don't have tooworry about scaling resources - you can just focus on your API logic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc7dd-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="cc7dd-109">Prerequisites</span></span> 

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

<span data-ttu-id="cc7dd-110">fonction qui en résulte Hello servira pour reste hello de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-110">hello resulting function will be used for hello rest of this tutorial.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="cc7dd-111">Connectez-vous à tooAzure</span><span class="sxs-lookup"><span data-stu-id="cc7dd-111">Sign in tooAzure</span></span>

<span data-ttu-id="cc7dd-112">Ouvrez hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-112">Open hello Azure portal.</span></span> <span data-ttu-id="cc7dd-113">toodo, connectez-vous trop[https://portal.azure.com](https://portal.azure.com) avec votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-113">toodo this, sign in too[https://portal.azure.com](https://portal.azure.com) with your Azure account.</span></span>

## <a name="customize-your-http-function"></a><span data-ttu-id="cc7dd-114">Personnaliser une fonction HTTP</span><span class="sxs-lookup"><span data-stu-id="cc7dd-114">Customize your HTTP function</span></span>

<span data-ttu-id="cc7dd-115">Par défaut, votre fonction a déclenché l’HTTP est configuré tooaccept n’importe quelle méthode HTTP.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-115">By default, your HTTP-triggered function is configured tooaccept any HTTP method.</span></span> <span data-ttu-id="cc7dd-116">Il existe également une URL par défaut sous forme de hello `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-116">There is also a default URL of hello form `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`.</span></span> <span data-ttu-id="cc7dd-117">Si vous avez suivi hello quickstart, puis `<funcname>` probablement similaire à « HttpTriggerJS1 ».</span><span class="sxs-lookup"><span data-stu-id="cc7dd-117">If you followed hello quickstart, then `<funcname>` probably looks something like "HttpTriggerJS1".</span></span> <span data-ttu-id="cc7dd-118">Dans cette section, vous allez modifier les demandes de tooGET uniquement hello fonction toorespond sur `/api/hello` Router à la place.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-118">In this section, you will modify hello function toorespond only tooGET requests against `/api/hello` route instead.</span></span> 

<span data-ttu-id="cc7dd-119">Accédez à fonction tooyour Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-119">Navigate tooyour function in hello Azure portal.</span></span> <span data-ttu-id="cc7dd-120">Sélectionnez **intégrer** Bonjour barre de navigation gauche.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-120">Select **Integrate** in hello left navigation.</span></span>

![Personnalisation d’une fonction HTTP](./media/functions-create-serverless-api/customizing-http.png)

<span data-ttu-id="cc7dd-122">Utilisez les paramètres de déclencheur HTTP tel que spécifié dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-122">Use the HTTP trigger settings as specified in hello table.</span></span>

| <span data-ttu-id="cc7dd-123">Champ</span><span class="sxs-lookup"><span data-stu-id="cc7dd-123">Field</span></span> | <span data-ttu-id="cc7dd-124">Exemple de valeur</span><span class="sxs-lookup"><span data-stu-id="cc7dd-124">Sample value</span></span> | <span data-ttu-id="cc7dd-125">Description</span><span class="sxs-lookup"><span data-stu-id="cc7dd-125">Description</span></span> |
|---|---|---|
| <span data-ttu-id="cc7dd-126">Méthodes HTTP autorisées</span><span class="sxs-lookup"><span data-stu-id="cc7dd-126">Allowed HTTP methods</span></span> | <span data-ttu-id="cc7dd-127">Méthodes sélectionnées</span><span class="sxs-lookup"><span data-stu-id="cc7dd-127">Selected methods</span></span> | <span data-ttu-id="cc7dd-128">Détermine quelles méthodes HTTP peuvent être utilisé tooinvoke cette fonction</span><span class="sxs-lookup"><span data-stu-id="cc7dd-128">Determines what HTTP methods may be used tooinvoke this function</span></span> |
| <span data-ttu-id="cc7dd-129">Méthodes HTTP sélectionnées</span><span class="sxs-lookup"><span data-stu-id="cc7dd-129">Selected HTTP methods</span></span> | <span data-ttu-id="cc7dd-130">GET</span><span class="sxs-lookup"><span data-stu-id="cc7dd-130">GET</span></span> | <span data-ttu-id="cc7dd-131">Autorise uniquement sélectionné toobe de méthodes HTTP utilisées tooinvoke cette fonction</span><span class="sxs-lookup"><span data-stu-id="cc7dd-131">Allows only selected HTTP methods toobe used tooinvoke this function</span></span> |
| <span data-ttu-id="cc7dd-132">Modèle d’itinéraire</span><span class="sxs-lookup"><span data-stu-id="cc7dd-132">Route template</span></span> | <span data-ttu-id="cc7dd-133">/hello</span><span class="sxs-lookup"><span data-stu-id="cc7dd-133">/hello</span></span> | <span data-ttu-id="cc7dd-134">Détermine l’itinéraire est tooinvoke utilisé cette fonction</span><span class="sxs-lookup"><span data-stu-id="cc7dd-134">Determines what route is used tooinvoke this function</span></span> |

<span data-ttu-id="cc7dd-135">Notez que vous n’avez pas inclus hello `/api` baser le préfixe de chemin d’accès dans le modèle d’itinéraire hello, comme cela est géré par un paramètre global.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-135">Note that you did not include hello `/api` base path prefix in hello route template, as this is handled by a global setting.</span></span>

<span data-ttu-id="cc7dd-136">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-136">Click **Save**.</span></span>

<span data-ttu-id="cc7dd-137">Pour plus d’informations sur la personnalisation des fonctions HTTP, consultez la page [Liaisons HTTP et de webhooks d’Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).</span><span class="sxs-lookup"><span data-stu-id="cc7dd-137">You can learn more about customizing HTTP functions in [Azure Functions HTTP and webhook bindings](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).</span></span>

### <a name="test-your-api"></a><span data-ttu-id="cc7dd-138">Tester l’API</span><span class="sxs-lookup"><span data-stu-id="cc7dd-138">Test your API</span></span>

<span data-ttu-id="cc7dd-139">Ensuite, testez votre toosee fonction qu’il fonctionne avec la surface de l’API nouvelle hello.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-139">Next, test your function toosee it working with hello new API surface.</span></span>

<span data-ttu-id="cc7dd-140">Accédez de page de développement toohello arrière en cliquant sur le nom de la fonction hello Bonjour barre de navigation gauche.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-140">Navigate back toohello development page by clicking on hello function's name in hello left navigation.</span></span>

<span data-ttu-id="cc7dd-141">Cliquez sur **obtenir l’URL de la fonction** et copier l’URL de hello.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-141">Click **Get function URL** and copy hello URL.</span></span> <span data-ttu-id="cc7dd-142">Vous devez voir qu’il utilise hello `/api/hello` Router maintenant.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-142">You should see that it uses hello `/api/hello` route now.</span></span>

<span data-ttu-id="cc7dd-143">Copier l’URL hello dans un nouvel onglet de navigateur ou de votre client REST préféré.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-143">Copy hello URL into a new browser tab or your preferred REST client.</span></span> <span data-ttu-id="cc7dd-144">Les navigateurs utilisent GET par défaut.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-144">Browsers will use GET by default.</span></span>

<span data-ttu-id="cc7dd-145">Exécuter la fonction hello et vérifiez qu’il fonctionne.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-145">Run hello function and confirm that it is working.</span></span> <span data-ttu-id="cc7dd-146">Vous devrez peut-être le paramètre « name » de hello tooprovide comme un code de démarrage rapide de requête chaîne toosatisfy hello.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-146">You may need tooprovide hello "name" parameter as a query string toosatisfy hello quickstart code.</span></span>

<span data-ttu-id="cc7dd-147">Vous pouvez aussi essayer d’appeler le point de terminaison hello avec tooconfirm de méthode HTTP autre que la fonction hello n’est pas exécutée.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-147">You can also try calling hello endpoint with another HTTP method tooconfirm that hello function is not executed.</span></span> <span data-ttu-id="cc7dd-148">Pour ce faire, vous devez toouse un client REST, telles que cURL, Postman ou Fiddler.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-148">For this, you will need toouse a REST client, such as cURL, Postman, or Fiddler.</span></span>

## <a name="proxies-overview"></a><span data-ttu-id="cc7dd-149">Vue d’ensemble des proxys</span><span class="sxs-lookup"><span data-stu-id="cc7dd-149">Proxies overview</span></span>

<span data-ttu-id="cc7dd-150">Dans la section suivante de hello, vous affichera votre API via un proxy.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-150">In hello next section, you will surface your API through a proxy.</span></span> <span data-ttu-id="cc7dd-151">Les proxys de fonctions Azure est une fonctionnalité d’aperçu qui vous permet de tooforward demande tooother des ressources.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-151">Azure Functions Proxies is a preview feature that allows you tooforward requests tooother resources.</span></span> <span data-ttu-id="cc7dd-152">Vous définissez comme un point de terminaison HTTP avec le déclencheur d’HTTP, mais au lieu d’écrire le code tooexecute lorsque ce point de terminaison est appelée, vous fournissez une implémentation à distance de tooa URL.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-152">You define an HTTP endpoint just like with HTTP trigger, but instead of writing code tooexecute when that endpoint is called, you provide a URL tooa remote implementation.</span></span> <span data-ttu-id="cc7dd-153">Cela vous permet de toocompose API plusieurs sources en une seule API qui est facile pour les clients tooconsume.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-153">This allows you toocompose multiple API sources into a single API surface which is easy for clients tooconsume.</span></span> <span data-ttu-id="cc7dd-154">Cela est particulièrement utile si vous souhaitez que votre API en tant que microservices toobuild.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-154">This is particularly useful if you wish toobuild your API as microservices.</span></span>

<span data-ttu-id="cc7dd-155">Un proxy peut pointer tooany HTTP ressources, telles que :</span><span class="sxs-lookup"><span data-stu-id="cc7dd-155">A proxy can point tooany HTTP resource, such as:</span></span>
- <span data-ttu-id="cc7dd-156">Azure Functions</span><span class="sxs-lookup"><span data-stu-id="cc7dd-156">Azure Functions</span></span> 
- <span data-ttu-id="cc7dd-157">Applications API dans [Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)</span><span class="sxs-lookup"><span data-stu-id="cc7dd-157">API apps in [Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)</span></span>
- <span data-ttu-id="cc7dd-158">Conteneurs Docker dans [App Service sur Linux](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)</span><span class="sxs-lookup"><span data-stu-id="cc7dd-158">Docker containers in [App Service on Linux](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)</span></span>
- <span data-ttu-id="cc7dd-159">Toute autre API hébergée</span><span class="sxs-lookup"><span data-stu-id="cc7dd-159">Any other hosted API</span></span>

<span data-ttu-id="cc7dd-160">toolearn en savoir plus sur les serveurs proxy, consultez [utilisation de proxys de fonctions Azure (aperçu)].</span><span class="sxs-lookup"><span data-stu-id="cc7dd-160">toolearn more about proxies, see [Working with Azure Functions Proxies (preview)].</span></span>

## <a name="create-your-first-proxy"></a><span data-ttu-id="cc7dd-161">Créer un premier proxy</span><span class="sxs-lookup"><span data-stu-id="cc7dd-161">Create your first proxy</span></span>

<span data-ttu-id="cc7dd-162">Dans cette section, vous allez créer un nouveau proxy qui sert comme un serveur frontal tooyour API globale.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-162">In this section, you will create a new proxy which serves as a frontend tooyour overall API.</span></span> 

### <a name="setting-up-hello-frontend-environment"></a><span data-ttu-id="cc7dd-163">Création d’un environnement de serveur frontal hello</span><span class="sxs-lookup"><span data-stu-id="cc7dd-163">Setting up hello frontend environment</span></span>

<span data-ttu-id="cc7dd-164">Répétez les étapes de hello trop[créer une application de la fonction](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) toocreate une nouvelle application de la fonction dans laquelle vous allez créer votre proxy.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-164">Repeat hello steps too[Create a function app](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) toocreate a new function app in which you will create your proxy.</span></span> <span data-ttu-id="cc7dd-165">Cette nouvelle application servira de serveur frontal de hello pour notre API et application de fonction hello que vous modifiiez précédemment servira d’un serveur principal.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-165">This new app will serve as hello frontend for our API, and hello function app you were previously editing will serve as a backend.</span></span>

<span data-ttu-id="cc7dd-166">Accédez tooyour nouvelle application frontale fonction dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-166">Navigate tooyour new frontend function app in hello portal.</span></span>

<span data-ttu-id="cc7dd-167">Sélectionnez **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-167">Select **Settings**.</span></span> <span data-ttu-id="cc7dd-168">Puis basculer **activer des proxys de fonctions Azure (aperçu)** trop « sur ».</span><span class="sxs-lookup"><span data-stu-id="cc7dd-168">Then toggle **Enable Azure Functions Proxies (preview)** too"On".</span></span>

<span data-ttu-id="cc7dd-169">Sélectionnez **Paramètres de la plateforme** et choisissez **Paramètres de l’application**.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-169">Select **Platform Settings** and choose **Application Settings**.</span></span>

<span data-ttu-id="cc7dd-170">Faites défiler la liste trop**paramètres de l’application** et créer un nouveau paramètre avec la clé « HELLO_HOST ».</span><span class="sxs-lookup"><span data-stu-id="cc7dd-170">Scroll down too**App settings** and create a new setting with key "HELLO_HOST".</span></span> <span data-ttu-id="cc7dd-171">Définir son hôte toohello de valeur de votre application de la fonction principale, telles que `<YourApp>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-171">Set its value toohello host of your backend function app, such as `<YourApp>.azurewebsites.net`.</span></span> <span data-ttu-id="cc7dd-172">Il s’agit de partie de hello URL que vous avez copiée précédemment lorsque vous testez votre fonction HTTP.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-172">This is part of hello URL that you copied earlier when testing your HTTP function.</span></span> <span data-ttu-id="cc7dd-173">Vous devez faire référence à ce paramètre dans la configuration de hello plus tard.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-173">You'll reference this setting in hello configuration later.</span></span>

> [!NOTE] 
> <span data-ttu-id="cc7dd-174">Paramètres de l’application sont recommandées pour hello hôte configuration tooprevent une dépendance codée en dur l’environnement pour le proxy de hello.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-174">App settings are recommended for hello host configuration tooprevent a hard-coded environment dependency for hello proxy.</span></span> <span data-ttu-id="cc7dd-175">À l’aide des paramètres de l’application signifie que vous pouvez déplacer la configuration du proxy hello entre les environnements et paramètres d’application propres à l’environnement hello seront appliqués.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-175">Using app settings means that you can move hello proxy configuration between environments, and hello environment-specific app settings will be applied.</span></span>

<span data-ttu-id="cc7dd-176">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-176">Click **Save**.</span></span>

### <a name="creating-a-proxy-on-hello-frontend"></a><span data-ttu-id="cc7dd-177">Création d’un proxy sur le serveur frontal de hello</span><span class="sxs-lookup"><span data-stu-id="cc7dd-177">Creating a proxy on hello frontend</span></span>

<span data-ttu-id="cc7dd-178">Accédez tooyour arrière frontal fonction application dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-178">Navigate back tooyour frontend function app in hello portal.</span></span>

<span data-ttu-id="cc7dd-179">Dans la navigation de gauche hello, cliquez sur hello signe plus le suivant '+' trop « Proxy (version préliminaire) ».</span><span class="sxs-lookup"><span data-stu-id="cc7dd-179">In hello left-hand navigation, click hello plus sign '+' next too"Proxies (preview)".</span></span>

![Création d’un proxy](./media/functions-create-serverless-api/creating-proxy.png)

<span data-ttu-id="cc7dd-181">Utiliser les paramètres de proxy tel que spécifié dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-181">Use proxy settings as specified in hello table.</span></span>

| <span data-ttu-id="cc7dd-182">Champ</span><span class="sxs-lookup"><span data-stu-id="cc7dd-182">Field</span></span> | <span data-ttu-id="cc7dd-183">Exemple de valeur</span><span class="sxs-lookup"><span data-stu-id="cc7dd-183">Sample value</span></span> | <span data-ttu-id="cc7dd-184">Description</span><span class="sxs-lookup"><span data-stu-id="cc7dd-184">Description</span></span> |
|---|---|---|
| <span data-ttu-id="cc7dd-185">Nom</span><span class="sxs-lookup"><span data-stu-id="cc7dd-185">Name</span></span> | <span data-ttu-id="cc7dd-186">HelloProxy</span><span class="sxs-lookup"><span data-stu-id="cc7dd-186">HelloProxy</span></span> | <span data-ttu-id="cc7dd-187">Nom convivial utilisé uniquement à des fins de gestion.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-187">A friendly name used only for management</span></span> |
| <span data-ttu-id="cc7dd-188">Modèle d’itinéraire</span><span class="sxs-lookup"><span data-stu-id="cc7dd-188">Route template</span></span> | <span data-ttu-id="cc7dd-189">/api/hello</span><span class="sxs-lookup"><span data-stu-id="cc7dd-189">/api/hello</span></span> | <span data-ttu-id="cc7dd-190">Détermine l’itinéraire est tooinvoke utilisé ce proxy</span><span class="sxs-lookup"><span data-stu-id="cc7dd-190">Determines what route is used tooinvoke this proxy</span></span> |
| <span data-ttu-id="cc7dd-191">URL principale</span><span class="sxs-lookup"><span data-stu-id="cc7dd-191">Backend URL</span></span> | <span data-ttu-id="cc7dd-192">https://%HELLO_HOST%/api/hello</span><span class="sxs-lookup"><span data-stu-id="cc7dd-192">https://%HELLO_HOST%/api/hello</span></span> | <span data-ttu-id="cc7dd-193">Spécifie la demande de hello toowhich hello point de terminaison doit être utilisé comme proxy</span><span class="sxs-lookup"><span data-stu-id="cc7dd-193">Specifies hello endpoint toowhich hello request should be proxied</span></span> |

<span data-ttu-id="cc7dd-194">Notez que les serveurs proxy ne fournit pas de hello `/api` préfixe de chemin d’accès de base et ce doit être inclus dans le modèle d’itinéraire hello.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-194">Note that Proxies does not provide hello `/api` base path prefix, and this must be included in hello route template.</span></span>

<span data-ttu-id="cc7dd-195">Hello `%HELLO_HOST%` syntaxe fait référence le paramètre d’application hello vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-195">hello `%HELLO_HOST%` syntax will reference hello app setting you created earlier.</span></span> <span data-ttu-id="cc7dd-196">Hello résolu QU'URL pointe tooyour (fonction) d’origine.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-196">hello resolved URL will point tooyour original function.</span></span>

<span data-ttu-id="cc7dd-197">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-197">Click **Create**.</span></span>

<span data-ttu-id="cc7dd-198">Vous pouvez essayer votre nouveau proxy par copie hello URL de Proxy et de le tester dans le navigateur de hello ou avec votre client HTTP favori.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-198">You can try out your new proxy by copying hello Proxy URL and testing it in hello browser or with your favorite HTTP client.</span></span>

## <a name="create-a-mock-api"></a><span data-ttu-id="cc7dd-199">Créer une API factice</span><span class="sxs-lookup"><span data-stu-id="cc7dd-199">Create a mock API</span></span>

<span data-ttu-id="cc7dd-200">Ensuite, vous allez utiliser un toocreate proxy une API fictive pour votre solution.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-200">Next, you will use a proxy toocreate a mock API for your solution.</span></span> <span data-ttu-id="cc7dd-201">Cela permet le développement client tooprogress, sans avoir besoin de back-end hello entièrement implémentée.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-201">This allows client development tooprogress, without needing hello backend fully implemented.</span></span> <span data-ttu-id="cc7dd-202">Dans le développement, créez une nouvelle application de fonction qui prend en charge cette logique et rediriger votre tooit proxy.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-202">Later in development, you could create a new function app which supports this logic and redirect your proxy tooit.</span></span>

<span data-ttu-id="cc7dd-203">toocreate cette simulation d’API, nous allons créer un nouveau proxy, cette fois à l’aide de hello [éditeur de Service d’applications](https://github.com/projectkudu/kudu/wiki/App-Service-Editor).</span><span class="sxs-lookup"><span data-stu-id="cc7dd-203">toocreate this mock API, we will create a new proxy, this time using hello [App Service Editor](https://github.com/projectkudu/kudu/wiki/App-Service-Editor).</span></span> <span data-ttu-id="cc7dd-204">tooget démarré, accédez à application de fonction tooyour dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-204">tooget started, navigate tooyour function app in hello portal.</span></span> <span data-ttu-id="cc7dd-205">Sélectionnez **Fonctionnalités de la plateforme** et **Éditeur App Service**.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-205">Select **Platform features** and find **App Service Editor**.</span></span> <span data-ttu-id="cc7dd-206">Cliquer sur ce bouton, hello App Service éditeur s’ouvre dans un nouvel onglet.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-206">Clicking this will open hello App Service Editor in a new tab.</span></span>

<span data-ttu-id="cc7dd-207">Sélectionnez `proxies.json` Bonjour barre de navigation gauche.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-207">Select `proxies.json` in hello left navigation.</span></span> <span data-ttu-id="cc7dd-208">Il s’agit de fichier hello qui stocke la configuration hello pour tous les proxys.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-208">This is hello file which stores hello configuration for all of your proxies.</span></span> <span data-ttu-id="cc7dd-209">Si vous utilisez une des hello [fonctions des méthodes de déploiement](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), c’est le fichier hello que vous voulez gérer dans le contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-209">If you use one of hello [Functions deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), this is hello file you will maintain in source control.</span></span> <span data-ttu-id="cc7dd-210">toolearn en savoir plus sur ce fichier, consultez [configuration avancée de proxys](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).</span><span class="sxs-lookup"><span data-stu-id="cc7dd-210">toolearn more about this file, see [Proxies advanced configuration](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).</span></span>

<span data-ttu-id="cc7dd-211">Si vous avez suivi jusqu'à présent, votre proxies.json doit ressembler à hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="cc7dd-211">If you've followed along so far, your proxies.json should look like hello following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        }
    }
}
```

<span data-ttu-id="cc7dd-212">Vous allez maintenant ajouter votre API factice.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-212">Next you'll add your mock API.</span></span> <span data-ttu-id="cc7dd-213">Remplacez votre fichier proxies.json par hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="cc7dd-213">Replace your proxies.json file with hello following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        },
        "GetUserByName" : {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/users/{username}"
            },
            "responseOverrides": {
                "response.statusCode": "200",
                "response.headers.Content-Type" : "application/json",
                "response.body": {
                    "name": "{username}",
                    "description": "Awesome developer and master of serverless APIs",
                    "skills": [
                        "Serverless",
                        "APIs",
                        "Azure",
                        "Cloud"
                    ]
                }
            }
        }
    }
}
```

<span data-ttu-id="cc7dd-214">Cela ajoute un nouveau proxy, « GetUserByName », sans propriété de backendUri hello.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-214">This adds a new proxy, "GetUserByName", without hello backendUri property.</span></span> <span data-ttu-id="cc7dd-215">Au lieu d’appeler une autre ressource, il modifie la réponse par défaut hello proxys à l’aide d’une substitution de la réponse.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-215">Instead of calling another resource, it modifies hello default response from Proxies using a response override.</span></span> <span data-ttu-id="cc7dd-216">Les substitutions de demandes et de réponses peuvent également être utilisées en association avec une URL principale.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-216">Request and response overrides can also be used in conjunction with a backend URL.</span></span> <span data-ttu-id="cc7dd-217">Cela est particulièrement utile lorsque le système hérité proxy tooa, où vous devrez peut-être toomodify en-têtes, les paramètres de requête, etc. toolearn plus d’informations sur les remplacements de demande et de réponse, consultez [modification des demandes et réponses de proxys](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).</span><span class="sxs-lookup"><span data-stu-id="cc7dd-217">This is particularly useful when proxying tooa legacy system, where you might need toomodify headers, query parameters, etc. toolearn more about request and response overrides, see [Modifying requests and responses in Proxies](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).</span></span>

<span data-ttu-id="cc7dd-218">Tester votre API fictive en appelant hello `/api/users/{username}` point de terminaison à l’aide d’un navigateur ou votre client REST favori.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-218">Test your mock API by calling hello `/api/users/{username}` endpoint using a browser or your favorite REST client.</span></span> <span data-ttu-id="cc7dd-219">Être vraiment tooreplace _{username}_ avec une valeur de chaîne représentant un nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-219">Be sure tooreplace _{username}_ with a string value representing a username.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc7dd-220">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cc7dd-220">Next steps</span></span>

<span data-ttu-id="cc7dd-221">Dans ce didacticiel, vous avez appris comment toobuild et personnaliser une API sur les fonctions d’Azure.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-221">In this tutorial, you learned how toobuild and customize an API on Azure Functions.</span></span> <span data-ttu-id="cc7dd-222">Vous avez également appris comment toobring plusieurs API, y compris mocks, ensemble comme une surface API unifiée.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-222">You also learned how toobring multiple APIs, including mocks, together as a unified API surface.</span></span> <span data-ttu-id="cc7dd-223">Vous pouvez utiliser ces toobuild techniques des API complexes, tout en s’exécutant sur hello sans modèle fourni par les fonctions Azure de calcul.</span><span class="sxs-lookup"><span data-stu-id="cc7dd-223">You can use these techniques toobuild out APIs of any complexity, all while running on hello serverless compute model provided by Azure Functions.</span></span>

<span data-ttu-id="cc7dd-224">Hello références suivantes peuvent être utiles lorsque vous développez votre API supplémentaire :</span><span class="sxs-lookup"><span data-stu-id="cc7dd-224">hello following references may be helpful as you develop your API further:</span></span>

- [<span data-ttu-id="cc7dd-225">Liaisons HTTP et webhook Azure Functions</span><span class="sxs-lookup"><span data-stu-id="cc7dd-225">Azure Functions HTTP and webhook bindings</span></span>](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook)
- <span data-ttu-id="cc7dd-226">[utilisation de proxys de fonctions Azure (aperçu)]</span><span class="sxs-lookup"><span data-stu-id="cc7dd-226">[Working with Azure Functions Proxies (preview)]</span></span>
- [<span data-ttu-id="cc7dd-227">Documenter une API Azure Functions (préversion)</span><span class="sxs-lookup"><span data-stu-id="cc7dd-227">Documenting an Azure Functions API (preview)</span></span>](https://docs.microsoft.com/azure/azure-functions/functions-api-definition-getting-started)


[Create your first function]: https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function
[utilisation de proxys de fonctions Azure (aperçu)]: https://docs.microsoft.com/azure/azure-functions/functions-proxies
