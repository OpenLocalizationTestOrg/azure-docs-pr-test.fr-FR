---
title: "Lancement de la réinitialisation du mot de passe libre-service Azure AD | Microsoft Docs"
description: "Conseils pour réussir le lancement de la réinitialisation du mot de passe libre-service Azure AD"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: f8cd7e68-2c8e-4f30-b326-b22b16de9787
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 73d31679b38ff009a767335adaebc49fbc5a75b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="roll-out-password-reset-for-users"></a>Lancer la réinitialisation du mot de passe des utilisateurs

La plupart des clients les étapes hello qui suivent tooensure optimiser le déploiement de la fonctionnalité SSPR.

1. [Activez la réinitialisation du mot de passe dans votre répertoire](active-directory-passwords-getting-started.md).
2. [Configurez les autorisations Active Directory locales pour l’écriture différée du mot de passe](active-directory-passwords-how-it-works.md#active-directory-permissions).
3. [Configurer l’écriture différée de mot de passe](active-directory-passwords-writeback.md#configuring-password-writeback) toowrite des mots de passe d’Azure AD sauvegarder tooyour locale active
4. [Affectez et vérifiez les licences requises](active-directory-passwords-licensing.md).
5. Si vous souhaitez tooroll progressivement, vous pouvez éventuellement limite mot de passe réinitialisé groupe tooa de tooroll les utilisateurs à la fonctionnalité de hello lentement au fil du temps. toodo ce défini hello **Self Service mot de passe réinitialisé activé** passer de **tout le monde** trop**un groupe** et sélectionnez un tooenable du groupe de sécurité pour la réinitialisation du mot de passe. Hello membres de ce groupe doivent tous avoir toothem de licences attribuées et est un excellent moyen tooenable [groupe de licence](active-directory-passwords-licensing.md#enable-group-or-user-based-licensing).
6. Remplir le jeu minimal de hello de [des données d’authentification](active-directory-passwords-data.md), en fonction de votre stratégie.
7. Apprendre à vos utilisateurs toouse SSPR, en leur envoyant des instructions tooshow les comment tooregister et comment tooreset.
    > [!NOTE]
    > Testez la réinitialisation de mot de passe en libre-service avec un utilisateur et non un administrateur, car Microsoft applique des spécifications d’authentification forte pour les comptes Administrateur Azure. Pour plus d’informations sur la stratégie de mot de passe administrateur hello, consultez notre [l’article de présentation approfondie](active-directory-passwords-how-it-works.md).

8. Vous pouvez choisir d’inscription de tooenforce à tout moment et nécessitent les utilisateurs tooreconfirm leurs informations d’authentification après un certain temps. Si vous ne souhaitez pas votre tooregister de toohave les utilisateurs, vous pouvez [déployer le mot de passe réinitialisé sans nécessiter d’inscription de l’utilisateur final](active-directory-passwords-data.md).
9. Au fil du temps, examinez les utilisateurs de l’inscription et l’utilisation en consultant hello [reporting fournie par Azure AD](active-directory-passwords-reporting.md).

## <a name="email-based-rollout"></a>Déploiement par courrier électronique

De nombreux clients de trouver qu'une campagne de courrier électronique, avec des instructions toouse simple, est hello plus simple façon tooget utilisateurs toouse SSPR. [Nous avons créé trois messages électroniques simples que vous pouvez utiliser comme modèles toohelp dans votre déploiement.](https://onedrive.live.com/?authkey=%21AD5ZP%2D8RyJ2Cc6M&id=A0B59A91C740AB16%2125063&cid=A0B59A91C740AB16)

* **Bientôt** toobe de modèle utilisée dans les semaines hello ou de jours avant que les utilisateurs de déploiement toolet savent dont ils ont besoin toodo quelque chose de messagerie.
* **Disponible pour l’instant** jour de hello modèle toobe utilisé de lancement toodrive utilisateurs tooregister de messagerie et de confirmer leurs données d’authentification afin de pouvoir utiliser SSPR quand ils en ont besoin.
* **Inscrire le rappel** envoyer par courrier électronique de modèle pour quelques jours tooweeks après déploiement tooremind utilisateurs tooregister et confirmer leurs données d’authentification.

## <a name="creating-your-own-password-portal"></a>Création de votre propre portail de mot de passe

Nombre de nos clients supérieure choisir la page Web de toohost et créer une entrée DNS, comme https://passwords.contoso.com racine. Ils remplissent cette page avec la réinitialisation de mot de passe de liens toohello Azure AD, réinitialisation de mot de passe d’inscription, les portails de modification de mot de passe et autres informations spécifiques à l’organisation. Dans les communications par courrier électronique ou un prospectus, vous envoyez, vous pouvez inclure une marque, facile à mémoriser, les URL que les utilisateurs peuvent accéder toowhen dont ils ont besoin de services de hello toouse.

* Portail de réinitialisation de mot de passe : https://passwordreset.microsoftonline.com/
* Portail d’inscription à la réinitialisation de mot de passe : http://aka.ms/ssprsetup
* Portail de modification de mot de passe : https://account.activedirectory.windowsazure.com/ChangePassword.aspx

## <a name="using-enforced-registration"></a>Utilisation de l’inscription forcée

Si vous souhaitez que votre tooregister d’utilisateurs pour la réinitialisation du mot de passe, vous pouvez forcer tooregister quand ils se connectent à l’aide d’Azure AD. Vous pouvez activer cette option à partir de votre annuaire **mot de passe réinitialisé** panneau en activant hello **tooRegister de demander aux utilisateurs lors de la connexion** option hello **inscription** onglet.

Les administrateurs peuvent demander aux utilisateurs dans le Registre toore après une période de temps en définissant un hello **nombre de jours avant que les utilisateurs sont invités à tooreconfirm leurs informations d’authentification** entre 0-730 jours.

Après avoir activé cette option, les utilisateurs se connectant verront un message les informant que leur administrateur leur impose tooverify leurs informations d’authentification.

## <a name="populate-authentication-data"></a>Renseigner les données d’authentification

Si vous [remplir de données d’authentification pour vos utilisateurs](active-directory-passwords-data.md), puis les utilisateurs n’ont pas besoin tooregister de mot de passe réinitialisé avant d’être en mesure de toouse SSPR. Tant que les utilisateurs disposent de données de l’authentification hello définies qui répond à la stratégie de réinitialisation du mot de passe hello que vous avez défini, les utilisateurs sont en mesure de tooreset leurs mots de passe.

## <a name="disabling-self-service-password-reset"></a>Désactivation de la réinitialisation de mot de passe en libre-service

La désactivation de réinitialisation de mot de passe libre-service est aussi simple que l’ouverture de votre client Azure AD et va trop**mot de passe réinitialisé**, **propriétés**et en choisissant **personne** sous  **Réinitialisation du mot de passe activée**

## <a name="next-steps"></a>Étapes suivantes

Hello suivant liens fournit des informations supplémentaires concernant le mot de passe réinitialisé à l’aide d’Azure AD

* [**Démarrage rapide**](active-directory-passwords-getting-started.md) : soyez rapidement opérationnel avec la gestion des mots de passe en libre-service d’Azure AD. 
* [**Licences**](active-directory-passwords-licensing.md) : configurez vos licences Azure AD.
* [**Données** ](active-directory-passwords-data.md) : comprendre les données de hello est nécessaire et comment il est utilisé pour la gestion de mot de passe
* [**Personnaliser** ](active-directory-passwords-customize.md) -personnaliser hello apparence Hello SSPR expérience pour votre entreprise.
* [**Stratégie**](active-directory-passwords-policy.md) : comprenez et définissez les stratégies de mot de passe d’Azure AD
* [**Écriture différée du mot de passe**](active-directory-passwords-writeback.md) : fonctionnement de l’écriture différée du mot de passe avec votre répertoire local.
* [**Rapports**](active-directory-passwords-reporting.md) : découvrez si, quand et où vos utilisateurs accèdent aux fonctionnalités de réinitialisation de mot de passe en libre-service
* [**Présentation approfondie technique** ](active-directory-passwords-how-it-works.md) -accédez derrière hello RIDEAU toounderstand son fonctionnement
* [**Forum Aux Questions (FAQ)**](active-directory-passwords-faq.md) : Comment ? Pourquoi ? Quoi ? Où ? Qui ? Quand ? -Réponses tooquestions vous souhaitiez toujours tooask
* [**Résoudre les problèmes** ](active-directory-passwords-troubleshoot.md) -en savoir comment tooresolve commun problèmes que nous pouvons voir avec SSPR
