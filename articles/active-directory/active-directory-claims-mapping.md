---
title: "Mappage de revendications dans Azure Active Directory (préversion publique) | Microsoft Docs"
description: "Cette page décrit le mappage de revendications Azure Active Directory."
services: active-directory
author: billmath
manager: femila
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: billmath
ms.openlocfilehash: ff07b9954d5c2ce71ab0ffd0db49fde15f323586
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="claims-mapping-in-azure-active-directory-public-preview"></a>Mappage de revendications dans Azure Active Directory (préversion publique)

>[!NOTE]
>Cette fonctionnalité remplace et remplace hello [personnalisation des revendications](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-claims-customization) proposés via le portail de hello aujourd'hui. Si vous personnalisez des revendications à l’aide du portail de hello en outre toohello méthode graphique/PowerShell détaillées dans ce document sur hello même application, les jetons émis pour cette application va ignorer la configuration hello dans le portail de hello.
Configurations effectuées par le biais des méthodes hello détaillées dans ce document n’apparaîtront pas dans le portail de hello.

Cette fonctionnalité est utilisée par le locataire administrateurs toocustomize hello revendications émises dans les jetons pour une application spécifique du client. Vous pouvez utiliser des stratégies de mappage de revendications pour effectuer les opérations suivantes :

- sélectionner les revendications incluses dans les jetons ;
- créer des types de revendications inexistants ;
- Choisissez ou modifiez la source hello de données émises dans les revendications spécifiques.

>[!NOTE]
>Cette fonctionnalité est actuellement disponible en préversion publique. Préparez-vous à toorevert ou supprimer toutes les modifications. Hello fonctionnalité est disponible dans n’importe quel abonnement Azure Active Directory (Azure AD) au cours de la version préliminaire publique. Toutefois, lorsque la fonctionnalité de hello devient disponible de manière générale, certains aspects de la fonctionnalité de hello peuvent nécessiter un abonnement premium à Azure Active Directory.

## <a name="claims-mapping-policy-type"></a>Type de stratégie de mappage de revendications
Dans Azure AD, un objet de **stratégie** représente un ensemble de règles appliquées à des applications individuelles ou à toutes les applications d’une organisation. Chaque type de stratégie a une structure unique, avec un ensemble de propriétés qui sont ensuite appliquées toowhich tooobjects qu'ils sont attribués.

Revendications d’un mappage de stratégie est un type de **stratégie** objet qui modifie hello de revendications émis dans les jetons émis pour des applications spécifiques.

## <a name="claim-sets"></a>Ensembles de revendications
Il existe des ensembles de revendications qui définissent comment et quand ils sont utilisés dans des jetons.

### <a name="core-claim-set"></a>Ensemble de revendications principal
Revendications présentes dans les noyaux hello revendications sont présentes dans chaque jeton, quelle que soit la stratégie. Ces revendications sont également considérées comme restreintes, et ne peuvent pas être modifiées.

### <a name="basic-claim-set"></a>Ensemble de revendications de base
ensemble de revendications basic de Hello inclut les revendications hello qui sont émises par défaut pour les jetons (dans le jeu de revendications addition toohello core). Ces revendications peuvent être omises ou modifiées à l’aide de revendications hello mappage de stratégies.

### <a name="restricted-claim-set"></a>Ensemble de revendications restreint
Les revendications restreintes ne peuvent pas être modifiées à l’aide d’une stratégie. source de données Hello ne peut pas être modifié, et aucune transformation n’est appliquée lors de la génération de ces revendications.

