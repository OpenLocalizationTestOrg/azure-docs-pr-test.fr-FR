---
title: "aaaUsage scénarios et les considérations relatives au déploiement d’Azure AD Join | Documents Microsoft"
description: "Explique comment les administrateurs peuvent configurer « Azure AD Join » pour leurs utilisateurs finaux (employés, étudiants, autres utilisateurs). Il aborde également les scénarios réels différents hello pour l’utilisation de Azure AD Join."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 81d4461e-21c8-4fdd-9076-0e4991979f62
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 7e57971481aa312ebf8a69999d194f9dcc3d4708
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="usage-scenarios-and-deployment-considerations-for-azure-ad-join"></a>Scénarios d’utilisation et considérations relatives au déploiement pour Azure AD Join
## <a name="usage-scenarios-for-azure-ad-join"></a>Scénarios d’utilisation pour Azure AD Join
### <a name="scenario-1-businesses-largely-in-hello-cloud"></a>Scénario 1 : Les entreprises en grande partie dans le cloud de hello
Azure Active Directory Join (Azure AD Join) peuvent tirer profit vous si vous opérer et gérez les identités de votre entreprise dans le cloud de hello ou déplacez toohello cloud plus rapidement. Vous pouvez utiliser un compte que vous avez créé dans toosign Azure AD dans tooWindows 10. Via [hello tout d’abord exécuter le processus de l’expérience (FRX)](active-directory-azureadjoin-user-frx.md), ou en joignant Azure AD à partir de [menu des paramètres hello](active-directory-azureadjoin-user-upgrade.md), vos utilisateurs peuvent joindre leur tooAzure ordinateurs Active Directory.  Profitez de vos utilisateurs peuvent également l’authentification unique (SSO) accès cloud trop de ressources, tels qu’Office 365, dans un navigateur ou dans les applications Office.

### <a name="scenario-2-educational-institutions"></a>Scénario 2 : établissements d’enseignement
Les établissements d’enseignement ont généralement deux types d’utilisateurs : les enseignants et les étudiants. Enseignants sont considérés comme des membres à long terme de l’organisation de hello. Il est souhaitable de créer des comptes locaux pour eux. Mais les étudiants sont shorter-term membres de l’organisation de hello et leurs comptes peuvent être gérés dans Azure AD. Cela signifie que cloud toohello au lieu d’être stockés en local peut être appliquée à l’échelle du répertoire. Cela signifie également que les étudiants seront en mesure de toosign dans tooWindows avec leurs comptes Azure AD et obtenir des ressources de 365 tooOffice d’accès dans les applications Office.

### <a name="scenario-3-retail-businesses"></a>Scénario 3 : entreprises de vente au détail
Les entreprises de vente au détail font appel à des saisonniers et à des salariés à long terme. En général, vous créez des comptes locaux et utilisez des ordinateurs joints au domaine pour les employés à plein temps. Mais saisonniers sont les membres de l’organisation de hello shorter-term, et il est souhaitable toomanage leurs comptes où les licences utilisateur peuvent être déplacées plus facilement sur. Lorsque vous créez leurs comptes d’utilisateur dans le cloud hello dont les licences d’Office 365, ces utilisateurs bénéficiez des avantages de hello de la connexion tooWindows et les applications Office avec un compte Azure AD, si vous conservez le plus de souplesse avec leurs licences après leur sortie.

### <a name="scenario-4-additional-scenarios"></a>Scénario 4 : autres cas de figure
En même temps que les avantages de hello indiqués précédemment, vous bénéficiez d’avoir à vos utilisateurs de joindre leur tooAzure d’appareils AD en raison d’une jointure simplifiée, la gestion des appareils efficace, l’inscription de gestion automatiques de l’appareil mobile et tooAzure de l’authentification unique Active Directory et les ressources locales.  

## <a name="deployment-considerations-for-azure-ad-join"></a>Considérations relatives au déploiement pour Azure AD Join
### <a name="enable-your-users-toojoin-a-company-owned-device-directly-tooazure-ad"></a>Activer votre toojoin utilisateurs un appareil d’entreprise directement tooAzure AD
Les entreprises peuvent fournir des organisations et comptes cloud uniquement toopartner entreprises. Ces partenaires peuvent ensuite accéder facilement aux applications et aux ressources d’entreprise avec l’authentification unique. Ce scénario est applicable toousers qui accèdent aux ressources principalement dans le cloud de hello, telles que les applications Office 365 ou SaaS qui s’appuient sur Azure AD pour l’authentification.

### <a name="prerequisites"></a>Composants requis
**Au niveau d’entreprise hello (administrateur)**

* Abonnement Azure avec Azure Active Directory  

**Au niveau de l’utilisateur hello**

* Windows 10 (éditions Professionnel et Entreprise)

### <a name="administrator-tasks"></a>Tâches de l’administrateur
* [Configuration de l’inscription des appareils](active-directory-azureadjoin-setup.md)

### <a name="user-tasks"></a>Tâches de l’utilisateur
* [Configuration d’un nouvel appareil Windows 10 avec Azure AD lors de l’installation](active-directory-azureadjoin-user-frx.md)
* [Configurer un appareil Windows 10 avec Azure AD à partir du menu Paramètres de hello](active-directory-azureadjoin-user-upgrade.md)
* [Joindre une organisation de tooyour appareil Windows 10 personnelle](active-directory-azureadjoin-personal-device.md)

## <a name="enable-byod-in-your-organization-for-windows-10"></a>Activation de BYOD (Apportez votre propre appareil) dans votre organisation pour Windows 10
Vous pouvez configurer votre toouse employés et les utilisateurs de leurs ressources et applications d’entreprise Windows appareils BYOD tooaccess personnel. Vos utilisateurs peuvent ajouter leurs comptes (comptes professionnels ou scolaires) tooa personnel Windows appareil tooaccess les ressources Azure AD de manière sécurisée et conforme.

### <a name="prerequisites"></a>Composants requis
**Au niveau d’entreprise hello (administrateur)**

* Abonnement Azure AD

**Au niveau de l’utilisateur hello**

* Windows 10 (éditions Professionnel et Entreprise)

### <a name="administrator-tasks"></a>Tâches de l’administrateur
* [Configuration de l’inscription des appareils](active-directory-azureadjoin-setup.md)

### <a name="user-tasks"></a>Tâches de l’utilisateur
* [Joindre une organisation de tooyour appareil Windows 10 personnelle](active-directory-azureadjoin-personal-device.md)

## <a name="additional-information"></a>Informations supplémentaires
* [Windows 10 pour les entreprises hello : appareils toouse de méthodes de travail](active-directory-azureadjoin-windows10-devices-overview.md)
* [Extension cloud appareils tooWindows 10 de fonctionnalités via Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)
* [Authentification des identités sans mot de passe avec Microsoft Passport](active-directory-azureadjoin-passport.md)
* [En savoir plus sur les scénarios d’utilisation pour Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Se connecter tooAzure de périphériques joints au domaine Active Directory pour des expériences Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configuration d’Azure AD Join](active-directory-azureadjoin-setup.md)

