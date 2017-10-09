---
title: "mot de passe libre-service aaaAzure AD réinitialiser la vue d’ensemble | Documents Microsoft"
description: "En quoi la réinitialisation de mot de passe en libre-service d’Azure AD peut-elle être utile à votre organisation ?"
services: active-directory
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
ms.openlocfilehash: 0efc291b1eeec0b7ae33ff5a7d9ed38e70c8be6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-self-service-password-reset-for-hello-it-professional"></a>Azure AD mot de passe libre-service réinitialiser hello pour les professionnels de l’informatique

« Libre-service » fait partie du jargon levé autour à l’intérieur de nombreux services informatiques sur hello world avec différentes significations. marché de Hello est submergé de produits qui vous permettent de toomanage les groupes locaux, des mots de passe ou des profils utilisateur de cloud de hello ou localement.

La réinitialisation de mot de passe libre-service (SSPR) Azure Active Directory (Azure AD) se distingue par sa facilité d’utilisation et de déploiement. La réinitialisation de mot de passe libre-service Azure AD intègre un ensemble de fonctionnalités qui offrent les avantages suivants :

* Autoriser votre toomanage utilisateurs leur mot de passe
  * Depuis n’importe quel appareil
  * De n’importe quel endroit
  * Quel que soit le moment
* Possibilité de préserver la conformité avec les stratégies que vous définissez en qualité d’administrateur

Si vous êtes prêt, vous pouvez commencer à utiliser Azure AD SSPR en vous aidant de notre [guide de démarrage rapide](active-directory-passwords-getting-started.md) et permettre ainsi à vos utilisateurs de réinitialiser rapidement leur propre mot de passe.

## <a name="what-is-possible"></a>Ce qui est possible

