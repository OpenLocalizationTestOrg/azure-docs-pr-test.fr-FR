---
title: "contrôle de version aaaClient et serveur SDK dans les applications mobiles et des Services mobiles | Documents Microsoft"
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
ms.openlocfilehash: 5874b7455ea407ca8c77fb1bd03d97d0767ebb47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="client-and-server-versioning-in-mobile-apps-and-mobile-services"></a><span data-ttu-id="d9a64-103">Contrôle de version client et serveur dans Mobile Apps et Mobile Services</span><span class="sxs-lookup"><span data-stu-id="d9a64-103">Client and server versioning in Mobile Apps and Mobile Services</span></span>
<span data-ttu-id="d9a64-104">version la plus récente d’Azure Mobile Services Hello est hello **Mobile Apps** fonctionnalité du Service d’applications Azure.</span><span class="sxs-lookup"><span data-stu-id="d9a64-104">hello latest version of Azure Mobile Services is hello **Mobile Apps** feature of Azure App Service.</span></span>

<span data-ttu-id="d9a64-105">Hello client des applications mobiles et kits de développement logiciel serveur à l’origine basées sur ces dans les Services mobiles, mais ils sont *pas* compatibles entre elles.</span><span class="sxs-lookup"><span data-stu-id="d9a64-105">hello Mobile Apps client and server SDKs are originally based on those in Mobile Services, but they are *not* compatible with each other.</span></span>
<span data-ttu-id="d9a64-106">Autrement dit, vous devez utiliser un SDK client *Mobile Apps* avec un SDK serveur *Mobile Apps* et il en est de même pour *Mobile Services*.</span><span class="sxs-lookup"><span data-stu-id="d9a64-106">That is, you must use a *Mobile Apps* client SDK with a *Mobile Apps* server SDK and similarly for *Mobile Services*.</span></span> <span data-ttu-id="d9a64-107">Ce contrat est appliqué à une valeur d’en-tête spécial utilisée par hello client et le SDK, `ZUMO-API-VERSION`.</span><span class="sxs-lookup"><span data-stu-id="d9a64-107">This contract is enforced through a special header value used by hello client and server SDKs, `ZUMO-API-VERSION`.</span></span>

<span data-ttu-id="d9a64-108">Remarque : chaque fois que ce document fait référence tooa *Services mobiles* principal, il n’est pas nécessaire toobe hébergé sur des Services mobiles.</span><span class="sxs-lookup"><span data-stu-id="d9a64-108">Note: whenever this document refers tooa *Mobile Services* backend, it does not necessarily need toobe hosted on Mobile Services.</span></span> <span data-ttu-id="d9a64-109">Il est désormais possible de toomigrate un toorun de service mobile sur le Service d’applications sans aucune modification du code, mais utilisent toujours les service hello *Services mobiles* versions du Kit de développement logiciel.</span><span class="sxs-lookup"><span data-stu-id="d9a64-109">It is now possible toomigrate a mobile service toorun on App Service without any code changes, but hello service would still be using *Mobile Services*  SDK versions.</span></span>

<span data-ttu-id="d9a64-110">toolearn en savoir plus sur la migration tooApp Service sans aucune modification du code, consultez l’article hello [migrer un tooAzure Service Mobile App Service].</span><span class="sxs-lookup"><span data-stu-id="d9a64-110">toolearn more about migrating tooApp Service without any code changes, see hello article [Migrate a Mobile Service tooAzure App Service].</span></span>

## <a name="header-specification"></a><span data-ttu-id="d9a64-111">Spécification de l’en-tête</span><span class="sxs-lookup"><span data-stu-id="d9a64-111">Header specification</span></span>
<span data-ttu-id="d9a64-112">clé de Hello `ZUMO-API-VERSION` peut être spécifié dans l’en-tête de hello HTTP ou de chaîne de requête hello.</span><span class="sxs-lookup"><span data-stu-id="d9a64-112">hello key `ZUMO-API-VERSION` may be specified in either hello HTTP header or hello query string.</span></span> <span data-ttu-id="d9a64-113">valeur de Hello est une chaîne de version sous forme de hello **x.y.z**.</span><span class="sxs-lookup"><span data-stu-id="d9a64-113">hello value is a version string in hello form **x.y.z**.</span></span>

<span data-ttu-id="d9a64-114">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="d9a64-114">For example:</span></span>

