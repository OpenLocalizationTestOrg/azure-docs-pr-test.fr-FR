---
title: "Didacticiel : Intégration d’Azure Active Directory à Marketo | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Marketo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b88c45f5-d288-4717-835c-ca965add8735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 87f88cde4f027f99a83c1ab3b318247bb4d658ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-marketo"></a>Didacticiel : Intégration d’Azure Active Directory à Marketo

Dans ce didacticiel, vous apprendrez comment toointegrate Marketo avec Azure Active Directory (Azure AD).

Intégration de Marketo avec Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooMarketo
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooMarketo (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec Marketo, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Marketo pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de Marketo à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-marketo-from-hello-gallery"></a>Ajout de Marketo à partir de la galerie de hello
intégration de hello tooconfigure de Marketo dans Azure AD, vous devez tooadd Marketo à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Marketo à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **Marketo**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_search.png)

5. Dans le volet de résultats hello, sélectionnez **Marketo**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Marketo grâce à un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Marketo est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Marketo doit toobe établie.

Dans Marketo, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec Marketo, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test de Marketo](#creating-a-marketo-test-user)**  -toohave un équivalent de Britta Simon dans Marketo est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de Marketo.

**tooconfigure Azure AD single sign-on avec Marketo, effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **Marketo** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_samlbase.png)

3. Sur hello **Marketo domaine et les URL** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_url.png)

    a. Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://saml.marketo.com/sp`

    b. Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://login.marketo.com/saml/assertion/\<munchkinid\>`

    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettre à jour ces valeurs hello URL d’identificateur et de réponse réelle. Contact [équipe de support technique de Marketo](http://investors.marketo.com/contactus.cfm) tooget ces valeurs.
 
4. Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_general_400.png)

6. Sur hello **Marketo Configuration** , cliquez sur **configurer de Marketo** tooopen **configurer l’authentification** fenêtre. Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_configure.png) 

7. tooget Munchkin des Id de votre application, connectez-vous en tooMarketo à l’aide des informations d’identification d’administrateur et procédez comme suit :
   
    a. Ouvrez une session dans l’application tooMarketo à l’aide des informations d’identification d’administrateur.
   
    b. Cliquez sur hello **Admin** bouton du volet de navigation supérieure hello.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    c. Parcourir les menus d’intégration toohello, cliquez sur hello **lien de Munchkin**.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_11.png)
   
    d. Copiez hello Id Munchkin indiqué sur l’écran hello et terminer votre URL de réponse dans l’Assistant de configuration hello Azure AD.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_12.png) 

8. tooconfigure hello SSO dans l’application hello, procédez comme hello étapes ci-dessous :
   
    a. Ouvrez une session dans l’application tooMarketo à l’aide des informations d’identification d’administrateur.
   
    b. Cliquez sur hello **Admin** bouton du volet de navigation supérieure hello.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    c. Parcourir les menus d’intégration toohello, cliquez sur **Single Sign On**.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_07.png) 
   
    d. tooenable hello paramètres SAML, cliquez sur **modifier** bouton.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_08.png) 
   
    e. **Activez** les paramètres d’authentification unique.
   
    f. Hello de coller **ID d’entité SAML**, Bonjour **ID de l’émetteur** zone de texte.
   
    g. Bonjour **ID d’entité** zone de texte, entrez l’URL hello `http://saml.marketo.com/sp`.
   
    h. Sélectionnez hello emplacement de l’ID d’utilisateur en tant que **élément identificateur de nom**.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_09.png)
   
    > [!NOTE]
    > Si votre identificateur de l’utilisateur n’est pas valeur UPN puis modifier la valeur dans l’onglet d’attributs hello hello.
   
    i. Téléchargez le certificat hello, qui vous avez téléchargé à partir de l’Assistant de configuration d’Azure AD. **Enregistrer** hello paramètres.
   
    j. Modifier les paramètres des Pages de redirection hello.
   
    k. Hello de coller **SAML Sign-On URL du Service unique** Bonjour **URL de connexion** zone de texte.
   
    l. Hello de coller **URL de déconnexion** Bonjour **URL de déconnexion** zone de texte.
   
    m. Bonjour **URL d’erreur**, copie votre **URL de l’instance Marketo** et cliquez sur **enregistrer** bouton toosave paramètres.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_10.png)

9. tooenable hello SSO pour les utilisateurs, hello complet suivant des actions :
   
    a. Ouvrez une session dans l’application tooMarketo à l’aide des informations d’identification d’administrateur.
   
    b. Cliquez sur hello **Admin** bouton du volet de navigation supérieure hello.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    c. Accédez toohello **sécurité** menu et cliquez sur **les paramètres de connexion**.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_13.png)
   
    d. Vérifiez hello **nécessitent la SSO** option et **enregistrer** hello paramètres.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_14.png)

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-marketo-test-user"></a>Créer un utilisateur de test Marketo

Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Marketo. Suivez ces étapes de toocreate un utilisateur dans la plateforme de Marketo.

1. Ouvrez une session dans l’application tooMarketo à l’aide des informations d’identification d’administrateur.

2. Cliquez sur hello **Admin** bouton du volet de navigation supérieure hello.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 

3. Accédez toohello **sécurité** menu et cliquez sur **les utilisateurs et les rôles**
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_19.png)  

4. Cliquez sur hello **inviter un nouvel utilisateur** lien sur l’onglet utilisateurs de hello
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_15.png) 

5. Bonjour de remplissage hello inviter un nouvel utilisateur Assistant informations suivantes
   
    a. Entrez hello utilisateur **par courrier électronique** adresse dans la zone de texte hello
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_16.png)
   
    b. Entrez hello **prénom** dans la zone de texte hello
   
    c. Entrez hello **nom** dans la zone de texte hello
   
    d. Cliquez sur **Suivant**

6. Bonjour **autorisations** onglet, sélectionnez hello **userRoles** et cliquez sur **suivant**
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_17.png)
7. Cliquez sur hello **envoyer** bouton invitation d’utilisateur toosend hello
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_18.png)

8. Utilisateur reçoit une notification par courrier électronique de hello et a tooclick hello lier et modifier le compte de hello tooactivate hello mot de passe. 

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooMarketo.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooMarketo, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Marketo**.

    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque Marketo hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Marketo application.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_203.png

