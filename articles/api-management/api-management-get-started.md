---
title: "aaaManage votre première API de gestion des API Azure | Documents Microsoft"
description: "Découvrez comment toocreate API, ajouter des opérations et commencer à la gestion des API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 51b7df8b-1c43-43c6-90c9-0aa24f48206b
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 7d43f33aa359c4d1e605e9fb41e43d323ca6a777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-first-api-in-azure-api-management"></a>Gérer votre première API dans Gestion des API Azure
## <a name="overview"></a>Vue d’ensemble
Ce guide vous explique comment tooquickly prise en main d’à l’aide de la gestion des API Azure et votre premier appel d’API.

## <a name="concepts"></a>Qu’est-ce que Gestion des API Azure ?
Vous pouvez utiliser Gestion des API Azure tootake n’importe quel serveur principal et lancer un programme API à part entière basé sur celui-ci.

Scénarios courants :

* **Sécurisation d’infrastructures mobiles** par régulation de l’accès à l’aide de clés d’API pour éviter les attaques par déni de service (DOS) en utilisant la limitation ou des stratégies de sécurité avancées, telles que la validation de jeton JWT
* **L’activation des écosystèmes partenaire ISV** en offrant l’intégration de partenaire rapide via le développeur de hello, portail et la création d’un toodecouple de façade API à partir des implémentations internes qui ne sont pas de la consommation du partenaire.
* **Exécution d’un programme API interne** en offrant un emplacement centralisé pour toocommunicate d’organisation hello sur la disponibilité de hello et de la plus récente des modifications tooAPIs, régulation d’accès basé sur les comptes de société, toutes basées sur un canal sécurisé entre Hello passerelle API et hello back-end.

système de Hello est constitué par hello suivant des composants :

* Hello **passerelle API** est le point de terminaison hello qui :
  
  * Accepte les API appelle et les route les serveurs principaux tooyour.
  * vérifie les clés d’API, les jetons JWT, les certificats et les autres informations d’identification ;
  * applique des quotas d’utilisation et des limites de débit ;
  * Transforme votre API hello volée, sans modification de code.
  * met en cache les réponses du serveur principal lorsqu’il est configuré ;
  * enregistre les métadonnées relatives aux appels à des fins d’analyse.
* Hello **portail de publication** est hello interface d’administration dans lequel vous configurez votre programme API. Utilisez-le pour :
  
  * définir ou importer le schéma d’API ;
  * intégrer des API aux produits sous forme de packages ;
  * Configurer des stratégies, telles que les quotas ou transformations sur hello API.
  * obtenir des informations issues de l’analyse ;
  * gérer les utilisateurs.
* Hello **portail des développeurs** sert de présence du site web principal hello pour les développeurs, où ils peuvent :
  
  * lire la documentation de l’API ;
  * Essayer une API via une console interactive de hello.
  * Créer un compte et vous abonner tooget API clés.
  * accéder aux analyses relatives à leur propre utilisation.

## <a name="create-service-instance"></a>Création d’une instance du service Gestion des API
> [!NOTE]
> toocomplete ce didacticiel, vous avez besoin d’un compte Azure. Si vous ne possédez pas de compte, vous pouvez créer un compte gratuit en quelques minutes. Pour plus d’informations, consultez la rubrique [Version d’évaluation gratuite d’Azure][Azure Free Trial].
> 
> 

Hello première étape de travail avec la gestion des API est toocreate une instance de service. Connectez-vous à toohello [Azure Portal] [ Azure Portal] et cliquez sur **nouveau**, **Web + Mobile**, **gestion des API**.

![Nouvelle instance Gestion des API][api-management-create-instance-menu]

Pour **nom**, spécifiez un toouse de nom de sous-domaine unique pour l’URL du service hello.

Choisissez hello souhaité **abonnement**, **groupe de ressources** et **emplacement** pour votre instance de service.

Entrez **Contoso Ltd.** pour hello **nom de l’organisation**, puis entrez votre adresse de messagerie dans hello **E-Mail administrateur** champ.

> [!NOTE]
> Cette adresse de messagerie est utilisée pour les notifications de hello système de gestion des API. Pour plus d’informations, consultez [comment tooconfigure notifications et modèles dans Azure API Management de messagerie][How tooconfigure notifications and email templates in Azure API Management].
> 
> 

