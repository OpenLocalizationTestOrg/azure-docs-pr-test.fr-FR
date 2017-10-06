---
title: "Didacticiel : Intégration d’Azure Active Directory avec Intacct | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Intacct."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 92518e02-a62c-4b1b-a8e9-2803eb2b49ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 3500039615166c2f61fb408d85bb82dfaefba134
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intacct"></a>Didacticiel : Intégration d’Azure Active Directory à Intacct

Dans ce didacticiel, vous apprendrez comment toointegrate Intacct avec Azure Active Directory (Azure AD).

Intégration d’Intacct à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooIntacct
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooIntacct (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD à Intacct, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Intacct pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout d’Intacct à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-intacct-from-hello-gallery"></a>Ajout d’Intacct à partir de la galerie de hello
intégration de hello tooconfigure de Intacct dans Azure AD, vous devez tooadd Intacct à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Intacct à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **Intacct**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_search.png)

5. Dans le volet de résultats hello, sélectionnez **Intacct**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Intacct avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Intacct est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Intacct doit toobe établie.

En l’occurrence, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique à Intacct, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test Intacct](#creating-an-intacct-test-user)**  -toohave un équivalent de Britta Simon dans Intacct est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Intacct.

**tooconfigure Azure AD single sign-on avec Intacct, procédez hello comme suit :**

1. Bonjour portail Azure, sur hello **Intacct** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_samlbase.png)

3. Sur hello **Intacct domaine et les URL** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_url.png)

    Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :
    | |
    |--|
    | `https://<companyname>.intacct.com/ia/acct/sso_response.phtml`|
    | `https://www.intacct.com/ia/acct/sso_response.phtml` |

    > [!NOTE] 
    > Cette valeur n’est pas la valeur réelle. Mettre à jour cette valeur avec l’URL de réponse réelle hello. Contact [équipe de support Intacct](https://us.intacct.com/support) tooget cette valeur.

4. Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-intacct-tutorial/tutorial_general_400.png)

6. Sur hello **Intacct Configuration** , cliquez sur **Intacct de configurer** tooopen **configurer l’authentification** fenêtre. Hello de copie **ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_configure.png) 

7. Dans une fenêtre de navigateur web, connectez-vous dans un site d’entreprise Intacct tooyour en tant qu’administrateur.

8. Cliquez sur hello **société** onglet, puis cliquez sur **Infos société**.

    ![Company](./media/active-directory-saas-intacct-tutorial/ic790037.png "Company")

9. Cliquez sur hello **sécurité** onglet, puis cliquez sur **modifier**.

    ![Sécurité](./media/active-directory-saas-intacct-tutorial/ic790038.png "Sécurité")

10. Bonjour **Single sign on (SSO)** section, effectuer hello comme suit :

    ![Single sign On](./media/active-directory-saas-intacct-tutorial/ic790039.png "Single sign On")

    a. Sélectionnez **Enable Single Sign-On**.

    b. Pour **Identity provider type**, sélectionnez **SAML 2.0**.

    c. Dans **URL de l’émetteur** zone de texte, valeur hello coller **ID d’entité SAML** dont vous avez copié à partir du portail Azure.
   
    d. Dans **URL de connexion** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure.

    e. Ouvrez votre **base 64** certificat dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite toohello **certificat** boîte.
   
    f. Cliquez sur **Enregistrer**.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-an-intacct-test-user"></a>Création d’un utilisateur de test Intacct

tooset des utilisateurs d’Azure AD afin de pouvoir se connecter dans tooIntacct, vous devez les configurer dans Intacct. Pour Intacct, l’approvisionnement est une tâche manuelle.

**comptes d’utilisateur tooprovision, effectuez hello comme suit :**

1. Connectez-vous à tooyour **Intacct** client.

2. Cliquez sur hello **société** onglet, puis cliquez sur **utilisateurs**.

    ![Utilisateurs](./media/active-directory-saas-intacct-tutorial/ic790041.png "Utilisateurs")
3. Cliquez sur hello **ajouter** onglet.

    ![Add](./media/active-directory-saas-intacct-tutorial/ic790042.png "Add")
4. Bonjour **informations utilisateur** section, effectuer hello comme suit :

    ![User Information](./media/active-directory-saas-intacct-tutorial/ic790043.png "User Information")

    a. Entrez hello **ID utilisateur**, hello **nom**, **prénom**, hello **adresse de messagerie**, hello **titre**, et hello **téléphone** d’un compte Azure AD que vous voulez tooprovision dans hello **informations utilisateur** section.

    b. Sélectionnez hello **des privilèges d’administration** d’un compte Azure AD que vous souhaitez tooprovision.
   
    c. Cliquez sur **Enregistrer**. titulaire du compte Azure AD Hello reçoit un message électronique et suit un tooconfirm de lier leur compte avant son activation.

>[!NOTE]
>tooprovision comptes d’utilisateur Azure AD, vous pouvez utiliser des autres outils de création de compte utilisateur Intacct ou les API fournies par Intacct.
        
### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooIntacct.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooIntacct, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Intacct**.

    ![Configurer l’authentification unique](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous testez votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque Intacct hello hello volet d’accès, vous devez être connecté automatiquement dans tooyour Intacct application.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_203.png

