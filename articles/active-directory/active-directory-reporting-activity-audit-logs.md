---
title: "rapports d’activité d’aaaAudit dans le portail d’Azure Active Directory hello | Documents Microsoft"
description: "Introduction toohello auditer les rapports d’activité dans le portail d’Azure Active Directory hello"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: a1f93126-77d1-4345-ab7d-561066041161
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 1567673f5030fc707b017c069f2ba7587962e5cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="audit-activity-reports-in-hello-azure-active-directory-portal"></a>Rapports d’activité dans le portail d’Azure Active Directory hello d’audit 

Les rapports dans Azure Active Directory (Azure AD), vous pouvez obtenir des informations de hello vous devez toodetermine faire de votre environnement.

Hello architecture reporting dans Azure AD se compose de hello suivant des composants :

- **Activité** 
    - **Activités de connexion** – informations sur l’utilisation de hello des applications gérées et les activités d’authentification des utilisateurs
    - **Activités du système** – Informations sur les activités du système liées aux utilisateurs et à la gestion des groupes, à vos applications gérées et aux activités de répertoire.
- **Sécurité** 
    - **Connexions risquées** -un risque de connexion est un indicateur pour une tentative de connexion qui ont peut-être été exécutée par une personne qui n’est pas propriétaire de légitime hello d’un compte d’utilisateur. Pour en savoir plus, consultez Connexions risquées.
    - **Utilisateurs avec indicateur de risque** : il s’agit d’un compte d’utilisateur susceptible d’être compromis. Pour en savoir plus, consultez Utilisateurs avec indicateur de risque.

Cette rubrique donne une vue d’ensemble des activités d’audit hello.
 
## <a name="who-can-access-hello-data"></a>Qui peut accéder à des données de salutation ?
* Utilisateurs dans le rôle d’administrateur de la sécurité ou de sécurité Reader hello
* Administrateurs généraux
* Les utilisateurs individuels (non administrateurs) peuvent voir leurs propres activités


## <a name="audit-logs"></a>Journaux d’audit

journaux d’audit de Hello dans Azure Active Directory fournissent des enregistrements d’activités du système pour la conformité.  
Votre première tooall de point d’entrée l’audit des données est **journaux d’Audit** Bonjour **activité** section de **Azure Active Directory**.

![Journaux d’audit](./media/active-directory-reporting-activity-audit-logs/61.png "Journaux d’Audit")

Un journal d’audit inclut un mode Liste par défaut, qui indique :

- date de Hello et l’heure de l’occurrence de hello
- Hello initiateur / acteur (*qui*) d’une activité 
- Hello d’activité (*que*) 
- cible de Hello

![Journaux d’audit](./media/active-directory-reporting-activity-audit-logs/18.png "Journaux d’Audit")

Vous pouvez personnaliser l’affichage de liste hello en cliquant sur **colonnes** dans la barre d’outils hello.

![Journaux d’audit](./media/active-directory-reporting-activity-audit-logs/19.png "Journaux d’Audit")

Cela vous permet de toodisplay des champs supplémentaires ou supprimer des champs qui sont déjà affichés.

![Journaux d’audit](./media/active-directory-reporting-activity-audit-logs/21.png "Journaux d’Audit")


En cliquant sur un élément dans la vue de liste hello, vous obtenez toutes les informations disponibles à ce sujet.

![Journaux d’audit](./media/active-directory-reporting-activity-audit-logs/22.png "Journaux d’Audit")


## <a name="filtering-audit-logs"></a>Filtrage des journaux d’audit

toonarrow bas hello signalés au niveau de tooa de données que fonctionne pour vous, vous pouvez filtrer les données d’audit hello hello suivant des champs à l’aide de :

- Plage de dates
- Initié par (intervenant)
- Catégorie
- Type de ressource d’activité
- Activité

![Journaux d’audit](./media/active-directory-reporting-activity-audit-logs/23.png "Journaux d’Audit")


Hello **plage de dates** filtre active tooyou toodefine un laps de temps pour hello a retourné des données.  
Les valeurs possibles sont les suivantes :

- 1 mois
- 7 jours
- 24 heures
- Personnalisée

Lorsque vous sélectionnez une plage personnalisée, vous pouvez configurer une heure de début et une heure de fin.

