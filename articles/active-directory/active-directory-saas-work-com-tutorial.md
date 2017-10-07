---
title: "Didacticiel : Intégration d’Azure Active Directory à Work.com | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Work.com."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 98e6739e-eb24-46bd-9dd3-20b489839076
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: dcdc51c884abd78c945b649de99f942d32373cf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workcom"></a>Didacticiel : Intégration d’Azure AD à Work.com

Dans ce didacticiel, vous apprendrez comment toointegrate Work.com avec Azure Active Directory (Azure AD).

Intégration de Work.com à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooWork.com
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooWork.com (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec Work.com, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Work.com pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajouter des Work.com à partir de la galerie de hello
2. Configurer et tester l’authentification unique Azure AD

## <a name="add-workcom-from-hello-gallery"></a>Ajouter des Work.com à partir de la galerie de hello
intégration de hello tooconfigure de Work.com dans Azure AD, vous devez tooadd Work.com à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Work.com à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **Work.com**, sélectionnez **Work.com** à partir du panneau résultats puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Ajouter à partir de la galerie](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Work.com avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Work.com est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Work.com doit toobe établie.

Dans Work.com, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec Work.com, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Créer un utilisateur de test Work.com](#create-a-workcom-test-user)**  -toohave un équivalent de Britta Simon dans Work.com est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configure-azure-ad-single-sign-on"></a>Configurer l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Work.com.

>[!NOTE]
>tooconfigure l’authentification unique, vous devez encore toosetup un nom de domaine Work.com personnalisé. Vous devez toodefine au moins un domaine nom, votre nom de domaine de test et déployez-le tooyour toute organisation.

**tooconfigure Azure AD single sign-on avec Work.com, procédez hello comme suit :**

1. Bonjour portail Azure, sur hello **Work.com** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Authentification basée sur SAML](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_samlbase.png)

3. Sur hello **Work.com domaine et les URL** section, hello suivants :

    ![Section Domaine et URL Work.com](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_url.png)

    Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`http://<companyname>.my.salesforce.com`

    > [!NOTE] 
    > Cette valeur n’est pas la valeur réelle. Mettre à jour de cette valeur avec hello URL de connexion réel. Contact [équipe de support Client de Work.com](https://help.salesforce.com/articleView?id=000159855&type=3) tooget cette valeur. 

4. Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![Section Certificat de signature SAML](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Bouton Enregistrer](./media/active-directory-saas-work-com-tutorial/tutorial_general_400.png)

6. Sur hello **Work.com Configuration** , cliquez sur **configurer de Work.com** tooopen **configurer l’authentification** fenêtre. Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Section Configuration de Work.com](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_configure.png) 
7. Ouvrez une session dans tooyour client Work.com en tant qu’administrateur.

8. Accédez trop**le programme d’installation**.
   
    ![Configuration](./media/active-directory-saas-work-com-tutorial/ic794108.png "Configuration")

9. Dans le volet de navigation gauche hello Bonjour **administrer** , cliquez sur **gestion des domaines** tooexpand hello section associée, puis cliquez sur **mon domaine** tooopen hello  **Mon domaine** page. 
   
    ![Mon domaine](./media/active-directory-saas-work-com-tutorial/ic767825.png "mon domaine")

10. tooverify votre domaine a été correctement configuré, assurez-vous qu’il s’agit de «**tooUsers de déploiement d’étape 4**» et passez en revue votre «**mes paramètres de domaine**».
   
    ![Domaine déployé tooUser](./media/active-directory-saas-work-com-tutorial/ic784377.png "tooUser de domaine déployés")

11. Ouvrez une session dans tooyour client Work.com.

12. Accédez trop**le programme d’installation**.
    
    ![Configuration](./media/active-directory-saas-work-com-tutorial/ic794108.png "Configuration")

13. Développez hello **des contrôles de sécurité** menu, puis sur **paramètres d’authentification unique**.
    
    ![Paramètres d’authentification unique](./media/active-directory-saas-work-com-tutorial/ic794113.png "paramètres d’authentification unique")