* **Modification de mot de passe libre-service** permet aux utilisateurs finaux ou aux administrateurs toochange leurs mots de passe sans assistance de l’administrateur
* **Déverrouillage de compte de libre-service** permet toounlock des utilisateurs finaux à leur propre compte sans assistance de l’administrateur
* **Réinitialisation du mot de passe libre-service** permet aux utilisateurs finaux ou aux administrateurs tooreset leurs mots de passe automatiquement sans assistance de l’administrateur. La réinitialisation de mot de passe en libre-service nécessite Azure AD Premium ou Basic - [Éditions d’Azure Active Directory](active-directory-editions.md).
* **Réinitialisation du mot de passe par l’administrateur** permet à un administrateur tooreset passe de l’utilisateur final ou d’un autre administrateur à partir de hello [portail Azure](https://docs.microsoft.com/azure/azure-portal-overview)
* **Rapports d’activité de gestion des mots de passe** : donnent aux administrateurs un aperçu de l’activité d’inscription et de réinitialisation des mots de passe dans leur organisation - [Rapports de gestion](active-directory-passwords-reporting.md).
* **L’écriture différée de mot de passe** permet la gestion des mots de passe local du cloud de hello afin que tous les précédents hello scénarios peuvent être effectuées par, ou en nom hello, fédéré ou mot de passe des utilisateurs synchronisés. L’écriture différée de mot de passe nécessite [Azure AD Premium](active-directory-get-started-premium.md).

## <a name="why-choose-azure-ad-self-service-password-reset"></a>Pourquoi opter pour la réinitialisation de mot de passe en libre-service Azure AD

* **Réduction des coûts** : la réinitialisation de mot de passe assistée par le support technique représente généralement 20 % des dépenses d’un service informatique.
* **Améliorer les expériences utilisateur final** et **réduire le volume de support technique** en offrant une fin utilisateurs hello power tooresolve leurs propres problèmes de mot de passe à la fois sans appel à un support technique ou d’ouverture d’une demande de prise en charge.
* **Encouragement à la mobilité** : les utilisateurs peuvent réinitialiser leur mot de passe où qu’ils se trouvent.

## <a name="azure-ad-self-service-password-reset-availability"></a>Disponibilité de la réinitialisation de mot de passe en libre-service Azure AD

La réinitialisation de mot de passe libre-service Azure AD est disponible dans trois niveaux, selon votre abonnement.

* **Azure AD Gratuit** : les administrateurs chargés uniquement du cloud peuvent réinitialiser leur propre mot de passe.
* **Azure AD De base** ou tout **abonnement Office 365 payé** : les clients utilisant uniquement le cloud et les administrateurs chargés uniquement du cloud peuvent réinitialiser leur propre mot de passe.
* **Azure AD Premium** : n’importe quel utilisateur ou administrateur, notamment les clients utilisant uniquement le cloud et les utilisateurs fédérés ou synchronisés par mot de passe, peuvent réinitialiser leur propre mot de passe. Les mots de passe locaux requièrent toobe d’écriture différée de mot de passe activée.

## <a name="azure-ad-self-service-password-reset-a-sum-of-hello-parts"></a>Azure AD mot de passe libre-service réinitialiser, une somme de parties de hello

Mot de passe libre-service, réinitialiser dans Azure AD est constitué par hello suivant des composants :

* **Portail de configuration de gestion de mot de passe** où vous pouvez contrôler les options pour la gestion des mots de passe dans votre locataire via hello portail Azure
* **Portail d’inscription à la réinitialisation de mot de passe** : permet aux utilisateurs de s’inscrire à la réinitialisation de mot de passe.
* **Portail de réinitialisation du mot de passe** où les utilisateurs peuvent réinitialiser leur mot de passe à l’aide des défis hello définis par l’administrateur de hello et les utilisateurs des réponses hello ont été fournis
* **Portail de changement de mot de passe utilisateur** : permet aux utilisateurs de changer leur propre mot de passe en entrant leur ancien mot de passe et en indiquant le nouveau.
* **Rapports de gestion des mots de passe** où les administrateurs peuvent afficher et analyser l’activité de mot de passe des rapports pour leurs clients Bonjour portail Azure
* **Mot de passe d’écriture différée à l’aide d’Azure AD Connect tooon local** permet de vous tooenable gestion de localement, fédéré, ou le mot de passe synchronisé les utilisateurs du cloud de hello

## <a name="azure-ad-pricing-sla-updates-and-roadmap"></a>Tarifs, contrat SLA, mises à jour et feuille de route Azure AD

Plus de détails sur ces rubriques se trouvent sur hello suivant des pages

* [**Détails concernant les tarifs d’Azure AD**](https://azure.microsoft.com/pricing/details/active-directory/)
* [**Tarifs d’Office 365**](https://products.office.com/compare-all-microsoft-office-products?tab=2)
* [**Contrats de niveau de service Azure**](https://azure.microsoft.com/support/legal/sla/)
* [**Contrat SLA Microsoft Online Services**](http://go.microsoft.com/fwlink/?LinkID=272026&clcid=0x409)
* [**Mises à jour Azure**](https://azure.microsoft.com/updates/)
* [**Feuille de route Azure**](https://www.microsoft.com/cloud-platform/roadmap-recently-available)

## <a name="next-steps"></a>Étapes suivantes

Hello suivant liens fournit des informations supplémentaires concernant le mot de passe réinitialisé à l’aide d’Azure AD

* [**Démarrage rapide**](active-directory-passwords-getting-started.md) : soyez rapidement opérationnel avec la gestion des mots de passe en libre-service d’Azure AD. 
* [**Licences**](active-directory-passwords-licensing.md) : configurez vos licences Azure AD.
* [**Données** ](active-directory-passwords-data.md) : comprendre les données de hello est nécessaire et comment il est utilisé pour la gestion de mot de passe
* [**Déploiement** ](active-directory-passwords-best-practices.md) -planifier et déployer des utilisateurs de tooyour SSPR hello d’aide est disponible ici
* [**Personnaliser** ](active-directory-passwords-customize.md) -personnaliser hello apparence Hello SSPR expérience pour votre entreprise.
* [**Rapports**](active-directory-passwords-reporting.md) : découvrez si, quand et où vos utilisateurs accèdent aux fonctionnalités de réinitialisation de mot de passe en libre-service
* [**Présentation approfondie technique** ](active-directory-passwords-how-it-works.md) -accédez derrière hello RIDEAU toounderstand son fonctionnement
* [**Forum Aux Questions (FAQ)**](active-directory-passwords-faq.md) : Comment ? Pourquoi ? Quoi ? Où ? Qui ? Quand ? -Réponses tooquestions vous souhaitiez toujours tooask
* [**Résoudre les problèmes** ](active-directory-passwords-troubleshoot.md) -en savoir comment tooresolve commun problèmes que nous pouvons voir avec SSPR

