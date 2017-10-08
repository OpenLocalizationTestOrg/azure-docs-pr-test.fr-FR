---
title: "Didacticiel : Intégration d’Azure Active Directory à Concur | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Concur."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: df47f55f-a894-4e01-a82e-0dbf55fc8af1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 13ba364af26a5ce0f1d2b51aaa0f84a4c353b107
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-concur-for-user-provisioning"></a>Didacticiel : Configuration de Concur pour l’approvisionnement des utilisateurs

objectif Hello de ce didacticiel est tooshow vous hello étapes que vous devez tooperform dans Concur et Azure AD tooautomatically approvisionner et configurer des comptes d’utilisateur à partir d’Azure AD tooConcur.

## <a name="prerequisites"></a>Composants requis

scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :

*   Un locataire Azure Active Directory.
*   Un abonnement Concur pour lequel l’authentification unique est activée
*   Un compte d’utilisateur dans Concur avec les autorisations d’administrateur d’équipe

## <a name="assigning-users-tooconcur"></a>Affectation d’utilisateurs tooConcur

Azure Active Directory utilise un concept appelé toodetermine « affectations » les utilisateurs qui doivent recevoir l’accès tooselected applications. Dans le contexte de hello de configuration de compte automatique d’utilisateurs, seuls les utilisateurs de hello et les groupes qui ont été « affectés » application tooan dans Azure AD est synchronisé.

Avant de configurer et de l’activation de hello service de configuration, vous devez toodecide quels utilisateurs ou des groupes dans Azure AD représentent hello utilisateurs qui doivent accéder à application de Concur tooyour. Une fois décidé, vous pouvez attribuer ces applications de Concur tooyour les utilisateurs en suivant les instructions hello ici :

