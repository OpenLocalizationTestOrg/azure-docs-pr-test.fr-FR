---
title: "hello aaaUnderstanding Azure Active Directory le manifeste d’Application | Documents Microsoft"
description: "Couverture détaillés de manifeste d’application Azure Active Directory hello, qui représente la configuration d’identité d’une application dans un locataire Azure AD et est utilisé toofacilitate OAuth autorisation, expérience de consentement et bien plus encore."
services: active-directory
documentationcenter: 
author: sureshja
manager: mbaldwin
editor: 
ms.assetid: 4804f3d4-0ff1-4280-b663-f8f10d54d184
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: sureshja
ms.custom: aaddev
ms.reviewer: elisol
ms.openlocfilehash: 096c9d5501edbfc08731fea670cee559d4442ad1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-azure-active-directory-application-manifest"></a>Présentation de manifeste de l’application hello Azure Active Directory
Les applications qui s’intègrent avec Azure Active Directory (AD) doivent être enregistrées avec un locataire Azure AD, en fournissant une configuration d’identité permanente de l’application hello. Cette configuration est consultée lors de l’exécution, l’activation de scénarios qui permettent à une application toooutsource et service broker d’authentification/autorisation via Azure AD. Pour plus d’informations sur le modèle d’application hello Azure AD, consultez hello [Ajout, mise à jour et suppression d’une Application] [ ADD-UPD-RMV-APP] l’article.

## <a name="updating-an-applications-identity-configuration"></a>Mise à jour d’une configuration de l’identité d’une application
En fait plusieurs options sont disponibles pour la mise à jour des propriétés de hello sur la configuration d’identité d’une application, qui varient dans les fonctions et les degrés de difficulté, y compris hello suivantes :

* Hello  **[du portail Azure] [ AZURE-PORTAL] interface utilisateur Web** vous permet de propriétés les plus courantes hello tooupdate d’une application. Il s’agit de hello plus rapide et moins manière susceptible d’engendrer des erreurs de mise à jour les propriétés de votre application, mais ne pas vous donner des propriétés de tooall un accès complet, comme hello deux méthodes.
* Pour les scénarios plus avancés, vous devez tooupdate les propriétés qui ne sont pas exposées dans hello portail Azure classic, vous pouvez modifier hello **manifeste d’application**. Cela est le focus de hello de cet article et est décrite plus en détail à compter de la section suivante de hello.
* Il est également possible trop**écrire une application qui utilise hello [API Graph] [ GRAPH-API]**  tooupdate votre application, ce qui nécessite hello plus d’efforts. Cela peut être une option intéressante, si vous écrivez des logiciels de gestion, ou propriétés de l’application tooupdate régulièrement de manière automatique.

## <a name="using-hello-application-manifest-tooupdate-an-applications-identity-configuration"></a>Configuration d’identité d’une application à l’aide de tooupdate de manifeste application hello
Via hello [portail Azure][AZURE-PORTAL], vous pouvez gérer la configuration d’identité de votre application en mettant à jour le manifeste de l’application hello à l’aide d’éditeur de manifeste hello inline. Vous pouvez également télécharger et télécharger le manifeste de l’application hello en tant qu’un fichier JSON. Aucun fichier réel n’est stocké dans le répertoire de hello. manifeste d’application Hello est simplement une opération HTTP GET sur l’entité d’Application hello API Azure AD Graph et téléchargement hello est une opération HTTP PATCH sur l’entité d’Application hello.

Par conséquent, dans le format de commande toounderstand hello et les propriétés de manifeste de l’application hello, vous devrez tooreference hello API Graph [entité d’Application] [ APPLICATION-ENTITY] documentation. Les exemples de mises à jour pouvant être effectuées via le manifeste d’application sont les suivants :