#### <a name="table-1-json-web-token-jwt-restricted-claim-set"></a>Tableau 1 : ensemble de revendications restreint JSON Web Token (JWT)
|Type de revendication (nom)|
| ----- |
|_claim_names|
|_claim_sources|
|access_token|
|account_type|
|acr|
|actor|
|actortoken|
|aio|
|altsecid|
|amr|
|app_chain|
|app_displayname|
|app_res|
|appctx|
|appctxsender|
|appid|
|appidacr|
|assertion|
|at_hash|
|aud|
|auth_data|
|auth_time|
|authorization_code|
|azp|
|azpacr|
|c_hash|
|ca_enf|
|cc|
|cert_token_use|
|client_id|
|cloud_graph_host_name|
|cloud_instance_name|
|cnf|
|code|
|controls|
|credential_keys|
|csr|
|csr_type|
|deviceid|
|dns_names|
|domain_dns_name|
|domain_netbios_name|
|e_exp|
|email|
|endpoint|
|enfpolids|
|exp|
|expires_on|
|grant_type|
|graph|
|group_sids|
|groups|
|hasgroups|
|hash_alg|
|home_oid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/expired|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier|
|iat|
|identityprovider|
|idp|
|in_corp|
|instance|
|ipaddr|
|isbrowserhostedapp|
|iss|
|jwk|
|key_id|
|key_type|
|mam_compliance_url|
|mam_enrollment_url|
|mam_terms_of_use_url|
|mdm_compliance_url|
|mdm_enrollment_url|
|mdm_terms_of_use_url|
|nameid|
|nbf|
|netbios_name|
|nonce|
|oid|
|on_prem_id|
|onprem_sam_account_name|
|onprem_sid|
|openid2_id|
|password|
|platf|
|polids|
|pop_jwk|
|preferred_username|
|previous_refresh_token|
|primary_sid|
|puid|
|pwd_exp|
|pwd_url|
|redirect_uri|
|refresh_token|
|refreshtoken|
|request_nonce|
|resource|
|role|
|roles|
|scope|
|scp|
|sid|
|signature|
|signin_state|
|src1|
|src2|
|sub|
|tbid|
|tenant_display_name|
|tenant_region_scope|
|thumbnail_photo|
|tid|
|tokenAutologonEnabled|
|trustedfordelegation|
|unique_name|
|upn|
|user_setting_sync_url|
|username|
|uti|
|ver|
|verified_primary_email|
|verified_secondary_email|
|wids|
|win_ver|

#### <a name="table-2-security-assertion-markup-language-saml-restricted-claim-set"></a>Tableau 2 : ensemble de revendications restreint Security Assertion Markup Language (SAML)
|Type de revendication (URI)|
| ----- |
|http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/expired|
|http://schemas.microsoft.com/identity/claims/accesstoken|
|http://schemas.microsoft.com/identity/claims/openid2_id|
|http://schemas.microsoft.com/identity/claims/identityprovider|
|http://schemas.microsoft.com/identity/claims/objectidentifier|
|http://schemas.microsoft.com/identity/claims/puid|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier[MR1] |
|http://schemas.microsoft.com/identity/claims/tenantid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod|
|http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/groups|
|http://schemas.microsoft.com/claims/groups.link|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/role|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/wids|
|http://schemas.microsoft.com/2014/09/devicecontext/claims/iscompliant|
|http://schemas.microsoft.com/2014/02/devicecontext/claims/isknown|
|http://schemas.microsoft.com/2012/01/devicecontext/claims/ismanaged|
|http://schemas.microsoft.com/2014/03/psso|
|http://schemas.microsoft.com/claims/authnmethodsreferences|
|http://schemas.xmlsoap.org/ws/2009/09/identity/claims/actor|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/samlissuername|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/confirmationkey|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/primarygroupsid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authorizationdecision|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authentication|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/sid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarygroupsid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarysid|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/denyonlysid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlywindowsdevicegroup|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdeviceclaim|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsfqbnversion|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowssubauthority|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsuserclaim|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/x500distinguishedname|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/ispersistent|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier|
|http://schemas.microsoft.com/identity/claims/scope|

## <a name="claims-mapping-policy-properties"></a>Propriétés de stratégie de mappage de revendications
Utilisez les propriétés de hello de mappage de stratégie toocontrol les revendications qui sont émises, et où les données de salutation en provenance de revendications. Si aucune stratégie n’est définie, système de hello émet des jetons contenant l’ensemble de revendications principal hello hello base du jeu de revendications et toutes les revendications facultatif hello application a choisi tooreceive.

### <a name="include-basic-claim-set"></a>Ensemble de revendications de base Include

