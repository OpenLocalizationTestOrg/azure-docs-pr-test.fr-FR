---
title: "Liences : réinitialisation de mot de passe en libre-service Azure AD | Microsoft Docs"
description: "Conditions de licence pour la réinitialisation du mot de passe en libre-service dans Azure AD"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 9cecaaac429165346f7082f1965dc8a21063fe7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="licensing-requirements-for-azure-ad-self-service-password-reset"></a>Conditions de licence pour la réinitialisation du mot de passe en libre-service Azure AD

Dans l’ordre pour toofunction de réinitialisation de mot de passe Azure AD, vous **doit disposer d’au moins une licence de votre organisation**. Nous n’imposent pas de gestionnaire de licences sur l’expérience de réinitialisation de mot de passe hello par l’utilisateur. conformité toomaintain avec votre contrat de licence de Microsoft, vous devez tooassign licences tooany utilisateurs qui utilisent les fonctionnalités premium.

* **Utilisateurs du cloud uniquement** : n’importe quelle référence Office 365 (O365) payante ou Azure AD Basic
* Utilisateurs **cloud** et/ou **locaux** : Azure AD Premium P1 ou P2, Enterprise Mobility + Security (EMS) ou Secure Productive Enterprise (SPE)

## <a name="licenses-required-for-password-writeback"></a>Licences requises pour la réécriture du mot de passe

l’écriture différée de mot de passe toouse, vous devez avoir un de hello suivant licences attribuées dans votre client.

* Azure AD Premium P1
* Azure AD Premium P2
* Enterprise Mobility + Security E3
* Enterprise Mobility + Security E5
* Secure Productive Enterprise E3
* Secure Productive Enterprise E5

> [!NOTE]
> Autonome Office 365 régimes de licences **ne prennent pas en charge l’écriture différée de mot de passe** et exiger de hello précédant les plans pour toowork de cette fonctionnalité.

Les informations de licence supplémentaires, y compris les coûts se trouvent sur hello suivant des pages

* [Site de tarification d’Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/)
* [Enterprise Mobility + Security](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
* [Secure Productive Enterprise](https://www.microsoft.com/secure-productive-enterprise/default.aspx)

## <a name="enable-group-or-user-based-licensing"></a>Activer les licences utilisateur ou groupe

Azure AD prend en charge basée sur le groupe de licences des licences de tooassign permettant aux administrateurs dans tooa groupe d’utilisateurs, plutôt que leur attribuer une à la fois. [Affecter, vérifier et résoudre les problèmes de licences](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses)

Certains services Microsoft ne sont pas disponibles dans tous les emplacements. Avant tooa utilisateur peut être affectée à une licence, administrateur de hello doit spécifier des propriétés de « Emplacement d’utilisation » hello sur utilisateur de hello. Attribution de licences peut être effectuée sous utilisateur > profil > section des paramètres de hello portail Azure. **Lorsque vous utilisez l’attribution de licence de groupe, tous les utilisateurs sans un emplacement d’utilisation spécifié héritent emplacement hello du répertoire de hello.**

## <a name="next-steps"></a>Étapes suivantes

Hello suivant liens fournit des informations supplémentaires concernant le mot de passe réinitialisé à l’aide d’Azure AD

* [**Démarrage rapide**](active-directory-passwords-getting-started.md) : soyez rapidement opérationnel avec la gestion des mots de passe en libre-service d’Azure AD. 
* [**Données** ](active-directory-passwords-data.md) : comprendre les données de hello est nécessaire et comment il est utilisé pour la gestion de mot de passe
* [**Déploiement** ](active-directory-passwords-best-practices.md) -planifier et déployer des utilisateurs de tooyour SSPR hello d’aide est disponible ici
* [**Personnaliser** ](active-directory-passwords-customize.md) -personnaliser hello apparence Hello SSPR expérience pour votre entreprise.
* [**Rapports**](active-directory-passwords-reporting.md) : découvrez si, quand et où vos utilisateurs accèdent aux fonctionnalités de réinitialisation de mot de passe en libre-service
* [**Présentation approfondie technique** ](active-directory-passwords-how-it-works.md) -accédez derrière hello RIDEAU toounderstand son fonctionnement
* [**Forum Aux Questions (FAQ)**](active-directory-passwords-faq.md) : Comment ? Pourquoi ? Quoi ? Où ? Qui ? Quand ? -Réponses tooquestions vous souhaitiez toujours tooask
* [**Résoudre les problèmes** ](active-directory-passwords-troubleshoot.md) -en savoir comment tooresolve commun problèmes que nous pouvons voir avec SSPR

