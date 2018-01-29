---
title: "Référence du modèle de données du modèle Gestion des API Azure | Microsoft Docs"
description: "Découvrez les représentations de type et d’entité des éléments courants utilisés dans les modèles de données pour les modèles du portail des développeurs dans la Gestion des API Azure."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: b0ad7e15-9519-4517-bb73-32e593ed6380
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/05/2017
ms.author: apimpm
ms.openlocfilehash: 92a52910ef8b9f078a8ea6ac409f89719f889b24
ms.sourcegitcommit: 7f1ce8be5367d492f4c8bb889ad50a99d85d9a89
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/06/2017
---
# <a name="azure-api-management-template-data-model-reference"></a>Référence du modèle de données du modèle Gestion des API Azure
Cette rubrique décrit les représentations de type et d’entité des éléments courants utilisés dans les modèles de données pour les modèles du portail des développeurs dans la Gestion des API Azure.  
  
 Pour plus d’informations sur l’utilisation de modèles, consultez la page [Guide pratique de personnalisation du portail des développeurs Gestion des API à l’aide de modèles](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).  
  
-   [API](#API)  
-   [API summary](#APISummary)  
-   [Application](#Application)  
-   [Attachment](#Attachment)  
-   [Code sample](#Sample)  
-   [Commentaire](#Comment)  
-   [Filtering](#Filtering)  
-   [En-tête](#Header)  
-   [Demande HTTP](#HTTPRequest)  
-   [Réponse HTTP](#HTTPResponse)  
-   [Problème](#Issue)  
-   [Opération](#Operation)  
-   [Operation menu](#Menu)  
-   [Operation menu item](#MenuItem)  
-   [Paging](#Paging)  
-   [Paramètre](#Parameter)  
-   [Produit](#Product)  
-   [Fournisseur](#Provider)  
-   [Representation](#Representation)  
-   [Abonnement](#Subscription)  
-   [Subscription summary](#SubscriptionSummary)  
-   [User account info](#UserAccountInfo)  
-   [User sign in](#UseSignIn)  
-   [User sign up](#UserSignUp)  
  
##  <a name="API"></a> API  
 L’entité `API` a les propriétés suivantes :  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|id|string|Identificateur de ressource. Identifie exclusivement l’API dans l’instance de service Gestion des API actuelle. La valeur est une URL relative valide au format `apis/{id}`, où `{id}` est un identificateur d’API. Cette propriété est en lecture seule.|  
|name|string|Nom de l’API. Ne doit pas être vide. La longueur maximale est de 100 caractères.|  
|description|string|Description de l’API. Ne doit pas être vide. Peut comporter des balises de mise en forme. La longueur maximale est de 1 000 caractères.|  
|serviceUrl|string|URL absolue du service principal qui implémente cette API.|  
|path|string|URL relative identifiant exclusivement cette API et tous les chemins d’accès à ses ressources au sein de l’instance de service Gestion des API. Elle est ajoutée à l’URL de base du point de terminaison d’API spécifiée lors de la création de l’instance de service pour former l’URL publique de cette API.|  
|protocols|tableau de nombres|Indique sur quels protocoles les opérations dans cette API peuvent être appelées. Les valeurs autorisées sont `1 - http` et `2 - https`, ou les deux.|  
|authenticationSettings|[Paramètres d’authentification du serveur d’autorisation](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#AuthenticationSettings)|Collection de paramètres d’authentification inclus dans cette API.|  
|subscriptionKeyParameterNames|objet|Propriété facultative utilisable pour donner des noms personnalisés aux paramètres de requête et/ou d’en-tête contenant la clé de l’abonnement. Lorsque cette propriété est présente, elle doit contenir au moins une des deux propriétés suivantes.<br /><br /> `{   "subscriptionKeyParameterNames":   {     "query": “customQueryParameterName",     "header": “customHeaderParameterName"   } }`|  
  
##  <a name="APISummary"></a> API summary  
 L’entité `API summary` a les propriétés suivantes :  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|id|string|Identificateur de ressource. Identifie exclusivement l’API dans l’instance de service Gestion des API actuelle. La valeur est une URL relative valide au format `apis/{id}`, où `{id}` est un identificateur d’API. Cette propriété est en lecture seule.|  
|name|string|Nom de l’API. Ne doit pas être vide. La longueur maximale est de 100 caractères.|  
|description|string|Description de l’API. Ne doit pas être vide. Peut comporter des balises de mise en forme. La longueur maximale est de 1 000 caractères.|  
  
##  <a name="Application"></a> Application  
 L’entité `application` a les propriétés suivantes :  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|ID|string|Identificateur unique de l’application.|  
|Intitulé|string|Titre de l’application.|  
|Description|string|Description de l’application.|  
|Url|URI|URI de l’application.|  
|Version|string|Informations de version de l’application.|  
|Configuration requise|string|Description des conditions requises de l’application.|  
|State|number|État actuel de l’application.<br /><br /> - 0 - Inscrite<br /><br /> - 1 - Soumise<br /><br /> - 2 - Publiée<br /><br /> - 3 - Rejetée<br /><br /> - 4 - Non publiée|  
|RegistrationDate|DateTime|Date et heure auxquelles l’application a été inscrite.|  
|CategoryId|number|Catégorie de l’application (finance, divertissement, etc.).|  
|DeveloperId|string|Identificateur unique du développeur qui a soumis l’application.|  
|Pièces jointes|Collection d’entités [Attachment](#Attachment).|Pièces jointes de l’application, telles que des captures d’écran ou des icônes.|  
|Icône|[Attachment](#Attachment)|Icône de l’application.|  
  
##  <a name="Attachment"></a> Attachment  
 L’entité `attachment` a les propriétés suivantes :  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|UniqueId|string|Identificateur unique de la pièce jointe.|  
|Url|string|URL de la ressource.|  
|Type|string|Type de pièce jointe.|  
|ContentType|string|Type de média de la pièce jointe.|  
  
##  <a name="Sample"></a> Code sample  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|title|string|Nom de l’opération.|  
|snippet|string|Cette propriété est déconseillée et ne doit pas être utilisée.|  
|brush|string|Modèle de coloration de la syntaxe de code à utiliser pour afficher l’exemple de code. Les valeurs autorisées sont `plain`, `php`, `java`, `xml`, `objc`, `python`, `ruby` et `csharp`.|  
|template|string|Nom de ce modèle d’exemple de code.|  
|body|string|Espace réservé de la portion d’exemple de code de l’extrait de code.|  
|statique|string|Méthode HTTP de l’opération.|  
|scheme|string|Protocole à utiliser pour la demande d’opération.|  
|path|string|Chemin de l’opération.|  
|query|string|Exemple de chaîne de requête avec des paramètres définis.|  
|host|string|URL de la passerelle du service Gestion des API de l’API qui contient cette opération.|  
|En-têtes|Collection d’entités [Header](#Header).|En-têtes de cette opération.|  
|parameters|Collection d’entités [Parameter](#Parameter).|Paramètres définis pour cette opération.|  
  
##  <a name="Comment"></a> Comment  
 L’entité `API` a les propriétés suivantes :  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|ID|number|ID du commentaire.|  
|CommentText|string|Corps du commentaire. Peut comporter du code HTML.|  
|DeveloperCompany|string|Nom de l’entreprise du développeur.|  
|PostedOn|DateTime|Date et l’heure auxquelles le commentaire a été publié.|  
  
##  <a name="Issue"></a> Issue  
 L’entité `issue` a les propriétés suivantes :  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|ID|string|Identificateur unique du problème.|  
|ApiID|string|ID de l’API pour laquelle ce problème a été signalé.|  
|Intitulé|string|Titre du problème.|  
|Description|string|Description du problème.|  
|SubscriptionDeveloperName|string|Prénom du développeur qui a signalé le problème.|  
|IssueState|string|État actuel du problème. Les valeurs possibles sont Proposed, Opened et Closed (Proposé, Ouvert et Fermé).|  
|ReportedOn|DateTime|Date et heure auxquelles le problème a été signalé.|  
|Commentaires|Collection d’entités [Comment](#Comment).|Commentaires sur ce problème.|  
|Pièces jointes|Collection d’entités [Attachment](api-management-template-data-model-reference.md#Attachment).|Pièces jointes à ce problème.|  
|Services|Collection d’entités [API](#API).|API auxquelles l’utilisateur qui a consigné le problème est abonné.|  
  
##  <a name="Filtering"></a> Filtering  
 L’entité `filtering` a les propriétés suivantes :  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|Modèle|string|Terme de recherche actuel ; ou `null` en l’absence de terme de recherche.|  
|Placeholder|string|Texte à afficher dans la zone de recherche si aucun terme de recherche n’est spécifié.|  
  
##  <a name="Header"></a> Header  
 Cette section décrit la représentation `parameter`.  
  
|Propriété|Description|Type|  
|--------------|-----------------|----------|  
|name|string|Nom du paramètre.|  
|description|string|Description du paramètre.|  
|value|string|Valeur de l’en-tête.|  
|typeName|string|Type de données de la valeur d’en-tête.|  
|options|string|Options.|  
|required|booléenne|Indique si l’en-tête est requis.|  
|readOnly|booléenne|Indique si l’en-tête est en lecture seule.|  
  
##  <a name="HTTPRequest"></a> HTTP Request  
 Cette section décrit la représentation `request`.  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|description|string|Description de la demande d’opération.|  
|En-têtes|tableau d’entités [Header](#Header).|En-têtes de demande.|  
|parameters|tableau de [Parameter](#Parameter)|Collection de paramètres de demande d’opération.|  
|representations|tableau de [Representation](#Representation)|Collection de représentations de demande d’opération.|  
  
##  <a name="HTTPResponse"></a> HTTP Response  
 Cette section décrit la représentation `response`.  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|statusCode|entier positif|Code de statut de la réponse de l’opération.|  
|description|string|Description de la réponse de l’opération.|  
|representations|tableau de [Representation](#Representation)|Collection de représentations de la réponse de l’opération.|  
  
##  <a name="Operation"></a> Operation  
 L’entité `operation` a les propriétés suivantes :  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|id|string|Identificateur de ressource. Identifie exclusivement l’opération dans l’instance de service Gestion des API actuelle. La valeur est une URL relative valide au format `apis/{aid}/operations/{id}`, où `{aid}` est un identificateur d’API et `{id}` un identificateur d’opération. Cette propriété est en lecture seule.|  
|name|string|Nom de l’opération. Ne doit pas être vide. La longueur maximale est de 100 caractères.|  
|description|string|Description de l’opération. Ne doit pas être vide. Peut comporter des balises de mise en forme. La longueur maximale est de 1 000 caractères.|  
|scheme|string|Indique sur quels protocoles les opérations dans cette API peuvent être appelées. Les valeurs autorisées sont `http`, `https`, ou à la fois `http` et `https`.|  
|uriTemplate|string|Modèle d’URL relative identifiant la ressource cible de cette opération. Peut comporter des paramètres. Exemple : `customers/{cid}/orders/{oid}/?date={date}`|  
|host|string|URL de la passerelle de la Gestion des API qui héberge l’API.|  
|httpMethod|string|Méthode HTTP de l’opération.|  
|request|[Demande HTTP](#HTTPRequest)|Entité qui contient les détails de la demande.|  
|responses|tableau de [HTTP Response](#HTTPResponse)|Tableau d’entités [HTTP Response](#HTTPResponse) de l’opération.|  
  
##  <a name="Menu"></a> Operation menu  
 L’entité `operation menu` a les propriétés suivantes :  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|ApiId|string|ID de l’API actuelle.|  
|CurrentOperationId|string|ID de l’opération actuelle.|  
|Action|string|Type de menu.|  
|MenuItems|Collection d’entités [Operation menu item](#MenuItem).|Opérations de l’API actuelle.|  
  
##  <a name="MenuItem"></a> Operation menu item  
 L’entité `operation menu item` a les propriétés suivantes :  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|ID|string|ID de l’opération.|  
|Intitulé|string|Description de l’opération.|  
|HttpMethod|string|Méthode HTTP de l’opération.|  
  
##  <a name="Paging"></a> Paging  
 L’entité `paging` a les propriétés suivantes :  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|Page|number|Numéro de page actuel.|  
|PageSize|number|Maximum de résultats à afficher sur une seule page.|  
|TotalItemCount|number|Nombre d’éléments à afficher.|  
|ShowAll|booléenne|Indique si tous les résultats doivent être affichés sur une seule page.|  
|PageCount|number|Nombre de pages de résultats.|  
  
##  <a name="Parameter"></a> Parameter  
 Cette section décrit la représentation `parameter`.  
  
|Propriété|Description|Type|  
|--------------|-----------------|----------|  
|name|string|Nom du paramètre.|  
|description|string|Description du paramètre.|  
|value|string|Valeur du paramètre.|  
|options|tableau de chaînes|Valeurs définies pour les valeurs du paramètre de requête.|  
|required|booléenne|Indique si le paramètre est obligatoire ou non.|  
|kind|number|Indique si ce paramètre est un paramètre de chemin d’accès (1) ou un paramètre de chaîne de requête (2).|  
|typeName|string|Type de paramètre.|  
  
##  <a name="Product"></a> Product  
 L’entité `product` a les propriétés suivantes :  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|ID|string|Identificateur de ressource. Identifie exclusivement le produit dans l’instance de service Gestion des API actuelle. La valeur est une URL relative valide au format `products/{pid}`, où `{pid}` est un identificateur de produit. Cette propriété est en lecture seule.|  
|Intitulé|string|Nom du produit. Ne doit pas être vide. La longueur maximale est de 100 caractères.|  
|Description|string|Description du produit. Ne doit pas être vide. Peut comporter des balises de mise en forme. La longueur maximale est de 1 000 caractères.|  
|Termes|string|Conditions d’utilisation du produit. Les développeurs qui veulent s’abonner au produit devront consulter et accepter ces conditions pour pouvoir terminer le processus d’abonnement.|  
|ProductState|number|Spécifie si le produit est publié ou non. Les produits publiés sont détectables par les développeurs sur le portail des développeurs. Les produits non publiés ne sont visibles que pour les administrateurs.<br /><br /> Les valeurs autorisées pour l’état du produit sont :<br /><br /> - `0 - Not Published`<br /><br /> - `1 - Published`<br /><br /> - `2 - Deleted`|  
|AllowMultipleSubscriptions|booléenne|Spécifie si un utilisateur peut avoir plusieurs abonnements à ce produit en même temps.|  
|MultipleSubscriptionsCount|number|Nombre d’abonnements à ce produit de l’utilisateur actuel.|  
  
##  <a name="Provider"></a> Provider  
 L’entité `provider` a les propriétés suivantes :  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|Propriétés|dictionnaire de chaînes|Propriétés de ce fournisseur d’authentification.|  
|AuthenticationType|string|Type de fournisseur. (Azure Active Directory, compte Facebook, compte Google, compte Microsoft, Twitter).|  
|Caption|string|Nom complet du fournisseur.|  
  
##  <a name="Representation"></a> Representation  
 Cette section décrit une `representation`.  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|contentType|string|Spécifie un type de contenu inscrit ou personnalisé pour cette représentation, par exemple, `application/xml`.|  
|sample|string|Exemple de la représentation.|  
  
##  <a name="Subscription"></a> Subscription  
 L’entité `subscription` a les propriétés suivantes :  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|ID|string|Identificateur de ressource. Identifie exclusivement l’abonnement dans l’instance de service Gestion des API actuelle. La valeur est une URL relative valide au format `subscriptions/{sid}`, où `{sid}` est un identificateur d’abonnement. Cette propriété est en lecture seule.|  
|ProductId|string|Identificateur de ressource du produit concerné par l’abonnement. La valeur est une URL relative valide au format `products/{pid}`, où `{pid}` est un identificateur de produit.|  
|ProductTitle|string|Nom du produit. Ne doit pas être vide. La longueur maximale est de 100 caractères.|  
|ProductDescription|string|Description du produit. Ne doit pas être vide. Peut comporter des balises de mise en forme. La longueur maximale est de 1 000 caractères.|  
|ProductDetailsUrl|string|URL relative des détails du produit.|  
|state|string|État de l’abonnement. Les états possibles sont :<br /><br /> - `0 - suspended` : l’abonnement est bloqué et l’abonné ne peut appeler aucune API du produit.<br /><br /> - `1 - active` : l’abonnement est actif.<br /><br /> - `2 - expired` : l’abonnement a atteint sa date d’expiration et a été désactivé.<br /><br /> - `3 - submitted` : la demande d’abonnement a été effectuée par le développeur, mais n’a pas encore été approuvée ou rejetée.<br /><br /> - `4 - rejected` : la demande d’abonnement a été refusée par un administrateur.<br /><br /> - `5 - cancelled` : l’abonnement a été annulé par le développeur ou l’administrateur.|  
|DisplayName|string|Nom complet de l’abonnement.|  
|CreatedDate|dateTime|Date à laquelle l’abonnement a été créé, au format ISO 8601 : `2014-06-24T16:25:00Z`.|  
|CanBeCancelled|booléenne|Indique si l’abonnement peut être annulé par l’utilisateur actuel.|  
|IsAwaitingApproval|booléenne|Indique si l’abonnement est en attente d’approbation.|  
|StartDate|dateTime|Date de début de l’abonnement, au format ISO 8601 : `2014-06-24T16:25:00Z`.|  
|ExpirationDate|dateTime|Date d’expiration de l’abonnement, au format ISO 8601 : `2014-06-24T16:25:00Z`.|  
|NotificationDate|dateTime|Date de notification de l’abonnement, au format ISO 8601 : `2014-06-24T16:25:00Z`.|  
|primaryKey|string|Clé primaire de l’abonnement. La longueur maximale est de 256 caractères.|  
|secondaryKey|string|Clé secondaire de l’abonnement. La longueur maximale est de 256 caractères.|  
|CanBeRenewed|booléenne|Indique si l’abonnement peut être renouvelé par l’utilisateur actuel.|  
|HasExpired|booléenne|Indique si l’abonnement a expiré.|  
|IsRejected|booléenne|Indique si la demande d’abonnement a été refusée.|  
|CancelUrl|string|URL relative pour annuler l’abonnement.|  
|RenewUrl|string|URL relative pour renouveler l’abonnement.|  
  
##  <a name="SubscriptionSummary"></a> Subscription summary  
 L’entité `subscription summary` a les propriétés suivantes :  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|ID|string|Identificateur de ressource. Identifie exclusivement l’abonnement dans l’instance de service Gestion des API actuelle. La valeur est une URL relative valide au format `subscriptions/{sid}`, où `{sid}` est un identificateur d’abonnement. Cette propriété est en lecture seule.|  
|DisplayName|string|Nom complet de l’abonnement.|  
  
##  <a name="UserAccountInfo"></a> User account info  
 L’entité `user account info` a les propriétés suivantes :  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|FirstName|string|Prénom. Ne doit pas être vide. La longueur maximale est de 100 caractères.|  
|LastName|string|Nom. Ne doit pas être vide. La longueur maximale est de 100 caractères.|  
|Email|string|Adresse de messagerie. Ne doit pas être vide et doit être unique au sein de l’instance de service. La longueur maximale est de 254 caractères.|  
|Mot de passe|string|Mot de passe du compte d’utilisateur.|  
|NameIdentifier|string|Identificateur du compte, identique à l’adresse de messagerie de l’utilisateur.|  
|ProviderName|string|Nom du fournisseur d’authentification.|  
|IsBasicAccount|booléenne|True si ce compte a été inscrit avec une adresse de messagerie et un mot de passe ; False si le compte a été inscrit à l’aide d’un fournisseur.|  
  
##  <a name="UseSignIn"></a> User sign in  
 L’entité `user sign in` a les propriétés suivantes :  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|Email|string|Adresse de messagerie. Ne doit pas être vide et doit être unique au sein de l’instance de service. La longueur maximale est de 254 caractères.|  
|Mot de passe|string|Mot de passe du compte d’utilisateur.|  
|ReturnUrl|string|URL de la page sur laquelle l’utilisateur a cliqué sur Se connecter.|  
|RememberMe|booléenne|Indique si les informations de l’utilisateur actuel doivent être enregistrées.|  
|RegistrationEnabled|booléenne|Indique si l’inscription est activée.|  
|DelegationEnabled|booléenne|Indique si la connexion déléguée est activée.|  
|DelegationUrl|string|URL de la connexion déléguée, si elle est activée.|  
|SsoSignUpUrl|string|URL d’authentification unique de l’utilisateur, le cas échéant.|  
|AuxServiceUrl|string|Si l’utilisateur actuel est administrateur, lien vers l’instance de service dans le portail Azure.|  
|Fournisseurs|Collection d’entités [Provider](#Provider).|Fournisseurs d’authentification de cet utilisateur.|  
|UserRegistrationTerms|string|Conditions qu’un utilisateur doit accepter pour pouvoir se connecter.|  
|UserRegistrationTermsEnabled|booléenne|Indique si les conditions sont activées.|  
  
##  <a name="UserSignUp"></a> User sign up  
 L’entité `user sign up` a les propriétés suivantes :  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|PasswordConfirm|booléenne|Valeur utilisée par le contrôle [d’inscription](api-management-page-controls.md#sign-up).|  
|Mot de passe|string|Mot de passe du compte d’utilisateur.|  
|PasswordVerdictLevel|number|Valeur utilisée par le contrôle [d’inscription](api-management-page-controls.md#sign-up).|  
|UserRegistrationTerms|string|Conditions qu’un utilisateur doit accepter pour pouvoir se connecter.|  
|UserRegistrationTermsOptions|number|Valeur utilisée par le contrôle [d’inscription](api-management-page-controls.md#sign-up).|  
|ConsentAccepted|booléenne|Valeur utilisée par le contrôle [d’inscription](api-management-page-controls.md#sign-up).|  
|Email|string|Adresse de messagerie. Ne doit pas être vide et doit être unique au sein de l’instance de service. La longueur maximale est de 254 caractères.|  
|FirstName|string|Prénom. Ne doit pas être vide. La longueur maximale est de 100 caractères.|  
|LastName|string|Nom. Ne doit pas être vide. La longueur maximale est de 100 caractères.|  
|UserData|string|Valeur utilisée par le contrôle [d’inscription](api-management-page-controls.md#sign-up).|  
|NameIdentifier|string|Valeur utilisée par le contrôle [d’inscription](api-management-page-controls.md#sign-up).|  
|ProviderName|string|Nom du fournisseur d’authentification.|

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur l’utilisation de modèles, consultez [Comment personnaliser le portail des développeurs Gestion des API Azure à l’aide de modèles](api-management-developer-portal-templates.md).
