---
title: "Didacticiel : configurer Workplace by Facebook pour l’approvisionnement des utilisateurs | Documents Microsoft"
description: "Découvrez comment tooautomatically approvisionner et configurer des comptes d’utilisateurs tooWorkplace Azure AD par Facebook."
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
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 33d294dbc8f441b29138408b3c9ca41f2141f8af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configure-workplace-by-facebook-for-user-provisioning"></a>Didactiel : configurer Workplace by Facebook pour l’approvisionnement des utilisateurs

Ce didacticiel montre que vous hello tooautomatically nécessaire d’étapes configurer et annuler la configuration des comptes d’utilisateur de tooWorkplace d’Azure Active Directory (Azure AD) par Facebook.

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec l’espace de travail par Facebook, hello éléments suivants sont nécessaires :

- Un abonnement Azure AD
- Un abonnement Workplace by Facebook pour lequel l’authentification unique est activée

étapes de hello tootest dans ce didacticiel, suivez ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir une [offre d’essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="assign-users-tooworkplace-by-facebook"></a>Affecter les utilisateurs des tooWorkplace par Facebook

Azure AD utilise un concept appelé toodetermine « affectations » les utilisateurs qui doivent recevoir l’accès tooselected applications. Dans le contexte de hello de configuration de compte automatique d’utilisateurs, seuls les utilisateurs de hello et les groupes qui ont été attribuées application tooan dans Azure AD sont synchronisés.

Avant de configurer et activer hello service, l’approvisionnement décider quels utilisateurs et groupes dans Azure AD représentent les utilisateurs de hello qui a besoin d’accès tooyour espace de travail par application Facebook. Vous pouvez ensuite affecter ces tooyour utilisateurs espace de travail par application Facebook en suivant hello les instructions de [affecter un utilisateur ou groupe d’applications d’entreprise tooan](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).

>[!IMPORTANT]
>*   Hello de test configuration de configuration en affectant une seule tooWorkplace d’utilisateur Azure AD par Facebook. Affectez des groupes et des utilisateurs supplémentaires ultérieurement.
>*   Lorsque vous affectez un tooWorkplace utilisateur par Facebook, vous devez sélectionner un rôle d’utilisateur valide. rôle d’accès par défaut Hello ne fonctionne pas pour la configuration.

## <a name="enable-automated-user-provisioning"></a>Activer l’approvisionnement automatique des utilisateurs

Cette section vous guide tout au long de la connexion de votre compte d’utilisateur Azure AD toohello provisionnement des API d’espace de travail par Facebook. Vous apprendrez également comment tooconfigure hello configuration service toocreate, mettre à jour et désactiver les comptes d’utilisateur affecté dans l’espace de travail par Facebook. Cela est fondé sur l’affectation d’utilisateurs et de groupes dans Azure AD.

>[!Tip]
>Vous pouvez également choisir tooenabled authentification SAML pour l’espace de travail par Facebook, en suivant les instructions hello prévues hello [portail Azure](https://portal.azure.com). L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que ces deux fonctionnalités se complètent.

### <a name="configure-user-account-provisioning-tooworkplace-by-facebook-in-azure-ad"></a>Configurer le compte d’utilisateur de configuration tooWorkplace par Facebook dans Azure AD

Azure prend en charge d’AD hello capacité tooautomatically synchroniser détails du compte de hello affecté tooWorkplace utilisateurs par Facebook. La synchronisation automatique permet d’espace de travail par les données de hello Facebook tooget lui tooauthorize des utilisateurs pour l’accès, avant leur tentative toosign dans pour hello première fois. Elle annule également l’approvisionnement des utilisateurs à Workplace by Facebook lorsque l’accès a été révoqué dans Azure AD.

1. Bonjour [portail Azure](https://portal.azure.com), sélectionnez **Azure Active Directory** > **applications d’entreprise** > **toutes les applications**.

2. Si vous avez déjà configuré l’espace de travail par Facebook pour l’authentification unique, recherchez votre instance de l’espace de travail par Facebook à l’aide du champ de recherche hello. Sinon, sélectionnez **ajouter** et recherchez **espace de travail par Facebook** dans la galerie d’applications hello. Sélectionnez **espace de travail par Facebook** de hello résultats de la recherche, puis l’ajouter tooyour la liste des applications.

3. Sélectionnez votre instance de l’espace de travail par Facebook, puis hello **Provisioning** onglet.

4. Définissez **Mode d’approvisionnement** trop**automatique**. 

    ![Capture instantanée des options d’approvisionnement de Workspace by Facebook](./media/active-directory-saas-facebook-at-work-provisioning-tutorial/provisioning.png)

5. Sous hello **informations d’identification administrateur** section, entrez hello **Secret jeton** et hello **URL de client** votre espace de travail par un administrateur de Facebook.

6. Bonjour portail Azure, sélectionnez **tester la connexion** tooensure Azure AD peut se connecter tooyour espace de travail par application Facebook. Si la connexion de hello échoue, assurez-vous que votre espace de travail par compte Facebook dispose d’autorisations d’administrateur d’équipe.

7. Entrez hello adresse de messagerie d’une personne ou un groupe qui doit recevoir des notifications d’erreur approvisionnement hello **courrier électronique de Notification** champ et la case à cocher hello.

8. Sélectionnez **Enregistrer**.

9. Sous la section des mappages de hello, sélectionnez **tooWorkplace de synchronisation Azure Active Directory Users par Facebook**.

10. Bonjour **des mappages d’attributs** section, passez en revue les attributs utilisateur hello sont synchronisées à partir d’Azure AD tooWorkplace par Facebook. Hello attributs sélectionnés en tant que **correspondance** propriétés sont des comptes d’utilisateur hello toomatch utilisé dans l’espace de travail par Facebook pour les opérations de mise à jour. sélectionner de toutes les modifications, toocommit **enregistrer**.

11. tooenable hello service de configuration Azure AD pour l’espace de travail par Facebook, Bonjour **paramètres** section, modifier hello **état d’approvisionnement** trop**sur**.

12. Sélectionnez **Enregistrer**.

Pour plus d’informations sur la façon de tooconfigure automatique de configuration, consultez [hello Facebook documentation](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers).

Vous pouvez à présent créer un compte de test. Attendez que les minutes too20 tooverify hello compte a été synchronisé tooWorkplace par Facebook.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)
* [Configurer l’authentification unique](active-directory-saas-facebook-at-work-tutorial.md)

