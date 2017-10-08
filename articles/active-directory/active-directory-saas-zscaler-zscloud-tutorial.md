---
title: "Didacticiel : Intégration d’Azure Active Directory avec Zscaler ZSCloud | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Zscaler ZSCloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 411d5684-a780-410a-9383-59f92cf569b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: af6d5c1994e715cccf959cc9fd3ba998e5b9effa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-zscloud"></a>Didacticiel : Intégration d’Azure Active Directory avec Zscaler ZSCloud

Dans ce didacticiel, vous apprendrez comment toointegrate Zscaler ZSCloud avec Azure Active Directory (Azure AD).

Intégration de Zscaler ZSCloud à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooZscaler ZSCloud
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooZscaler ZSCloud (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD à Zscaler ZSCloud, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Zscaler ZSCloud pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de Zscaler ZSCloud à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-zscaler-zscloud-from-hello-gallery"></a>Ajout de Zscaler ZSCloud à partir de la galerie de hello
intégration de hello tooconfigure de Zscaler ZSCloud dans Azure AD, vous devez tooadd Zscaler ZSCloud à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Zscaler ZSCloud à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **Zscaler ZSCloud**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_search.png)

5. Dans le volet de résultats hello, sélectionnez **Zscaler ZSCloud**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Zscaler ZSCloud grâce à un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Zscaler ZSCloud est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Zscaler ZSCloud doit toobe établie.

Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Zscaler ZSCloud.

tooconfigure et test Azure AD l’authentification unique avec Zscaler ZSCloud, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Configuration des paramètres proxy](#configuring-proxy-settings)**  -paramètres de proxy tooconfigure hello dans Internet Explorer
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test de Zscaler ZSCloud](#creating-a-zscaler-zscloud-test-user)**  -toohave un équivalent de Britta Simon dans Zscaler ZSCloud qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Zscaler ZSCloud.

**tooconfigure Azure AD single sign-on avec Zscaler ZSCloud, procédez hello comme suit :**

1. Bonjour portail Azure, sur hello **Zscaler ZSCloud** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_samlbase.png)

3. Sur hello **Zscaler ZSCloud domaine et les URL** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_url.png)

     Bonjour **URL de connexion** zone de texte, tapez l’URL hello utilisée par vos utilisateurs sur toosign tooyour application ZScaler ZSCloud.
    
    > [!NOTE] 
    > Vous avez tooupdate cette valeur avec hello URL de connexion réel. Contact [équipe de support technique Zscaler ZSCloud Client](https://support.zscaler.com/hc/articles/210172606-Zscaler-is-Expanding-Its-Zscloud-Global-Footprint) tooget cette valeur. 
 
4. Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_400.png)

6. Sur hello **Zscaler ZSCloud Configuration** , cliquez sur **configurer Zscaler ZSCloud** tooopen **configurer l’authentification** fenêtre. Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_configure.png) 

7. Dans une fenêtre de navigateur web, connectez-vous tooyour site de société ZScaler ZSCloud en tant qu’administrateur.

8. Dans le menu hello haut de hello, cliquez sur **Administration**.
   
    ![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800206.png "Administration")

9. Sous **Manage Administrators & Roles**, cliquez sur **Manage Users & Authentication**.   
            
    ![Gérer les utilisateurs et l’authentification](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800207.png "Gérer les utilisateurs et l’authentification")

10. Bonjour **choisir les Options d’authentification pour votre organisation** section, effectuer hello comme suit :   
                
    ![Authentication](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800208.png "Authentication")
   
    a. Sélectionnez **Authenticate using SAML Single Sign-On**.

    b. Cliquez sur **Configure SAML Single Sign-On Parameters**.

