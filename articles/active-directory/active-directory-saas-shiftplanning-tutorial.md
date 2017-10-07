---
title: "Didacticiel : intégration d’Azure Active Directory à Humanity | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et l’humanité."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6aa771e9-31c6-48d1-8dde-024bebc06943
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 7d8a04a2eb3c997f86f1e199c47809fa3dad60e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-humanity"></a>Didacticiel : intégration d’Azure Active Directory à Humanity

Dans ce didacticiel, vous apprendrez comment toointegrate humanité avec Azure Active Directory (Azure AD).

Intégration humanité à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooHumanity
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooHumanity (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec l’humanité, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Humanity pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de l’humanité à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-humanity-from-hello-gallery"></a>Ajout de l’humanité à partir de la galerie de hello
intégration de hello tooconfigure de l’humanité dans Azure AD, vous devez tooadd humanité à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd humanité à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **humanité**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_search.png)

5. Dans le volet de résultats hello, sélectionnez **humanité**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Humanity, grâce à un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello humanité est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans l’humanité hello doit toobe établie.

Dans l’humanité, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec l’humanité, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test humanité](#creating-a-humanity-test-user)**  -toohave un équivalent de Britta Simon dans humanité est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application l’humanité.

**tooconfigure Azure AD single sign-on avec humanité, effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **humanité** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_samlbase.png)

3. Sur hello **URL et le domaine de l’humanité** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_url.png)

    a. Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://company.humanity.com/includes/saml/`

    b. Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://company.humanity.com/app/`

    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur. Contact [équipe de support Client de l’humanité](https://www.humanity.com/support/) tooget ces valeurs. 
 
4. Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_400.png)

6. Sur hello **humanité Configuration** , cliquez sur **configurer l’humanité** tooopen **configurer l’authentification** fenêtre. Hello de copie **SAML Sign-On URL du Service unique et l’URL de déconnexion** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_configure.png) 

7. Dans une fenêtre de navigateur web, connectez-vous tooyour **humanité** site d’entreprise en tant qu’administrateur.

8. Dans le menu hello haut de hello, cliquez sur **Admin**.
   
    ![Administrateur](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Administrateur")

9. Sous **Integration**, cliquez sur **Single Sign-On**.
   
    ![Authentification unique](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "Authentification unique")

10. Bonjour **Single Sign-On** section, effectuer hello comme suit :
   
    ![Authentification unique](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "Authentification unique")
   
    a. Sélectionnez **SAML Enabled**.

    b. Sélectionnez **Allow Password Login**.

    c. Hello de coller **SAML Sign-On URL du Service unique** valeur hello **URL de l’émetteur SAML** zone de texte.

    d. Hello de coller **URL de déconnexion** valeur hello **URL de déconnexion distante** zone de texte.
   
    e. Ouvrez votre certificat codé en base 64 dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite toohello **certificat X.509** zone de texte.

11. Cliquez sur **Save Settings**.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-humanity-test-user"></a>Créer un utilisateur de test Humanity

Dans l’ordre tooenable Azure AD les utilisateurs toolog dans tooHumanity, vous devez les configurer dans l’humanité. Dans les cas de hello de l’humanité, cette configuration est une tâche manuelle.

**tooprovision un compte d’utilisateur, effectuez hello comme suit :**

1. Connectez-vous à tooyour **humanité** site d’entreprise en tant qu’administrateur.

2. Cliquez sur **Admin**.
   
    ![Administrateur](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Administrateur")

3. Cliquez sur **Staff**.
   
    ![Staff](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "Staff")

4. Sous **Actions**, cliquez sur **Ajouter des employés**.
   
    ![Add Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "Add Employees")

5. Bonjour **ajouter des employés** section, effectuer hello comme suit :
   
    ![Save Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "Save Employees")
   
    a. Hello de type **prénom**, **nom**, et **messagerie** d’un compte AAD valide que vous voulez tooprovision dans hello relatives des zones de texte.

    b. Cliquez sur **Save Employees**.

>[!NOTE]
>Vous pouvez utiliser n’importe quel autre humanité utilisateur compte outil de création ou API fournie par l’humanité tooprovision des comptes d’utilisateur AAD.

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooHumanity.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooHumanity, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **humanité**.

    ![Configurer l’authentification unique](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque humanité hello hello volet d’accès, vous devez obtenir l’application de l’humanité tooyour automatiquement signé sur.
Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_203.png

