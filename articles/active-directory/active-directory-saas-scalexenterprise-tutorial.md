---
title: "Didacticiel : Intégration d’Azure Active Directory avec ScaleX Enterprise | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et ScaleX Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2379a8d-a659-45f1-87db-9ba156d83183
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: e398b98d9e0957b5f92c82359651c345d22c3a54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scalex-enterprise"></a>Didacticiel : Intégration d’Azure Active Directory avec ScaleX Enterprise

Dans ce didacticiel, vous apprendrez comment toointegrate ScaleX Enterprise avec Azure Active Directory (Azure AD).

Intégration ScaleX Enterprise à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooScaleX Enterprise
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooScaleX entreprise (SSO) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez. Qu’est-ce que l’accès aux applications et l’authentification unique avec [Azure Active Directory](active-directory-appssoaccess-whatis.md) ?

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec ScaleX Enterprise, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement ScaleX Enterprise pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de ScaleX entreprise à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-scalex-enterprise-from-hello-gallery"></a>Ajout de ScaleX entreprise à partir de la galerie de hello
intégration de hello tooconfigure de ScaleX Enterprise dans tooAzure AD, vous devez tooadd ScaleX entreprise à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd ScaleX Enterprise à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. Cliquez sur **ajouter** bouton en haut de hello de boîte de dialogue hello.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **ScaleX Enterprise**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_search.png)

5. Dans le volet de résultats hello, sélectionnez **ScaleX Enterprise**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec ScaleX Enterprise avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello ScaleX Enterprise est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans ScaleX Enterprise doit toobe établie.

Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans ScaleX Enterprise.

tooconfigure et test Azure AD l’authentification unique avec ScaleX Enterprise, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test ScaleX Enterprise](#creating-a-scalex-enterprise-test-user)**  -toohave un équivalent de Britta Simon dans ScaleX Enterprise qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application d’entreprise de ScaleX.

**tooconfigure Azure AD single sign-on avec ScaleX Enterprise, procédez hello comme suit :**

1. Bonjour portail Azure, sur hello **ScaleX Enterprise** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, en tant que **Mode** sélectionnez **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_samlbase.png)

3. Sur hello **URL et le domaine d’entreprise ScaleX** section, effectuer hello comme suit si vous le souhaitez application hello tooconfigure **IDP** en mode initié par :

    ![Configurer l’authentification unique](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url1.png)

    a. Bonjour **identificateur** zone de texte, valeur hello de type hello suivant le modèle à l’aide de :`https://platform.rescale.com/saml2/<company id>/`

    b. Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://platform.rescale.com/saml2/<company id>/acs/`

4. Vérifiez **afficher les paramètres d’URL avancés**, si vous le souhaitez application hello tooconfigure **SP** en mode initié par :

    ![Configurer l’authentification unique](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url2.png)

    Bonjour **URL de connexion** zone de texte, valeur hello de type hello suivant le modèle à l’aide de :`https://platform.rescale.com/saml2/<company id>/sso/`
     
    > [!NOTE] 
    > Ils ne sont pas des valeurs réelles hello. Mettre à jour ces valeurs hello identificateur réelle, les URL de réponse ou les URL de connexion. Contact [équipe de support Client d’entreprise ScaleX](http://info.rescale.com/contact_sales) tooget ces valeurs. 

5. Votre application ScaleX attend les assertions SAML hello dans un format spécifique, ce qui nécessite vous toomodify attribut personnalisé tooyour SAML attributs du jeton configuration des mappages. Cliquez sur **afficher et modifier tous les autres attributs utilisateur** hello de tooopen de case à cocher personnalisé les paramètres d’attributs.

    ![Configurer l’authentification unique](./media/active-directory-saas-scalexenterprise-tutorial/scalex_attributes.png)
    
    a. Cliquez avec le bouton droit sur les attributs hello **nom** et cliquez sur Supprimer.

    ![Configurer l’authentification unique](./media/active-directory-saas-scalexenterprise-tutorial/delete_attribute_name.png)

    b. Cliquez sur **emailaddress** fenêtre de modifier l’attribut attribut tooopen hello. Modifier sa valeur à partir de **user.mail** trop**user.userprincipalname** et cliquez sur Ok.

    ![Configurer l’authentification unique](./media/active-directory-saas-scalexenterprise-tutorial/edit_email_attribute.png)   
    
5. Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_certificate.png) 

6. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_400.png)
    
7. Sur hello **ScaleX Enterprise Configuration** , cliquez sur **configurer un ScaleX Enterprise** tooopen **configurer l’authentification** fenêtre. Hello de copie **ID d’entité SAML** et **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_configure.png) 

8. tooconfigure l’authentification unique sur **ScaleX Enterprise** côté, connexion toohello ScaleX Enterprise site Web d’entreprise en tant qu’administrateur.

9. Cliquez sur menu hello Bonjour supérieur droit et sélectionnez **Contoso Administration**.

    > [!NOTE] 
    > Contoso est simplement un exemple. Ce doit être le nom réel de votre société. 

    ![Configurer l’authentification unique](./media/active-directory-saas-scalexenterprise-tutorial/Test_Admin.png) 

10. Sélectionnez **intégrations** de menu du haut hello et sélectionnez **Single Sign-On**.

    ![Configurer l’authentification unique](./media/active-directory-saas-scalexenterprise-tutorial/admin_sso.png) 

11. Remplissez le formulaire de hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-scalexenterprise-tutorial/scalex_admin_save.png) 
    
    a. Sélectionnez **Créer n’importe quel utilisateur pouvant s’authentifier avec l’authentification unique.**

    b. **Fournisseur de service saml**: coller hello valeur ***urn : oasis : noms : tc : SAML:2.0:nameid-format : persistant***

    c. **Nom du champ de courrier électronique de fournisseur d’identité dans la réponse d’ACS**: collez la valeur de hello`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`

    d. **ID d’entité de EntityDescriptor :** hello de coller **ID d’entité SAML** valeur copiée à partir de hello portail Azure.

    e. **URL SingleSignOnService fournisseur d’identité :** hello de coller **SAML Sign-On URL du Service unique** de hello portail Azure.

    f. **Certificat d’identité du fournisseur public X509 :** certificat de hello ouvrir X509 téléchargé à partir de la hello Azure dans le bloc-notes et collez contenu hello dans cette zone. Assurez-vous que pas de saut de ligne dans hello du milieu du contenu du certificat hello.
    
    g. Vérifiez hello suivant des cases à cocher : **activé, NameID de chiffrer et AuthnRequests de connexion.**

    h. Cliquez sur **paramètres d’authentification unique de mise à jour** toosave les paramètres hello.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_01.png) 

2. Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_02.png) 

3. En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-scalex-enterprise-test-user"></a>Création d’un utilisateur de test ScaleX Enterprise

tooenable Azure AD les utilisateurs toolog dans tooScaleX Enterprise, vous devez les configurer dans tooScaleX Enterprise. Dans les cas de hello de ScaleX Enterprise, cette configuration est une tâche automatique et aucune étape manuelle est nécessaire. Tout utilisateur qui peut s’authentifier correctement avec les informations d’identification SSO est automatiquement configuré sur hello ScaleX côté.

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’utilisateur accès tooScaleX Enterprise.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooScaleX Enterprise, procédez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **ScaleX Enterprise**.

    ![Configurer l’authentification unique](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.

### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Cliquez sur hello ScaleX Enterprise vignette Bonjour volet d’accès, vous obtenez automatiquement signé sur tooyour application ScaleX entreprise. Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](https://msdn.microsoft.com/library/dn308586).


## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_203.png

