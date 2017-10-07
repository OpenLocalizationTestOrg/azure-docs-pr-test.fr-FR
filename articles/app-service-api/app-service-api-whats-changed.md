---
title: "aaaApp Service API Apps - Nouveautés | Documents Microsoft"
description: "Découvrez les nouveautés d’API Apps dans Azure App Service"
services: app-service\api
documentationcenter: .net
author: mohitsriv
manager: erikre
editor: tdykstra
ms.assetid: a9b58066-e8fd-48b8-a651-4613b1736433
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2016
ms.author: rachelap
ms.openlocfilehash: 79df54f1dae91d7c5d3b66d208d0d1c1d7d55ae9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-api-apps---whats-changed"></a>App Service API Apps : les nouveautés
À partir de l’événement Connect() hello novembre 2015, un nombre d’améliorations tooAzure du Service d’applications ont été [annoncé](https://azure.microsoft.com/blog/azure-app-service-updates-november-2015/). Ces améliorations sont notamment les modifications sous-jacentes tooAPI applications toobetter s’aligner avec les applications Web et Mobile, réduire le nombre de concept et améliorer les performances de déploiement et d’exécution. En commençant le 30 novembre 2015, de nouvelles applications API vous créez à l’aide du portail de gestion Azure hello ou les outils dernière hello reflète ces modifications. Cet article décrit ces modifications, ainsi que comment tooredeploy parti tootake applications existantes des capacités de hello.

## <a name="feature-changes"></a>Évolution des fonctionnalités
Hello les principales fonctionnalités des applications API : authentification, CORS et l’API de métadonnées : ont transférés directement dans le Service d’applications. Avec cette modification, les fonctions hello sont disponibles sur le Web, mobiles et les applications API. En fait, toutes les partage trois hello même **Microsoft.Web/sites** le type de ressource dans le Gestionnaire de ressources. passerelle des applications API Hello n’est plus nécessaire ni fourni avec les applications API. Cela permet également de faciliter toouse gestion des API Azure, car il y a simplement hello gestion des API passerelle unique.

![Vue d’ensemble d’API Apps](./media/app-service-api-whats-changed/api-apps-overview.png)

Un principe de conception clés avec hello mettre à jour des applications API est tooenable toobring votre API comme est, dans la langue de votre choix.  Si votre API est déjà déployé comme une application Web ou d’une application Mobile, il est inutile tooredeploy Tirez parti de tootake application des nouvelles fonctionnalités de hello. Si vous utilisez actuellement la version préliminaire d’API Apps, vous trouverez des conseils de migration détaillés ci-dessous.

### <a name="authentication"></a>Authentification
Hello existant clé en main les applications API, les Services/applications mobiles et les applications Web les fonctionnalités d’authentification ont été unifiées et sont disponibles dans un panneau de l’authentification unique du Service d’applications Azure dans le portail de gestion hello. Pour une introduction tooauthentication les services dans le Service d’applications, consultez [l’authentification du développement du Service d’applications / autorisation](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/).

Pour les scénarios d’API, il existe plusieurs nouveautés utiles :

* **Prise en charge pour l’utilisation d’Azure Active Directory directement**, sans code de client de jeton AAD tooexchange hello pour un jeton de session : votre client permettre simplement inclure les jetons hello AAD dans l’en-tête d’autorisation de hello, en fonction du jeton de support toohello spécification. Cela signifie également qu'aucun SDK Service spécifique à l’application n’est requis sur hello client ou côté serveur. 
* **Accès de service ou « Interne »**: Si vous avez un processus démon ou un autre client nécessitant tooAPIs accès sans une interface, vous pouvez demander un jeton à l’aide d’un principal du service AAD et passez-le tooApp Service pour l’authentification avec votre application.
* **Différée d’autorisation**: de nombreuses applications ont des restrictions d’accès pour les différentes parties de l’application hello. Vous pouvez choisir de certains toobe API disponible publiquement, tandis que d’autres nécessitent l’ouverture de session. fonction de l’authentification/autorisation Hello d’origine a été tout ou rien, avec l’ensemble du site hello nécessitant une connexion. Cette option existe toujours, mais vous pouvez également autoriser votre code d’application des décisions d’accès toorender une fois que le Service d’applications a authentifié l’utilisateur de hello.

Pour plus d’informations sur les nouvelles fonctionnalités de l’authentification hello, consultez [l’authentification et autorisation pour API Apps dans Azure App Service](app-service-api-authentication.md). Pour plus d’informations sur comment toomigrate des applications API existantes à partir d’applications d’API précédentes hello modèle voir d’un nouveau toohello [applications API existantes de migration](#migrating-existing-api-apps) plus loin dans cet article.

### <a name="cors"></a>CORS
Au lieu d’un CSV **MS_CrossDomainOrigins** application défini, il existe désormais un panneau dans le portail de gestion Azure hello pour la configuration CORS. Il est aussi possible de la configurer à l’aide des outils Resource Manager, tels que Microsoft Azure PowerShell, CLI ou l’ [Explorateur de ressources](https://resources.azure.com/). Ensemble hello **cors** propriété hello **Microsoft.Web/sites/config** type de ressource pour votre  **&lt;nom du site&gt;/web** ressource. Par exemple :

    {
        "cors": {
            "allowedOrigins": [
                "https://localhost:44300"
            ]
        }
    } 

### <a name="api-metadata"></a>Métadonnées des API
Panneau de définition d’API Hello est désormais disponible sur le Web, mobiles et les applications API. Dans le portail de gestion hello, vous pouvez spécifier une url relative ou une url absolue qui pointe tooan le point de terminaison de cette représentation hôtes un Swagger 2.0 de votre API. Vous pouvez aussi la configurer à l’aide des outils Resource Manager. Ensemble hello **apiDefinition** propriété hello **Microsoft.Web/sites/config** type de ressource pour votre  **&lt;nom du site&gt;/web** ressource. Par exemple :

    {
        "apiDefinition":
        {
            "url": "https://myStorageAccount.blob.core.windows.net/swagger/apiDefinition.json"
        }
    }

À ce stade, point de terminaison de métadonnées hello doit toobe accessible publiquement sans authentification pour nombreux clients en aval (génération de client par exemple, Visual Studio API REST et le flux de « Ajouter des API » PowerApps) tooconsume il. Cela signifie que si vous sont à l’aide de l’authentification du Service de l’application et que vous souhaitez définition à partir de l’API tooexpose hello au sein de votre application, vous devez option de différé de l’authentification toouse hello décrite précédemment afin que les métadonnées de Swagger tooyour hello itinéraire sont publique.

## <a name="management-portal"></a>Portail de gestion
En sélectionnant **Nouveau > Web + Mobile > application API** hello de créer des applications API qui reflètent hello nouvelles fonctionnalités décrites dans l’article de hello portal. **Parcourir &gt; API Apps** affiche uniquement ces nouvelles applications API. Une fois que vous accédez à une application API, des partages de panneau hello hello même mise en page et les fonctionnalités que celles des applications Web et mobiles. Hello seules différences sont quickstart contenu et l’ordre des paramètres.

Les applications API existantes (ou Marketplace API apps créés à partir de Logic Apps) avec hello des fonctions de prévisualisation précédentes sera toujours visibles dans le concepteur Logic Apps hello et en parcourant toutes les ressources dans un groupe de ressources.

## <a name="visual-studio"></a>Visual Studio
La plupart des applications Web Outils fonctionnera avec les API de nouvelles applications, car ils partagent hello sous-jacent même **Microsoft.Web/sites** type de ressource. Bonjour Azure Visual Studio pour les outils, cependant, doivent être mis à niveau tooversion 2.8.1 ou version ultérieure étant donné qu’il expose un certain nombre de tooAPIs spécifique de fonctionnalités. Télécharger hello SDK à partir de hello [page Téléchargements Azure](https://azure.microsoft.com/downloads/).

Rationalisation hello Hello types de services d’application, de publier est également unifiée sous **publier > Microsoft Azure App Service**:

![Publication API Apps](./media/app-service-api-whats-changed/api-apps-publish.png)

toolearn plus d’informations sur le SDK 2.8.1, annonce de type hello lecture [billet de blog](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-1-for-net/).

Vous pouvez également importer manuellement hello publier le profil à partir de tooenable portail de gestion hello publier. Cependant, Cloud Explorer, la génération de code et la sélection/création d’applications API nécessitera le SDK 2.8.1 ou une version ultérieure.

## <a name="migrating-existing-api-apps"></a>Migration des applications API existantes
Si votre API personnalisée est déployé toohello précédente version un aperçu des applications d’API, nous demander que vous migrez toohello nouveau modèle pour les applications d’API par le 31 décembre 2015. Étant donné que les modèles anciens et nouveaux de hello sont basées sur les API Web hébergées dans un Service d’applications, majorité hello du code existant peut être réutilisée.

### <a name="hosting-and-redeployment"></a>Hébergement et redéploiement
étapes Hello pour redéployer sont hello même que le déploiement de n’importe quel existant tooApp d’API Web Service. Étapes :

1. Créez une application API vide. Cela est possible dans le portail hello avec New > API App, dans Visual Studio à partir de la publication, ou d’outils du Gestionnaire de ressources. Si vous utilisez les outils du Gestionnaire de ressources ou des modèles, définir hello **type** valeur trop**api** sur hello **Microsoft.Web/sites** Démarrages rapides de ressource type toohave hello et paramètres portail de gestion Hello orienté vers les scénarios d’API.
2. Se connecter et de déployer votre projet toohello vide application API à l’aide des mécanismes de déploiement hello pris en charge par le Service d’applications. Lecture [documentation sur le déploiement du Service d’applications Azure](../app-service-web/web-sites-deploy.md) toolearn plus. 

### <a name="authentication"></a>Authentification
Hello prise en charge des services de l’authentification du Service d’applications hello mêmes fonctions qui étaient disponibles dans le modèle d’applications API précédent hello. Si vous utilisez des jetons de session et que vous avez besoin de kits de développement logiciel, utilisez hello suivant des kits de développement logiciel client et le serveur :

* Client : [Kit de développement logiciel Client Azure Mobile](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/)
* Serveur : [Extension d’authentification .NET Microsoft Azure Mobile App](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/) 

Si vous utilisez hello alpha de Service d’applications SDK au lieu de cela, ils sont désormais déconseillées :

* Client : [Kit de développement logiciel Microsoft Azure AppService](http://www.nuget.org/packages/Microsoft.Azure.AppService)
* Serveur : [Microsoft.Azure.AppService.ApiApps.Service](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service)

En particulier avec Azure Active Directory, toutefois, aucun Service spécifique à l’application est requis si vous utilisez le jeton AAD de hello directement.

### <a name="internal-access"></a>Accès interne
modèle d’applications API précédent Hello inclus un niveau d’accès interne intégrée. Cela nécessaire utilisation du Kit de développement logiciel de hello pour la signature des demandes. Comme décrit précédemment, avec le nouveau modèle d’applications API hello, principaux du service AAD peut servir comme une solution de remplacement pour l’authentification de service sans nécessiter un application spécifique au Service SDK. Pour en savoir plus, consultez [Authentification du principal du service pour API Apps dans Azure App Service](app-service-api-dotnet-service-principal-auth.md).

### <a name="discovery"></a>Découverte
Hello précédente applications API modèle avait API de découverte lors de l’exécution dans les autres applications API hello même groupe de ressources derrière hello même passerelle. Cela est particulièrement utile dans les architectures qui implémentent des modèles de microservice. Bien que cette fonctionnalité ne soit pas directement prise en charge, plusieurs options s’offrent à vous :

1. Utiliser hello API Azure Resource Manager pour la découverte.
2. Placez Azure API Management devant vos API hébergées par App Service. Azure API Management sert de façade et peut fournir une URL externe stable même si votre topologie interne change.
3. Créer votre propre application API de découverte et disposent d’autres applications API inscrire avec l’application de découverte hello au démarrage.
4. Au moment du déploiement, remplir paramètres d’application hello toutes les applications de hello API (et les clients) avec les points de terminaison hello Hello autres applications API. Ceci est envisageable dans les déploiements de modèle et dans la mesure où les applications API vous permettent maintenant le contrôle de l’url de hello.

## <a name="using-api-apps-with-logic-apps"></a>Utilisation d’API Apps avec Logic Apps
nouveau modèle d’applications API Hello fonctionne bien avec [Logic Apps, version du schéma 2015-08-01](../logic-apps/logic-apps-schema-2015-08-01.md).

## <a name="next-steps"></a>Étapes suivantes
toolearn lire plus, les articles hello Bonjour [section de la documentation sur les applications API](https://azure.microsoft.com/documentation/services/app-service/api/). Ils ont été mis à jour tooreflect hello nouveau modèle pour les applications de l’API. En outre, atteignent sur les forums hello pour des détails supplémentaires ou obtenir des conseils sur la migration :

* [Forum MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureAPIApps)
* [Dépassement de capacité de la pile](http://stackoverflow.com/questions/tagged/azure-api-apps)

