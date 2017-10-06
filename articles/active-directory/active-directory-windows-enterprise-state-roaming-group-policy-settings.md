---
title: "les paramètres de stratégie et de la gestion des appareils mobiles aaaGroup | Documents Microsoft"
description: "Fournit des informations sur les paramètres de stratégie de groupe et de gestion des appareils mobiles (MDM) qui doivent être utilisés sur les appareils d’entreprise. Ces stratégies sont appliquées toohello l’ensemble appareil utilisateur."
services: active-directory
keywords: "quels sont les paramètres de stratégie de groupe et de MDM pour Enterprise State Roaming, Enterprise State Roaming, cloud windows"
documentationcenter: 
author: tanning
manager: femila
editor: curtand
ms.assetid: 6471a9b3-8dd4-4237-89d1-bfbeca9f8252
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 762419b47014b1fb4d92ac528785e20078afe689
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="group-policy-and-mdm-settings"></a>Paramètres de stratégie de groupe et de gestion des appareils mobiles
Utilisez ces paramètres de gestion des appareils mobiles et de stratégie de groupe uniquement sur les appareils d’entreprise, car ces stratégies sont appliquées toohello l’ensemble appareil utilisateur. Application d’une synchronisation de paramètres de gestion des appareils mobiles stratégie toodisable un personnel, appartenant à l’utilisateur de périphérique susceptible d’affecter les utilisez hello de ce périphérique. En outre, comptes d’utilisateur de l’appareil de hello seront également affectés par la stratégie de hello.

Les entreprises qui permettre utiliser les toomanage d’itinérance pour les appareils personnels (non managés) hello tooenable portail Azure ou désactiver l’itinérance, plutôt que d’à l’aide de la stratégie de groupe ou MDM.
Hello les tableaux suivants décrire les paramètres de stratégie hello disponibles.

## <a name="mdm-settings"></a>Paramètres de MDM
paramètres de stratégie de gestion des appareils mobiles Hello s’appliquent tooboth Windows 10 et Windows 10 Mobile.  La prise en charge Windows 10 Mobile existe uniquement pour l’itinérance basée sur compte Microsoft via le compte OneDrive de l’utilisateur.  Reportez-vous trop « Appareils et points de terminaison » pour plus d’informations sur les périphériques qui sont pris en charge pour Azure AD basée sur la synchronisation.

| Nom | Description |
| --- | --- |
| Autoriser la connexion de comptes Microsoft |Permet de tooauthenticate les utilisateurs à l’aide d’un compte Microsoft sur l’appareil de hello |
| Autoriser la synchronisation de mes paramètres |Permet de paramètres de Windows tooroam les utilisateurs et les données d’application ; La désactivation de cette stratégie désactivera synchronisation, ainsi que des sauvegardes sur des appareils mobiles |

## <a name="group-policy-settings"></a>Paramètres de stratégie de groupe
paramètres de stratégie de groupe Hello s’appliquent tooWindows 10 appareils qui appartiennent à un domaine Active Directory de tooan jointes. Hello inclut également des paramètres hérités qui apparaîtrait toomanage les paramètres de synchronisation, mais qui ne fonctionnent pas pour l’état itinérant pour Windows 10 entreprise, qui sont signalées par « n’utilisez pas' dans la description de hello.

| Nom | Description |
| --- | --- |
| Comptes : bloquer les comptes Microsoft |Ce paramètre de stratégie empêche les utilisateurs d’ajouter de nouveaux comptes Microsoft sur l’ordinateur |
| Ne pas synchroniser |Empêche les paramètres de Windows tooroam les utilisateurs et les données d’application |
| Ne pas synchroniser les options personnalisées |Désactive la synchronisation de groupe de thèmes hello |
| Ne pas synchroniser les paramètres du navigateur |Désactive la synchronisation de groupe d’Internet Explorer hello |
| Ne pas synchroniser les mots de passe |Désactive la synchronisation du groupe Mots de passe |
| Ne pas synchroniser les autres paramètres Windows |Désactive la synchronisation du groupe Autres paramètres Windows |
| Ne pas synchroniser la personnalisation du Bureau |N’utilisez pas cette fonction ; aucun effet |
| Ne pas synchroniser en cas de connexion limitée |Désactive l’itinérance en cas de connexion limitée, par exemple la 3G mobile |
| Ne pas synchroniser les applications |N’utilisez pas cette fonction ; aucun effet |
| Ne pas synchroniser les paramètres d’application |Désactive l’itinérance des données d’application |
| Ne pas synchroniser les paramètres de démarrage |N’utilisez pas cette fonction ; aucun effet |

## <a name="related-topics"></a>Rubriques connexes
* [Présentation d’Enterprise State Roaming](active-directory-windows-enterprise-state-roaming-overview.md)
* [Activer Enterprise State Roaming dans Azure Active Directory](active-directory-windows-enterprise-state-roaming-enable.md)
* [FAQ sur l’itinérance des paramètres et des données](active-directory-windows-enterprise-state-roaming-faqs.md)
* [Référence des paramètres d’itinérance Windows 10](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
* [Dépannage](active-directory-windows-enterprise-state-roaming-troubleshooting.md)

