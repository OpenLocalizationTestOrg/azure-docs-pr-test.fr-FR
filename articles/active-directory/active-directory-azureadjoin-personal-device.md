---
title: "Association d’un appareil personnel à votre organisation | Microsoft Docs"
description: "Explique la manière dont les utilisateurs peuvent inscrire leurs appareils Windows 10 personnels sur le réseau de leur entreprise, avec des étapes de déploiement pour un scénario de BYOD."
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
ms.openlocfilehash: 9418365ea18b065551448742b21c8b17a1749fc8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="join-a-personal-device-to-your-organization"></a>Association d’un appareil personnel à votre organisation
## <a name="to-join-a-windows-10-device-to-your-organization"></a>Association d’un appareil Windows 10 à votre organisation
1. Dans le menu **Démarrer**, sélectionnez **Paramètres**.
2. Sélectionnez **Comptes** puis cliquez sur **Votre compte**.
3. Cliquez sur **Ajouter un compte professionnel ou scolaire**puis saisissez votre compte professionnel.
4. Sur la page de connexion pour votre organisation, entrez votre nom d’utilisateur et votre mot de passe, puis cliquez sur **OK**.
5. Vous devrez ensuite relever un défi Multi-Factor Authentication. (Ce défi est configurable par un administrateur informatique).
6. Azure Active Directory (Azure AD) vérifie si l’appareil requiert l’inscription à la gestion des appareils mobiles.
7. Windows enregistre l’appareil dans le répertoire de l’organisation dans Azure AD et l’inscrit dans la gestion des appareils mobiles, le cas échéant.
8. Si vous êtes un utilisateur géré, Windows vous dirige vers le bureau par le biais de la connexion automatique.
9. Si vous êtes un utilisateur fédéré, vous accédez à l’écran d’ouverture de session Windows pour entrer vos informations d’identification.

## <a name="additional-information"></a>Informations supplémentaires
* [Windows 10 pour l’entreprise : plusieurs manières d’utiliser des appareils professionnels](active-directory-azureadjoin-windows10-devices-overview.md)
* [Extension des fonctionnalités du cloud aux appareils Windows 10 via Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)
* [Authentification des identités sans mot de passe avec Microsoft Passport](active-directory-azureadjoin-passport.md)
* [En savoir plus sur les scénarios d’utilisation pour Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Connecter des appareils joints au domaine à Azure AD pour des expériences Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configuration d’Azure AD Join](active-directory-azureadjoin-setup.md)

