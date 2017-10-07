---
title: "Didacticiel : Intégration d’Azure Active Directory à TINFOIL SECURITY | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory à TINFOIL SECURITY."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: da02da92-e3b0-4c09-ad6c-180882b0f9f8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 1a3fa9880d9e026c2d6d6548188df2269ff69139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tinfoil-security"></a>Didacticiel : Intégration d’Azure Active Directory à TINFOIL SECURITY

Dans ce didacticiel, vous apprendrez comment toointegrate TINFOIL SECURITY avec Azure Active Directory (Azure AD).

Intégration de TINFOIL SECURITY à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooTINFOIL sécurité
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooTINFOIL sécurité (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD à TINFOIL SECURITY, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement TINFOIL SECURITY pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajouter TINFOIL SECURITY à partir de la galerie de hello
2. Configurer et tester l’authentification unique Azure AD

## <a name="add-tinfoil-security-from-hello-gallery"></a>Ajouter TINFOIL SECURITY à partir de la galerie de hello
intégration de hello tooconfigure de TINFOIL SECURITY dans Azure AD, vous devez tooadd TINFOIL SECURITY à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd TINFOIL SECURITY à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **TINFOIL SECURITY**, sélectionnez **TINFOIL SECURITY** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.

    ![TINFOIL SECURITY à partir de la galerie](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec TINFOIL SECURITY, avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello TINFOIL SECURITY est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et l’utilisateur en mode de sécurité TINFOIL hello doit toobe établie.

Dans TINFOIL SECURITY, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec TINFOIL SECURITY, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Créer un utilisateur de test de TINFOIL SECURITY](#create-a-tinfoil-security-test-user)**  -toohave un équivalent de Britta Simon dans TINFOIL SECURITY qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configure-azure-ad-single-sign-on"></a>Configurer l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de TINFOIL SECURITY.

**tooconfigure Azure AD single sign-on avec TINFOIL SECURITY, procédez hello comme suit :**

1. Bonjour portail Azure, sur hello **TINFOIL SECURITY** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Authentification basée sur SAML](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_samlbase.png)

3. Sur hello **URL et le domaine de sécurité TINFOIL** section, hello utilisateur n’est pas tooperform toutes les étapes que l’application hello est déjà pré-intégration à Azure.

    ![Configurer l’authentification unique](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_url.png)


4. Sur hello **le certificat de signature SAML** section, hello de copie **l’empreinte numérique** valeur.

    ![Section Certificat de signature SAML](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_certificate.png) 

5. mappages d’attributs tooadd hello requis, effectuez hello comme suit :
    
    ![Attributs](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "Attributs")
    
    | Nom de l'attribut    |   Valeur de l’attribut |
    | ------------------- | -------------------- |
    | accountid | UXXXXXXXXXXXXX |
    
    a. Cliquez sur **Ajouter un attribut utilisateur**.
    
    ![Ajouter un attribut](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "Attributs")
    
    ![Ajouter un attribut](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "Attributs")
    
    b. Bonjour **nom de l’attribut** zone de texte, type **accountid**.
    
    c. Bonjour **valeur d’attribut** zone de texte, valeur d’ID coller hello compte qui vous obtiendrez ultérieure du didacticiel de hello.
    
    d. Cliquez sur **OK**.    

6. Cliquez sur le bouton **Enregistrer** .

    ![Bouton Enregistrer](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_400.png)

7. Sur hello **Configuration de la sécurité TINFOIL** , cliquez sur **configurer la sécurité TINFOIL** tooopen **configurer l’authentification** fenêtre. Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configuration de TINFOIL SECURITY](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_configure.png) 

8. Dans une autre fenêtre de navigateur web, connectez-vous au site de votre entreprise TINFOIL SECURITY en tant qu’administrateur.

9. Dans la barre d’outils de hello en haut de hello, cliquez sur **mon compte**.
   
    ![Tableau de bord](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "Tableau de bord")

10. Cliquez sur **Security**.
   
    ![Sécurité](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "Sécurité")

11. Sur hello **Single Sign-On** configuration page, effectuer hello comme suit :
   
    ![Authentification unique](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "Authentification unique")
   
    a. Sélectionnez **Enable SAML**.
   
    b. Cliquez sur **Manual Configuration**.
   
    c. Dans **URL de publication SAML** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure
   
    d. Dans **empreinte numérique du certificat SAML** zone de texte, valeur hello coller **l’empreinte numérique** dont vous avez copié à partir de **le certificat de signature SAML** section.
  
    e. Copie **votre ID de compte** valeur et collez la valeur hello dans **valeur d’attribut** zone de texte sous **ajouter un attribut** section dans le portail Azure.
   
    f. Cliquez sur **Enregistrer**.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Utilisateurs et groupes -> Tous les utilisateurs ](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Utilisateur](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="create-a-tinfoil-security-test-user"></a>Créer un utilisateur de test TINFOIL SECURITY

Dans l’ordre tooenable Azure AD les utilisateurs toolog à TINFOIL SECURITY, vous devez les configurer sur TINFOIL SECURITY. Dans les cas de hello de TINFOIL SECURITY, cette configuration est une tâche manuelle.

**tooget un utilisateur, effectuez hello comme suit :**

1. Si l’utilisateur de hello fait partie d’un compte d’entreprise, vous devez trop[contacter l’équipe de support de TINFOIL SECURITY hello](https://www.tinfoilsecurity.com/contact) compte d’utilisateur tooget hello créé.

2. Si l’utilisateur de hello est un utilisateur normal de TINFOIL SECURITY SaaS, utilisateur de hello peut ajouter un tooany collaborateur de sites de l’utilisateur hello. Par courrier électronique un toosend de processus une toohello invitation spécifié cette déclencheurs toocreate un nouveau compte d’utilisateur TINFOIL SECURITY.

> [!NOTE]
> Vous pouvez utiliser n’importe quel autre TINFOIL SECURITY utilisateur compte outil de création ou API fournie par TINFOIL SECURITY tooprovision comptes d’utilisateur Azure AD.
> 
> 

### <a name="assign-hello-azure-ad-test-user"></a>Affecter l’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooTINFOIL sécurité.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooTINFOIL sécurité, effectuer hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **TINFOIL SECURITY**.

    ![Sélectionner TINFOIL SECURITY](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="test-single-sign-on"></a>Tester l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque de TINFOIL SECURITY hello Bonjour volet d’accès, vous devez obtenir l’application de TINFOIL SECURITY tooyour automatiquement signé sur. Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_203.png

