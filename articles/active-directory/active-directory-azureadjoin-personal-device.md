---
title: aaaJoin une organisation de tooyour appareil personnel | Documents Microsoft
description: "Explique comment les utilisateurs peuvent inscrire leur personnel Windows 10 appareils tootheir réseau d’entreprise et fournit les étapes de déploiement pour un scénario BYOD."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 9f3d38f5-1cfd-43d4-97da-4fed1255a1ff
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 979e2461dd9ad0438aa402a0a3223cc84c4c625c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-personal-device-tooyour-organization"></a>Joindre une organisation de tooyour appareil personnel
## <a name="toojoin-a-windows-10-device-tooyour-organization"></a>organisation de tooyour périphérique toojoin Windows 10
1. À partir de hello **Démarrer** menu, sélectionnez **paramètres**.
2. Sélectionnez **Comptes** puis cliquez sur **Votre compte**.
3. Cliquez sur **Ajouter un compte professionnel ou scolaire**puis saisissez votre compte professionnel.
4. Sur hello-page de connexion pour votre organisation, entrez votre nom d’utilisateur et un mot de passe, puis cliquez sur **OK**.
5. Vous devrez ensuite relever un défi Multi-Factor Authentication. (Ce défi est configurable par un administrateur informatique).
6. Azure Active Directory (Azure AD) vérifie si le périphérique de hello requiert inscription de gestion des appareils mobiles.
7. Windows enregistre l’appareil de hello dans l’annuaire de l’organisation hello dans Azure AD et s’inscrit dans la gestion des appareils mobiles, le cas échéant.
8. Si vous êtes un utilisateur géré, Windows effectue le bureau toohello via hello automatique connectez-vous.
9. Si vous êtes un utilisateur fédéré, vous serez prises tooa Windows connectez-vous écran tooenter vos informations d’identification.

## <a name="additional-information"></a>Informations supplémentaires
* [Windows 10 pour les entreprises hello : appareils toouse de méthodes de travail](active-directory-azureadjoin-windows10-devices-overview.md)
* [Extension cloud appareils tooWindows 10 de fonctionnalités via Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)
* [Authentification des identités sans mot de passe avec Microsoft Passport](active-directory-azureadjoin-passport.md)
* [En savoir plus sur les scénarios d’utilisation pour Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Se connecter tooAzure de périphériques joints au domaine Active Directory pour des expériences Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configuration d’Azure AD Join](active-directory-azureadjoin-setup.md)