**Chaîne :** IncludeBasicClaimSet

**Type de données :** valeur booléenne (True ou False)

**Résumé :** cette propriété détermine si les ensemble de revendications basic de hello est inclus dans les jetons concernés par cette stratégie. 

- Si set tooTrue, toutes les revendications dans le jeu de revendications basic de hello est émis dans les jetons affectées par la stratégie de hello. 
- Si set tooFalse, les revendications dans le jeu de revendications basic de hello n’est pas dans les jetons hello, sauf s’ils sont individuellement ajoutés dans la propriété de schéma de revendications hello Hello même stratégie.

>[!NOTE] 
>Revendications présentes dans les noyaux hello revendications sont présents dans chaque jeton, indépendamment de ce que cette propriété est définie. 

### <a name="claims-schema"></a>Schéma de revendications

**Chaîne :** ClaimsSchema

**Type de données :** objet blob JSON avec une ou plusieurs entrées de schéma de revendication

**Résumé :** cette propriété définit les revendications qui sont présentes dans les jetons hello affectées par la stratégie de hello, en outre toohello base de revendications ensemble et les principaux hello.
Pour chaque entrée de schéma de revendication définie dans cette propriété, certaines informations sont requises. Vous devez spécifier d'où proviennent les données de salutation (**valeur** ou **paire Source/ID**), et les données de salutation de revendication est émise comme (**Type de revendication**).

### <a name="claim-schema-entry-elements"></a>Éléments d’entrée du schéma de revendication

**Valeur :** élément la valeur hello définit une valeur statique en tant que toobe de données hello émis dans une revendication de hello.

**Paire source/ID :** hello Source et de définissent des éléments de code où les données de salutation hello revendication en provenance de. 

élément de Source de Hello doit être définie tooone suivants de hello : 


- « utilisateur » : les données de salutation Bonjour de revendication est une propriété sur l’objet utilisateur de hello. 
- « application » : les données de salutation Bonjour de revendication est une propriété sur le principal de service d’application (client) hello. 
- « ressource » : les données de salutation Bonjour de revendication est une propriété sur le principal du service ressources hello.
- « public » : données hello dans hello revendication sont une propriété sur le principal du service hello qui est public hello du jeton de hello (soit hello client ou ressources principal de service).
- « company » : données hello Bonjour de revendication est une propriété sur l’objet de société du client de ressource hello.
- « transformation » : les données de salutation Bonjour de revendication est à partir de la transformation des revendications (voir la section hello « transformation des revendications » plus loin dans cet article). 

Si la source de hello est transformation, hello **TransformationID** élément doit être inclus dans cette définition de la revendication également.

élément de code Hello identifie dont la propriété sur la source de hello fournit la valeur de hello pour hello revendication. Hello tableau suivant répertorie les valeurs hello d’ID valide pour chaque valeur de la Source.

