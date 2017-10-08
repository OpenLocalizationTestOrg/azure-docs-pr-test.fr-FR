---
title: "aaaSet un nouveau périphérique auprès d’Azure AD lors de l’installation | Documents Microsoft"
description: "Rubrique qui explique comment les utilisateurs peuvent configurer Azure AD Join lors de la première utilisation."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 06a149f7-4aa1-4fb9-a8ec-ac2633b031fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 6afce4be7f084f1956a6f9dbddaa8def0605956d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-new-device-with-azure-ad-during-setup"></a>Configuration d’un nouvel appareil avec Azure AD lors de l’installation
Dans Windows 10, les utilisateurs peuvent joindre leur tooAzure périphériques Active Directory (Azure AD) dans hello première mise en route (FRX). Cela permet aux organisations toodistribute périphériques emballée tootheir employés ou des étudiants, ou choisir leurs propres appareils (CYOD).
Si les éditions de Windows 10 Professionnel ou Windows 10 entreprise est installé sur un appareil, hello rencontrer des processus d’installation par défaut toohello appareils d’entreprise.

## <a name="toojoin-a-device-tooazure-ad"></a>toojoin un tooAzure appareil AD
1. Lorsque vous activez votre nouveau périphérique et démarrez le processus d’installation de hello, vous devez voir hello **se préparer** message. Suivez tooset des invites hello de votre appareil.
2. Commencez par personnaliser votre région et votre langue. Puis acceptez le contrat de licence logiciel Microsoft hello.
   ![Personnalisation pour votre région](./media/active-directory-azureadjoin/active-directory-azureadjoin-customize-region.png)
3. Sélectionnez hello réseau toouse pour la connexion toohello Internet.
4. Sélectionnez si vous utilisez un périphérique personnel ou un périphérique appartenant à l'entreprise. S’il s’agit d’entreprise, cliquez sur **ce périphérique appartient toomy organisation**. Expérience d’Azure AD Join hello démarre. Voici un des écrans que vous voyez si vous utilisez Windows 10 Professionnel.
   <center>
   ![Qui possède cet écran d’ordinateur](./media/active-directory-azureadjoin/active-directory-azureadjoin-who-owns-pc.png)
5. Entrez les informations d’identification de hello tooyou fournis par votre organisation.
   <center>
   ![Écran de connexion](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)
6. Une fois que vous avez entré votre nom d'utilisateur, un client correspondant se trouve dans Azure AD. Si vous êtes dans un domaine fédéré, vous serez redirigé tooyour locale sécuriser Service d’émission de jeton server--par exemple, Active Directory Federation Services (ADFS).
7. Si vous êtes un utilisateur dans un domaine non fédéré, entrez vos informations d’identification directement sur hello Azure page AD-hébergé. Si la marque de votre société a été ajoutée, vous allez également voir le logo de votre organisation et le texte d’accompagnement.
8. Vous devrez ensuite relever un défi Multi-Factor Authentication. Ce défi est configurable par un administrateur informatique.
9. Azure AD vérifie si cet utilisateur/appareil exige une inscription à la gestion des appareils mobiles.
10. Windows enregistre l’appareil de hello dans l’annuaire de l’organisation hello dans Azure AD et s’inscrit dans la gestion des appareils mobiles, le cas échéant.
11. Si vous êtes un utilisateur géré, Windows effectue le bureau toohello via le processus de connexion automatique hello.
12. Si vous êtes un utilisateur fédéré, vous êtes dirigé toohello l’authentification Windows dans l’écran tooenter vos informations d’identification.

> [!NOTE]
> Joindre un domaine de Windows Server Active Directory local dans les Windows hello out-of-box expérience n’est pas pris en charge. Par conséquent, si vous envisagez de toojoin un domaine tooa de l’ordinateur, vous devez sélectionner le lien de hello **configurer Windows avec un compte local** à la place. Vous pouvez ensuite joindre le domaine hello à partir des paramètres de hello sur votre ordinateur comme vous l’avez fait avant.
> 
> 

## <a name="additional-information"></a>Informations supplémentaires
* [Windows 10 pour les entreprises hello : appareils toouse de méthodes de travail](active-directory-azureadjoin-windows10-devices-overview.md)
* [Extension cloud appareils tooWindows 10 de fonctionnalités via Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)
* [Authentification des identités sans mot de passe avec Microsoft Passport](active-directory-azureadjoin-passport.md)
* [En savoir plus sur les scénarios d’utilisation pour Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Se connecter tooAzure de périphériques joints au domaine Active Directory pour des expériences Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configuration d’Azure AD Join](active-directory-azureadjoin-setup.md)

