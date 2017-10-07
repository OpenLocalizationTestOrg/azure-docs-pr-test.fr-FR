---
title: "aaaAzure modèle de données d’Application Insights télémétrie - contexte de données de télémétrie | Documents Microsoft"
description: "Modèle de données du contexte de télémétrie d’Application Insights"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/15/2017
ms.author: sergkanz
ms.openlocfilehash: 6cdd6240d1c448f883d104a871ee9d5f6b5af2ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="telemetry-context-application-insights-data-model"></a><span data-ttu-id="3776e-103">Contexte de télémétrie : modèle de données d’Application Insights</span><span class="sxs-lookup"><span data-stu-id="3776e-103">Telemetry context: Application Insights data model</span></span>

<span data-ttu-id="3776e-104">Chaque élément de télémétrie peut avoir des champs de contexte fortement typés.</span><span class="sxs-lookup"><span data-stu-id="3776e-104">Every telemetry item may have a strongly typed context fields.</span></span> <span data-ttu-id="3776e-105">Chaque champ permet un scénario de surveillance spécifique.</span><span class="sxs-lookup"><span data-stu-id="3776e-105">Every field enables a specific monitoring scenario.</span></span> <span data-ttu-id="3776e-106">Utilisez hello propriétés personnalisées collection toostore personnalisées ou spécifiques à l’application des informations contextuelles.</span><span class="sxs-lookup"><span data-stu-id="3776e-106">Use hello custom properties collection toostore custom or application-specific contextual information.</span></span>


##<a name="application-version"></a><span data-ttu-id="3776e-107">Version de l’application</span><span class="sxs-lookup"><span data-stu-id="3776e-107">Application version</span></span>

<span data-ttu-id="3776e-108">Les informations dans les champs de contexte d’application hello sont toujours sur l’application hello qui envoie les données de télémétrie hello.</span><span class="sxs-lookup"><span data-stu-id="3776e-108">Information in hello application context fields is always about hello application that is sending hello telemetry.</span></span> <span data-ttu-id="3776e-109">Version de l’application est utilisée tooanalyze des modifications de tendance dans le comportement de l’application hello et ses déploiements toohello de corrélation.</span><span class="sxs-lookup"><span data-stu-id="3776e-109">Application version is used tooanalyze trend changes in hello application behavior and its correlation toohello deployments.</span></span>

<span data-ttu-id="3776e-110">Longueur maximale : 1024</span><span class="sxs-lookup"><span data-stu-id="3776e-110">Max length: 1024</span></span>


##<a name="client-ip-address"></a><span data-ttu-id="3776e-111">Adresse IP du client</span><span class="sxs-lookup"><span data-stu-id="3776e-111">Client IP address</span></span>

<span data-ttu-id="3776e-112">adresse IP de Hello de périphérique de client hello.</span><span class="sxs-lookup"><span data-stu-id="3776e-112">hello IP address of hello client device.</span></span> <span data-ttu-id="3776e-113">IPv4 et IPv6 sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="3776e-113">IPv4 and IPv6 are supported.</span></span> <span data-ttu-id="3776e-114">Lors de la télémétrie est envoyée à partir d’un service, contexte d’emplacement hello est sur l’utilisateur hello qui a lancé une opération de service de hello hello.</span><span class="sxs-lookup"><span data-stu-id="3776e-114">When telemetry is sent from a service, hello location context is about hello user that initiated hello operation in hello service.</span></span> <span data-ttu-id="3776e-115">Application Insights extraire des informations de géolocalisation hello à partir de l’adresse IP du client hello et puis de le tronquer.</span><span class="sxs-lookup"><span data-stu-id="3776e-115">Application Insights extract hello geo-location information from hello client IP and then truncate it.</span></span> <span data-ttu-id="3776e-116">Ainsi, l’adresse IP du client en elle-même ne peut pas être utilisée comme information identifiable de l’utilisateur final.</span><span class="sxs-lookup"><span data-stu-id="3776e-116">So client IP by itself cannot be used as end-user identifiable information.</span></span> 

<span data-ttu-id="3776e-117">Longueur maximale : 46</span><span class="sxs-lookup"><span data-stu-id="3776e-117">Max length: 46</span></span>


