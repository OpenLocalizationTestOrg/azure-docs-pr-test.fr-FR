---
title: "Didacticiel : Intégration d’Azure Active Directory avec Jobscience | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Jobscience."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 77282dcc-bbe2-4728-953d-adb4ab6a713b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 4a4c78aad6d324795a15a9569542afc23b4716d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobscience"></a>Didacticiel : Intégration d’Azure Active Directory à Jobscience

Dans ce didacticiel, vous apprendrez comment toointegrate Jobscience avec Azure Active Directory (Azure AD).

Intégration de Jobscience à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooJobscience
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooJobscience (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec Jobscience, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Jobscience pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois ici : [offre d’essai](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de Jobscience à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-jobscience-from-hello-gallery"></a>Ajout de Jobscience à partir de la galerie de hello
intégration de hello tooconfigure de Jobscience dans Azure AD, vous devez tooadd Jobscience à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Jobscience à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **Jobscience**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_search.png)

5. Dans le volet de résultats hello, sélectionnez **Jobscience**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Jobscience avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Jobscience est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Jobscience doit toobe établie.

En l’occurrence, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec Jobscience, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test de Jobscience](#creating-a-jobscience-test-user)**  -toohave un équivalent de Britta Simon dans Jobscience est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de Jobscience.

**tooconfigure Azure AD single sign-on avec Jobscience, procédez hello comme suit :**

1. Bonjour portail Azure, sur hello **Jobscience** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_samlbase.png)

3. Sur hello **Jobscience domaine et les URL** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_url.png)

    Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`http://<company name>.my.salesforce.com`
    
    > [!NOTE] 
    > Cette valeur n’est pas la valeur réelle. Mettre à jour de cette valeur avec hello URL de connexion réel. Obtenir cette valeur en [équipe de support Client de Jobscience](https://www.jobscience.com/support) ou à partir du profil d’authentification unique hello, vous allez créer qui est expliqué plus loin dans le didacticiel de hello. 
 
4. Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-jobscience-tutorial/tutorial_general_400.png)

6. Sur hello **Jobscience Configuration** , cliquez sur **configurer de Jobscience** tooopen **configurer l’authentification** fenêtre. Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_configure.png) 

7. Ouvrez une session dans tooyour site d’entreprise Jobscience en tant qu’administrateur.