11. Sur hello **Configure SAML Single Sign-On Parameters** page de boîte de dialogue, effectuer hello comme suit, puis cliquez sur **terminé**

    ![Authentification unique](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800209.png "Authentification unique")
    
    a. Hello de coller **SAML Sign-On URL du Service unique** valeur hello **URL d’utilisateurs de toowhich hello portail SAML sont envoyés pour l’authentification** zone de texte.
    
    b. Bonjour **attribut contenant le nom de connexion** zone de texte, type **NameID**.
    
    c. tooupload votre certificat téléchargé, cliquez sur **Zscaler pem**.
    
    d. Sélectionnez **Enable SAML Auto-Provisioning**.

12. Sur hello **configurer l’authentification utilisateur** boîte de dialogue de page, effectuer hello comme suit :

    ![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800210.png "Administration")
    
    a. Cliquez sur **Enregistrer**.

    b. Cliquez sur **Activate Now**.

## <a name="configuring-proxy-settings"></a>Configuration des paramètres de proxy
### <a name="tooconfigure-hello-proxy-settings-in-internet-explorer"></a>paramètres de proxy tooconfigure hello dans Internet Explorer

1. Démarrez **Internet Explorer**.

2. Sélectionnez **options Internet** de hello **outils** menu Ouvrir hello **Options Internet** boîte de dialogue.   
    
     ![Options Internet](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769492.png "Options Internet")

3. Cliquez sur hello **connexions** onglet.   
  
     ![Connexions](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769493.png "Connexions")

4. Cliquez sur **paramètres LAN** tooopen hello **paramètres LAN** boîte de dialogue.

5. Dans la section serveur Proxy de hello, procédez hello comme suit :   
   
    ![Serveur proxy](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769494.png "Serveur proxy")

    a. Sélectionnez **Utiliser un serveur proxy pour le réseau local**.

    b. Dans la zone de texte adresse hello, tapez **gateway.zscalerone.net**.

    c. Dans la zone de texte Port hello, tapez **80**.

    d. Sélectionnez **Ne pas utiliser de serveur proxy pour les adresses locales**.

    e. Cliquez sur **OK** tooclose hello **les paramètres de réseau local (LAN)** boîte de dialogue.

6. Cliquez sur **OK** tooclose hello **Options Internet** boîte de dialogue.

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.

### <a name="creating-a-zscaler-zscloud-test-user"></a>Créer un utilisateur de test Zscaler ZSCloud

tooenable Azure AD les utilisateurs toolog tooZScaler ZSCloud, elles doivent être mis en service tooZScaler ZSCloud.  
Dans les cas de hello de ZScaler ZSCloud, cette configuration est une tâche manuelle.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>configuration, de l’utilisateur tooconfigure effectuer hello comme suit :

1. Connectez-vous à tooyour **Zscaler** client.

2. Cliquez sur **Administration**.   
   
    ![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781035.png "Administration")

3. Cliquez sur **User Management**.   
        
     ![Add](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Add")

4. Bonjour **utilisateurs** , cliquez sur **ajouter**.
      
    ![Add](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Add")

5. Dans la section Ajouter un utilisateur de hello, procédez hello comme suit :
        
    ![Ajouter un utilisateur](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781038.png "Ajouter un utilisateur")
   
    a. Hello de type **UserID**, **nom d’utilisateur complet**, **mot de passe**, **confirmer le mot de passe**, puis sélectionnez **groupes**et hello **service** d’un compte AAD valide que vous souhaitez tooprovision.

    b. Cliquez sur **Enregistrer**.

> [!NOTE]
> Vous pouvez utiliser n’importe quel autre ZScaler ZSCloud utilisateur compte outil de création ou API fournie par ZScaler ZSCloud tooprovision des comptes d’utilisateur AAD.

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooZscaler ZSCloud.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooZscaler ZSCloud, procédez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Zscaler ZSCloud**.

    ![Configurer l’authentification unique](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Si vous souhaitez tootest vos paramètres d’authentification unique, ouvrez hello panneau d’accès.

Lorsque vous cliquez sur hello Zscaler ZSCloud vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour application Zscaler ZSCloud.

Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_203.png

