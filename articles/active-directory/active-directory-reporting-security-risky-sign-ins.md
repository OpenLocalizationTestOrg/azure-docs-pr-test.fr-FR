---
title: "rapport des connexions aaaRisky dans le portail d’Azure Active Directory hello | Documents Microsoft"
description: "En savoir plus sur les rapports de connexions risquée hello dans le portail d’Azure Active Directory hello"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: 7728fcd7-3dd5-4b99-a0e4-949c69788c0f
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d8df5cafea6b38f3e364c24a6aff599abe088e88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="risky-sign-ins-report-in-hello-azure-active-directory-portal"></a>Rapport des connexions présentant un risque dans le portail d’Azure Active Directory hello

Avec les rapports de sécurité hello dans Azure Active Directory (Azure AD) vous pouvez obtenir probabilité hello de comptes d’utilisateur compromis dans votre environnement. 

Azure AD détecte les actions suspectes qui sont des comptes d’utilisateur tooyour connexes. Pour chaque action détectée, un enregistrement appelé *événement à risque* est créé. Pour en savoir plus, voir [Événements à risque dans Azure Active Directory](active-directory-identity-protection-risk-events.md). 

Hello détecté risque toocalculate utilisé :

- **Connexions risquées** -un risque de connexion est un indicateur pour une tentative de connexion qui ont peut-être été exécutée par une personne qui n’est pas propriétaire de légitime hello d’un compte d’utilisateur. Pour en savoir plus, voir [Connexions risquées](active-directory-identityprotection.md#risky-sign-ins). 

- **Utilisateurs avec indicateur de risque** : il s’agit d’un compte d’utilisateur susceptible d’être compromis. Pour en savoir plus, voir [Utilisateurs avec indicateur de risque](active-directory-identityprotection.md#users-flagged-for-risk).  

Dans [hello portail Azure](https://portal.azure.com), vous pouvez trouver hello la sécurité des rapports sur hello **Azure Active Directory** panneau Bonjour **sécurité** section. 

![Connexions risquées](./media/active-directory-reporting-security-risky-sign-ins/10.png)


## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a>Licence Azure AD tooaccess un rapport de sécurité avez-vous besoin ?  

Toutes les éditions d’Azure Active Directory vous indiquent les rapports de connexions risquées.  
Toutefois, au niveau de granularité d’un rapport du hello varie entre les éditions de hello : 

- Bonjour **éditions Azure Active Directory gratuit et Basic**, vous obtenez déjà une liste de connexions présentant un risque. 

- Hello **Azure Active Directory Premium 1** edition étend ce modèle en vous permettant également tooexamine certains hello sous-jacent des événements à risque qui ont été détectés pour chaque rapport. 

- Hello **Azure Active Directory Premium 2** édition fournit des hello plus des informations détaillées sur tous les événements à risque sous-jacent et il vous permet également de stratégies de sécurité tooconfigure répondent automatiquement tooconfigured niveaux de risque.



## <a name="azure-active-directory-free-and-basic-edition"></a>Édition Azure Active Directory gratuite et de base

Hello Azure Active Directory gratuit et les éditions de base fournissent une liste de risquée connexions qui ont été détectées pour vos utilisateurs. Ce rapport répertorie :

- **Utilisateur** hello - nom de l’utilisateur hello qui a été utilisé pendant l’opération de connexion hello
- **IP** -hello l’adresse IP du périphérique hello qui a été utilisé tooconnect tooAzure Active Directory
- **Emplacement** -emplacement de hello utilisé tooconnect tooAzure Active Directory
- **L’heure** -hello heure hello connectez-vous
- **État** -hello l’état de la connexion au hello


![Connexions risquées](./media/active-directory-reporting-security-risky-sign-ins/01.png)

Selon votre examen de hello risquée connectez-vous, vous pouvez fournir des commentaires tooAzure Active Directory sous forme de hello suivant des actions :

- Résoudre
- Marquer comme faux positif
- Ignorer
- Réactiver

![Connexions risquées](./media/active-directory-reporting-security-risky-sign-ins/21.png)

Pour en savoir plus, voir [Fermeture manuelle des événements à risque](active-directory-identityprotection.md#closing-risk-events-manually).

Ce rapport fournit une option permettant de :

- Rechercher des ressources
- Télécharger des données de rapport hello


![Connexions risquées](./media/active-directory-reporting-security-risky-sign-ins/93.png)


## <a name="azure-active-directory-premium-editions"></a>Éditions Premium d’Azure Active Directory

rapport des connexions risquée Hello dans les éditions premium hello Azure Active Directory vous offre :

- Agrégé des informations sur hello [risque de types d’événements](active-directory-identity-protection-risk-events.md) qui ont été détectées

- Un rapport de hello toodownload option


![Connexions risquées](./media/active-directory-reporting-security-risky-sign-ins/456.png)


Lorsque vous sélectionnez un événement à risque, vous obtenez une vue de rapport détaillé pour cet événement à risque qui vous permet d’effectuer les opérations suivantes :

- Une option tooconfigure un [stratégie de mise à jour risque d’utilisateur](active-directory-identityprotection.md#user-risk-security-policy)  

- Passez en revue la chronologie de la détection de hello pour un événement à risque hello  

- Passer en revue la liste des utilisateurs pour lesquels cet événement à risque a été détecté

- [Fermer manuellement les événements à risque](active-directory-identityprotection.md#closing-risk-events-manually) ou réactiver un événement à risque fermé manuellement. 


![Connexions risquées](./media/active-directory-reporting-security-risky-sign-ins/457.png)

Lorsque vous sélectionnez un utilisateur, vous obtenez une vue de rapport détaillé pour cet utilisateur qui vous permet d’effectuer les opérations suivantes :

- Ouvrez hello que permet d’afficher toutes les connexions

- Réinitialiser le mot de passe de l’utilisateur hello

- Ignorer tous les événements

- Examiner les événements à risque signalé pour l’utilisateur de hello. 


![Connexions risquées](./media/active-directory-reporting-security-risky-sign-ins/324.png)


tooinvestigate un événement à risque, sélectionnez-en un dans la liste de hello.  
Cette opération ouvre hello **détails** panneau pour cet événement risque. Sur hello **détails** panneau, vous avez hello option tooeither [fermeture manuelle d’un événement à risque](active-directory-identityprotection.md#closing-risk-events-manually) ou réactiver un événement risque fermé manuellement. 


![Connexions risquées](./media/active-directory-reporting-security-risky-sign-ins/325.png)





## <a name="next-steps"></a>Étapes suivantes

- Pour en savoir plus sur Azure Active Directory Identity Protection, voir [Protection de l’identité Azure Active Directory](active-directory-identityprotection.md).

