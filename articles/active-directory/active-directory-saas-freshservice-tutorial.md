---
title: "Didacticiel : intégration d’Azure Active Directory à Freshservice | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Freshservice."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3dd22b1f-445d-45c6-8eda-30207eb9a1a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: d73624b87d058f66885ae72fda69a0aacc89c1ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshservice"></a>Didacticiel : intégration d’Azure Active Directory à Freshservice

Dans ce didacticiel, vous apprendrez comment toointegrate Freshservice avec Azure Active Directory (Azure AD).

Intégration de Freshservice à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooFreshservice
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooFreshservice (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD à Freshservice, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Freshservice pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de Freshservice à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-freshservice-from-hello-gallery"></a>Ajout de Freshservice à partir de la galerie de hello
intégration de hello tooconfigure de Freshservice dans Azure AD, vous devez tooadd Freshservice à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Freshservice à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **Freshservice**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_search.png)

5. Dans le volet de résultats hello, sélectionnez **Freshservice**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Freshservice, avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Freshservice est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Freshservice doit toobe établie.

En l’occurrence, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique à Freshservice, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test de Freshservice](#creating-a-freshservice-test-user)**  -toohave un équivalent de Britta Simon dans Freshservice est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Freshservice.

**tooconfigure Azure AD single sign-on avec Freshservice, procédez hello comme suit :**

1. Bonjour portail Azure, sur hello **Freshservice** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_samlbase.png)

3. Sur hello **Freshservice domaine et les URL** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_url.png)

    a. Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<democompany>.freshservice.com`

    b. Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<democompany>.freshservice.com`

    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur. Contact [équipe de support Client de Freshservice](https://support.freshservice.com/) tooget ces valeurs. 
 
4. Sur hello **le certificat de signature SAML** section, copiez **l’empreinte numérique** valeur du certificat.

    ![Configurer l’authentification unique](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-freshservice-tutorial/tutorial_general_400.png)

6. Sur hello **Freshservice Configuration** , cliquez sur **configurer de Freshservice** tooopen **configurer l’authentification** fenêtre. Hello de copie **URL de déconnexion et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_configure.png) 

7. Dans une fenêtre de navigateur web, ouvrez une session dans le site d’entreprise Freshservice tooyour en tant qu’administrateur.

8. Dans le menu hello haut de hello, cliquez sur **Admin**.
   
    ![Administrateur](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Administrateur")

9. Bonjour **portail client**, cliquez sur **sécurité**.
   
    ![Sécurité](./media/active-directory-saas-freshservice-tutorial/ic790815.png "Sécurité")

10. Bonjour **sécurité** section, effectuer hello comme suit :
   
    ![Single Sign On](./media/active-directory-saas-freshservice-tutorial/ic790816.png "Single Sign On")
   
    a. Activez **Single Sign On**.

    b. Sélectionnez **SAML SSO**.

    c. Bonjour **URL de connexion SAML** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure.

    d. Bonjour **URL de déconnexion** zone de texte, valeur hello coller **URL de déconnexion** dont vous avez copié à partir du portail Azure.

    e. Dans **Security Certificate Fingerprint** zone de texte, collez hello **l’empreinte numérique** valeur de certificat que vous avez copié à partir du portail Azure.

    f. Cliquez sur **Enregistrer**.
   
> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-freshservice-test-user"></a>Création d’un utilisateur de test Freshservice

tooenable Azure AD les utilisateurs toolog dans tooFreshService, vous devez les configurer dans FreshService. Dans les cas de hello d’occurrence, cette configuration est une tâche manuelle.

**tooprovision un compte d’utilisateur, effectuez hello comme suit :**

1. Connectez-vous à tooyour **FreshService** site d’entreprise en tant qu’administrateur.

2. Dans le menu hello haut de hello, cliquez sur **Admin**.
   
    ![Administrateur](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Administrateur")

3. Bonjour **gestion des utilisateurs** , cliquez sur **demandeurs**.
   
    ![Requesters](./media/active-directory-saas-freshservice-tutorial/ic790818.png "Requesters")

4. Cliquez sur **New Requester**.
   
    ![New Requesters](./media/active-directory-saas-freshservice-tutorial/ic790819.png "New Requesters")

5. Bonjour **nouveau demandeur** section, effectuer hello comme suit :
   
    ![New Requester](./media/active-directory-saas-freshservice-tutorial/ic790820.png "New Requester")   

    a. Entrez hello **prénom** et **messagerie** les attributs d’un compte Azure Active Directory valide que vous voulez tooprovision dans hello relatives des zones de texte.

    b. Cliquez sur **Enregistrer**.
   
    >[!NOTE]
    >titulaire du compte Azure Active Directory Hello Obtient un message électronique contenant un compte de hello tooconfirm lien avant son activation
    >  

>[!NOTE]
>Vous pouvez utiliser n’importe quel autre FreshService utilisateur compte outil de création ou API fournie par FreshService tooprovision des comptes d’utilisateur AAD.
>  

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooFreshservice, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Freshservice**.

    ![Configurer l’authentification unique](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque Freshservice hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Freshservice application.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_203.png

