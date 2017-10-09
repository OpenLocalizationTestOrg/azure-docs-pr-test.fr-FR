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
# <a name="client-and-server-versioning-in-mobile-apps-and-mobile-services"></a>Contrôle de version client et serveur dans Mobile Apps et Mobile Services
version la plus récente d’Azure Mobile Services Hello est hello **Mobile Apps** fonctionnalité du Service d’applications Azure.

Hello client des applications mobiles et kits de développement logiciel serveur à l’origine basées sur ces dans les Services mobiles, mais ils sont *pas* compatibles entre elles.
Autrement dit, vous devez utiliser un SDK client *Mobile Apps* avec un SDK serveur *Mobile Apps* et il en est de même pour *Mobile Services*. Ce contrat est appliqué à une valeur d’en-tête spécial utilisée par hello client et le SDK, `ZUMO-API-VERSION`.

Remarque : chaque fois que ce document fait référence tooa *Services mobiles* principal, il n’est pas nécessaire toobe hébergé sur des Services mobiles. Il est désormais possible de toomigrate un toorun de service mobile sur le Service d’applications sans aucune modification du code, mais utilisent toujours les service hello *Services mobiles* versions du Kit de développement logiciel.

toolearn en savoir plus sur la migration tooApp Service sans aucune modification du code, consultez l’article hello [migrer un tooAzure Service Mobile App Service].

## <a name="header-specification"></a>Spécification de l’en-tête
clé de Hello `ZUMO-API-VERSION` peut être spécifié dans l’en-tête de hello HTTP ou de chaîne de requête hello. valeur de Hello est une chaîne de version sous forme de hello **x.y.z**.

Par exemple :

GET https://service.azurewebsites.net/tables/TodoItem

HEADERS: ZUMO-API-VERSION: 2.0.0

POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0

## <a name="opting-out-of-version-checking"></a>Désactivation de la vérification de version
Vous pouvez désactiver la vérification en définissant la valeur de version **true** pour le paramètre d’application hello **MS_SkipVersionCheck**. Définir ce paramètre dans votre fichier web.config ou Bonjour section Paramètres de l’Application Hello portail Azure.

> [!NOTE]
> Il existe un nombre de changements de comportement entre les Services mobiles et des applications mobiles, en particulier dans les zones hello de synchronisation hors connexion, l’authentification et des notifications push. Vous devez uniquement refuser version vérification après tooensure test complet que ces modifications de comportement n’interrompent pas les fonctionnalités de votre application.
>
>

## <a name="summary-of-compatibility-for-all-versions"></a>Résumé des compatibilités pour toutes les versions
graphique de Hello ci-dessous montre la compatibilité hello entre tous les types de client et le serveur. Un serveur principal est classé comme soit Mobile **Services** ou Mobile **applications** basé sur le serveur hello Kit de développement logiciel qu’il utilise.

|  | **Mobile Services** Node.js ou .NET | **Mobile Apps** Node.js ou .NET |
| --- | --- | --- |
| [Clients Mobile Services] |OK |Erreur\* |
| [Clients Mobile Apps] |Erreur\* |OK |

\*Peut être contrôlée en spécifiant **MS_SkipVersionCheck**.

<!-- IMPORTANT!  hello anchors for Mobile Services and Mobile Apps MUST be 1.0.0 and 2.0.0 respectively, since there is an exception error message that uses those anchors. -->

<!-- NOTE: hello fwlink toothis document is http://go.microsoft.com/fwlink/?LinkID=690568 -->

## <a name="1.0.0"></a>Client et serveur Mobile Services
le client Hello kits de développement logiciel dans le tableau hello ci-dessous sont compatibles avec **Mobile Services**.

Remarque : hello kits de développement logiciel de Mobile Services client *pas* envoyer une valeur d’en-tête pour `ZUMO-API-VERSION`. Si le service de hello reçoit cet en-tête ou une valeur de chaîne de requête, une erreur est renvoyée, sauf si vous avez choisi explicitement comme décrit ci-dessus.