[Affecter une application d’entreprise tooan utilisateur ou un groupe](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-tooconcur"></a>Conseils importants pour l’affectation d’utilisateurs tooConcur

*   Il est recommandé qu’un seul utilisateur Azure AD avoir tooConcur tootest hello est mise en service de configuration. Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.

*   Lorsque vous affectez un tooConcur d’utilisateur, vous devez sélectionner un rôle d’utilisateur valide. rôle de « Accès par défaut » Hello ne fonctionne pas pour la configuration.

## <a name="enable-user-provisioning"></a>Activer l’approvisionnement d’utilisateurs

Cette section vous guide à travers de la connexion du compte d’utilisateur de votre tooConcur AD Azure API de configuration et configurez hello toocreate du service de configuration, de mettre à jour et de désactiver les comptes d’utilisateur affecté dans Concur en fonction de l’affectation d’utilisateurs et de groupes dans Azure AD.

> [!Tip] 
> Vous pouvez également choisir tooenabled basé sur SAML Single Sign-On pour Concur, en suivant les instructions hello fournies dans [portail Azure](https://portal.azure.com). L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que chacune de ces deux fonctionnalités compléte l’autre.

### <a name="tooconfigure-user-account-provisioning"></a>approvisionnement des comptes utilisateur tooconfigure :

objectif Hello de cette section est toooutline comment tooenable configuration d’utilisateur Active Directory de comptes de tooConcur.

applications tooenable dans hello Expense Service, il y a une configuration correcte toobe et l’utilisation d’un profil d’administrateur de Service Web. N’ajoutez pas hello WS Admin rôle tooyour profil d’administrateur existant que vous utilisez pour les fonctions administratives T & E.

Concur Consultants ou administrateur de client de hello doit créer un profil d’administrateur de Service Web distinct et administrateur de Client hello doit utiliser ce profil pour les fonctions d’administrateur de Services Web hello (par exemple, l’activation des applications). Ces profils doivent être conservés séparément à partir de quotidienne T & E profil d’administrateur l’administrateur de client hello (hello T & profil d’administrateur E ne doivent pas avoir rôle d’écart hello attribué).

Lorsque vous créez hello profil toobe est utilisé pour activer l’application hello, entrez le nom de l’administrateur de client hello dans les champs du profil utilisateur hello. Cela affecte le profil toohello de la propriété. Après la création d’un ou plusieurs profils, le client de hello doit se connecter avec ce hello tooclick de profil «*activer*» bouton pour une application partenaire dans le menu des Services Web hello.

Cette action ne doit pas être exécutée avec le profil de hello qu’ils utilisent pour l’administration T & E normale pour hello suivant raisons.

* Hello client a toobe hello qui clique sur «*Oui*» sur la boîte de dialogue de hello qui s’affiche après l’activation d’une application. Ce clic signifie que les clients hello sont disposé pour hello partenaire application tooaccess leurs données, afin de vous ou hello partenaire cliquez sur ce bouton Oui.

* Si un administrateur de clients ayant activé une application à l’aide de T Bonjour profil d’administrateur E quitte l’entreprise hello (entraînant profil hello cessera), toute application activée à l’aide de ce profil ne fonctionne pas tant que l’application hello est activée avec un autre active WS Admin profil. C’est pourquoi vous êtes supposé toocreate les profils WS Admin distincts.

* Si un administrateur quitte l’entreprise de hello, nom de hello associée toohello profil WS Admin peut être administrateur de remplacement toohello modifiés si vous le souhaitez sans affecter hello activée application car ce profil n’a pas besoin d’être désactivé.

**configuration, de l’utilisateur tooconfigure effectuer hello comme suit :**

1. Ouvrez une session sur tooyour **Concur** client.

2. À partir de hello **Administration** menu, sélectionnez **Services Web**.
   
    ![Client Concur](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Client Concur")

3. Sur hello gauche, à partir de hello **Services Web** volet, sélectionnez **Enable Partner Application**.
   
    ![Enable Partner Application](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "Enable Partner Application")

4. À partir de hello **Enable Application** liste, sélectionnez **Azure Active Directory**, puis cliquez sur **activer**.
   
    ![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")

5. Cliquez sur **Oui** tooclose hello **confirmer l’Action** boîte de dialogue.
   
    ![Confirm Action](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "Confirm Action")

6. Bonjour [portail Azure](https://portal.azure.com), parcourir toohello **Azure Active Directory > applications d’entreprise > toutes les applications** section.

7. Si vous avez déjà configuré Concur pour l’authentification unique, recherchez votre instance de Concur à l’aide du champ de recherche hello. Sinon, sélectionnez **ajouter** et recherchez **Concur** dans la galerie d’applications hello. Sélectionnez Concur à partir des résultats de recherche hello et ajoutez-le tooyour la liste des applications.

8. Sélectionnez votre instance de Concur, puis hello **Provisioning** onglet.

9. Ensemble hello **Mode d’approvisionnement** trop**automatique**. 
 
    ![approvisionnement](./media/active-directory-saas-concur-provisioning-tutorial/provisioning.png)

10. Sous hello **informations d’identification administrateur** section, entrez hello **nom d’utilisateur** et hello **mot de passe** de l’administrateur Concur.

11. Bonjour portail Azure, cliquez sur **tester la connexion** tooensure AD Azure peut se connecter tooyour Concur application. Si hello connexion échoue, assurez-vous que votre compte de Concur dispose d’autorisations d’administrateur d’équipe.

12. Entrez hello adresse de messagerie d’une personne ou un groupe qui doit recevoir des notifications d’erreur approvisionnement hello **courrier électronique de Notification** champ et la case à cocher hello.

13. Cliquez sur **Enregistrer.**

14. Sous la section des mappages de hello, sélectionnez **tooConcur de synchronisation Azure Active Directory Users.**

15. Bonjour **des mappages d’attributs** section, passez en revue les attributs utilisateur hello qui sont synchronisés à partir d’Azure AD tooConcur. Hello attributs sélectionnés en tant que **correspondance** propriétés sont des comptes d’utilisateur hello toomatch utilisés dans Concur pour les opérations de mise à jour. Sélectionnez toocommit de bouton hello enregistrer toutes les modifications.

16. tooenable hello service de configuration d’Azure AD pour Concur, modification hello **état d’approvisionnement** trop**sur** Bonjour **paramètres** section

17. Cliquez sur **Enregistrer.**

Vous pouvez à présent créer un compte de test. Attendez que les minutes too20 tooverify hello compte a été synchronisé tooConcur.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)
* [Configurer l’authentification unique](active-directory-saas-concur-tutorial.md)