8. Accédez trop**le programme d’installation**.
   
   ![Configuration](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Configuration")

9. Dans le volet de navigation gauche hello Bonjour **administrer** , cliquez sur **gestion des domaines** tooexpand hello section associée, puis cliquez sur **mon domaine** tooopen hello  **Mon domaine** page. 
   
   ![Mon domaine](./media/active-directory-saas-jobscience-tutorial/ic767825.png "mon domaine")

10. tooverify votre domaine a été correctement configuré, assurez-vous qu’il s’agit de «**tooUsers de déploiement d’étape 4**» et passez en revue votre «**mes paramètres de domaine**».

    ![Domaine déployé tooUser](./media/active-directory-saas-jobscience-tutorial/ic784377.png "tooUser de domaine déployés")

11. Sur le site d’entreprise hello Jobscience, cliquez sur **des contrôles de sécurité**, puis cliquez sur **paramètres d’authentification unique**.
    
    ![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784364.png "Security Controls")

12. Bonjour **paramètres d’authentification unique** section, effectuer hello comme suit :
    
    ![Paramètres d’authentification unique](./media/active-directory-saas-jobscience-tutorial/ic781026.png "paramètres d’authentification unique")
    
    a. Sélectionnez **SAML Enabled**.

    b. Cliquez sur **Nouveau**.

13. Sur hello **SAML unique Sign-On Setting Edit** boîte de dialogue, effectuer hello comme suit :
    
    ![Configuration de l’authentification unique SAML](./media/active-directory-saas-jobscience-tutorial/ic784365.png "Configuration de l’authentification unique SAML")
    
    a. Bonjour **nom** zone de texte, tapez un nom pour votre configuration.

    b. Dans **émetteur** zone de texte, valeur hello coller **ID d’entité SAML**, lequel vous avez copié à partir du portail Azure.

    c. Bonjour **Id d’entité** zone de texte, type`https://salesforce-jobscience.com`

    d. Cliquez sur **Parcourir** tooupload votre certificat Azure AD.

    e. En tant que **SAML Identity Type**, sélectionnez **Assertion contient hello ID de fédération à partir de l’objet utilisateur de hello**.

    f. En tant que **emplacement d’identité SAML**, sélectionnez **identité figure dans l’élément NameIdentifier de hello Hello Subject statement**.

    g. Dans **Identity Provider Login URL** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir du portail Azure.

    h. Dans **Identity Provider Logout URL** zone de texte, valeur hello coller **URL de déconnexion**, lequel vous avez copié à partir du portail Azure.

    i. Cliquez sur **Enregistrer**.

14. Dans le volet de navigation gauche hello Bonjour **administrer** , cliquez sur **gestion des domaines** tooexpand hello section associée, puis cliquez sur **mon domaine** tooopen hello  **Mon domaine** page. 
    
    ![Mon domaine](./media/active-directory-saas-jobscience-tutorial/ic767825.png "mon domaine")

15. Sur hello **mon domaine** page hello **Login Page Branding** , cliquez sur **modifier**.
    
    ![Personnalisation de la page de connexion](./media/active-directory-saas-jobscience-tutorial/ic767826.png "personnalisation de la page de connexion")

16. Sur hello **Login Page Branding** page hello **Service d’authentification** section et le nom hello votre **SAML SSO Settings** s’affiche. Sélectionnez-le, puis cliquez sur **Save**.
    
    ![Personnalisation de la page de connexion](./media/active-directory-saas-jobscience-tutorial/ic784366.png "personnalisation de la page de connexion")

17. tooget hello SP initiée par l’authentification unique de, cliquez sur l’URL de connexion sur hello **Single Sign On paramètres** Bonjour **des contrôles de sécurité** section de menu.

    ![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784368.png "Security Controls")
    
    Cliquez sur le profil d’authentification unique hello que vous avez créé à l’étape hello ci-dessus. Cette page affiche hello l’authentification unique sur l’URL de votre société (par exemple, [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).    

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-jobscience-test-user"></a>Création d’un utilisateur de test Jobscience

Dans l’ordre tooenable Azure AD les utilisateurs toolog dans tooJobscience, vous devez les configurer dans Jobscience. Dans les cas de hello de Jobscience, cette configuration est une tâche manuelle.

>[!NOTE]
>Vous pouvez utiliser n’importe quel autre occurrence utilisateur compte outil de création ou API fournie par Jobscience tooprovision Azure Active Directory des comptes d’utilisateur.
>  
        
**configuration, de l’utilisateur tooconfigure effectuer hello comme suit :**

1. Connectez-vous à tooyour **Jobscience** site d’entreprise en tant qu’administrateur.

2. Accédez à tooSetup.
   
   ![Configuration](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Configuration")
3. Accédez trop**gérer les utilisateurs \> utilisateurs**.
   
   ![Utilisateurs](./media/active-directory-saas-jobscience-tutorial/ic784369.png "Utilisateurs")
4. Cliquez sur **New User**.
   
   ![Tous les utilisateurs](./media/active-directory-saas-jobscience-tutorial/ic784370.png "Tous les utilisateurs")
5. Sur hello **modifier un utilisateur** boîte de dialogue, effectuer hello comme suit :
   
   ![Modification de l’utilisateur](./media/active-directory-saas-jobscience-tutorial/ic784371.png "modification de l’utilisateur")
   
   a. Bonjour **prénom** zone de texte, tapez un prénom de l’utilisateur hello comme Brian.
   
   b. Bonjour **nom** zone de texte, tapez un nom d’utilisateur hello comme Simon.
   
   c. Bonjour **Alias** zone de texte, tapez un nom d’alias d’utilisateur hello comme brittas.

   d. Bonjour **messagerie** adresse de messagerie de type hello d’utilisateur de zone de texte, comme Brittasimon@contoso.com.

   e. Bonjour **nom d’utilisateur** zone de texte, tapez un nom d’utilisateur de l’utilisateur comme Brittasimon@contoso.com.

   f. Bonjour **surnom** zone de texte, tapez le nom d’utilisateur comme Simon nick.

   g. Cliquez sur **Enregistrer**.

    
> [!NOTE]
> titulaire du compte Azure Active Directory Hello reçoit un message électronique et suit un tooconfirm de lier leur compte avant son activation.

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooJobscience.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooJobscience, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Jobscience**.

    ![Configurer l’authentification unique](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque de Jobscience hello Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour Jobscience application.
Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_203.png