<span data-ttu-id="d9a64-115">GET https://service.azurewebsites.net/tables/TodoItem</span><span class="sxs-lookup"><span data-stu-id="d9a64-115">GET https://service.azurewebsites.net/tables/TodoItem</span></span>

<span data-ttu-id="d9a64-116">HEADERS: ZUMO-API-VERSION: 2.0.0</span><span class="sxs-lookup"><span data-stu-id="d9a64-116">HEADERS: ZUMO-API-VERSION: 2.0.0</span></span>

<span data-ttu-id="d9a64-117">POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0</span><span class="sxs-lookup"><span data-stu-id="d9a64-117">POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0</span></span>

## <a name="opting-out-of-version-checking"></a><span data-ttu-id="d9a64-118">Désactivation de la vérification de version</span><span class="sxs-lookup"><span data-stu-id="d9a64-118">Opting out of version checking</span></span>
<span data-ttu-id="d9a64-119">Vous pouvez désactiver la vérification en définissant la valeur de version **true** pour le paramètre d’application hello **MS_SkipVersionCheck**.</span><span class="sxs-lookup"><span data-stu-id="d9a64-119">You can opt out of version checking by setting a value of **true** for hello app setting **MS_SkipVersionCheck**.</span></span> <span data-ttu-id="d9a64-120">Définir ce paramètre dans votre fichier web.config ou Bonjour section Paramètres de l’Application Hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d9a64-120">Specify this either in your web.config or in hello Application Settings section of hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="d9a64-121">Il existe un nombre de changements de comportement entre les Services mobiles et des applications mobiles, en particulier dans les zones hello de synchronisation hors connexion, l’authentification et des notifications push.</span><span class="sxs-lookup"><span data-stu-id="d9a64-121">There are a number of behavior changes between Mobile Services and Mobile Apps, particularly in hello areas of offline sync, authentication, and push notifications.</span></span> <span data-ttu-id="d9a64-122">Vous devez uniquement refuser version vérification après tooensure test complet que ces modifications de comportement n’interrompent pas les fonctionnalités de votre application.</span><span class="sxs-lookup"><span data-stu-id="d9a64-122">You should only opt out of version checking after complete testing tooensure that these behavioral changes do not break your app's functionality.</span></span>
>
>

## <a name="summary-of-compatibility-for-all-versions"></a><span data-ttu-id="d9a64-123">Résumé des compatibilités pour toutes les versions</span><span class="sxs-lookup"><span data-stu-id="d9a64-123">Summary of compatibility for all versions</span></span>
<span data-ttu-id="d9a64-124">graphique de Hello ci-dessous montre la compatibilité hello entre tous les types de client et le serveur.</span><span class="sxs-lookup"><span data-stu-id="d9a64-124">hello chart below shows hello compatibility between all client and server types.</span></span> <span data-ttu-id="d9a64-125">Un serveur principal est classé comme soit Mobile **Services** ou Mobile **applications** basé sur le serveur hello Kit de développement logiciel qu’il utilise.</span><span class="sxs-lookup"><span data-stu-id="d9a64-125">A backend is classified as either Mobile **Services** or Mobile **Apps** based on hello server SDK that it uses.</span></span>

|  | <span data-ttu-id="d9a64-126">**Mobile Services** Node.js ou .NET</span><span class="sxs-lookup"><span data-stu-id="d9a64-126">**Mobile Services** Node.js or .NET</span></span> | <span data-ttu-id="d9a64-127">**Mobile Apps** Node.js ou .NET</span><span class="sxs-lookup"><span data-stu-id="d9a64-127">**Mobile Apps** Node.js or .NET</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d9a64-128">[Clients Mobile Services]</span><span class="sxs-lookup"><span data-stu-id="d9a64-128">[Mobile Services clients]</span></span> |<span data-ttu-id="d9a64-129">OK</span><span class="sxs-lookup"><span data-stu-id="d9a64-129">Ok</span></span> |<span data-ttu-id="d9a64-130">Erreur\*</span><span class="sxs-lookup"><span data-stu-id="d9a64-130">Error\*</span></span> |
| <span data-ttu-id="d9a64-131">[Clients Mobile Apps]</span><span class="sxs-lookup"><span data-stu-id="d9a64-131">[Mobile Apps clients]</span></span> |<span data-ttu-id="d9a64-132">Erreur\*</span><span class="sxs-lookup"><span data-stu-id="d9a64-132">Error\*</span></span> |<span data-ttu-id="d9a64-133">OK</span><span class="sxs-lookup"><span data-stu-id="d9a64-133">Ok</span></span> |