![Nouveau service Gestion des API][api-management-create-instance-step1]

Les instances du service Gestion des API sont disponibles dans trois niveaux : Développeur, Standard et Premium.

> [!NOTE]
> Hello niveau développeur est pour le développement, le test et des programmes d’API pilotes lorsque la haute disponibilité n’est pas un problème. Dans hello Standard et les niveaux Premium, vous pouvez faire évoluer votre toohandle de nombre d’unités réservées plus de trafic. les niveaux Standard et Premium Hello fournissent votre service de gestion des API avec hello plus de puissance de traitement et de performances. Vous pouvez effectuer ce didacticiel à l’aide de n’importe quel niveau. Pour en savoir plus sur les niveaux du service Gestion des API, consultez la page relative à la [tarification du service Gestion des API][API Management pricing].
> 
> 

Cliquez sur **créer** toostart votre instance du service de configuration.

![Nouveau service Gestion des API][api-management-instance-created]

Après la création de l’instance de service de hello, étape suivante de hello est toocreate ou importer une API.

## <a name="create-api"></a>Importation d’une API
Une API se compose d’un ensemble d’opérations pouvant être appelées à partir d’une application cliente. Opérations d’API sont traitées tooexisting des services web.

Il est possible de créer des API (et d’ajouter des opérations) manuellement ou de les importer. Dans ce didacticiel, nous allons importer hello API pour un service web de calculatrice exemple fourni par Microsoft et hébergé sur Azure.

> [!NOTE]
> Pour obtenir des conseils sur la création d’une API et l’ajout manuel des opérations, consultez [comment toocreate API](api-management-howto-create-apis.md) et [comment tooadd opérations tooan API](api-management-howto-add-operations.md).
> 
> 

API est configurés à partir du portail de publication hello. tooreach, cliquez sur **portail de publication** à partir de la barre d’outils du service hello.

![Portail des éditeurs][api-management-management-console]

calcul de hello tooimport API, cliquez sur **API** de hello **gestion des API** menu sur hello gauche, puis cliquez sur **API d’importation**.

![Bouton Importer l’API][api-management-import-api]

Effectuez hello suivant les étapes tooconfigure hello calculatrice API :

1. Cliquez sur **From URL**, entrez **http://calcapi.cloudapp.net/calcapi.json** dans hello **URL du document de spécification** texte, puis cliquez sur hello **Swagger**  case d’option.
2. Type **calc** dans hello **suffixe d’URL d’API Web** zone de texte.
3. Cliquez sur Bonjour **produits (facultatifs)** et sélectionnez **Starter**.
4. Cliquez sur **enregistrer** tooimport hello API.

![Ajouter une nouvelle API][api-management-import-new-api]

