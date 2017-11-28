---
title: "Contrôle de version des Kits de développement logiciel (SDK) clients et serveurs dans Mobile Apps et Mobile Services | Microsoft Docs"
description: "Liste des Kits de développement logiciel (SDK) clients et des compatibilités avec les versions des Kits de développement logiciel (SDK) serveurs pour Mobile Services et Azure Mobile Apps"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 35b19672-c9d6-49b5-b405-a6dcd1107cd5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: f79e819b1547f81498ea213858faf3c75e374782
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="client-and-server-versioning-in-mobile-apps-and-mobile-services"></a><span data-ttu-id="eb51a-103">Contrôle de version client et serveur dans Mobile Apps et Mobile Services</span><span class="sxs-lookup"><span data-stu-id="eb51a-103">Client and server versioning in Mobile Apps and Mobile Services</span></span>
<span data-ttu-id="eb51a-104">La dernière version d'Azure Mobile Services est la fonctionnalité **Mobile Apps** d'Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="eb51a-104">The latest version of Azure Mobile Services is the **Mobile Apps** feature of Azure App Service.</span></span>

<span data-ttu-id="eb51a-105">Les Kits de développement logiciel (SDK) clients et serveurs Mobile Apps se fondent à l'origine sur ceux de Mobile Services, mais ils ne sont *pas* compatibles les uns avec les autres.</span><span class="sxs-lookup"><span data-stu-id="eb51a-105">The Mobile Apps client and server SDKs are originally based on those in Mobile Services, but they are *not* compatible with each other.</span></span>
<span data-ttu-id="eb51a-106">Autrement dit, vous devez utiliser un SDK client *Mobile Apps* avec un SDK serveur *Mobile Apps* et il en est de même pour *Mobile Services*.</span><span class="sxs-lookup"><span data-stu-id="eb51a-106">That is, you must use a *Mobile Apps* client SDK with a *Mobile Apps* server SDK and similarly for *Mobile Services*.</span></span> <span data-ttu-id="eb51a-107">Ce contrat s'applique au moyen d'une valeur d'en-tête spéciale utilisée par les SDK clients et serveurs, `ZUMO-API-VERSION`.</span><span class="sxs-lookup"><span data-stu-id="eb51a-107">This contract is enforced through a special header value used by the client and server SDKs, `ZUMO-API-VERSION`.</span></span>

<span data-ttu-id="eb51a-108">Remarque : chaque fois que ce document fait référence à un backend *Mobile Services* , il n'est pas nécessaire qu'il soit hébergé sur Mobile Services.</span><span class="sxs-lookup"><span data-stu-id="eb51a-108">Note: whenever this document refers to a *Mobile Services* backend, it does not necessarily need to be hosted on Mobile Services.</span></span> <span data-ttu-id="eb51a-109">Il est désormais possible de faire migrer un service mobile sur App Service sans aucune modification de code, mais dans ce cas le service utilisera toujours les versions du SDK *Mobile Services*.</span><span class="sxs-lookup"><span data-stu-id="eb51a-109">It is now possible to migrate a mobile service to run on App Service without any code changes, but the service would still be using *Mobile Services*  SDK versions.</span></span>

