---
title: "aaaWriting Expressions pour les mappages d’attributs dans Azure Active Directory | Documents Microsoft"
description: "Découvrez comment les valeurs d’attribut de tootransform toouse expression mappages dans un format acceptable lors de la configuration automatique des objets d’application SaaS dans Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: b13c51cd-1bea-4e5e-9791-5d951a518943
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: markvi
ms.openlocfilehash: caa0dd8144f6e5279a869e015ed75bd24169d585
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="writing-expressions-for-attribute-mappings-in-azure-active-directory"></a>Écriture d’expressions pour les mappages d’attributs dans Azure Active Directory
Lorsque vous configurez la mise en service application SaaS de tooa, un des types hello de mappages d’attributs que vous pouvez spécifier est un mappage d’expression. Dans ce cas, vous devez écrire une expression de type script qui vous permet de tootransform les données de vos utilisateurs en formats plus acceptables pour l’application SaaS de hello.

## <a name="syntax-overview"></a>Vue d’ensemble de la syntaxe
syntaxe Hello des Expressions pour les mappages d’attributs est pas sans rappeler de Visual Basic pour les fonctions d’Applications (VBA).

* expression entière de Hello doit être définie en termes de fonctions, lesquelles sont constituées d’un nom suivi d’arguments entre parenthèses : <br>
  *NomDeFonction(&lt;&lt;argument 1&gt;&gt;,&lt;<argument N>&gt;)*
* Vous pouvez imbriquer des fonctions dans d’autres. Par exemple : <br> *FonctionUne(FonctionDeux(&lt;<argument1>&gt;))*
* Vous pouvez passer trois différents types d’arguments dans des fonctions :
  
  1. Des attributs, qui doivent être placés entre crochets. Par exemple : [nom_attribut]
  2. Des constantes de chaîne, qui doivent être placées entre des guillemets doubles. Par exemple : "États-Unis"
  3. D’autres fonctions. Par exemple : fonction_une (<<argument1>>, fonction_deux(<<argument2>>))
