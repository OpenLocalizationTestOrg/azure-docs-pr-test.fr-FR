---
title: "Didacticiel : Intégration d’Azure Active Directory à Slack | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et la marge."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffc5e73f-6c38-4bbb-876a-a7dd269d4e1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 7f0151401af4dc63d2f714d4b4f66380c4b51e0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-slack"></a>Didacticiel : Intégration d’Azure AD avec Slack

Dans ce didacticiel, vous apprendrez comment toointegrate marge avec Azure Active Directory (Azure AD).

Intégration de marge à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooSlack
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSlack (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

intégration d’Azure AD avec une marge de tooconfigure, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Slack pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de la marge à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-slack-from-hello-gallery"></a>Ajout de la marge à partir de la galerie de hello
intégration de hello tooconfigure marge dans Azure AD, vous devez tooadd Slack à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Slack à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **Slack**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-slack-tutorial/tutorial_slack_search.png)

5. Dans le volet de résultats hello, sélectionnez **Slack**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-slack-tutorial/tutorial_slack_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Slack avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Slack est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans la marge hello doit toobe établie.

Dans la marge, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec une marge, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur test marge](#creating-a-slack-test-user)**  -toohave un équivalent de Britta Simon dans Slack est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de marge.

**tooconfigure Azure AD authentification unique avec une marge, effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **Slack** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-slack-tutorial/tutorial_slack_samlbase.png)

3. Sur hello **URL et le domaine de la marge** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-slack-tutorial/tutorial_slack_url.png)

    a. Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.slack.com`

    b. Bonjour **identificateur** zone de texte, tapez l’URL hello :`https://slack.com`

    > [!NOTE] 
    > valeur de Hello n’est pas réelle. Vous avez tooupdate valeur hello hello réel URL de connexion. Contact [équipe de support marge](https://slack.com/help/contact) valeur de hello tooget
     
4. Marge application attend les assertions SAML hello dans un format spécifique. Configurer hello suivant des revendications pour cette application. Vous pouvez gérer les valeurs de ces attributs hello depuis hello »**attributs utilisateur**« section sur la page d’intégration d’application. Hello suivant capture d’écran montre un exemple de cela.
    
    ![Configurer l’authentification unique](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute.png)

5. Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, sélectionnez **user.mail** en tant que **identificateur d’utilisateur** et pour chaque ligne indiqué dans le tableau hello ci-dessous, effectuez hello comme suit :
    
    | Nom de l'attribut | Valeur de l’attribut |
    | --- | --- |
    | first_name | user.givenname |
    | last_name | user.surname |
    | User.Email | user.mail |  
    | User.Username | user.userprincipalname |

    a. Cliquez sur **attribut** tooopen **modifier l’attribut** boîte de dialogue zone et effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute1.png)

    a. Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.
    
    b. À partir de hello **valeur** liste, la valeur de l’attribut select hello indiqué pour cette ligne.
    
    c. Cliquez sur **OK**

6. Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-slack-tutorial/tutorial_slack_certificate.png)

7. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-slack-tutorial/tutorial_general_400.png)

8. Sur hello **Slack Configuration** , cliquez sur **configurer une marge** tooopen **configurer l’authentification** fenêtre. Hello de copie **ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-slack-tutorial/tutorial_slack_configure.png) 

9.  Dans une fenêtre de navigateur web, ouvrez une session dans le site de société Slack tooyour en tant qu’administrateur.

10.  Accédez trop**Microsoft Azure AD** puis passez trop**paramètres d’équipe**.

     ![Configurer l’authentification unique côté application](./media/active-directory-saas-slack-tutorial/tutorial_slack_001.png)

11.  Bonjour **paramètres d’équipe** , cliquez sur hello **authentification** onglet, puis cliquez sur **modifier les paramètres**.

     ![Configurer l’authentification unique côté application](./media/active-directory-saas-slack-tutorial/tutorial_slack_002.png)

12. Sur hello **paramètres d’authentification SAML** boîte de dialogue, effectuer hello comme suit :

    ![Configurer l’authentification unique côté application](./media/active-directory-saas-slack-tutorial/tutorial_slack_003.png)

    a.  Bonjour **SAML 2.0 point de terminaison (HTTP)** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir du portail Azure.

    b.  Bonjour **émetteur de fournisseur d’identité** zone de texte, valeur hello coller **ID d’entité SAML**, lequel vous avez copié à partir du portail Azure.

    c.  Ouvrez votre fichier de certificat téléchargé dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite toohello **certificat Public** zone de texte.

    d. Configurez hello trois paramètres ci-dessus comme il convient pour votre équipe de marge. Pour plus d’informations sur les paramètres de hello, Veuillez trouver hello **guide de configuration de l’authentification unique de marge** ici. `https://get.slack.help/hc/articles/220403548-Guide-to-single-sign-on-with-Slack%60`

    e.  Cliquez sur **Enregistrer la configuration**.
     
    <!-- Deselect **Allow users toochange their email address**.

    e.  Select **Allow users toochoose their own username**.

    f.  As **Authentication for your team must be used by**, select **It’s optional**. -->

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-slack-test-user"></a>Création d’un utilisateur de test Slack

objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans la marge. Slack prend en charge l’approvisionnement juste-à-temps, option activée par défaut.

Vous n’avez aucune opération à effectuer dans cette section. Un nouvel utilisateur est créé au cours d’une tentative de tooaccess Slack s’il n’existe pas encore.

> [!NOTE]
> Si vous devez manuellement toocreate un utilisateur, vous devez tooContact [équipe de support marge](https://slack.com/help/contact).

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooSlack.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooSlack, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Slack**.

    ![Configurer l’authentification unique](./media/active-directory-saas-slack-tutorial/tutorial_slack_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur la vignette de marge hello dans hello volet d’accès, vous devez obtenir application de marge automatiquement signé sur tooyour.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-slack-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-slack-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-slack-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-slack-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-slack-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-slack-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-slack-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-slack-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-slack-tutorial/tutorial_general_203.png

