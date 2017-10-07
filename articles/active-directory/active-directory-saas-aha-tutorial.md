---
title: "Didacticiel : Intégration d’Azure Active Directory à Aha! | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Aha !."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ad955d3d-896a-41bb-800d-68e8cb5ff48d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: d844db3c0a035560e6fb275017215171743fba56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-aha"></a>Didacticiel : Intégration d’Azure Active Directory à Aha!

Dans ce didacticiel, vous apprendrez comment toointegrate Aha ! à Azure Active Directory (Azure AD).

L’intégration d’Aha! avec Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooAha !
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooAha ! (par le biais de l’authentification unique) avec leur compte Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD à Aha !, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Aha! Un abonnement pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout d’Aha! à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-aha-from-hello-gallery"></a>Ajout d’Aha! à partir de la galerie de hello
intégration de hello tooconfigure de Aha ! dans Azure AD, vous devez tooadd Aha ! à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Aha ! à partir de la galerie hello, effectuez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **Aha !**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-aha-tutorial/tutorial_aha_search.png)

5. Dans le volet de résultats hello, sélectionnez **Aha !**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-aha-tutorial/tutorial_aha_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous configurez et testez l’authentification unique Azure AD avec Aha! au moyen d’un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Aha ! est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Aha ! doit toobe établie.

Dans Aha !, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD sur l’authentification unique avec Aha !, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un sentiment ! utilisateur de test](#creating-an-aha-test-user)**  -toohave un équivalent de Britta Simon dans Aha ! qui est lié toohello la représentation sous forme de Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Aha ! application Aha!.

**tooconfigure Azure AD l’authentification unique avec Aha !, effectuer hello comme suit :**

1. Bonjour portail Azure, sur hello **Aha !** cliquez sur **Authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-aha-tutorial/tutorial_aha_samlbase.png)

3. Sur hello **Aha ! Domaine et les URL** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-aha-tutorial/tutorial_aha_url.png)

    a. Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.aha.io/session/new`

    b. Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.aha.io`

    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur. Pour obtenir ces valeurs, contactez [ Équipe de support client](https://www.aha.io/company/contact) tooget ces valeurs. 
 
4. Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-aha-tutorial/tutorial_aha_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-aha-tutorial/tutorial_general_400.png)

6. Dans une fenêtre de navigateur web, connectez-vous tooyour Aha ! en tant qu’administrateur.

7. Dans le menu hello haut de hello, cliquez sur **paramètres**.

    ![Paramètres](./media/active-directory-saas-aha-tutorial/IC798950.png "Paramètres")

8. Cliquez sur **Account**.
   
    ![Profil](./media/active-directory-saas-aha-tutorial/IC798951.png "Profil")

9. Cliquez sur **Security and single sign-on**.
   
    ![Sécurité et authentification unique](./media/active-directory-saas-aha-tutorial/IC798952.png "Sécurité et authentification unique")

10. Dans la section **Single Sign-On**, pour **Identity Provider**, sélectionnez **SAML2.0**.
   
    ![Sécurité et authentification unique](./media/active-directory-saas-aha-tutorial/IC798953.png "Sécurité et authentification unique")

11. Sur hello **Single Sign-On** configuration page, effectuer hello comme suit :
    
    ![Authentification unique](./media/active-directory-saas-aha-tutorial/IC798954.png "Authentification unique")
    
       a. Bonjour **nom** zone de texte, tapez un nom pour votre configuration.

       b. Pour **Configure using**, sélectionnez **Metadata File**.
   
       c. tooupload votre fichier de métadonnées téléchargé, cliquez sur **Parcourir**.
   
       d. Cliquez sur **Update**.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Créer**.
 
### <a name="creating-an-aha-test-user"></a>Création d’un utilisateur de test Aha!

toolog d’utilisateurs tooenable Azure AD dans tooAha !, vous devez les configurer dans Aha !.  

Dans le cas de hello de Aha !, cette configuration est une tâche automatique. Vous n’avez rien à faire.

Les utilisateurs sont automatiquement créés si nécessaire pendant hello première seule tentative de connexion.

>[!NOTE]
>Vous pouvez utiliser n’importe quel autre outil de création de compte utilisateur Aha! ou toute API fournie par Aha! tooprovision des comptes d’utilisateur AAD.

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooAha !.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooAha !, effectuer hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Aha !**.

    ![Configurer l’authentification unique](./media/active-directory-saas-aha-tutorial/tutorial_aha_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Si vous souhaitez tootest vos paramètres d’authentification unique, ouvrez hello panneau d’accès. Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-aha-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-aha-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-aha-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-aha-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-aha-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-aha-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-aha-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-aha-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-aha-tutorial/tutorial_general_203.png

