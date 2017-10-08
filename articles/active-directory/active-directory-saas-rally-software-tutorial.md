---
title: "Didacticiel : Intégration d’Azure Active Directory à Rally Software | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Rally Software."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba25fade-e152-42dd-8377-a30bbc48c3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: jeedes
ms.openlocfilehash: c75c8b98ce7fab19964c13de5ad7e19ef3ebd0e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rally-software"></a>Didacticiel : Intégration d’Azure Active Directory à Rally Software

Dans ce didacticiel, vous apprendrez comment toointegrate Rally de logiciel avec Azure Active Directory (Azure AD).

Intégration Rally Software à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooRally logiciel.
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooRally logiciels (Single Sign-On) avec leurs comptes Azure AD.
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD à Rally Software, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Rally Software pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de Rally Software à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-rally-software-from-hello-gallery"></a>Ajout de Rally Software à partir de la galerie de hello
tooconfigure hello intégration de Rally Software dans Azure AD, vous devez tooadd Rally Software à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Rally le logiciel à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![bouton d’Azure Active Directory Hello][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![panneau des applications Enterprise Hello][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Nouveau bouton d’application Hello][3]

4. Dans la zone de recherche de hello, tapez **Rally Software**, sélectionnez **Rally Software** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.

    ![Rally Software dans la liste des résultats hello](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD

Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Rally Software à l’aide d’un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Rally Software est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Rally Software doit toobe établie.

Dans Rally Software, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec Rally Software, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Créer un utilisateur de test Rally Software](#create-a-rally-software-test-user)**  -toohave un équivalent de Britta Simon dans Rally Software qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configure-azure-ad-single-sign-on"></a>Configurer l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Rally Software.

**tooconfigure Azure AD single sign-on avec Rally Software, procédez hello comme suit :**

1. Bonjour portail Azure, sur hello **Rally Software** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Lien Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_samlbase.png)

3. Sur hello **URL et le domaine de logiciel Rally** section, effectuer hello comme suit :

    ![Informations d’authentification unique dans Domaine et URL Rally Software](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_url.png)

    a. Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<tenant-name>.rally.com`

    b. Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<tenant-name>.rally.com`

    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur. Contact [équipe de support Client de logiciel Rally](https://help.rallydev.com/) tooget ces valeurs. 
 


4. Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-rally-software-tutorial/tutorial_general_400.png)

6. Sur hello **Rally la Configuration logicielle** , cliquez sur **configurer Rally Software** tooopen **configurer l’authentification** fenêtre. Hello de copie **URL de déconnexion et l’ID d’entité SAML** de hello **section de référence rapide.**

    ![Configuration de Rally Software](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_configure.png) 

7. Connectez-vous à tooyour **Rally Software** client.

8. Dans la barre d’outils de hello en haut de hello, cliquez sur **le programme d’installation**, puis sélectionnez **abonnement**.
   
    ![Subscription](./media/active-directory-saas-rally-software-tutorial/ic769531.png "Subscription")

9. Cliquez sur hello **Action** bouton. Sélectionnez **modifier un abonnement** à hello haut à droite de la barre d’outils hello.

10. Sur hello **abonnement** page de boîte de dialogue, effectuer hello comme suit, puis cliquez sur **Enregistrer & fermer**:
   
    ![Authentication](./media/active-directory-saas-rally-software-tutorial/ic769542.png "Authentication")
   
    a. Sélectionnez **Rally or SSO authentication** dans la liste déroulante Authentication.

    b. Bonjour **URL du fournisseur d’identité** zone de texte, valeur hello coller **ID d’entité SAML**, lequel vous avez copié à partir du portail Azure. 

    c. Bonjour **déconnexion de SSO** zone de texte, valeur hello coller **URL de déconnexion**, lequel vous avez copié à partir du portail Azure.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD

objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

   ![Créer un utilisateur de test Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-rally-software-tutorial/create_aaduser_01.png)

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-rally-software-tutorial/create_aaduser_02.png)

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.

    ![bouton Ajouter de Hello](./media/active-directory-saas-rally-software-tutorial/create_aaduser_03.png)

4. Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-rally-software-tutorial/create_aaduser_04.png)

    a. Bonjour **nom** , tapez **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.

    c. Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.

    d. Cliquez sur **Créer**.
 
### <a name="create-a-rally-software-test-user"></a>Créer un utilisateur de test Rally Software

Pour Azure AD les utilisateurs toobe en mesure de toosign dans, ils doivent être mis en service toohello application Rally Software à l’aide de leur nom d’utilisateur Azure Active Directory.

**configuration, de l’utilisateur tooconfigure effectuer hello comme suit :**

1. Ouvrez une session dans tooyour client Rally Software.

2. Accédez trop**le programme d’installation \> utilisateurs**, puis cliquez sur **+ ajouter un nouveau**.
   
    ![Utilisateurs](./media/active-directory-saas-rally-software-tutorial/ic781039.png "Utilisateurs")

3. Nom de hello dans la zone de texte hello nouvel utilisateur, puis tapez **ajouter avec des détails**.

4. Bonjour **Create User** section, effectuer hello comme suit :
   
    ![Create User](./media/active-directory-saas-rally-software-tutorial/ic781040.png "Create User")

    a. Bonjour **nom d’utilisateur** zone de texte, nom d’utilisateur comme hello du type **Brittsimon**.
   
    b. Dans **adresse de messagerie** zone de texte, entrez hello adresse de messagerie de l’utilisateur comme  **brittasimon@contoso.com** .

    c. Dans **prénom** texte, entrez le nom d’utilisateur comme hello **Brian**.

    d. Dans **nom** texte, entrez le nom d’utilisateur comme hello **Simon**.

    e. Cliquez sur **Enregistrer et fermer**.

   >[!NOTE]
   >Vous pouvez utiliser n’importe quel autre Rally Software utilisateur compte outil de création ou API fournie par Rally Software tooprovision comptes d’utilisateur Azure AD.

### <a name="assign-hello-azure-ad-test-user"></a>Affecter l’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooRally logiciel.

![Attribuer le rôle d’utilisateur hello][200] 

**tooassign Britta Simon tooRally logiciel, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Rally Software**.

    ![lien de Rally Software Hello dans la liste des Applications hello](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_app.png)  

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![lien de « Utilisateurs et groupes » Hello][202]

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![volet d’ajouter l’affectation de Hello][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="test-single-sign-on"></a>Tester l’authentification unique

objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque Rally Software hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour application Rally Software.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_203.png

