---
title: Utilisation des proxys dans Azure Functions | Microsoft Docs
description: "Présentation de l’utilisation de Azure Functions Proxies"
services: functions
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/11/2017
ms.author: mahender
ms.openlocfilehash: 102e54627a8fee721d3ed85e86a8009e706bb5b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="work-with-azure-functions-proxies-preview"></a><span data-ttu-id="e4838-103">Utilisation de Azure Functions Proxies (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="e4838-103">Work with Azure Functions Proxies (preview)</span></span>

> [!NOTE] 
> <span data-ttu-id="e4838-104">Azure Functions Proxies est actuellement disponible en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="e4838-104">Azure Functions Proxies is currently in preview.</span></span> <span data-ttu-id="e4838-105">La version préliminaire est proposée gratuitement, mais une facturation standard s’applique à l’exécution des proxys.</span><span class="sxs-lookup"><span data-stu-id="e4838-105">It is free while in preview, but standard Functions billing applies to proxy executions.</span></span> <span data-ttu-id="e4838-106">Pour plus d’informations, consultez [Tarification d’Azure Functions](https://azure.microsoft.com/pricing/details/functions/).</span><span class="sxs-lookup"><span data-stu-id="e4838-106">For more information, see [Azure Functions pricing](https://azure.microsoft.com/pricing/details/functions/).</span></span>

<span data-ttu-id="e4838-107">Cet article vous explique comment configurer et utiliser Azure Functions Proxies.</span><span class="sxs-lookup"><span data-stu-id="e4838-107">This article explains how to configure and work with Azure Functions Proxies.</span></span> <span data-ttu-id="e4838-108">Cette fonctionnalité vous permet de spécifier des points de terminaison sur votre Function App implémentés par une autre ressource.</span><span class="sxs-lookup"><span data-stu-id="e4838-108">With this feature, you can specify endpoints on your function app that are implemented by another resource.</span></span> <span data-ttu-id="e4838-109">Vous pouvez utiliser ces proxys pour diviser une API de grande taille en plusieurs applications Function (comme dans une architecture microservice), tout en continuant à présenter une surface API unique aux clients.</span><span class="sxs-lookup"><span data-stu-id="e4838-109">You can use these proxies to break a large API into multiple function apps (as in a microservice architecture), while still presenting a single API surface for clients.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]


## <span data-ttu-id="e4838-110"><a name="enable"></a>Activation d’Azure Functions Proxies</span><span class="sxs-lookup"><span data-stu-id="e4838-110"><a name="enable"></a>Enable Azure Functions Proxies</span></span>

<span data-ttu-id="e4838-111">Les proxies ne sont pas activés par défaut.</span><span class="sxs-lookup"><span data-stu-id="e4838-111">Proxies are not enabled by default.</span></span> <span data-ttu-id="e4838-112">Vous pouvez créer des proxys lorsque la fonctionnalité est désactivée, mais ils ne s’exécuteront pas.</span><span class="sxs-lookup"><span data-stu-id="e4838-112">You can create proxies while the feature is disabled, but they will not execute.</span></span> <span data-ttu-id="e4838-113">Pour activer les proxys, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="e4838-113">To enable proxies, do the following:</span></span>

1. <span data-ttu-id="e4838-114">Ouvrez le [portail Azure] et accédez à votre Function App.</span><span class="sxs-lookup"><span data-stu-id="e4838-114">Open the [Azure portal], and then go to your function app.</span></span>
2. <span data-ttu-id="e4838-115">Sélectionnez **Paramètres Function App**.</span><span class="sxs-lookup"><span data-stu-id="e4838-115">Select **Function app settings**.</span></span>
3. <span data-ttu-id="e4838-116">Réglez **Activer les proxys Azure Functions (préversion)** sur **Activé**.</span><span class="sxs-lookup"><span data-stu-id="e4838-116">Switch **Enable Azure Functions Proxies (preview)** to **On**.</span></span>

<span data-ttu-id="e4838-117">Vous pouvez également revenir ici pour mettre à jour le runtime proxy lorsque de nouvelles fonctionnalités sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="e4838-117">You can also return here to update the proxy runtime as new features become available.</span></span>


## <span data-ttu-id="e4838-118"><a name="create"></a>Création d’un proxy</span><span class="sxs-lookup"><span data-stu-id="e4838-118"><a name="create"></a>Create a proxy</span></span>

<span data-ttu-id="e4838-119">Cette section vous explique comment créer un proxy dans le portail Functions.</span><span class="sxs-lookup"><span data-stu-id="e4838-119">This section shows you how to create a proxy in the Functions portal.</span></span>

1. <span data-ttu-id="e4838-120">Ouvrez le [portail Azure] et accédez à votre Function App.</span><span class="sxs-lookup"><span data-stu-id="e4838-120">Open the [Azure portal], and then go to your function app.</span></span>
2. <span data-ttu-id="e4838-121">Dans le volet gauche, sélectionnez **Nouveau proxy**.</span><span class="sxs-lookup"><span data-stu-id="e4838-121">In the left pane, select **New proxy**.</span></span>
3. <span data-ttu-id="e4838-122">Entrez un nom pour votre proxy.</span><span class="sxs-lookup"><span data-stu-id="e4838-122">Provide a name for your proxy.</span></span>
4. <span data-ttu-id="e4838-123">Configurez le point de terminaison exposé sur cette Function App en spécifiant le **modèle de routage** et les **méthodes HTTP**.</span><span class="sxs-lookup"><span data-stu-id="e4838-123">Configure the endpoint that's exposed on this function app by specifying the **route template** and **HTTP methods**.</span></span> <span data-ttu-id="e4838-124">Ces paramètres se comportent selon les règles des [déclencheurs HTTP].</span><span class="sxs-lookup"><span data-stu-id="e4838-124">These parameters behave according to the rules for [HTTP triggers].</span></span>
5. <span data-ttu-id="e4838-125">Définissez l’**URL principale** sur un autre point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="e4838-125">Set the **backend URL** to another endpoint.</span></span> <span data-ttu-id="e4838-126">Il peut s’agir d’une fonction dans une autre Function App ou bien de n’importe quelle autre API.</span><span class="sxs-lookup"><span data-stu-id="e4838-126">This endpoint could be a function in another function app, or it could be any other API.</span></span> <span data-ttu-id="e4838-127">La valeur ne doit pas nécessairement être statique et peut faire référence aux [paramètres de l’application] et aux [paramètres de la demande client d’origine].</span><span class="sxs-lookup"><span data-stu-id="e4838-127">The value does not need to be static, and it can reference [application settings] and [parameters from the original client request].</span></span>
6. <span data-ttu-id="e4838-128">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="e4838-128">Click **Create**.</span></span>

<span data-ttu-id="e4838-129">Votre proxy existe désormais sous la forme d’un nouveau point de terminaison de votre application de fonction.</span><span class="sxs-lookup"><span data-stu-id="e4838-129">Your proxy now exists as a new endpoint on your function app.</span></span> <span data-ttu-id="e4838-130">Du point de vue du client, cela équivaut à un HttpTrigger dans Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="e4838-130">From a client perspective, it is equivalent to an HttpTrigger in Azure Functions.</span></span> <span data-ttu-id="e4838-131">Vous pouvez essayer votre nouveau proxy en copiant l’URL de proxy et en le testant avec le client HTTP de votre choix.</span><span class="sxs-lookup"><span data-stu-id="e4838-131">You can try out your new proxy by copying the Proxy URL and testing it with your favorite HTTP client.</span></span>

## <span data-ttu-id="e4838-132"><a name="modify-requests-responses"></a>Modification de demandes et de réponses</span><span class="sxs-lookup"><span data-stu-id="e4838-132"><a name="modify-requests-responses"></a>Modify requests and responses</span></span>

<span data-ttu-id="e4838-133">La fonctionnalité Proxys Azure Functions vous permet de modifier les demandes envoyées sur le serveur principal et les réponses reçues de ce dernier.</span><span class="sxs-lookup"><span data-stu-id="e4838-133">With Azure Functions Proxies, you can modify requests to and responses from the back end.</span></span> <span data-ttu-id="e4838-134">Ces transformations peuvent impliquer l’utilisation de variables, comme décrit dans la section [Utilisation de variables].</span><span class="sxs-lookup"><span data-stu-id="e4838-134">These transformations can use variables as defined in [Use variables].</span></span>

### <span data-ttu-id="e4838-135"><a name="modify-backend-request"></a>Modification de la demande du serveur principal</span><span class="sxs-lookup"><span data-stu-id="e4838-135"><a name="modify-backend-request"></a>Modify the back-end request</span></span>

<span data-ttu-id="e4838-136">Par défaut, la demande du serveur principal est initialisée comme une copie de la demande d’origine.</span><span class="sxs-lookup"><span data-stu-id="e4838-136">By default, the back-end request is initialized as a copy of the original request.</span></span> <span data-ttu-id="e4838-137">Outre la définition de l’URL du serveur principal, vous pouvez apporter des modifications à la méthode HTTP, aux en-têtes et aux paramètres de chaîne de requête.</span><span class="sxs-lookup"><span data-stu-id="e4838-137">In addition to setting the back-end URL, you can make changes to the HTTP method, headers, and query string parameters.</span></span> <span data-ttu-id="e4838-138">Les valeurs modifiées peuvent faire référence aux [paramètres de l’application] et aux [paramètres de la demande client d’origine].</span><span class="sxs-lookup"><span data-stu-id="e4838-138">The modified values can reference [application settings] and [parameters from the original client request].</span></span>

<span data-ttu-id="e4838-139">Il n’est actuellement pas possible de modifier les demandes du serveur principal via un portail.</span><span class="sxs-lookup"><span data-stu-id="e4838-139">Currently, there is no portal experience for modifying back-end requests.</span></span> <span data-ttu-id="e4838-140">Consultez la section [Définition d’un objet requestOverrides] pour savoir comment appliquer cette fonctionnalité avec un fichier proxies.json.</span><span class="sxs-lookup"><span data-stu-id="e4838-140">To learn how to apply this capability from proxies.json, see [Define a requestOverrides object].</span></span>

### <span data-ttu-id="e4838-141"><a name="modify-response"></a>Modification de la réponse</span><span class="sxs-lookup"><span data-stu-id="e4838-141"><a name="modify-response"></a>Modify the response</span></span>

<span data-ttu-id="e4838-142">Par défaut, la réponse client est initialisée comme une copie de la réponse du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="e4838-142">By default, the client response is initialized as a copy of the back-end response.</span></span> <span data-ttu-id="e4838-143">Vous pouvez apporter des modifications au code d’état, au motif, aux en-têtes et au corps.</span><span class="sxs-lookup"><span data-stu-id="e4838-143">You can make changes to the response's status code, reason phrase, headers, and body.</span></span> <span data-ttu-id="e4838-144">Les valeurs modifiées peuvent faire référence aux [paramètres de l’application], aux [paramètres de la demande client d’origine] et aux [paramètres de la réponse du serveur principal].</span><span class="sxs-lookup"><span data-stu-id="e4838-144">The modified values can reference [application settings], [parameters from the original client request], and [parameters from the back-end response].</span></span>

<span data-ttu-id="e4838-145">Il n’est actuellement pas possible de modifier les réponses.</span><span class="sxs-lookup"><span data-stu-id="e4838-145">Currently, there is no portal experience for modifying responses.</span></span> <span data-ttu-id="e4838-146">Consultez la section [Définition d’un objet responseOverrides] pour savoir comment appliquer cette fonctionnalité avec un fichier proxies.json.</span><span class="sxs-lookup"><span data-stu-id="e4838-146">To learn how to apply this capability from proxies.json, see [Define a responseOverrides object].</span></span>

## <span data-ttu-id="e4838-147"><a name="using-variables"></a>Utilisation de variables</span><span class="sxs-lookup"><span data-stu-id="e4838-147"><a name="using-variables"></a>Use variables</span></span>

<span data-ttu-id="e4838-148">La configuration d’un proxy ne doit pas nécessairement être statique.</span><span class="sxs-lookup"><span data-stu-id="e4838-148">The configuration for a proxy does not need to be static.</span></span> <span data-ttu-id="e4838-149">Vous pouvez définir comme condition l’utilisation des variables de la demande d’origine, de la réponse du serveur principal ou des paramètres de l’application.</span><span class="sxs-lookup"><span data-stu-id="e4838-149">You can condition it to use variables from the original request, the back-end response, or application settings.</span></span>

### <span data-ttu-id="e4838-150"><a name="request-parameters"></a>Référencement des paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="e4838-150"><a name="request-parameters"></a>Reference request parameters</span></span>

<span data-ttu-id="e4838-151">Les paramètres de la demande peuvent être entrés au niveau de la propriété d’URL du serveur principal ou peuvent être utilisés lors de la modification des demandes et des réponses.</span><span class="sxs-lookup"><span data-stu-id="e4838-151">You can use request parameters as inputs to the back-end URL property or as part of modifying requests and responses.</span></span> <span data-ttu-id="e4838-152">Certains paramètres peuvent être liés à partir du modèle de routage spécifié dans la configuration du proxy de base, alors que d’autres proviennent des propriétés de la demande entrante.</span><span class="sxs-lookup"><span data-stu-id="e4838-152">Some parameters can be bound from the route template that's specified in the base proxy configuration, and others can come from properties of the incoming request.</span></span>

#### <a name="route-template-parameters"></a><span data-ttu-id="e4838-153">Paramètres de modèle de routage</span><span class="sxs-lookup"><span data-stu-id="e4838-153">Route template parameters</span></span>
<span data-ttu-id="e4838-154">Les paramètres utilisés dans le modèle de routage peuvent être référencés par nom.</span><span class="sxs-lookup"><span data-stu-id="e4838-154">Parameters that are used in the route template are available to be referenced by name.</span></span> <span data-ttu-id="e4838-155">Les noms des paramètres sont placés entre accolades ({}).</span><span class="sxs-lookup"><span data-stu-id="e4838-155">The parameter names are enclosed in braces ({}).</span></span>

<span data-ttu-id="e4838-156">Par exemple, si un proxy dispose d’un modèle de routage du type `/pets/{petId}`, l’URL du serveur principal peut inclure la valeur de `{petId}`, comme dans `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`.</span><span class="sxs-lookup"><span data-stu-id="e4838-156">For example, if a proxy has a route template, such as `/pets/{petId}`, the back-end URL can include the value of `{petId}`, as in `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`.</span></span> <span data-ttu-id="e4838-157">Si le modèle de routage prend fin dans un caractère générique, tel que `/api/{*restOfPath}`, la valeur `{restOfPath}` est une chaîne représentant les autres segments de chemin d’accès de la demande entrante.</span><span class="sxs-lookup"><span data-stu-id="e4838-157">If the route template terminates in a wildcard, such as `/api/{*restOfPath}`, the value `{restOfPath}` is a string representation of the remaining path segments from the incoming request.</span></span>

#### <a name="additional-request-parameters"></a><span data-ttu-id="e4838-158">Paramètres de demande supplémentaires</span><span class="sxs-lookup"><span data-stu-id="e4838-158">Additional request parameters</span></span>
<span data-ttu-id="e4838-159">Outre les paramètres de modèle de routage, les valeurs suivantes peuvent être utilisées dans les valeurs de configuration :</span><span class="sxs-lookup"><span data-stu-id="e4838-159">In addition to the route template parameters, the following values can be used in config values:</span></span>

* <span data-ttu-id="e4838-160">**{request.method}** : méthode HTTP utilisée lors de la demande d’origine.</span><span class="sxs-lookup"><span data-stu-id="e4838-160">**{request.method}**: The HTTP method that's used on the original request.</span></span>
* <span data-ttu-id="e4838-161">**{request.headers.\<HeaderName\>}** : un en-tête qui peut être lu à partir de la demande d’origine.</span><span class="sxs-lookup"><span data-stu-id="e4838-161">**{request.headers.\<HeaderName\>}**: A header that can be read from the original request.</span></span> <span data-ttu-id="e4838-162">Remplacez *\<HeaderName\>* par le nom de l’en-tête que vous souhaitez lire.</span><span class="sxs-lookup"><span data-stu-id="e4838-162">Replace *\<HeaderName\>* with the name of the header that you want to read.</span></span> <span data-ttu-id="e4838-163">Si l’en-tête n’est pas inclus dans la demande, la valeur sera une chaîne vide.</span><span class="sxs-lookup"><span data-stu-id="e4838-163">If the header is not included on the request, the value will be the empty string.</span></span>
* <span data-ttu-id="e4838-164">**{request.querystring.\<ParameterName\>}** : un paramètre de chaîne de requête qui peut être lu à partir de la demande d’origine.</span><span class="sxs-lookup"><span data-stu-id="e4838-164">**{request.querystring.\<ParameterName\>}**: A query string parameter that can be read from the original request.</span></span> <span data-ttu-id="e4838-165">Remplacez *\<ParameterName\>* par le nom de l’en-tête que vous souhaitez lire.</span><span class="sxs-lookup"><span data-stu-id="e4838-165">Replace *\<ParameterName\>* with the name of the parameter that you want to read.</span></span> <span data-ttu-id="e4838-166">Si le paramètre n’est pas inclus dans la demande, la valeur sera une chaîne vide.</span><span class="sxs-lookup"><span data-stu-id="e4838-166">If the parameter is not included on the request, the value will be the empty string.</span></span>

### <span data-ttu-id="e4838-167"><a name="response-parameters"></a>Référencement des paramètres de réponse du serveur principal</span><span class="sxs-lookup"><span data-stu-id="e4838-167"><a name="response-parameters"></a>Reference back-end response parameters</span></span>

<span data-ttu-id="e4838-168">Les paramètres de réponse peuvent être utilisés lors de la modification de la réponse au client.</span><span class="sxs-lookup"><span data-stu-id="e4838-168">Response parameters can be used as part of modifying the response to the client.</span></span> <span data-ttu-id="e4838-169">Les valeurs suivantes peuvent être utilisées dans la configuration :</span><span class="sxs-lookup"><span data-stu-id="e4838-169">The following values can be used in config values:</span></span>

* <span data-ttu-id="e4838-170">**{backend.response.statusCode}** : code d’état HTTP renvoyé dans la réponse du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="e4838-170">**{backend.response.statusCode}**: The HTTP status code that's returned on the back-end response.</span></span>
* <span data-ttu-id="e4838-171">**{backend.response.statusReason}** : motif HTTP renvoyé dans la réponse du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="e4838-171">**{backend.response.statusReason}**: The HTTP reason phrase that's returned on the back-end response.</span></span>
* <span data-ttu-id="e4838-172">**{backend.response.headers.\<HeaderName\>}** : en-tête pouvant être lu à partir de la réponse du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="e4838-172">**{backend.response.headers.\<HeaderName\>}**: A header that can be read from the back-end response.</span></span> <span data-ttu-id="e4838-173">Remplacez *\<HeaderName\>* par le nom de l’en-tête que vous souhaitez lire.</span><span class="sxs-lookup"><span data-stu-id="e4838-173">Replace *\<HeaderName\>* with the name of the header you want to read.</span></span> <span data-ttu-id="e4838-174">Si l’en-tête n’est pas inclus dans la demande, la valeur sera une chaîne vide.</span><span class="sxs-lookup"><span data-stu-id="e4838-174">If the header is not included on the request, the value will be the empty string.</span></span>

### <span data-ttu-id="e4838-175"><a name="use-appsettings"></a>Référencement des paramètres de l’application</span><span class="sxs-lookup"><span data-stu-id="e4838-175"><a name="use-appsettings"></a>Reference application settings</span></span>

<span data-ttu-id="e4838-176">Vous pouvez également référencer les [paramètres de l’application définis pour la Function App](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) en mettant le nom du paramètre entre signes de pourcentage (%).</span><span class="sxs-lookup"><span data-stu-id="e4838-176">You can also reference [application settings defined for the function app](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) by surrounding the setting name with percent signs (%).</span></span>

<span data-ttu-id="e4838-177">Par exemple, dans une URL de serveur principal de *https://%ORDER_PROCESSING_HOST%/api/orders*, %ORDER_PROCESSING_HOST% sera remplacé par la valeur du paramètre ORDER_PROCESSING_HOST.</span><span class="sxs-lookup"><span data-stu-id="e4838-177">For example, a back-end URL of *https://%ORDER_PROCESSING_HOST%/api/orders* would have "%ORDER_PROCESSING_HOST%" replaced with the value of the ORDER_PROCESSING_HOST setting.</span></span>

> [!TIP] 
> <span data-ttu-id="e4838-178">Utilisez des paramètres d’application pour les hôtes de serveur principal lorsque vous avez plusieurs déploiements ou environnements de test.</span><span class="sxs-lookup"><span data-stu-id="e4838-178">Use application settings for back-end hosts when you have multiple deployments or test environments.</span></span> <span data-ttu-id="e4838-179">De cette façon, vous avez l’assurance de toujours parler au serveur principal adapté à cet environnement.</span><span class="sxs-lookup"><span data-stu-id="e4838-179">That way, you can make sure that you are always talking to the right back end for that environment.</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="e4838-180">Configuration avancée</span><span class="sxs-lookup"><span data-stu-id="e4838-180">Advanced configuration</span></span>

<span data-ttu-id="e4838-181">Les serveurs proxy que vous configurez sont stockés dans un fichier proxies.json, situé à la racine d’un répertoire de Function App.</span><span class="sxs-lookup"><span data-stu-id="e4838-181">The proxies that you configure are stored in a proxies.json file, which is located in the root of a function app directory.</span></span> <span data-ttu-id="e4838-182">Vous pouvez modifier manuellement ce fichier et le déployer dans le cadre de votre application lors de l’utilisation de l’une des [méthodes de déploiement](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) prises en charge par Functions.</span><span class="sxs-lookup"><span data-stu-id="e4838-182">You can manually edit this file and deploy it as part of your app when you use any of the [deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) that Functions supports.</span></span> <span data-ttu-id="e4838-183">La fonctionnalité doit être [activée](#enable) pour permettre le traitement du fichier.</span><span class="sxs-lookup"><span data-stu-id="e4838-183">The feature must be [enabled](#enable) for the file to be processed.</span></span> 

> [!TIP] 
> <span data-ttu-id="e4838-184">Si vous n’avez pas défini l’une des méthodes de déploiement, vous pouvez également utiliser le fichier proxies.json dans le portail.</span><span class="sxs-lookup"><span data-stu-id="e4838-184">If you have not set up one of the deployment methods, you can also work with the proxies.json file in the portal.</span></span> <span data-ttu-id="e4838-185">Accédez à votre Function App et sélectionnez **Fonctionnalités de la plateforme**, puis **Éditeur App Service**.</span><span class="sxs-lookup"><span data-stu-id="e4838-185">Go to your function app, select **Platform features**, and then select **App Service Editor**.</span></span> <span data-ttu-id="e4838-186">Cela vous permettra d’afficher l’ensemble de la structure de fichiers de votre Function App et d’y apporter des modifications.</span><span class="sxs-lookup"><span data-stu-id="e4838-186">By doing so, you can view the entire file structure of your function app and then make changes.</span></span>

<span data-ttu-id="e4838-187">Proxies.json est défini par un objet proxy, composé de proxys nommés et de leurs définitions.</span><span class="sxs-lookup"><span data-stu-id="e4838-187">Proxies.json is defined by a proxies object, which is composed of named proxies and their definitions.</span></span> <span data-ttu-id="e4838-188">Vous pouvez éventuellement référencer un [schéma JSON](http://json.schemastore.org/proxies) de complétion de code si votre éditeur est compatible.</span><span class="sxs-lookup"><span data-stu-id="e4838-188">Optionally, if your editor supports it, you can reference a [JSON schema](http://json.schemastore.org/proxies) for code completion.</span></span> <span data-ttu-id="e4838-189">Voici un exemple de fichier :</span><span class="sxs-lookup"><span data-stu-id="e4838-189">An example file might look like the following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>"
        }
    }
}
```

<span data-ttu-id="e4838-190">Chaque proxy a un nom convivial, tel que *proxy1* dans l’exemple ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="e4838-190">Each proxy has a friendly name, such as *proxy1* in the preceding example.</span></span> <span data-ttu-id="e4838-191">L’objet de définition de proxy correspondant est défini par les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="e4838-191">The corresponding proxy definition object is defined by the following properties:</span></span>

* <span data-ttu-id="e4838-192">**matchCondition** : Obligatoire - un objet définissant les demandes qui déclenchent l’exécution de ce proxy.</span><span class="sxs-lookup"><span data-stu-id="e4838-192">**matchCondition**: Required--an object defining the requests that trigger the execution of this proxy.</span></span> <span data-ttu-id="e4838-193">Il contient deux propriétés partagées avec les [déclencheurs HTTP] :</span><span class="sxs-lookup"><span data-stu-id="e4838-193">It contains two properties that are shared with [HTTP triggers]:</span></span>
    * <span data-ttu-id="e4838-194">_méthodes_ : un tableau des méthodes HTTP auxquelles le proxy répond.</span><span class="sxs-lookup"><span data-stu-id="e4838-194">_methods_: An array of the HTTP methods that the proxy responds to.</span></span> <span data-ttu-id="e4838-195">À défaut de spécification, le proxy répond à toutes les méthodes HTTP sur le routage.</span><span class="sxs-lookup"><span data-stu-id="e4838-195">If it is not specified, the proxy responds to all HTTP methods on the route.</span></span>
    * <span data-ttu-id="e4838-196">_route_ : Obligatoire - définit le modèle de routage, en contrôlant les URL de demande auxquelles votre proxy répond.</span><span class="sxs-lookup"><span data-stu-id="e4838-196">_route_: Required--defines the route template, controlling which request URLs your proxy responds to.</span></span> <span data-ttu-id="e4838-197">Contrairement aux déclencheurs HTTP, il n’y a pas de valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="e4838-197">Unlike in HTTP triggers, there is no default value.</span></span>
* <span data-ttu-id="e4838-198">**backendUri** : l’URL de la ressource principale à laquelle la demande doit être transmise par proxy.</span><span class="sxs-lookup"><span data-stu-id="e4838-198">**backendUri**: The URL of the back-end resource to which the request should be proxied.</span></span> <span data-ttu-id="e4838-199">Cette valeur peut faire référence aux paramètres de l’application et à ceux de la demande client d’origine.</span><span class="sxs-lookup"><span data-stu-id="e4838-199">This value can reference application settings and parameters from the original client request.</span></span> <span data-ttu-id="e4838-200">Si cette propriété n’est pas incluse, Azure Functions répond avec un message HTTP 200 OK.</span><span class="sxs-lookup"><span data-stu-id="e4838-200">If this property is not included, Azure Functions responds with an HTTP 200 OK.</span></span>
* <span data-ttu-id="e4838-201">**requestOverrides** : un objet définissant les transformations apportées à la demande du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="e4838-201">**requestOverrides**: An object that defines transformations to the back-end request.</span></span> <span data-ttu-id="e4838-202">Consultez la section [Définition d’un objet requestOverrides].</span><span class="sxs-lookup"><span data-stu-id="e4838-202">See [Define a requestOverrides object].</span></span>
* <span data-ttu-id="e4838-203">**responseOverrides** : un objet définissant les transformations apportées à la réponse client.</span><span class="sxs-lookup"><span data-stu-id="e4838-203">**responseOverrides**: An object that defines transformations to the client response.</span></span> <span data-ttu-id="e4838-204">Consultez la section [Définition d’un objet responseOverrides].</span><span class="sxs-lookup"><span data-stu-id="e4838-204">See [Define a responseOverrides object].</span></span>

> [!NOTE] 
> <span data-ttu-id="e4838-205">La propriété de routage Proxys Azure Functions n’honore pas la propriété routePrefix de la configuration d’hôte de Functions.</span><span class="sxs-lookup"><span data-stu-id="e4838-205">The route property Azure Functions Proxies does not honor the routePrefix property of the Functions host configuration.</span></span> <span data-ttu-id="e4838-206">Si vous souhaitez inclure un préfixe tel que /api, il doit être inclus dans la propriété de routage.</span><span class="sxs-lookup"><span data-stu-id="e4838-206">If you want to include a prefix such as /api, it must be included in the route property.</span></span>

### <span data-ttu-id="e4838-207"><a name="requestOverrides"></a>Définition d’un objet requestOverrides</span><span class="sxs-lookup"><span data-stu-id="e4838-207"><a name="requestOverrides"></a>Define a requestOverrides object</span></span>

<span data-ttu-id="e4838-208">L’objet requestOverrides définit les modifications apportées à la demande lors de l’appel de la ressource du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="e4838-208">The requestOverrides object defines changes made to the request when the back-end resource is called.</span></span> <span data-ttu-id="e4838-209">L’objet est défini par les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="e4838-209">The object is defined by the following properties:</span></span>

* <span data-ttu-id="e4838-210">**backend.request.method** : la méthode HTTP qui est utilisée pour appeler le serveur principal.</span><span class="sxs-lookup"><span data-stu-id="e4838-210">**backend.request.method**: The HTTP method that's used to call the back end.</span></span>
* <span data-ttu-id="e4838-211">**backend.request.querystring.\<ParameterName\>** : un paramètre de chaîne de requête pouvant être défini pour l’appel au serveur principal.</span><span class="sxs-lookup"><span data-stu-id="e4838-211">**backend.request.querystring.\<ParameterName\>**: A query string parameter that can be set for the call to the back end.</span></span> <span data-ttu-id="e4838-212">Remplacez *\<ParameterName\>* par le nom de l’en-tête que vous souhaitez définir.</span><span class="sxs-lookup"><span data-stu-id="e4838-212">Replace *\<ParameterName\>* with the name of the parameter that you want to set.</span></span> <span data-ttu-id="e4838-213">Si une chaîne vide est fournie, le paramètre n’est pas inclus dans la demande du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="e4838-213">If the empty string is provided, the parameter is not included on the back-end request.</span></span>
* <span data-ttu-id="e4838-214">**backend.request.headers.\<HeaderName\>** : un en-tête qui peut être défini pour l’appel au serveur principal.</span><span class="sxs-lookup"><span data-stu-id="e4838-214">**backend.request.headers.\<HeaderName\>**: A header that can be set for the call to the back end.</span></span> <span data-ttu-id="e4838-215">Remplacez *\<HeaderName\>* par le nom de l’en-tête que vous souhaitez définir.</span><span class="sxs-lookup"><span data-stu-id="e4838-215">Replace *\<HeaderName\>* with the name of the header that you want to set.</span></span> <span data-ttu-id="e4838-216">Si vous fournissez une chaîne vide, l’en-tête n’est pas inclus dans la demande du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="e4838-216">If you provide the empty string, the header is not included on the back-end request.</span></span>

<span data-ttu-id="e4838-217">Les valeurs peuvent faire référence aux paramètres de l’application et aux paramètres de la demande client d’origine.</span><span class="sxs-lookup"><span data-stu-id="e4838-217">Values can reference application settings and parameters from the original client request.</span></span>

<span data-ttu-id="e4838-218">Voici un exemple de configuration :</span><span class="sxs-lookup"><span data-stu-id="e4838-218">An example configuration might look like the following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>",
            "requestOverrides": {
                "backend.request.headers.Accept": "application/xml",
                "backend.request.headers.x-functions-key": "%ANOTHERAPP_API_KEY%"
            }
        }
    }
}
```