### <a name="MobileServicesClients"></a> SDK clients Mobile *Services*
| Plateforme cliente | Version | Valeur d'en-tête de version |
| --- | --- | --- |
| Client géré (Windows, Xamarin) |[1.3.2](https://www.nuget.org/packages/WindowsAzure.MobileServices/1.3.2) |n/a |
| iOS |[2.2.2](http://aka.ms/gc6fex) |n/a |
| Android |[2.0.3](https://go.microsoft.com/fwLink/?LinkID=280126) |n/a |
| HTML |[1.2.7](http://ajax.aspnetcdn.com/ajax/mobileservices/MobileServices.Web-1.2.7.min.js) |n/a |

### <a name="mobile-services-server-sdks"></a>SDK serveurs Mobile *Services*
| Plateforme de serveur | Version | En-têtes de versions acceptés |
| --- | --- | --- |
| .NET |[WindowsAzure.MobileServices.Backend.* Version 1.0.x](https://www.nuget.org/packages/WindowsAzure.MobileServices.Backend/) |** Aucun en-tête de version ** |
| Node.js |(bientôt disponible) |**Aucun en-tête de version** |

<!-- TODO: add Node npm version -->

### <a name="behavior-of-mobile-services-backends"></a>Comportement des backends Mobile Services
| ZUMO-API-VERSION | Valeur de MS_SkipVersionCheck | Réponse |
| --- | --- | --- |
| Non spécifié |Quelconque |200 - OK |
| Valeur quelconque |True |200 - OK |
| Valeur quelconque |False/Non spécifié |400 - Requête incorrecte |

## <a name="2.0.0"></a>Client et serveur Azure Mobile Apps
### <a name="MobileAppsClients"></a> SDK clients Mobile *Apps*
Vérification de la version a été introduite dans hello suivant les versions du client de hello SDK pour **Azure Mobile Apps**:

| Plateforme cliente | Version | Valeur d'en-tête de version |
| --- | --- | --- |
| Client géré (Windows, Xamarin) |[2.0.0](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/2.0.0) |2.0.0 |
| iOS |[3.0.0](http://go.microsoft.com/fwlink/?LinkID=529823) |2.0.0 |
| Android |[3.0.0](http://go.microsoft.com/fwlink/?LinkID=717033&clcid=0x409) |3.0.0 |

<!-- TODO: add HTML version when released -->

### <a name="mobile-apps-server-sdks"></a>Kits de développement logiciel (SDK) du serveur Mobile *Apps*
La vérification de version est incluse dans les versions suivantes du SDK serveur :

| Plateforme de serveur | Foundation | En-têtes de versions acceptés |
| --- | --- | --- |
| .NET |[Microsoft.Azure.Mobile.Server](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) |2.0.0 |
| Node.js |[azure-mobile-apps)](https://www.npmjs.com/package/azure-mobile-apps) |2.0.0 |

### <a name="behavior-of-mobile-apps-backends"></a>Comportement des serveurs principaux Mobile Apps
| ZUMO-API-VERSION | Valeur de MS_SkipVersionCheck | Réponse |
| --- | --- | --- |
| x.y.z ou Null |True |200 - OK |
| Null |False/Non spécifié |400 - Requête incorrecte |
| 1.x.y |False/Non spécifié |400 - Requête incorrecte |
| 2.0.0-2.x.y |False/Non spécifié |200 - OK |
| 3.0.0-3.x.y |False/Non spécifié |400 - Requête incorrecte |

## <a name="next-steps"></a>Étapes suivantes
* [migrer un tooAzure Service Mobile App Service]

[Clients Mobile Services]: #MobileServicesClients
[Clients Mobile Apps]: #MobileAppsClients


[Mobile App Server SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server
[migrer un tooAzure Service Mobile App Service]: app-service-mobile-migrating-from-mobile-services.md
