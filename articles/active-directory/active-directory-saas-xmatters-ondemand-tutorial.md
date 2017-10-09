---
title: "Didacticiel : Intégration d’Azure Active Directory à XMatters OnDemand | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de xMatters OnDemand."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ca0633db-4f95-432e-b3db-0168193b5ce9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 7cc8f9f0d8cefc8a60b9514027437ced50c66242
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-xmatters-ondemand"></a>Didacticiel : Intégration d’Azure Active Directory à xMatters OnDemand

Dans ce didacticiel, vous apprendrez comment toointegrate xMatters OnDemand avec Azure Active Directory (Azure AD).

Intégration de xMatters OnDemand à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a tooxMatters d’accès à la demande
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooxMatters OnDemand (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD à xMatters OnDemand, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement xMatters OnDemand pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de xMatters OnDemand à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-xmatters-ondemand-from-hello-gallery"></a>Ajout de xMatters OnDemand à partir de la galerie de hello
intégration de hello tooconfigure de xMatters OnDemand dans Azure AD, vous devez tooadd xMatters OnDemand à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd xMatters OnDemand à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **xMatters OnDemand**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_search.png)

5. Dans le volet de résultats hello, sélectionnez **xMatters OnDemand**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec xMatters OnDemand avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel hello utilisateur équivalent dans xMatters OnDemand est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans xMatters OnDemand doit toobe établie.

Dans xMatters OnDemand, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique à xMatters OnDemand, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test de xMatters OnDemand](#creating-a-xmatters-ondemand-test-user)**  -toohave un homologue de Britta Simon dans xMatters OnDemand est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre xMatters OnDemand application.

**tooconfigure Azure AD single sign-on avec xMatters OnDemand, procédez hello comme suit :**

1. Bonjour portail Azure, sur hello **xMatters OnDemand** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_samlbase.png)

3. Sur hello **xMatters OnDemand domaine et les URL** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_url.png)
    
    a. Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :   
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au/`|
    | `https://<companyname>.cs1.xmatters.com/`|
    | `https://<companyname>.xmatters.com/`|
    | `https://www.xmatters.com`|
    | `https://<companyname>.xmatters.com.au/`|

    b. Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au`|
    | `https://<companyname>.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.cs1.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.au1.xmatters.com.au/<instancename>`|

    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettre à jour ces valeurs hello URL d’identificateur et de réponse réelle. Contact [équipe de support technique xMatters OnDemand](https://www.xmatters.com/company/contact-us/) tooget ces valeurs.

4. Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier certificat hello localement en tant que **c:\\XMatters OnDemand.cer**.

    ![Configurer l’authentification unique](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_certificate.png)
    
    > [!IMPORTANT]
    > Vous devez tooforward hello certificat toohello [équipe de support technique xMatters OnDemand](https://www.xmatters.com/company/contact-us/). certificat de Hello doit toobe téléchargé par l’équipe de support technique xMatters hello que vous puissiez finaliser la configuration de l’authentification unique de l’hello. 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_400.png)

6. Sur hello **xMatters OnDemand Configuration** , cliquez sur **configurer xMatters OnDemand** tooopen **configurer l’authentification** fenêtre. Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_configure.png) 

7. Dans une fenêtre de navigateur web, connectez-vous tooyour site de société XMatters OnDemand en tant qu’administrateur.

8. Dans la barre d’outils de hello en haut de hello, cliquez sur **Admin**, puis cliquez sur **détails de la société** dans la barre de navigation hello hello côté gauche.
   
    ![Administrateur](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "Administrateur")

9. Sur hello **Configuration SAML** page, effectuer hello comme suit :
   
    ![Configuration SAML](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "Configuration SAML")
   
    a. Sélectionnez **Enable SAML**.
   
    b. Coller **ID d’entité SAML**, lequel vous avez copié à partir de hello portail Azure en hello **ID fournisseur d’identité** zone de texte.
   
    c. Coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir de hello portail Azure en hello **URL d’authentification unique** zone de texte.
   
    d. Coller **URL de déconnexion**, lequel vous avez copié à partir de hello portail Azure en hello **URL de déconnexion unique** zone de texte.
   
    e. Dans la page de détails de la société hello, en haut hello, cliquez sur **enregistrer les modifications**.
    
    ![Détails sur la société](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "Détails sur la société")

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-xmatters-ondemand-test-user"></a>Création d’un utilisateur de test xMatters OnDemand

Dans l’ordre tooenable Azure AD les utilisateurs toolog dans tooXMatters à la demande, vous devez les configurer dans XMatters OnDemand. Dans les cas de hello de XMatters OnDemand, cette configuration est une tâche manuelle.

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a>effectuer des comptes d’utilisateur, tooprovision hello comme suit :
1. Connectez-vous à tooyour **XMatters OnDemand** client.

2.  Cliquez sur **utilisateurs** onglet, puis cliquez sur **ajouter un utilisateur**.
  
    ![Utilisateurs](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "Utilisateurs")

3. Bonjour **ajouter un utilisateur** section, effectuer hello comme suit :
   
    ![Ajouter un utilisateur](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "Ajouter un utilisateur")

    a. Sélectionnez **Active**.

    b. Bonjour **ID utilisateur** zone de texte, id d’utilisateur comme type hello Brittasimon@contoso.com.
   
    c. Bonjour **prénom** prénom type d’utilisateur hello comme Brian zone de texte.

    d. Bonjour **nom** zone de texte, tapez nom de famille de l’utilisateur hello comme Simon.
    
    e. Bonjour **Site** zone de texte, site valide de hello entrée d’un Azure valide compte AD tooprovision.
    
    f. Cliquez sur **Enregistrer**.

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooxMatters à la demande.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooxMatters OnDemand, procédez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **xMatters OnDemand**.

    ![Configurer l’authentification unique](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur hello xMatters OnDemand mosaïque hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour xMatters OnDemand application.
Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_203.png