* **Déclaration des étendues d’autorisation (oauth2Permissions)** exposées par votre API web. Consultez la rubrique « Exposition Web API tooOther Applications » hello [intégration d’Applications avec Azure Active Directory] [ INTEGRATING-APPLICATIONS-AAD] pour plus d’informations sur l’implémentation de l’emprunt d’identité utilisateur à l’aide de hello oauth2Permissions déléguée étendue d’autorisation. Comme mentionné précédemment, les propriétés de l’entité sont documentées dans hello API Graph [entité et le Type complexe] [ APPLICATION-ENTITY] article de référence, y compris les propriété oauth2Permissions hello qui est un collection de type [OAuth2Permission][APPLICATION-ENTITY-OAUTH2-PERMISSION].
* **Déclaration des rôles d’application (appRoles) exposées par votre application**. propriété appRoles de l’entité de l’Application Hello est une collection de type [AppRole][APPLICATION-ENTITY-APP-ROLE]. Consultez hello [le contrôle d’accès dans les applications cloud à l’aide d’Azure AD basée sur les rôles] [ RBAC-CLOUD-APPS-AZUREAD] article pour obtenir un exemple d’implémentation.
* **Déclarer des applications (knownClientApplications) clients connus**, qui permettent de consentement de hello tie toologically Hello spécifié client ou les applications toohello ressource/API web.
* **Demande de revendication appartenances aux groupes Azure AD tooissue** pour hello signé à l’utilisateur (groupMembershipClaims).  Cela peut également être revendications tooissue configuré sur les appartenances aux rôles de l’utilisateur hello active. Consultez hello [autorisation dans les Applications Cloud à l’aide de groupes Active Directory] [ AAD-GROUPS-FOR-AUTHORIZATION] article pour obtenir un exemple d’implémentation.
* **Autoriser votre attribution de OAuth 2.0 implicite application toosupport** flux (oauth2AllowImplicitFlow). Ce type de flux d’octroi est utilisé avec les pages web JavaScript incorporées ou les applications SPA (Single Page Applications). Pour plus d’informations sur l’octroi d’autorisation implicite hello, consultez [hello de présentation OAuth2 implicite accorder des flux dans Azure Active Directory][IMPLICIT-GRANT].
* **Activer l’utilisation de X509 certificats comme clé secrète de hello** (keyCredentials). Consultez hello [créer des applications de service et le démon dans Office 365] [ O365-SERVICE-DAEMON-APPS] et [tooauth du guide du développeur avec des API Azure Resource Manager] [ DEV-GUIDE-TO-AUTH-WITH-ARM] articles pour les exemples d’implémentation.
* **Ajouter un nouvel URI d’ID d’application** pour votre application (identifierURIs[]). URI d’ID d’application sont utilisés toouniquely identifier une application dans son locataire Azure AD (ou sur plusieurs locataires Azure AD, pour les scénarios d’architecture mutualisées lorsque qualifié via le domaine personnalisé vérifié). Ils sont utilisés lors de la demande d’application de ressource autorisations tooa, ou l’acquisition d’un jeton d’accès pour une application de ressource. Lorsque vous mettez à jour cet élément, hello même mise à jour est effectuée servicePrincipalNames [du principal du service de correspondante toohello] collection, qui se trouve dans le client de base de l’application hello.

Hello manifeste d’application fournit également un bon moyen tootrack hello état d’enregistrement de votre application. Car il n’est disponible au format JSON, la représentation sous forme de fichier hello peut être vérifiée dans votre contrôle de code source, ainsi que du code source de votre application.

## <a name="step-by-step-example"></a>Exemple étape par étape
Permet désormais de guide tooupdate de hello étapes requises de configuration d’identité de votre application via le manifeste de l’application hello. Nous en surbrillance un des hello précédents exemples, montrant comment toodeclare une nouvelle autorisation d’étendue sur une application de ressource :

1. Connectez-vous à toohello [portail Azure][AZURE-PORTAL].
2. Une fois que vous avez été authentifié, choisissez votre locataire Azure AD en le sélectionnant dans hello coin supérieur droit de la page de hello.
3. Sélectionnez **Azure Active Directory** extension à partir de hello gauche du volet de navigation, cliquez sur **inscriptions d’application**.
4. Recherchez l’application hello tooupdate dans la liste de hello et cliquez dessus.
5. À partir de la page d’application hello, cliquez sur **manifeste** éditeur de manifeste tooopen hello inline. 
6. Vous pouvez modifier directement le manifeste de hello à l’aide de cet éditeur. Notez que ce manifeste hello suit le schéma hello pour hello [entité d’Application] [ APPLICATION-ENTITY] comme mentionné précédemment : par exemple, la condition que nous souhaitons tooimplement/exposent une nouvelle autorisation d’appelée « Employees.Read.All » pour notre application de ressource (API), vous devez simplement ajouter une collection d’oauth2Permissions toohello élément de nouveau/seconde, Internet Explorer :
   
        "oauth2Permissions": [
        {
        "adminConsentDescription": "Allow hello application tooaccess MyWebApplication on behalf of hello signed-in user.",
        "adminConsentDisplayName": "Access MyWebApplication",
        "id": "aade5b35-ea3e-481c-b38d-cba4c78682a0",
        "isEnabled": true,
        "type": "User",
        "userConsentDescription": "Allow hello application tooaccess MyWebApplication on your behalf.",
        "userConsentDisplayName": "Access MyWebApplication",
        "value": "user_impersonation"
        },
        {
        "adminConsentDescription": "Allow hello application toohave read-only access tooall Employee data.",
        "adminConsentDisplayName": "Read-only access tooEmployee records",
        "id": "2b351394-d7a7-4a84-841e-08a6a17e4cb8",
        "isEnabled": true,
        "type": "User",
        "userConsentDescription": "Allow hello application toohave read-only access tooyour Employee data.",
        "userConsentDisplayName": "Read-only access tooyour Employee records",
        "value": "Employees.Read.All"
        }
        ],
   
    Hello entrée doit être unique et vous devez générer par conséquent un nouveau Global Unique ID (GUID) pour hello `"id"` propriété. Dans ce cas, étant donné que nous avons spécifié `"type": "User"`, cette autorisation peut être consenti tooby n’importe quel compte authentifié par hello locataire Azure AD dans le hello application de l’API des ressources est enregistrée. Cette tooaccess des autorisations d’application accorde hello client il procuration du compte hello. chaînes de nom de description et l’affichage Hello sont utilisées durant le consentement et l’affichage Bonjour portail Azure.