<span data-ttu-id="d9a64-134">\*Peut être contrôlée en spécifiant **MS_SkipVersionCheck**.</span><span class="sxs-lookup"><span data-stu-id="d9a64-134">\*This can be controlled by specifying **MS_SkipVersionCheck**.</span></span>

<!-- IMPORTANT!  hello anchors for Mobile Services and Mobile Apps MUST be 1.0.0 and 2.0.0 respectively, since there is an exception error message that uses those anchors. -->

<!-- NOTE: hello fwlink toothis document is http://go.microsoft.com/fwlink/?LinkID=690568 -->

## <span data-ttu-id="d9a64-135"><a name="1.0.0"></a>Client et serveur Mobile Services</span><span class="sxs-lookup"><span data-stu-id="d9a64-135"><a name="1.0.0"></a>Mobile Services client and server</span></span>
<span data-ttu-id="d9a64-136">le client Hello kits de développement logiciel dans le tableau hello ci-dessous sont compatibles avec **Mobile Services**.</span><span class="sxs-lookup"><span data-stu-id="d9a64-136">hello client SDKs in hello table below are compatible with **Mobile Services**.</span></span>

<span data-ttu-id="d9a64-137">Remarque : hello kits de développement logiciel de Mobile Services client *pas* envoyer une valeur d’en-tête pour `ZUMO-API-VERSION`.</span><span class="sxs-lookup"><span data-stu-id="d9a64-137">Note: hello Mobile Services client SDKs *do not* send a header value for `ZUMO-API-VERSION`.</span></span> <span data-ttu-id="d9a64-138">Si le service de hello reçoit cet en-tête ou une valeur de chaîne de requête, une erreur est renvoyée, sauf si vous avez choisi explicitement comme décrit ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="d9a64-138">If hello service receives this header or query string value, an error will be returned, unless you have explicitly opted out as described above.</span></span>

