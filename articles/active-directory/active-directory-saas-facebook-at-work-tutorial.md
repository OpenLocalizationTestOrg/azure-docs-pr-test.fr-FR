---
title: "Didacticiel : Intégration d’Azure Active Directory à Workplace par Facebook | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et l’espace de travail par Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: jeedes
ms.openlocfilehash: fd19b3f178a2aee7dd2f204d6d3cf6df8fe6b444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a>Didacticiel : Intégration d’Azure Active Directory à Workplace by Facebook

Dans ce didacticiel, vous apprendrez comment toointegrate espace de travail par Facebook avec Azure Active Directory (Azure AD).

Intégration d’espace de travail par Facebook à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a tooWorkplace d’accès par Facebook.
- Vous pouvez autoriser les utilisateurs tooautomatically obtenir connecté tooWorkplace par Facebook (SSO) avec leurs comptes Azure AD.
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.

Pour plus d’informations sur l’intégration d’applications SaaS (software as a service) à Azure AD, consultez l’article [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec l’espace de travail par Facebook, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Workplace by Facebook pour lequel l’authentification unique est activée

étapes de hello tootest dans ce didacticiel, suivez ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajoutez l’espace de travail par Facebook à partir de la galerie de hello.
2. Configurez et testez l’authentification unique Azure AD.

## <a name="add-workplace-by-facebook-from-hello-gallery"></a>Ajouter un espace de travail par Facebook à partir de la galerie de hello
intégration de hello tooconfigure du poste de travail par Facebook dans Azure AD, ajouter un espace de travail par Facebook à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

1. Bonjour [portail Azure](https://portal.azure.com)hello du volet gauche, dans Sélectionnez **Azure Active Directory**. 

    ![bouton d’Azure Active Directory Hello][1]

2. Parcourir trop**des applications d’entreprise** > **toutes les applications**.

    ![panneau des applications Enterprise Hello][2]
    
3. tooadd hello nouvelle application, sélectionnez **nouvelle application** haut hello de boîte de dialogue hello.

    ![Nouveau bouton d’application Hello][3]

4. Dans la zone de recherche de hello, tapez **espace de travail par Facebook**, puis sélectionnez **espace de travail par Facebook** à partir des résultats. Puis sélectionnez **ajouter**, application de hello tooadd.

    ![Espace de travail dans la liste des résultats hello par Facebook](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_search.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Workplace by Facebook, avec un utilisateur de test appelé « Britta Simon ».

Pour l’authentification unique toowork, Azure AD doit tooknow quel utilisateur d’équivalent hello dans l’espace de travail par Facebook est tooa utilisateur dans Azure AD. En d’autres termes, une relation entre des liens entre un utilisateur Azure AD et un utilisateur dans l’espace de travail par Facebook hello doit être établie.

Établir cette relation en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans l’espace de travail par Facebook.

### <a name="configure-azure-ad-single-sign-on"></a>Configurer l’authentification unique Azure AD

Dans cette section, vous activez l’authentification unique de Azure AD dans hello portail Azure, et vous configurez l’authentification unique dans votre espace de travail par application Facebook.

1. Bonjour portail Azure, sur hello **espace de travail par Facebook** page d’intégration d’application, sélectionnez **l’authentification unique**.

    ![Configurer le lien d’authentification unique][4]

2. Bonjour **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable SSO.
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. Bonjour **espace de travail par le domaine de Facebook et URL** section, hello suivant :

    a. Bonjour **URL de connexion** zone de texte, tapez une URL qui utilise hello modèle :`https://<company subdomain>.facebook.com`

    b. Bonjour **identificateur** zone de texte, tapez une URL qui utilise hello modèle :`https://www.facebook.com/company/<scim company id>`

    > [!NOTE]
    > Ces valeurs sont données à titre d’exemple uniquement. Mettre à jour ces valeurs avec l’URL de connexion réel hello et identificateur. Contact hello [espace de travail par équipe de support Facebook Client](https://workplace.fb.com/faq/) tooget ces valeurs. 

4. Bonjour **le certificat de signature SAML** section, sélectionnez **certificat (Base64)**, puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. Sélectionnez **Enregistrer**.

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_400.png)

6. Bonjour **espace de travail par la Configuration de Facebook** section, sélectionnez **configurer le poste de travail par Facebook** tooopen hello **configurer l’authentification** fenêtre. Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **aide-mémoire** section.

    ![Configuration de Workplace by Facebook](./media/active-directory-saas-facebook-at-work-tutorial/config.png) 

7. Dans une fenêtre de navigateur web, connectez-vous tooyour espace de travail par site d’entreprise Facebook en tant qu’administrateur.
  
   > [!NOTE] 
   > Dans le cadre du processus d’authentification SAML de hello, espace de travail pouvez utiliser des chaînes de requête de configuration too2.5 kilo-octets dans la taille de la commande toopass paramètres tooAzure AD.

8. Bonjour **tableau de bord entreprise**, accédez toohello **authentification** onglet.

9. Sous **l’authentification SAML**, sélectionnez **SSO uniquement** à partir de la liste déroulante de hello.

10. Entrez les valeurs hello copiés à partir de hello **espace de travail par la Configuration de Facebook** section Hello Azure portal dans les champs correspondants hello :

    *   Dans le **URL SAML** zone de texte, valeur hello coller **-Service URL d’authentification**, qui vous avez copié à partir de hello portail Azure.
    *   Dans le **URL de l’émetteur SAML** zone de texte, valeur hello coller **ID d’entité SAML**, lequel vous avez copié à partir de hello portail Azure.
    *   Dans **redirection de déconnexion SAML (facultatif)**, collez la valeur hello **URL de déconnexion**, lequel vous avez copié à partir de hello portail Azure.
    *   Ouvrez votre **certificat codé en base 64** dans le bloc-notes, téléchargé à partir de hello portail Azure. Copiez le contenu de hello de celui-ci dans le Presse-papiers, puis collez-la toothe **certificat SAML** zone de texte.

11. Vous devrez peut-être audience de hello tooenter URL destinataire URL et des services ACS (Assertion Consumer Service) URL, répertorié sous hello **Configuration SAML** section.

12. Faites défiler bas toohello de section de hello et sélectionnez **Test SSO**. Une fenêtre contextuelle s’affiche, hello Azure AD-page de connexion. tooauthenticate, entrez vos informations d’identification comme d’habitude. Vérifiez l’adresse de messagerie hello retourné à partir d’Azure AD est hello identique hello compte espace de travail que vous êtes connecté.

13. Si le test de hello terminée avec succès, faites défiler bas toohello de page de hello et sélectionnez **enregistrer**.

14. La page de connexion à Azure AD sera désormais présentée à tous les utilisateurs de Workplace pour qu’ils s’authentifient.

Vous pouvez choisir tooconfigure une déconnexion SAML de l’URL, qui peut être toopoint utilisé dans la page de déconnexion hello Azure AD. Lorsque ce paramètre est activé et configuré, hello utilisateur n’est plus redirigée toohello page de déconnexion de poste de travail. Au lieu de cela, utilisateur de hello est redirigé toohello URL qui a été ajoutée dans le paramètre de redirection de déconnexion SAML hello.


> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello. Après l’ajout de cette application à partir de hello **Active Directory** > **des Applications d’entreprise** , sélectionnez simplement les hello **Single Sign-On** onglet et hello d’accès incorporé documentation via hello **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello Bonjour [AD Azure incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985).

### <a name="configure-reauthentication-frequency"></a>Configuration de la fréquence de réauthentification

Vous pouvez configurer tooprompt d’espace de travail pour une vérification SAML chaque jour, trois jours, une semaine, deux semaines, mois, ou jamais.

> [!NOTE] 
>Hello valeur minimale pour la vérification de SAML hello sur des applications mobiles est définie tooone semaine.

Vous pouvez également forcer une réinitialisation SAML pour tous les utilisateurs. toodo, hello utilisation **requièrent l’authentification SAML pour tous les utilisateurs désormais** bouton.


### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

1. Bonjour **portail Azure**hello du volet gauche, dans Sélectionnez **Azure Active Directory**.

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis sélectionnez **tous les utilisateurs**.
    
    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, sélectionnez **ajouter**.
 
    ![bouton Ajouter de Hello](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_03.png) 

4. Bonjour **utilisateur** boîte de dialogue zone, hello suivant :
 
    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, tapez **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** zone de texte, hello de type **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **Afficher le mot de passe** et prenez-en note.

    d. Sélectionnez **Créer**.
 
### <a name="create-a-workplace-by-facebook-test-user"></a>Création d’un utilisateur de test Workplace by Facebook

Dans cette section, un utilisateur appelé Britta Simon est créé dans Workplace by Facebook. Workplace by Facebook prend en charge l’approvisionnement juste-à-temps, qui est activé par défaut.

Vous n’avez aucune opération à effectuer dans cette section. Si un utilisateur n’existe pas dans l’espace de travail par Facebook, un nouveau est créé lors de l’espace de travail de tooaccess par Facebook.

>[!Note]
>Si vous avez besoin de toocreate un utilisateur manuellement, contactez hello [espace de travail par équipe de support Facebook Client](https://workplace.fb.com/faq/).

### <a name="assign-hello-azure-ad-test-user"></a>Affecter l’utilisateur de test hello Azure AD

Dans cette section, vous activez Britta Simon toouse Azure SSO en accordant l’accès des tooWorkplace par Facebook.

![Affecter des utilisateurs][200] 

1. Bonjour Azure afficher les applications de portail, ouvrez hello. Atteindre la vue de répertoire toohello, accédez trop**des applications d’entreprise**, puis sélectionnez **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **espace de travail par Facebook**.

    ![Hello, espace de travail par un lien de Facebook dans la liste des Applications hello](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_app.png) 

3. Dans le menu hello hello gauche, sélectionnez **utilisateurs et groupes**.

    ![lien de « Utilisateurs et groupes » Hello][202] 

4. Sélectionnez **Ajouter**. Ensuite, dans hello **ajouter l’affectation** volet, sélectionnez **utilisateurs et groupes**.

    ![volet d’ajouter l’affectation de Hello][203]

5. Bonjour **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Bonjour **utilisateurs et groupes** boîte de dialogue, sélectionnez **sélectionnez**.

7. Bonjour **ajouter l’affectation** boîte de dialogue, sélectionnez **affecter**.
    
### <a name="test-single-sign-on"></a>Tester l’authentification unique

Si vous souhaitez tootest vos paramètres d’authentification unique, ouvrez hello panneau d’accès.
Pour plus d’informations, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).


## <a name="next-steps"></a>Étapes suivantes

* Consultez hello [liste des didacticiels sur la façon de toointegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md).
* Voir [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).
* En savoir plus sur la façon trop[configuration d’utilisateur](active-directory-saas-facebook-at-work-provisioning-tutorial.md).



<!--Image references-->

[1]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_203.png