#### <a name="table-3-valid-id-values-per-source"></a>Tableau 3 : valeurs d’ID valides par source
|Source|ID|Description|
|-----|-----|-----|
|Utilisateur|surname|Nom de famille|
|Utilisateur|givenname|Prénom|
|Utilisateur|displayname|Display Name|
|Utilisateur|objectid|ObjectID|
|Utilisateur|mail|Adresse de messagerie|
|Utilisateur|userPrincipalName|Nom d’utilisateur principal|
|Utilisateur|department|department|
|Utilisateur|onpremisessamaccountname|Nom de compte Sam local|
|Utilisateur|netbiosname|Nom NetBios|
|Utilisateur|dnsdomainname|Nom de domaine DNS|
|Utilisateur|onpremisesecurityidentifier|Identificateur de sécurité local|
|Utilisateur|companyname|Nom de l’organisation|
|Utilisateur|streetaddress|Adresse postale|
|Utilisateur|postalcode|Code postal|
|Utilisateur|preferredlanguange|Langue par défaut|
|Utilisateur|onpremisesuserprincipalname|UPN local|
|Utilisateur|mailNickName|pseudonyme de messagerie|
|Utilisateur|extensionattribute1|Attribut d’extension 1|
|Utilisateur|extensionattribute2|Attribut d’extension 2|
|Utilisateur|extensionattribute3|Attribut d’extension 3|
|Utilisateur|extensionattribute4|Attribut d’extension 4|
|Utilisateur|extensionattribute5|Attribut d’extension 5|
|Utilisateur|extensionattribute6|Attribut d’extension 6|
|Utilisateur|extensionattribute7|Attribut d’extension 7|
|Utilisateur|extensionattribute8|Attribut d’extension 8|
|Utilisateur|extensionattribute9|Attribut d’extension 9|
|Utilisateur|extensionattribute10|Attribut d’extension 10|
|Utilisateur|extensionattribute11|Attribut d’extension 11|
|Utilisateur|extensionattribute12|Attribut d’extension 12|
|Utilisateur|extensionattribute13|Attribut d’extension 13|
|Utilisateur|extensionattribute14|Attribut d’extension 14|
|Utilisateur|extensionattribute15|Attribut d’extension 15|
|Utilisateur|othermail|Autre adresse e-mail|
|Utilisateur|country|Pays|
|Utilisateur|city|City|
|Utilisateur|state|State|
|Utilisateur|jobtitle|Fonction|
|Utilisateur|employeeid|ID d’employé|
|Utilisateur|facsimiletelephonenumber|Numéro de télécopie|
|application, ressource, audience|displayname|Nom d’affichage|
|application, ressource, audience|objected|ObjectID|
|application, ressource, audience|tags|Balise de principal du service|
|Entreprise|tenantcountry|Pays du locataire|

**TransformationID :** hello TransformationID l’élément doit être fourni que si hello élément Source est défini trop « transformation ».

- Cet élément doit correspondre à un élément d’entrée de transformation hello Bonjour ID hello **ClaimsTransformation** propriété qui définit la façon dont les données hello pour cette revendication sont générées.

**Type de revendication :** hello **JwtClaimType** et **SamlClaimType** éléments définissent cette entrée de schéma de revendication fait référence à de revendication.

- Hello JwtClaimType doit contenir le nom hello de toobe de revendication hello émis dans les jetons Web JSON.
- Hello SamlClaimType doit contenir hello URI Hello revendication toobe émis dans les jetons SAML.

>[!NOTE]
>Les noms et les URI de revendications de hello restreint revendication ensemble ne peut pas être utilisé pour les éléments de type de revendication hello. Pour plus d’informations, consultez hello « Exceptions et restrictions » plus loin dans cet article.

### <a name="claims-transformation"></a>Transformation de revendications

**Chaîne :** ClaimsTransformation

**Type de données :** blob JSON avec une ou plusieurs entrées de transformation 

**Résumé :** utiliser cette propriété tooapply transformations toosource les données communes, données de sortie toogenerate hello pour les revendications sont précisées dans hello schéma de revendications.

**ID :** utilisation hello ID élément tooreference cette entrée de transformation Bonjour une entrée de schéma de revendications TransformationID. Cette valeur doit être unique pour chaque entrée de transformation au sein de cette stratégie.

**TransformationMethod :** élément TransformationMethod de hello identifie l’opération donnée effectuée toogenerate hello pour hello revendication.

Selon la méthode hello choisie, un ensemble d’entrées et sorties est attendu. Ils sont définis à l’aide de hello **InputClaims**, **InputParameters** et **OutputClaims** éléments.

#### <a name="table-4-transformation-methods-and-expected-inputs-and-outputs"></a>Tableau 4 : méthodes de transformation et entrées et sorties attendues
|Méthode de transformation|Entrée attendue|Sortie attendue|Description|
|-----|-----|-----|-----|
|Join|string1, string2, séparateur|outputClaim|Joint les chaînes d’entrée à l’aide d’un séparateur. Par exemple : string1:"foo@bar.com", string2:"sandbox", separator:"." produit outputClaim:"foo@bar.com.sandbox"|
|ExtractMailPrefix|mail|outputClaim|Extrait la partie locale de hello d’une adresse e-mail. Par exemple : mail:"foo@bar.com" produit outputClaim:"foo". Si aucun @ signe est présent, puis de la chaîne d’entrée de replacer hello est retourné tel.|

