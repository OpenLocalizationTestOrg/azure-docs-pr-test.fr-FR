---
title: "ressources de modèle de gestion des API aaaAzure | Documents Microsoft"
description: "En savoir plus sur les types de ressources disponibles pour une utilisation dans les modèles de portail de développement de gestion des API Azure hello."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 51a1b4c6-a9fd-4524-9e0e-03a9800c3e94
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 2221e3852986d485d13817b483e473dfe451d3c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-template-resources"></a>Ressources du modèle Gestion des API Azure
Gestion des API Azure fournit hello les types de ressources pour une utilisation dans les modèles de portail de développement hello suivants.  
  
-   [Ressources de chaînes](#strings)  
  
-   [Ressources de glyphes](#glyphs)  
  
##  <a name="strings"></a> Ressources de chaînes  
 Gestion des API fournit un ensemble complet de ressources de chaîne à utiliser dans le portail des développeurs hello. Ces ressources sont traduits dans toutes les langues hello pris en charge par la gestion des API. ensemble de modèles par défaut de Hello utilise ces ressources pour les en-têtes de page, les étiquettes et les chaînes constantes qui sont affichés dans le portail des développeurs hello. toouse une ressource de chaîne dans vos modèles, fournir préfixe de chaîne de ressource hello suivi par nom de chaîne hello, comme indiqué dans hello l’exemple suivant.  
  
```  
{% localized "Prefix|Name" %}  
  
```  
  
 Hello exemple suivant provient de modèle de liste de produits hello et affiche **produits** en hello haut hello.  
  
```  
<h2>{% localized "ProductsStrings|PageTitleProducts" %}</h2>  
  
```  
  
 Consultez toohello suivant des tables pour les ressources de chaîne hello disponibles pour une utilisation dans vos modèles de portail de développement. Utiliser le nom de la table hello en tant que préfixe de hello pour les ressources de chaîne hello dans cette table.  
  
-   [ApisStrings](#ApisStrings)  
  
-   [ApplicationListStrings](#ApplicationListStrings)  
  
-   [AppDetailsStrings](#AppDetailsStrings)  
  
-   [AppStrings](#AppStrings)  
  
-   [CommonResources](#CommonResources)  
  
-   [CommonStrings](#CommonStrings)  
  
-   [Documentation](#Documentation)  
  
-   [ErrorPageStrings](#ErrorPageStrings)  
  
-   [IssuesStrings](#IssuesStrings)  
  
-   [NotFoundStrings](#NotFoundStrings)  
  
-   [ProductDetailsStrings](#ProductDetailsStrings)  
  
-   [ProductsStrings](#ProductsStrings)  
  
-   [ProviderInfoStrings](#ProviderInfoStrings)  
  
-   [SigninResources](#SigninResources)  
  
-   [SigninStrings](#SigninStrings)  
  
-   [SignupStrings](#SignupStrings)  
  
-   [SubscriptionListStrings](#SubscriptionListStrings)  
  
-   [SubscriptionStrings](#SubscriptionStrings)  
  
-   [UpdateProfileStrings](#UpdateProfileStrings)  
  
-   [UserProfile](#UserProfile)  
  
###  <a name="ApisStrings"></a> ApisStrings  
  
|Nom|Texte|  
|----------|----------|  
|PageTitleApis|API|  
  
###  <a name="AppDetailsStrings"></a> AppDetailsStrings  
  
|Nom|Texte|  
|----------|----------|  
|WebApplicationsDetailsTitle|Aperçu de l’application.|  
|WebApplicationsRequirementsHeader|Configuration requise|  
|WebApplicationsScreenshotAlt|Capture d'écran|  
|WebApplicationsScreenshotsHeader|Captures d’écran.|  
  
###  <a name="ApplicationListStrings"></a> ApplicationListStrings  
  
|Nom|Texte|  
|----------|----------|  
|WebDevelopersAppDeleteConfirmation|Êtes-vous sûr de vouloir tooremove application ?|  
|WebDevelopersAppNotPublished|Non publié.|  
|WebDevelopersAppNotSubminted|Non soumis.|  
|WebDevelopersAppTableCategoryHeader|Catégorie|  
|WebDevelopersAppTableNameHeader|Nom|  
|WebDevelopersAppTableStateHeader|State|  
|WebDevelopersEditLink|Modifier|  
|WebDevelopersRegisterAppLink|Inscription de l’application|  
|WebDevelopersRemoveLink|Supprimer|  
|WebDevelopersSubmitLink|Submit|  
|WebDevelopersYourApplicationsHeader|Vos applications|  
  
###  <a name="AppStrings"></a> AppStrings  
  
|Nom|Texte|  
|----------|----------|  
|WebApplicationsHeader|Applications|  
  
###  <a name="CommonResources"></a> CommonResources  
  
|Nom|Texte|  
|----------|----------|  
|NoItemsToDisplay|Aucun résultat trouvé.|  
|GeneralExceptionMessage|Il y a un problème. Il peut s’agir d’un dysfonctionnement temporaire ou d’un bogue. Réessayez.|  
|GeneralJsonExceptionMessage|Il y a un problème. Il peut s’agir d’un dysfonctionnement temporaire ou d’un bogue. Veuillez recharger hello page, puis réessayez.|  
|ConfirmationMessageUnsavedChanges|Certaines modifications n’ont pas été enregistrées. Êtes-vous sûr que vous le souhaitez toocancel et ignorer les modifications de hello ?|  
|AzureActiveDirectory|Azure Active Directory|  
|HttpLargeRequestMessage|Le texte de la requête HTTP est trop long.|  
  
###  <a name="CommonStrings"></a> CommonStrings  
  
|Nom|Texte|  
|----------|----------|  
|ButtonLabelCancel|Annuler|  
|ButtonLabelSave|Enregistrer|  
|GeneralExceptionMessage|Il y a un problème. Il peut s’agir d’un dysfonctionnement temporaire ou d’un bogue. Réessayez.|  
|NoItemsToDisplay|Il n’y a aucune toodisplay d’éléments.|  
|PagerButtonLabelFirst|Premier|  
|PagerButtonLabelLast|Dernier|  
|PagerButtonLabelNext|Suivant|  
|PagerButtonLabelPrevious|Précédent|  
|PagerLabelPageNOfM|Page {0} sur {1\}|  
|PasswordTooShort|Hello mot de passe est trop court|  
|EmailAsPassword|N’utilisez pas votre adresse de messagerie comme mot de passe.|  
|PasswordSameAsUserName|Votre mot de passe ne peut pas contenir votre nom d’utilisateur.|  
|PasswordTwoCharacterClasses|Utilisez différentes classes de caractères.|  
|PasswordTooManyRepetitions|Trop de répétitions.|  
|PasswordSequenceFound|Votre mot de passe contient des séquences.|  
|PagerLabelPageSize|Taille de la page|  
|CurtainLabelLoading|Chargement en cours...|  
|TablePlaceholderNothingToDisplay|Aucune donnée de portée et de la période de hello sélectionné|  
|ButtonLabelClose|fermez|  
  
###  <a name="Documentation"></a> Documentation  
  
|Nom|Texte|  
|----------|----------|  
|WebDocumentationInvalidHeaderErrorMessage|En-tête non valide « {0} ».|  
|WebDocumentationInvalidRequestErrorMessage|URL de demande non valide.|  
|TextboxLabelAccessToken|Jeton d’accès *|  
|DropdownOptionPrimaryKeyFormat|Primaire-{0}|  
|DropdownOptionSecondaryKeyFormat|Secondaire-{0}|  
|WebDocumentationSubscriptionKeyText|Votre clé d’abonnement|  
|WebDocumentationTemplatesAddHeaders|Ajoutez les en-têtes HTTP requis.|  
|WebDocumentationTemplatesBasicAuthSample|Exemple d’autorisation de base|  
|WebDocumentationTemplatesCurlForBasicAuth|Pour une autorisation de base, utilisez : --user {nom_utilisateur}:{mot_de_passe}.|  
|WebDocumentationTemplatesCurlValuesForPath|Fournissez des valeurs aux paramètres de chemin d’accès (indiqués entre {...}), à votre clé d’abonnement et aux paramètres de requête.|  
|WebDocumentationTemplatesDeveloperKey|Spécifiez votre clé d’abonnement.|  
|WebDocumentationTemplatesJavaApache|Cet exemple utilise le client d’Apache HTTP hello à partir des composants de HTTP (http://hc.apache.org/httpcomponents-client-ga/)|  
|WebDocumentationTemplatesOptionalParams|Fournissez des valeurs aux paramètres facultatifs, en fonction des besoins.|  
|WebDocumentationTemplatesPhpPackage|Cet exemple utilise le package de hello HTTP_Request2. (Pour plus d’informations : http://pear.php.net/package/HTTP_Request2)|  
|WebDocumentationTemplatesPythonValuesForPath|Fournissez des valeurs aux paramètres de chemin d’accès (indiqués entre {...}) et au corps de la demande si nécessaire.|  
|WebDocumentationTemplatesRequestBody|Spécifiez le corps de la demande.|  
|WebDocumentationTemplatesRequiredParams|Spécifier des valeurs pour hello suivant les paramètres requis|  
|WebDocumentationTemplatesValuesForPath|Donnez des valeurs aux paramètres de chemin d’accès (indiqués entre {...}).|  
|OAuth2AuthorizationEndpointDescription|point de terminaison d’autorisation Hello est toointeract utilisé avec le propriétaire de la ressource hello et obtenir un octroi d’autorisation.|  
|OAuth2AuthorizationEndpointName|Point de terminaison d’autorisation|  
|OAuth2TokenEndpointDescription|sert de point de terminaison token Hello en hello client tooobtain un jeton d’accès à l’aide de son autorisation d’accorder ou de jeton d’actualisation.|  
|OAuth2TokenEndpointName|Point de terminaison de jeton|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_Description|< p\> client de hello lance le flux de hello en dirigeant le point de terminaison d’autorisation du propriétaire des ressources hello agent utilisateur toohello.  client de Hello inclut son identificateur de client, étendue demandée, d’état local, un serveur d’autorisation de la redirection des URI toowhich hello est envoyé de l’agent utilisateur hello une fois que l’accès est accordé (ou refusé).     < /p\> < p\> authentifie le propriétaire de la ressource hello (via l’agent utilisateur du hello) de serveur d’autorisation de hello et établit si le propriétaire de la ressource hello accorde ou refuse la demande d’accès du client hello.     < /p\> < p\> en supposant que le propriétaire de la ressource hello accorde l’accès, le serveur d’autorisation de hello redirige client de toohello arrière de l’agent utilisateur hello à l’aide de la redirection de hello URI fourni plus haut (dans la demande hello ou au cours du client inscription de t).  URI de redirection Hello inclut un code d’autorisation et n’importe quel état local fourni par le client de hello précédemment.     </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_ErrorDescription|< p\> si l’utilisateur de hello refuse la demande d’accès hello de si la demande de hello n’est pas valide, les clients hello seront informés à l’aide de hello ajoutés sur toohello redirection des paramètres suivants : < /p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_Name|Demande d’autorisation.|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_RequestDescription|< p\> hello client application doit envoyer le point de terminaison d’autorisation hello utilisateur toohello Bonjour de tooinitiate commande processus OAuth.          Au point de terminaison d’autorisation hello, utilisateur de hello authentifie et accorde ou refuse l’accès toohello application.     </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_ResponseDescription|< p\> en supposant que le propriétaire de la ressource hello accorde l’accès, le serveur d’autorisation redirige client de toohello arrière de l’agent utilisateur hello à l’aide de la redirection de hello URI fourni plus haut (dans la demande hello ou lors de l’inscription du client).  URI de redirection Hello inclut un code d’autorisation et n’importe quel état local fourni par le client de hello précédemment. </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_TokenRequest_Description|< p\> hello client demande un jeton d’accès serveur d’autorisation de hello « point de terminaison token s en incluant le code d’autorisation hello à l’étape précédente de hello.  Lors de la demande de hello, client de hello s’authentifie avec un serveur d’autorisation de hello.  client de Hello inclut hello URI utilisé tooobtain hello d’autorisation le code de redirection pour la vérification. < /p\> < p\> serveur d’autorisation de hello authentifie hello client, valide le code d’autorisation de hello et garantit que la redirection de hello URI reçus correspondances hello URI utilisé tooredirect hello client à l’étape (C).  S’il est valide, hello d’autorisation répond avec un jeton d’accès et, éventuellement, un jeton d’actualisation. </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_TokenRequest_ErrorDescription|< p\> si l’authentification du client hello demande a échoué ou n’est pas valide, serveur d’autorisation de hello répond avec un code d’état HTTP 400 (demande incorrecte) (sauf mention contraire) et inclut hello paramètres avec la réponse de hello suivants. </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_TokenRequest_RequestDescription|< p\> client de hello rend un point de terminaison demande toohello jeton en envoyant hello hello « application/x--www-form-urlencoded » au format utilisant un codage de caractères UTF-8 dans le corps d’entité hello HTTP demande des paramètres suivants. </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_TokenRequest_ResponseDescription|< p\> serveur d’autorisation de hello émet un jeton d’accès et un jeton d’actualisation facultatif et constructions hello réponse en ajoutant hello suivant paramètres toohello corps d’entité de réponse hello HTTP avec un code d’état du 200 (OK). </p\>|  
|OAuth2Flow_ClientCredentialsGrant_Step_TokenRequest_Description|< p\> hello s’authentifie avec un serveur d’autorisation de hello et demande un jeton d’accès à partir du point de terminaison token hello. < /p\> < p\> serveur d’autorisation de hello authentifie hello client et si elle est valide, émet un jeton d’accès. </p\>|  
|OAuth2Flow_ClientCredentialsGrant_Step_TokenRequest_ErrorDescription|< p\> si la demande de hello l’authentification du client a échoué ou n’est pas valide serveur d’autorisation de hello répond avec un code d’état HTTP 400 (demande incorrecte) (sauf mention contraire) et inclut hello paramètres avec la réponse de hello suivants. </p\>|  
|OAuth2Flow_ClientCredentialsGrant_Step_TokenRequest_RequestDescription|< p\> client de hello rend un point de terminaison demande toohello jeton en ajoutant hello hello « application/x--www-form-urlencoded » au format utilisant un codage de caractères UTF-8 dans le corps d’entité hello HTTP demande des paramètres suivants. </p\>|  
|OAuth2Flow_ClientCredentialsGrant_Step_TokenRequest_ResponseDescription|< p\> si demande de jeton d’accès hello est valide et autorisés, serveur d’autorisation de hello émet un jeton d’accès et un jeton d’actualisation facultatif et constructions hello réponse en ajoutant hello suivant paramètres toohello corps d’entité de hello HTTP réponse avec un code d’état du 200 (OK). </p\>|  
|OAuth2Flow_ImplicitGrant_Step_AuthorizationRequest_Description|< p\> client de hello lance le flux de hello en dirigeant le propriétaire de la ressource hello'' s agent utilisateur toohello point de terminaison.  client de Hello inclut son identificateur de client, étendue demandée, d’état local, un serveur d’autorisation de la redirection des URI toowhich hello est envoyé de l’agent utilisateur hello une fois que l’accès est accordé (ou refusé). < /p\> < p\> serveur d’autorisation de hello authentifie le propriétaire de la ressource hello (via l’agent utilisateur du hello) et établit si le propriétaire de la ressource hello accorde ou refuse les client hello'' demande d’accès s. < /p\> < p\> en supposant que le propriétaire de la ressource hello accorde l’accès, le serveur d’autorisation de hello redirige client de toohello arrière de l’agent utilisateur hello à l’aide de la redirection hello URI fourni précédemment.  URI de redirection Hello inclut un jeton d’accès hello dans un fragment d’URI hello. </p\>|  
|OAuth2Flow_ImplicitGrant_Step_AuthorizationRequest_ErrorDescription|< p\> Si propriétaire de la ressource hello refuse la demande d’accès hello ou si la demande de hello échoue pour des raisons autres qu’un URI de redirection manquant ou non valide, serveur d’autorisation de hello informe client hello en ajoutant hello suivant paramètres toohello fragme composant NT d’à l’aide des URI de redirection hello hello format « application/x--www-form-urlencoded ». </p\>|  
|OAuth2Flow_ImplicitGrant_Step_AuthorizationRequest_RequestDescription|< p\> hello client application doit envoyer le point de terminaison d’autorisation hello utilisateur toohello Bonjour de tooinitiate commande processus OAuth.      Au point de terminaison d’autorisation hello, utilisateur de hello authentifie et accorde ou refuse l’accès toohello application. </p\>|  
|OAuth2Flow_ImplicitGrant_Step_AuthorizationRequest_ResponseDescription|< p\> si le propriétaire de la ressource hello accorde la demande d’accès hello, serveur d’autorisation de hello émet un jeton d’accès, puis les remet toohello client en ajoutant hello paramètres toohello fragment composant de l’URI de redirection hello suivant à l’aide de hello « un format de pplication/x--www-form-urlencoded ». </p\>|  
|OAuth2Flow_ObtainAuthorization_AuthorizationCodeGrant_Description|Flux de code d’autorisation est optimisé pour les clients permettant de maintenir la confidentialité de hello de leurs informations d’identification (par exemple, applications serveur web implémentées à l’aide de PHP, Java, Python, Ruby, ASP.NET, etc..).|  
|OAuth2Flow_ObtainAuthorization_AuthorizationCodeGrant_Name|Octroi du code d’autorisation.|  
|OAuth2Flow_ObtainAuthorization_ClientCredentialsGrant_Description|Flux d’informations d’identification de client convient dans les cas où le client hello (votre application) demande accéder aux ressources de toohello protégé sous son contrôle. client de Hello est considéré comme un propriétaire de la ressource, par conséquent, aucune intervention de l’utilisateur final n’est requise.|  
|OAuth2Flow_ObtainAuthorization_ClientCredentialsGrant_Name|Octroi des identifiants du client.|  
|OAuth2Flow_ObtainAuthorization_ImplicitGrant_Description|Flux implicite est optimisé pour les clients non compatibles avec maintien de confidentialité hello de leur toooperate de connus d’informations d’identification une URI de redirection particulier. Ces clients sont généralement implémentés dans un navigateur avec un langage de script comme JavaScript.|  
|OAuth2Flow_ObtainAuthorization_ImplicitGrant_Name|Octroi implicite.|  
|OAuth2Flow_ObtainAuthorization_ResourceOwnerPasswordCredentialsGrant_Description|Flux d’informations d’identification ressources propriétaire du mot de passe est approprié dans le cas où le propriétaire de la ressource hello une relation d’approbation avec le client hello (votre application), tels que des systèmes d’exploitation hello ou d’une application disposant de privilèges élevés. Ce flux est adapté aux clients capables d’obtenir des informations d’identification du propriétaire des ressources hello (nom d’utilisateur et mot de passe, généralement à l’aide d’un formulaire interactif).|  
|OAuth2Flow_ObtainAuthorization_ResourceOwnerPasswordCredentialsGrant_Name|Octroi des informations de mot de passe du propriétaire de la ressource.|  
|OAuth2Flow_ResourceOwnerPasswordCredentialsGrant_Step_TokenRequest_Description|< p\> propriétaire de la ressource hello fournit hello son nom d’utilisateur et un mot de passe. < /p\> < p\> hello client demande un jeton d’accès serveur d’autorisation de hello « point de terminaison token s en incluant les informations d’identification hello provenance du propriétaire de la ressource hello.  Lors de la demande de hello, client de hello s’authentifie avec un serveur d’autorisation de hello. < /p\> < p\> serveur d’autorisation de hello authentifie hello client et valide les informations d’identification de propriétaire de ressource hello et s’il est valide, émet un jeton d’accès. </p\>|  
|OAuth2Flow_ResourceOwnerPasswordCredentialsGrant_Step_TokenRequest_ErrorDescription|< p\> si la demande de hello l’authentification du client a échoué ou n’est pas valide serveur d’autorisation de hello répond avec un code d’état HTTP 400 (demande incorrecte) (sauf mention contraire) et inclut hello paramètres avec la réponse de hello suivants. </p\>|  
|OAuth2Flow_ResourceOwnerPasswordCredentialsGrant_Step_TokenRequest_RequestDescription|< p\> client de hello rend un point de terminaison demande toohello jeton en ajoutant hello hello « application/x--www-form-urlencoded » au format utilisant un codage de caractères UTF-8 dans le corps d’entité hello HTTP demande des paramètres suivants. </p\>|  
|OAuth2Flow_ResourceOwnerPasswordCredentialsGrant_Step_TokenRequest_ResponseDescription|< p\> si demande de jeton d’accès hello est valide et autorisés, serveur d’autorisation de hello émet un jeton d’accès et un jeton d’actualisation facultatif et constructions hello réponse en ajoutant hello suivant paramètres toohello corps d’entité de hello HTTP respo NSE avec un code d’état du 200 (OK). </p\>|  
|OAuth2Step_AccessTokenRequest_Name|Demande de jeton d’accès.|  
|OAuth2Step_AuthorizationRequest_Name|Demande d’autorisation.|  
|OAuth2AccessToken_AuthorizationCodeGrant_TokenResponse|OBLIGATOIRE. jeton d’accès Hello émis par le serveur d’autorisation de hello.|  
|OAuth2AccessToken_ClientCredentialsGrant_TokenResponse|OBLIGATOIRE. jeton d’accès Hello émis par le serveur d’autorisation de hello.|  
|OAuth2AccessToken_ImplicitGrant_AuthorizationResponse|OBLIGATOIRE. jeton d’accès Hello émis par le serveur d’autorisation de hello.|  
|OAuth2AccessToken_ResourceOwnerPasswordCredentialsGrant_TokenResponse|OBLIGATOIRE. jeton d’accès Hello émis par le serveur d’autorisation de hello.|  
|OAuth2ClientId_AuthorizationCodeGrant_AuthorizationRequest|OBLIGATOIRE. Identificateur client.|  
|OAuth2ClientId_AuthorizationCodeGrant_TokenRequest|REQUIS si le client de hello n’authentifie pas avec le serveur d’autorisation de hello.|  
|OAuth2ClientId_ImplicitGrant_AuthorizationRequest|OBLIGATOIRE. Identificateur du client Hello.|  
|OAuth2Code_AuthorizationCodeGrant_AuthorizationResponse|OBLIGATOIRE. code d’autorisation Hello généré par le serveur d’autorisation de hello.|  
|OAuth2Code_AuthorizationCodeGrant_TokenRequest|OBLIGATOIRE. code d’autorisation Hello provenant du serveur d’autorisation de hello.|  
|OAuth2ErrorDescription_AuthorizationCodeGrant_AuthorizationErrorResponse|FACULTATIF. Texte ASCII lisible fournissant des informations supplémentaires.|  
|OAuth2ErrorDescription_AuthorizationCodeGrant_TokenErrorResponse|FACULTATIF. Texte ASCII lisible fournissant des informations supplémentaires.|  
|OAuth2ErrorDescription_ClientCredentialsGrant_TokenErrorResponse|FACULTATIF. Texte ASCII lisible fournissant des informations supplémentaires.|  
|OAuth2ErrorDescription_ImplicitGrant_AuthorizationErrorResponse|FACULTATIF. Texte ASCII lisible fournissant des informations supplémentaires.|  
|OAuth2ErrorDescription_ResourceOwnerPasswordCredentialsGrant_TokenErrorResponse|FACULTATIF. Texte ASCII lisible fournissant des informations supplémentaires.|  
|OAuth2ErrorUri_AuthorizationCodeGrant_AuthorizationErrorResponse|FACULTATIF. URI identifiant une page web contrôlable de visu avec des informations sur l’erreur de hello.|  
|OAuth2ErrorUri_AuthorizationCodeGrant_TokenErrorResponse|FACULTATIF. URI identifiant une page web contrôlable de visu avec des informations sur l’erreur de hello.|  
|OAuth2ErrorUri_ClientCredentialsGrant_TokenErrorResponse|FACULTATIF. URI identifiant une page web contrôlable de visu avec des informations sur l’erreur de hello.|  
|OAuth2ErrorUri_ImplicitGrant_AuthorizationErrorResponse|FACULTATIF. URI identifiant une page web contrôlable de visu avec des informations sur l’erreur de hello.|  
|OAuth2ErrorUri_ResourceOwnerPasswordCredentialsGrant_TokenErrorResponse|FACULTATIF. URI identifiant une page web contrôlable de visu avec des informations sur l’erreur de hello.|  
|OAuth2Error_AuthorizationCodeGrant_AuthorizationErrorResponse|OBLIGATOIRE. Un code d’erreur ASCII unique depuis hello : invalid_request, unauthorized_client, access_denied, unsupported_response_type, invalid_scope, server_error, temporarily_unavailable.|  
|OAuth2Error_AuthorizationCodeGrant_TokenErrorResponse|OBLIGATOIRE. Un code d’erreur ASCII unique depuis hello : invalid_request, invalid_client, invalid_grant, unauthorized_client, unsupported_grant_type, invalid_scope.|  
|OAuth2Error_ClientCredentialsGrant_TokenErrorResponse|OBLIGATOIRE. Un code d’erreur ASCII unique depuis hello : invalid_request, invalid_client, invalid_grant, unauthorized_client, unsupported_grant_type, invalid_scope.|  
|OAuth2Error_ImplicitGrant_AuthorizationErrorResponse|OBLIGATOIRE. Un code d’erreur ASCII unique depuis hello : invalid_request, unauthorized_client, access_denied, unsupported_response_type, invalid_scope, server_error, temporarily_unavailable.|  
|OAuth2Error_ResourceOwnerPasswordCredentialsGrant_TokenErrorResponse|OBLIGATOIRE. Un code d’erreur ASCII unique depuis hello : invalid_request, invalid_client, invalid_grant, unauthorized_client, unsupported_grant_type, invalid_scope.|  
|OAuth2ExpiresIn_AuthorizationCodeGrant_TokenResponse|RECOMMANDÉ. durée de vie Hello en secondes du jeton d’accès hello.|  
|OAuth2ExpiresIn_ClientCredentialsGrant_TokenResponse|RECOMMANDÉ. durée de vie Hello en secondes du jeton d’accès hello.|  
|OAuth2ExpiresIn_ImplicitGrant_AuthorizationResponse|RECOMMANDÉ. durée de vie Hello en secondes du jeton d’accès hello.|  
|OAuth2ExpiresIn_ResourceOwnerPasswordCredentialsGrant_TokenResponse|RECOMMANDÉ. durée de vie Hello en secondes du jeton d’accès hello.|  
|OAuth2GrantType_AuthorizationCodeGrant_TokenRequest|OBLIGATOIRE. DOIT avoir la valeur trop « authorization_code ».|  
|OAuth2GrantType_ClientCredentialsGrant_TokenRequest|OBLIGATOIRE. DOIT avoir la valeur trop valeur « client_credentials ».|  
|OAuth2GrantType_ResourceOwnerPasswordCredentialsGrant_TokenRequest|OBLIGATOIRE. DOIT avoir la valeur trop « password ».|  
|OAuth2Password_ResourceOwnerPasswordCredentialsGrant_TokenRequest|OBLIGATOIRE. mot de passe du propriétaire de ressource Hello.|  
|OAuth2RedirectUri_AuthorizationCodeGrant_AuthorizationRequest|FACULTATIF. point de terminaison de redirection Hello URI doit être un URI absolu.|  
|OAuth2RedirectUri_AuthorizationCodeGrant_TokenRequest|OBLIGATOIRE si paramètre « redirect_uri » de hello a été inclus dans la demande d’autorisation de hello et leurs valeurs doivent être identiques.|  
|OAuth2RedirectUri_ImplicitGrant_AuthorizationRequest|FACULTATIF. point de terminaison de redirection Hello URI doit être un URI absolu.|  
|OAuth2RefreshToken_AuthorizationCodeGrant_TokenResponse|FACULTATIF. jeton d’actualisation Hello, qui peut être utilisé tooobtain nouveaux jetons d’accès.|  
|OAuth2RefreshToken_ClientCredentialsGrant_TokenResponse|FACULTATIF. jeton d’actualisation Hello, qui peut être utilisé tooobtain nouveaux jetons d’accès.|  
|OAuth2RefreshToken_ResourceOwnerPasswordCredentialsGrant_TokenResponse|FACULTATIF. jeton d’actualisation Hello, qui peut être utilisé tooobtain nouveaux jetons d’accès.|  
|OAuth2ResponseType_AuthorizationCodeGrant_AuthorizationRequest|OBLIGATOIRE. DOIT avoir la valeur trop « code ».|  
|OAuth2ResponseType_ImplicitGrant_AuthorizationRequest|OBLIGATOIRE. Valeur doit être définie trop « token ».|  
|OAuth2Scope_AuthorizationCodeGrant_AuthorizationRequest|FACULTATIF. étendue Hello de demande d’accès hello.|  
|OAuth2Scope_AuthorizationCodeGrant_TokenResponse|FACULTATIF si toohello identiques étendue demandée par le client de hello ; dans le cas contraire, il est nécessaire.|  
|OAuth2Scope_ClientCredentialsGrant_TokenRequest|FACULTATIF. étendue Hello de demande d’accès hello.|  
|OAuth2Scope_ClientCredentialsGrant_TokenResponse|FACULTATIF, si elles sont identiques toohello étendue demandée par le client de hello ; dans le cas contraire, il est nécessaire.|  
|OAuth2Scope_ImplicitGrant_AuthorizationRequest|FACULTATIF. étendue Hello de demande d’accès hello.|  
|OAuth2Scope_ImplicitGrant_AuthorizationResponse|FACULTATIF si toohello identiques étendue demandée par le client de hello ; dans le cas contraire, il est nécessaire.|  
|OAuth2Scope_ResourceOwnerPasswordCredentialsGrant_TokenRequest|FACULTATIF. étendue Hello de demande d’accès hello.|  
|OAuth2Scope_ResourceOwnerPasswordCredentialsGrant_TokenResponse|FACULTATIF, si elles sont identiques toohello étendue demandée par le client de hello ; dans le cas contraire, il est nécessaire.|  
|OAuth2State_AuthorizationCodeGrant_AuthorizationErrorResponse|REQUIS si le paramètre « state » de hello était présent dans la demande d’autorisation du client hello.  valeur exacte de Hello provenant du client de hello.|  
|OAuth2State_AuthorizationCodeGrant_AuthorizationRequest|RECOMMANDÉ. Valeur opaque hello client toomaintain état entre la demande de hello et le rappel.  serveur d’autorisation de Hello inclut cette valeur lors de la redirection du client de toohello arrière de l’agent utilisateur hello.  paramètre de Hello doit être utilisé pour empêcher la falsification de requête.|  
|OAuth2State_AuthorizationCodeGrant_AuthorizationResponse|REQUIS si le paramètre « state » de hello était présent dans la demande d’autorisation du client hello.  valeur exacte de Hello provenant du client de hello.|  
|OAuth2State_ImplicitGrant_AuthorizationErrorResponse|REQUIS si le paramètre « state » de hello était présent dans la demande d’autorisation du client hello.  valeur exacte de Hello provenant du client de hello.|  
|OAuth2State_ImplicitGrant_AuthorizationRequest|RECOMMANDÉ. Valeur opaque hello client toomaintain état entre la demande de hello et le rappel.  serveur d’autorisation de Hello inclut cette valeur lors de la redirection du client de toohello arrière de l’agent utilisateur hello.  paramètre de Hello doit être utilisé pour empêcher la falsification de requête.|  
|OAuth2State_ImplicitGrant_AuthorizationResponse|REQUIS si le paramètre « state » de hello était présent dans la demande d’autorisation du client hello.  valeur exacte de Hello provenant du client de hello.|  
|OAuth2TokenType_AuthorizationCodeGrant_TokenResponse|OBLIGATOIRE. type de Hello du jeton hello émis.|  
|OAuth2TokenType_ClientCredentialsGrant_TokenResponse|OBLIGATOIRE. type de Hello du jeton hello émis.|  
|OAuth2TokenType_ImplicitGrant_AuthorizationResponse|OBLIGATOIRE. type de Hello du jeton hello émis.|  
|OAuth2TokenType_ResourceOwnerPasswordCredentialsGrant_TokenResponse|OBLIGATOIRE. type de Hello du jeton hello émis.|  
|OAuth2UserName_ResourceOwnerPasswordCredentialsGrant_TokenRequest|OBLIGATOIRE. nom d’utilisateur du propriétaire de ressource de Hello.|  
|OAuth2UnsupportedTokenType|Le type de jeton « {0} » n’est pas pris en charge.|  
|OAuth2InvalidState|Réponse non valide du serveur d’autorisation.|  
|OAuth2GrantType_AuthorizationCode|Code d’autorisation.|  
|OAuth2GrantType_Implicit|Implicite.|  
|OAuth2GrantType_ClientCredentials|Informations d'identification du client|  
|OAuth2GrantType_ResourceOwnerPassword|Mot de passe de propriétaire de la ressource.|  
|WebDocumentation302Code|302 Trouvé.|  
|WebDocumentation400Code|400 (Demande incorrecte).|  
|OAuth2SendingMethod_AuthHeader|En-tête d’autorisation.|  
|OAuth2SendingMethod_QueryParam|Paramètre de requête.|  
|OAuth2AuthorizationServerGeneralException|Une erreur s’est produite lors de l’autorisation d’accès par {0}.|  
|OAuth2AuthorizationServerCommunicationException|Un serveur de tooauthorization de connexion HTTP n’a pas pu être établi ou a été fermé de façon inattendue.|  
|WebDocumentationOAuth2GeneralErrorMessage|Une erreur inattendue s’est produite.|  
|AuthorizationServerCommunicationException|Une exception de communication du serveur d’autorisation s’est produite. Contactez l’administrateur.|  
|TextblockSubscriptionKeyHeaderDescription|Clé d’abonnement qui fournit l’accès toothis API. Trouvée dans votre <a href='/developer'\>profil</a\>.|  
|TextblockOAuthHeaderDescription|Jeton d’accès OAuth 2.0 obtenu à partir de <i\>{0}</i\>. Types d’octrois pris en charge : <i\>{1}</i\>.|  
|TextblockContentTypeHeaderDescription|Type de média du corps hello envoyé toohello API.|  
|ErrorMessageApiNotAccessible|Hello API que vous essayez de toocall n’est pas accessible pour l’instant. Veuillez contacter le serveur de publication hello API < un href = « / émet »\>ici < /a\>.|  
|ErrorMessageApiTimedout|Hello API que vous essayez de toocall prend plu de réponse de tooget normal précédent. Veuillez contacter le serveur de publication hello API < un href = « / émet »\>ici < /a\>.|  
|BadRequestParameterExpected|« Le paramètre "{0}" est attendu. »|  
|TooltipTextDoubleClickToSelectAll|Double-cliquez sur tooselect tous.|  
|TooltipTextHideRevealSecret|Afficher/masquer|  
|ButtonLinkOpenConsole|Essayer|  
|SectionHeadingRequestBody|Corps de la demande|  
|SectionHeadingRequestParameters|Paramètres de la demande|  
|SectionHeadingRequestUrl|URL de la demande|  
|SectionHeadingResponse|Réponse|  
|SectionHeadingRequestHeaders|En-têtes de requête|  
|FormLabelSubtextOptional|facultatif|  
|SectionHeadingCodeSamples|Exemples de code|  
|TextblockOpenidConnectHeaderDescription|Jeton d’ID OpenID Connect obtenu à partir de <i\>{0}</i\>. Types d’octrois pris en charge : <i\>{1}</i\>.|  
  
###  <a name="ErrorPageStrings"></a> ErrorPageStrings  
  
|Nom|Texte|  
|----------|----------|  
|LinkLabelBack|Retour|  
|LinkLabelHomePage|page d'accueil|  
|LinkLabelSendUsEmail|Envoyez-nous un e-mail.|  
|PageTitleError|Désolé, il est une page demandée de problème à servir hello|  
|TextblockPotentialCauseIntermittentIssue|Il peut s’agir d’un problème intermittent d’accès aux données qui a déjà disparu.|  
|TextblockPotentialCauseOldLink|lien Hello que vous avez cliqué sur est peut-être ancien et pas point toohello corriger emplacement plus.|  
|TextblockPotentialCauseTechnicalProblem|Un problème technique a pu se produire de notre côté.|  
|TextblockPotentialSolutionRefresh|Essayez d’actualiser la page de hello.|  
|TextblockPotentialSolutionStartOver|Recommencez à partir de notre {0}.|  
|TextblockPotentialSolutionTryAgain|Accédez de {0} et recommencez l’action hello effectuée à nouveau.|  
|TextReportProblem|{0} décrivant la cause du problème ; nous nous en occuperons dès que possible.|  
|TitlePotentialCause|Cause potentielle.|  
|TitlePotentialSolution|Il n’est peut-être seulement un problème temporaire, quelques opérations tootry|  
  
###  <a name="IssuesStrings"></a> IssuesStrings  
  
|Nom|Texte|  
|----------|----------|  
|WebIssuesIndexTitle|Problèmes|  
|WebIssuesNoActiveSubscriptions|Vous ne disposez d’aucun abonnement actif. Vous devez toosubscribe pour un tooreport produit un problème.|  
|WebIssuesNotSignin|Vous n’êtes pas connecté. Veuillez {0} tooreport un problème ou publier un commentaire.|  
|WebIssuesReportIssueButton|Signaler un problème|  
|WebIssuesSignIn|se connecter|  
|WebIssuesStatusReportedBy|État: {0} &#124; Signalé par {1}.|  
  
###  <a name="NotFoundStrings"></a> NotFoundStrings  
  
|Nom|Texte|  
|----------|----------|  
|LinkLabelHomePage|page d'accueil|  
|LinkLabelSendUsEmail|Envoyez-nous un e-mail.|  
|PageTitleNotFound|Nous sommes désolés, nous ne trouvons page hello que vous recherchez|  
|TextblockPotentialCauseMisspelledUrl|Vous avez peut-être mal orthographié hello URL si vous l’avez tapée.|  
|TextblockPotentialCauseOldLink|lien Hello que vous avez cliqué sur est peut-être ancien et pas point toohello corriger emplacement plus.|  
|TextblockPotentialSolutionRetype|Essayez de retaper hello URL.|  
|TextblockPotentialSolutionStartOver|Recommencez à partir de notre {0}.|  
|TextReportProblem|{0} décrivant la cause du problème ; nous nous en occuperons dès que possible.|  
|TitlePotentialCause|Cause potentielle.|  
|TitlePotentialSolution|Solution potentielle.|  
  
###  <a name="ProductDetailsStrings"></a> ProductDetailsStrings  
  
|Nom|Texte|  
|----------|----------|  
|WebProductsAgreement|En vous abonnant trop {0} produit, j’accepte toohello `<a data-toggle='modal' href='#legal-terms'\>Terms of Use</a\>`.|  
|WebProductsLegalTermsLink|Conditions d’utilisation|  
|WebProductsSubscribeButton|S'abonner|  
|WebProductsUsageLimitsHeader|Limites d’utilisation|  
|WebProductsYouAreNotSubscribed|Vous êtes abonné toothis produit.|  
|WebProductsYouRequestedSubscription|Vous avez demandé de produit de toothis d’abonnement.|  
|ErrorYouNeedtoAgreeWithLegalTerms|Vous devez accepter les conditions d’utilisation de toohello avant de pouvoir continuer.|  
|ButtonLabelAddSubscription|Ajouter un abonnement|  
|LinkLabelChangeSubscriptionName|Modifier|  
|ButtonLabelConfirm|Confirmer|  
|TextblockMultipleSubscriptionsCount|Vous avez produit de toothis abonnements {0} :|  
|TextblockSingleSubscriptionsCount|Vous avez produit de toothis abonnement de {0} :|  
|TextblockSingleApisCount|Ce produit contient {0} API :|  
|TextblockMultipleApisCount|Ce produit contient {0} API :|  
|TextblockHeaderSubscribe|S’abonner tooproduct|  
|TextblockSubscriptionDescription|Un nouvel abonnement sera créé ainsi :|  
|TextblockSubscriptionLimitReached|Limite d’abonnements atteinte.|  
  
###  <a name="ProductsStrings"></a> ProductsStrings  
  
|Nom|Texte|  
|----------|----------|  
|PageTitleProducts|Produits|  
  
###  <a name="ProviderInfoStrings"></a> ProviderInfoStrings  
  
|Nom|Texte|  
|----------|----------|  
|TextboxExternalIdentitiesDisabled|Connexion est désactivée par les administrateurs de hello moment hello.|  
|TextboxExternalIdentitiesSigninInvitation|Vous pouvez également vous connecter avec|  
|TextboxExternalIdentitiesSigninInvitationPrimary|Connectez-vous avec :|  
  
###  <a name="SigninResources"></a> SigninResources  
  
|Nom|Texte|  
|----------|----------|  
|PrincipalNotFound|Principal introuvable ou signature non valide.|  
|ErrorSsoAuthenticationFailed|Échec de l’authentification SSO.|  
|ErrorSsoAuthenticationFailedDetailed|Jeton fourni non valide ou signature non vérifiable.|  
|ErrorSsoTokenInvalid|Jeton SSO non valide.|  
|ValidationErrorSpecificEmailAlreadyExists|Adresse de messagerie « {0} » déjà inscrite.|  
|ValidationErrorSpecificEmailInvalid|Adresse de messagerie « {0} » non valide.|  
|ValidationErrorPasswordInvalid|Le mot de passe n’est pas valide. Corrigez les erreurs hello et recommencez l’opération.|  
|PropertyTooShort|{0} est trop court.|  
|WebAuthenticationAddresserEmailInvalidErrorMessage|Adresse de messagerie non valide.|  
|ValidationMessageNewPasswordConfirmationRequired|Confirmez le nouveau mot de passe.|  
|ValidationErrorPasswordConfirmationRequired|Le mot de passe de confirmation est vide.|  
|WebAuthenticationEmailChangeNotice|Message électronique de confirmation de modification est trop sur hello {0}. Suivez les instructions qu’il contient tooconfirm votre nouvelle adresse de messagerie. Si par courrier électronique hello n’arrive pas tooyour la boîte de réception hello quelques minutes, vérifiez votre dossier courrier indésirable.|  
|WebAuthenticationEmailChangeNoticeHeader|Votre demande de modification de l’adresse de messagerie a été traitée.|  
|WebAuthenticationEmailChangeNoticeTitle|Modification de l’adresse de messagerie demandée.|  
|WebAuthenticationEmailHasBeenRevertedNotice|Votre adresse de messagerie existe déjà. La demande a été annulée.|  
|ValidationErrorEmailAlreadyExists|L’adresse de messagerie existe déjà.|  
|ValidationErrorEmailInvalid|Adresse de messagerie non valide.|  
|TextboxLabelEmail|Email|  
|ValidationErrorEmailRequired|L’adresse de messagerie est obligatoire.|  
|WebAuthenticationErrorNoticeHeader|Erreur|  
|WebAuthenticationFieldLengthErrorMessage|{0} doit avoir la longueur {1} au maximum.|  
|TextboxLabelEmailFirstName|Prénom|  
|ValidationErrorFirstNameRequired|Le prénom est obligatoire.|  
|ValidationErrorFirstNameInvalid|Prénom non valide.|  
|NoticeInvalidInvitationToken|Veuillez noter que les liens de confirmation ne sont valides que pendant 48 heures. Si vous vous trouvez toujours dans cette plage de temps, vérifiez que votre lien est correct. Si votre liaison a expiré, puis répétez l’action hello que vous essayez de tooconfirm.|  
|NoticeHeaderInvalidInvitationToken|Jeton d’invitation non valide.|  
|NoticeTitleInvalidInvitationToken|Erreur de confirmation.|  
|WebAuthenticationLastNameInvalidErrorMessage|Nom non valide.|  
|TextboxLabelEmailLastName|Nom|  
|ValidationErrorLastNameRequired|Le nom est obligatoire.|  
|WebAuthenticationLinkExpiredNotice|Lien de confirmation envoyé tooyou a expiré. `<a href={0}?token={1}>Resend confirmation email.</a\>`|  
|NoticePasswordResetLinkInvalidOrExpired|Votre lien de réinitialisation du mot de passe n’est pas valide ou a expiré.|  
|WebAuthenticationLinkExpiredNoticeTitle|Lien envoyé.|  
|WebAuthenticationNewPasswordLabel|Nouveau mot de passe|  
|ValidationMessageNewPasswordRequired|Un nouveau mot de passe est requis.|  
|TextboxLabelNotificationsSenderEmail|Adresse de messagerie de l’expéditeur des notifications|  
|TextboxLabelOrganizationName|Nom de l’organisation|  
|WebAuthenticationOrganizationRequiredErrorMessage|Le nom de l’organisation est vide.|  
|WebAuthenticationPasswordChangedNotice|Votre mot de passe a bien été mis à jour.|  
|WebAuthenticationPasswordChangedNoticeTitle|Mot de passe mis à jour.|  
|WebAuthenticationPasswordCompareErrorMessage|Les mots de passe ne correspondent pas.|  
|WebAuthenticationPasswordConfirmLabel|Confirmer le mot de passe|  
|ValidationErrorPasswordInvalidDetailed|Le mot de passe est trop faible.|  
|WebAuthenticationPasswordLabel|Mot de passe|  
|ValidationErrorPasswordRequired|Le mot de passe est requis.|  
|WebAuthenticationPasswordResetSendNotice|Message électronique de confirmation du mot de passe modification est trop sur hello {0}. Suivez les instructions de hello dans hello messagerie toocontinue votre processus de modification de mot de passe.|  
|WebAuthenticationPasswordResetSendNoticeHeader|Votre demande de réinitialisation de mot de passe a bien été traitée.|  
|WebAuthenticationPasswordResetSendNoticeTitle|Réinitialisation de mot de passe demandée.|  
|WebAuthenticationRequestNotFoundNotice|Demande introuvable.|  
|WebAuthenticationSenderEmailRequiredErrorMessage|L’adresse de messagerie de l’expéditeur des notifications est vide.|  
|WebAuthenticationSigninPasswordLabel|Confirmez la modification de hello en entrant un mot de passe|  
|WebAuthenticationSignupConfirmNotice|Message électronique de confirmation d’inscription est en cours trop {0}. < br /\> Veuillez suivez les instructions dans hello tooactivate de messagerie de votre compte. < br /\> si la messagerie de hello n’arrive pas dans votre boîte de réception dans hello quelques minutes, consultez votre dossier courrier indésirable.|  
|WebAuthenticationSignupConfirmNoticeHeader|Votre compte a bien été créé.|  
|WebAuthenticationSignupConfirmNoticeRepeatHeader|L’e-mail de confirmation d’inscription a été renvoyé.|  
|WebAuthenticationSignupConfirmNoticeTitle|Compte créé|  
|WebAuthenticationTokenRequiredErrorMessage|Le jeton est vide.|  
|WebAuthenticationUserAlreadyRegisteredNotice|Apparemment, qu'un utilisateur avec cette adresse de messagerie est déjà inscrit dans le système de hello. Si vous avez oublié votre mot de passe, veuillez réessayer toorestore ou contactez notre équipe de support.|  
|WebAuthenticationUserAlreadyRegisteredNoticeHeader|Utilisateur déjà inscrit.|  
|WebAuthenticationUserAlreadyRegisteredNoticeTitle|Déjà inscrit.|  
|ButtonLabelChangePassword|Modifier le mot de passe|  
|ButtonLabelChangeAccountInfo|Modifier les informations du compte|  
|ButtonLabelCloseAccount|Fermer le compte|  
|WebAuthenticationInvalidCaptchaErrorMessage|Texte entré ne correspond pas à texte sur l’image de hello. Réessayez.|  
|ValidationErrorCredentialsInvalid|L’adresse de messagerie ou le mot de passe n’est pas valide. Corrigez les erreurs hello et recommencez l’opération.|  
|WebAuthenticationRequestIsNotValid|La demande n’est pas valide.|  
|WebAuthenticationUserIsNotConfirm|Veuillez confirmer votre inscription avant de tenter de toosign dans.|  
|WebAuthenticationInvalidEmailFormated|L’adresse de messagerie n’est pas valide : {0}.|  
|WebAuthenticationUserNotFound|Utilisateur non trouvé.|  
|WebAuthenticationTenantNotRegistered|Votre compte appartient locataire d’Azure Active Directory tooa qui n’est pas autorisé tooaccess ce portail.|  
|WebAuthenticationAuthenticationFailed|L’authentification a échoué.|  
|WebAuthenticationGooglePlusNotEnabled|L’authentification a échoué. Si vous autorisé application hello, Veuillez contactez hello admin toomake que l’authentification Google est configurée correctement.|  
|ValidationErrorAllowedTenantIsRequired|Le client autorisé est requis.|  
|ValidationErrorTenantIsNotValid|client Azure Active Directory de Hello '{0}' n’est pas valide.|  
|WebAuthenticationActiveDirectoryTitle|Azure Active Directory|  
|WebAuthenticationLoginUsingYourProvider|Connectez-vous avec votre compte {0}.|  
|WebAuthenticationUserLimitNotice|Ce service a atteint le nombre maximal de hello des utilisateurs autorisés. Veuillez `<a href="mailto:{0}"\>contact hello administrator</a\>` tooupgrade leur enregistrement d’utilisateur de service et de réactiver.|  
|WebAuthenticationUserLimitNoticeHeader|Inscription des utilisateurs désactivée.|  
|WebAuthenticationUserLimitNoticeTitle|Inscription des utilisateurs désactivée.|  
|WebAuthenticationUserRegistrationDisabledNotice|L’inscription des utilisateurs a été désactivée par l’administrateur de hello. Connectez-vous avec un fournisseur d’identité externe.|  
|WebAuthenticationUserRegistrationDisabledNoticeHeader|Inscription des utilisateurs désactivée.|  
|WebAuthenticationUserRegistrationDisabledNoticeTitle|Inscription des utilisateurs désactivée.|  
|WebAuthenticationSignupPendingConfirmationNotice|Nous pouvons achever la création de votre compte hello nous devons tooverify votre adresse de messagerie. Nous avons envoyé un message électronique trop {0}. Suivez les instructions de hello hello messagerie tooactivate à l’intérieur de votre compte. Si par courrier électronique hello n’arrive dans hello quelques minutes, vérifiez votre dossier courrier indésirable.|  
|WebAuthenticationSignupPendingConfirmationAccountFoundNotice|Nous avons trouvé un compte non confirmé pour l’adresse de messagerie hello {0}. toocomplete hello la création de votre compte, que nous devons tooverify votre adresse de messagerie. Nous avons envoyé un message électronique trop {0}. Suivez les instructions de hello hello messagerie tooactivate à l’intérieur de votre compte. Par courrier électronique hello n’arrive dans hello quelques minutes, vérifiez votre dossier courrier indésirable|  
|WebAuthenticationSignupConfirmationAlmostDone|C’est presque fini.|  
|WebAuthenticationSignupConfirmationEmailSent|Nous avons envoyé un message électronique trop {0}. Suivez les instructions de hello hello messagerie tooactivate à l’intérieur de votre compte. Si par courrier électronique hello n’arrive dans hello quelques minutes, vérifiez votre dossier courrier indésirable.|  
|WebAuthenticationEmailSentNotificationMessage|Message électronique envoyé avec succès trop {0}|  
|WebAuthenticationNoAadTenantConfigured|Aucun client Azure Active Directory est configuré pour le service hello.|  
|CheckboxLabelUserRegistrationTermsConsentRequired|J’accepte toohello `<a data-toggle="modal" href="#" data-target="#terms"\>Terms of Use</a\>`.|  
|TextblockUserRegistrationTermsProvided|Veuillez consulter les `<a data-toggle="modal" href="#" data-target="#terms"\>Terms of Use.</a\>`.|  
|DialogHeadingTermsOfUse|Conditions d’utilisation|  
|ValidationMessageConsentNotAccepted|Vous devez accepter les conditions d’utilisation de toohello avant de pouvoir continuer.|  
  
###  <a name="SigninStrings"></a> SigninStrings  
  
|Nom|Texte|  
|----------|----------|  
|WebAuthenticationForgotPassword|Vous avez oublié votre mot de passe ?|  
|WebAuthenticationIfAdministrator|Si vous êtes un administrateur, vous devez vous connecter `<a href="{0}"\>here</a\>`.|  
|WebAuthenticationNotAMember|Vous n’êtes pas encore membre ? `<a href="/signup"\>Sign up now</a\>`|  
|WebAuthenticationRemember|Se souvenir de moi sur cet ordinateur|  
|WebAuthenticationSigininWithPassword|Connectez-vous avec votre nom d’utilisateur et votre mot de passe.|  
|WebAuthenticationSigninTitle|de connexion|  
|WebAuthenticationSignUpNow|ici|  
  
###  <a name="SignupStrings"></a> SignupStrings  
  
|Nom|Texte|  
|----------|----------|  
|PageTitleSignup|Inscription|  
|WebAuthenticationAlreadyAMember|Déjà membre ?|  
|WebAuthenticationCreateNewAccount|Créer un nouveau compte Gestion des API|  
|WebAuthenticationSigninNow|Se connecter|  
|ButtonLabelSignup|Inscription|  
  
###  <a name="SubscriptionListStrings"></a> SubscriptionListStrings  
  
|Nom|Texte|  
|----------|----------|  
|SubscriptionCancelConfirmation|Êtes-vous sûr de vouloir toocancel cet abonnement ?|  
|SubscriptionRenewConfirmation|Êtes-vous sûr de vouloir toorenew cet abonnement ?|  
|WebDevelopersManageSubscriptions|Gérer les abonnements|  
|WebDevelopersPrimaryKey|Clé primaire|  
|WebDevelopersRegenerateLink|Régénérer|  
|WebDevelopersSecondaryKey|Clé secondaire|  
|ButtonLabelShowKey|Afficher|  
|ButtonLabelRenewSubscription|Renouveler|  
|WebDevelopersSubscriptionReqested|Demandé sur {0}|  
|WebDevelopersSubscriptionRequestedState|Demandé|  
|WebDevelopersSubscriptionTableNameHeader|Nom|  
|WebDevelopersSubscriptionTableStateHeader|State|  
|WebDevelopersUsageStatisticsLink|Rapports d’analyse|  
|WebDevelopersYourSubscriptions|Vos abonnements|  
|SubscriptionPropertyLabelRequestedDate|Demandé le|  
|SubscriptionPropertyLabelStartedDate|Démarré le|  
|PageTitleRenameSubscription|Renommer l’abonnement|  
|SubscriptionPropertyLabelName|Nom d’abonnement|  
  
###  <a name="SubscriptionStrings"></a> SubscriptionStrings  
  
|Nom|Texte|  
|----------|----------|  
|SectionHeadingCloseAccount|Recherche tooclose votre compte ?|  
|PageTitleDeveloperProfile|Profil|  
|ButtonLabelHideKey|Masquer|  
|ButtonLabelRegenerateKey|Régénérer|  
|InformationMessageKeyWasRegenerated|Êtes-vous sûr de vouloir tooregenerate cette clé ?|  
|ButtonLabelShowKey|Afficher|  
  
###  <a name="UpdateProfileStrings"></a> UpdateProfileStrings  
  
|Nom|Texte|  
|----------|----------|  
|ButtonLabelUpdateProfile|Mettre à jour le profil|  
|PageTitleUpdateProfile|Mettre à jour les informations du compte|  
  
###  <a name="UserProfile"></a> UserProfile  
  
|Nom|Texte|  
|----------|----------|  
|ButtonLabelChangeAccountInfo|Modifier les informations du compte|  
|ButtonLabelChangePassword|Modifier le mot de passe|  
|ButtonLabelCloseAccount|Fermer le compte|  
|TextboxLabelEmail|Email|  
|TextboxLabelEmailFirstName|Prénom|  
|TextboxLabelEmailLastName|Nom|  
|TextboxLabelNotificationsSenderEmail|Adresse de messagerie de l’expéditeur des notifications|  
|TextboxLabelOrganizationName|Nom de l’organisation|  
|SubscriptionStateActive|Actif|  
|SubscriptionStateCancelled|Annulé|  
|SubscriptionStateExpired|Expiré|  
|SubscriptionStateRejected|Rejeté|  
|SubscriptionStateRequested|Demandé|  
|SubscriptionStateSuspended|Interrompu|  
|DefaultSubscriptionNameTemplate|{0} (par défaut)|  
|SubscriptionNameTemplate|Accès développeurs #{0}|  
|TextboxLabelSubscriptionName|Nom d’abonnement|  
|ValidationMessageSubscriptionNameRequired|Le nom d'abonnement ne peut pas être vide.|  
|ApiManagementUserLimitReached|Ce service a atteint le nombre maximal de hello des utilisateurs autorisés. Mettez à niveau tooa niveau de tarification supérieur.|  
  
##  <a name="glyphs"></a> Ressources de glyphes  
 Modèles portails de gestion des API développeur peuvent utiliser des glyphes hello à partir de [Glyphicons d’amorçage](http://getbootstrap.com/components/#glyphicons). Ce jeu de glyphes inclut plus de 250 glyphes dans un format de police à partir de hello [Glyphicon](http://glyphicons.com/) Halflings définie. toouse un glyphe à partir de ce définie, utilisez hello selon la syntaxe.  
  
```html  
<span class="glyphicon glyphicon-user">  
```  
  
 Pour hello une liste complète des glyphes, consultez [Glyphicons d’amorçage](http://getbootstrap.com/components/#glyphicons).

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur l’utilisation des modèles, consultez [comment toocustomize hello portail des développeurs gestion des API à l’aide de modèles](api-management-developer-portal-templates.md).
