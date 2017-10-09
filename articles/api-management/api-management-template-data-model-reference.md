---
title: "référence du modèle de données de modèle de gestion des API aaaAzure | Documents Microsoft"
description: "En savoir plus sur les représentations de type d’entité et hello pour les éléments communs utilisés dans les modèles de données hello pour les modèles de portail de développement hello dans Gestion des API Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: b0ad7e15-9519-4517-bb73-32e593ed6380
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 7d049d8ecc9e597cf48ce0c820c172798bcf86de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-template-data-model-reference"></a>Référence du modèle de données du modèle Gestion des API Azure
Cette rubrique décrit les représentations de type d’entité et hello pour les éléments communs utilisés dans les modèles de données hello pour les modèles de portail de développement hello dans Gestion des API Azure.  
  
 Pour plus d’informations sur l’utilisation des modèles, consultez [comment toocustomize hello portail des développeurs gestion des API à l’aide de modèles](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).  
  
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
 Hello `API` entité a hello propriétés suivantes.  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|id|string|Identificateur de ressource. Identifie de façon unique les API hello au sein de l’instance de service de gestion des API actuelle hello. valeur de Hello est une URL relative valide au format hello de `apis/{id}` où `{id}` est un identificateur d’API. Cette propriété est en lecture seule.|  
