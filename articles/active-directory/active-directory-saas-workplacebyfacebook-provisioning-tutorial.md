---
title: "Didacticiel : Intégration d’Azure Active Directory à Workplace par Facebook | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Workplace by Facebook."
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
ms.openlocfilehash: 9b22679c304248ed7ba7a6bd9eaf82b64f7143cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-workplace-by-facebook-for-user-provisioning"></a>Didacticiel : Configuration de Workplace by Facebook pour l’approvisionnement des utilisateurs

L’objectif de ce didacticiel est de vous montrer les étapes à effectuer dans Workplace by Facebook et Azure AD pour approvisionner et déprovisionner automatiquement des comptes d’utilisateur d’Azure AD vers Workplace by Facebook.

## <a name="prerequisites"></a>Composants requis

Pour configurer l’intégration d’Azure AD avec Workplace by Facebook, vous avez besoin des éléments suivants :

- Un abonnement Azure AD
- Un abonnement Workplace by Facebook pour lequel l’authentification unique est activée

> [!NOTE]
> Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.

Vous devez en outre suivre les recommandations ci-dessous :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="assigning-users-to-workplace-by-facebook"></a>Affectation d’utilisateurs à Workplace by Facebook

Azure Active Directory utilise un concept appelé « affectations » pour déterminer les utilisateurs devant recevoir l’accès aux applications sélectionnées. Dans le cadre de l’approvisionnement automatique des comptes d’utilisateur, seuls les utilisateurs et les groupes qui ont été « affectés » à une application dans Azure AD sont synchronisés.

Avant de configurer et d’activer le service d’approvisionnement, vous devez déterminer quels utilisateurs et/ou groupes dans Azure AD représentent les utilisateurs qui ont besoin d’accéder à votre application Workplace by Facebook. Une fois que vous avez choisi, vous pouvez affecter ces utilisateurs à votre application Workplace by Facebook en suivant les instructions fournies ici :

[Affecter un utilisateur ou un groupe à une application d’entreprise](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-workplace-by-facebook"></a>Conseils importants concernant l’affectation d’utilisateurs à Workplace by Facebook

*   Nous vous recommandons de n’assigner qu’un seul utilisateur Azure AD à Workplace by Facebook afin de tester la configuration de l’approvisionnement. Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.

*   Quand vous assignez un utilisateur à Workplace by Facebook, vous devez sélectionner un rôle d’utilisateur valide. Le rôle « Accès par défaut » ne fonctionne pas pour l’approvisionnement.

## <a name="enable-user-provisioning"></a>Activer l’approvisionnement d’utilisateurs

Cette section vous explique comment connecter votre annuaire Azure AD à l’API d’approvisionnement de comptes d’utilisateur Workplace by Facebook, et comment créer, mettre à jour et désactiver les comptes utilisateur affectés dans Workplace by Facebook en fonction des affectations d’utilisateurs et de groupes dans Azure AD.

>[!Tip]
>Vous pouvez également choisir d’activer l’authentification unique basée sur SAML pour Workplace by Facebook, grâce aux instructions disponibles sur le [portail Azure](https://portal.azure.com). L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que chacune de ces deux fonctionnalités compléte l’autre.

### <a name="to-configure-user-account-provisioning-to-workplace-by-facebook-in-azure-ad"></a>Pour configurer l’approvisionnement de comptes d’utilisateur vers Workplace by Facebook dans Azure AD

Cette section décrit comment activer l’approvisionnement des comptes d’utilisateur Active Directory vers Workplace by Facebook.

Azure AD prend en charge la possibilité de synchroniser automatiquement les informations de compte des utilisateurs affectés à Workplace by Facebook. La synchronisation automatique permet à Workplace by Facebook d’obtenir les données nécessaires pour autoriser l’accès des utilisateurs, avant leur première tentative de connexion. Elle annule également l’approvisionnement des utilisateurs à Workplace by Facebook lorsque l’accès a été révoqué dans Azure AD.

1. Sur le [portail Azure](https://portal.azure.com), accédez à la section **Azure Active Directory** > **Applications d’entreprise** > **Toutes les applications**.

2. Si vous avez déjà configuré Workplace by Facebook pour l’authentification unique, recherchez votre instance de Workplace by Facebook à l’aide du champ de recherche. Sinon, sélectionnez **Ajouter** et recherchez **Workplace by Facebook** dans la galerie d’applications. Sélectionnez Workplace by Facebook dans les résultats de recherche et ajoutez-le à votre liste d’applications.

3. Sélectionnez votre instance de Workplace by Facebook, puis sélectionnez l’onglet **Approvisionnement**.

4. Définissez le **Mode d’approvisionnement** sur **Automatique**. 

    ![approvisionnement](./media/active-directory-saas-workplacebyfacebook-provisioning-tutorial/provisioning.png)

5. Dans la section **Informations d’identification de l’administrateur**, entrez le jeton secret et l’URL d’abonné de votre administrateur Workplace by Facebook.

6. Sur le portail Azure, cliquez sur **Tester la connexion** pour vérifier qu’Azure AD peut se connecter à votre application Workplace by Facebook. Si la connexion échoue, vérifiez que votre compte Workplace by Facebook dispose des autorisations d’administrateur d’équipe.

7. Entrez l’adresse e-mail d’une personne ou d’un groupe qui doit recevoir les notifications d’erreur d’approvisionnement dans le champ **E-mail de notification**, et cochez la case.

8. Cliquez sur **Enregistrer.**

9. Dans la section Mappages, sélectionnez **Synchroniser des utilisateurs Azure Active Directory avec Workplace by Facebook**.

10. Dans la section **Mappages d’attributs**, passez en revue les attributs utilisateur qui sont synchronisés à partir d’Azure AD vers Workplace by Facebook. Les attributs sélectionnés en tant que propriétés de **Correspondance** servent à faire correspondre les comptes d’utilisateur dans Workplace by Facebook, en vue d’opérations de mise à jour. Cliquez sur le bouton Enregistrer pour valider les modifications.

11. Pour activer le service d’approvisionnement Azure AD pour Workplace by Facebook, modifiez le paramètre **État de l’approvisionnement** en spécifiant **Activé** dans la section **Paramètres**.

12. Cliquez sur **Enregistrer.**

Pour plus d’informations sur la façon de configurer l’approvisionnement automatique, consultez [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers).

Vous pouvez désormais créer un compte de test. Patientez jusqu’à 20 minutes avant de vérifier que le compte a bien été synchronisé avec Workplace by Facebook.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)
* [Configurer l’authentification unique](active-directory-saas-workplacebyfacebook-tutorial.md)