**InputClaims :** utiliser un InputClaims élément toopass hello de données à partir d’une transformation de revendication schéma entrée tooa. Il possède deux attributs : **ClaimTypeReferenceId** et **TransformationClaimType**.

- **ClaimTypeReferenceId** est jointe à un élément ID de hello revendication schéma entrée toofind hello approprié revendication d’entrée. 
- **TransformationClaimType** toogive utilisé n’est une entrée de toothis de nom unique. Ce nom doit correspondre à une des entrées hello attendu pour la méthode de transformation hello.

**InputParameters :** utiliser un toopass d’élément InputParameters une transformation tooa de valeur constante. Il possède deux attributs : **Value** et **ID**.

- **Valeur** hello réelle valeur constante toobe passé.
- **ID** toogive utilisé n’est une entrée de toothis de nom unique. Ce nom doit correspondre à une des entrées hello attendu pour la méthode de transformation hello.

**OutputClaims :** utilisez un OutputClaims élément toohold hello données générées par une transformation et pouvoir le lier une entrée de schéma tooa revendication. Il possède deux attributs : **ClaimTypeReferenceId** et **TransformationClaimType**.

- **ClaimTypeReferenceId** est jointe avec l’ID de hello d’entrée schéma de hello revendication toofind hello une revendication de sortie appropriée.
- **TransformationClaimType** toogive utilisé n’est une sortie de toothis de nom unique. Ce nom doit correspondre à une des sorties hello attendu pour la méthode de transformation hello.

### <a name="exceptions-and-restrictions"></a>Exceptions et restrictions

**NameID de SAML et UPN :** hello les attributs à partir de laquelle vous source les valeurs NameID et UPN hello et hello transformations qui sont autorisées, les revendications sont limités.

#### <a name="table-5-attributes-allowed-as-a-data-source-for-saml-nameid"></a>Tableau 5 : attributs autorisés en tant que sources de données pour NameID SAML
|Source|ID|Description|
|-----|-----|-----|
|Utilisateur|mail|Adresse de messagerie|
|Utilisateur|userPrincipalName|Nom d’utilisateur principal|
|Utilisateur|onpremisessamaccountname|Nom de compte Sam local|
|Utilisateur|employeeid|ID d’employé|
|Utilisateur|extensionattribute1|Attribut d’extension 1|
|Utilisateur|extensionattribute2|Attribut d’extension 2|
|Utilisateur|extensionattribute3|Attribut d’extension 3|
|Utilisateur|extensionattribute4|Attribut d’extension 4|
|Utilisateur|extensionattribute5|Attribut d’extension 5|
|Utilisateur|extensionattribute6|Attribut d’extension 6|
|Utilisateur|extensionattribute7|Attribut d’extension 7|
|Utilisateur|extensionattribute8|Attribut d’extension 8|
|Utilisateur|extensionattribute9|Attribut d’extension 9|
|Utilisateur|extensionattribute10|Attribut d’extension 10|
|Utilisateur|extensionattribute11|Attribut d’extension 11|
|Utilisateur|extensionattribute12|Attribut d’extension 12|
|Utilisateur|extensionattribute13|Attribut d’extension 13|
|Utilisateur|extensionattribute14|Attribut d’extension 14|
|Utilisateur|extensionattribute15|Attribut d’extension 15|

#### <a name="table-6-transformation-methods-allowed-for-saml-nameid"></a>Tableau 6 : méthodes de transformation autorisées pour NameID SAML
|Méthode de transformation|Restrictions|
| ----- | ----- |
|ExtractMailPrefix|Aucune|
|Join|suffixe Hello jointe doit être un domaine vérifié du client de ressource hello.|

### <a name="custom-signing-key"></a>Clé de signature personnalisée
Toohello objet principal de service pour un effet tootake de stratégie de mappage de revendications doit être affectée à une clé de signature personnalisée. Tous les jetons émis qui ont été affectés par la stratégie de hello sont signés avec cette clé. Les applications doivent être tooaccept configuré les jetons signés avec cette clé. Cela garantit que les jetons ont été modifiés par le créateur de hello Hello un accusé de réception de revendications stratégie de mappage. Cela protège les applications contre des stratégies de mappage de revendications créées par des acteurs malveillants.

