---
title: "Didacticiel : Intégration d’Azure Active Directory à Salesforce | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et la force de vente."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2d7d420-dc91-41b8-a6b3-59579e043b35
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 1d848518ee30910e051cdc4746c599219f3b5a3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce"></a>Didacticiel : Intégration d’Azure Active Directory à Salesforce

Dans ce didacticiel, vous apprendrez comment toointegrate Salesforce avec Azure Active Directory (Azure AD).

Intégration de Salesforce à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooSalesforce
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSalesforce (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD à Salesforce, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Salesforce pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de Salesforce à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-salesforce-from-hello-gallery"></a>Ajout de Salesforce à partir de la galerie de hello
tooconfigure hello intégration de Salesforce dans Azure AD, vous devez tooadd Salesforce à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd force de vente à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. Cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue hello.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **Salesforce**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_search.png)

5. Dans le volet de résultats hello, sélectionnez **Salesforce**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Salesforce, avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Salesforce est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Salesforce doit toobe établie.

Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Salesforce.

tooconfigure et test Azure AD l’authentification unique auprès de Salesforce, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test Salesforce](#creating-a-salesforce-test-user)**  -toohave un équivalent de Britta Simon dans Salesforce est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Salesforce.

**tooconfigure Azure AD single sign-on avec Salesforce, procédez hello comme suit :**

1. Bonjour portail Azure, sur hello **Salesforce** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_samlbase.png)

3. Sur hello **URL et domaine Salesforce** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_url.png)

    Bonjour **URL de connexion** zone de texte, valeur hello de type hello suivant le modèle à l’aide de : 
   * Compte d’entreprise : `https://<subdomain>.my.salesforce.com`
   * Compte de développeur : `https://<subdomain>-dev-ed.my.salesforce.com`

    > [!NOTE] 
    > Ces valeurs ne sont pas hello réel. Mettre à jour ces valeurs avec une URL de connexion réel hello. Contact [équipe de support technique de force de vente Client](https://help.salesforce.com/support) tooget ces valeurs. 
 
4. Sur hello **le certificat de signature SAML** , cliquez sur **certificat** , puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/tutorial_general_400.png)

6. Sur hello **Salesforce Configuration** , cliquez sur **configurer la force de vente** tooopen **configurer l’authentification** fenêtre. Hello de copie **ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.** 

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS>
7.  Ouvrez un nouvel onglet dans votre navigateur et connectez-vous à tooyour Salesforce compte d’administrateur.

8.  Sous hello **administrateur** volet de navigation, cliquez sur **des contrôles de sécurité** tooexpand hello liés de section. Puis cliquez sur **Paramètres de l’authentification unique**.

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso.png)

9.  Sur hello **paramètres d’authentification unique** , cliquez sur hello **modifier** bouton.
    ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)

      > [!NOTE]
      > Si vous êtes tooenable Impossible de l’authentification unique sur les paramètres de votre compte Salesforce, vous devrez peut-être toocontact [équipe de support technique de force de vente Client](https://help.salesforce.com/support). 

10. Sélectionnez **SAML activé**, puis cliquez sur **Enregistrer**.

      ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/sf-enable-saml.png)
11. tooconfigure votre SAML unique l’authentification sur les paramètres, cliquez sur **nouveau**.

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-new.png)

12. Sur hello **SAML unique Sign-On Setting Edit** , vérifiez hello suivant configurations :

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/sf-saml-config.png)

    a. Pourquoi **nom** , tapez un nom convivial pour cette configuration. En fournissant une valeur pour **nom** remplir automatiquement hello **nom de l’API** zone de texte.

    b. Coller **ID d’entité SMAL** valeur hello **émetteur** champ Salesforce.

    c. Bonjour **zone de texte de l’entité**, tapez votre nom de domaine Salesforce à l’aide de hello suivant le modèle :
      
      * Compte d’entreprise : `https://<subdomain>.my.salesforce.com`
      * Compte de développeur : `https://<subdomain>-dev-ed.my.salesforce.com`
      
    d. Cliquez sur **Parcourir** ou **choisir un fichier** tooopen hello **tooUpload de choisir un fichier** boîte de dialogue, sélectionnez votre certificat Salesforce, puis cliquez sur **ouvrir**certificat de hello tooupload.

    e. Pour **Type d’identité SAML**, sélectionnez **L’assertion contient le nom d’utilisateur de l’utilisateur salesforce.com**.

    f. Pour **emplacement d’identité SAML**, sélectionnez **identité figure dans l’élément NameIdentifier de hello Hello instruction de sujet**

    g. Coller **-Service URL d’authentification** dans hello **Identity Provider Login URL** champ Salesforce.
    
    h. Pour **Liaison de demande initiée par le fournisseur de service**, sélectionnez **Redirection HTTP**.
    
    i. Enfin, cliquez sur **enregistrer** tooapply vos paramètres unique SAML de session.

13. Dans le volet de navigation gauche hello dans Salesforce, cliquez sur **gestion des domaines** tooexpand hello section associée, puis cliquez sur **mon domaine**.

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/sf-my-domain.png)

14. Faites défiler vers le bas toohello **Configuration de l’authentification** et cliquez sur hello **modifier** bouton.

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/sf-edit-auth-config.png)

15. Bonjour **Service d’authentification** section, sélectionnez hello le nom convivial de votre configuration de SAML SSO, puis cliquez sur **enregistrer**.

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/sf-auth-config.png)

    > [!NOTE]
    > Si plus d’un service d’authentification est activée, les utilisateurs sont demandée tooselect le service d’authentification qu’ils aiment toosign avec lors de l’initialisation d’environnement de Salesforce tooyour de l’authentification unique. Si vous ne souhaitez pas qu’il toohappen, vous devez **laisser tous les autres services d’authentification désactivée**.
<CE>    
> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** section, cliquez simplement sur **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Dans le volet de navigation gauche hello Bonjour **portail Azure**, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_02.png) 

3. En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-salesforce-test-user"></a>Création d’un utilisateur de test Salesforce

Dans cette section, un utilisateur appelé Britta Simon est créé dans Salesforce. Salesforce prend en charge l’approvisionnement juste-à-temps, option activée par défaut.
Vous n’avez aucune opération à effectuer dans cette section. Si un utilisateur n’existe pas déjà dans Salesforce, un nouveau est créé lorsque vous essayez de tooaccess Salesforce.

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooSalesforce.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooSalesforce, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Salesforce**.

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

tootest votre seule paramètres d’authentification, ouvrez hello volet d’accès au [https://myapps.microsoft.com](https://myapps.microsoft.com/), puis connectez-vous à un compte de test hello, puis cliquez sur **Salesforce**.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)
* [Configurer l’approvisionnement de l’utilisateur](active-directory-saas-salesforce-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_203.png

