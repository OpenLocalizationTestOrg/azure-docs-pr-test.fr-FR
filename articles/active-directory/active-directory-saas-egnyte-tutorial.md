---
title: "Didacticiel : Intégration d’Azure Active Directory avec Egnyte | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory à Box."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8c2101d4-1779-4b36-8464-5c1ff780da18
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: d86fa28a1e7b23474cb76c08aef8539acadaf24d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-egnyte"></a>Didacticiel : Intégration d’Azure Active Directory à Egnyte

Dans ce didacticiel, vous apprendrez comment toointegrate Egnyte avec Azure Active Directory (Azure AD).

Intégration d’Egnyte à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooEgnyte
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooEgnyte (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD à Egnyte, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Egnyte pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout d’Egnyte à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-egnyte-from-hello-gallery"></a>Ajout d’Egnyte à partir de la galerie de hello
intégration de hello tooconfigure d’Egnyte dans Azure AD, vous devez tooadd Egnyte à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Egnyte à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **Egnyte**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_search.png)

5. Dans le volet de résultats hello, sélectionnez **Egnyte**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Egnyte, avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Egnyte est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Egnyte doit toobe établie.

Dans Egnyte, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec Egnyte, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test Egnyte](#creating-an-egnyte-test-user)**  -toohave un équivalent de Britta Simon dans Egnyte est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Egnyte.

**tooconfigure Azure AD single sign-on avec Egnyte, procédez hello comme suit :**

1. Bonjour portail Azure, sur hello **Egnyte** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_samlbase.png)

3. Sur hello **Egnyte domaine et les URL** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_url.png)

    Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.egnyte.com`

    > [!NOTE] 
    > Cette valeur n’est pas la valeur réelle. Mettre à jour de cette valeur avec hello URL de connexion réel. Contact [équipe de support Client de Egnyte](https://www.egnyte.com/corp/contact_egnyte.html) tooget cette valeur. 
 
4. Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-egnyte-tutorial/tutorial_general_400.png)

6. Sur hello **Egnyte Configuration** , cliquez sur **Egnyte de configurer** tooopen **configurer l’authentification** fenêtre. Hello de copie **ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_configure.png) 

7. Dans une fenêtre de navigateur web, ouvrez une session dans le site d’entreprise Egnyte tooyour en tant qu’administrateur.

8. Cliquez sur **Settings**.
   
   ![Paramètres](./media/active-directory-saas-egnyte-tutorial/ic787819.png "Paramètres")

9. Dans le menu de hello, cliquez sur **paramètres**.

   ![Paramètres](./media/active-directory-saas-egnyte-tutorial/ic787820.png "Paramètres")

10. Cliquez sur hello **Configuration** onglet, puis cliquez sur **sécurité**.

    ![Sécurité](./media/active-directory-saas-egnyte-tutorial/ic787821.png "Sécurité")

11. Bonjour **unique authentification** section, effectuer hello comme suit :

    ![Single Sign On Authentication](./media/active-directory-saas-egnyte-tutorial/ic787822.png "Single Sign On Authentication")   
    
    a. Pour **Single sign-on authentication**, sélectionnez **SAML 2.0**.
   
    b. Pour **Identity provider**, sélectionnez **AzureAD**.
   
    c. Coller **SAML Sign-On URL du Service unique** copiées à partir du portail Azure hello **Identity provider login URL** zone de texte.
   
    d. Coller **ID d’entité SAML** dont vous avez copié à partir du portail Azure en hello **entity ID fournisseur d’identité** zone de texte.
      
    e. Ouvrez votre certificat codé en base 64 dans le bloc-notes téléchargé à partir du portail Azure, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite toohello **certificat de fournisseur d’identité** zone de texte.
   
    f. Pour **Default user mapping**, sélectionnez **Email address**.
   
    g. Pour **Use domain-specific issuer value**, sélectionnez **disabled**.
   
    h. Cliquez sur **Enregistrer**.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-an-egnyte-test-user"></a>Création d’un utilisateur de test Egnyte

tooenable Azure AD les utilisateurs toolog dans tooEgnyte, vous devez les configurer dans Egnyte. Dans le cas de hello d’Egnyte, cette configuration est une tâche manuelle.

**effectuer des comptes d’utilisateur, tooprovision hello comme suit :**

1. Connectez-vous à tooyour **Egnyte** site d’entreprise en tant qu’administrateur.

2. Accédez trop**paramètres \> utilisateurs et groupes**.

3. Cliquez sur **ajouter un nouvel utilisateur**, puis sélectionnez hello type d’utilisateur vous souhaitez tooadd.
   
   ![Utilisateurs](./media/active-directory-saas-egnyte-tutorial/ic787824.png "Utilisateurs")

4. Bonjour **nouvel utilisateur Standard** section, effectuer hello comme suit :
   
   ![New Standard User](./media/active-directory-saas-egnyte-tutorial/ic787825.png "New Standard User")   

   a. Hello de type **messagerie**, **nom d’utilisateur**et d’autres détails d’un compte Azure Active Directory valide que vous souhaitez tooprovision.
   
   b. Cliquez sur **Enregistrer**.
    
    >[!NOTE]
    >titulaire du compte Azure Active Directory Hello recevra un e-mail de notification.
    >

>[!NOTE]
>Vous pouvez utiliser n’importe quel autre Egnyte utilisateur compte outil de création ou API fournie par Egnyte tooprovision des comptes d’utilisateur AAD.
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooEgnyte.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooEgnyte, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Egnyte**.

    ![Configurer l’authentification unique](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque Egnyte hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Egnyte application.
Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_203.png

