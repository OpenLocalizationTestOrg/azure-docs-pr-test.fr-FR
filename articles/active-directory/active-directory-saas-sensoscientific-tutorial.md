---
title: "Didacticiel : Intégration d’Azure Active Directory avec Système de surveillance de température sans fil SensoScientific | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et le système de surveillance de température SensoScientific sans fil."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee9a924d-ccde-45b0-ab40-877f82f5dfa2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: jeedes
ms.openlocfilehash: 4eabf7fc6457c217fd5c0c2539ab88c8110055e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sensoscientific-wireless-temperature-monitoring-system"></a>Didacticiel : Intégration d’Azure Active Directory avec Système de surveillance de température sans fil SensoScientific

Dans ce didacticiel, vous apprendrez comment toointegrate SensoScientific sans fil température système de surveillance avec Azure Active Directory (Azure AD).

Intégration de système de surveillance de température SensoScientific sans fil auprès d’Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooSensoScientific système de surveillance de température sans fil
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSensoScientific système de surveillance sans fil température (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec le système de surveillance de température SensoScientific sans fil, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Système de surveillance de température sans fil SensoScientific pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de système de surveillance de température SensoScientific sans fil à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-sensoscientific-wireless-temperature-monitoring-system-from-hello-gallery"></a>Ajout de système de surveillance de température SensoScientific sans fil à partir de la galerie de hello
intégration de hello tooconfigure du système de surveillance de température SensoScientific sans fil dans Azure AD, vous devez tooadd système de surveillance de température SensoScientific sans fil à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd SensoScientific sans fil température analyse système à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **système de surveillance de température SensoScientific sans fil**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_search.png)

5. Dans le volet de résultats hello, sélectionnez **système de surveillance de température SensoScientific sans fil**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Système de surveillance de température sans fil SensoScientific avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans le système de surveillance de température SensoScientific sans fil est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans le système de surveillance de température SensoScientific sans fil hello doit toobe établie.

Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans le système de surveillance de température SensoScientific sans fil.

tooconfigure et test Azure AD l’authentification unique avec le système de surveillance de température SensoScientific sans fil, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test du système de surveillance de température SensoScientific sans fil](#creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user)**  -toohave un équivalent de Britta Simon SensoScientific sans fil température analyse système qui est lié à la représentation sous forme de toohello Azure AD de utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de système de surveillance de température SensoScientific sans fil.

**tooconfigure Azure AD l’authentification unique avec SensoScientific sans fil température surveillance système, effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **système de surveillance de température SensoScientific sans fil** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_samlbase.png)

3. Sur hello **URL et le domaine du système d’analyse SensoScientific sans fil température** section, sans tooperform besoin de toutes les étapes en tant qu’application hello est déjà pré-intégration à Azure :

    ![Configurer l’authentification unique](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_url.png)

4. Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_400.png)

6. Sur hello **Configuration du système d’analyse SensoScientific sans fil température** , cliquez sur **configurer SensoScientific sans fil température analyse le système** tooopen  **Configurer l’authentification** fenêtre. Hello de copie **URL de déconnexion, l’ID d’entité SAML** et **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_configure.png) 

7. Ouverture de session tooyour application du système de surveillance de température SensoScientific sans fil en tant qu’administrateur.

8. Dans le menu de navigation hello en haut de hello, cliquez sur **Configuration** et goto **configurer** sous **Single Sign On** tooopen hello Single Sign On Settings.

    ![Configurer l’authentification unique](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_admin.png) 

9. Dans **Single Sign On Settings** formulaire effectuer hello comme suit :
 
    a. Sélectionnez **Nom de l’émetteur** comme Azure AD.
    
    b. Hello de coller **ID d’entité SAML** dont vous avez copié à partir du portail Azure, dans la zone de texte URL de l’émetteur.
    
    c. Hello de coller **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure, dans la zone de texte URL de Service unique Sign-On.

    d. Hello de coller **URL de déconnexion** dont vous avez copié à partir du portail Azure, dans la zone de texte URL de Service de déconnexion unique.

    e. Parcourir les certificats hello que vous avez téléchargé à partir du portail Azure et téléchargez ici.
    
    f. Cliquez sur **Enregistrer**.
  
> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation](https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user"></a>Création d’un utilisateur de test Système de surveillance de température sans fil SensoScientific

tooenable Azure AD les utilisateurs toolog dans tooSensoScientific système de surveillance de température sans fil, vous devez les configurer dans le système de surveillance de température SensoScientific sans fil. Travailler avec [équipe de support technique de système de surveillance de température SensoScientific sans fil](https://www.sensoscientific.com/contact-us/) pour ajouter des utilisateurs de hello de plate-forme de système de surveillance de température SensoScientific sans fil hello. Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique. 

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooSensoScientific système de surveillance de température sans fil.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooSensoScientific système de surveillance de température sans fil, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **système de surveillance de température SensoScientific sans fil**.

    ![Configurer l’authentification unique](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès. Cliquez sur la vignette du système de surveillance de température SensoScientific sans fil hello Bonjour volet d’accès, vous serez application du système de surveillance de température SensoScientific sans fil automatiquement signé sur tooyour. Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](https://msdn.microsoft.com/library/dn308586).

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_203.png