##<a name="device-type"></a><span data-ttu-id="3776e-118">Type d’appareil</span><span class="sxs-lookup"><span data-stu-id="3776e-118">Device type</span></span>

<span data-ttu-id="3776e-119">À l’origine de ce champ a été utilisé à l’aide de type hello de tooindicate de hello hello fin utilisateur de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="3776e-119">Originally this field was used tooindicate hello type of hello device hello end user of hello application is using.</span></span> <span data-ttu-id="3776e-120">Nous sommes utilisé principalement les données de télémétrie de JavaScript toodistinguish hello type d’appareil « Browser » à partir des données de télémétrie côté serveur avec le type d’appareil hello « PC ».</span><span class="sxs-lookup"><span data-stu-id="3776e-120">Today used primarily toodistinguish JavaScript telemetry with hello device type 'Browser' from server-side telemetry with hello device type 'PC'.</span></span>

<span data-ttu-id="3776e-121">Longueur maximale : 64</span><span class="sxs-lookup"><span data-stu-id="3776e-121">Max length: 64</span></span>


##<a name="operation-id"></a><span data-ttu-id="3776e-122">ID d’opération</span><span class="sxs-lookup"><span data-stu-id="3776e-122">Operation id</span></span>

<span data-ttu-id="3776e-123">Identificateur unique de l’opération de racine hello.</span><span class="sxs-lookup"><span data-stu-id="3776e-123">A unique identifier of hello root operation.</span></span> <span data-ttu-id="3776e-124">Cet identificateur permet de télémétrie de toogroup sur plusieurs composants.</span><span class="sxs-lookup"><span data-stu-id="3776e-124">This identifier allows toogroup telemetry across multiple components.</span></span> <span data-ttu-id="3776e-125">Pour plus d’informations, consultez [Corrélation de la télémétrie](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="3776e-125">See [telemetry correlation](application-insights-correlation.md) for details.</span></span> <span data-ttu-id="3776e-126">id d’opération Hello est créé par une demande ou un affichage de page.</span><span class="sxs-lookup"><span data-stu-id="3776e-126">hello operation id is created by either a request or a page view.</span></span> <span data-ttu-id="3776e-127">Toutes les autres données de télémétrie définit cette valeur du champ toohello pour hello contenant la demande ou la page de vue.</span><span class="sxs-lookup"><span data-stu-id="3776e-127">All other telemetry sets this field toohello value for hello containing request or page view.</span></span> 

<span data-ttu-id="3776e-128">Longueur maximale : 128</span><span class="sxs-lookup"><span data-stu-id="3776e-128">Max length: 128</span></span>


##<a name="parent-operation-id"></a><span data-ttu-id="3776e-129">ID d’opération parent</span><span class="sxs-lookup"><span data-stu-id="3776e-129">Parent operation ID</span></span>

<span data-ttu-id="3776e-130">Bonjour identificateur unique du parent immédiat de l’élément de données de télémétrie hello.</span><span class="sxs-lookup"><span data-stu-id="3776e-130">hello unique identifier of hello telemetry item's immediate parent.</span></span> <span data-ttu-id="3776e-131">Pour plus d’informations, consultez [Corrélation de la télémétrie](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="3776e-131">See [telemetry correlation](application-insights-correlation.md) for details.</span></span>

<span data-ttu-id="3776e-132">Longueur maximale : 128</span><span class="sxs-lookup"><span data-stu-id="3776e-132">Max length: 128</span></span>


##<a name="operation-name"></a><span data-ttu-id="3776e-133">Nom d’opération</span><span class="sxs-lookup"><span data-stu-id="3776e-133">Operation name</span></span>

<span data-ttu-id="3776e-134">nom Hello (groupe) de l’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="3776e-134">hello name (group) of hello operation.</span></span> <span data-ttu-id="3776e-135">nom de l’opération Hello est créé par une demande ou un affichage de page.</span><span class="sxs-lookup"><span data-stu-id="3776e-135">hello operation name is created by either a request or a page view.</span></span> <span data-ttu-id="3776e-136">Tous les autres éléments de télémétrie définir cette valeur de toohello de champ pour hello contenant la demande ou la page de vue.</span><span class="sxs-lookup"><span data-stu-id="3776e-136">All other telemetry items set this field toohello value for hello containing request or page view.</span></span> <span data-ttu-id="3776e-137">Nom de l’opération est utilisée pour rechercher tous les éléments de télémétrie hello pour un groupe d’opérations (par exemple ' GET Home/Index »).</span><span class="sxs-lookup"><span data-stu-id="3776e-137">Operation name is used for finding all hello telemetry items for a group of operations (for example 'GET Home/Index').</span></span> <span data-ttu-id="3776e-138">Cette propriété de contexte est utilisé tooanswer questions du type « quels sont les exceptions standard hello levées sur cette page. »</span><span class="sxs-lookup"><span data-stu-id="3776e-138">This context property is used tooanswer questions like "what are hello typical exceptions thrown on this page."</span></span>

<span data-ttu-id="3776e-139">Longueur maximale : 1024</span><span class="sxs-lookup"><span data-stu-id="3776e-139">Max length: 1024</span></span>


##<a name="synthetic-source-of-hello-operation"></a><span data-ttu-id="3776e-140">Source synthétique d’opération de hello</span><span class="sxs-lookup"><span data-stu-id="3776e-140">Synthetic source of hello operation</span></span>

<span data-ttu-id="3776e-141">Nom de la source synthétique.</span><span class="sxs-lookup"><span data-stu-id="3776e-141">Name of synthetic source.</span></span> <span data-ttu-id="3776e-142">Certaines données de télémétrie à partir de l’application hello peuvent représenter le trafic synthétique.</span><span class="sxs-lookup"><span data-stu-id="3776e-142">Some telemetry from hello application may represent synthetic traffic.</span></span> <span data-ttu-id="3776e-143">Il peut être du robot d’indexation hello web site web, tests de disponibilité de site ou des traces à partir de bibliothèques de diagnostic à Application Insights SDK lui-même.</span><span class="sxs-lookup"><span data-stu-id="3776e-143">It may be web crawler indexing hello web site, site availability tests, or traces from diagnostic libraries like Application Insights SDK itself.</span></span>

<span data-ttu-id="3776e-144">Longueur maximale : 1024</span><span class="sxs-lookup"><span data-stu-id="3776e-144">Max length: 1024</span></span>


##<a name="session-id"></a><span data-ttu-id="3776e-145">ID de session</span><span class="sxs-lookup"><span data-stu-id="3776e-145">Session id</span></span>

<span data-ttu-id="3776e-146">ID de session - instance hello d’interaction de l’utilisateur hello avec application hello.</span><span class="sxs-lookup"><span data-stu-id="3776e-146">Session ID - hello instance of hello user's interaction with hello app.</span></span> <span data-ttu-id="3776e-147">Les informations dans les champs de contexte de session hello sont toujours sur l’utilisateur final de hello.</span><span class="sxs-lookup"><span data-stu-id="3776e-147">Information in hello session context fields is always about hello end user.</span></span> <span data-ttu-id="3776e-148">Lors de la télémétrie est envoyée à partir d’un service, le contexte de session hello est sur l’utilisateur hello qui a lancé une opération de service de hello hello.</span><span class="sxs-lookup"><span data-stu-id="3776e-148">When telemetry is sent from a service, hello session context is about hello user that initiated hello operation in hello service.</span></span>

<span data-ttu-id="3776e-149">Longueur maximale : 64</span><span class="sxs-lookup"><span data-stu-id="3776e-149">Max length: 64</span></span>


##<a name="anonymous-user-id"></a><span data-ttu-id="3776e-150">ID d’utilisateur anonyme</span><span class="sxs-lookup"><span data-stu-id="3776e-150">Anonymous user id</span></span>

<span data-ttu-id="3776e-151">ID d’utilisateur anonyme. Représente l’utilisateur final de hello de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="3776e-151">Anonymous user id. Represents hello end user of hello application.</span></span> <span data-ttu-id="3776e-152">Lors de la télémétrie est envoyée à partir d’un service, contexte de l’utilisateur hello est sur l’utilisateur hello qui a lancé une opération de service de hello hello.</span><span class="sxs-lookup"><span data-stu-id="3776e-152">When telemetry is sent from a service, hello user context is about hello user that initiated hello operation in hello service.</span></span>

<span data-ttu-id="3776e-153">[Échantillonnage](app-insights-sampling.md) est un des hello techniques toominimize hello quantité des données de télémétrie collectées.</span><span class="sxs-lookup"><span data-stu-id="3776e-153">[Sampling](app-insights-sampling.md) is one of hello techniques toominimize hello amount of collected telemetry.</span></span> <span data-ttu-id="3776e-154">Échantillonnage algorithme tentatives tooeither exemple ou annuler tous les hello corrélés télémétrie.</span><span class="sxs-lookup"><span data-stu-id="3776e-154">Sampling algorithm attempts tooeither sample in or out all hello correlated telemetry.</span></span> <span data-ttu-id="3776e-155">L’ID d’utilisateur anonyme est utilisé pour la génération de score d’échantillonnage.</span><span class="sxs-lookup"><span data-stu-id="3776e-155">Anonymous user id is used for sampling score generation.</span></span> <span data-ttu-id="3776e-156">L’ID d’utilisateur anonyme doit donc être une valeur suffisamment aléatoire.</span><span class="sxs-lookup"><span data-stu-id="3776e-156">So anonymous user id should be a random enough value.</span></span> 

<span data-ttu-id="3776e-157">À l’aide du nom d’utilisateur utilisateur anonyme id toostore est une utilisation incorrecte d’un champ de hello.</span><span class="sxs-lookup"><span data-stu-id="3776e-157">Using anonymous user id toostore user name is a misuse of hello field.</span></span> <span data-ttu-id="3776e-158">Utilisez un ID d’utilisateur authentifié.</span><span class="sxs-lookup"><span data-stu-id="3776e-158">Use Authenticated user id.</span></span>

<span data-ttu-id="3776e-159">Longueur maximale : 128</span><span class="sxs-lookup"><span data-stu-id="3776e-159">Max length: 128</span></span>


##<a name="authenticated-user-id"></a><span data-ttu-id="3776e-160">ID d’utilisateur authentifié</span><span class="sxs-lookup"><span data-stu-id="3776e-160">Authenticated user id</span></span>

<span data-ttu-id="3776e-161">Id de l’utilisateur authentifié. Hello opposé de l’id d’utilisateur anonyme, ce champ représente l’utilisateur hello avec un nom convivial.</span><span class="sxs-lookup"><span data-stu-id="3776e-161">Authenticated user id. hello opposite of anonymous user id, this field represents hello user with a friendly name.</span></span> <span data-ttu-id="3776e-162">Comme il s’agit de ses informations d’identification personnelle, par défaut, il n’est pas collecté par la plupart des SDK.</span><span class="sxs-lookup"><span data-stu-id="3776e-162">Since its PII information it is not collected by default by most SDK.</span></span>

<span data-ttu-id="3776e-163">Longueur maximale : 1024</span><span class="sxs-lookup"><span data-stu-id="3776e-163">Max length: 1024</span></span>


##<a name="account-id"></a><span data-ttu-id="3776e-164">ID de compte</span><span class="sxs-lookup"><span data-stu-id="3776e-164">Account id</span></span>

<span data-ttu-id="3776e-165">Dans les applications mutualisées agit hello l’ID de compte ou nom, les utilisateurs hello agit avec.</span><span class="sxs-lookup"><span data-stu-id="3776e-165">In multi-tenant applications this is hello account ID or name, which hello user is acting with.</span></span> <span data-ttu-id="3776e-166">C’est par exemple l’ID d’abonnement pour le portail Azure ou un nom de blogueur pour une plateforme de blog.</span><span class="sxs-lookup"><span data-stu-id="3776e-166">Examples may be subscription ID for Azure portal or blog name blogging platform.</span></span>

<span data-ttu-id="3776e-167">Longueur maximale : 1024</span><span class="sxs-lookup"><span data-stu-id="3776e-167">Max length: 1024</span></span>


##<a name="cloud-role"></a><span data-ttu-id="3776e-168">Rôle cloud</span><span class="sxs-lookup"><span data-stu-id="3776e-168">Cloud role</span></span>

<span data-ttu-id="3776e-169">Nom de l’application de hello hello rôle fait partie de.</span><span class="sxs-lookup"><span data-stu-id="3776e-169">Name of hello role hello application is a part of.</span></span> <span data-ttu-id="3776e-170">Mappe directement le nom du rôle toohello dans azure.</span><span class="sxs-lookup"><span data-stu-id="3776e-170">Maps directly toohello role name in azure.</span></span> <span data-ttu-id="3776e-171">Peut également être utilisé toodistinguish micro services, qui font partie d’une application unique.</span><span class="sxs-lookup"><span data-stu-id="3776e-171">Can also be used toodistinguish micro services, which are part of a single application.</span></span>

<span data-ttu-id="3776e-172">Longueur maximale : 256</span><span class="sxs-lookup"><span data-stu-id="3776e-172">Max length: 256</span></span>


##<a name="cloud-role-instance"></a><span data-ttu-id="3776e-173">Instance de rôle cloud</span><span class="sxs-lookup"><span data-stu-id="3776e-173">Cloud role instance</span></span>

<span data-ttu-id="3776e-174">Nom d’instance hello où l’application hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="3776e-174">Name of hello instance where hello application is running.</span></span> <span data-ttu-id="3776e-175">Nom de l’ordinateur pour un ordinateur local, nom de l’instance pour Azure.</span><span class="sxs-lookup"><span data-stu-id="3776e-175">Computer name for on-premises, instance name for Azure.</span></span>

<span data-ttu-id="3776e-176">Longueur maximale : 256</span><span class="sxs-lookup"><span data-stu-id="3776e-176">Max length: 256</span></span>


##<a name="internal-sdk-version"></a><span data-ttu-id="3776e-177">Interne : version du SDK</span><span class="sxs-lookup"><span data-stu-id="3776e-177">Internal: SDK version</span></span>

<span data-ttu-id="3776e-178">Version du SDK.</span><span class="sxs-lookup"><span data-stu-id="3776e-178">SDK version.</span></span> <span data-ttu-id="3776e-179">Pour plus d’informations, consultez https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification.</span><span class="sxs-lookup"><span data-stu-id="3776e-179">See https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification for information.</span></span>

<span data-ttu-id="3776e-180">Longueur maximale : 64</span><span class="sxs-lookup"><span data-stu-id="3776e-180">Max length: 64</span></span>


##<a name="internal-node-name"></a><span data-ttu-id="3776e-181">Interne : nom du nœud</span><span class="sxs-lookup"><span data-stu-id="3776e-181">Internal: Node name</span></span>

<span data-ttu-id="3776e-182">Ce champ représente le nom du nœud hello utilisé à des fins de facturation.</span><span class="sxs-lookup"><span data-stu-id="3776e-182">This field represents hello node name used for billing purposes.</span></span> <span data-ttu-id="3776e-183">Utiliser toooverride hello standard la détection des nœuds.</span><span class="sxs-lookup"><span data-stu-id="3776e-183">Use it toooverride hello standard detection of nodes.</span></span>

<span data-ttu-id="3776e-184">Longueur maximale : 256</span><span class="sxs-lookup"><span data-stu-id="3776e-184">Max length: 256</span></span>


## <a name="next-steps"></a><span data-ttu-id="3776e-185">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3776e-185">Next steps</span></span>

- <span data-ttu-id="3776e-186">Découvrez comment trop[étendre et de filtrer les données de télémétrie](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="3776e-186">Learn how too[extend and filter telemetry](app-insights-api-filtering-sampling.md).</span></span>
- <span data-ttu-id="3776e-187">Pour connaître les types et les modèles de données Application Insights, consultez [Modèle de données](application-insights-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="3776e-187">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="3776e-188">Découvrez la [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) de la collection de propriétés de contexte standard.</span><span class="sxs-lookup"><span data-stu-id="3776e-188">Check out standard context properties collection [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet).</span></span>