<span data-ttu-id="eb51a-110">Pour en savoir plus sur la migration vers App Service sans aucune modification de code, consultez l’article [Migrer un service Mobile Services sur Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="eb51a-110">To learn more about migrating to App Service without any code changes, see the article [Migrate a Mobile Service to Azure App Service].</span></span>

## <a name="header-specification"></a><span data-ttu-id="eb51a-111">Spécification de l’en-tête</span><span class="sxs-lookup"><span data-stu-id="eb51a-111">Header specification</span></span>
<span data-ttu-id="eb51a-112">La clé `ZUMO-API-VERSION` peut être spécifiée dans l'en-tête HTTP ou dans la chaîne de requête.</span><span class="sxs-lookup"><span data-stu-id="eb51a-112">The key `ZUMO-API-VERSION` may be specified in either the HTTP header or the query string.</span></span> <span data-ttu-id="eb51a-113">La valeur est une chaîne de version sous la forme **x.y.z**.</span><span class="sxs-lookup"><span data-stu-id="eb51a-113">The value is a version string in the form **x.y.z**.</span></span>

<span data-ttu-id="eb51a-114">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="eb51a-114">For example:</span></span>

<span data-ttu-id="eb51a-115">GET https://service.azurewebsites.net/tables/TodoItem</span><span class="sxs-lookup"><span data-stu-id="eb51a-115">GET https://service.azurewebsites.net/tables/TodoItem</span></span>

<span data-ttu-id="eb51a-116">HEADERS: ZUMO-API-VERSION: 2.0.0</span><span class="sxs-lookup"><span data-stu-id="eb51a-116">HEADERS: ZUMO-API-VERSION: 2.0.0</span></span>

<span data-ttu-id="eb51a-117">POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0</span><span class="sxs-lookup"><span data-stu-id="eb51a-117">POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0</span></span>

## <a name="opting-out-of-version-checking"></a><span data-ttu-id="eb51a-118">Désactivation de la vérification de version</span><span class="sxs-lookup"><span data-stu-id="eb51a-118">Opting out of version checking</span></span>
<span data-ttu-id="eb51a-119">Vous pouvez désactiver la vérification de version en définissant la valeur **true** pour le paramètre d’application **MS_SkipVersionCheck**.</span><span class="sxs-lookup"><span data-stu-id="eb51a-119">You can opt out of version checking by setting a value of **true** for the app setting **MS_SkipVersionCheck**.</span></span> <span data-ttu-id="eb51a-120">Spécifiez cette valeur dans votre fichier web.config ou dans la section Paramètres de l’application du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="eb51a-120">Specify this either in your web.config or in the Application Settings section of the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="eb51a-121">Il existe un certain nombre de différences de comportement entre Mobile Services et Mobile Apps, en particulier dans les domaines de la synchronisation hors connexion, de l'authentification et des notifications Push.</span><span class="sxs-lookup"><span data-stu-id="eb51a-121">There are a number of behavior changes between Mobile Services and Mobile Apps, particularly in the areas of offline sync, authentication, and push notifications.</span></span> <span data-ttu-id="eb51a-122">Avant de désactiver la vérification de version, assurez-vous par des tests complets que ces modifications de comportement ne suppriment pas de fonctionnalités dans votre application.</span><span class="sxs-lookup"><span data-stu-id="eb51a-122">You should only opt out of version checking after complete testing to ensure that these behavioral changes do not break your app's functionality.</span></span>
>
>

## <a name="summary-of-compatibility-for-all-versions"></a><span data-ttu-id="eb51a-123">Résumé des compatibilités pour toutes les versions</span><span class="sxs-lookup"><span data-stu-id="eb51a-123">Summary of compatibility for all versions</span></span>
<span data-ttu-id="eb51a-124">Le tableau ci-dessous indique les compatibilités entre tous les types de clients et de serveurs.</span><span class="sxs-lookup"><span data-stu-id="eb51a-124">The chart below shows the compatibility between all client and server types.</span></span> <span data-ttu-id="eb51a-125">Un backend est classé soit comme Mobile **Services**, soit comme Mobile **Apps** en fonction du SDK serveur qu’il utilise.</span><span class="sxs-lookup"><span data-stu-id="eb51a-125">A backend is classified as either Mobile **Services** or Mobile **Apps** based on the server SDK that it uses.</span></span>

|  | <span data-ttu-id="eb51a-126">**Mobile Services** Node.js ou .NET</span><span class="sxs-lookup"><span data-stu-id="eb51a-126">**Mobile Services** Node.js or .NET</span></span> | <span data-ttu-id="eb51a-127">**Mobile Apps** Node.js ou .NET</span><span class="sxs-lookup"><span data-stu-id="eb51a-127">**Mobile Apps** Node.js or .NET</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eb51a-128">[Clients Mobile Services]</span><span class="sxs-lookup"><span data-stu-id="eb51a-128">[Mobile Services clients]</span></span> |<span data-ttu-id="eb51a-129">OK</span><span class="sxs-lookup"><span data-stu-id="eb51a-129">Ok</span></span> |<span data-ttu-id="eb51a-130">Erreur\*</span><span class="sxs-lookup"><span data-stu-id="eb51a-130">Error\*</span></span> |
| <span data-ttu-id="eb51a-131">[Clients Mobile Apps]</span><span class="sxs-lookup"><span data-stu-id="eb51a-131">[Mobile Apps clients]</span></span> |<span data-ttu-id="eb51a-132">Erreur\*</span><span class="sxs-lookup"><span data-stu-id="eb51a-132">Error\*</span></span> |<span data-ttu-id="eb51a-133">OK</span><span class="sxs-lookup"><span data-stu-id="eb51a-133">Ok</span></span> |

<span data-ttu-id="eb51a-134">\*Peut être contrôlée en spécifiant **MS_SkipVersionCheck**.</span><span class="sxs-lookup"><span data-stu-id="eb51a-134">\*This can be controlled by specifying **MS_SkipVersionCheck**.</span></span>

<!-- IMPORTANT!  The anchors for Mobile Services and Mobile Apps MUST be 1.0.0 and 2.0.0 respectively, since there is an exception error message that uses those anchors. -->

<!-- NOTE: the fwlink to this document is http://go.microsoft.com/fwlink/?LinkID=690568 -->

## <span data-ttu-id="eb51a-135"><a name="1.0.0"></a>Client et serveur Mobile Services</span><span class="sxs-lookup"><span data-stu-id="eb51a-135"><a name="1.0.0"></a>Mobile Services client and server</span></span>
<span data-ttu-id="eb51a-136">Les SDK clients du tableau ci-dessous sont compatibles avec **Mobile Services**.</span><span class="sxs-lookup"><span data-stu-id="eb51a-136">The client SDKs in the table below are compatible with **Mobile Services**.</span></span>

<span data-ttu-id="eb51a-137">Remarque : les SDK clients Mobile Services n’envoient *pas* de valeur d’en-tête pour `ZUMO-API-VERSION`.</span><span class="sxs-lookup"><span data-stu-id="eb51a-137">Note: the Mobile Services client SDKs *do not* send a header value for `ZUMO-API-VERSION`.</span></span> <span data-ttu-id="eb51a-138">Si le service reçoit cette valeur d'en-tête ou de chaîne de requête, une erreur est renvoyée, sauf en cas de désactivation expresse comme indiqué ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="eb51a-138">If the service receives this header or query string value, an error will be returned, unless you have explicitly opted out as described above.</span></span>

### <span data-ttu-id="eb51a-139"><a name="MobileServicesClients"></a> SDK clients Mobile *Services*</span><span class="sxs-lookup"><span data-stu-id="eb51a-139"><a name="MobileServicesClients"></a> Mobile *Services* client SDKs</span></span>
| <span data-ttu-id="eb51a-140">Plateforme cliente</span><span class="sxs-lookup"><span data-stu-id="eb51a-140">Client platform</span></span> | <span data-ttu-id="eb51a-141">Version</span><span class="sxs-lookup"><span data-stu-id="eb51a-141">Version</span></span> | <span data-ttu-id="eb51a-142">Valeur d'en-tête de version</span><span class="sxs-lookup"><span data-stu-id="eb51a-142">Version header value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eb51a-143">Client géré (Windows, Xamarin)</span><span class="sxs-lookup"><span data-stu-id="eb51a-143">Managed client (Windows, Xamarin)</span></span> |[<span data-ttu-id="eb51a-144">1.3.2</span><span class="sxs-lookup"><span data-stu-id="eb51a-144">1.3.2</span></span>](https://www.nuget.org/packages/WindowsAzure.MobileServices/1.3.2) |<span data-ttu-id="eb51a-145">n/a</span><span class="sxs-lookup"><span data-stu-id="eb51a-145">n/a</span></span> |
| <span data-ttu-id="eb51a-146">iOS</span><span class="sxs-lookup"><span data-stu-id="eb51a-146">iOS</span></span> |[<span data-ttu-id="eb51a-147">2.2.2</span><span class="sxs-lookup"><span data-stu-id="eb51a-147">2.2.2</span></span>](http://aka.ms/gc6fex) |<span data-ttu-id="eb51a-148">n/a</span><span class="sxs-lookup"><span data-stu-id="eb51a-148">n/a</span></span> |
| <span data-ttu-id="eb51a-149">Android</span><span class="sxs-lookup"><span data-stu-id="eb51a-149">Android</span></span> |[<span data-ttu-id="eb51a-150">2.0.3</span><span class="sxs-lookup"><span data-stu-id="eb51a-150">2.0.3</span></span>](https://go.microsoft.com/fwLink/?LinkID=280126) |<span data-ttu-id="eb51a-151">n/a</span><span class="sxs-lookup"><span data-stu-id="eb51a-151">n/a</span></span> |
| <span data-ttu-id="eb51a-152">HTML</span><span class="sxs-lookup"><span data-stu-id="eb51a-152">HTML</span></span> |[<span data-ttu-id="eb51a-153">1.2.7</span><span class="sxs-lookup"><span data-stu-id="eb51a-153">1.2.7</span></span>](http://ajax.aspnetcdn.com/ajax/mobileservices/MobileServices.Web-1.2.7.min.js) |<span data-ttu-id="eb51a-154">n/a</span><span class="sxs-lookup"><span data-stu-id="eb51a-154">n/a</span></span> |

### <a name="mobile-services-server-sdks"></a><span data-ttu-id="eb51a-155">SDK serveurs Mobile *Services*</span><span class="sxs-lookup"><span data-stu-id="eb51a-155">Mobile *Services* server SDKs</span></span>
| <span data-ttu-id="eb51a-156">Plateforme de serveur</span><span class="sxs-lookup"><span data-stu-id="eb51a-156">Server platform</span></span> | <span data-ttu-id="eb51a-157">Version</span><span class="sxs-lookup"><span data-stu-id="eb51a-157">Version</span></span> | <span data-ttu-id="eb51a-158">En-têtes de versions acceptés</span><span class="sxs-lookup"><span data-stu-id="eb51a-158">Accepted version header</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eb51a-159">.NET</span><span class="sxs-lookup"><span data-stu-id="eb51a-159">.NET</span></span> |[<span data-ttu-id="eb51a-160">WindowsAzure.MobileServices.Backend.* Version 1.0.x</span><span class="sxs-lookup"><span data-stu-id="eb51a-160">WindowsAzure.MobileServices.Backend.* Version 1.0.x</span></span>](https://www.nuget.org/packages/WindowsAzure.MobileServices.Backend/) |<span data-ttu-id="eb51a-161">** Aucun en-tête de version **</span><span class="sxs-lookup"><span data-stu-id="eb51a-161">**No version header **</span></span> |
| <span data-ttu-id="eb51a-162">Node.js</span><span class="sxs-lookup"><span data-stu-id="eb51a-162">Node.js</span></span> |<span data-ttu-id="eb51a-163">(bientôt disponible)</span><span class="sxs-lookup"><span data-stu-id="eb51a-163">(coming soon)</span></span> |<span data-ttu-id="eb51a-164">**Aucun en-tête de version**</span><span class="sxs-lookup"><span data-stu-id="eb51a-164">**No version header**</span></span> |

<!-- TODO: add Node npm version -->

### <a name="behavior-of-mobile-services-backends"></a><span data-ttu-id="eb51a-165">Comportement des backends Mobile Services</span><span class="sxs-lookup"><span data-stu-id="eb51a-165">Behavior of Mobile Services backends</span></span>
| <span data-ttu-id="eb51a-166">ZUMO-API-VERSION</span><span class="sxs-lookup"><span data-stu-id="eb51a-166">ZUMO-API-VERSION</span></span> | <span data-ttu-id="eb51a-167">Valeur de MS_SkipVersionCheck</span><span class="sxs-lookup"><span data-stu-id="eb51a-167">Value of MS_SkipVersionCheck</span></span> | <span data-ttu-id="eb51a-168">Réponse</span><span class="sxs-lookup"><span data-stu-id="eb51a-168">Response</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eb51a-169">Non spécifié</span><span class="sxs-lookup"><span data-stu-id="eb51a-169">Not specified</span></span> |<span data-ttu-id="eb51a-170">Quelconque</span><span class="sxs-lookup"><span data-stu-id="eb51a-170">Any</span></span> |<span data-ttu-id="eb51a-171">200 - OK</span><span class="sxs-lookup"><span data-stu-id="eb51a-171">200 - OK</span></span> |
| <span data-ttu-id="eb51a-172">Valeur quelconque</span><span class="sxs-lookup"><span data-stu-id="eb51a-172">Any value</span></span> |<span data-ttu-id="eb51a-173">True</span><span class="sxs-lookup"><span data-stu-id="eb51a-173">True</span></span> |<span data-ttu-id="eb51a-174">200 - OK</span><span class="sxs-lookup"><span data-stu-id="eb51a-174">200 - OK</span></span> |
| <span data-ttu-id="eb51a-175">Valeur quelconque</span><span class="sxs-lookup"><span data-stu-id="eb51a-175">Any value</span></span> |<span data-ttu-id="eb51a-176">False/Non spécifié</span><span class="sxs-lookup"><span data-stu-id="eb51a-176">False/Not Specified</span></span> |<span data-ttu-id="eb51a-177">400 - Requête incorrecte</span><span class="sxs-lookup"><span data-stu-id="eb51a-177">400 - Bad Request</span></span> |

## <span data-ttu-id="eb51a-178"><a name="2.0.0"></a>Client et serveur Azure Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="eb51a-178"><a name="2.0.0"></a>Azure Mobile Apps client and server</span></span>
### <span data-ttu-id="eb51a-179"><a name="MobileAppsClients"></a> SDK clients Mobile *Apps*</span><span class="sxs-lookup"><span data-stu-id="eb51a-179"><a name="MobileAppsClients"></a> Mobile *Apps* client SDKs</span></span>
<span data-ttu-id="eb51a-180">La vérification de version a été introduite à partir des versions suivantes du SDK client pour **Azure Mobile Apps**:</span><span class="sxs-lookup"><span data-stu-id="eb51a-180">Version checking was introduced starting with the following versions of the client SDK for **Azure Mobile Apps**:</span></span>

| <span data-ttu-id="eb51a-181">Plateforme cliente</span><span class="sxs-lookup"><span data-stu-id="eb51a-181">Client platform</span></span> | <span data-ttu-id="eb51a-182">Version</span><span class="sxs-lookup"><span data-stu-id="eb51a-182">Version</span></span> | <span data-ttu-id="eb51a-183">Valeur d'en-tête de version</span><span class="sxs-lookup"><span data-stu-id="eb51a-183">Version header value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eb51a-184">Client géré (Windows, Xamarin)</span><span class="sxs-lookup"><span data-stu-id="eb51a-184">Managed client (Windows, Xamarin)</span></span> |[<span data-ttu-id="eb51a-185">2.0.0</span><span class="sxs-lookup"><span data-stu-id="eb51a-185">2.0.0</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/2.0.0) |<span data-ttu-id="eb51a-186">2.0.0</span><span class="sxs-lookup"><span data-stu-id="eb51a-186">2.0.0</span></span> |
| <span data-ttu-id="eb51a-187">iOS</span><span class="sxs-lookup"><span data-stu-id="eb51a-187">iOS</span></span> |[<span data-ttu-id="eb51a-188">3.0.0</span><span class="sxs-lookup"><span data-stu-id="eb51a-188">3.0.0</span></span>](http://go.microsoft.com/fwlink/?LinkID=529823) |<span data-ttu-id="eb51a-189">2.0.0</span><span class="sxs-lookup"><span data-stu-id="eb51a-189">2.0.0</span></span> |
| <span data-ttu-id="eb51a-190">Android</span><span class="sxs-lookup"><span data-stu-id="eb51a-190">Android</span></span> |[<span data-ttu-id="eb51a-191">3.0.0</span><span class="sxs-lookup"><span data-stu-id="eb51a-191">3.0.0</span></span>](http://go.microsoft.com/fwlink/?LinkID=717033&clcid=0x409) |<span data-ttu-id="eb51a-192">3.0.0</span><span class="sxs-lookup"><span data-stu-id="eb51a-192">3.0.0</span></span> |

<!-- TODO: add HTML version when released -->

### <a name="mobile-apps-server-sdks"></a><span data-ttu-id="eb51a-193">Kits de développement logiciel (SDK) du serveur Mobile *Apps*</span><span class="sxs-lookup"><span data-stu-id="eb51a-193">Mobile *Apps* server SDKs</span></span>
<span data-ttu-id="eb51a-194">La vérification de version est incluse dans les versions suivantes du SDK serveur :</span><span class="sxs-lookup"><span data-stu-id="eb51a-194">Version checking is included in following server SDK versions:</span></span>

| <span data-ttu-id="eb51a-195">Plateforme de serveur</span><span class="sxs-lookup"><span data-stu-id="eb51a-195">Server platform</span></span> | <span data-ttu-id="eb51a-196">Foundation</span><span class="sxs-lookup"><span data-stu-id="eb51a-196">SDK</span></span> | <span data-ttu-id="eb51a-197">En-têtes de versions acceptés</span><span class="sxs-lookup"><span data-stu-id="eb51a-197">Accepted version header</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eb51a-198">.NET</span><span class="sxs-lookup"><span data-stu-id="eb51a-198">.NET</span></span> |[<span data-ttu-id="eb51a-199">Microsoft.Azure.Mobile.Server</span><span class="sxs-lookup"><span data-stu-id="eb51a-199">Microsoft.Azure.Mobile.Server</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) |<span data-ttu-id="eb51a-200">2.0.0</span><span class="sxs-lookup"><span data-stu-id="eb51a-200">2.0.0</span></span> |
| <span data-ttu-id="eb51a-201">Node.js</span><span class="sxs-lookup"><span data-stu-id="eb51a-201">Node.js</span></span> |[<span data-ttu-id="eb51a-202">azure-mobile-apps)</span><span class="sxs-lookup"><span data-stu-id="eb51a-202">azure-mobile-apps)</span></span>](https://www.npmjs.com/package/azure-mobile-apps) |<span data-ttu-id="eb51a-203">2.0.0</span><span class="sxs-lookup"><span data-stu-id="eb51a-203">2.0.0</span></span> |

### <a name="behavior-of-mobile-apps-backends"></a><span data-ttu-id="eb51a-204">Comportement des serveurs principaux Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="eb51a-204">Behavior of Mobile Apps backends</span></span>
| <span data-ttu-id="eb51a-205">ZUMO-API-VERSION</span><span class="sxs-lookup"><span data-stu-id="eb51a-205">ZUMO-API-VERSION</span></span> | <span data-ttu-id="eb51a-206">Valeur de MS_SkipVersionCheck</span><span class="sxs-lookup"><span data-stu-id="eb51a-206">Value of MS_SkipVersionCheck</span></span> | <span data-ttu-id="eb51a-207">Réponse</span><span class="sxs-lookup"><span data-stu-id="eb51a-207">Response</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eb51a-208">x.y.z ou Null</span><span class="sxs-lookup"><span data-stu-id="eb51a-208">x.y.z or Null</span></span> |<span data-ttu-id="eb51a-209">True</span><span class="sxs-lookup"><span data-stu-id="eb51a-209">True</span></span> |<span data-ttu-id="eb51a-210">200 - OK</span><span class="sxs-lookup"><span data-stu-id="eb51a-210">200 - OK</span></span> |
| <span data-ttu-id="eb51a-211">Null</span><span class="sxs-lookup"><span data-stu-id="eb51a-211">Null</span></span> |<span data-ttu-id="eb51a-212">False/Non spécifié</span><span class="sxs-lookup"><span data-stu-id="eb51a-212">False/Not Specified</span></span> |<span data-ttu-id="eb51a-213">400 - Requête incorrecte</span><span class="sxs-lookup"><span data-stu-id="eb51a-213">400 - Bad Request</span></span> |
| <span data-ttu-id="eb51a-214">1.x.y</span><span class="sxs-lookup"><span data-stu-id="eb51a-214">1.x.y</span></span> |<span data-ttu-id="eb51a-215">False/Non spécifié</span><span class="sxs-lookup"><span data-stu-id="eb51a-215">False/Not Specified</span></span> |<span data-ttu-id="eb51a-216">400 - Requête incorrecte</span><span class="sxs-lookup"><span data-stu-id="eb51a-216">400 - Bad Request</span></span> |
| <span data-ttu-id="eb51a-217">2.0.0-2.x.y</span><span class="sxs-lookup"><span data-stu-id="eb51a-217">2.0.0-2.x.y</span></span> |<span data-ttu-id="eb51a-218">False/Non spécifié</span><span class="sxs-lookup"><span data-stu-id="eb51a-218">False/Not Specified</span></span> |<span data-ttu-id="eb51a-219">200 - OK</span><span class="sxs-lookup"><span data-stu-id="eb51a-219">200 - OK</span></span> |
| <span data-ttu-id="eb51a-220">3.0.0-3.x.y</span><span class="sxs-lookup"><span data-stu-id="eb51a-220">3.0.0-3.x.y</span></span> |<span data-ttu-id="eb51a-221">False/Non spécifié</span><span class="sxs-lookup"><span data-stu-id="eb51a-221">False/Not Specified</span></span> |<span data-ttu-id="eb51a-222">400 - Requête incorrecte</span><span class="sxs-lookup"><span data-stu-id="eb51a-222">400 - Bad Request</span></span> |

## <a name="next-steps"></a><span data-ttu-id="eb51a-223">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="eb51a-223">Next Steps</span></span>
* <span data-ttu-id="eb51a-224">[Migrer un service Mobile Services sur Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="eb51a-224">[Migrate a Mobile Service to Azure App Service]</span></span>

<span data-ttu-id="eb51a-225">[Clients Mobile Services]: #MobileServicesClients</span><span class="sxs-lookup"><span data-stu-id="eb51a-225">[Mobile Services clients]: #MobileServicesClients</span></span>
<span data-ttu-id="eb51a-226">[Clients Mobile Apps]: #MobileAppsClients</span><span class="sxs-lookup"><span data-stu-id="eb51a-226">[Mobile Apps clients]: #MobileAppsClients</span></span>


[Mobile App Server SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server
<span data-ttu-id="eb51a-227">[Migrer un service Mobile Services sur Azure App Service]: app-service-mobile-migrating-from-mobile-services.md</span><span class="sxs-lookup"><span data-stu-id="eb51a-227">[Migrate a Mobile Service to Azure App Service]: app-service-mobile-migrating-from-mobile-services.md</span></span>