14. Sur hello **paramètres d’authentification unique** boîte de dialogue de page, effectuer hello comme suit :
    
    ![SAML activé](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML activé")
    
    a. Sélectionnez **SAML Enabled**.
    
    b. Cliquez sur **Nouveau**.

15. Bonjour **paramètres d’authentification unique SAML** section, effectuer hello comme suit :
    
    ![Configuration de l’authentification unique SAML](./media/active-directory-saas-work-com-tutorial/ic794114.png "Configuration de l’authentification unique SAML")
    
    a. Bonjour **nom** zone de texte, tapez un nom pour votre configuration.  
       
    > [!NOTE]
    > En fournissant une valeur pour **nom** permet de remplir automatiquement hello **nom de l’API** zone de texte.
    
    b. Dans **émetteur** zone de texte, valeur hello coller **ID d’entité SAML** dont vous avez copié à partir du portail Azure.
    
    c. certificat de hello téléchargé tooupload à partir du portail Azure, cliquez sur **Parcourir**.
    
    d. Bonjour **Id d’entité** zone de texte, type `https://salesforce-work.com`.
    
    e. En tant que **SAML Identity Type**, sélectionnez **Assertion contient hello ID de fédération à partir de l’objet utilisateur de hello**.
    
    f. En tant que **emplacement d’identité SAML**, sélectionnez **identité figure dans l’élément NameIdentifier de hello Hello Subject statement**.
    
    g. Dans **Identity Provider Login URL** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure.

    h. Dans **Identity Provider Logout URL** zone de texte, valeur hello coller **URL de déconnexion** dont vous avez copié à partir du portail Azure.
    
    i. Pour **Service Provider Initiated Request Binding**, sélectionnez **HTTP POST**.
    
    j. Cliquez sur **Enregistrer**.

16. Dans votre portail classique Work.com, dans le volet de navigation gauche hello, cliquez sur **gestion des domaines** tooexpand hello section associée, puis cliquez sur **mon domaine** tooopen hello **mon domaine**page. 
    
    ![Mon domaine](./media/active-directory-saas-work-com-tutorial/ic794115.png "mon domaine")

17. Sur hello **mon domaine** page hello **Login Page Branding** , cliquez sur **modifier**.
    
    ![Personnalisation de la page de connexion](./media/active-directory-saas-work-com-tutorial/ic767826.png "personnalisation de la page de connexion")

14. Sur hello **Login Page Branding** page hello **Service d’authentification** section et le nom hello votre **SAML SSO Settings** s’affiche. Sélectionnez-le, puis cliquez sur **Save**.
    
    ![Personnalisation de la page de connexion](./media/active-directory-saas-work-com-tutorial/ic784366.png "personnalisation de la page de connexion")

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-work-com-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Utilisateurs et groupes -> Tous les utilisateurs](./media/active-directory-saas-work-com-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Ajouter](./media/active-directory-saas-work-com-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Boîte de dialogue utilisateur](./media/active-directory-saas-work-com-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="create-a-workcom-test-user"></a>Créer un utilisateur de test Work.com
Pour Azure Active Directory utilisateurs toobe en mesure de toosign dans, ils doivent être mis en service tooWork.com. Dans les cas de hello de Work.com, cette configuration est une tâche manuelle.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>configuration, de l’utilisateur tooconfigure effectuer hello comme suit :
1. Se connecter tooyour site d’entreprise Work.com en tant qu’administrateur.

2. Accédez trop**le programme d’installation**.
   
    ![Configuration](./media/active-directory-saas-work-com-tutorial/IC794108.png "Configuration")
3. Accédez trop**gérer les utilisateurs \> utilisateurs**.
   
    ![Gestion des utilisateurs](./media/active-directory-saas-work-com-tutorial/IC784369.png "Gestion des utilisateurs")

4. Cliquez sur **New User**.
   
    ![Tous les utilisateurs](./media/active-directory-saas-work-com-tutorial/IC794117.png "Tous les utilisateurs")

5. Bonjour section modification utilisateur, effectuer hello comme suit, dans les attributs d’un Azure valide compte AD tooprovision dans hello relatives des zones de texte :
   
    ![Modification de l’utilisateur](./media/active-directory-saas-work-com-tutorial/ic794118.png "modification de l’utilisateur")
   
    a. Bonjour **prénom** hello de type zone de texte **prénom** d’utilisateur de hello **Brian**.
    
    b. Bonjour **nom** hello de type zone de texte **nom** d’utilisateur de hello **Simon**.
    
    c. Bonjour **Alias** hello de type zone de texte **nom** d’utilisateur de hello **BrittaS**.
    
    d. Bonjour **messagerie** hello de type zone de texte **adresse de messagerie** d’utilisateur  **Brittasimon@contoso.com** .
    
    e. Bonjour **nom d’utilisateur** zone de texte, tapez un nom d’utilisateur de l’utilisateur comme  **Brittasimon@contoso.com** .
    
    f. Bonjour **surnom** zone de texte, tapez un **surnom** d’utilisateur **Simon**.
    
    g. Sélectionnez **Rôle**, **Licence utilisateur** et **Profil**.
    
    h. Cliquez sur **Enregistrer**.  
      
    > [!NOTE]
    > détenteur du compte de Hello Azure AD reçoit un message électronique contenant un compte de hello tooconfirm lien avant son activation.
    > 
    > 

### <a name="assign-hello-azure-ad-test-user"></a>Affecter l’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooWork.com.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooWork.com, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Work.com**.

    ![Work.com dans la liste des applications](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="test-single-sign-on"></a>Tester l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque Work.com hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Work.com application.
Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_203.png

