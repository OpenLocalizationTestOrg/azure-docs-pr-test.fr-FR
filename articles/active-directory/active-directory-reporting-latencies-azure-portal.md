---
title: "latences de création de rapports Active Directory aaaAzure | Documents Microsoft"
description: "En savoir plus sur la quantité de hello de temps que nécessaire pour remonter des rapports tooshow d’événements dans votre portail Azure"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 9b88958d-94a2-4f4b-a18c-616f0617a24e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi;dhanyahk
ms.reviewer: dhanyahk
ms.openlocfilehash: eee959331262ba59b313dd038cb54699dbef48a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-latencies"></a>Latences de création de rapports Azure Active Directory

Avec [reporting](active-directory-preview-explainer.md) Bonjour Azure Active Directory, vous obtenez toutes les informations de hello nécessaires toodetermine faire de votre environnement. Hello durée que nécessaire pour les rapports tooshow données haut Bonjour portail Azure est également appelé latence. 

Cette rubrique répertorie les informations de latence hello pour hello toutes les catégories de rapports Bonjour portail Azure. 


## <a name="activity-reports"></a>Rapports d’activité

Il existe deux zones de rapports d’activité :

- **Activités de connexion** – informations sur l’utilisation de hello des applications gérées et les activités d’authentification des utilisateurs
- **Activités du système** – Informations sur les activités du système liées aux utilisateurs et à la gestion des groupes, à vos applications gérées et aux activités de répertoire

Hello tableau suivant répertorie les informations de latence hello pour les rapports d’activité.

| Rapport | Minimale | Moyenne | Maximale |
| :-- | --- | --- | --- |
| Journaux d’audit             | 30 minutes  | 45 minutes | 1 heure     |
| Connexions               | 15 minutes  | 15 minutes | 2 heures*   |

>[!NOTE]
> Pour certaines données d’activité des connexions provenant d’applications office hérité, il peut prendre des heures de too8 pour hello remonter des rapports tooshow de données. 


## <a name="security-reports"></a>Rapports de sécurité

Il existe deux zones de rapports de sécurité :

- **Connexions risquées** -un risque de connexion est un indicateur pour une tentative de connexion qui ont peut-être été exécutée par une personne qui n’est pas propriétaire de légitime hello d’un compte d’utilisateur. 
- **Utilisateurs avec indicateur de risque** : il s’agit d’un compte d’utilisateur susceptible d’être compromis. 

Hello tableau suivant répertorie les informations de latence hello pour les rapports de sécurité.

| Rapport | Minimale | Moyenne | Maximale |
| :-- | --- | --- | --- |
| Les utilisateurs à risque          | 5 minutes   | 15 minutes  | 2 heures  |
| Connexions risquées         | 5 minutes   | 15 minutes  | 2 heures  |

## <a name="risk-events"></a>Événements à risque

Azure Active Directory utilise des algorithmes et des paramètres heuristiques actions suspectes toodetect qui sont des comptes d’utilisateur associés tooyour d’apprentissage adaptatif. Chaque action suspecte détectée est stockée dans un enregistrement appelé événement à risque.

Hello tableau suivant répertorie les informations de latence hello pour les événements à risque.

| Rapport | Minimale | Moyenne | Maximale |
| :-- | --- | --- | --- |
| Connexions depuis des adresses IP anonymes |5 minutes |15 minutes |2 heures |
| Connexions depuis des emplacements non connus |5 minutes |15 minutes |2 heures |
| Utilisateurs avec des informations d’identification volées |2 heures |4 heures |8 heures |
| Voyage Impossible tooatypical emplacements |5 minutes |1 heure |8 heures  |
| Connexions depuis des appareils infectés |2 heures |4 heures |8 heures  |
| Connexions depuis des adresses IP avec des activités suspectes |2 heures |4 heures |8 heures  |



## <a name="next-steps"></a>Étapes suivantes

Si vous souhaitez tooknow plus d’informations sur les rapports d’activité hello Bonjour portail Azure, consultez :

- [Rapports d’activité de connexion dans le portail d’Azure Active Directory hello](active-directory-reporting-activity-sign-ins.md)
- [Rapports d’activité dans le portail d’Azure Active Directory hello d’audit](active-directory-reporting-activity-audit-logs.md)

Si vous souhaitez tooknow plus d’informations sur les rapports de sécurité hello Bonjour portail Azure, consultez :

- [Utilisateurs sur les rapports de sécurité risque dans le portail d’Azure Active Directory hello](active-directory-reporting-security-user-at-risk.md)
- [Rapport des connexions présentant un risque dans le portail d’Azure Active Directory hello](active-directory-reporting-security-risky-sign-ins.md)

Si vous souhaitez tooknow plus d’informations sur les événements à risque, consultez [événements à risque Azure Active Directory](active-directory-reporting-risk-events.md).