> [!NOTE]
> **Gestion des API** prend actuellement en charge les versions 1.2 et 2.0 du document Swagger dans le cadre d’une importation. Même si la [spécification Swagger 2.0](http://swagger.io/specification) indique que les propriétés `host`, `basePath` et `schemes` sont facultatives, votre document Swagger 2.0 **DOIT** contenir ces propriétés ; dans le cas contraire, l’importation échouera. 
> 
> 

Une fois les API hello est importé, hello page Résumé pour l’API de hello s’affiche dans le portail de publication hello.

![Résumé des API][api-management-imported-api-summary]

Hello section API comporte plusieurs onglets. Hello **Résumé** onglet affiche les mesures de base et de plus d’informations sur les API de hello. Hello [paramètres](api-management-howto-create-apis.md#configure-api-settings) onglet est utilisée configuration hello tooview et modifier d’API. Hello [Operations](api-management-howto-add-operations.md) onglet est les opérations utilisées toomanage hello l’API. Hello **sécurité** onglet peut être l’authentification de la passerelle tooconfigure utilisé pour le serveur principal de hello à l’aide de l’authentification de base ou [authentification mutuelle des certificats](api-management-howto-mutual-certificates.md)et tooconfigure [ autorisation de l’utilisateur à l’aide d’OAuth 2.0](api-management-howto-oauth2.md).  Hello **problèmes** onglet est tooview utilisé les problèmes signalés par les développeurs de hello qui sont à l’aide de votre API. Hello **produits** onglet est produits hello tooconfigure utilisé qui contiennent cette API.

Par défaut, chaque instance Gestion des API est fournie avec deux exemples de produits :

* **Starter**
* **Illimité**

Dans ce didacticiel, hello API de calculatrice de base a été ajouté produit des Starter toohello lorsque hello API a été importé.

Dans l’ordre toomake appelle tooan API, les développeurs doivent tout d’abord s’abonnent produit tooa qui leur donne accès tooit. Les développeurs peuvent s’abonner tooproducts dans le portail des développeurs hello ou les administrateurs peuvent s’abonner tooproducts les développeurs dans le portail de publication hello. Vous êtes un administrateur depuis la création d’instance gestion des API de hello Bonjour étapes précédentes dans le didacticiel de hello, donc vous sentez déjà abonnés tooevery produit par défaut.

## <a name="call-operation"></a>Appeler une opération à partir du portail des développeurs hello
Opérations peuvent être appelées directement depuis le portail des développeurs hello, qui fournit un moyen pratique de tooview et tester le fonctionnement d’une API hello. Dans cette étape du didacticiel, vous appelez l’API du calcul de base hello **ajouter deux entiers** opération. Cliquez sur **portail des développeurs** à partir du menu de hello en hello haut à droite de portail de publication hello.

![Portail des développeurs][api-management-developer-portal-menu]

Cliquez sur **API** dans le menu du haut hello, puis cliquez sur **calculatrice de base** toosee hello opérations disponibles.

![Portail des développeurs][api-management-developer-portal-calc-api]

Notez les descriptions d’exemple hello et les paramètres qui ont été importées avec hello API et opérations, en fournissant une documentation pour les développeurs hello qui utilisera cette opération. Ces descriptions peuvent également être ajoutées lorsque des opérations sont ajoutées manuellement.

toocall hello **ajouter deux entiers** opération, cliquez sur **essayez-la**.

![Essayer][api-management-developer-portal-calc-api-console]

Vous pouvez entrer des valeurs pour les paramètres de hello ou conserver les valeurs par défaut hello, puis cliquez sur **envoyer**.

![HTTP Get][api-management-invoke-get]

Une fois une opération est appelée, le portail des développeurs hello affiche hello **état de la réponse**, hello **les en-têtes de réponse**et n’importe quel **contenu de la réponse**.

![Réponse][api-management-invoke-get-response]

## <a name="view-analytics"></a>Affichage des analyses
analytique tooview de calculatrice de base, portail de publication commutateur toohello arrière en sélectionnant **gérer** à partir du menu de hello en hello supérieur droit du portail des développeurs hello.

![Gérer][api-management-manage-menu]

vue par défaut pour le portail de publication hello Hello est hello **tableau de bord**, qui fournit une vue d’ensemble de votre instance de la gestion des API.

![tableau de bord][api-management-dashboard]

Pointez la souris de hello sur graphique hello pour **calculatrice de base** toosee des métriques hello spécifiques pour l’utilisation de hello Hello API pour une période donnée.

> [!NOTE]
> Si vous ne voyez pas toutes les lignes de votre graphique, basculez le portail des développeurs toohello arrière effectuer des appels dans hello API, attendez quelques instants et puis revenir toohello le tableau de bord.
> 
> 

Cliquez sur **afficher les détails** tooview page de résumé hello pour hello API, y compris une version supérieure de métriques de hello affiché.

![Analyse][api-management-mouse-over]

![Résumé][api-management-api-summary-metrics]

Pour les métriques détaillées et des rapports, cliquez sur **Analytique** de hello **gestion des API** menu à gauche de hello.

![Vue d'ensemble][api-management-analytics-overview]

Hello **Analytique** section a hello suivant quatre onglets :

* **Un coup de œil** fournit de l’utilisation globale et des mesures de santé, également hello développeurs, produits principaux, API supérieur et opérations supérieure.
* **Utilisation** fournit une présentation détaillée des appels d’API et de la bande passante, y compris une représentation géographique.
* **Intégrité** se concentre sur les codes d'état, les taux de réussite en cache, les temps de réponse et les temps de réponse d'API et de service.
* **Activité** fournit des rapports qui explorent sur une activité spécifique par le développeur, produit, API et opération hello.

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[protéger votre API avec les limites de taux](api-management-howto-product-with-rules.md).

[Azure Free Trial]: http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=api_management_hero_a

[Create an API Management instance]: #create-service-instance
[Create an API]: #create-api
[Add an operation]: #add-operation
[Add hello new API tooa product]: #add-api-to-product
[Subscribe toohello product that contains hello API]: #subscribe
[Call an operation from hello Developer Portal]: #call-operation
[View analytics]: #view-analytics
[Next steps]: #next-steps


[How toomanage developer accounts in Azure API Management]: api-management-howto-create-or-invite-developers.md
[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[How tooconfigure notifications and email templates in Azure API Management]: api-management-howto-configure-notifications.md
[Responses]: api-management-howto-add-operations.md#responses
[How create and publish a product]: api-management-howto-add-products.md
[API Management pricing]: http://azure.microsoft.com/pricing/details/api-management/

[Azure Portal]: https://portal.azure.com/

[api-management-management-console]: ./media/api-management-get-started/api-management-management-console.png
[api-management-create-instance-menu]: ./media/api-management-get-started/api-management-create-instance-menu.png
[api-management-create-instance-step1]: ./media/api-management-get-started/api-management-create-instance-step1.png
[api-management-create-instance-step2]: ./media/api-management-get-started/api-management-create-instance-step2.png
[api-management-instance-created]: ./media/api-management-get-started/api-management-instance-created.png
[api-management-import-api]: ./media/api-management-get-started/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-get-started/api-management-import-new-api.png
[api-management-imported-api-summary]: ./media/api-management-get-started/api-management-imported-api-summary.png
[api-management-calc-operations]: ./media/api-management-get-started/api-management-calc-operations.png
[api-management-list-products]: ./media/api-management-get-started/api-management-list-products.png
[api-management-add-api-to-product]: ./media/api-management-get-started/api-management-add-api-to-product.png
[api-management-add-myechoapi-to-product]: ./media/api-management-get-started/api-management-add-myechoapi-to-product.png
[api-management-api-added-to-product]: ./media/api-management-get-started/api-management-api-added-to-product.png
[api-management-developers]: ./media/api-management-get-started/api-management-developers.png
[api-management-add-subscription]: ./media/api-management-get-started/api-management-add-subscription.png
[api-management-add-subscription-window]: ./media/api-management-get-started/api-management-add-subscription-window.png
[api-management-subscription-added]: ./media/api-management-get-started/api-management-subscription-added.png
[api-management-developer-portal-menu]: ./media/api-management-get-started/api-management-developer-portal-menu.png
[api-management-developer-portal-calc-api]: ./media/api-management-get-started/api-management-developer-portal-calc-api.png
[api-management-developer-portal-calc-api-console]: ./media/api-management-get-started/api-management-developer-portal-calc-api-console.png
[api-management-invoke-get]: ./media/api-management-get-started/api-management-invoke-get.png
[api-management-invoke-get-response]: ./media/api-management-get-started/api-management-invoke-get-response.png
[api-management-manage-menu]: ./media/api-management-get-started/api-management-manage-menu.png
[api-management-dashboard]: ./media/api-management-get-started/api-management-dashboard.png

[api-management-add-response]: ./media/api-management-get-started/api-management-add-response.png
[api-management-add-response-window]: ./media/api-management-get-started/api-management-add-response-window.png
[api-management-developer-key]: ./media/api-management-get-started/api-management-developer-key.png
[api-management-mouse-over]: ./media/api-management-get-started/api-management-mouse-over.png
[api-management-api-summary-metrics]: ./media/api-management-get-started/api-management-api-summary-metrics.png
[api-management-analytics-overview]: ./media/api-management-get-started/api-management-analytics-overview.png
[api-management-analytics-usage]: ./media/api-management-get-started/api-management-analytics-usage.png
[api-management-]: ./media/api-management-get-started/api-management-.png
[api-management-]: ./media/api-management-get-started/api-management-.png
