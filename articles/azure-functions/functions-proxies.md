---
title: aaaWork avec les serveurs proxy dans les fonctions de Azure | Documents Microsoft
description: "Vue d’ensemble de la procédure toouse Proxies de fonctions Azure"
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
ms.openlocfilehash: 4d94c89e8f8f2d2c771b01bae142bf9a4f3b7f2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-azure-functions-proxies-preview"></a><span data-ttu-id="2ef5d-103">Utilisation de Azure Functions Proxies (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="2ef5d-103">Work with Azure Functions Proxies (preview)</span></span>

> [!NOTE] 
> <span data-ttu-id="2ef5d-104">Azure Functions Proxies est actuellement disponible en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-104">Azure Functions Proxies is currently in preview.</span></span> <span data-ttu-id="2ef5d-105">C’est gratuit tandis que dans l’aperçu, mais les fonctions standard facturation applique tooproxy exécutions.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-105">It is free while in preview, but standard Functions billing applies tooproxy executions.</span></span> <span data-ttu-id="2ef5d-106">Pour plus d’informations, consultez [Tarification d’Azure Functions](https://azure.microsoft.com/pricing/details/functions/).</span><span class="sxs-lookup"><span data-stu-id="2ef5d-106">For more information, see [Azure Functions pricing](https://azure.microsoft.com/pricing/details/functions/).</span></span>

<span data-ttu-id="2ef5d-107">Cet article explique comment tooconfigure et fonctionnent avec les proxys de fonctions Azure.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-107">This article explains how tooconfigure and work with Azure Functions Proxies.</span></span> <span data-ttu-id="2ef5d-108">Cette fonctionnalité vous permet de spécifier des points de terminaison sur votre Function App implémentés par une autre ressource.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-108">With this feature, you can specify endpoints on your function app that are implemented by another resource.</span></span> <span data-ttu-id="2ef5d-109">Vous pouvez utiliser ces toobreak proxys une API volumineuse dans plusieurs applications de fonction (par exemple, une architecture de microservice), tout en présentant une surface API unique pour les clients.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-109">You can use these proxies toobreak a large API into multiple function apps (as in a microservice architecture), while still presenting a single API surface for clients.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]


## <span data-ttu-id="2ef5d-110"><a name="enable"></a>Activation d’Azure Functions Proxies</span><span class="sxs-lookup"><span data-stu-id="2ef5d-110"><a name="enable"></a>Enable Azure Functions Proxies</span></span>

<span data-ttu-id="2ef5d-111">Les proxies ne sont pas activés par défaut.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-111">Proxies are not enabled by default.</span></span> <span data-ttu-id="2ef5d-112">Vous pouvez créer des proxys lors de la fonctionnalité de hello est désactivée, mais ils ne seront exécute pas.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-112">You can create proxies while hello feature is disabled, but they will not execute.</span></span> <span data-ttu-id="2ef5d-113">les proxys tooenable, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="2ef5d-113">tooenable proxies, do hello following:</span></span>

1. <span data-ttu-id="2ef5d-114">Ouvrez hello [portail Azure], puis passez tooyour fonction app.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-114">Open hello [Azure portal], and then go tooyour function app.</span></span>
2. <span data-ttu-id="2ef5d-115">Sélectionnez **Paramètres Function App**.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-115">Select **Function app settings**.</span></span>
3. <span data-ttu-id="2ef5d-116">Commutateur **activer des proxys de fonctions Azure (aperçu)** trop**sur**.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-116">Switch **Enable Azure Functions Proxies (preview)** too**On**.</span></span>

<span data-ttu-id="2ef5d-117">Vous pouvez également revenir ici tooupdate hello proxy runtime que de nouvelles fonctionnalités sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-117">You can also return here tooupdate hello proxy runtime as new features become available.</span></span>


## <span data-ttu-id="2ef5d-118"><a name="create"></a>Création d’un proxy</span><span class="sxs-lookup"><span data-stu-id="2ef5d-118"><a name="create"></a>Create a proxy</span></span>

<span data-ttu-id="2ef5d-119">Cette section vous montre comment toocreate un proxy dans hello portal de fonctions.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-119">This section shows you how toocreate a proxy in hello Functions portal.</span></span>

1. <span data-ttu-id="2ef5d-120">Ouvrez hello [portail Azure], puis passez tooyour fonction app.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-120">Open hello [Azure portal], and then go tooyour function app.</span></span>
2. <span data-ttu-id="2ef5d-121">Dans le volet gauche de hello, sélectionnez **nouveau proxy**.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-121">In hello left pane, select **New proxy**.</span></span>
3. <span data-ttu-id="2ef5d-122">Entrez un nom pour votre proxy.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-122">Provide a name for your proxy.</span></span>
4. <span data-ttu-id="2ef5d-123">Configurer des hello de point de terminaison qui est exposé sur cette application de la fonction en spécifiant hello **modèle d’itinéraire** et **méthodes HTTP**.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-123">Configure hello endpoint that's exposed on this function app by specifying hello **route template** and **HTTP methods**.</span></span> <span data-ttu-id="2ef5d-124">Ces paramètres comportent en fonction des règles de toohello pour [HTTP déclencheurs].</span><span class="sxs-lookup"><span data-stu-id="2ef5d-124">These parameters behave according toohello rules for [HTTP triggers].</span></span>
5. <span data-ttu-id="2ef5d-125">Ensemble hello **URL principal** tooanother le point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-125">Set hello **backend URL** tooanother endpoint.</span></span> <span data-ttu-id="2ef5d-126">Il peut s’agir d’une fonction dans une autre Function App ou bien de n’importe quelle autre API.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-126">This endpoint could be a function in another function app, or it could be any other API.</span></span> <span data-ttu-id="2ef5d-127">Hello valeur ne doit pas toobe statique, et il peut référencer [paramètres de l’application] et [paramètres à partir de la demande du client d’origine hello].</span><span class="sxs-lookup"><span data-stu-id="2ef5d-127">hello value does not need toobe static, and it can reference [application settings] and [parameters from hello original client request].</span></span>
6. <span data-ttu-id="2ef5d-128">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-128">Click **Create**.</span></span>

<span data-ttu-id="2ef5d-129">Votre proxy existe désormais sous la forme d’un nouveau point de terminaison de votre application de fonction.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-129">Your proxy now exists as a new endpoint on your function app.</span></span> <span data-ttu-id="2ef5d-130">À partir d’un point de vue du client, il est équivalent tooan HttpTrigger dans les fonctions d’Azure.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-130">From a client perspective, it is equivalent tooan HttpTrigger in Azure Functions.</span></span> <span data-ttu-id="2ef5d-131">Vous pouvez essayer votre nouveau proxy en copiant hello URL de Proxy et de test avec votre client HTTP favori.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-131">You can try out your new proxy by copying hello Proxy URL and testing it with your favorite HTTP client.</span></span>

## <span data-ttu-id="2ef5d-132"><a name="modify-requests-responses"></a>Modification de demandes et de réponses</span><span class="sxs-lookup"><span data-stu-id="2ef5d-132"><a name="modify-requests-responses"></a>Modify requests and responses</span></span>

<span data-ttu-id="2ef5d-133">Avec les serveurs proxy de fonctions Azure, vous pouvez modifier les requêtes tooand réponses de back-end hello.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-133">With Azure Functions Proxies, you can modify requests tooand responses from hello back end.</span></span> <span data-ttu-id="2ef5d-134">Ces transformations peuvent impliquer l’utilisation de variables, comme décrit dans la section [Utilisation de variables].</span><span class="sxs-lookup"><span data-stu-id="2ef5d-134">These transformations can use variables as defined in [Use variables].</span></span>

### <span data-ttu-id="2ef5d-135"><a name="modify-backend-request"></a>Modifier hello principal demande</span><span class="sxs-lookup"><span data-stu-id="2ef5d-135"><a name="modify-backend-request"></a>Modify hello back-end request</span></span>

<span data-ttu-id="2ef5d-136">Par défaut, demande de back-end hello est initialisée comme une copie de la demande d’origine de hello.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-136">By default, hello back-end request is initialized as a copy of hello original request.</span></span> <span data-ttu-id="2ef5d-137">En outre vous toosetting hello principal URL, vous pouvez apporter modifications toohello HTTP méthode, les en-têtes et les paramètres de chaîne de requête.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-137">In addition toosetting hello back-end URL, you can make changes toohello HTTP method, headers, and query string parameters.</span></span> <span data-ttu-id="2ef5d-138">Hello valeurs modifiées peuvent référencer [paramètres de l’application] et [paramètres à partir de la demande du client d’origine hello].</span><span class="sxs-lookup"><span data-stu-id="2ef5d-138">hello modified values can reference [application settings] and [parameters from hello original client request].</span></span>

<span data-ttu-id="2ef5d-139">Il n’est actuellement pas possible de modifier les demandes du serveur principal via un portail.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-139">Currently, there is no portal experience for modifying back-end requests.</span></span> <span data-ttu-id="2ef5d-140">toolearn tooapply cette fonctionnalité à partir de proxies.json, voir [définir un objet requestOverrides].</span><span class="sxs-lookup"><span data-stu-id="2ef5d-140">toolearn how tooapply this capability from proxies.json, see [Define a requestOverrides object].</span></span>

### <span data-ttu-id="2ef5d-141"><a name="modify-response"></a>Modifier la réponse de hello</span><span class="sxs-lookup"><span data-stu-id="2ef5d-141"><a name="modify-response"></a>Modify hello response</span></span>

<span data-ttu-id="2ef5d-142">Par défaut, la réponse hello du client est initialisé comme une copie de la réponse du serveur principal hello.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-142">By default, hello client response is initialized as a copy of hello back-end response.</span></span> <span data-ttu-id="2ef5d-143">Vous pouvez apporter de code d’état de la réponse de modifications toohello, phrase de motif, en-têtes et corps.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-143">You can make changes toohello response's status code, reason phrase, headers, and body.</span></span> <span data-ttu-id="2ef5d-144">Hello valeurs modifiées peuvent référencer [paramètres de l’application], [paramètres à partir de la demande du client d’origine hello], et [paramètres de réponse du serveur principal hello].</span><span class="sxs-lookup"><span data-stu-id="2ef5d-144">hello modified values can reference [application settings], [parameters from hello original client request], and [parameters from hello back-end response].</span></span>

<span data-ttu-id="2ef5d-145">Il n’est actuellement pas possible de modifier les réponses.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-145">Currently, there is no portal experience for modifying responses.</span></span> <span data-ttu-id="2ef5d-146">toolearn tooapply cette fonctionnalité à partir de proxies.json, voir [définir un objet responseOverrides].</span><span class="sxs-lookup"><span data-stu-id="2ef5d-146">toolearn how tooapply this capability from proxies.json, see [Define a responseOverrides object].</span></span>

## <span data-ttu-id="2ef5d-147"><a name="using-variables"></a>Utilisation de variables</span><span class="sxs-lookup"><span data-stu-id="2ef5d-147"><a name="using-variables"></a>Use variables</span></span>

<span data-ttu-id="2ef5d-148">configuration Hello pour un serveur proxy n’a pas besoin toobe statique.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-148">hello configuration for a proxy does not need toobe static.</span></span> <span data-ttu-id="2ef5d-149">Vous pouvez que celle-ci variables toouse à partir de la demande d’origine de hello, réponse de back-end hello ou paramètres de l’application.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-149">You can condition it toouse variables from hello original request, hello back-end response, or application settings.</span></span>

### <span data-ttu-id="2ef5d-150"><a name="request-parameters"></a>Référencement des paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="2ef5d-150"><a name="request-parameters"></a>Reference request parameters</span></span>

<span data-ttu-id="2ef5d-151">Vous pouvez utiliser les paramètres de la demande comme entrées de propriété de l’URL principale toohello ou dans le cadre de la modification des demandes et réponses.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-151">You can use request parameters as inputs toohello back-end URL property or as part of modifying requests and responses.</span></span> <span data-ttu-id="2ef5d-152">Certains paramètres peuvent être liés à partir du modèle d’itinéraire hello qui est spécifié dans la configuration du proxy base hello et d’autres peuvent provenir de propriétés de la demande entrante de hello.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-152">Some parameters can be bound from hello route template that's specified in hello base proxy configuration, and others can come from properties of hello incoming request.</span></span>

#### <a name="route-template-parameters"></a><span data-ttu-id="2ef5d-153">Paramètres de modèle de routage</span><span class="sxs-lookup"><span data-stu-id="2ef5d-153">Route template parameters</span></span>
<span data-ttu-id="2ef5d-154">Paramètres qui sont utilisés dans le modèle d’itinéraire hello sont disponible toobe référencée par son nom.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-154">Parameters that are used in hello route template are available toobe referenced by name.</span></span> <span data-ttu-id="2ef5d-155">les noms de paramètre Hello sont placés entre accolades ({}).</span><span class="sxs-lookup"><span data-stu-id="2ef5d-155">hello parameter names are enclosed in braces ({}).</span></span>

<span data-ttu-id="2ef5d-156">Par exemple, si un proxy dispose d’un modèle d’itinéraire, tel que `/pets/{petId}`, hello principal URL peut inclure la valeur hello `{petId}`, comme dans `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-156">For example, if a proxy has a route template, such as `/pets/{petId}`, hello back-end URL can include hello value of `{petId}`, as in `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`.</span></span> <span data-ttu-id="2ef5d-157">Si modèle d’itinéraire hello se termine dans un caractère générique, tel que `/api/{*restOfPath}`, hello valeur `{restOfPath}` est une représentation de chaîne de hello restant de segments de chemin d’accès à partir de la demande entrante de hello.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-157">If hello route template terminates in a wildcard, such as `/api/{*restOfPath}`, hello value `{restOfPath}` is a string representation of hello remaining path segments from hello incoming request.</span></span>

#### <a name="additional-request-parameters"></a><span data-ttu-id="2ef5d-158">Paramètres de demande supplémentaires</span><span class="sxs-lookup"><span data-stu-id="2ef5d-158">Additional request parameters</span></span>
<span data-ttu-id="2ef5d-159">En outre toohello les paramètres de modèle d’itinéraire, hello valeurs suivantes peut être utilisée dans les valeurs de configuration :</span><span class="sxs-lookup"><span data-stu-id="2ef5d-159">In addition toohello route template parameters, hello following values can be used in config values:</span></span>

* <span data-ttu-id="2ef5d-160">**{request.method}** : hello méthode HTTP qui est utilisé à la demande d’origine de hello.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-160">**{request.method}**: hello HTTP method that's used on hello original request.</span></span>
* <span data-ttu-id="2ef5d-161">**{request.headers. \<HeaderName\>}**: un en-tête qui peut être lu à partir de la demande d’origine de hello.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-161">**{request.headers.\<HeaderName\>}**: A header that can be read from hello original request.</span></span> <span data-ttu-id="2ef5d-162">Remplacez  *\<HeaderName\>*  avec nom hello d’en-tête hello que vous souhaitez tooread.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-162">Replace *\<HeaderName\>* with hello name of hello header that you want tooread.</span></span> <span data-ttu-id="2ef5d-163">Si l’en-tête de hello n’est pas inclus dans la demande de hello, valeur de hello sera une chaîne vide hello.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-163">If hello header is not included on hello request, hello value will be hello empty string.</span></span>
* <span data-ttu-id="2ef5d-164">**{request.querystring. \<Nom_paramètre\>}**: un paramètre de chaîne de requête permettre être lus à partir de la demande d’origine de hello.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-164">**{request.querystring.\<ParameterName\>}**: A query string parameter that can be read from hello original request.</span></span> <span data-ttu-id="2ef5d-165">Remplacez  *\<nom_paramètre\>*  avec nom hello du paramètre hello que vous souhaitez tooread.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-165">Replace *\<ParameterName\>* with hello name of hello parameter that you want tooread.</span></span> <span data-ttu-id="2ef5d-166">Si le paramètre hello n’est pas inclus dans la demande de hello, valeur de hello sera une chaîne vide hello.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-166">If hello parameter is not included on hello request, hello value will be hello empty string.</span></span>

### <span data-ttu-id="2ef5d-167"><a name="response-parameters"></a>Référencement des paramètres de réponse du serveur principal</span><span class="sxs-lookup"><span data-stu-id="2ef5d-167"><a name="response-parameters"></a>Reference back-end response parameters</span></span>

<span data-ttu-id="2ef5d-168">Paramètres de réponse peuvent être utilisés dans le cadre de la modification de client de toohello réponse hello.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-168">Response parameters can be used as part of modifying hello response toohello client.</span></span> <span data-ttu-id="2ef5d-169">Hello valeurs suivantes sont utilisables dans les valeurs de configuration :</span><span class="sxs-lookup"><span data-stu-id="2ef5d-169">hello following values can be used in config values:</span></span>

* <span data-ttu-id="2ef5d-170">**{backend.response.statusCode}** : hello le code d’état HTTP retourné de réponse du serveur principal hello.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-170">**{backend.response.statusCode}**: hello HTTP status code that's returned on hello back-end response.</span></span>
* <span data-ttu-id="2ef5d-171">**{backend.response.statusReason}** : phrase de motif hello HTTP qui est renvoyée en cas de réponse du serveur principal hello.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-171">**{backend.response.statusReason}**: hello HTTP reason phrase that's returned on hello back-end response.</span></span>
* <span data-ttu-id="2ef5d-172">**{backend.response.headers. \<HeaderName\>}**: un en-tête qui peut être lu à partir de la réponse du serveur principal hello.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-172">**{backend.response.headers.\<HeaderName\>}**: A header that can be read from hello back-end response.</span></span> <span data-ttu-id="2ef5d-173">Remplacez  *\<HeaderName\>*  avec nom hello d’en-tête de hello souhaité tooread.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-173">Replace *\<HeaderName\>* with hello name of hello header you want tooread.</span></span> <span data-ttu-id="2ef5d-174">Si l’en-tête de hello n’est pas inclus dans la demande de hello, valeur de hello sera une chaîne vide hello.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-174">If hello header is not included on hello request, hello value will be hello empty string.</span></span>

### <span data-ttu-id="2ef5d-175"><a name="use-appsettings"></a>Référencement des paramètres de l’application</span><span class="sxs-lookup"><span data-stu-id="2ef5d-175"><a name="use-appsettings"></a>Reference application settings</span></span>

<span data-ttu-id="2ef5d-176">Vous pouvez également référencer [paramètres d’application définis pour l’application de fonction hello](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) en entourant le nom du paramètre hello avec des signes de pourcentage (%).</span><span class="sxs-lookup"><span data-stu-id="2ef5d-176">You can also reference [application settings defined for hello function app](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) by surrounding hello setting name with percent signs (%).</span></span>

<span data-ttu-id="2ef5d-177">Par exemple, une URL principale *https://%ORDER_PROCESSING_HOST%/api/orders* aurait « ORDER_PROCESSING_HOST % » remplacé par la valeur hello du paramètre de ORDER_PROCESSING_HOST hello.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-177">For example, a back-end URL of *https://%ORDER_PROCESSING_HOST%/api/orders* would have "%ORDER_PROCESSING_HOST%" replaced with hello value of hello ORDER_PROCESSING_HOST setting.</span></span>

> [!TIP] 
> <span data-ttu-id="2ef5d-178">Utilisez des paramètres d’application pour les hôtes de serveur principal lorsque vous avez plusieurs déploiements ou environnements de test.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-178">Use application settings for back-end hosts when you have multiple deployments or test environments.</span></span> <span data-ttu-id="2ef5d-179">De cette façon, vous pouvez vous assurer que vous vous entretenez toujours toohello immédiatement fin pour cet environnement.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-179">That way, you can make sure that you are always talking toohello right back end for that environment.</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="2ef5d-180">Configuration avancée</span><span class="sxs-lookup"><span data-stu-id="2ef5d-180">Advanced configuration</span></span>

<span data-ttu-id="2ef5d-181">les proxys Hello que vous configurez sont stockés dans un fichier proxies.json, qui se trouve dans un répertoire d’application de fonction racine hello.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-181">hello proxies that you configure are stored in a proxies.json file, which is located in hello root of a function app directory.</span></span> <span data-ttu-id="2ef5d-182">Vous pouvez manuellement modifier ce fichier et le déployer dans le cadre de votre application quand vous utilisez une des hello [méthodes de déploiement](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) qui prend en charge des fonctions.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-182">You can manually edit this file and deploy it as part of your app when you use any of hello [deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) that Functions supports.</span></span> <span data-ttu-id="2ef5d-183">fonctionnalité de Hello doit être [activé](#enable) pour toobe de fichier hello traité.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-183">hello feature must be [enabled](#enable) for hello file toobe processed.</span></span> 

> [!TIP] 
> <span data-ttu-id="2ef5d-184">Si vous n’avez pas défini un hello des méthodes de déploiement, vous pouvez également travailler avec fichier de proxies.json hello dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-184">If you have not set up one of hello deployment methods, you can also work with hello proxies.json file in hello portal.</span></span> <span data-ttu-id="2ef5d-185">Application de fonction tooyour accédez, sélectionnez **fonctionnalités de plateforme**, puis sélectionnez **éditeur de Service d’applications**.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-185">Go tooyour function app, select **Platform features**, and then select **App Service Editor**.</span></span> <span data-ttu-id="2ef5d-186">En procédant ainsi, vous pouvez afficher la structure de fichiers complète hello de votre application de la fonction et apporter des modifications.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-186">By doing so, you can view hello entire file structure of your function app and then make changes.</span></span>

<span data-ttu-id="2ef5d-187">Proxies.json est défini par un objet proxy, composé de proxys nommés et de leurs définitions.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-187">Proxies.json is defined by a proxies object, which is composed of named proxies and their definitions.</span></span> <span data-ttu-id="2ef5d-188">Vous pouvez éventuellement référencer un [schéma JSON](http://json.schemastore.org/proxies) de complétion de code si votre éditeur est compatible.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-188">Optionally, if your editor supports it, you can reference a [JSON schema](http://json.schemastore.org/proxies) for code completion.</span></span> <span data-ttu-id="2ef5d-189">Un exemple de fichier peut se présenter comme hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="2ef5d-189">An example file might look like hello following:</span></span>

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

<span data-ttu-id="2ef5d-190">Chaque proxy a un nom convivial, tel que *proxy1* Bonjour précédent exemple.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-190">Each proxy has a friendly name, such as *proxy1* in hello preceding example.</span></span> <span data-ttu-id="2ef5d-191">objet de définition de proxy Hello correspondant est défini par hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="2ef5d-191">hello corresponding proxy definition object is defined by hello following properties:</span></span>

* <span data-ttu-id="2ef5d-192">**matchCondition**: obligatoire : un objet définissant les demandes hello qui déclenchent l’exécution de hello du proxy.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-192">**matchCondition**: Required--an object defining hello requests that trigger hello execution of this proxy.</span></span> <span data-ttu-id="2ef5d-193">Il contient deux propriétés partagées avec les [HTTP déclencheurs] :</span><span class="sxs-lookup"><span data-stu-id="2ef5d-193">It contains two properties that are shared with [HTTP triggers]:</span></span>
    * <span data-ttu-id="2ef5d-194">_méthodes_: un tableau de méthodes hello HTTP qui hello proxy répond à.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-194">_methods_: An array of hello HTTP methods that hello proxy responds to.</span></span> <span data-ttu-id="2ef5d-195">S’il n’est pas spécifié, le proxy de hello répond tooall les méthodes HTTP sur l’itinéraire de hello.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-195">If it is not specified, hello proxy responds tooall HTTP methods on hello route.</span></span>
    * <span data-ttu-id="2ef5d-196">_itinéraire_: obligatoire : définit le modèle d’itinéraire hello, contrôle qui demande les URL de votre proxy répond à.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-196">_route_: Required--defines hello route template, controlling which request URLs your proxy responds to.</span></span> <span data-ttu-id="2ef5d-197">Contrairement aux déclencheurs HTTP, il n’y a pas de valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-197">Unlike in HTTP triggers, there is no default value.</span></span>
* <span data-ttu-id="2ef5d-198">**backendUri**: URL hello hello principal toowhich hello de demande de ressource doit être traitée.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-198">**backendUri**: hello URL of hello back-end resource toowhich hello request should be proxied.</span></span> <span data-ttu-id="2ef5d-199">Cette valeur peut référencer des paramètres d’application et les paramètres à partir de la demande du client d’origine hello.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-199">This value can reference application settings and parameters from hello original client request.</span></span> <span data-ttu-id="2ef5d-200">Si cette propriété n’est pas incluse, Azure Functions répond avec un message HTTP 200 OK.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-200">If this property is not included, Azure Functions responds with an HTTP 200 OK.</span></span>
* <span data-ttu-id="2ef5d-201">**requestOverrides**: un objet qui définit la demande de transformations toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-201">**requestOverrides**: An object that defines transformations toohello back-end request.</span></span> <span data-ttu-id="2ef5d-202">Consultez la section [définir un objet requestOverrides].</span><span class="sxs-lookup"><span data-stu-id="2ef5d-202">See [Define a requestOverrides object].</span></span>
* <span data-ttu-id="2ef5d-203">**responseOverrides**: un objet qui définit la réponse de transformations toohello client.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-203">**responseOverrides**: An object that defines transformations toohello client response.</span></span> <span data-ttu-id="2ef5d-204">Consultez la section [définir un objet responseOverrides].</span><span class="sxs-lookup"><span data-stu-id="2ef5d-204">See [Define a responseOverrides object].</span></span>

> [!NOTE] 
> <span data-ttu-id="2ef5d-205">propriété d’itinéraire Hello Proxies de fonctions Azure ne respecte pas la propriété de préfixe d’itinéraire hello de configuration de l’hôte fonctions hello.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-205">hello route property Azure Functions Proxies does not honor hello routePrefix property of hello Functions host configuration.</span></span> <span data-ttu-id="2ef5d-206">Si vous voulez tooinclude un préfixe tel que/API, il doit être inclus dans la propriété d’itinéraire hello.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-206">If you want tooinclude a prefix such as /api, it must be included in hello route property.</span></span>

### <span data-ttu-id="2ef5d-207"><a name="requestOverrides"></a>Définition d’un objet requestOverrides</span><span class="sxs-lookup"><span data-stu-id="2ef5d-207"><a name="requestOverrides"></a>Define a requestOverrides object</span></span>

<span data-ttu-id="2ef5d-208">objet de requestOverrides Hello définit les modifications apportées toohello demande lors de la ressource principale de hello est appelée.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-208">hello requestOverrides object defines changes made toohello request when hello back-end resource is called.</span></span> <span data-ttu-id="2ef5d-209">objet de Hello est défini par hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="2ef5d-209">hello object is defined by hello following properties:</span></span>

* <span data-ttu-id="2ef5d-210">**backend.Request.Method**: hello méthode HTTP qui a utilisé le principal hello toocall.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-210">**backend.request.method**: hello HTTP method that's used toocall hello back end.</span></span>
* <span data-ttu-id="2ef5d-211">**backend.Request.QueryString. \<Nom_paramètre\>**: un paramètre de chaîne de requête qui peut être défini pour hello appel toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-211">**backend.request.querystring.\<ParameterName\>**: A query string parameter that can be set for hello call toohello back end.</span></span> <span data-ttu-id="2ef5d-212">Remplacez  *\<nom_paramètre\>*  avec nom hello du paramètre hello que vous souhaitez tooset.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-212">Replace *\<ParameterName\>* with hello name of hello parameter that you want tooset.</span></span> <span data-ttu-id="2ef5d-213">Si une chaîne vide hello est fournie, le paramètre hello n’est pas inclus à la demande de back-end hello.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-213">If hello empty string is provided, hello parameter is not included on hello back-end request.</span></span>
* <span data-ttu-id="2ef5d-214">**backend.Request.Headers. \<HeaderName\>**: un en-tête qui peut être défini pour hello appel toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-214">**backend.request.headers.\<HeaderName\>**: A header that can be set for hello call toohello back end.</span></span> <span data-ttu-id="2ef5d-215">Remplacez  *\<HeaderName\>*  avec nom hello d’en-tête hello que vous souhaitez tooset.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-215">Replace *\<HeaderName\>* with hello name of hello header that you want tooset.</span></span> <span data-ttu-id="2ef5d-216">Si vous fournissez une chaîne vide hello, en-tête de hello n’est pas inclus à la demande de back-end hello.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-216">If you provide hello empty string, hello header is not included on hello back-end request.</span></span>

<span data-ttu-id="2ef5d-217">Valeurs peuvent référencer des paramètres d’application et de paramètres à partir de la demande du client d’origine hello.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-217">Values can reference application settings and parameters from hello original client request.</span></span>

<span data-ttu-id="2ef5d-218">Un exemple de configuration peut se présenter comme hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="2ef5d-218">An example configuration might look like hello following:</span></span>

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

### <span data-ttu-id="2ef5d-219"><a name="responseOverrides"></a>Définition d’un objet responseOverrides</span><span class="sxs-lookup"><span data-stu-id="2ef5d-219"><a name="responseOverrides"></a>Define a responseOverrides object</span></span>

<span data-ttu-id="2ef5d-220">objet de requestOverrides Hello définit les modifications apportées à réponse toohello qui a passé arrière toohello client.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-220">hello requestOverrides object defines changes that are made toohello response that's passed back toohello client.</span></span> <span data-ttu-id="2ef5d-221">objet de Hello est défini par hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="2ef5d-221">hello object is defined by hello following properties:</span></span>

* <span data-ttu-id="2ef5d-222">**response.statusCode**: toobe de code d’état HTTP de hello retourné toohello client.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-222">**response.statusCode**: hello HTTP status code toobe returned toohello client.</span></span>
* <span data-ttu-id="2ef5d-223">**response.statusReason**: toobe de phrase de motif hello HTTP retourné toohello client.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-223">**response.statusReason**: hello HTTP reason phrase toobe returned toohello client.</span></span>
* <span data-ttu-id="2ef5d-224">**Response.Body**: représentation sous forme de chaîne hello de hello corps toobe retourné toohello client.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-224">**response.body**: hello string representation of hello body toobe returned toohello client.</span></span>
* <span data-ttu-id="2ef5d-225">**Response.Headers. \<HeaderName\>**: un en-tête qui peut être défini pour le client de toohello réponse hello.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-225">**response.headers.\<HeaderName\>**: A header that can be set for hello response toohello client.</span></span> <span data-ttu-id="2ef5d-226">Remplacez  *\<HeaderName\>*  avec nom hello d’en-tête hello que vous souhaitez tooset.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-226">Replace *\<HeaderName\>* with hello name of hello header that you want tooset.</span></span> <span data-ttu-id="2ef5d-227">Si vous fournissez une chaîne vide hello, en-tête de hello n’est pas inclus dans la réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-227">If you provide hello empty string, hello header is not included on hello response.</span></span>

<span data-ttu-id="2ef5d-228">Valeurs peuvent référencer des paramètres d’application, les paramètres de demande du client d’origine hello et les paramètres de réponse du serveur principal hello.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-228">Values can reference application settings, parameters from hello original client request, and parameters from hello back-end response.</span></span>

<span data-ttu-id="2ef5d-229">Un exemple de configuration peut se présenter comme hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="2ef5d-229">An example configuration might look like hello following:</span></span>

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
> <span data-ttu-id="2ef5d-230">Dans cet exemple, corps de hello est définie directement, etc. `backendUri` propriété est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-230">In this example, hello body is being set directly, so no `backendUri` property is needed.</span></span> <span data-ttu-id="2ef5d-231">Hello montre comment vous pouvez utiliser des proxys de fonctions Azure pour la simulation d’API.</span><span class="sxs-lookup"><span data-stu-id="2ef5d-231">hello example shows how you might use Azure Functions Proxies for mocking APIs.</span></span>

[portail Azure]: https://portal.azure.com
[HTTP déclencheurs]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger
[Modify hello back-end request]: #modify-backend-request
[Modify hello response]: #modify-response
[définir un objet requestOverrides]: #requestOverrides
[définir un objet responseOverrides]: #responseOverrides
[paramètres de l’application]: #use-appsettings
[Utilisation de variables]: #using-variables
[paramètres à partir de la demande du client d’origine hello]: #request-parameters
[paramètres de réponse du serveur principal hello]: #response-parameters
