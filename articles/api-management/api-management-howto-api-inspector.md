---
title: "appels aaaTrace avec l’inspecteur de l’API - gestion des API Azure | Documents Microsoft"
description: "Découvrez comment tootrace les appels à l’aide de hello inspecteur de l’API de gestion des API Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 4b222327-c8a4-4f33-9a06-adff2a9834d9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: b0c401caa8da1b789f6cfe5edf97a5f118d78f26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-api-inspector-tootrace-calls-in-azure-api-management"></a><span data-ttu-id="e29b7-103">Méthode d’appel de toouse hello tootrace d’inspecteur de l’API de gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="e29b7-103">How toouse hello API Inspector tootrace calls in Azure API Management</span></span>
<span data-ttu-id="e29b7-104">Gestion des API fournit un inspecteur de l’API toohelp de l’outil de débogage et dépannage de votre API.</span><span class="sxs-lookup"><span data-stu-id="e29b7-104">API Management provides an API Inspector tool toohelp you with debugging and troubleshooting your APIs.</span></span> <span data-ttu-id="e29b7-105">Bonjour inspecteur de l’API peut être utilisé par programme et peut également être utilisé directement depuis le portail des développeurs hello.</span><span class="sxs-lookup"><span data-stu-id="e29b7-105">hello API Inspector can be used programmatically and can also be used directly from hello developer portal.</span></span> 

