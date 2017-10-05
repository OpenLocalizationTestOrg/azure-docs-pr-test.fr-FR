---
title: "Suivre les appels avec l’inspecteur d’API - Gestion des API Azure | Microsoft Docs"
description: "Découvrez comment suivre les appels à l'aide de l'inspecteur d'API dans Gestion des API Azure."
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
ms.openlocfilehash: a9d4d3be7f046af975f6dc25670070204848588c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-api-inspector-to-trace-calls-in-azure-api-management"></a><span data-ttu-id="57d93-103">Utilisation de l'inspecteur d'API pour le suivi des appels dans Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="57d93-103">How to use the API Inspector to trace calls in Azure API Management</span></span>
<span data-ttu-id="57d93-104">Gestion des API Azure fournit un outil Inspecteur d’API pour vous aider au débogage et à la résolution des problèmes de vos API.</span><span class="sxs-lookup"><span data-stu-id="57d93-104">API Management provides an API Inspector tool to help you with debugging and troubleshooting your APIs.</span></span> <span data-ttu-id="57d93-105">L'inspecteur d'API peut être utilisé par programme et directement depuis le portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="57d93-105">The API Inspector can be used programmatically and can also be used directly from the developer portal.</span></span> 

<span data-ttu-id="57d93-106">En plus des opérations de suivi, l'inspecteur d’API assure également le suivi des évaluations d’ [expression de stratégie](https://msdn.microsoft.com/library/azure/dn910913.aspx) .</span><span class="sxs-lookup"><span data-stu-id="57d93-106">In addition to tracing operations, API Inspector also traces [policy expression](https://msdn.microsoft.com/library/azure/dn910913.aspx) evaluations.</span></span> <span data-ttu-id="57d93-107">Pour une démonstration, consultez l'épisode [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) , à partir de la 21e minute.</span><span class="sxs-lookup"><span data-stu-id="57d93-107">For a demonstration, see [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 21:00.</span></span>

<span data-ttu-id="57d93-108">Ce guide contient une procédure détaillée pour l'utilisation de l'inspecteur d'API.</span><span class="sxs-lookup"><span data-stu-id="57d93-108">This guide provides a walk-through of using API Inspector.</span></span>

> [!NOTE]
> <span data-ttu-id="57d93-109">Le suivi de l’inspecteur d’API n’est généré et mis à disposition que pour les demandes contenant des clés d’abonnement qui appartiennent au compte [administrateur](api-management-howto-create-groups.md) .</span><span class="sxs-lookup"><span data-stu-id="57d93-109">API Inspector traces are only generated and made available for requests containing subscription keys that belong to the [administrator](api-management-howto-create-groups.md) account.</span></span>
> 
> 

## <span data-ttu-id="57d93-110"><a name="trace-call"> </a> Utilisation de l’inspecteur d’API pour suivre un appel</span><span class="sxs-lookup"><span data-stu-id="57d93-110"><a name="trace-call"> </a> Use API Inspector to trace a call</span></span>
<span data-ttu-id="57d93-111">Pour utiliser l’inspecteur d’API, ajoutez un en-tête de demande **ocp-apim-trace: true** à l’appel de l’opération, puis téléchargez et inspectez le suivi avec l’URL indiquée par l’en-tête de réponse **ocp-apim-trace-location**.</span><span class="sxs-lookup"><span data-stu-id="57d93-111">To use API Inspector, add an **ocp-apim-trace: true** request header to your operation call, and then download and inspect the trace using the URL indicated by the **ocp-apim-trace-location** response header.</span></span> <span data-ttu-id="57d93-112">Cette opération peut se faire par programme ou directement depuis le portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="57d93-112">This can be done programatically, and can also be done directly from the developer portal.</span></span>

<span data-ttu-id="57d93-113">Ce didacticiel montre comment utiliser l’inspecteur d’API pour suivre les opérations à l’aide de l’API Basic Calculator qui est configurée dans le didacticiel de prise en main [Gestion de votre première API](api-management-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="57d93-113">This tutorial shows how to use the API Inspector to trace operations using the Basic Calculator API that is configured in the [Manage your first API](api-management-get-started.md) getting started tutorial.</span></span> <span data-ttu-id="57d93-114">Si vous n'avez pas effectué ce didacticiel, prenez quelques minutes pour importer l'API Basic Calculator. Vous pouvez également utiliser une autre API, par exemple l'API Echo.</span><span class="sxs-lookup"><span data-stu-id="57d93-114">If you haven't completed that tutorial it only takes a few moments to import the Basic Calculator API, or you can use another API of your choosing such as the Echo API.</span></span> <span data-ttu-id="57d93-115">Chaque instance du service Gestion des API est pré-configurée avec une API Echo qui peut être utilisée pour faire des expériences et en savoir plus sur la gestion des API.</span><span class="sxs-lookup"><span data-stu-id="57d93-115">Each API Management service instance comes pre-configured with an Echo API that can be used to experiment with and learn about API Management.</span></span> <span data-ttu-id="57d93-116">L'API Echo renvoie ce qui lui est fourni.</span><span class="sxs-lookup"><span data-stu-id="57d93-116">The Echo API returns back whatever input is sent to it.</span></span> <span data-ttu-id="57d93-117">Pour l'utiliser, vous pouvez appeler un verbe HTTP, et la valeur de retour sera simplement ce que vous avez envoyé.</span><span class="sxs-lookup"><span data-stu-id="57d93-117">To use it, you can invoke any HTTP verb, and the return value will simply be what you sent.</span></span> 

<span data-ttu-id="57d93-118">Pour commencer, cliquez sur **Portail des développeurs** dans le portail Azure de votre service Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="57d93-118">To get started, click **Developer portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="57d93-119">Les opérations peuvent être appelées directement depuis le portail des développeurs, ce qui permet d'afficher et de tester les opérations d'une API.</span><span class="sxs-lookup"><span data-stu-id="57d93-119">Operations can be called directly from the developer portal which provides a convenient way to view and test the operations of an API.</span></span>

> <span data-ttu-id="57d93-120">Si vous n’avez pas encore créé d’instance de service Gestion des API, consultez la page [Création d’une instance de service Gestion des API][Create an API Management service instance] dans le didacticiel [Prise en main de Gestion des API Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="57d93-120">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

![Portail des développeurs Gestion des API][api-management-developer-portal-menu]

<span data-ttu-id="57d93-122">Cliquez sur **API** dans le menu supérieur et sélectionnez **Basic Calculator**.</span><span class="sxs-lookup"><span data-stu-id="57d93-122">Click **APIs** from the top menu, and then click **Basic Calculator**.</span></span>

![API Echo][api-management-api]

<span data-ttu-id="57d93-124">Cliquez sur **Essayer** pour essayer l’opération **Ajouter deux entiers**.</span><span class="sxs-lookup"><span data-stu-id="57d93-124">Click **Try it** to try the **Add two integers** operation.</span></span>

![Essayer][api-management-open-console]

<span data-ttu-id="57d93-126">Conservez les valeurs de paramètres par défaut et sélectionnez la clé d'abonnement du produit à utiliser dans la liste déroulante **subscription-key** .</span><span class="sxs-lookup"><span data-stu-id="57d93-126">Keep the default parameter values, and select the subscription key for the product you want to use from the **subscription-key** drop-down.</span></span>

<span data-ttu-id="57d93-127">Par défaut, dans le portail des développeurs, l’en-tête **Ocp-Apim-Trace** est déjà défini sur **true**.</span><span class="sxs-lookup"><span data-stu-id="57d93-127">By default in the developer portal the **Ocp-Apim-Trace** header is already set to **true**.</span></span> <span data-ttu-id="57d93-128">Il indique si un suivi est généré.</span><span class="sxs-lookup"><span data-stu-id="57d93-128">This header configures whether or not a trace is generated.</span></span>

![Envoyer][api-management-http-get]

<span data-ttu-id="57d93-130">Cliquez sur **Envoyer** pour appeler l'opération.</span><span class="sxs-lookup"><span data-stu-id="57d93-130">Click **Send** to invoke the operation.</span></span>

![Envoyer][api-management-send-results]

<span data-ttu-id="57d93-132">Les en-têtes de réponse contiennent un élément **ocp-apim-trace-location** avec une valeur similaire à celle de l'exemple qui suit.</span><span class="sxs-lookup"><span data-stu-id="57d93-132">In the response headers will be an **ocp-apim-trace-location** with a value similar to the following example.</span></span>

```
ocp-apim-trace-location : https://contosoltdxw7zagdfsprykd.blob.core.windows.net/apiinspectorcontainer/ZW3e23NsW4wQyS-SHjS0Og2-2?sv=2013-08-15&sr=b&sig=Mgx7cMHsLmVDv%2B%2BSzvg3JR8qGTHoOyIAV7xDsZbF7%2Bk%3D&se=2014-05-04T21%3A00%3A13Z&sp=r&verify_guid=a56a17d83de04fcb8b9766df38514742
```

<span data-ttu-id="57d93-133">Le suivi peut être téléchargé depuis l'emplacement spécifié et examiné, comme indiqué dans l'étape suivante.</span><span class="sxs-lookup"><span data-stu-id="57d93-133">The trace can be downloaded from the specified location and reviewed as demonstrated in the next step.</span></span> <span data-ttu-id="57d93-134">Notez que seules les 100 dernières entrées de journal sont stockées et que les emplacements de journal sont réutilisés en rotation.</span><span class="sxs-lookup"><span data-stu-id="57d93-134">Note that only the last 100 log entries are stored and log locations are reused in rotation.</span></span> <span data-ttu-id="57d93-135">Par conséquent, si vous effectuez plus de 100 appels en gardant le suivi activé, vous finirez par remplacer les premières entrées.</span><span class="sxs-lookup"><span data-stu-id="57d93-135">So if you make more than 100 calls with tracing enabled you will eventually start overwriting the first traces in place.</span></span>

## <span data-ttu-id="57d93-136"><a name="inspect-trace"> </a>Inspection du suivi</span><span class="sxs-lookup"><span data-stu-id="57d93-136"><a name="inspect-trace"> </a>Inspect the trace</span></span>
<span data-ttu-id="57d93-137">Pour examiner les valeurs du suivi, téléchargez le fichier de suivi à partir de l’URL **ocp-apim-trace-location**.</span><span class="sxs-lookup"><span data-stu-id="57d93-137">To review the values in the trace, download the trace file from the **ocp-apim-trace-location** URL.</span></span> <span data-ttu-id="57d93-138">Il s'agit d'un fichier texte au format JSON. Il se présente comme l'exemple ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="57d93-138">It is a text file in JSON format, and contains entries similar to the following example.</span></span>

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
                    "message": "Request is being forwarded to the backend service.",
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
                    "message": "Response headers have been sent to the caller. Starting to stream the response body."
                }
            },
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.4256650Z",
                "elapsed": "00:00:00.1963155",
                "data": {
                    "message": "Response body streaming to the caller is complete."
                }
            }
        ]
    }
}
```

## <span data-ttu-id="57d93-139"><a name="next-steps"> </a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="57d93-139"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="57d93-140">Pour une démonstration du suivi des expressions de stratégie, regardez la vidéo [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/).</span><span class="sxs-lookup"><span data-stu-id="57d93-140">Watch a demo of tracing policy expressions in [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/).</span></span> <span data-ttu-id="57d93-141">Avancez à la 21e minute pour voir la démonstration.</span><span class="sxs-lookup"><span data-stu-id="57d93-141">Fast-forward to 21:00 to see the demo.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Cloud+Cover/Episode-177-More-API-Management-Features-with-Vlad-Vinogradsky/player]
> 
> 

[Use API Inspector to trace a call]: #trace-call
[Inspect the trace]: #inspect-trace
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




