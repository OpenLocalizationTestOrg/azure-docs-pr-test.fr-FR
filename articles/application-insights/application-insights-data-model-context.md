---
title: "Modèle de données de télémétrie d’Azure Application Insights- Contexte de télémétrie | Microsoft Docs"
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
ms.openlocfilehash: d6a0cad8bda6ca68aa691867e84f540c5ac9f6f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="telemetry-context-application-insights-data-model"></a><span data-ttu-id="ad906-103">Contexte de télémétrie : modèle de données d’Application Insights</span><span class="sxs-lookup"><span data-stu-id="ad906-103">Telemetry context: Application Insights data model</span></span>

<span data-ttu-id="ad906-104">Chaque élément de télémétrie peut avoir des champs de contexte fortement typés.</span><span class="sxs-lookup"><span data-stu-id="ad906-104">Every telemetry item may have a strongly typed context fields.</span></span> <span data-ttu-id="ad906-105">Chaque champ permet un scénario de surveillance spécifique.</span><span class="sxs-lookup"><span data-stu-id="ad906-105">Every field enables a specific monitoring scenario.</span></span> <span data-ttu-id="ad906-106">Utilisez la collection de propriétés personnalisées pour stocker des informations contextuelles personnalisées ou spécifiques à l’application.</span><span class="sxs-lookup"><span data-stu-id="ad906-106">Use the custom properties collection to store custom or application-specific contextual information.</span></span>


##<a name="application-version"></a><span data-ttu-id="ad906-107">Version de l’application</span><span class="sxs-lookup"><span data-stu-id="ad906-107">Application version</span></span>

<span data-ttu-id="ad906-108">Les informations dans les champs de contexte de l’application concernent toujours l’application qui envoie les données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="ad906-108">Information in the application context fields is always about the application that is sending the telemetry.</span></span> <span data-ttu-id="ad906-109">La version de l’application est utilisée pour analyser la tendance des changements dans le comportement des applications et sa corrélation avec les déploiements.</span><span class="sxs-lookup"><span data-stu-id="ad906-109">Application version is used to analyze trend changes in the application behavior and its correlation to the deployments.</span></span>

<span data-ttu-id="ad906-110">Longueur maximale : 1024</span><span class="sxs-lookup"><span data-stu-id="ad906-110">Max length: 1024</span></span>


##<a name="client-ip-address"></a><span data-ttu-id="ad906-111">Adresse IP du client</span><span class="sxs-lookup"><span data-stu-id="ad906-111">Client IP address</span></span>

<span data-ttu-id="ad906-112">Adresse IP de l’appareil client.</span><span class="sxs-lookup"><span data-stu-id="ad906-112">The IP address of the client device.</span></span> <span data-ttu-id="ad906-113">IPv4 et IPv6 sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="ad906-113">IPv4 and IPv6 are supported.</span></span> <span data-ttu-id="ad906-114">Quand des données de télémétrie sont envoyées à partir d’un service, le contexte de l’emplacement concerne l’utilisateur qui a lancé l’opération dans le service.</span><span class="sxs-lookup"><span data-stu-id="ad906-114">When telemetry is sent from a service, the location context is about the user that initiated the operation in the service.</span></span> <span data-ttu-id="ad906-115">Application Insights extrait les informations d’emplacement géographique de l’adresse IP du client puis les tronque.</span><span class="sxs-lookup"><span data-stu-id="ad906-115">Application Insights extract the geo-location information from the client IP and then truncate it.</span></span> <span data-ttu-id="ad906-116">Ainsi, l’adresse IP du client en elle-même ne peut pas être utilisée comme information identifiable de l’utilisateur final.</span><span class="sxs-lookup"><span data-stu-id="ad906-116">So client IP by itself cannot be used as end-user identifiable information.</span></span> 

<span data-ttu-id="ad906-117">Longueur maximale : 46</span><span class="sxs-lookup"><span data-stu-id="ad906-117">Max length: 46</span></span>


##<a name="device-type"></a><span data-ttu-id="ad906-118">Type d’appareil</span><span class="sxs-lookup"><span data-stu-id="ad906-118">Device type</span></span>

