---
title: "Didacticiel : Intégration d’Azure Active Directory à Workplace par Facebook | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et l’espace de travail par Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6341e67e-8ce6-42dc-a4ea-7295904a53ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 551ec353a5ec1da936373587688c299a6f4acca7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-workplace-by-facebook-for-user-provisioning"></a>Didacticiel : Configuration de Workplace by Facebook pour l’approvisionnement des utilisateurs

objectif Hello de ce didacticiel est tooshow vous hello étapes que vous devez tooperform dans l’espace de travail par Facebook et Azure AD tooautomatically approvisionner et configurer des comptes d’utilisateur de tooWorkplace d’Azure AD par Facebook.

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec l’espace de travail par Facebook, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Workplace by Facebook pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="assigning-users-tooworkplace-by-facebook"></a>Affectation de tooWorkplace les utilisateurs par Facebook

Azure Active Directory utilise un concept appelé toodetermine « affectations » les utilisateurs qui doivent recevoir l’accès tooselected applications. Dans le contexte de hello de configuration de compte automatique d’utilisateurs, seuls les utilisateurs de hello et les groupes qui ont été « affectés » application tooan dans Azure AD est synchronisé.

Avant de configurer et de l’activation de hello service de configuration, vous devez toodecide quels utilisateurs ou des groupes dans Azure AD représentent hello des utilisateurs qui doivent accéder aux tooyour espace de travail par application Facebook. Après choisi, vous pouvez attribuer ces tooyour utilisateurs espace de travail par application Facebook en suivant les instructions hello ici :

[Affecter une application d’entreprise tooan utilisateur ou un groupe](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-tooworkplace-by-facebook"></a>Conseils importants pour l’assignation tooWorkplace utilisateurs par Facebook

*   Il est recommandé qu’un seul utilisateur Azure AD est affecté au tooWorkplace Facebook tootest hello est mise en service de configuration. Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.

*   Lorsque vous affectez un tooWorkplace utilisateur par Facebook, vous devez sélectionner un rôle d’utilisateur valide. rôle de « Accès par défaut » Hello ne fonctionne pas pour la configuration.

## <a name="enable-user-provisioning"></a>Activer l’approvisionnement des utilisateurs

Cette section vous guide à travers de la connexion de votre tooWorkplace Azure AD par compte d’utilisateur de Facebook à l’API de configuration et configurez hello toocreate du service de configuration, de mettre à jour et de désactiver les comptes d’utilisateur affecté dans l’espace de travail par Facebook en fonction de l’utilisateur et de groupe affectation dans Azure AD.

>[!Tip]
>Vous pouvez également choisir tooenabled basé sur SAML Single Sign-On pour l’espace de travail par Facebook, suivant les instructions hello fournies dans [portail Azure](https://portal.azure.com). L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que chacune de ces deux fonctionnalités compléte l’autre.

### <a name="tooconfigure-user-account-provisioning-tooworkplace-by-facebook-in-azure-ad"></a>compte d’utilisateur tooconfigure configuration tooWorkplace par Facebook dans Azure AD :

objectif Hello de cette section est toooutline comment tooenable configuration d’utilisateur Active Directory de comptes de tooWorkplace par Facebook.

Azure prend en charge d’AD hello capacité tooautomatically synchroniser détails du compte de hello affecté tooWorkplace utilisateurs par Facebook. La synchronisation automatique permet d’espace de travail par les données de hello Facebook tooget lui tooauthorize des utilisateurs pour l’accès, avant leur tentative toosign dans pour hello première fois. Elle annule également l’approvisionnement des utilisateurs à Workplace by Facebook lorsque l’accès a été révoqué dans Azure AD.

1. Bonjour [portail Azure](https://portal.azure.com), parcourir toohello **Azure Active Directory** > **applications d’entreprise** > **detouteslesapplications** section.

2. Si vous avez déjà configuré l’espace de travail par Facebook pour l’authentification unique, recherchez votre instance de l’espace de travail par Facebook à l’aide du champ de recherche hello. Sinon, sélectionnez **ajouter** et recherchez **espace de travail par Facebook** dans la galerie d’applications hello. Sélectionnez l’espace de travail par Facebook hello résultats de recherche et l’ajouter tooyour la liste des applications.

3. Sélectionnez votre instance de l’espace de travail par Facebook, puis hello **Provisioning** onglet.

4. Ensemble hello **Mode d’approvisionnement** trop**automatique**. 

    ![approvisionnement](./media/active-directory-saas-workplacebyfacebook-provisioning-tutorial/provisioning.png)

5. Sous hello **informations d’identification administrateur** section, entrez hello jeton Secret et hello URL de client de votre espace de travail par un administrateur de Facebook.

6. Bonjour portail Azure, cliquez sur **tester la connexion** tooensure Azure AD peut se connecter tooyour espace de travail par application Facebook. Si la connexion de hello échoue, vérifiez que votre espace de travail par compte Facebook a des autorisations d’administrateur d’équipe.

7. Entrez hello adresse de messagerie d’une personne ou un groupe qui doit recevoir des notifications d’erreur approvisionnement hello **courrier électronique de Notification** champ et la case à cocher hello.

8. Cliquez sur **Enregistrer.**

9. Sous la section des mappages de hello, sélectionnez **tooWorkplace de synchronisation Azure Active Directory Users par Facebook.**

10. Bonjour **des mappages d’attributs** section, passez en revue les attributs utilisateur hello sont synchronisées à partir d’Azure AD tooWorkplace par Facebook. Hello attributs sélectionnés en tant que **correspondance** propriétés sont des comptes d’utilisateur hello toomatch utilisé dans l’espace de travail par Facebook pour les opérations de mise à jour. Sélectionnez toocommit de bouton hello enregistrer toutes les modifications.

11. tooenable hello service de configuration d’Azure AD pour l’espace de travail par Facebook, modification hello **état d’approvisionnement** trop**sur** Bonjour **paramètres** section

12. Cliquez sur **Enregistrer.**

Pour plus d’informations sur la façon de tooconfigure automatique de configuration, consultez [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)

Vous pouvez à présent créer un compte de test. Attendez que les minutes too20 tooverify hello compte a été synchronisé tooWorkplace par Facebook.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)
* [Configurer l’authentification unique](active-directory-saas-workplacebyfacebook-tutorial.md)