### <a name="cross-tenant-scenarios"></a>Scénarios inter-locataires
Stratégies de mappage ne s’appliquent pas aux utilisateurs de tooguest de revendications. Si un utilisateur invité tente tooaccess une application avec des revendications de mappage stratégie attribuée tooits service principal, jeton de valeur par défaut de hello est publié (stratégie de hello n’a aucun effet).

## <a name="claims-mapping-policy-assignment"></a>Attribution de stratégie de mappage de revendications
Stratégies de mappage ne peuvent être assignées tooservice des objets principal de revendications.

### <a name="example-claims-mapping-policies"></a>Exemples de stratégies de mappage de revendications

Dans Azure AD, de nombreux scénarios sont possibles où vous pouvez personnaliser des revendications émises dans des jetons pour des principaux du service spécifiques. Dans cette section, nous guider quelques scénarios courants qui peuvent vous aider à comprendre comment toouse hello déclare le type de stratégie de mappage.

#### <a name="prerequisites"></a>Composants requis
Bonjour exemple suivant, vous créez, mettre à jour, liez et supprimez des stratégies pour les principaux de service. Si vous êtes de nouveau tooAzure AD, nous vous recommandons que vous découvrez comment tooget une annonce Azure client avant de procéder à ces exemples. 

tooget démarré, hello comme suit :


1. Télécharger le dernier hello [version préliminaire publique de Module PowerShell Azure AD](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.127).
2.  Exécutez hello Connect commande toosign dans tooyour compte d’administrateur Azure AD. Exécutez cette commande chaque fois que vous démarrez une nouvelle session.
    
     ``` powershell
    Connect-AzureAD -Confirm
    
    ```
3.  toosee toutes les stratégies qui ont été créés dans votre organisation, hello exécution suivant la commande. Nous vous recommandons d’exécuter cette commande après la plupart des opérations Bonjour suivant des scénarios, toocheck vos stratégies sont créés en tant que prévu.
   
    ``` powershell
        Get-AzureADPolicy
    
    ```
#### <a name="example-create-and-assign-a-policy-tooomit-hello-basic-claims-from-tokens-issued-tooa-service-principal"></a>Exemple : Créer et attribuer une stratégie tooomit hello base de revendications à partir de principal du service tooa jetons émis.
Dans cet exemple, vous créez une stratégie qui supprime les ensemble de revendications basic de hello toolinked des jetons émis principaux de service.


1. Créez une stratégie de mappage de revendications. Cette stratégie, les principaux du service lié toospecific, supprime hello revendication base ensemble de jetons.
    1. stratégie de hello toocreate, exécutez la commande suivante : 
    
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"false"}}') -DisplayName "OmitBasicClaims” -Type "ClaimsMappingPolicy"
    ```
    2. toosee votre nouvelle stratégie et tooget hello stratégie ObjectId, hello exécution suivant de commandes :
    
     ``` powershell
    Get-AzureADPolicy
    ```
2.  Affecter le principal du service tooyour hello stratégie. Vous devez également tooget hello ObjectId de votre principal de service. 
    1.  toosee principaux de service d’ensemble de l’entreprise, vous pouvez interroger Microsoft Graph. Ou, dans l’Explorateur d’Azure AD Graph, connectez-vous tooyour compte Azure AD.
    2.  Lorsque vous avez hello ObjectId de votre hello service principal, exécutez commande suivante :  
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
    ```
#### <a name="example-create-and-assign-a-policy-tooinclude-hello-employeeid-and-tenantcountry-as-claims-in-tokens-issued-tooa-service-principal"></a>Exemple : Créer et affecter un tooinclude stratégie hello EmployeeID et TenantCountry comme tooa principal du service d’émission des revendications dans les jetons.
Dans cet exemple, vous créez une stratégie qui ajoute hello EmployeeID et TenantCountry tootokens émis toolinked principaux de service. Hello EmployeeID est émis en tant que type de revendication de nom hello dans les jetons SAML et les jetons Web JSON. Hello TenantCountry est émis comme pays de hello revendication dans les jetons SAML et les jetons Web JSON. Dans cet exemple, nous continuons de demandes de basic de hello tooinclude définies dans les jetons hello.