<span data-ttu-id="ad906-119">À l’origine, ce champ était utilisé pour indiquer le type de l’appareil utilisé par l’utilisateur final de l’application.</span><span class="sxs-lookup"><span data-stu-id="ad906-119">Originally this field was used to indicate the type of the device the end user of the application is using.</span></span> <span data-ttu-id="ad906-120">Aujourd’hui, il est utilisé principalement pour distinguer la télémétrie JavaScript avec le type d’appareil « Navigateur » de la télémétrie côté serveur avec le type d’appareil « PC ».</span><span class="sxs-lookup"><span data-stu-id="ad906-120">Today used primarily to distinguish JavaScript telemetry with the device type 'Browser' from server-side telemetry with the device type 'PC'.</span></span>

<span data-ttu-id="ad906-121">Longueur maximale : 64</span><span class="sxs-lookup"><span data-stu-id="ad906-121">Max length: 64</span></span>


##<a name="operation-id"></a><span data-ttu-id="ad906-122">ID d’opération</span><span class="sxs-lookup"><span data-stu-id="ad906-122">Operation id</span></span>

<span data-ttu-id="ad906-123">Identificateur unique de l’opération racine.</span><span class="sxs-lookup"><span data-stu-id="ad906-123">A unique identifier of the root operation.</span></span> <span data-ttu-id="ad906-124">Cet identificateur permet de regrouper les données de télémétrie pour plusieurs composants.</span><span class="sxs-lookup"><span data-stu-id="ad906-124">This identifier allows to group telemetry across multiple components.</span></span> <span data-ttu-id="ad906-125">Pour plus d’informations, consultez [Corrélation de la télémétrie](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="ad906-125">See [telemetry correlation](application-insights-correlation.md) for details.</span></span> <span data-ttu-id="ad906-126">L’ID d’opération est créé par une demande ou par la vue d’une page.</span><span class="sxs-lookup"><span data-stu-id="ad906-126">The operation id is created by either a request or a page view.</span></span> <span data-ttu-id="ad906-127">Le reste de la télémétrie définit ce champ sur la valeur correspondant à la demande ou à la vue de page qui la contient.</span><span class="sxs-lookup"><span data-stu-id="ad906-127">All other telemetry sets this field to the value for the containing request or page view.</span></span> 

<span data-ttu-id="ad906-128">Longueur maximale : 128</span><span class="sxs-lookup"><span data-stu-id="ad906-128">Max length: 128</span></span>


##<a name="parent-operation-id"></a><span data-ttu-id="ad906-129">ID d’opération parent</span><span class="sxs-lookup"><span data-stu-id="ad906-129">Parent operation ID</span></span>

<span data-ttu-id="ad906-130">Identificateur unique du parent immédiat de l’élément de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="ad906-130">The unique identifier of the telemetry item's immediate parent.</span></span> <span data-ttu-id="ad906-131">Pour plus d’informations, consultez [Corrélation de la télémétrie](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="ad906-131">See [telemetry correlation](application-insights-correlation.md) for details.</span></span>

<span data-ttu-id="ad906-132">Longueur maximale : 128</span><span class="sxs-lookup"><span data-stu-id="ad906-132">Max length: 128</span></span>


##<a name="operation-name"></a><span data-ttu-id="ad906-133">Nom d’opération</span><span class="sxs-lookup"><span data-stu-id="ad906-133">Operation name</span></span>

<span data-ttu-id="ad906-134">Nom (groupe) de l’opération.</span><span class="sxs-lookup"><span data-stu-id="ad906-134">The name (group) of the operation.</span></span> <span data-ttu-id="ad906-135">Le nom de l’opération est créé par une demande ou par la vue d’une page.</span><span class="sxs-lookup"><span data-stu-id="ad906-135">The operation name is created by either a request or a page view.</span></span> <span data-ttu-id="ad906-136">Tous les autres éléments de télémétrie définissent ce champ sur la valeur correspondant à la demande ou à la vue de page qui la contient.</span><span class="sxs-lookup"><span data-stu-id="ad906-136">All other telemetry items set this field to the value for the containing request or page view.</span></span> <span data-ttu-id="ad906-137">Le nom de l’opération est utilisé pour rechercher tous les éléments de télémétrie pour un groupe d’opérations (par exemple « GET Home/Index »).</span><span class="sxs-lookup"><span data-stu-id="ad906-137">Operation name is used for finding all the telemetry items for a group of operations (for example 'GET Home/Index').</span></span> <span data-ttu-id="ad906-138">Cette propriété de contexte est utilisée pour répondre à des questions comme « quelles sont les exceptions généralement levées sur cette page ? ».</span><span class="sxs-lookup"><span data-stu-id="ad906-138">This context property is used to answer questions like "what are the typical exceptions thrown on this page."</span></span>

<span data-ttu-id="ad906-139">Longueur maximale : 1024</span><span class="sxs-lookup"><span data-stu-id="ad906-139">Max length: 1024</span></span>


##<a name="synthetic-source-of-the-operation"></a><span data-ttu-id="ad906-140">Source synthétique de l’opération</span><span class="sxs-lookup"><span data-stu-id="ad906-140">Synthetic source of the operation</span></span>

<span data-ttu-id="ad906-141">Nom de la source synthétique.</span><span class="sxs-lookup"><span data-stu-id="ad906-141">Name of synthetic source.</span></span> <span data-ttu-id="ad906-142">Certaines données de télémétrie de l’application peuvent représenter le trafic synthétique.</span><span class="sxs-lookup"><span data-stu-id="ad906-142">Some telemetry from the application may represent synthetic traffic.</span></span> <span data-ttu-id="ad906-143">Il peut s’agir d’un robot d’indexation web indexant le site web, de tests de disponibilité du site ou de traces de bibliothèques de diagnostic, comme le SDK Application Insights lui-même.</span><span class="sxs-lookup"><span data-stu-id="ad906-143">It may be web crawler indexing the web site, site availability tests, or traces from diagnostic libraries like Application Insights SDK itself.</span></span>

<span data-ttu-id="ad906-144">Longueur maximale : 1024</span><span class="sxs-lookup"><span data-stu-id="ad906-144">Max length: 1024</span></span>


##<a name="session-id"></a><span data-ttu-id="ad906-145">ID de session</span><span class="sxs-lookup"><span data-stu-id="ad906-145">Session id</span></span>

<span data-ttu-id="ad906-146">ID de session : l’instance de l’interaction de l’utilisateur avec l’application.</span><span class="sxs-lookup"><span data-stu-id="ad906-146">Session ID - the instance of the user's interaction with the app.</span></span> <span data-ttu-id="ad906-147">Les informations dans les champs de contexte de session concernent toujours l’utilisateur final.</span><span class="sxs-lookup"><span data-stu-id="ad906-147">Information in the session context fields is always about the end user.</span></span> <span data-ttu-id="ad906-148">Quand des données de télémétrie sont envoyées à partir d’un service, le contexte de session concerne l’utilisateur qui a lancé l’opération dans le service.</span><span class="sxs-lookup"><span data-stu-id="ad906-148">When telemetry is sent from a service, the session context is about the user that initiated the operation in the service.</span></span>

<span data-ttu-id="ad906-149">Longueur maximale : 64</span><span class="sxs-lookup"><span data-stu-id="ad906-149">Max length: 64</span></span>


##<a name="anonymous-user-id"></a><span data-ttu-id="ad906-150">ID d’utilisateur anonyme</span><span class="sxs-lookup"><span data-stu-id="ad906-150">Anonymous user id</span></span>

<span data-ttu-id="ad906-151">ID d’utilisateur anonyme.</span><span class="sxs-lookup"><span data-stu-id="ad906-151">Anonymous user id.</span></span> <span data-ttu-id="ad906-152">Représente l’utilisateur final de l’application.</span><span class="sxs-lookup"><span data-stu-id="ad906-152">Represents the end user of the application.</span></span> <span data-ttu-id="ad906-153">Quand des données de télémétrie sont envoyées à partir d’un service, le contexte d’utilisateur concerne l’utilisateur qui a lancé l’opération dans le service.</span><span class="sxs-lookup"><span data-stu-id="ad906-153">When telemetry is sent from a service, the user context is about the user that initiated the operation in the service.</span></span>

<span data-ttu-id="ad906-154">[L’échantillonnage](app-insights-sampling.md) est une des techniques pour réduire la quantité de données de télémétrie collectées.</span><span class="sxs-lookup"><span data-stu-id="ad906-154">[Sampling](app-insights-sampling.md) is one of the techniques to minimize the amount of collected telemetry.</span></span> <span data-ttu-id="ad906-155">L’algorithme d’échantillonnage tente de prélever des échantillons dans ou en dehors de toute la télémétrie corrélée.</span><span class="sxs-lookup"><span data-stu-id="ad906-155">Sampling algorithm attempts to either sample in or out all the correlated telemetry.</span></span> <span data-ttu-id="ad906-156">L’ID d’utilisateur anonyme est utilisé pour la génération de score d’échantillonnage.</span><span class="sxs-lookup"><span data-stu-id="ad906-156">Anonymous user id is used for sampling score generation.</span></span> <span data-ttu-id="ad906-157">L’ID d’utilisateur anonyme doit donc être une valeur suffisamment aléatoire.</span><span class="sxs-lookup"><span data-stu-id="ad906-157">So anonymous user id should be a random enough value.</span></span> 

<span data-ttu-id="ad906-158">Utiliser l’ID d’utilisateur anonyme pour stocker un nom d’utilisateur est une utilisation incorrecte du champ.</span><span class="sxs-lookup"><span data-stu-id="ad906-158">Using anonymous user id to store user name is a misuse of the field.</span></span> <span data-ttu-id="ad906-159">Utilisez un ID d’utilisateur authentifié.</span><span class="sxs-lookup"><span data-stu-id="ad906-159">Use Authenticated user id.</span></span>

<span data-ttu-id="ad906-160">Longueur maximale : 128</span><span class="sxs-lookup"><span data-stu-id="ad906-160">Max length: 128</span></span>


##<a name="authenticated-user-id"></a><span data-ttu-id="ad906-161">ID d’utilisateur authentifié</span><span class="sxs-lookup"><span data-stu-id="ad906-161">Authenticated user id</span></span>

<span data-ttu-id="ad906-162">ID d’utilisateur authentifié.</span><span class="sxs-lookup"><span data-stu-id="ad906-162">Authenticated user id.</span></span> <span data-ttu-id="ad906-163">À l’opposé de l’ID d’utilisateur anonyme, ce champ représente l’utilisateur avec un nom convivial.</span><span class="sxs-lookup"><span data-stu-id="ad906-163">The opposite of anonymous user id, this field represents the user with a friendly name.</span></span> <span data-ttu-id="ad906-164">Comme il s’agit de ses informations d’identification personnelle, par défaut, il n’est pas collecté par la plupart des SDK.</span><span class="sxs-lookup"><span data-stu-id="ad906-164">Since its PII information it is not collected by default by most SDK.</span></span>

<span data-ttu-id="ad906-165">Longueur maximale : 1024</span><span class="sxs-lookup"><span data-stu-id="ad906-165">Max length: 1024</span></span>


##<a name="account-id"></a><span data-ttu-id="ad906-166">ID de compte</span><span class="sxs-lookup"><span data-stu-id="ad906-166">Account id</span></span>

<span data-ttu-id="ad906-167">Dans les applications multi-locataires, il s’agit de l’ID ou du nom du compte avec lequel l’utilisateur agit.</span><span class="sxs-lookup"><span data-stu-id="ad906-167">In multi-tenant applications this is the account ID or name, which the user is acting with.</span></span> <span data-ttu-id="ad906-168">C’est par exemple l’ID d’abonnement pour le portail Azure ou un nom de blogueur pour une plateforme de blog.</span><span class="sxs-lookup"><span data-stu-id="ad906-168">Examples may be subscription ID for Azure portal or blog name blogging platform.</span></span>

<span data-ttu-id="ad906-169">Longueur maximale : 1024</span><span class="sxs-lookup"><span data-stu-id="ad906-169">Max length: 1024</span></span>


##<a name="cloud-role"></a><span data-ttu-id="ad906-170">Rôle cloud</span><span class="sxs-lookup"><span data-stu-id="ad906-170">Cloud role</span></span>

<span data-ttu-id="ad906-171">Nom du rôle dont l’application fait partie.</span><span class="sxs-lookup"><span data-stu-id="ad906-171">Name of the role the application is a part of.</span></span> <span data-ttu-id="ad906-172">Mappé directement au le nom du rôle dans Azure.</span><span class="sxs-lookup"><span data-stu-id="ad906-172">Maps directly to the role name in azure.</span></span> <span data-ttu-id="ad906-173">Peut également être utilisé pour distinguer des microservices, qui font partie d’une même application.</span><span class="sxs-lookup"><span data-stu-id="ad906-173">Can also be used to distinguish micro services, which are part of a single application.</span></span>

<span data-ttu-id="ad906-174">Longueur maximale : 256</span><span class="sxs-lookup"><span data-stu-id="ad906-174">Max length: 256</span></span>


##<a name="cloud-role-instance"></a><span data-ttu-id="ad906-175">Instance de rôle cloud</span><span class="sxs-lookup"><span data-stu-id="ad906-175">Cloud role instance</span></span>

<span data-ttu-id="ad906-176">Nom de l’instance où l’application s’exécute.</span><span class="sxs-lookup"><span data-stu-id="ad906-176">Name of the instance where the application is running.</span></span> <span data-ttu-id="ad906-177">Nom de l’ordinateur pour un ordinateur local, nom de l’instance pour Azure.</span><span class="sxs-lookup"><span data-stu-id="ad906-177">Computer name for on-premises, instance name for Azure.</span></span>

<span data-ttu-id="ad906-178">Longueur maximale : 256</span><span class="sxs-lookup"><span data-stu-id="ad906-178">Max length: 256</span></span>


##<a name="internal-sdk-version"></a><span data-ttu-id="ad906-179">Interne : version du SDK</span><span class="sxs-lookup"><span data-stu-id="ad906-179">Internal: SDK version</span></span>

<span data-ttu-id="ad906-180">Version du SDK.</span><span class="sxs-lookup"><span data-stu-id="ad906-180">SDK version.</span></span> <span data-ttu-id="ad906-181">Pour plus d’informations, consultez https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification.</span><span class="sxs-lookup"><span data-stu-id="ad906-181">See https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification for information.</span></span>

<span data-ttu-id="ad906-182">Longueur maximale : 64</span><span class="sxs-lookup"><span data-stu-id="ad906-182">Max length: 64</span></span>


##<a name="internal-node-name"></a><span data-ttu-id="ad906-183">Interne : nom du nœud</span><span class="sxs-lookup"><span data-stu-id="ad906-183">Internal: Node name</span></span>

<span data-ttu-id="ad906-184">Ce champ représente le nom du nœud utilisé pour la facturation.</span><span class="sxs-lookup"><span data-stu-id="ad906-184">This field represents the node name used for billing purposes.</span></span> <span data-ttu-id="ad906-185">Utilisez-le pour remplacer la détection standard de nœuds.</span><span class="sxs-lookup"><span data-stu-id="ad906-185">Use it to override the standard detection of nodes.</span></span>

<span data-ttu-id="ad906-186">Longueur maximale : 256</span><span class="sxs-lookup"><span data-stu-id="ad906-186">Max length: 256</span></span>


## <a name="next-steps"></a><span data-ttu-id="ad906-187">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ad906-187">Next steps</span></span>

- <span data-ttu-id="ad906-188">Découvrez comment [étendre et filtrer la télémétrie](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="ad906-188">Learn how to [extend and filter telemetry](app-insights-api-filtering-sampling.md).</span></span>
- <span data-ttu-id="ad906-189">Pour connaître les types et les modèles de données Application Insights, consultez [Modèle de données](application-insights-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="ad906-189">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="ad906-190">Découvrez la [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) de la collection de propriétés de contexte standard.</span><span class="sxs-lookup"><span data-stu-id="ad906-190">Check out standard context properties collection [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet).</span></span>
