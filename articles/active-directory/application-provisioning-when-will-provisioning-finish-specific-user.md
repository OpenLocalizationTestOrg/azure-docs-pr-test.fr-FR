---
title: "aaaFind quand un utilisateur spécifique sont en mesure de tooaccess une application | Documents Microsoft"
description: "Comment toofind out quand un utilisateur d’essentiel être en mesure de tooaccess une application que vous avez configuré pour l’approvisionnement des utilisateurs auprès d’Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: bb9520499dcc8bbbe6fae05c5238c8852815ea0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-when-a-specific-user-will-be-able-tooaccess-an-application"></a>Savoir quand un utilisateur spécifique sera en mesure de tooaccess une application
Lorsque vous utilisez l’approvisionnement automatique des utilisateurs avec une application, Azure AD approvisionne et met à jour automatiquement les comptes d’utilisateur dans une application selon différents éléments comme [l’affectation d’utilisateurs et de groupes](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) et selon un intervalle régulier planifié (généralement toutes les 10 minutes).

## <a name="how-long-does-it-take"></a>Combien de temps cela prend-il ?

Hello temps d’un toobe utilisateur donné configuré dépend principalement ou non une synchronisation initiale « complète » a déjà eu lieu.

Hello première synchronisation entre Azure AD et une application peut prendre entre 20 minutes tooseveral heures, en fonction de la taille de hello du répertoire de hello Azure AD et hello des utilisateurs dans la portée pour la configuration. 

Les synchronisations suivantes après la synchronisation initiale hello être plus rapides (par exemple, dans les 10 minutes), comme hello configuration service stocke les filigranes qui représentent l’état hello des deux systèmes après la synchronisation initiale hello, améliorer les performances des synchronisations suivantes.

## <a name="how-toocheck-hello-status-of-a-user"></a>Comment toocheck hello état d’un utilisateur

état de configuration hello toosee pour un utilisateur sélectionné, consultez hello les journaux d’Audit dans Azure AD.

Hello, journaux d’audit de configuration sont accessibles dans hello portail Azure, Bonjour **Azure Active Directory &gt; applications d’entreprise &gt; \[nom de l’Application\] &gt; lesjournauxd’Audit**onglet. Hello du filtre de session hello **l’approvisionnement de comptes** catégorie tooonly voir hello événements pour cette application de configuration. Vous pouvez rechercher des utilisateurs en fonction de hello « correspondance ID » qui a été configuré pour eux dans les mappages d’attributs hello. 

Par exemple, si vous avez configuré hello « nom d’utilisateur principal » ou « adresse de messagerie » comme hello attribut côté hello Azure AD correspondant, et ne pas en cours de configuration de l’utilisateur hello a la valeur «audrey@contoso.com«, puis les journaux audit hello de recherche pour »audrey@contoso.com» et passez en revue puis entrées retournées.

Hello d’audit de configuration journaux enregistrent toutes hello opérations effectuées par hello mise en service du service, y compris :

* Interrogation d’Azure AD concernant les utilisateurs assignés qui se trouvent dans l’étendue de l’approvisionnement
* Interrogation d’application cible de hello existence hello de ces utilisateurs
* Comparaison d’objets utilisateur hello entre le système de hello
* Ajout, mise à jour ou la désactivation du compte d’utilisateur hello dans le système cible de hello en fonction de comparaison de hello

## <a name="next-steps"></a>Étapes suivantes
[Automatiser la configuration de l’utilisateur et Deprovisioning tooSaaS Applications avec Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)».
