---
title: "vue d’ensemble de l’itinérance aaaEnterprise état | Documents Microsoft"
description: "Fournit des informations sur les paramètres Enterprise State Roaming dans les périphériques Windows. Enterprise State Roaming fournit aux utilisateurs une expérience unifiée sur leurs appareils Windows et réduit le temps de hello nécessaire pour la configuration d’un nouveau périphérique."
services: active-directory
keywords: "Qu’est-ce que Enterprise State Roaming, la synchronisation d’entreprise et Windows cloud"
documentationcenter: 
author: tanning
manager: femila
editor: curtand
ms.assetid: 83b3b58f-94c1-4ab0-be05-20e01f5ae3f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 436076383b70b7cd65a612e3928f62f26ac5fa84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-state-roaming-overview"></a>Présentation d’Enterprise State Roaming
Avec Windows 10, [Azure Active Directory (Azure AD)](active-directory-whatis.md) utilisateurs gain hello capacité toosecurely synchroniser leurs paramètres de l’utilisateur et l’application Paramètres données toohello dans le cloud. Enterprise State Roaming fournit aux utilisateurs une expérience unifiée sur leurs appareils Windows et réduit le temps de hello nécessaire pour la configuration d’un nouveau périphérique. Enterprise State Roaming fonctionne similaire toohello standard [synchronisation des paramètres de consommateur](http://windows.microsoft.com/en-US/windows-8/sync-settings-pcs) qui a été introduite dans Windows 8. En outre, Enterprise State Roaming offre :

* **Séparation des données d’entreprise des données client** : les organisations maîtrisent leurs données, et les données d’entreprise ne sont pas mélangées dans le compte cloud client ou aucune donnée client ne figure dans le compte cloud d’entreprise.
* **Amélioration de la sécurité** : les données sont automatiquement chiffrées avant de quitter un appareil Windows 10 de l’utilisateur hello à l’aide d’Azure Rights Management (Azure RMS) et données restent chiffrées au repos dans le cloud de hello. Tout le contenu reste chiffré au repos dans le cloud hello, à l’exception des espaces de noms hello, telles que les noms de paramètres et les noms d’application Windows.  
* **Une meilleure gestion et surveillance** – fournit le contrôle et la visibilité sur qui synchronise les paramètres de votre organisation et sur quels appareils grâce à l’intégration de portail hello Azure AD. 

Enterprise State Roaming est disponible dans plusieurs régions Azure. Vous trouverez la liste hello mis à jour des régions disponibles sur hello [Services Azure par régions](https://azure.microsoft.com/regions/#services) page sous Azure Active Directory.

| Article | Description |
| --- | --- |
| [Activer Enterprise State Roaming dans Azure Active Directory](active-directory-windows-enterprise-state-roaming-enable.md) |Enterprise State Roaming est organisation tooany disponibles avec un abonnement Premium Azure Active Directory (Azure AD). Pour plus d’informations sur la façon de tooget un abonnement Azure AD, consultez hello [produit d’Azure AD](https://azure.microsoft.com/services/active-directory) page. |
| [FAQ sur l’itinérance des paramètres et des données](active-directory-windows-enterprise-state-roaming-faqs.md) |Cette rubrique répond à certaines questions que les administrateurs informatiques peuvent se poser sur les paramètres et la synchronisation des données d’application. |
| [Paramètres de stratégie de groupe et de MDM pour la synchronisation des paramètres](active-directory-windows-enterprise-state-roaming-group-policy-settings.md) |Windows 10 fournit la stratégie de groupe et de la synchronisation de périphérique mobile de gestion des stratégie paramètres toolimit paramètres. |
| [Référence des paramètres d’itinérance Windows 10](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md) |Hello Voici une liste complète de tous les paramètres hello seront déplacés et/ou sauvegardé dans Windows 10. |
| [Dépannage](active-directory-windows-enterprise-state-roaming-troubleshooting.md) |Cette rubrique présente certaines étapes de base pour la résolution des problèmes et contient une liste de problèmes connus. |

