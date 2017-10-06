---
title: "Didacticiel : Intégration d’Azure Active Directory à Halogen Software | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et halogène logiciel."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ca2298d-9a0c-4f14-925c-fa23f2659d28
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: bdb67de713771d6e306f287c4b13895f6336f7ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halogen-software"></a>Didacticiel : Intégration d’Azure Active Directory avec Halogen Software

Dans ce didacticiel, vous apprendrez comment toointegrate logiciel halogène avec Azure Active Directory (Azure AD).

Intégration du logiciel de halogène avec Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooHalogen logiciel
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooHalogen logiciels (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec halogène logiciel, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Halogen Software pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario

Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout d’un logiciel de halogène à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-halogen-software-from-hello-gallery"></a>Ajout d’un logiciel de halogène à partir de la galerie de hello

tooconfigure hello intégration des logiciels de halogène dans Azure AD, vous devez tooadd halogène logiciel à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd logiciel halogène à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **halogène logiciel**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_search.png)

5. Dans le volet de résultats hello, sélectionnez **halogène logiciel**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Halogen Software à l’aide d’un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello halogène logiciel est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans le logiciel de halogène hello doit toobe établie.

Dans le logiciel de HALOGÈNE, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec halogène logiciel, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test halogène logiciel](#creating-a-halogen-software-test-user)**  -toohave un équivalent de Britta Simon à halogène un logiciel qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application halogène.

**tooconfigure Azure AD authentification unique avec le logiciel de HALOGÈNE, effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **halogène logiciel** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_samlbase.png)

3. Sur hello **halogène logiciel domaine et les URL** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_url.png)

    a. Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://global.hgncloud.com/<companyname>`

    b. Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle : `https://global.halogensoftware.com/<companyname>`,`https://global.hgncloud.com/<companyname>`

    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur. Contact [équipe de support Client de logiciel halogène](https://support.halogensoftware.com/) tooget ces valeurs. 
 


4. Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-halogen-software-tutorial/tutorial_general_400.png)

6. Dans une autre fenêtre de navigateur, l’authentification tooyour **halogène logiciel** application en tant qu’administrateur.

7. Cliquez sur hello **Options** onglet. 
   
    ![Qu’est-ce qu’Azure AD Connect ?][12]

8. Dans le volet de navigation gauche hello, cliquez sur **Configuration SAML**. 
   
    ![Qu’est-ce qu’Azure AD Connect ?][13]

9. Sur hello **Configuration SAML** page, effectuer hello comme suit : 

    ![Qu’est-ce qu’Azure AD Connect ?][14]

     a. Dans **Unique Identifier** (Identificateur unique), sélectionnez **NameID**.

     b. Dans **Unique Identifier Maps To** (l’identificateur unique mappe vers), sélectionnez **Username** (Nom d’utilisateur).
  
     c. tooupload votre fichier de métadonnées téléchargé, cliquez sur **Parcourir** tooselect fichier hello, puis **télécharger le fichier**.
 
     d. configuration de hello tootest, cliquez sur **exécuter le Test**. 
    
    >[!NOTE]
    >Vous devez toowait pour le message de type hello »*hello SAML test est terminé. Please close this window* » s’affiche. Ensuite, fermez hello ouvert fenêtre du navigateur. Hello **SAML d’activer** case à cocher est activée uniquement si le test de hello a été effectuée. 
     
     e. Sélectionnez **Enable SAML**.
    
     f. Cliquez sur **Enregistrer les modifications**. 

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD

objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, nom du type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-halogen-software-test-user"></a>Création d’un utilisateur de test Halogen Software

objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon halogène logiciel.

**toocreate un utilisateur appelé Britta Simon halogène logiciel, effectuez hello comme suit :**

1. Ouverture de session tooyour **halogène logiciel** application en tant qu’administrateur.

2. Cliquez sur hello **Centre utilisateur** onglet, puis cliquez sur **Create User**.
   
    ![Qu’est-ce qu’Azure AD Connect ?][300]  

3. Sur hello **nouvel utilisateur** boîte de dialogue de page, effectuer hello comme suit :
   
    ![Qu’est-ce qu’Azure AD Connect ?][301]

    a. Bonjour **prénom** zone de texte, type prénom utilisateur hello comme **Brian**.
    
    b. Bonjour **nom** zone de texte, nom d’utilisateur hello comme type **Simon**. 

    c. Bonjour **nom d’utilisateur** zone de texte, type **Britta Simon**, nom d’utilisateur hello comme hello portail Azure.

    d. Bonjour **mot de passe** zone de texte, tapez un mot de passe pour Brian.
    
    e. Cliquez sur **Enregistrer**.

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooHalogen logiciel.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooHalogen logiciel, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **halogène logiciel**.

    ![Configurer l’authentification unique](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque halogène logiciel hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour halogène programme.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_12.png

[13]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_13.png

[14]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_14.png

[100]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_203.png

[300]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_300.png

[301]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_301.png