* Pour les constantes de chaîne, si vous avez besoin d’une barre oblique inverse (\) ou un guillemet (") dans la chaîne de hello, il doit être échappé avec le symbole de barre oblique inverse (\) hello. Par exemple : « Nom de la société : \"Contoso\" »

## <a name="list-of-functions"></a>Liste des fonctions
[Append](#append)&nbsp;&nbsp;&nbsp;&nbsp;[FormatDateTime](#formatdatetime)&nbsp;&nbsp;&nbsp;&nbsp;[Join](#join)&nbsp;&nbsp;&nbsp;&nbsp;[Mid](#mid)&nbsp;&nbsp;&nbsp;&nbsp;[Not](#not)&nbsp;&nbsp;&nbsp;&nbsp;[Replace](#replace)&nbsp;&nbsp;&nbsp;&nbsp;[StripSpaces](#stripspaces)&nbsp;&nbsp;&nbsp;&nbsp;[Switch](#switch)

- - -
### <a name="append"></a>Append
**Fonction :**<br> Append(source, suffixe)

**Description :**<br> Prend une valeur de chaîne source et ajoute la fin de toohello hello suffixe de celle-ci.

**Paramètres :**<br> 

| Nom | Requis / Répétition | Type | Remarques |
| --- | --- | --- | --- |
| **source** |Requis |String |En général, nom d’attribut hello à partir de l’objet de source de hello |
| **suffix** |Requis |String |chaîne Hello que vous souhaitez tooappend toohello valeur de fin de hello source. |

- - -
### <a name="formatdatetime"></a>FormatDateTime
**Fonction :**<br> FormatDateTime(source, inputFormat, outputFormat)

**Description :**<br> prend une chaîne de date dans un format et la convertit dans un autre format.

**Paramètres :**<br> 

| Nom | Requis / Répétition | Type | Remarques |
| --- | --- | --- | --- |
| **source** |Requis |String |En général, nom d’attribut hello à partir de l’objet de source de hello. |
| **inputFormat** |Requis |String |Format attendu de la valeur de la source hello. Pour plus d’informations sur les formats pris en charge, consultez [http://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx](http://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx). |
| **outputFormat** |Requis |String |Format de date de sortie hello. |

- - -
### <a name="join"></a>Join
**Fonction :**<br> Join(séparateur, source1, source2, …)

**Description :**<br> Join() est tooAppend() similaire, sauf qu’il peut combiner plusieurs **source** des valeurs de chaîne dans une chaîne unique, et chaque valeur doivent être séparé par un **séparateur** chaîne.

Si une des valeurs de la source hello est un attribut à valeurs multiples, toutes les valeurs de cet attribut sera la valeur de séparation de hello joints entre eux, séparées.

**Paramètres :**<br> 

| Nom | Requis / Répétition | Type | Remarques |
| --- | --- | --- | --- |
| **separator** |Requis |String |Chaîne utilisée tooseparate valeurs de la source lorsque celles-ci sont concaténées en une seule chaîne. Peut être "" si aucun séparateur n’est requis. |
| **source1  … sourceN ** |Requis, nombre de fois variable |String |Toobe de valeurs de chaîne joints entre eux. |

- - -
### <a name="mid"></a>Mid
**Fonction :**<br> Mid(source, début, longueur)

**Description :**<br> Retourne une sous-chaîne de la valeur de la source hello. Une sous-chaîne est une chaîne qui contient uniquement des caractères hello à partir de la chaîne source hello.

**Paramètres :**<br> 

| Nom | Requis / Répétition | Type | Remarques |
| --- | --- | --- | --- |
| **source** |Requis |String |En général, nom d’attribut de hello. |
| **start** |Requis |integer |Index Bonjour **source** chaîne où la sous-chaîne doit commencer. Premier caractère dans la chaîne de hello ont index égal à 1, le deuxième caractère ont des index 2 et ainsi de suite. |
| **length** |Requis |integer |Longueur de la sous-chaîne de hello. Si la longueur termine en dehors hello **source** chaîne, fonction renvoie la sous-chaîne de **Démarrer** index jusqu'à la fin **source** chaîne. |

- - -
### <a name="not"></a>not
**Fonction :**<br> Not(source)

**Description :**<br> Retournements hello une valeur booléenne de hello **source**. Si la valeur **source** est « *True* », cette fonction retourne «*False* ». Sinon, elle retourne «*True*».

**Paramètres :**<br> 

| Nom | Requis / Répétition | Type | Remarques |
| --- | --- | --- | --- |
| **source** |Requis |Chaîne de type Boolean |Les valeurs **sources** attendues sont « True » ou « False ». |

- - -
### <a name="replace"></a>Replace
**Fonction :**<br> ObsoleteReplace(source, oldValue, regexPattern, regexGroupName, replacementValue, replacementAttributeName, template)

**Description :**<br>
Remplace les valeurs dans une chaîne. Fonctionne différemment selon les paramètres hello fournis :

* Quand **oldValue** et **replacementValue** sont fournis :
  
  * Remplace toutes les occurrences de l’ancienne valeur de la source de hello replacementValue
* Quand **oldValue** et **template** sont fournis :
  
  * Remplace toutes les occurrences de hello **oldValue** Bonjour **modèle** avec hello **source** valeur
* Quand **oldValueRegexPattern**, **oldValueRegexGroupName** et **replacementValue** sont fournis :
  
  * Remplace toutes les valeurs correspondant à oldValueRegexPattern dans la chaîne source hello avec replacementValue
* Quand **oldValueRegexPattern**, **oldValueRegexGroupName** et **replacementPropertyName** sont fournis :
  
  * Si **source** a une valeur, **source** est retourné.
  * Si **source** n’a aucune valeur, utilise **oldValueRegexPattern** et **oldValueRegexGroupName** tooextract valeur de remplacement à partir de la propriété hello avec  **replacementPropertyName**. Valeur de remplacement est retournée comme résultat de hello

**Paramètres :**<br> 

| Nom | Requis / Répétition | Type | Remarques |
| --- | --- | --- | --- |
| **source** |Requis |String |En général, nom d’attribut hello à partir de l’objet de source de hello. |
| **oldValue** |Facultatif |String |Valeur toobe remplacé dans **source** ou **modèle**. |
| **regexPattern** |Facultatif |String |Modèle Regex pour toobe de valeur hello remplacé dans **source**. Ou, lorsque replacementPropertyName est utilisé, valeur tooextract à partir de la propriété de remplacement de modèle. |
| **regexGroupName** |Facultatif |String |Nom du groupe hello à l’intérieur de **regexPattern**. Nous extrayons la valeur de ce groupe comme replacementValue à partir de la propriété de remplacement uniquement quand replacementPropertyName est utilisé. |
| **replacementValue** |Facultatif |String |Tooreplace nouvelle valeur ancienne avec. |
| **replacementAttributeName** |Facultatif |String |Nom de hello attribut toobe est utilisé pour la valeur de remplacement, lors de la source n’a aucune valeur. |
| **template** |Facultatif |String |Lorsque **modèle** valeur est fournie, nous allons nous intéresser **oldValue** dans hello modèle et remplacez-la par la valeur de la source. |

- - -
### <a name="stripspaces"></a>StripSpaces
**Fonction :**<br> StripSpaces(source)

**Description :**<br> Supprime tous les espaces (« ») chaîne de caractères à partir de hello source.

**Paramètres :**<br> 

| Nom | Requis / Répétition | Type | Remarques |
| --- | --- | --- | --- |
| **source** |Requis |String |**source** tooupdate de valeur. |

- - -
### <a name="switch"></a>Switch
**Fonction :**<br> Switch(source, defaultValue, key1, value1, key2, value2, …)

**Description :**<br> quand la valeur **source** correspond à une **clé**, retourne la **valeur** de cette **clé**. Si la valeur **source** ne correspond à aucune clé, retourne **defaultValue**.  Les paramètres **key** et **value** doivent toujours être fournis par paires. fonction Hello attend toujours un nombre pair de paramètres.

**Paramètres :**<br> 

| Nom | Requis / Répétition | Type | Remarques |
| --- | --- | --- | --- |
| **source** |Requis |String |**Source** tooupdate de valeur. |
| **defaultValue** |Facultatif |String |Toobe de valeur par défaut utilisée lors de la source ne correspond pas à toutes les clés. Peut être une chaîne vide (""). |
| **key** |Requis |String |**Clé** toocompare **source** avec la valeur. |
| **value** |Requis |String |Valeur de remplacement pour hello **source** clé hello correspondante. |

## <a name="examples"></a>Exemples
### <a name="strip-known-domain-name"></a>Supprimer un nom de domaine connu
Vous devez toostrip un nom de domaine connu de tooobtain de messagerie d’un utilisateur un nom d’utilisateur. <br>
Par exemple, si le domaine de hello est « contoso.com », vous pouvez utiliser hello expression suivante :

**Expression :** <br>
`Replace([mail], "@contoso.com", , ,"", ,)`

**Exemple d’entrée/sortie :** <br>

* **ENTRÉE** (e-mail) : "john.doe@contoso.com"
* **SORTIE** : « john.doe »

### <a name="append-constant-suffix-toouser-name"></a>Ajouter le nom de suffixe de constante toouser
Si vous utilisez un bac à sable Salesforce, vous devrez peut-être tooappend un tooall suffixe supplémentaire à vos noms d’utilisateur avant de les synchroniser.

**Expression :** <br>
`Append([userPrincipalName], ".test"))`

**Exemple d’entrée/sortie :** <br>

* **ENTRÉE** : (userPrincipalName) : "John.Doe@contoso.com"
* **SORTIE**:  "John.Doe@contoso.com.test"

### <a name="generate-user-alias-by-concatenating-parts-of-first-and-last-name"></a>Générer des alias d’utilisateurs en concaténant des parties du prénom et du nom
Vous devez toogenerate un alias de l’utilisateur en prenant les 3 premières lettres du prénom de l’utilisateur et les 5 premières lettres du nom de l’utilisateur.

**Expression :** <br>
`Append(Mid([givenName], 1, 3), Mid([surname], 1, 5))`

**Exemple d’entrée/sortie :** <br>

* **ENTRÉE** (givenName): « John »
* **ENTRÉE** (surname) : « Doe »
* **SORTIE** : « JohDoe »

### <a name="output-date-as-a-string-in-a-certain-format"></a>Sortir une date sous la forme d’une chaîne dans un certain format
Vous souhaitez application de SaaS tooa toosend dates dans un format donné. <br>
Par exemple, vous souhaitez tooformat dates pour ServiceNow.

**Expression :** <br>

`FormatDateTime([extensionAttribute1], "yyyyMMddHHmmss.fZ", "yyyy-MM-dd")`

**Exemple d’entrée/sortie :**

* **ENTRÉE** (extensionAttribute1) : « 20150123105347.1Z »
* **SORTIE** : « 2015-01-23 »

### <a name="replace-a-value-based-on-predefined-set-of-options"></a>Remplacer une valeur en fonction d’un ensemble d’options prédéfini
Vous devez horaire toodefine hello d’utilisateur hello basée sur du code d’état hello stocké dans Azure AD. <br>
Si le code d’état hello ne correspond pas à une des options de hello prédéfinie, utilisez la valeur par défaut « Australie/Sydney ».

**Expression :** <br>

`Switch([state], "Australia/Sydney", "NSW", "Australia/Sydney","QLD", "Australia/Brisbane", "SA", "Australia/Adelaide")`

**Exemple d’entrée/sortie :**

* **ENTRÉE** (state) : « QLD »
* **SORTIE**: « Australia/Brisbane »

## <a name="related-articles"></a>Articles connexes
* [Index d’articles pour la gestion des applications dans Azure Active Directory](active-directory-apps-index.md)
* [Automatiser la configuration d’utilisateur/Deprovisioning tooSaaS applications](active-directory-saas-app-provisioning.md)
* [Personnalisation des mappages d’attributs pour l’approvisionnement des utilisateurs](active-directory-saas-customizing-attribute-mappings.md)
* [Filtres d’étendue pour l’approvisionnement des utilisateurs](active-directory-saas-scoping-filters.md)
* [SCIM tooenable la configuration automatique des utilisateurs et groupes à partir d’Azure Active Directory tooapplications](active-directory-scim-provisioning.md)
* [Notifications d’approvisionnement de comptes](active-directory-saas-account-provisioning-notifications.md)
* [Liste des didacticiels sur la façon de tooIntegrate applications SaaS](active-directory-saas-tutorial-list.md)

