---
title: "Didacticiel : Intégration d’Azure Active Directory à Netsuite | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory à Netsuite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dafa0864-aef2-4f5e-9eac-770504688ef4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 7cf205d5bda5333872fb589e57f4779a8670b595
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netsuite"></a>Didacticiel : Intégration d’Azure Active Directory à Netsuite

Dans ce didacticiel, vous apprendrez comment toointegrate Netsuite avec Azure Active Directory (Azure AD).

Intégration de Netsuite à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooNetsuite
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooNetsuite (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD à Netsuite, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Netsuite pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de Netsuite à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-netsuite-from-hello-gallery"></a>Ajout de Netsuite à partir de la galerie de hello
intégration de hello tooconfigure de Netsuite dans Azure AD, vous devez tooadd Netsuite à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Netsuite à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. Cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue hello.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **Netsuite**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_search.png)

5. Dans le volet de résultats hello, sélectionnez **Netsuite**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Netsuite sur un utilisateur de test nommé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Netsuite est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Netsuite doit toobe établie.

Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Netsuite.

tooconfigure et test Azure AD l’authentification unique avec Netsuite, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test Netsuite](#creating-a-netsuite-test-user)**  -toohave un équivalent de Britta Simon dans Netsuite est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Netsuite.

**tooconfigure Azure AD single sign-on avec Netsuite, procédez hello comme suit :**

1. Bonjour portail Azure, sur hello **Netsuite** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_samlbase.png)

3. Sur hello **Netsuite domaine et les URL** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_url.png)

    Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle : `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs``https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`

    > [!NOTE] 
    > Cette valeur n’est pas la valeur réelle. Valeur de hello de mise à jour avec hello URL de réponse réelle. Contact [équipe de support Netsuite](http://www.netsuite.com/portal/services/support.shtml) tooget cette valeur.
 
4. Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier XML de hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-netsuite-tutorial/tutorial_general_400.png)

6. Sur hello **Netsuite Configuration** , cliquez sur **Netsuite de configurer** tooopen **configurer l’authentification** fenêtre. Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_configure.png) 

7. Ouvrez un nouvel onglet dans votre navigateur et connectez-vous à votre site d’entreprise Netsuite en tant qu’administrateur.

8. Dans la barre d’outils de hello en hello haut hello, cliquez sur **le programme d’installation**, puis cliquez sur **le Gestionnaire d’installation**.

    ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

9. À partir de hello **les tâches d’installation** liste, sélectionnez **intégration**.

    ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-integration.png)

10. Bonjour **gérer l’authentification** , cliquez sur **SAML Single Sign-on**.

    ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-saml.png)

11. Sur hello **le programme d’installation SAML** page, effectuer hello comme suit :
   
    a. Hello de copie **SAML Sign-On URL du Service unique** valeur **aide-mémoire** section de **configurer l’authentification** et collez-le dans hello **fournisseur d’identité Page de connexion** champ Netsuite.

    ![Configurer l’authentification unique](./media/active-directory-saas-netsuite-tutorial/ns-saml-setup.png)
  
    b. Dans Netsuite, sélectionnez **Méthode d’authentification principale**.

    c. Pour le champ hello **métadonnées du fournisseur d’identité SAMLV2**, sélectionnez **télécharger un fichier de métadonnées IDP**. Puis cliquez sur **Parcourir** fichier de métadonnées hello tooupload que vous avez téléchargé à partir du portail Azure.

    ![Configurer l’authentification unique](./media/active-directory-saas-netsuite-tutorial/ns-sso-setup.png)

    d. Cliquez sur **Envoyer**.

12. Dans Azure AD, activez la case à cocher **Afficher et modifier tous les autres attributs utilisateur**, puis ajoutez un attribut.

    ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-attributes.png)

13. Pourquoi **nom de l’attribut** , tapez dans `account`. Pourquoi **valeur d’attribut** , tapez votre ID de compte Netsuite. Cette valeur est constante et la modification à un compte. Obtenir des instructions sur la façon de toofind votre ID de compte sont présentés ci-dessous :

      ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-add-attribute.png)

    a. Dans Netsuite, cliquez sur **le programme d’installation** à partir du menu de navigation supérieur hello.

    b. Puis cliquez sur sous hello **les tâches d’installation** section du menu de navigation gauche hello, sélectionnez hello **intégration** section, puis cliquez sur **préférences de Services Web**.

    c. Copiez votre ID de compte Netsuite et collez-le dans hello **valeur d’attribut** champ dans Azure AD.

    ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-account-id.png)

14. Avant que les utilisateurs peuvent effectuer l’authentification unique dans Netsuite, ils doivent d’abord être affectés les autorisations appropriées de hello dans Netsuite. Suivez les instructions de hello ci-dessous tooassign ces autorisations.

    a. Dans le menu de navigation supérieur hello, cliquez sur **le programme d’installation**, puis cliquez sur **le Gestionnaire d’installation**.
      
      ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    b. Dans le menu de navigation gauche hello, sélectionnez **utilisateurs/rôles**, puis cliquez sur **gérer les rôles**.
      
      ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-manage-roles.png)

    c. Cliquez sur **Nouveau rôle**.

    d. Tapez un **nom** pour votre nouveau rôle, puis sélectionnez hello **unique Sign-On uniquement** case à cocher.
      
      ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-new-role.png)

    e. Cliquez sur **Enregistrer**.

    f. Dans le menu hello haut de hello, cliquez sur **autorisations**. Cliquez sur **Configuration**.
      
       ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-sso.png)

    g. Sélectionnez **Configurer l’authentification unique SAM**, puis cliquez sur **Ajouter**.

    h. Cliquez sur **Enregistrer**.

    i. Dans le menu de navigation supérieur hello, cliquez sur **le programme d’installation**, puis cliquez sur **le Gestionnaire d’installation**.
      
       ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    j. Dans le menu de navigation gauche hello, sélectionnez **utilisateurs/rôles**, puis cliquez sur **gérer les utilisateurs**.
      
       ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-manage-users.png)

    k. Sélectionnez un utilisateur de test. Puis cliquez sur **Modifier**.
      
       ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-edit-user.png)

    l. Dans la boîte de dialogue rôles hello, sélectionnez le rôle de hello que vous avez créé et cliquez sur **ajouter**.
      
       ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-add-role.png)

    m. Cliquez sur **Enregistrer**.
    
> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_01.png) 

2.  liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_02.png) 

3. En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**. 

### <a name="creating-a-netsuite-test-user"></a>Création d’un utilisateur de test Netsuite

Dans cette section, un utilisateur nommé Britta Simon est créé dans Netsuite. Netsuite prend en charge l’approvisionnement juste-à-temps, option activée par défaut.
Vous n’avez aucune opération à effectuer dans cette section. Si un utilisateur n’existe pas déjà dans Netsuite, un nouveau est créé lorsque vous essayez de tooaccess Netsuite.


### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooNetsuite.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooNetsuite, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Netsuite**.

    ![Configurer l’authentification unique](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

tootest votre seule paramètres d’authentification, ouvrez hello volet d’accès au [https://myapps.microsoft.com](https://myapps.microsoft.com/), connectez-vous à un compte de test hello, puis cliquez sur **Netsuite**.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)
* [Configurer l’approvisionnement de l’utilisateur](active-directory-saas-netsuite-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_203.png