<span data-ttu-id="e29b7-106">En outre les opérations tootracing, API inspecteur effectue également le suivi [expression de stratégie](https://msdn.microsoft.com/library/azure/dn910913.aspx) évaluations.</span><span class="sxs-lookup"><span data-stu-id="e29b7-106">In addition tootracing operations, API Inspector also traces [policy expression](https://msdn.microsoft.com/library/azure/dn910913.aspx) evaluations.</span></span> <span data-ttu-id="e29b7-107">Pour une démonstration, consultez [Cloud couvrent épisode 177 : fonctionnalités de gestion des API plus](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) et avançons too21:00.</span><span class="sxs-lookup"><span data-stu-id="e29b7-107">For a demonstration, see [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too21:00.</span></span>

<span data-ttu-id="e29b7-108">Ce guide contient une procédure détaillée pour l'utilisation de l'inspecteur d'API.</span><span class="sxs-lookup"><span data-stu-id="e29b7-108">This guide provides a walk-through of using API Inspector.</span></span>

> [!NOTE]
> <span data-ttu-id="e29b7-109">Traces d’inspecteur de l’API sont uniquement générées et sont accessibles pour les demandes contenant des clés d’abonnement qui appartiennent toohello [administrateur](api-management-howto-create-groups.md) compte.</span><span class="sxs-lookup"><span data-stu-id="e29b7-109">API Inspector traces are only generated and made available for requests containing subscription keys that belong toohello [administrator](api-management-howto-create-groups.md) account.</span></span>
> 
> 

## <span data-ttu-id="e29b7-110"><a name="trace-call"></a> Utilisation API inspecteur tootrace un appel</span><span class="sxs-lookup"><span data-stu-id="e29b7-110"><a name="trace-call"> </a> Use API Inspector tootrace a call</span></span>
<span data-ttu-id="e29b7-111">toouse inspecteur d’API, ajoutez un **ocp-apim-trace : true** demande d’appel de l’opération tooyour en-tête, puis téléchargez et inspecter trace hello à l’aide des URL de hello indiquée par hello **apim ocp-emplacement suivi** en-tête de réponse.</span><span class="sxs-lookup"><span data-stu-id="e29b7-111">toouse API Inspector, add an **ocp-apim-trace: true** request header tooyour operation call, and then download and inspect hello trace using hello URL indicated by hello **ocp-apim-trace-location** response header.</span></span> <span data-ttu-id="e29b7-112">Cela peut être effectué par programmation et peut également être effectué directement depuis le portail des développeurs hello.</span><span class="sxs-lookup"><span data-stu-id="e29b7-112">This can be done programatically, and can also be done directly from hello developer portal.</span></span>

<span data-ttu-id="e29b7-113">Ce didacticiel montre comment les opérations de tootrace toouse hello API inspecteur à l’aide hello API calculatrice de base qui est configuré dans hello [gérer votre première API](api-management-get-started.md) didacticiel de mise en route.</span><span class="sxs-lookup"><span data-stu-id="e29b7-113">This tutorial shows how toouse hello API Inspector tootrace operations using hello Basic Calculator API that is configured in hello [Manage your first API](api-management-get-started.md) getting started tutorial.</span></span> <span data-ttu-id="e29b7-114">Si vous n’avez pas encore terminé ce didacticiel ne prend que quelques instants de tooimport hello API de calculatrice de base, ou vous pouvez utiliser une autre API de votre choix, par exemple hello Echo API.</span><span class="sxs-lookup"><span data-stu-id="e29b7-114">If you haven't completed that tutorial it only takes a few moments tooimport hello Basic Calculator API, or you can use another API of your choosing such as hello Echo API.</span></span> <span data-ttu-id="e29b7-115">Chaque instance de service de gestion des API est préconfigurée avec une API d’écho qui peuvent être utilisé tooexperiment avec et en savoir plus sur la gestion des API.</span><span class="sxs-lookup"><span data-stu-id="e29b7-115">Each API Management service instance comes pre-configured with an Echo API that can be used tooexperiment with and learn about API Management.</span></span> <span data-ttu-id="e29b7-116">Hello Echo API renvoie toute entrée est envoyée tooit.</span><span class="sxs-lookup"><span data-stu-id="e29b7-116">hello Echo API returns back whatever input is sent tooit.</span></span> <span data-ttu-id="e29b7-117">toouse, vous pouvez appeler n’importe quel verbe HTTP et la valeur de retour hello simplement à ce que vous avez envoyé.</span><span class="sxs-lookup"><span data-stu-id="e29b7-117">toouse it, you can invoke any HTTP verb, and hello return value will simply be what you sent.</span></span> 

<span data-ttu-id="e29b7-118">tooget démarré, cliquez sur **portail des développeurs** Bonjour portail Azure pour votre service de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="e29b7-118">tooget started, click **Developer portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="e29b7-119">Opérations peuvent être appelées directement depuis le portail des développeurs hello qui fournit un moyen pratique de tooview et tester le fonctionnement d’une API hello.</span><span class="sxs-lookup"><span data-stu-id="e29b7-119">Operations can be called directly from hello developer portal which provides a convenient way tooview and test hello operations of an API.</span></span>

> <span data-ttu-id="e29b7-120">Si vous n’avez pas encore créé une instance de service de gestion des API, consultez [de créer une instance de service de gestion des API] [ Create an API Management service instance] Bonjour [prise en main Azure API Management] [ Get started with Azure API Management] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="e29b7-120">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

![Portail des développeurs Gestion des API][api-management-developer-portal-menu]

<span data-ttu-id="e29b7-122">Cliquez sur **API** dans le menu du haut hello, puis cliquez sur **calculatrice de base**.</span><span class="sxs-lookup"><span data-stu-id="e29b7-122">Click **APIs** from hello top menu, and then click **Basic Calculator**.</span></span>

![API Echo][api-management-api]

<span data-ttu-id="e29b7-124">Cliquez sur **essayez-la** tootry hello **ajouter deux entiers** opération.</span><span class="sxs-lookup"><span data-stu-id="e29b7-124">Click **Try it** tootry hello **Add two integers** operation.</span></span>

![Essayer][api-management-open-console]

<span data-ttu-id="e29b7-126">Conserver les valeurs par défaut hello et clé d’abonnement sélectionnez hello pour produit hello toouse de hello **clé d’abonnement** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="e29b7-126">Keep hello default parameter values, and select hello subscription key for hello product you want toouse from hello **subscription-key** drop-down.</span></span>

<span data-ttu-id="e29b7-127">Par défaut dans hello portail des développeurs de hello **Ocp-Apim-Trace** en-tête est déjà défini trop**true**.</span><span class="sxs-lookup"><span data-stu-id="e29b7-127">By default in hello developer portal hello **Ocp-Apim-Trace** header is already set too**true**.</span></span> <span data-ttu-id="e29b7-128">Il indique si un suivi est généré.</span><span class="sxs-lookup"><span data-stu-id="e29b7-128">This header configures whether or not a trace is generated.</span></span>

![Envoyer][api-management-http-get]

<span data-ttu-id="e29b7-130">Cliquez sur **envoyer** opération hello de tooinvoke.</span><span class="sxs-lookup"><span data-stu-id="e29b7-130">Click **Send** tooinvoke hello operation.</span></span>

![Envoyer][api-management-send-results]

<span data-ttu-id="e29b7-132">Dans la réponse de hello en-têtes sera un **apim ocp-emplacement suivi** avec un toohello comme valeur l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="e29b7-132">In hello response headers will be an **ocp-apim-trace-location** with a value similar toohello following example.</span></span>

```
ocp-apim-trace-location : https://contosoltdxw7zagdfsprykd.blob.core.windows.net/apiinspectorcontainer/ZW3e23NsW4wQyS-SHjS0Og2-2?sv=2013-08-15&sr=b&sig=Mgx7cMHsLmVDv%2B%2BSzvg3JR8qGTHoOyIAV7xDsZbF7%2Bk%3D&se=2014-05-04T21%3A00%3A13Z&sp=r&verify_guid=a56a17d83de04fcb8b9766df38514742
```

<span data-ttu-id="e29b7-133">trace de Hello peut être téléchargé à partir de l’emplacement spécifié type hello et consulté comme illustré dans l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="e29b7-133">hello trace can be downloaded from hello specified location and reviewed as demonstrated in hello next step.</span></span> <span data-ttu-id="e29b7-134">Notez que seuls hello dernière 100 entrées de journal sont stockées et emplacements de journaux sont réutilisés dans la rotation.</span><span class="sxs-lookup"><span data-stu-id="e29b7-134">Note that only hello last 100 log entries are stored and log locations are reused in rotation.</span></span> <span data-ttu-id="e29b7-135">Par conséquent, si vous effectuez des appels de plus de 100 avec le suivi activé vous finalement démarrera écraser les traces de première hello en place.</span><span class="sxs-lookup"><span data-stu-id="e29b7-135">So if you make more than 100 calls with tracing enabled you will eventually start overwriting hello first traces in place.</span></span>

## <span data-ttu-id="e29b7-136"><a name="inspect-trace"></a>Inspecter la trace de hello</span><span class="sxs-lookup"><span data-stu-id="e29b7-136"><a name="inspect-trace"> </a>Inspect hello trace</span></span>
<span data-ttu-id="e29b7-137">valeurs hello tooreview trace de hello, téléchargez le fichier de trace de hello de hello **apim ocp-emplacement suivi** URL.</span><span class="sxs-lookup"><span data-stu-id="e29b7-137">tooreview hello values in hello trace, download hello trace file from hello **ocp-apim-trace-location** URL.</span></span> <span data-ttu-id="e29b7-138">Il est un fichier texte au format JSON et contient des entrées similaires toohello est l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="e29b7-138">It is a text file in JSON format, and contains entries similar toohello following example.</span></span>

```json
{
    "traceId": "abcd8ea63d134c1fabe6371566c7cbea",
    "traceEntries": {
        "inbound": [
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.2998610Z",
                "elapsed": "00:00:00.0725926",
                "data": {
                    "request": {
                        "method": "GET",
                        "url": "https://contoso5.azure-api.net/calc/add?a=51&b=49",
                        "headers": [
                            {
                                "name": "Ocp-Apim-Subscription-Key",
                                "value": "5d7c41af64a44a68a2ea46580d271a59"
                            },
                            {
                                "name": "Connection",
                                "value": "Keep-Alive"
                            },
                            {
                                "name": "Host",
                                "value": "contoso5.azure-api.net"
                            }
                        ]
                    }
                }
            },
            {
                "source": "mapper",
                "timestamp": "2015-06-23T19:51:35.2998610Z",
                "elapsed": "00:00:00.0726213",
                "data": {
                    "configuration": {
                        "api": {
                            "from": "/calc",
                            "to": {
                                "scheme": "http",
                                "host": "calcapi.cloudapp.net",
                                "port": 80,
                                "path": "/api",
                                "queryString": "",
                                "query": {},
                                "isDefaultPort": true
                            }
                        },
                        "operation": {
                            "method": "GET",
                            "uriTemplate": "/add?a={a}&b={b}"
                        },
                        "user": {
                            "id": 1,
                            "groups": [
                                "Administrators",
                                "Developers"
                            ]
                        },
                        "product": {
                            "id": 1
                        }
                    }
                }
            },
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.2998610Z",
                "elapsed": "00:00:00.0727522",
                "data": {
                    "message": "Request is being forwarded toohello backend service.",
                    "request": {
                        "method": "GET",
                        "url": "http://calcapi.cloudapp.net/api/add?a=51&b=49",
                        "headers": [
                            {
                                "name": "Ocp-Apim-Subscription-Key",
                                "value": "5d7c41af64a44a68a2ea46580d271a59"
                            },
                            {
                                "name": "X-Forwarded-For",
                                "value": "33.52.215.35"
                            }
                        ]
                    }
                }
            }
        ],
        "outbound": [
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.4256650Z",
                "elapsed": "00:00:00.1960601",
                "data": {
                    "response": {
                        "status": {
                            "code": 200,
                            "reason": "OK"
                        },
                        "headers": [
                            {
                                "name": "Pragma",
                                "value": "no-cache"
                            },
                            {
                                "name": "Content-Length",
                                "value": "124"
                            },
                            {
                                "name": "Cache-Control",
                                "value": "no-cache"
                            },
                            {
                                "name": "Content-Type",
                                "value": "application/xml; charset=utf-8"
                            },
                            {
                                "name": "Date",
                                "value": "Tue, 23 Jun 2015 19:51:35 GMT"
                            },
                            {
                                "name": "Expires",
                                "value": "-1"
                            },
                            {
                                "name": "Server",
                                "value": "Microsoft-IIS/8.5"
                            },
                            {
                                "name": "X-AspNet-Version",
                                "value": "4.0.30319"
                            },
                            {
                                "name": "X-Powered-By",
                                "value": "ASP.NET"
                            }
                        ]
                    }
                }
            },
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.4256650Z",
                "elapsed": "00:00:00.1961112",
                "data": {
                    "message": "Response headers have been sent toohello caller. Starting toostream hello response body."
                }
            },
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.4256650Z",
                "elapsed": "00:00:00.1963155",
                "data": {
                    "message": "Response body streaming toohello caller is complete."
                }
            }
        ]
    }
}
```

## <span data-ttu-id="e29b7-139"><a name="next-steps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e29b7-139"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="e29b7-140">Pour une démonstration du suivi des expressions de stratégie, regardez la vidéo [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/).</span><span class="sxs-lookup"><span data-stu-id="e29b7-140">Watch a demo of tracing policy expressions in [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/).</span></span> <span data-ttu-id="e29b7-141">Démonstration de hello too21:00 toosee avance rapide.</span><span class="sxs-lookup"><span data-stu-id="e29b7-141">Fast-forward too21:00 toosee hello demo.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Cloud+Cover/Episode-177-More-API-Management-Features-with-Vlad-Vinogradsky/player]
> 
> 

[Use API Inspector tootrace a call]: #trace-call
[Inspect hello trace]: #inspect-trace
[Next steps]: #next-steps

[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[Responses]: api-management-howto-add-operations.md#responses
[How create and publish a product]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Azure Classic Portal]: https://manage.windowsazure.com/


[api-management-developer-portal-menu]: ./media/api-management-howto-api-inspector/api-management-developer-portal-menu.png
[api-management-api]: ./media/api-management-howto-api-inspector/api-management-api.png
[api-management-echo-api-get]: ./media/api-management-howto-api-inspector/api-management-echo-api-get.png
[api-management-developer-key]: ./media/api-management-howto-api-inspector/api-management-developer-key.png
[api-management-open-console]: ./media/api-management-howto-api-inspector/api-management-open-console.png
[api-management-http-get]: ./media/api-management-howto-api-inspector/api-management-http-get.png
[api-management-send-results]: ./media/api-management-howto-api-inspector/api-management-send-results.png




