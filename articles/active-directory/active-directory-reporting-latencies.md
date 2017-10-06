---
title: aaaAzure les latences Reporting Active Directory | Documents Microsoft
description: "Quantité de temps que nécessaire pour remonter des rapports tooshow d’événements dans votre répertoire Azure Active Directory."
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 346b14f8-d16d-4b07-8211-e6c5eec07062
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 14367d21dfb28359f991037cc924d416420be456
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-report-latencies"></a>Latences de rapport Azure Active Directory
*Cette documentation fait partie de hello [Guide Azure Active Directory Reporting](active-directory-reporting-guide.md).*

| Rapport | Minimale | Moyenne | Maximale |
| --- | --- | --- | --- |
| **Rapports de sécurité** | | | |
| Activité de connexion anormale |2 heures |4 heures |8 heures |
| Connexions à partir de sources inconnues |2 heures |4 heures |8 heures |
| Connexions après plusieurs échecs |2 heures |4 heures |8 heures |
| Connexions depuis plusieurs zones géographiques |2 heures |4 heures |8 heures |
| Connexions depuis des adresses IP avec des activités suspectes |2 heures |4 heures |8 heures |
| Connexions à partir d’appareils potentiellement infectés |2 heures |4 heures |8 heures |
| Utilisateurs ayant une activité de connexion anormale |2 heures |4 heures |8 heures |
| Utilisateurs avec des informations d’identification volées |2 heures |4 heures |8 heures |
| Toute l’activité de connexion des utilisateurs |2 heures |4 heures |8 heures |
| **Rapports d’application** | | | |
| Activité d’approvisionnement de compte |2 heures |4 heures |8 heures |
| Erreurs de configuration de compte |2 heures |4 heures |8 heures |
| Utilisation des applications |2 heures |4 heures |8 heures |
| État de substitution de mot de passe |2 heures |4 heures |8 heures |
| **Rapports d’audit et d’activité** | | | |
| Rapport d'audit |1 minute |15 minutes |30 minutes |
| Activité de réinitialisation de mot de passe (Azure AD) |2 heures |4 heures |8 heures |
| Activité de réinitialisation de mot de passe (Identity Manager) |2 heures |4 heures |8 heures |
| Activité d’enregistrement de réinitialisation de mot de passe (Azure AD) |2 heures |4 heures |8 heures |
| Activité d’enregistrement de réinitialisation de mot de passe (Identity Manager) |2 heures |4 heures |8 heures |
| Activité de groupes en libre-service (Azure AD) |2 heures |4 heures |8 heures |
| Activité de groupes en libre-service (Identity Manager) |2 heures |4 heures |8 heures |
| **Rapports RMS** | | | |
| Utilisateurs RMS les plus actifs |2 heures |4 heures |8 heures |
| Utilisation de RMS |2 heures |4 heures |8 heures |
| Utilisation d’un appareil RMS |2 heures |4 heures |8 heures |
| Utilisation d’applications fonctionnant avec RMS |2 heures |4 heures |8 heures |

