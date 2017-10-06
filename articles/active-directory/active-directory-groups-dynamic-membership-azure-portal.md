---
title: "l’appartenance au groupe dynamique aaaAttribute dans Azure Active Directory | Documents Microsoft"
description: "Comment toocreate avancée des règles pour l’appartenance au groupe dynamique, y compris les paramètres et les opérateurs de règle d’expression pris en charge."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: fb434cc2-9a91-4ebf-9753-dd81e289787e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8cd06ed70433eff65401c67d7351d5dcc12a9dd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-attribute-based-rules-for-dynamic-group-membership-in-azure-active-directory"></a>Créer des règles basées sur les attributs pour l’appartenance à un groupe dynamique dans Azure Active Directory
Dans Azure Active Directory (Azure AD), vous pouvez créer des règles avancées tooenable complexe basée sur les attributs d’appartenance dynamique pour les groupes. Cet article décrit en détail les attributs hello et règles de l’appartenance dynamique toocreate la syntaxe pour les utilisateurs ou périphériques.

Lorsque tous les attributs d’une modification de l’utilisateur ou périphérique, système de hello évalue toutes les règles de groupe dynamique dans un répertoire de toosee si la modification de hello déclencherait n’importe quel groupe ajoute ou supprime. Si un utilisateur ou un appareil respecte une règle d’un groupe, il est ajouté en tant que membre de ce groupe. Si elles ne répondent plus aux règles de hello, ils sont supprimés.

> [!NOTE]
> - Vous pouvez définir une règle d’appartenance dynamique sur les groupes de sécurité ou Office 365.
>
> - Cette fonctionnalité requiert une licence Azure AD Premium P1 pour chaque utilisateur membre tooat ajouté au moins un dynamique.
>
> - Vous pouvez créer un groupe dynamique pour les appareils ou utilisateurs, mais vous ne pouvez pas créer une règle qui contient à la fois des objets d’utilisateur et d’appareils.

> - Moment hello n’est pas possible de toocreate un groupe de périphériques en fonction de qui possède les attributs de l’utilisateur. Règles d’adhésion périphérique peuvent uniquement immédiate attributs de référence des objets de périphérique dans le répertoire de hello.

