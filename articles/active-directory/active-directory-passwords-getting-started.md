---
title: "Démarrage rapide : Azure AD SSPR | Microsoft Docs"
description: "Déployer rapidement la réinitialisation de mot de passe en libre-service Azure AD"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: bde8799f-0b42-446a-ad95-7ebb374c3bec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 4fed3a1c690fd6423ee5d3e5baef690d8896fbe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-azure-ad-self-service-password-reset"></a>Démarrage rapide : Réinitialisation de mot de passe en libre-service Azure AD

> [!IMPORTANT]
> **Rencontrez-vous des problèmes de connexion ?** Dans ce cas, [voici comment vous pouvez modifier et réinitialiser votre mot de passe](active-directory-passwords-update-your-own-password.md).

## <a name="rapidly-deploy-self-service-password-reset"></a>Déployer rapidement la réinitialisation de mot de passe en libre-service

Mot de passe libre-service réinitialisé (SSPR) offre un simple signifie pour informatique administrateurs tooempower utilisateurs tooreset ou déverrouiller leurs comptes ou les mots de passe. Hello système inclut tootrack de création de rapports détaillé lorsque les utilisateurs utilisent le système de hello, ainsi que des notifications tooalert vous toomisuse ou les abus.

Ce guide part du principe que vous avez déjà une version d’essai opérationnelle ou une licence de locataire Azure AD. Si vous avez besoin d’aide pour configurer Azure AD, voir l’article hello [prise en main d’Azure AD](https://azure.microsoft.com/trial/get-started-active-directory/).

1. À partir de votre locataire Azure AD existant, sélectionnez **Réinitialisation de mot de passe**

2. À partir de hello **« Propriétés »** écran, sous l’option hello « Self Service mot de passe réinitialisé activé » choisissez hello suivantes
    * Personne - personne est une fonctionnalité SSPR toouse en mesure de
    * Un groupe - seuls les membres d’un Azure AD spécifique du groupe que vous choisissez sont des fonctionnalités de libre-service en mesure de toouse
    * Tout le monde - tous les utilisateurs disposant de comptes dans votre locataire Azure AD sont une fonctionnalité SSPR toouse en mesure de

3. À partir de hello **« Méthodes d’authentification »** écran Choisissez
    * Nombre de méthodes requis tooreset - nous prenons en charge un minimum ou un maximum de deux
    * Méthodes toousers disponible - Nous avons besoin au moins un mais il peut être judicieux de toohave un choix supplémentaire disponible
        * **Messagerie** envoie un message électronique à un utilisateur de toohello code configurée de l’adresse de messagerie de l’authentification
        * **Téléphone mobile** donne hello utilisateur hello choix tooreceive un appel ou de texte avec un code de tootheir configuré le numéro de téléphone mobile
        * **Téléphone de bureau** utilisateur de hello d’appels avec un code de tootheir configuré numéro de téléphone professionnel
        * **Les Questions de sécurité** nécessite que vous toochoose
            * Nombre de questions requis tooregister - minimum hello pour une inscription réussie, ce qui signifie un utilisateur peut choisir tooanswer toocreate plus d’un pool de toopull à partir de questions. Cette option peut être définie à partir de 3 à 5 et doit être supérieure à ou égal nombre toohello de tooreset obligatoire de questions.
                * Questions personnalisées peuvent être ajoutées en cliquant sur bouton de « Custom » hello lors de la sélection des questions de sécurité
            * Nombre de questions requises tooreset - peut être définie à partir de 3 à 5 questions toobe est a répondu correctement avant d’autoriser un toobe de mot de passe utilisateurs réinitialiser ou déverrouillé.

4. RECOMMANDÉ : **« Personnalisation »** vous permet de toochange hello « Contactez votre administrateur » lien toopoint tooa page ou adresse de messagerie vous définissez

5. FACULTATIF : hello **« Registration »** écran fournit aux administrateurs des options de hello pour :
    * Exiger des utilisateurs tooregister lors de la connexion
    * Nombre de jours avant que les utilisateurs sont invités à tooreconfirm leurs informations d’authentification

6. FACULTATIF : hello **« Notification »** écran fournit aux administrateurs des options de hello pour :
    * Notifier les utilisateurs lors des réinitialisations de mot de passe ?
    * Notifier tous les administrateurs quand d’autres administrateurs réinitialisent leur mot de passe ?

**À ce stade, vous avez configuré la réinitialisation de mot de passe en libre-service pour votre locataire Azure AD**. Vous pouvez vous arrêter là ou continuer sur tooconfigure la synchronisation des mots de passe tooan domaine Active Directory sur site.

> [!NOTE]
> Testez la réinitialisation de mot de passe en libre-service avec un utilisateur et non un administrateur, car Microsoft applique des spécifications d’authentification forte pour les comptes Administrateur Azure. Pour plus d’informations sur la stratégie de mot de passe administrateur hello, consultez notre [article de stratégie de mot de passe](active-directory-passwords-policy.md#administrator-password-policy-differences).

## <a name="configure-synchronization-tooexisting-identity-source"></a>Configurer la source de synchronisation d’identité tooexisting

tooenable tooAzure de synchronisation d’identité Active Directory sur site, vous devez tooinstall et configurer [Azure AD Connect](./connect/active-directory-aadconnect.md) sur un serveur de votre organisation. Cette application gère la synchronisation des utilisateurs et des groupes à partir de votre identité source tooyour Azure AD de client existant.

* [Mise à niveau à partir de la synchronisation d’annuaire ou Azure AD Sync tooAzure AD Connect](./connect/active-directory-aadconnect-dirsync-deprecated.md)
* [Prise en main d’Azure AD Connect à l’aide de paramètres express](./connect/active-directory-aadconnect-get-started-express.md)
* [Configurer l’écriture différée de mot de passe](active-directory-passwords-writeback.md#configuring-password-writeback) toowrite des mots de passe d’Azure AD sauvegarder tooyour locale active.

## <a name="disabling-self-service-password-reset"></a>Désactivation de la réinitialisation de mot de passe en libre-service

La désactivation de réinitialisation de mot de passe libre-service est aussi simple que l’ouverture de votre client Azure AD et va trop**réinitialisation de mot de passe > Propriétés** > choisissez **aucun** sous **réinitialisation de mot de passe libre-service Activé**

### <a name="learn-more"></a>En savoir plus
Hello suivant liens fournit des informations supplémentaires concernant le mot de passe réinitialisé à l’aide d’Azure AD

* [**Licences**](active-directory-passwords-licensing.md) : configurez vos licences Azure AD.
* [**Données** ](active-directory-passwords-data.md) : comprendre les données de hello est nécessaire et comment il est utilisé pour la gestion de mot de passe
* [**Déploiement** ](active-directory-passwords-best-practices.md) -planifier et déployer des utilisateurs de tooyour SSPR hello d’aide est disponible ici
* [**Personnaliser** ](active-directory-passwords-customize.md) -personnaliser hello apparence Hello SSPR expérience pour votre entreprise.
* [**Stratégie**](active-directory-passwords-policy.md) : comprenez et définissez les stratégies de mot de passe d’Azure AD
* [**Rapports**](active-directory-passwords-reporting.md) : découvrez si, quand et où vos utilisateurs accèdent aux fonctionnalités de réinitialisation de mot de passe en libre-service
* [**Présentation approfondie technique** ](active-directory-passwords-how-it-works.md) -accédez derrière hello RIDEAU toounderstand son fonctionnement
* [**Forum Aux Questions (FAQ)**](active-directory-passwords-faq.md) : Comment ? Pourquoi ? Quoi ? Où ? Qui ? Quand ? -Réponses tooquestions vous souhaitiez toujours tooask
* [**Résoudre les problèmes** ](active-directory-passwords-troubleshoot.md) -en savoir comment tooresolve commun problèmes que nous pouvons voir avec SSPR

## <a name="next-steps"></a>Étapes suivantes

Ce guide de démarrage rapide, vous avez appris à la méthode de réinitialisation de mot de passe libre-service tooconfigure pour vos utilisateurs. toocontinue toohello Azure toocomplete portail ces étapes suivent hello lien toohello portal.

> [!div class="nextstepaction"]
> [Activer la réinitialisation du mot de passe libre-service](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/PasswordReset)

