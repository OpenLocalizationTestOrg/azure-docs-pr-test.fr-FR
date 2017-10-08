---
title: "référence de l’API de rapport d’activité aaaAzure connexion dans Active Directory | Documents Microsoft"
description: "Informations de référence pour le rapport d’activité hello signe dans Azure Active Directory API"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ddcd9ae0-f6b7-4f13-a5e1-6cbf51a25634
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 8123f308a291503f2c61ac5de26696806c6402ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-sign-in-activity-report-api-reference"></a>Référence d’API de création de rapports sur l’activité de connexion Azure Active Directory
Cette rubrique fait partie d’une collection de rubriques hello Azure Active Directory sur les API de création de rapports.  
Création de rapports Azure AD fournit une API qui vous permet de tooaccess données de rapport activité de connexion à l’aide de code ou les outils connexes.
Hello cette rubrique traite de tooprovide des informations de référence sur hello **API de rapport d’activité de connexion**.

Consultez l'article :

* [Activités de connexion](active-directory-reporting-azure-portal.md#activity-reports) pour plus d’informations conceptuelles
* [Prise en main de hello API Azure Active Directory Reporting](active-directory-reporting-api-getting-started.md) pour plus d’informations sur les API de création de rapports de hello.


## <a name="who-can-access-hello-api-data"></a>Qui peut accéder à des données d’API hello ?
* Les utilisateurs et principaux du Service de rôle d’administrateur de la sécurité ou de sécurité Reader hello
* Administrateurs généraux
* N’importe quelle application qui a l’autorisation tooaccess hello API (autorisation de l’application peut être configurés uniquement en fonction d’autorisation de l’administrateur Global)

accès tooconfigure pour un application tooaccess API de sécurité comme les événements d’ouverture de session, hello utilisation suivant des applications de hello tooadd PowerShell Principal du Service dans le rôle de sécurité Reader hello

```PowerShell
Connect-MsolService
$servicePrincipal = Get-MsolServicePrincipal -AppPrincipalId "<app client id>"
$role = Get-MsolRole | ? Name -eq "Security Reader"
Add-MsolRoleMember -RoleObjectId $role.ObjectId -RoleMemberType ServicePrincipal -RoleMemberObjectId $servicePrincipal.ObjectId
```

## <a name="prerequisites"></a>Composants requis
Ce rapport par le biais de tooaccess hello API de création de rapports, vous devez avoir :

* Une [édition Azure Active Directory Premium P1 ou P2](active-directory-editions.md)
* Hello terminé [API reporting de conditions préalables tooaccess hello Azure AD](active-directory-reporting-api-prerequisites.md). 

## <a name="accessing-hello-api"></a>L’accès aux API de hello
Vous pouvez soit accéder à cette API via hello [Explorateur graphique](https://graphexplorer2.cloudapp.net) ou par programmation à l’aide, par exemple, PowerShell. Dans l’ordre pour PowerShell toocorrectly interpréter la syntaxe de filtre OData hello utilisée dans les appels de Graph AAD REST, vous devez utiliser hello backtick (aka : accent grave) caractère trop « caractère d’échappement « hello $. sert de caractère de guillemet inversé Hello [caractère d’échappement de PowerShell](https://technet.microsoft.com/library/hh847755.aspx), ce qui permet de PowerShell toodo une interprétation littéral de caractère de $ hello et éviter toute confusion entre elle en tant que nom d’une variable PowerShell (ie : $filter).

Hello de cette rubrique concerne les hello Explorateur graphique. Pour obtenir un exemple PowerShell, consultez ce [script PowerShell](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script).

## <a name="api-endpoint"></a>Point de terminaison d’API
Vous pouvez accéder à cette API à l’aide de hello suivant l’URI de base :  

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta  



En raison de toohello le volume de données, cette API a une limite d’un million d’enregistrements retournés. 

Cet appel retourne les données de hello dans des lots. Chaque lot comporte un maximum de 1 000 enregistrements.  
tooget hello suivant lot d’enregistrements, utilisez hello de lien suivant. Obtenir hello [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) plus d’informations à partir de hello premier ensemble d’enregistrements retournés. jeton d’évitement Hello sera à fin hello hello du jeu de résultats.  

    https://graph.windows.net/$tenantdomain/activities/signinEvents?api-version=beta&%24skiptoken=-1339686058


## <a name="supported-filters"></a>Filtres pris en charge
Vous pouvez réduire nombre hello d’enregistrements retournés par une API appeler sous forme d’un filtre.  
Connectez-vous API hello suivant des filtres, les données associées sont prises en charge :

* **$top =\<retourné de nombre d’enregistrements toobe\>**  -nombre de hello toolimit d’enregistrements renvoyés. Il s’agit d’une opération coûteuse. Vous ne devez pas utiliser ce filtre si vous souhaitez tooreturn des milliers d’objets.  
* **$filter =\<votre instruction de filtrage\>**  -toospecify, sur la base de hello de champs de filtre pris en charge, type hello d’enregistrements qui vous intéressent

## <a name="supported-filter-fields-and-operators"></a>Opérateurs et champs de filtre pris en charge
type de hello toospecify d’enregistrements qui que vous intéressent, vous pouvez générer une instruction de filtrage qui peut contenir un ou une combinaison de hello suivant des champs de filtre :

* [signinDateTime](#signindatetime) : définit une date ou une plage de dates
* [userId](#userid) -définit. un hello d’utilisateur spécifique en fonction de l’utilisateur
* [userPrincipalName](#userprincipalname) -définit le nom d’un utilisateur spécifique en fonction hello utilisateur utilisateur principal (UPN)
* [appId](#appid) -définit l’ID de l’application de hello une application spécifique en fonction
* [appDisplayName](#appdisplayname) -définit le nom d’affichage d’une application hello application spécifique en fonction
* [loginStatus](#loginStatus) -définit l’état de hello de connexions de hello (réussite / échec)

> [!NOTE]
> Lorsque vous utilisez l’Explorateur graphique, hello vous devez hello toouse correct de cas pour chaque lettre est vos champs de filtre.
> 
> 

toonarrow étendue hello Hello a retourné des données, vous pouvez créer des combinaisons de filtres de hello pris en charge et les champs de filtre. Par exemple, hello instruction suivante retourne hello top 10 enregistrements entre le 1er juillet 2016 et juillet 2016 de 6 :

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta&$top=10&$filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T00:00:00Z


- - -
### <a name="signindatetime"></a>signinDateTime
**Opérateurs pris en charge**: eq, ge, le, gt, lt

**Exemple**:

Utilisation d’une date spécifique

    $filter=signinDateTime+eq+2016-04-25T23:59:00Z    



Utilisation d’une plage de dates    

    $filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T17:05:21Z


**Remarques**:

paramètre de Hello datetime doit être au format UTC de hello 

- - -
### <a name="userid"></a>userId
**Opérateurs pris en charge**: eq

**Exemple**:

    $filter=userId+eq+’00000000-0000-0000-0000-000000000000’

**Remarques**:

Hello Id_utilisateur est une valeur de chaîne

- - -
### <a name="userprincipalname"></a>userPrincipalName
**Opérateurs pris en charge**: eq

**Exemple**:

    $filter=userPrincipalName+eq+'audrey.oliver@wingtiptoysonline.com' 


**Remarques**:

valeur Hello userPrincipalName est une valeur de chaîne

- - -
### <a name="appid"></a>appId
**Opérateurs pris en charge**: eq

**Exemple**:

    $filter=appId+eq+’00000000-0000-0000-0000-000000000000’



**Remarques**:

valeur Hello appId est une valeur de chaîne

- - -
### <a name="appdisplayname"></a>appDisplayName
**Opérateurs pris en charge**: eq

**Exemple**:

    $filter=appDisplayName+eq+'Azure+Portal' 


**Remarques**:

valeur Hello appDisplayName est une valeur de chaîne

- - -
### <a name="loginstatus"></a>loginStatus
**Opérateurs pris en charge**: eq

**Exemple**:

    $filter=loginStatus+eq+'1'  


**Remarques**:

Il existe deux options pour hello loginStatus : 0 - Réussite, 1 - Échec

- - -
## <a name="next-steps"></a>Étapes suivantes
* Voulez-vous toosee exemples pour les activités filtrées connectez-vous ? Extraire hello [exemples de rapports API d’activité de connexion Azure Active Directory](active-directory-reporting-api-sign-in-activity-samples.md).
* Voulez-vous tooknow plus d’informations sur les API de création de rapports hello Azure AD ? Consultez [prise en main de hello API Azure Active Directory Reporting](active-directory-reporting-api-getting-started.md).