|name|string|Nom de l’API de hello. Ne doit pas être vide. La longueur maximale est de 100 caractères.|  
|description|string|Description de l’API de hello. Ne doit pas être vide. Peut comporter des balises de mise en forme. La longueur maximale est de 1 000 caractères.|  
|serviceUrl|string|URL absolue du service de serveur principal hello qui implémente cette API.|  
|path|string|URL relative identifiant de manière unique cette API et tous ses chemins d’accès de ressource au sein de l’instance de service de gestion des API hello. Il est ajouté l’URL de base du point de terminaison toohello API spécifié pendant hello service instance création tooform une URL publique pour cette API.|  
|protocols|tableau de nombres|Décrit dans quel hello protocoles opérations dans cette API peuvent être appelées. Les valeurs autorisées sont `1 - http` et `2 - https`, ou les deux.|  
|authenticationSettings|[Paramètres d’authentification du serveur d’autorisation](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#AuthenticationSettings)|Collection de paramètres d’authentification inclus dans cette API.|  
|subscriptionKeyParameterNames|objet|Propriété facultative qui peut être utilisé toospecify des noms personnalisés pour les paramètres de requête et/ou d’en-tête contenant la clé d’abonnement hello. Lorsque cette propriété est présente, elle doit contenir au moins une des deux propriétés suivantes : hello.<br /><br /> `{   "subscriptionKeyParameterNames":   {     "query": “customQueryParameterName",     "header": “customHeaderParameterName"   } }`|  
  
##  <a name="APISummary"></a> API summary  
 Hello `API summary` entité a hello propriétés suivantes.  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|id|string|Identificateur de ressource. Identifie de façon unique les API hello au sein de l’instance de service de gestion des API actuelle hello. valeur de Hello est une URL relative valide au format hello de `apis/{id}` où `{id}` est un identificateur d’API. Cette propriété est en lecture seule.|  
|name|string|Nom de l’API de hello. Ne doit pas être vide. La longueur maximale est de 100 caractères.|  
|description|string|Description de l’API de hello. Ne doit pas être vide. Peut comporter des balises de mise en forme. La longueur maximale est de 1 000 caractères.|  
  
##  <a name="Application"></a> Application  
 Hello `application` entité a hello propriétés suivantes.  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|ID|string|Bonjour identificateur unique de l’application hello.|  
|Intitulé|string|titre de Hello de l’application hello.|  
|Description|string|description de Hello de l’application hello.|  
|Url|URI|Hello URI pour une application hello.|  
|Version|string|Informations de version pour l’application hello.|  
|Configuration requise|string|Description de la configuration requise pour l’application hello.|  
|State|number|état actuel de Hello de l’application hello.<br /><br /> - 0 - Inscrite<br /><br /> - 1 - Soumise<br /><br /> - 2 - Publiée<br /><br /> - 3 - Rejetée<br /><br /> - 4 - Non publiée|  
|RegistrationDate|DateTime|application de hello de date et d’heure Hello a été inscrite.|  
|CategoryId|number|catégorie Hello de l’application hello (Finance, loisirs, etc.).|  
|DeveloperId|string|Identificateur unique de Hello développeur hello soumis application hello.|  
|Pièces jointes|Collection d’entités [Attachment](#Attachment).|Les pièces jointes pour l’application hello tels que des captures d’écran ou des icônes.|  
|Icône|[Attachment](#Attachment)|hello d’icône Hello pour une application hello.|  
  
##  <a name="Attachment"></a> Attachment  
 Hello `attachment` entité a hello propriétés suivantes.  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|UniqueId|string|Identificateur unique de Hello pour la pièce jointe de hello.|  
|Url|string|Hello l’URL de ressource de hello.|  
|Type|string|type Hello de pièce jointe.|  
|ContentType|string|type de média Hello de pièce jointe de hello.|  
  
##  <a name="Sample"></a> Code sample  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|title|string|nom Hello d’opération de hello.|  
|snippet|string|Cette propriété est déconseillée et ne doit pas être utilisée.|  
|brush|string|Le code qui toobe de modèle utilisée pour afficher l’exemple de code hello de coloration de syntaxe. Les valeurs autorisées sont `plain`, `php`, `java`, `xml`, `objc`, `python`, `ruby` et `csharp`.|  
|template|string|nom de Hello de cet exemple de modèle de code.|  
|body|string|Un espace réservé pour une partie d’exemple de code hello d’extrait de code hello.|  
|method|string|Bonjour la méthode HTTP de l’opération de hello.|  
|scheme|string|Bonjour toouse de protocole pour la demande d’opération hello.|  
|path|string|chemin d’accès de Hello d’opération de hello.|  
|query|string|Exemple de chaîne de requête avec des paramètres définis.|  
|host|string|URL de Hello de passerelle de service de gestion des API hello pour hello API qui contient cette opération.|  
|headers|Collection d’entités [Header](#Header).|En-têtes de cette opération.|  
|parameters|Collection d’entités [Parameter](#Parameter).|Paramètres définis pour cette opération.|  
  
##  <a name="Comment"></a> Comment  
 Hello `API` entité a hello propriétés suivantes.  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|ID|number|id de Hello de commentaire de hello.|  
|CommentText|string|corps de Hello de commentaire de hello. Peut comporter du code HTML.|  
|DeveloperCompany|string|nom de la société Hello du développeur de hello.|  
|PostedOn|DateTime|commentaire de hello de date et d’heure Hello a été validé.|  
  
##  <a name="Issue"></a> Issue  
 Hello `issue` entité a hello propriétés suivantes.  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|ID|string|Identificateur unique de Hello pour problème de hello.|  
|ApiID|string|id de Hello pour API hello pour laquelle ce problème a été signalé.|  
|Intitulé|string|Titre du problème de hello.|  
|Description|string|Description du problème de hello.|  
|SubscriptionDeveloperName|string|Prénom du développeur hello hello problème signalé.|  
|IssueState|string|état actuel de Hello du problème de hello. Les valeurs possibles sont Proposed, Opened et Closed (Proposé, Ouvert et Fermé).|  
|ReportedOn|DateTime|problème de hello de date et d’heure Hello a été signalée.|  
|Commentaires|Collection d’entités [Comment](#Comment).|Commentaires sur ce problème.|  
|Pièces jointes|Collection d’entités [Attachment](api-management-template-data-model-reference.md#Attachment).|N’importe quel problème toohello de pièces jointes.|  
|Services|Collection d’entités [API](#API).|Hello API abonné utilisateur hello tooby que ce problème de hello.|  
  
##  <a name="Filtering"></a> Filtering  
 Hello `filtering` entité a hello propriétés suivantes.  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|Modèle|string|terme de recherche actuel Hello ; ou `null` s’il n’existe aucun critère de recherche.|  
|Placeholder|string|Bonjour toodisplay de texte dans la zone de recherche hello lorsqu’il n’existe aucun critère de recherche spécifié.|  
  
##  <a name="Header"></a> Header  
 Cette section décrit hello `parameter` représentation.  
  
|Propriété|Description|Type|  
|--------------|-----------------|----------|  
|name|string|Nom du paramètre.|  
|description|string|Description du paramètre.|  
|value|string|Valeur de l’en-tête.|  
|typeName|string|Type de données de la valeur d’en-tête.|  
|options|string|Options.|  
|required|booléenne|Indique si l’en-tête de hello est requis.|  
|readOnly|booléenne|Indique si les en-tête hello est en lecture seule.|  
  
##  <a name="HTTPRequest"></a> HTTP Request  
 Cette section décrit hello `request` représentation.  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|description|string|Description de la demande d’opération.|  
|En-têtes|tableau d’entités [Header](#Header).|En-têtes de demande.|  
|parameters|tableau de [Parameter](#Parameter)|Collection de paramètres de demande d’opération.|  
|representations|tableau de [Representation](#Representation)|Collection de représentations de demande d’opération.|  
  
##  <a name="HTTPResponse"></a> HTTP Response  
 Cette section décrit hello `response` représentation.  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|statusCode|entier positif|Code de statut de la réponse de l’opération.|  
|description|string|Description de la réponse de l’opération.|  
|representations|tableau de [Representation](#Representation)|Collection de représentations de la réponse de l’opération.|  
  
##  <a name="Operation"></a> Opération  
 Hello `operation` entité a hello propriétés suivantes.  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|id|string|Identificateur de ressource. Identifie l’opération hello au sein de l’instance de service de gestion des API actuelle hello. valeur de Hello est une URL relative valide au format hello de `apis/{aid}/operations/{id}` où `{aid}` est un identificateur d’API et `{id}` est un identificateur de l’opération. Cette propriété est en lecture seule.|  
|name|string|Nom de l’opération de hello. Ne doit pas être vide. La longueur maximale est de 100 caractères.|  
|description|string|Description de l’opération de hello. Ne doit pas être vide. Peut comporter des balises de mise en forme. La longueur maximale est de 1 000 caractères.|  
|scheme|string|Décrit dans quel hello protocoles opérations dans cette API peuvent être appelées. Les valeurs autorisées sont `http`, `https`, ou à la fois `http` et `https`.|  
|uriTemplate|string|Modèle d’URL relative identifiant la ressource cible de hello pour cette opération. Peut comporter des paramètres. Exemple : `customers/{cid}/orders/{oid}/?date={date}`|  
|host|string|Gestion des API Hello URL passerelle qui héberge les API hello.|  
|httpMethod|string|Méthode HTTP de l’opération.|  
|request|[Demande HTTP](#HTTPRequest)|Entité qui contient les détails de la demande.|  
|responses|tableau de [HTTP Response](#HTTPResponse)|Tableau d’entités [HTTP Response](#HTTPResponse) de l’opération.|  
  
##  <a name="Menu"></a> Operation menu  
 Hello `operation menu` entité a hello propriétés suivantes.  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|ApiId|string|id de Hello de hello des API actuelle.|  
|CurrentOperationId|string|id de Hello de l’opération en cours hello.|  
|Action|string|type de menu Hello.|  
|MenuItems|Collection d’entités [Operation menu item](#MenuItem).|opérations de Hello pour les API actuelle hello.|  
  
##  <a name="MenuItem"></a> Operation menu item  
 Hello `operation menu item` entité a hello propriétés suivantes.  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|ID|string|id de Hello d’opération de hello.|  
|Intitulé|string|description de Hello d’opération de hello.|  
|HttpMethod|string|Bonjour la méthode Http de l’opération de hello.|  
  
##  <a name="Paging"></a> Paging  
 Hello `paging` entité a hello propriétés suivantes.  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|Page|number|numéro de page actuel Hello.|  
|PageSize|number|Bonjour toobe nombre maximal de résultats affiché sur une seule page.|  
|TotalItemCount|number|nombre de Hello d’éléments à afficher.|  
|ShowAll|booléenne|Si toosho tous les résultats sur une seule page.|  
|PageCount|number|nombre de Hello de pages de résultats.|  
  
##  <a name="Parameter"></a> Parameter  
 Cette section décrit hello `parameter` représentation.  
  
|Propriété|Description|Type|  
|--------------|-----------------|----------|  
|name|string|Nom du paramètre.|  
|description|string|Description du paramètre.|  
|value|string|Valeur du paramètre.|  
|options|tableau de chaînes|Valeurs définies pour les valeurs du paramètre de requête.|  
|required|booléenne|Indique si le paramètre est obligatoire ou non.|  
|kind|number|Indique si ce paramètre est un paramètre de chemin d’accès (1) ou un paramètre de chaîne de requête (2).|  
|typeName|string|Type de paramètre.|  
  
##  <a name="Product"></a> Produit  
 Hello `product` entité a hello propriétés suivantes.  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|ID|string|Identificateur de ressource. Identifie le produit hello au sein de l’instance de service de gestion des API actuelle hello. valeur de Hello est une URL relative valide au format hello de `products/{pid}` où `{pid}` est un identificateur de produit. Cette propriété est en lecture seule.|  
|Intitulé|string|Nom du produit de hello. Ne doit pas être vide. La longueur maximale est de 100 caractères.|  
|Description|string|Description du produit de hello. Ne doit pas être vide. Peut comporter des balises de mise en forme. La longueur maximale est de 1 000 caractères.|  
|Termes|string|Conditions d’utilisation du produit. Les développeurs de la tentative de toosubscribe toohello produit seront affiche et nécessaire tooaccept ces termes avant de pouvoir effectuer les processus d’inscription hello.|  
|ProductState|number|Spécifie si le produit de hello est publié ou non. Les produits publiés sont détectables par les développeurs sur le portail des développeurs hello. Les produits non publiés sont visibles tooadministrators uniquement.<br /><br /> Hello les valeurs autorisées pour l’état du produit sont :<br /><br /> - `0 - Not Published`<br /><br /> - `1 - Published`<br /><br /> - `2 - Deleted`|  
|AllowMultipleSubscriptions|booléenne|Spécifie si un utilisateur peut avoir plusieurs produits de toothis d’abonnements à hello même temps.|  
|MultipleSubscriptionsCount|number|nombre de Hello du produit de toothis d’abonnements par utilisateur en cours de hello.|  
  
##  <a name="Provider"></a> Provider  
 Hello `provider` entité a hello propriétés suivantes.  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|Propriétés|dictionnaire de chaînes|Propriétés de ce fournisseur d’authentification.|  
|AuthenticationType|string|type de fournisseur Hello. (Azure Active Directory, compte Facebook, compte Google, compte Microsoft, Twitter).|  
|Caption|string|Nom complet du fournisseur de hello.|  
  
##  <a name="Representation"></a> Representation  
 Cette section décrit une `representation`.  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|contentType|string|Spécifie un type de contenu inscrit ou personnalisé pour cette représentation, par exemple, `application/xml`.|  
|sample|string|Un exemple de représentation sous forme de hello.|  
  
##  <a name="Subscription"></a> Subscription  
 Hello `subscription` entité a hello propriétés suivantes.  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|ID|string|Identificateur de ressource. Identifie l’abonnement hello au sein de l’instance de service de gestion des API actuelle hello. valeur de Hello est une URL relative valide au format hello de `subscriptions/{sid}` où `{sid}` est un identificateur d’abonnement. Cette propriété est en lecture seule.|  
|ProductId|string|identificateur de ressource Hello Hello abonné produit. valeur de Hello est une URL relative valide au format hello de `products/{pid}` où `{pid}` est un identificateur de produit.|  
|ProductTitle|string|Nom du produit de hello. Ne doit pas être vide. La longueur maximale est de 100 caractères.|  
|ProductDescription|string|Description du produit de hello. Ne doit pas être vide. Peut comporter des balises de mise en forme. La longueur maximale est de 1 000 caractères.|  
|ProductDetailsUrl|string|Détails du produit toohello URL relatives.|  
|state|string|état Hello d’abonnement de hello. Les états possibles sont :<br /><br /> - `0 - suspended`– hello abonnement est bloqué et l’abonné de hello ne peut pas appeler aucune API du produit de hello.<br /><br /> - `1 - active`– hello abonnement est actif.<br /><br /> - `2 - expired`– les abonnement hello a atteint sa date d’expiration et a été désactivé.<br /><br /> - `3 - submitted`– demande d’abonnement hello a été effectuée par le développeur de hello, mais pas encore approuvé ou rejeté.<br /><br /> - `4 - rejected`– demande d’abonnement hello a été refusée par un administrateur.<br /><br /> - `5 - cancelled`– les abonnement hello a été annulée par le développeur de hello ou un administrateur.|  
|DisplayName|string|Nom complet de l’abonnement de hello.|  
|CreatedDate|dateTime|abonnement hello Hello a été créé, au format ISO 8601 : `2014-06-24T16:25:00Z`.|  
|CanBeCancelled|booléenne|Indique si l’abonnement de hello peut être annulée par l’utilisateur actuel hello.|  
|IsAwaitingApproval|booléenne|Indique si les abonnement hello sont en attente d’approbation.|  
|StartDate|dateTime|Hello date de début de l’abonnement de hello, au format ISO 8601 : `2014-06-24T16:25:00Z`.|  
|ExpirationDate|dateTime|date d’expiration de Hello pour l’abonnement hello, au format ISO 8601 : `2014-06-24T16:25:00Z`.|  
|NotificationDate|dateTime|date de notification de Hello pour l’abonnement hello, au format ISO 8601 : `2014-06-24T16:25:00Z`.|  
|primaryKey|string|clé d’abonnement primaire Hello. La longueur maximale est de 256 caractères.|  
|secondaryKey|string|clé d’abonnement secondaire Hello. La longueur maximale est de 256 caractères.|  
|CanBeRenewed|booléenne|Indique si l’abonnement de hello peut être renouvelé par l’utilisateur actuel hello.|  
|HasExpired|booléenne|Si l’abonnement de hello a expiré.|  
|IsRejected|booléenne|Indique si la demande d’abonnement hello a été refusé.|  
|CancelUrl|string|Hello relatif Url toocancel hello abonnement.|  
|RenewUrl|string|Hello relatif Url toorenew hello abonnement.|  
  
##  <a name="SubscriptionSummary"></a> Subscription summary  
 Hello `subscription summary` entité a hello propriétés suivantes.  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|ID|string|Identificateur de ressource. Identifie l’abonnement hello au sein de l’instance de service de gestion des API actuelle hello. valeur de Hello est une URL relative valide au format hello de `subscriptions/{sid}` où `{sid}` est un identificateur d’abonnement. Cette propriété est en lecture seule.|  
|DisplayName|string|Hello affiche le nom de l’abonnement de hello|  
  
##  <a name="UserAccountInfo"></a> User account info  
 Hello `user account info` entité a hello propriétés suivantes.  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|FirstName|string|Prénom. Ne doit pas être vide. La longueur maximale est de 100 caractères.|  
|LastName|string|Nom. Ne doit pas être vide. La longueur maximale est de 100 caractères.|  
|Email|string|Adresse de messagerie. Ne doit pas être vide et doit être unique au sein de l’instance de service hello. La longueur maximale est de 254 caractères.|  
|Mot de passe|string|Mot de passe du compte d’utilisateur.|  
|NameIdentifier|string|Identifiant du compte, hello identique à l’adresse de messagerie hello utilisateur.|  
|ProviderName|string|Nom du fournisseur d’authentification.|  
|IsBasicAccount|booléenne|True si ce compte a été enregistré à l’aide de la messagerie et le mot de passe ; Si le compte de hello a été inscrite à l’aide d’un fournisseur de la valeur False.|  
  
##  <a name="UseSignIn"></a> User sign in  
 Hello `user sign in` entité a hello propriétés suivantes.  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|Email|string|Adresse de messagerie. Ne doit pas être vide et doit être unique au sein de l’instance de service hello. La longueur maximale est de 254 caractères.|  
|Mot de passe|string|Mot de passe du compte d’utilisateur.|  
|ReturnUrl|string|Hello l’URL de page hello où hello utilisateur a cliqué de connexion.|  
|RememberMe|booléenne|Si toosave hello les informations de l’utilisateur actuel.|  
|RegistrationEnabled|booléenne|Indique si l’inscription est activée.|  
|DelegationEnabled|booléenne|Indique si la connexion déléguée est activée.|  
|DelegationUrl|string|Hello déléguée signe dans l’url, s’il est activé.|  
|SsoSignUpUrl|string|Hello unique URL de connexion pour l’utilisateur de hello, le cas échéant.|  
|AuxServiceUrl|string|Si l’utilisateur actuel hello est un administrateur, il s’agit d’une instance de service de toohello lien Bonjour portail classique Azure.|  
|Fournisseurs|Collection d’entités [Provider](#Provider).|fournisseurs d’authentification Hello pour cet utilisateur.|  
|UserRegistrationTerms|string|Conditions auxquelles un utilisateur doit accepter toobefore l’ouverture de session.|  
|UserRegistrationTermsEnabled|booléenne|Indique si les conditions sont activées.|  
  
##  <a name="UserSignUp"></a> User sign up  
 Hello `user sign up` entité a hello propriétés suivantes.  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|PasswordConfirm|booléenne|Valeur utilisée par hello [inscription](api-management-page-controls.md#sign-up)d’abonnement à un contrôle.|  
|Mot de passe|string|Mot de passe du compte d’utilisateur.|  
|PasswordVerdictLevel|number|Valeur utilisée par hello [inscription](api-management-page-controls.md#sign-up)d’abonnement à un contrôle.|  
|UserRegistrationTerms|string|Conditions auxquelles un utilisateur doit accepter toobefore l’ouverture de session.|  
|UserRegistrationTermsOptions|number|Valeur utilisée par hello [inscription](api-management-page-controls.md#sign-up)d’abonnement à un contrôle.|  
|ConsentAccepted|booléenne|Valeur utilisée par hello [inscription](api-management-page-controls.md#sign-up)d’abonnement à un contrôle.|  
|Email|string|Adresse de messagerie. Ne doit pas être vide et doit être unique au sein de l’instance de service hello. La longueur maximale est de 254 caractères.|  
|FirstName|string|Prénom. Ne doit pas être vide. La longueur maximale est de 100 caractères.|  
|LastName|string|Nom. Ne doit pas être vide. La longueur maximale est de 100 caractères.|  
|UserData|string|Valeur utilisée par hello [inscription](api-management-page-controls.md#sign-up) contrôle.|  
|NameIdentifier|string|Valeur utilisée par hello [inscription](api-management-page-controls.md#sign-up)d’abonnement à un contrôle.|  
|ProviderName|string|Nom du fournisseur d’authentification.|

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur l’utilisation des modèles, consultez [comment toocustomize hello portail des développeurs gestion des API à l’aide de modèles](api-management-developer-portal-templates.md).