6. Lorsque vous avez terminé la mise à jour du manifeste de hello, cliquez sur **enregistrer** manifeste de hello toosave.  
   
Maintenant que hello manifeste est enregistré, vous pouvez autoriser un client enregistré application accès toohello nouveau que nous ajoutées ci-dessus. Cette fois, que vous pouvez utiliser hello l’interface utilisateur de Web du portail Azure plutôt que de modifier le manifeste de l’application hello client :  

1. Tout d’abord accéder toohello **paramètres** Panneau de hello toowhich d’application client vous souhaitez tooadd accès toohello nouvelle API, cliquez sur **autorisations requises** et choisissez **sélectionner une API** .
2. Puis s’affiche avec la liste hello des applications de ressources inscrit (API) de client de hello. Cliquez sur hello ressource application tooselect, ou le nom de zone de recherche hello application hello hello de type. Lorsque vous avez trouvé l’application hello, cliquez sur **sélectionnez**.  
3. Cette opération prendra toohello **autorisations Select** page qui affiche la liste de hello des autorisations d’Application et des autorisations déléguées qui sont disponibles pour l’application de ressource hello. Sélectionnez hello nouvelle autorisation dans l’ordre tooadd il toohello client demandée par la liste des autorisations. Cette nouvelle autorisation sera stockée dans la configuration d’identité de l’application hello client, dans la propriété de collection hello « requiredResourceAccess ».


Vous avez terminé. Vos applications s’exécutent désormais à l’aide de leur nouvelle configuration d’identité.

## <a name="next-steps"></a>Étapes suivantes
* Pour plus d’informations sur la relation hello entre les objets d’Application et de Principal du Service d’une application, consultez [Application et les objets principal du service dans Azure AD][AAD-APP-OBJECTS].
* Consultez hello [glossaire du développeur Azure AD] [ AAD-DEVELOPER-GLOSSARY] pour les définitions de certains des concepts de développement hello core Azure Active Directory (AD).

Utilisez la section commentaires hello tooprovide commentaires et nous aider à affiner et mettre en forme notre contenu.

<!--article references -->
[AAD-APP-OBJECTS]: active-directory-application-objects.md
[AAD-DEVELOPER-GLOSSARY]: active-directory-dev-glossary.md
[AAD-GROUPS-FOR-AUTHORIZATION]: http://www.dushyantgill.com/blog/2014/12/10/authorization-cloud-applications-using-ad-groups/
[ADD-UPD-RMV-APP]: active-directory-integrating-applications.md
[APPLICATION-ENTITY]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[APPLICATION-ENTITY-APP-ROLE]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#approle-type
[APPLICATION-ENTITY-OAUTH2-PERMISSION]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permission-type
[AZURE-PORTAL]: https://portal.azure.com
[DEV-GUIDE-TO-AUTH-WITH-ARM]: http://www.dushyantgill.com/blog/2015/05/23/developers-guide-to-auth-with-azure-resource-manager-api/
[GRAPH-API]: active-directory-graph-api.md
[IMPLICIT-GRANT]: active-directory-dev-understanding-oauth2-implicit-grant.md
[INTEGRATING-APPLICATIONS-AAD]: https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
[O365-PERM-DETAILS]: https://msdn.microsoft.com/office/office365/HowTo/application-manifest
[O365-SERVICE-DAEMON-APPS]: https://msdn.microsoft.com/office/office365/howto/building-service-apps-in-office-365
[RBAC-CLOUD-APPS-AZUREAD]: http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/