Hello **initié par** filtre permet de vous toodefine les nom d’un acteur ou son nom principal universel (UPN).

Hello **catégorie** filtre vous permet de tooselect un Hello suivant filtre :

- Tout
- Catégorie principale
- Répertoire principal
- Gestion des mots de passe en libre-service
- Gestion des groupes en libre service
- Approvisionnement de comptes - Substitution de mot de passe automatique
- Utilisateurs invités
- Service MIM
- Identity Protection
- B2C

Hello **type de ressource d’activité** filtre vous permet de tooselect filtre les valeurs hello suivantes :

- Tout 
- Groupe
- Répertoire
- Utilisateur
- Application
- Stratégie
- Appareil
- Autres

Lorsque vous sélectionnez **groupe** en tant que **type de ressource d’activité**, vous obtenez des tooalso une catégorie de filtre supplémentaires qui vous permet de fournir un **Source**:

- Azure AD
- O365


Hello **activité** filtre est basé sur la catégorie de hello et sélection du type de ressource activité vous apporter. Vous pouvez sélectionner une activité spécifique toosee ou tous. 

Vous pouvez obtenir liste hello de toutes les activités d’Audit à l’aide de hello API Graph https://graph.windows.net/$ tenantdomain/activités/auditActivityTypes ? api-version = beta, où $tenantdomain = votre nom de domaine ou consultez l’article de toohello [rapport d’audit événements](active-directory-reporting-audit-events.md).


## <a name="audit-logs-shortcuts"></a>Raccourcis de journaux d’audit

En outre trop**Azure Active Directory**, hello portail Azure vous offre deux points d’entrée supplémentaires tooaudit données :

- Utilisateurs et groupes
- Applications d’entreprise

### <a name="users-and-groups-audit-logs"></a>Journaux d’audit des utilisateurs et des groupes

Avec l’utilisateur et d’audit basées sur le groupe de rapports, vous pouvez obtenir tooquestions réponses telles que :

- Quels types de mises à jour ont été les utilisateurs hello appliqués ?

- Combien d’utilisateurs ont été modifiés ?

- Combien de mots de passe ont été modifiés ?

- Qu’a fait un administrateur dans un répertoire ?

- Quelles sont les groupes hello qui ont été ajoutés ?

- Existe-t-il des groupes comportant des modifications d’adhésion ?

- Les propriétaires de hello du groupe ont été modifiés ?

- Les licences ont été attribuées à un utilisateur ou groupe de tooa ?

Si vous souhaitez simplement tooreview données toousers connexes et les groupes d’audit, vous trouverez une vue filtrée sous **journaux d’Audit** Bonjour **activité** section Hello **utilisateurs et groupes**. Dans ce point d’entrée, **Utilisateurs et groupes** est présélectionné comme **Type de ressource d’activité**.

![Journaux d’audit](./media/active-directory-reporting-activity-audit-logs/93.png "Journaux d’Audit")

### <a name="enterprise-applications-audit-logs"></a>Journaux d’audit d’applications d’entreprise

Rapports d’audit avec basée sur l’application, vous pouvez obtenir des tooquestions réponses telles que :

* Quelles sont les applications hello qui ont été ajoutées ou mis à jour ?
* Quelles sont les applications hello qui ont été supprimées ?
* Le principal du service d’une application a-t-il été modifié ?
* Les noms de hello des applications ont été modifiés ?
* Qui a donné son consentement tooan application ?

Si vous souhaitez simplement tooreview l’audit des données connexes tooyour applications, vous trouverez une vue filtrée sous **journaux d’Audit** Bonjour **activité** section Hello **des applications d’entreprise**  panneau. Dans ce point d’entrée, **Applications d’entreprise** est présélectionné comme **Type de ressource d’activité**.

![Journaux d’audit](./media/active-directory-reporting-activity-audit-logs/134.png "Journaux d’Audit")

Vous pouvez filtrer cet affichage le plus bas toojust **groupes** ou simplement **utilisateurs**.

![Journaux d’audit](./media/active-directory-reporting-activity-audit-logs/25.png "Journaux d’Audit")


## <a name="next-steps"></a>Étapes suivantes

Pour une vue d’ensemble de la création de rapports, consultez hello [reporting d’Azure Active Directory](active-directory-reporting-azure-portal.md).

