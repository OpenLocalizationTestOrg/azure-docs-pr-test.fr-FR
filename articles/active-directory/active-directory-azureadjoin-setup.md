---
title: "aaaSetting d’Azure AD Join pour vos utilisateurs | Documents Microsoft"
description: "Explique comment les administrateurs peuvent configurer Azure AD Join pour l’inscription locale d’appareils et d’annuaires."
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: bfc5d415-c918-4d8b-afee-b3f41cc28469
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 60a5aeb11292cb6057ab1065c3ab77e5981d0cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-azure-ad-join-in-your-organization"></a>Configuration d’Azure AD Join dans votre organisation
Avant de configurer Azure Active Directory Join (Azure AD Join), vous devez tooeither synchronisation vers le haut de votre annuaire local du cloud de toohello les utilisateurs ou créer manuellement des comptes gérés dans Azure AD.

Obtenir des instructions détaillées pour la synchronisation de votre tooAzure d’utilisateurs local AD est couvert dans [intégrer vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).

toomanually créer et gérer des utilisateurs dans Azure AD, consultez trop[gestion des utilisateurs dans Azure AD](https://msdn.microsoft.com/library/azure/hh967609.aspx).

## <a name="set-up-device-registration"></a>Configuration de l’inscription des appareils
1. Ouvrez une session toohello portail Azure en tant qu’administrateur.
2. Dans le volet gauche de hello, sélectionnez **Active Directory**.
3. Sur hello **répertoire** , sélectionnez votre annuaire.
4. Sélectionnez hello **configurer** onglet.
5. Accédez toohello **périphériques** section.
6. Sur hello **périphériques** définir hello, onglet :  
   * **NOMBRE de périphériques par utilisateur maximale**: sélectionnez hello le nombre maximal d’appareils qu’un utilisateur dans Azure AD.  Si un utilisateur atteint ce quota, elles seront pas en mesure de tooadd des périphériques supplémentaires jusqu'à ce qu’un ou plusieurs des appareils existants sont supprimés.
   * **EXIGER l’authentification MULTIFACTEUR tooJOIN périphériques**: définir si les utilisateurs sont requis tooprovide une authentification de second facteur toojoin leur tooAzure appareil AD. Pour plus d’informations sur l’authentification multifacteur Azure, consultez [prise en main d’Azure multi-Factor Authentication dans le cloud de hello](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).
   * **Les utilisateurs peuvent les appareils AZURE AD JOIN**: sélectionnez hello utilisateurs et groupes sont autorisés à toojoin périphériques tooAzure AD.
   * **AZURE de ON administrateurs supplémentaires à des appareils joints AD**: avec Azure AD Premium ou hello Enterprise Mobility Suite (EMS), vous pouvez choisir quels utilisateurs sont accordés des droits d’administrateur local toohello appareil. Les administrateurs globaux et les propriétaires des appareils bénéficient de droits d’administrateur local par défaut.

<center>![Configuration de l’inscription des appareils](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png)</center>

Une fois que vous configurez Azure AD Join pour vos utilisateurs, ils peuvent se connecter tooAzure AD via leurs d’entreprise ou appareils personnels.

Voici hello trois scénarios vous pouvez utiliser tooenable tooset de vos utilisateurs d’Azure AD Join :

* Les utilisateurs joindre un appareil d’entreprise directement tooAzure AD.
* Toohello de périphérique aux utilisateurs appartenant à une société de jonction de domaine Active Directory local et puis étend hello appareil tooAzure AD.
* Ajoutez les utilisateurs du travail ou scolaire comptes tooWindows sur un appareil personnel

## <a name="additional-information"></a>Informations supplémentaires
* [Windows 10 pour les entreprises hello : appareils toouse de méthodes de travail](active-directory-azureadjoin-windows10-devices-overview.md)
* [Extension cloud appareils tooWindows 10 de fonctionnalités via Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)
* [En savoir plus sur les scénarios d’utilisation pour Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Se connecter tooAzure de périphériques joints au domaine Active Directory pour des expériences Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configuration d’Azure AD Join](active-directory-azureadjoin-setup.md)