## <a name="toocreate-an-advanced-rule"></a>toocreate une règle avancée
1. Connectez-vous à toohello [centre d’administration Azure AD](https://aad.portal.azure.com) avec un compte qui est un administrateur global ou un administrateur de compte d’utilisateur.
2. Sélectionnez **Utilisateurs et groupes**.
3. Sélectionnez **Tous les groupes**.

   ![Panneau de groupes hello ouverture](./media/active-directory-groups-dynamic-membership-azure-portal/view-groups-blade.png)
4. Dans **Tous les groupes**, sélectionnez **Nouveau groupe**.

   ![Ajouter un nouveau groupe](./media/active-directory-groups-dynamic-membership-azure-portal/add-group-type.png)
5. Sur hello **groupe** panneau, entrez un nom et une description pour le nouveau groupe de hello. Sélectionnez un **type d’appartenance** du **utilisateur dynamique** ou **appareils dynamique**, selon si votre choix toocreate une règle pour les utilisateurs ou périphériques, puis sélectionnez **Ajouter des requêtes dynamiques**. Pour les attributs hello utilisées pour les règles de l’appareil, consultez [à l’aide de règles toocreate d’attributs pour les objets périphériques](#using-attributes-to-create-rules-for-device-objects).

   ![Ajouter une règle d’appartenance dynamique](./media/active-directory-groups-dynamic-membership-azure-portal/add-dynamic-group-rule.png)
6. Sur hello **règles d’appartenance dynamique** panneau, entrez votre règle dans hello **l’appartenance dynamique à ajouter de règle avancée** zone, appuyez sur entrée, puis sélectionnez **créer** bas hello Panneau de Hello.
7. Sélectionnez **créer** sur hello **groupe** groupe de panneau toocreate hello.

## <a name="constructing-hello-body-of-an-advanced-rule"></a>Construction de corps hello d’une règle avancée
Hello règle avancée que vous pouvez créer pour les appartenances dynamiques hello pour les groupes est essentiellement une expression binaire qui se compose de trois parties et génère un résultat true ou false. Hello trois parties sont :

* Paramètre de gauche (leftParameter)
* Opérateur binaire (binaryOperator)
* Constante de droite (rightConstant)

Une règle avancée complète ressemble toothis similaire : (leftParameter binaryOperator « RightConstant »), où hello ouverture et fermeture des parenthèses est facultative pour hello ensemble binaire de l’expression, des guillemets doubles sont facultatifs, requis uniquement pour hello droite constante lorsqu’il est la chaîne et la syntaxe de hello pour le paramètre de gauche hello est user.property. Une règle avancée peut se composer de plusieurs expressions binaires séparées par hello- et- ou et - les opérateurs logiques pas.

Hello Voici des exemples d’une règle avancée correctement construite :
```
(user.department -eq "Sales") -or (user.department -eq "Marketing")
(user.department -eq "Sales") -and -not (user.jobTitle -contains "SDE")
```
Pour hello complète la liste des paramètres pris en charge et les opérateurs de règle d’expression, consultez les sections ci-dessous. Pour les attributs hello utilisées pour les règles de l’appareil, consultez [à l’aide de règles toocreate d’attributs pour les objets périphériques](#using-attributes-to-create-rules-for-device-objects).

Hello total du corps de hello de votre règle avancée ne peut pas dépasser 2048 caractères.

> [!NOTE]
> Les opérations de chaîne et regex (expressions régulières) ne prennent pas en compte la casse. Vous pouvez également effectuer des vérifications de la valeur Null, en utilisant $null en tant que constante. Par exemple : user.department -eq $null.
> Les chaînes contenant des guillemets doubles doivent être placées dans une séquence d’échappement à l’aide du caractère « ' ». Par exemple : `"\`Sales".

## <a name="supported-expression-rule-operators"></a>Opérateurs de règle d’expression pris en charge
Hello tableau suivant répertorie tous les opérateurs de règle d’expression hello pris en charge et leur toobe syntaxe utilisé dans le corps de hello Hello règle avancée :

| Operator | Syntaxe |
| --- | --- |
| Non égal à |-ne |
| Égal à |-eq |
| Ne commence pas par |-notStartsWith |
| Commence par |-startsWith |
| Ne contient pas |-notContains |
| Contient |-contains |
| Ne correspond pas |-notMatch |
| Correspond |-match |
| Dans | -in |
| Pas dans | -notIn |

## <a name="operator-precedence"></a>Précédence des opérateurs

Tous les opérateurs sont répertoriés ci-dessous par priorité, de toohigher inférieur. Les opérateurs sur la même ligne ont la même priorité :
````
-any -all
-or
-and
-not
-eq -ne -startsWith -notStartsWith -contains -notContains -match –notMatch -in -notIn
````
Tous les opérateurs peuvent être utilisés avec ou sans le préfixe de trait d’union hello. Des parenthèses ne sont nécessaires que lorsque la priorité ne répond pas à vos besoins.
Par exemple :
```
   user.department –eq "Marketing" –and user.country –eq "US"
```
équivaut à :
```
   (user.department –eq "Marketing") –and (user.country –eq "US")
```
## <a name="using-hello--in-and--notin-operators"></a>À l’aide de hello - dans et les opérateurs notIn -

Si vous souhaitez que la valeur de hello toocompare d’un attribut utilisateur par rapport à un nombre de valeurs différentes, vous pouvez utiliser hello - dans les opérateurs notIn - ou. Voici un exemple à l’aide de hello - In, opérateur :
```
    user.department -In [ "50001", "50002", "50003", “50005”, “50006”, “50007”, “50008”, “50016”, “50020”, “50024”, “50038”, “50039”, “51100” ]
```
Notez que hello hello » [ » et «] » au début de hello et à la fin de la liste des valeurs hello. Cette condition a la valeur tooTrue de valeur hello user.department est égal à une des valeurs hello dans la liste de hello.


## <a name="query-error-remediation"></a>Correction d’erreur de requête
Hello tableau suivant répertorie les erreurs potentielles et comment toocorrect les s’ils se produisent

| Erreur d’analyse de requête | Utilisation incorrecte | Utilisation corrigée |
| --- | --- | --- |
| Erreur : attribut non pris en charge. |(user.invalidProperty -eq "Value") |(user.department -eq "value")<br/>Propriété doit correspondre à l’un de hello [prise en charge de la liste des propriétés](#supported-properties). |
| Erreur : l’opérateur n’est pas pris en charge sur l’attribut. |(user.accountEnabled -contains true) |(user.accountEnabled - eq true)<br/>La propriété est de type booléen. Utiliser des opérateurs de hello pris en charge (-eq ou - ne) sur un type booléen de hello au-dessus de liste. |
| Erreur : erreur de compilation de la requête. |(user.department -eq "Sales") -and (user.department -eq "Marketing")(user.userPrincipalName -match "*@domain.ext") |(user.department -eq "Sales") -and (user.department -eq "Marketing")<br/>Opérateur logique doit correspondre à l’un à partir de la liste des propriétés hello pris en charge ci-dessus. (user.userPrincipalName-correspond à «. *@domain.ext») ou (user.userPrincipalName-correspond à «@domain.ext$») erreur dans l’expression régulière. |
| Erreur : l’expression binaire n’est pas au format correct. |(user.department –eq “Sales”) (user.department -eq "Sales")(user.department-eq"Sales") |(user.accountEnabled -eq true) -and (user.userPrincipalName -contains "alias@domain")<br/>La requête comporte plusieurs erreurs. Une parenthèse n’est pas au bon endroit. |
| Erreur : une erreur inconnue s’est produite lors de la configuration des appartenances dynamiques. |(user.accountEnabled -eq "True" AND user.userPrincipalName -contains "alias@domain") |(user.accountEnabled -eq true) -and (user.userPrincipalName -contains "alias@domain")<br/>La requête comporte plusieurs erreurs. Une parenthèse n’est pas au bon endroit. |

## <a name="supported-properties"></a>Propriétés prises en charge
Hello Voici toutes les propriétés utilisateur hello que vous pouvez utiliser dans votre règle avancée :

### <a name="properties-of-type-boolean"></a>Propriétés de type booléen
Opérateurs autorisés

* -eq
* -ne

| Propriétés | Valeurs autorisées | Usage |
| --- | --- | --- |
| accountEnabled |true false |user.accountEnabled -eq true |
| dirSyncEnabled |true false |user.dirSyncEnabled -eq true |

### <a name="properties-of-type-string"></a>Propriétés de type chaîne
Opérateurs autorisés

* -eq
* -ne
* -notStartsWith
* -startsWith
* -contains
* -notContains
* -match
* -notMatch
* -in
* -notIn

| Propriétés | Valeurs autorisées | Usage |
| --- | --- | --- |
| city |Toute valeur de chaîne ou $null |(user.city -eq "value") |
| country |Toute valeur de chaîne ou $null |(user.country -eq "value") |
| companyName | Toute valeur de chaîne ou $null | (user.companyName -eq "value") |
| department |Toute valeur de chaîne ou $null |(user.department -eq "value") |
| displayName |Toute valeur de chaîne. |(user.displayName -eq "value") |
| facsimileTelephoneNumber |Toute valeur de chaîne ou $null |(user.facsimileTelephoneNumber -eq "value") |
| givenName |Toute valeur de chaîne ou $null |(user.givenName -eq "value") |
| jobTitle |Toute valeur de chaîne ou $null |(user.jobTitle -eq "value") |
| mail |Valeur de chaîne ou $null (adresse SMTP de l’utilisateur de hello) |(user.mail -eq "value") |
| mailNickName |Toute valeur de chaîne (alias de messagerie de l’utilisateur de hello) |(user.mailNickName -eq "value") |
| mobile |Toute valeur de chaîne ou $null |(user.mobile -eq "value") |
| objectId |GUID de l’objet utilisateur de hello |(user.objectId -eq "1111111-1111-1111-1111-111111111111") |
| onPremisesSecurityIdentifier | Identificateur de sécurité (SID) local pour les utilisateurs qui ont été synchronisés à partir des locaux toohello cloud. |(user.onPremisesSecurityIdentifier -eq "S-1-1-11-1111111111-1111111111-1111111111-1111111") |
| passwordPolicies |Aucune DisableStrongPassword DisablePasswordExpiration DisablePasswordExpiration, DisableStrongPassword |(user.passwordPolicies -eq "DisableStrongPassword") |
| physicalDeliveryOfficeName |Toute valeur de chaîne ou $null |(user.physicalDeliveryOfficeName -eq "value") |
| postalCode |Toute valeur de chaîne ou $null |(user.postalCode -eq "value") |
| preferredLanguage |Code ISO 639-1 |(user.preferredLanguage -eq "en-US") |
| sipProxyAddress |Toute valeur de chaîne ou $null |(user.sipProxyAddress -eq "value") |
| state |Toute valeur de chaîne ou $null |(user.state -eq "value") |
| streetAddress |Toute valeur de chaîne ou $null |(user.streetAddress -eq "value") |
| surname |Toute valeur de chaîne ou $null |(user.surname -eq "value") |
| telephoneNumber |Toute valeur de chaîne ou $null |(user.telephoneNumber -eq "value") |
| usageLocation |Paramètre régional à deux lettres |(user.usageLocation -eq "US") |
| userPrincipalName |Toute valeur de chaîne. |(user.userPrincipalName -eq "alias@domain") |
| userType |member guest $null |(user.userType -eq "Member") |

### <a name="properties-of-type-string-collection"></a>Propriétés de type collection de chaînes
Opérateurs autorisés

* -contains
* -notContains

| Propriétés | Valeurs autorisées | Usage |
| --- | --- | --- |
| otherMails |Toute valeur de chaîne. |(user.otherMails -contains "alias@domain") |
| proxyAddresses |SMTP: alias@domain smtp: alias@domain |(user.proxyAddresses -contains "SMTP: alias@domain") |

## <a name="multi-value-properties"></a>Propriétés à valeurs multiples
Opérateurs autorisés

* -un (satisfait lorsqu’au moins un élément dans la collection de hello correspond à la condition de hello)
* -toutes les (condition satisfaite lorsque tous les éléments de collection de hello correspond à la condition de hello)

| Propriétés | Valeurs | Usage |
| --- | --- | --- |
| assignedPlans |Chaque objet de collection de hello expose hello les propriétés de chaîne suivantes : capabilityStatus, service, servicePlanId |user.assignedPlans -any (assignedPlan.servicePlanId -eq "efb87545-963c-4e0d-99df-69c6916d9eb0" -et assignedPlan.capabilityStatus -eq "Enabled") |

Les propriétés à valeurs multiples sont des collections d’objets de hello même type. Vous pouvez utiliser - tooapply d’opérateurs tout et - tous les articles un tooone condition ou l’ensemble des hello dans la collection de hello, respectivement. Par exemple :

assignedPlans est une propriété à valeurs multiples qui répertorie tous les plans de service toohello utilisateur attribués. Hello ci-dessous expression permettent de sélectionner les utilisateurs qui ont hello Exchange Online (Plan 2) plan de service qui se trouve également dans l’état activé :

```
user.assignedPlans -any (assignedPlan.servicePlanId -eq "efb87545-963c-4e0d-99df-69c6916d9eb0" -and assignedPlan.capabilityStatus -eq "Enabled")
```

(identificateur de Guid hello identifie plan de service Exchange Online (Plan 2) hello.)

> [!NOTE]
> Cela est utile si vous souhaitez tooidentify tous les utilisateurs pour lesquels un Office 365 (ou un autre Service en ligne Microsoft) fonctionnalité a été activée pour l’exemple tootarget avec un certain jeu de stratégies.

Hello expression suivante sélectionne tous les utilisateurs qui disposent de tout plan de service qui est associé à hello service Intune (identifié par le nom du service « SCO ») :
```
user.assignedPlans -any (assignedPlan.service -eq "SCO" -and assignedPlan.capabilityStatus -eq "Enabled")
```

## <a name="use-of-null-values"></a>Utiliser des valeurs Null

toospecify une valeur null dans une règle, vous pouvez utiliser « null » ou $null. Exemple :
```
   user.mail –ne null
```
équivaut à :
```
   user.mail –ne $null
   ```

## <a name="extension-attributes-and-custom-attributes"></a>Attributs d’extension et attributs personnalisés
Les attributs d’extension et les attributs personnalisés sont pris en charge dans les règles d’appartenance dynamique.

Attributs d’extension sont synchronisés à partir du serveur Active Directory local et prennent format hello de « ExtensionAttributeX », où X est égal à 1-15.
Voici en exemple de règle utilisant un attribut d’extension :
```
(user.extensionAttribute15 -eq "Marketing")
```
Attributs personnalisés sont synchronisés à partir d’Active Directory du serveur Windows local ou à partir de la connecté SaaS d’application et hello hello sous le format « user.extension_[GUID]\__ [Attribute] », où [GUID] est hello identificateur unique dans AAD application hello qui attribut hello créé dans AAD et [Attribute] est nom hello d’attribut de hello telle qu’elle a été créée.
Voici un exemple de règle utilisant un attribut personnalisé :
```
user.extension_c272a57b722d4eb29bfe327874ae79cb__OfficeNumber  
```
Hello nom d’attribut personnalisé peut être trouvé dans le répertoire de hello en interrogeant un utilisateur de l’attribut à l’aide de l’Explorateur graphique et la recherche de nom de l’attribut hello.

## <a name="direct-reports-rule"></a>Règle de « collaborateurs directs »
Vous pouvez créer un groupe contenant tous les collaborateurs directs d’un responsable. Lorsque les rapports directs du responsable hello changent dans hello futures, les membres de groupe hello seront ajustées automatiquement.

> [!NOTE]
> 1. Pour hello règle toowork, vérifiez que hello **Manager ID** propriété est correctement définie sur les utilisateurs de votre client. Vous pouvez vérifier la valeur actuelle de hello pour un utilisateur sur leurs **onglet profil**.
> 2. Cette règle prend uniquement en charge les collaborateurs **directs**. Il n’est actuellement pas possible de toocreate un groupe pour une hiérarchie imbriquée, par exemple, un groupe qui inclut les collaborateurs directs et les rapports.

**groupe de hello tooconfigure**

1. Suivez les étapes 1 à 5 de la section [toocreate hello de règle avancée](#to-create-the-advanced-rule), puis sélectionnez un **type d’appartenance** de **utilisateur dynamique**.
2. Sur hello **règles d’appartenance dynamique** panneau, entrez la règle de hello avec hello selon la syntaxe :

    *Collaborateurs directs pour {ID objet_du_responsable}*

    Exemple de règle valide :
```
                    Direct Reports for "62e19b97-8b3d-4d4a-a106-4ce66896a863"
```
    where “62e19b97-8b3d-4d4a-a106-4ce66896a863” is hello objectID of hello manager. hello object ID can be found on manager's **Profile tab**.
3. Après avoir enregistré la règle de hello, tous les utilisateurs avec hello spécifié de valeur d’ID de gestionnaire sera ajoutée toohello groupe.

## <a name="using-attributes-toocreate-rules-for-device-objects"></a>À l’aide de règles toocreate d’attributs pour les objets périphériques
Vous pouvez également créer une règle qui sélectionne des objets d’appareil pour l’appartenance à un groupe. Hello suivant des attributs d’appareil peut être utilisé.

 Attribut d’appareil  | Valeurs | Exemple
 ----- | ----- | ----------------
 accountEnabled | true false | (device.accountEnabled -eq true)
 displayName | Toute valeur de chaîne. |(device.displayName -eq "Rob Iphone”)
 deviceOSType | Toute valeur de chaîne. | (device.deviceOSType -eq "IOS")
 deviceOSVersion | Toute valeur de chaîne. | (device.OSVersion -eq "9.1")
 deviceCategory | Un nom de catégorie d’appareil valide. | (device.deviceCategory -eq "BYOD")
 deviceManufacturer | Toute valeur de chaîne. | (device.deviceManufacturer -eq "Samsung")
 deviceModel | Toute valeur de chaîne. | (device.deviceModel -eq "iPad Air")
 deviceOwnership | Personnel, Entreprise | (device.deviceOwnership -eq "Company")
 domainName | Toute valeur de chaîne. | (device.domainName -eq "contoso.com")
 enrollmentProfileName | Nom de profil de l’inscription d’appareil Apple. | (device.enrollmentProfileName -eq "DEP iPhones")
 isRooted | true false | (device.isRooted -eq true)
 managementType | Gestion des périphériques mobiles (pour les appareils mobiles).<br>PC (pour les ordinateurs gérés par agent des PC Intune hello) | (device.managementType -eq "MDM")
 organizationalUnit | toute valeur de chaîne correspondant au nom hello d’unité d’organisation hello définie par un annuaire local Active Directory. | (device.organizationalUnit -eq "US PCs")
 deviceId | Un ID d’appareil Azure AD valide. | (device.deviceId -eq "d4fe7726-5966-431c-b3b8-cddc8fdb717d")
 objectId | Un ID d’objet Azure AD valide. |  (device.objectId -eq 76ad43c9-32c5-45e8-a272-7b58b58f596d")




## <a name="next-steps"></a>Étapes suivantes
Ces articles fournissent des informations supplémentaires sur les groupes dans Azure Active Directory.

* [Consulter les groupes existants](active-directory-groups-view-azure-portal.md)
* [Création d’un nouveau groupe et ajout de membres](active-directory-groups-create-azure-portal.md)
* [Gérer les paramètres d’un groupe](active-directory-groups-settings-azure-portal.md)
* [Gérer l’appartenance à un groupe](active-directory-groups-membership-azure-portal.md)
* [Gérer les règles dynamiques pour les utilisateurs dans un groupe](active-directory-groups-dynamic-membership-azure-portal.md)
