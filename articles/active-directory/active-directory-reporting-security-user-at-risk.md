---
title: "aaaUsers signalées pour le rapport de sécurité risque dans le portail d’Azure Active Directory hello | Documents Microsoft"
description: "En savoir plus sur les utilisateurs hello signalées pour le rapport de sécurité risque dans le portail d’Azure Active Directory hello"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 5077cd61d6119745a85ed712623904633a151331
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="users-flagged-for-risk-security-report-in-hello-azure-active-directory-portal"></a>Utilisateurs marqués en vue d’état de sécurité risque dans le portail d’Azure Active Directory hello

Avec les rapports de sécurité hello Bonjour Azure Active Directory (Azure AD), vous pouvez obtenir probabilité hello de comptes d’utilisateur compromis dans votre environnement. 

Azure Active Directory détecte les actions suspectes qui sont des comptes d’utilisateur tooyour connexes. Pour chaque action détectée, un enregistrement appelé *événement à risque* est créé. Pour plus d’informations, consultez [Événements à risque dans Azure Active Directory](active-directory-identity-protection-risk-events.md). 

Hello détecté risque toocalculate utilisé :

- **Connexions risquées** -un risque de connexion est un indicateur pour une tentative de connexion qui ont peut-être été exécutée par une personne qui n’est pas propriétaire de légitime hello d’un compte d’utilisateur. Pour plus d’informations, consultez [Connexions risquées](active-directory-identityprotection.md#risky-sign-ins). 

- **Utilisateurs avec indicateur de risque** : il s’agit d’un compte d’utilisateur susceptible d’être compromis. Pour plus d’informations, consultez [Utilisateurs avec indicateur de risque](active-directory-identityprotection.md#users-flagged-for-risk).  

Bonjour portail Azure, vous pouvez trouver hello la sécurité des rapports sur hello **Azure Active Directory** panneau Bonjour **sécurité** section.  

![Connexions risquées](./media/active-directory-reporting-security-user-at-risk/10.png)



## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a>Licence Azure AD tooaccess un rapport de sécurité avez-vous besoin ?  

Toutes les éditions d’Azure Active Directory vous indiquent les rapports d’utilisateurs associés à un indicateur de risque.  
Toutefois, au niveau de granularité d’un rapport du hello varie entre les éditions de hello : 

- Bonjour **éditions Azure Active Directory gratuit et Basic**, vous obtenez déjà une liste d’utilisateurs avec indicateur de risque. 

- Hello **Azure Active Directory Premium 1** edition étend ce modèle en vous permettant également tooexamine certains hello sous-jacent des événements à risque qui ont été détectés pour chaque rapport. 

- Hello **Azure Active Directory Premium 2** vous offre une édition hello des informations plus détaillées sur tous les événements à risque sous-jacent et vous permet de stratégies de sécurité tooconfigure répondre automatiquement aux risques de tooconfigured niveaux.



## <a name="azure-active-directory-free-and-basic-edition"></a>Édition Azure Active Directory gratuite et de base

utilisateurs Hello signalées pour le rapport des risques dans les éditions gratuites et de base du Azure Active Directory hello vous fournit une liste des comptes d’utilisateur qui ont peut-être été compromis. 


![Connexions risquées](./media/active-directory-reporting-security-user-at-risk/03.png)

Sélection d’un utilisateur ouvre lame hello utilisateur connexes.
Pour les utilisateurs qui sont exposés, vous pouvez consulter les hello historique de l’utilisateur de connexion et réinitialiser le mot de passe de hello si nécessaire.

![Connexions risquées](./media/active-directory-reporting-security-user-at-risk/46.png)


Cette boîte de dialogue fournit une option permettant de :

- Télécharger des rapports de hello

- Rechercher des utilisateurs

![Connexions risquées](./media/active-directory-reporting-security-user-at-risk/16.png)


## <a name="azure-active-directory-premium-editions"></a>Éditions Premium d’Azure Active Directory

les utilisateurs Hello signalées pour le rapport des risques dans les éditions premium hello Azure Active Directory vous offre :

- Une [liste des comptes d’utilisateurs](active-directory-identityprotection.md#users-flagged-for-risk) qui ont peut-être été compromis 

- Agrégé des informations sur hello [risque de types d’événements](active-directory-identity-protection-risk-events.md) qui ont été détectées

- Un rapport de hello toodownload option

- Une option tooconfigure un [stratégie de mise à jour risque d’utilisateur](active-directory-identityprotection.md#user-risk-security-policy)  


![Connexions risquées](./media/active-directory-reporting-security-user-at-risk/71.png)

Lorsque vous sélectionnez un utilisateur, vous obtenez une vue de rapport détaillé pour cet utilisateur qui vous permet d’effectuer les opérations suivantes :

- Ouvrez hello que permet d’afficher toutes les connexions

- Réinitialiser le mot de passe de l’utilisateur hello

- Ignorer tous les événements

- Examiner les événements à risque signalé pour l’utilisateur de hello. 


![Connexions risquées](./media/active-directory-reporting-security-user-at-risk/324.png)


tooinvestigate un événement à risque, sélectionnez-en un dans hello de hello liste tooopen **détails** panneau pour cet événement risque. Sur hello **détails** panneau, vous avez hello option tooeither [fermeture manuelle d’un événement à risque](active-directory-identityprotection.md#closing-risk-events-manually) ou réactiver un événement risque fermé manuellement. 


![Connexions risquées](./media/active-directory-reporting-security-user-at-risk/325.png)



## <a name="next-steps"></a>Étapes suivantes

- Pour en savoir plus sur Azure Active Directory Identity Protection, voir [Protection de l’identité Azure Active Directory](active-directory-identityprotection.md).

