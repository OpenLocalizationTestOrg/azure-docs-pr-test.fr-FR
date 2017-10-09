---
title: "aaaSet d’un périphérique Windows 10 avec Azure AD à partir des paramètres | Documents Microsoft"
description: "Explique comment les utilisateurs peuvent participer tooAzure AD via le menu Paramètres de hello."
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: b844e1d9-ad43-4e4a-a398-5c4a43bf2f5c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: d6485228338db571cc01f913c99fbba49e0bb74a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-windows-10-device-with-azure-ad-from-settings"></a>Configuration d’un appareil Windows 10 avec Azure AD à partir des paramètres
Si vous êtes déjà à l’aide de Windows 7 ou Windows 8 et que votre ordinateur ou le périphérique a été mis à niveau tooWindows 10, vous pouvez joindre tooAzure Active Directory (Azure AD) via le menu Paramètres de hello.

## <a name="toojoin-tooazure-ad-from-hello-settings-menu"></a>toojoin tooAzure AD à partir du menu Paramètres de hello
1. À partir de hello **Démarrer** menu, cliquez sur hello **paramètres** icône.
2. Accédez à **Paramètres**, sélectionnez **Système**->**Info produit**->**Rejoindre Azure AD**.
   
   <center>
   ![Rejoindre Azure AD à partir du menu Paramètres de hello](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png)</center>
3. Cliquez sur **continuer** dans la fenêtre de message hello Azure AD Join.
   
   <center>
   ![Fenêtre de message Joindre Azure AD](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png)</center>
4. Indiquez vos informations d’identification de connexion. Cette expérience de connexion inclut toutes les étapes de hello sont l’authentification toocomplete requis. Si vous faites partie d’un locataire fédéré, votre administrateur vous fournira avec l’expérience de fédération hello qui est hébergé par votre organisation.
   <center>
   ![Indiquer les informations d’identification de connexion](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</center>
5. Si votre organisation a configuré l’authentification multifacteur Azure pour joindre tooAzure AD, fournir le second facteur de hello avant de continuer.
6. Cliquez sur **accepter** sur hello **autoriser cette toobe périphérique géré** écran.
7. Vous devez voir le message de type hello « votre appareil est maintenant organisation jointes tooyour dans Azure AD ».

## <a name="additional-information"></a>Informations supplémentaires
* [En savoir plus sur les scénarios d’utilisation pour Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Se connecter tooAzure de périphériques joints au domaine Active Directory pour des expériences Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configuration d’Azure AD Join](active-directory-azureadjoin-setup.md)
* [Authentification des identités sans mot de passe avec Microsoft Passport](active-directory-azureadjoin-passport.md)