### <span data-ttu-id="e4838-219"><a name="responseOverrides"></a>Définition d’un objet responseOverrides</span><span class="sxs-lookup"><span data-stu-id="e4838-219"><a name="responseOverrides"></a>Define a responseOverrides object</span></span>

<span data-ttu-id="e4838-220">L’objet requestOverrides définit les modifications apportées à la réponse retransmise au client.</span><span class="sxs-lookup"><span data-stu-id="e4838-220">The requestOverrides object defines changes that are made to the response that's passed back to the client.</span></span> <span data-ttu-id="e4838-221">L’objet est défini par les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="e4838-221">The object is defined by the following properties:</span></span>

* <span data-ttu-id="e4838-222">**response.statusCode** : code d’état HTTP à renvoyer au client.</span><span class="sxs-lookup"><span data-stu-id="e4838-222">**response.statusCode**: The HTTP status code to be returned to the client.</span></span>
* <span data-ttu-id="e4838-223">**response.statusReason** : motif HTTP à renvoyer au client.</span><span class="sxs-lookup"><span data-stu-id="e4838-223">**response.statusReason**: The HTTP reason phrase to be returned to the client.</span></span>
* <span data-ttu-id="e4838-224">**response.body** : la représentation sous forme de chaîne du corps à renvoyer au client.</span><span class="sxs-lookup"><span data-stu-id="e4838-224">**response.body**: The string representation of the body to be returned to the client.</span></span>
* <span data-ttu-id="e4838-225">**response.headers.\<HeaderName\>** : un en-tête pouvant être défini pour la réponse au client.</span><span class="sxs-lookup"><span data-stu-id="e4838-225">**response.headers.\<HeaderName\>**: A header that can be set for the response to the client.</span></span> <span data-ttu-id="e4838-226">Remplacez *\<HeaderName\>* par le nom de l’en-tête que vous souhaitez définir.</span><span class="sxs-lookup"><span data-stu-id="e4838-226">Replace *\<HeaderName\>* with the name of the header that you want to set.</span></span> <span data-ttu-id="e4838-227">Si vous fournissez une chaîne vide, l’en-tête n’est pas inclus dans la réponse.</span><span class="sxs-lookup"><span data-stu-id="e4838-227">If you provide the empty string, the header is not included on the response.</span></span>