1. Créez une stratégie de mappage de revendications. Cette stratégie, les principaux du service lié toospecific, ajoute hello EmployeeID et TenantCountry tootokens de revendications.
    1. stratégie de hello toocreate, exécutez la commande suivante :  
     
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"true", "ClaimsSchema": [{"Source":"user","ID":"employeeid","SamlClaimType":"http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name","JwtClaimType":"name"},{"Source":"company","ID":" tenantcountry ","SamlClaimType":" http://schemas.xmlsoap.org/ws/2005/05/identity/claims/country ","JwtClaimType":"country"}]}}') -DisplayName "ExtraClaimsExample” -Type "ClaimsMappingPolicy"
    ```
    
    2. toosee votre nouvelle stratégie et tooget hello stratégie ObjectId, hello exécution suivant de commandes :
     
     ``` powershell  
    Get-AzureADPolicy
    ```
2.  Affecter le principal du service tooyour hello stratégie. Vous devez également tooget hello ObjectId de votre principal de service. 
    1.  toosee principaux de service d’ensemble de l’entreprise, vous pouvez interroger Microsoft Graph. Ou, dans l’Explorateur d’Azure AD Graph, connectez-vous tooyour compte Azure AD.
    2.  Lorsque vous avez hello ObjectId de votre hello service principal, exécutez commande suivante :  
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
    ```
#### <a name="example-create-and-assign-a-policy-that-uses-a-claims-transformation-in-tokens-issued-tooa-service-principal"></a>Exemple : Créer et attribuer une stratégie qui utilise une transformation des revendications dans les jetons émis principal du service tooa.
Dans cet exemple, vous créez une stratégie qui émet une revendication personnalisée « JoinedData » tooJWTs émis toolinked principaux du service. Cette revendication contient une valeur créée en joignant les données hello stockées dans l’attribut d’extensionattribute1 hello sur l’objet d’utilisateur de hello ayant « .sandbox ». Dans cet exemple, les demandes de basic de hello définies dans les jetons hello est exclue.


1. Créez une stratégie de mappage de revendications. Cette stratégie, les principaux du service lié toospecific, ajoute hello EmployeeID et TenantCountry tootokens de revendications.
    1. stratégie de hello toocreate, exécutez la commande suivante : 
     
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"true", "ClaimsSchema":[{"Source":"user","ID":"extensionattribute1"},{"Source":"transformation","ID":"DataJoin","TransformationId":"JoinTheData","JwtClaimType":"JoinedData"}],"ClaimsTransformation":[{"ID":"JoinTheData","TransformationMethod":"Join","InputClaims":[{"ClaimTypeReferenceId":"extensionattribute1","TransformationClaimType":"string1"}], "InputParameters": [{"Id":"string2","Value":"sandbox"},{"Id":"separator","Value":"."}],"OutputClaims":[{"ClaimTypeReferenceId":"DataJoin","TransformationClaimType":"outputClaim"}]}]}}') -DisplayName "TransformClaimsExample” -Type "ClaimsMappingPolicy"
    ```
    
    2. toosee votre nouvelle stratégie et tooget hello stratégie ObjectId, hello exécution suivant de commandes : 
     
     ``` powershell
    Get-AzureADPolicy
    ```
2.  Affecter le principal du service tooyour hello stratégie. Vous devez également tooget hello ObjectId de votre principal de service. 
    1.  toosee principaux de service d’ensemble de l’entreprise, vous pouvez interroger Microsoft Graph. Ou, dans l’Explorateur d’Azure AD Graph, connectez-vous tooyour compte Azure AD.
    2.  Lorsque vous avez hello ObjectId de votre hello service principal, exécutez commande suivante : 
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
    ```
