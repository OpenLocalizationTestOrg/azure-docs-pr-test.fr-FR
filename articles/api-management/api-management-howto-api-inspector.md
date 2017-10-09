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
# <a name="how-toouse-hello-api-inspector-tootrace-calls-in-azure-api-management"></a>Méthode d’appel de toouse hello tootrace d’inspecteur de l’API de gestion des API Azure
Gestion des API fournit un inspecteur de l’API toohelp de l’outil de débogage et dépannage de votre API. Bonjour inspecteur de l’API peut être utilisé par programme et peut également être utilisé directement depuis le portail des développeurs hello. 

En outre les opérations tootracing, API inspecteur effectue également le suivi [expression de stratégie](https://msdn.microsoft.com/library/azure/dn910913.aspx) évaluations. Pour une démonstration, consultez [Cloud couvrent épisode 177 : fonctionnalités de gestion des API plus](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) et avançons too21:00.

Ce guide contient une procédure détaillée pour l'utilisation de l'inspecteur d'API.

> [!NOTE]
> Traces d’inspecteur de l’API sont uniquement générées et sont accessibles pour les demandes contenant des clés d’abonnement qui appartiennent toohello [administrateur](api-management-howto-create-groups.md) compte.
> 
> 

## <a name="trace-call"></a> Utilisation API inspecteur tootrace un appel
toouse inspecteur d’API, ajoutez un **ocp-apim-trace : true** demande d’appel de l’opération tooyour en-tête, puis téléchargez et inspecter trace hello à l’aide des URL de hello indiquée par hello **apim ocp-emplacement suivi** en-tête de réponse. Cela peut être effectué par programmation et peut également être effectué directement depuis le portail des développeurs hello.

Ce didacticiel montre comment les opérations de tootrace toouse hello API inspecteur à l’aide hello API calculatrice de base qui est configuré dans hello [gérer votre première API](api-management-get-started.md) didacticiel de mise en route. Si vous n’avez pas encore terminé ce didacticiel ne prend que quelques instants de tooimport hello API de calculatrice de base, ou vous pouvez utiliser une autre API de votre choix, par exemple hello Echo API. Chaque instance de service de gestion des API est préconfigurée avec une API d’écho qui peuvent être utilisé tooexperiment avec et en savoir plus sur la gestion des API. Hello Echo API renvoie toute entrée est envoyée tooit. toouse, vous pouvez appeler n’importe quel verbe HTTP et la valeur de retour hello simplement à ce que vous avez envoyé. 

tooget démarré, cliquez sur **portail des développeurs** Bonjour portail Azure pour votre service de gestion des API. Opérations peuvent être appelées directement depuis le portail des développeurs hello qui fournit un moyen pratique de tooview et tester le fonctionnement d’une API hello.

> Si vous n’avez pas encore créé une instance de service de gestion des API, consultez [de créer une instance de service de gestion des API] [ Create an API Management service instance] Bonjour [prise en main Azure API Management] [ Get started with Azure API Management] didacticiel.
> 
> 

![Portail des développeurs Gestion des API][api-management-developer-portal-menu]

Cliquez sur **API** dans le menu du haut hello, puis cliquez sur **calculatrice de base**.

![API Echo][api-management-api]

Cliquez sur **essayez-la** tootry hello **ajouter deux entiers** opération.

![Essayer][api-management-open-console]

Conserver les valeurs par défaut hello et clé d’abonnement sélectionnez hello pour produit hello toouse de hello **clé d’abonnement** liste déroulante.

Par défaut dans hello portail des développeurs de hello **Ocp-Apim-Trace** en-tête est déjà défini trop**true**. Il indique si un suivi est généré.

![Envoyer][api-management-http-get]

Cliquez sur **envoyer** opération hello de tooinvoke.

![Envoyer][api-management-send-results]

Dans la réponse de hello en-têtes sera un **apim ocp-emplacement suivi** avec un toohello comme valeur l’exemple suivant.

```
ocp-apim-trace-location : https://contosoltdxw7zagdfsprykd.blob.core.windows.net/apiinspectorcontainer/ZW3e23NsW4wQyS-SHjS0Og2-2?sv=2013-08-15&sr=b&sig=Mgx7cMHsLmVDv%2B%2BSzvg3JR8qGTHoOyIAV7xDsZbF7%2Bk%3D&se=2014-05-04T21%3A00%3A13Z&sp=r&verify_guid=a56a17d83de04fcb8b9766df38514742
```

trace de Hello peut être téléchargé à partir de l’emplacement spécifié type hello et consulté comme illustré dans l’étape suivante de hello. Notez que seuls hello dernière 100 entrées de journal sont stockées et emplacements de journaux sont réutilisés dans la rotation. Par conséquent, si vous effectuez des appels de plus de 100 avec le suivi activé vous finalement démarrera écraser les traces de première hello en place.

## <a name="inspect-trace"></a>Inspecter la trace de hello
valeurs hello tooreview trace de hello, téléchargez le fichier de trace de hello de hello **apim ocp-emplacement suivi** URL. Il est un fichier texte au format JSON et contient des entrées similaires toohello est l’exemple suivant.

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

## <a name="next-steps"></a>Étapes suivantes
* Pour une démonstration du suivi des expressions de stratégie, regardez la vidéo [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/). Démonstration de hello too21:00 toosee avance rapide.

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