<span data-ttu-id="e4838-228">Les valeurs peuvent faire référence aux paramètres de l’application, aux paramètres de la demande client d’origine et aux paramètres de la réponse du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="e4838-228">Values can reference application settings, parameters from the original client request, and parameters from the back-end response.</span></span>

<span data-ttu-id="e4838-229">Voici un exemple de configuration :</span><span class="sxs-lookup"><span data-stu-id="e4838-229">An example configuration might look like the following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "responseOverrides": {
                "response.body": "Hello, {test}",
                "response.headers.Content-Type": "text/plain"
            }
        }
    }
}
```
> [!NOTE] 
> <span data-ttu-id="e4838-230">Dans cet exemple, le corps est défini directement. Aucune propriété `backendUri` n’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e4838-230">In this example, the body is being set directly, so no `backendUri` property is needed.</span></span> <span data-ttu-id="e4838-231">Cet exemple illustre comment utiliser les Proxys Azure Functions pour simuler des API.</span><span class="sxs-lookup"><span data-stu-id="e4838-231">The example shows how you might use Azure Functions Proxies for mocking APIs.</span></span>

<span data-ttu-id="e4838-232">[portail Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="e4838-232">[Azure portal]: https://portal.azure.com</span></span>
<span data-ttu-id="e4838-233">[déclencheurs HTTP]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger</span><span class="sxs-lookup"><span data-stu-id="e4838-233">[HTTP triggers]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger</span></span>
[Modify the back-end request]: #modify-backend-request
[Modify the response]: #modify-response
<span data-ttu-id="e4838-234">[Définition d’un objet requestOverrides]: #requestOverrides</span><span class="sxs-lookup"><span data-stu-id="e4838-234">[Define a requestOverrides object]: #requestOverrides</span></span>
<span data-ttu-id="e4838-235">[Définition d’un objet responseOverrides]: #responseOverrides</span><span class="sxs-lookup"><span data-stu-id="e4838-235">[Define a responseOverrides object]: #responseOverrides</span></span>
<span data-ttu-id="e4838-236">[paramètres de l’application]: #use-appsettings</span><span class="sxs-lookup"><span data-stu-id="e4838-236">[application settings]: #use-appsettings</span></span>
<span data-ttu-id="e4838-237">[Utilisation de variables]: #using-variables</span><span class="sxs-lookup"><span data-stu-id="e4838-237">[Use variables]: #using-variables</span></span>
<span data-ttu-id="e4838-238">[paramètres de la demande client d’origine]: #request-parameters</span><span class="sxs-lookup"><span data-stu-id="e4838-238">[parameters from the original client request]: #request-parameters</span></span>
<span data-ttu-id="e4838-239">[paramètres de la réponse du serveur principal]: #response-parameters</span><span class="sxs-lookup"><span data-stu-id="e4838-239">[parameters from the back-end response]: #response-parameters</span></span>