### <span data-ttu-id="d9a64-139"><a name="MobileServicesClients"></a> SDK clients Mobile *Services*</span><span class="sxs-lookup"><span data-stu-id="d9a64-139"><a name="MobileServicesClients"></a> Mobile *Services* client SDKs</span></span>
| <span data-ttu-id="d9a64-140">Plateforme cliente</span><span class="sxs-lookup"><span data-stu-id="d9a64-140">Client platform</span></span> | <span data-ttu-id="d9a64-141">Version</span><span class="sxs-lookup"><span data-stu-id="d9a64-141">Version</span></span> | <span data-ttu-id="d9a64-142">Valeur d'en-tête de version</span><span class="sxs-lookup"><span data-stu-id="d9a64-142">Version header value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d9a64-143">Client géré (Windows, Xamarin)</span><span class="sxs-lookup"><span data-stu-id="d9a64-143">Managed client (Windows, Xamarin)</span></span> |[<span data-ttu-id="d9a64-144">1.3.2</span><span class="sxs-lookup"><span data-stu-id="d9a64-144">1.3.2</span></span>](https://www.nuget.org/packages/WindowsAzure.MobileServices/1.3.2) |<span data-ttu-id="d9a64-145">n/a</span><span class="sxs-lookup"><span data-stu-id="d9a64-145">n/a</span></span> |
| <span data-ttu-id="d9a64-146">iOS</span><span class="sxs-lookup"><span data-stu-id="d9a64-146">iOS</span></span> |[<span data-ttu-id="d9a64-147">2.2.2</span><span class="sxs-lookup"><span data-stu-id="d9a64-147">2.2.2</span></span>](http://aka.ms/gc6fex) |<span data-ttu-id="d9a64-148">n/a</span><span class="sxs-lookup"><span data-stu-id="d9a64-148">n/a</span></span> |
| <span data-ttu-id="d9a64-149">Android</span><span class="sxs-lookup"><span data-stu-id="d9a64-149">Android</span></span> |[<span data-ttu-id="d9a64-150">2.0.3</span><span class="sxs-lookup"><span data-stu-id="d9a64-150">2.0.3</span></span>](https://go.microsoft.com/fwLink/?LinkID=280126) |<span data-ttu-id="d9a64-151">n/a</span><span class="sxs-lookup"><span data-stu-id="d9a64-151">n/a</span></span> |
| <span data-ttu-id="d9a64-152">HTML</span><span class="sxs-lookup"><span data-stu-id="d9a64-152">HTML</span></span> |[<span data-ttu-id="d9a64-153">1.2.7</span><span class="sxs-lookup"><span data-stu-id="d9a64-153">1.2.7</span></span>](http://ajax.aspnetcdn.com/ajax/mobileservices/MobileServices.Web-1.2.7.min.js) |<span data-ttu-id="d9a64-154">n/a</span><span class="sxs-lookup"><span data-stu-id="d9a64-154">n/a</span></span> |

### <a name="mobile-services-server-sdks"></a><span data-ttu-id="d9a64-155">SDK serveurs Mobile *Services*</span><span class="sxs-lookup"><span data-stu-id="d9a64-155">Mobile *Services* server SDKs</span></span>
| <span data-ttu-id="d9a64-156">Plateforme de serveur</span><span class="sxs-lookup"><span data-stu-id="d9a64-156">Server platform</span></span> | <span data-ttu-id="d9a64-157">Version</span><span class="sxs-lookup"><span data-stu-id="d9a64-157">Version</span></span> | <span data-ttu-id="d9a64-158">En-têtes de versions acceptés</span><span class="sxs-lookup"><span data-stu-id="d9a64-158">Accepted version header</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d9a64-159">.NET</span><span class="sxs-lookup"><span data-stu-id="d9a64-159">.NET</span></span> |[<span data-ttu-id="d9a64-160">WindowsAzure.MobileServices.Backend.* Version 1.0.x</span><span class="sxs-lookup"><span data-stu-id="d9a64-160">WindowsAzure.MobileServices.Backend.* Version 1.0.x</span></span>](https://www.nuget.org/packages/WindowsAzure.MobileServices.Backend/) |<span data-ttu-id="d9a64-161">** Aucun en-tête de version **</span><span class="sxs-lookup"><span data-stu-id="d9a64-161">**No version header **</span></span> |
| <span data-ttu-id="d9a64-162">Node.js</span><span class="sxs-lookup"><span data-stu-id="d9a64-162">Node.js</span></span> |<span data-ttu-id="d9a64-163">(bientôt disponible)</span><span class="sxs-lookup"><span data-stu-id="d9a64-163">(coming soon)</span></span> |<span data-ttu-id="d9a64-164">**Aucun en-tête de version**</span><span class="sxs-lookup"><span data-stu-id="d9a64-164">**No version header**</span></span> |

<!-- TODO: add Node npm version -->

### <a name="behavior-of-mobile-services-backends"></a><span data-ttu-id="d9a64-165">Comportement des backends Mobile Services</span><span class="sxs-lookup"><span data-stu-id="d9a64-165">Behavior of Mobile Services backends</span></span>
| <span data-ttu-id="d9a64-166">ZUMO-API-VERSION</span><span class="sxs-lookup"><span data-stu-id="d9a64-166">ZUMO-API-VERSION</span></span> | <span data-ttu-id="d9a64-167">Valeur de MS_SkipVersionCheck</span><span class="sxs-lookup"><span data-stu-id="d9a64-167">Value of MS_SkipVersionCheck</span></span> | <span data-ttu-id="d9a64-168">Réponse</span><span class="sxs-lookup"><span data-stu-id="d9a64-168">Response</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d9a64-169">Non spécifié</span><span class="sxs-lookup"><span data-stu-id="d9a64-169">Not specified</span></span> |<span data-ttu-id="d9a64-170">Quelconque</span><span class="sxs-lookup"><span data-stu-id="d9a64-170">Any</span></span> |<span data-ttu-id="d9a64-171">200 - OK</span><span class="sxs-lookup"><span data-stu-id="d9a64-171">200 - OK</span></span> |
| <span data-ttu-id="d9a64-172">Valeur quelconque</span><span class="sxs-lookup"><span data-stu-id="d9a64-172">Any value</span></span> |<span data-ttu-id="d9a64-173">True</span><span class="sxs-lookup"><span data-stu-id="d9a64-173">True</span></span> |<span data-ttu-id="d9a64-174">200 - OK</span><span class="sxs-lookup"><span data-stu-id="d9a64-174">200 - OK</span></span> |
| <span data-ttu-id="d9a64-175">Valeur quelconque</span><span class="sxs-lookup"><span data-stu-id="d9a64-175">Any value</span></span> |<span data-ttu-id="d9a64-176">False/Non spécifié</span><span class="sxs-lookup"><span data-stu-id="d9a64-176">False/Not Specified</span></span> |<span data-ttu-id="d9a64-177">400 - Requête incorrecte</span><span class="sxs-lookup"><span data-stu-id="d9a64-177">400 - Bad Request</span></span> |

## <span data-ttu-id="d9a64-178"><a name="2.0.0"></a>Client et serveur Azure Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="d9a64-178"><a name="2.0.0"></a>Azure Mobile Apps client and server</span></span>
### <span data-ttu-id="d9a64-179"><a name="MobileAppsClients"></a> SDK clients Mobile *Apps*</span><span class="sxs-lookup"><span data-stu-id="d9a64-179"><a name="MobileAppsClients"></a> Mobile *Apps* client SDKs</span></span>
<span data-ttu-id="d9a64-180">Vérification de la version a été introduite dans hello suivant les versions du client de hello SDK pour **Azure Mobile Apps**:</span><span class="sxs-lookup"><span data-stu-id="d9a64-180">Version checking was introduced starting with hello following versions of hello client SDK for **Azure Mobile Apps**:</span></span>

| <span data-ttu-id="d9a64-181">Plateforme cliente</span><span class="sxs-lookup"><span data-stu-id="d9a64-181">Client platform</span></span> | <span data-ttu-id="d9a64-182">Version</span><span class="sxs-lookup"><span data-stu-id="d9a64-182">Version</span></span> | <span data-ttu-id="d9a64-183">Valeur d'en-tête de version</span><span class="sxs-lookup"><span data-stu-id="d9a64-183">Version header value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d9a64-184">Client géré (Windows, Xamarin)</span><span class="sxs-lookup"><span data-stu-id="d9a64-184">Managed client (Windows, Xamarin)</span></span> |[<span data-ttu-id="d9a64-185">2.0.0</span><span class="sxs-lookup"><span data-stu-id="d9a64-185">2.0.0</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/2.0.0) |<span data-ttu-id="d9a64-186">2.0.0</span><span class="sxs-lookup"><span data-stu-id="d9a64-186">2.0.0</span></span> |
| <span data-ttu-id="d9a64-187">iOS</span><span class="sxs-lookup"><span data-stu-id="d9a64-187">iOS</span></span> |[<span data-ttu-id="d9a64-188">3.0.0</span><span class="sxs-lookup"><span data-stu-id="d9a64-188">3.0.0</span></span>](http://go.microsoft.com/fwlink/?LinkID=529823) |<span data-ttu-id="d9a64-189">2.0.0</span><span class="sxs-lookup"><span data-stu-id="d9a64-189">2.0.0</span></span> |
| <span data-ttu-id="d9a64-190">Android</span><span class="sxs-lookup"><span data-stu-id="d9a64-190">Android</span></span> |[<span data-ttu-id="d9a64-191">3.0.0</span><span class="sxs-lookup"><span data-stu-id="d9a64-191">3.0.0</span></span>](http://go.microsoft.com/fwlink/?LinkID=717033&clcid=0x409) |<span data-ttu-id="d9a64-192">3.0.0</span><span class="sxs-lookup"><span data-stu-id="d9a64-192">3.0.0</span></span> |

<!-- TODO: add HTML version when released -->

### <a name="mobile-apps-server-sdks"></a><span data-ttu-id="d9a64-193">Kits de développement logiciel (SDK) du serveur Mobile *Apps*</span><span class="sxs-lookup"><span data-stu-id="d9a64-193">Mobile *Apps* server SDKs</span></span>
<span data-ttu-id="d9a64-194">La vérification de version est incluse dans les versions suivantes du SDK serveur :</span><span class="sxs-lookup"><span data-stu-id="d9a64-194">Version checking is included in following server SDK versions:</span></span>

| <span data-ttu-id="d9a64-195">Plateforme de serveur</span><span class="sxs-lookup"><span data-stu-id="d9a64-195">Server platform</span></span> | <span data-ttu-id="d9a64-196">Foundation</span><span class="sxs-lookup"><span data-stu-id="d9a64-196">SDK</span></span> | <span data-ttu-id="d9a64-197">En-têtes de versions acceptés</span><span class="sxs-lookup"><span data-stu-id="d9a64-197">Accepted version header</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d9a64-198">.NET</span><span class="sxs-lookup"><span data-stu-id="d9a64-198">.NET</span></span> |[<span data-ttu-id="d9a64-199">Microsoft.Azure.Mobile.Server</span><span class="sxs-lookup"><span data-stu-id="d9a64-199">Microsoft.Azure.Mobile.Server</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) |<span data-ttu-id="d9a64-200">2.0.0</span><span class="sxs-lookup"><span data-stu-id="d9a64-200">2.0.0</span></span> |
| <span data-ttu-id="d9a64-201">Node.js</span><span class="sxs-lookup"><span data-stu-id="d9a64-201">Node.js</span></span> |[<span data-ttu-id="d9a64-202">azure-mobile-apps)</span><span class="sxs-lookup"><span data-stu-id="d9a64-202">azure-mobile-apps)</span></span>](https://www.npmjs.com/package/azure-mobile-apps) |<span data-ttu-id="d9a64-203">2.0.0</span><span class="sxs-lookup"><span data-stu-id="d9a64-203">2.0.0</span></span> |

### <a name="behavior-of-mobile-apps-backends"></a><span data-ttu-id="d9a64-204">Comportement des serveurs principaux Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="d9a64-204">Behavior of Mobile Apps backends</span></span>
| <span data-ttu-id="d9a64-205">ZUMO-API-VERSION</span><span class="sxs-lookup"><span data-stu-id="d9a64-205">ZUMO-API-VERSION</span></span> | <span data-ttu-id="d9a64-206">Valeur de MS_SkipVersionCheck</span><span class="sxs-lookup"><span data-stu-id="d9a64-206">Value of MS_SkipVersionCheck</span></span> | <span data-ttu-id="d9a64-207">Réponse</span><span class="sxs-lookup"><span data-stu-id="d9a64-207">Response</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d9a64-208">x.y.z ou Null</span><span class="sxs-lookup"><span data-stu-id="d9a64-208">x.y.z or Null</span></span> |<span data-ttu-id="d9a64-209">True</span><span class="sxs-lookup"><span data-stu-id="d9a64-209">True</span></span> |<span data-ttu-id="d9a64-210">200 - OK</span><span class="sxs-lookup"><span data-stu-id="d9a64-210">200 - OK</span></span> |
| <span data-ttu-id="d9a64-211">Null</span><span class="sxs-lookup"><span data-stu-id="d9a64-211">Null</span></span> |<span data-ttu-id="d9a64-212">False/Non spécifié</span><span class="sxs-lookup"><span data-stu-id="d9a64-212">False/Not Specified</span></span> |<span data-ttu-id="d9a64-213">400 - Requête incorrecte</span><span class="sxs-lookup"><span data-stu-id="d9a64-213">400 - Bad Request</span></span> |
| <span data-ttu-id="d9a64-214">1.x.y</span><span class="sxs-lookup"><span data-stu-id="d9a64-214">1.x.y</span></span> |<span data-ttu-id="d9a64-215">False/Non spécifié</span><span class="sxs-lookup"><span data-stu-id="d9a64-215">False/Not Specified</span></span> |<span data-ttu-id="d9a64-216">400 - Requête incorrecte</span><span class="sxs-lookup"><span data-stu-id="d9a64-216">400 - Bad Request</span></span> |
| <span data-ttu-id="d9a64-217">2.0.0-2.x.y</span><span class="sxs-lookup"><span data-stu-id="d9a64-217">2.0.0-2.x.y</span></span> |<span data-ttu-id="d9a64-218">False/Non spécifié</span><span class="sxs-lookup"><span data-stu-id="d9a64-218">False/Not Specified</span></span> |<span data-ttu-id="d9a64-219">200 - OK</span><span class="sxs-lookup"><span data-stu-id="d9a64-219">200 - OK</span></span> |
| <span data-ttu-id="d9a64-220">3.0.0-3.x.y</span><span class="sxs-lookup"><span data-stu-id="d9a64-220">3.0.0-3.x.y</span></span> |<span data-ttu-id="d9a64-221">False/Non spécifié</span><span class="sxs-lookup"><span data-stu-id="d9a64-221">False/Not Specified</span></span> |<span data-ttu-id="d9a64-222">400 - Requête incorrecte</span><span class="sxs-lookup"><span data-stu-id="d9a64-222">400 - Bad Request</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d9a64-223">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d9a64-223">Next Steps</span></span>
* <span data-ttu-id="d9a64-224">[migrer un tooAzure Service Mobile App Service]</span><span class="sxs-lookup"><span data-stu-id="d9a64-224">[Migrate a Mobile Service tooAzure App Service]</span></span>

[Clients Mobile Services]: #MobileServicesClients
[Clients Mobile Apps]: #MobileAppsClients


[Mobile App Server SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server
[migrer un tooAzure Service Mobile App Service]: app-service-mobile-migrating-from-mobile-services.md
