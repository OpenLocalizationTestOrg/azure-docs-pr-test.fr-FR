---
title: "audit d’Active Directory aaaAzure référence de l’API | Documents Microsoft"
description: "Comment tooget main hello API d’audit Azure Active Directory"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 44e46be8-09e5-4981-be2b-d474aaa92792
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 5f33b62ede9be445f35704739e328580dc454368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-audit-api-reference"></a>Référence d’API d’audit Azure Active Directory
Cette rubrique fait partie d’une collection de rubriques hello Azure Active Directory sur les API de création de rapports.  
Création de rapports Azure AD fournit une API qui vous permet de tooaccess les données d’audit à l’aide de code ou les outils connexes.
Hello cette rubrique traite de tooprovide des informations de référence sur hello **audit API**.

Consultez l'article :

* [Journaux d’audit](active-directory-reporting-azure-portal.md#activity-reports) pour plus d’informations conceptuelles

* [Prise en main de hello API Azure Active Directory Reporting](active-directory-reporting-api-getting-started.md) pour plus d’informations sur les API de création de rapports de hello.


Pour :

- Consulter les questions les plus fréquentes, lisez notre [FAQ](active-directory-reporting-faq.md). 

- En savoir plus les problèmes, consultez [Envoyer un ticket de support](active-directory-troubleshooting-support-howto.md). 


## <a name="who-can-access-hello-data"></a>Qui peut accéder à des données de salutation ?
* Utilisateurs dans le rôle d’administrateur de la sécurité ou de sécurité Reader hello
* Administrateurs généraux
* N’importe quelle application qui a l’autorisation tooaccess hello API (autorisation de l’application peut être configurés uniquement en fonction d’autorisation de l’administrateur Global)

## <a name="prerequisites"></a>Composants requis
Dans tooaccess commande par le biais de ce rapport hello API de création de rapports, vous devez avoir :

* Une [édition Azure Active Directory gratuite ou une édition récente](active-directory-editions.md)
* Hello terminé [API reporting de conditions préalables tooaccess hello Azure AD](active-directory-reporting-api-prerequisites.md). 

## <a name="accessing-hello-api"></a>L’accès aux API de hello
Vous pouvez soit accéder à cette API via hello [Explorateur graphique](https://graphexplorer2.cloudapp.net) ou par programmation à l’aide, par exemple, PowerShell. Dans l’ordre pour PowerShell toocorrectly interpréter la syntaxe de filtre OData hello utilisée dans les appels de Graph AAD REST, vous devez utiliser hello backtick (aka : accent grave) caractère trop « caractère d’échappement « hello $. sert de caractère de guillemet inversé Hello [caractère d’échappement de PowerShell](https://technet.microsoft.com/library/hh847755.aspx), ce qui permet de PowerShell toodo une interprétation littéral de caractère de $ hello et éviter toute confusion entre elle en tant que nom d’une variable PowerShell (ie : $filter).

Hello de cette rubrique concerne les hello Explorateur graphique. Pour obtenir un exemple PowerShell, consultez ce [script PowerShell](active-directory-reporting-api-audit-samples.md#powershell-script).

## <a name="api-endpoint"></a>Point de terminaison d’API
Vous pouvez accéder à cette API à l’aide de hello suivant l’URI :  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta

Il n’existe aucune limite sur le nombre de hello d’enregistrements retournés par l’API d’audit hello Azure AD (à l’aide de la pagination de OData).
Pour connaître les limites de rétention de données de rapports, consultez [Stratégies de rétention des rapports](active-directory-reporting-retention.md).

Cet appel retourne les données de hello dans des lots. Chaque lot comporte un maximum de 1 000 enregistrements.  
tooget hello suivant lot d’enregistrements, utilisez hello de lien suivant. Permet d’obtenir des informations de skiptoken hello hello premier ensemble d’enregistrements retournés. jeton d’évitement Hello sera à fin hello hello du jeu de résultats.  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta&%24skiptoken=-1339686058




## <a name="supported-filters"></a>Filtres pris en charge
Vous pouvez réduire nombre hello d’enregistrements retournés par une API appeler sous forme d’un filtre.  
Connectez-vous API hello suivant des filtres, les données associées sont prises en charge :

* **$top =\<retourné de nombre d’enregistrements toobe\>**  -nombre de hello toolimit d’enregistrements renvoyés. Il s’agit d’une opération coûteuse. Vous ne devez pas utiliser ce filtre si vous souhaitez tooreturn des milliers d’objets.     
* **$filter =\<votre instruction de filtrage\>**  -toospecify, sur la base de hello de champs de filtre pris en charge, type hello d’enregistrements qui vous intéressent

## <a name="supported-filter-fields-and-operators"></a>Opérateurs et champs de filtre pris en charge
type de hello toospecify d’enregistrements qui que vous intéressent, vous pouvez générer une instruction de filtrage qui peut contenir un ou une combinaison de hello suivant des champs de filtre :

* [activityDate](#activitydate) : définit une date ou une plage de dates
* [catégorie](#category) -définit hello catégorie toofilter sur.
* [activityStatus](#activitystatus) -définit l’état de hello d’une activité
* [type d’activité](#activitytype) -définit le type hello d’une activité
* [activité](#activity) -définit l’activité hello en tant que chaîne  
* [nom del’acteur/](#actorname) -définit l’acteur de hello sous forme de nom de hello acteur
* [acteur/objectid](#actorobjectid) -définit l’acteur de hello sous forme d’ID de hello acteur   
* [acteur/upn](#actorupn) -définit l’acteur de hello sous forme nom d’acteur hello d’utilisateur principal (UPN) 
* [nom de la cible](#targetname) -définit la cible de hello sous forme de nom de hello acteur
* [cible/objectid](#targetobjectid) -définit la cible de hello sous forme de hello ID cible  
* [cible/upn](#targetupn) -définit l’acteur de hello sous forme nom d’acteur hello d’utilisateur principal (UPN)   

- - -
### <a name="activitydate"></a>activityDate
**Opérateurs pris en charge**: eq, ge, le, gt, lt

**Exemple**:

    $filter=tdomain + 'activities/audit?api-version=beta&`$filter=activityDate gt ' + $7daysago    

**Remarques**:

datetime doit être au format UTC

- - -
### <a name="category"></a>category

**Valeurs prises en charge** :

| Catégorie                         | Valeur     |
| :--                              | ---       |
| Annuaire principal                   | Répertoire |
| Gestion des mots de passe en libre-service | SSPR      |
| Gestion des groupes en libre-service    | SSGM      |
| Approvisionnement des comptes             | Synchronisation      |
| Substitution de mot de passe automatique      | Substitution de mot de passe automatique |
| Identity Protection              | IdentityProtection |
| Utilisateurs invités                    | Utilisateurs invités |
| Service MIM                      | Service MIM |



**Opérateurs pris en charge**: eq

**Exemple**:

    $filter=category eq 'SSPR'
- - -
### <a name="activitystatus"></a>activityStatus

**Valeurs prises en charge** :

| État de l’activité | Valeur |
| :--             | ---   |
| Succès         | 0     |
| Échec         | - 1   |

**Opérateurs pris en charge**: eq

**Exemple**:

    $filter=activityStatus eq -1    

---
### <a name="activitytype"></a>activityType
**Opérateurs pris en charge**: eq

**Exemple**:

    $filter=activityType eq 'User'    

**Remarques**:

respecte la casse

- - -
### <a name="activity"></a>activity
**Opérateurs pris en charge**: eq, contains, startsWith

**Exemple**:

    $filter=activity eq 'Add application' or contains(activity, 'Application') or startsWith(activity, 'Add')    

**Remarques**:

respecte la casse

- - -
### <a name="actorname"></a>actor/name
**Opérateurs pris en charge**: eq, contains, startsWith

**Exemple**:

    $filter=actor/name eq 'test' or contains(actor/name, 'test') or startswith(actor/name, 'test')    

**Remarques**:

ne respecte pas la casse

- - -
### <a name="actorobjectid"></a>actor/objectid
**Opérateurs pris en charge**: eq

**Exemple**:

    $filter=actor/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba'    


- - -
### <a name="targetname"></a>target/name
**Opérateurs pris en charge**: eq, contains, startsWith

**Exemple**:

    $filter=targets/any(t: t/name eq 'some name')    

**Remarques**:

ne respecte pas la casse

- - -
### <a name="targetupn"></a>target/upn
**Opérateurs pris en charge**: eq, startsWith

**Exemple**:

    $filter=targets/any(t: startswith(t/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity/userPrincipalName,'abc'))    

**Remarques**:

* ne respecte pas la casse
* Vous avez besoin d’espace de noms complet tooadd hello lors de l’interrogation Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity

- - -
### <a name="targetobjectid"></a>target/objectid
**Opérateurs pris en charge**: eq

**Exemple**:

    $filter=targets/any(t: t/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba')    

- - -
### <a name="actorupn"></a>actor/upn
**Opérateurs pris en charge**: eq, startsWith

**Exemple**:

    $filter=startswith(actor/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity/userPrincipalName,'abc')    

**Remarques**:

* ne respecte pas la casse 
* Vous avez besoin d’espace de noms complet tooadd hello lors de l’interrogation Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity

- - -
## <a name="next-steps"></a>Étapes suivantes
* Voulez-vous toosee exemples pour les activités filtrées système ? Extraire hello [exemples d’API d’audit Azure Active Directory](active-directory-reporting-api-audit-samples.md).
* Voulez-vous tooknow plus d’informations sur les API de création de rapports hello Azure AD ? Consultez [prise en main de hello API Azure Active Directory Reporting](active-directory-reporting-api-getting-started.md).

