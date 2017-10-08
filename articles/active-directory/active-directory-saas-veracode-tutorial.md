---
title: "Didacticiel : Intégration d’Azure Active Directory à Veracode | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Veracode."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4fe78050-cb6d-4db9-96ec-58cc0779167f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: d17307b3864b7df8ee55f569d8f962e2e315b936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-veracode"></a>Didacticiel : Intégration d’Azure AD à Veracode

Dans ce didacticiel, vous apprendrez comment toointegrate Veracode avec Azure Active Directory (Azure AD).

Intégration Veracode à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooVeracode.
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooVeracode (Single Sign-On) avec leurs comptes Azure AD.
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure veracode intégration d’Azure AD, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Veracode pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajouter des Veracode à partir de la galerie de hello
2. Configurer et tester l’authentification unique Azure AD

## <a name="add-veracode-from-hello-gallery"></a>Ajouter des Veracode à partir de la galerie de hello
intégration de hello tooconfigure de Veracode dans Azure AD, vous devez tooadd Veracode à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Veracode à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![bouton d’Azure Active Directory Hello][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![panneau des applications Enterprise Hello][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Nouveau bouton d’application Hello][3]

4. Dans la zone de recherche de hello, tapez **Veracode**, sélectionnez **Veracode** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.

    ![Veracode dans la liste des résultats hello](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD

Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Veracode avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Veracode est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Veracode doit toobe établie.

Dans Veracode, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique sur veracode, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Créer un utilisateur de test Veracode](#create-a-veracode-test-user)**  -toohave un équivalent de Britta Simon dans Veracode est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configure-azure-ad-single-sign-on"></a>Configurer l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Veracode.

**tooconfigure Azure AD l’authentification unique sur veracode, effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **Veracode** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Lien Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_samlbase.png)

3. Sur hello **Veracode domaine et les URL** section, l’utilisateur n’a pas tooperform toutes les étapes que l’application hello est déjà pré-intégration à Azure. 

    ![Configurer l’authentification unique](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_url.png)

4. Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_certificate.png) 

5. objectif Hello de cette section est toooutline comment tooenable utilisateurs tooauthenticate tooVeracode avec leur compte dans Azure AD en utilisant la fédération basée sur le protocole SAML de hello.

    Votre application Veracode attend les assertions SAML hello dans un format spécifique, ce qui vous oblige à tooyour de mappages d’attributs personnalisés tooadd **attributs du jeton saml** configuration. Hello suivant capture d’écran montre un exemple de cela.
    
    ![Attributs](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "Attributs")

6. mappages d’attributs tooadd hello requis, effectuez hello comme suit :

    | Nom de l'attribut | Valeur de l’attribut |
    |--- |--- |
    | firstname |User.givenname |
    | lastname |User.Surname |
    | email |User.mail |
    
    a. Pour chaque ligne de données dans la table hello ci-dessus, cliquez sur **ajouter un attribut utilisateur**.
    
    ![Attributs](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "Attributs")
    
    ![Attributs](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "Attributs")
    
    b. Bonjour **nom de l’attribut** zone de texte, nom d’attribut type hello indiqué pour cette ligne.
    
    c. Bonjour **valeur d’attribut** zone de texte, valeur de l’attribut select hello indiqué pour cette ligne.
    
    d. Cliquez sur **OK**.

7. Cliquez sur le bouton **Enregistrer** .

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-veracode-tutorial/tutorial_general_400.png)

8. Sur hello **Veracode Configuration** , cliquez sur **Veracode de configurer** tooopen **configurer l’authentification** fenêtre. Hello de copie **ID d’entité SAML** de hello **section de référence rapide.**

    ![Configuration de Veracode](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_configure.png) 

9. Dans une autre fenêtre de navigateur web, connectez-vous au site de votre entreprise Veracode en tant qu’administrateur.

10. Dans le menu hello haut de hello, cliquez sur **paramètres**, puis cliquez sur **Admin**.
   
    ![Administration](./media/active-directory-saas-veracode-tutorial/ic802911.png "Administration")

11. Cliquez sur hello **SAML** onglet.

12. Bonjour **organisation SAML paramètres** section, effectuer hello comme suit :
   
    ![Administration](./media/active-directory-saas-veracode-tutorial/ic802912.png "Administration")
   
    a.  Dans **émetteur** zone de texte, valeur hello coller **ID d’entité SAML** dont vous avez copié à partir du portail Azure.
    
    b. Cliquez sur votre certificat téléchargé à partir du portail Azure, de tooupload **choisir un fichier**.
   
    c. Sélectionnez **Enable Self Registration**.

13. Bonjour **les paramètres d’inscription libre-service** section, effectuer hello comme suit, puis cliquez sur **enregistrer**:
   
    ![Administration](./media/active-directory-saas-veracode-tutorial/ic802913.png "Administration")
   
    a. Dans **New User Activation**, sélectionnez **No Activation Required**.
   
    b. Dans **User Data Updates**, sélectionnez **Preference Veracode User Data**.
   
    c. Pour **des détails d’attribut SAML**, sélectionnez hello qui suit :
      * **Rôles d’utilisateur**
      * **Administrateur de la stratégie**
      * **Réviseur**
      * **Responsable de la sécurité**
      * **Responsable**
      * **Expéditeur**
      * **Créateur**
      * **Tous les types d’analyse**
      * **Appartenance aux équipes**
      * **Équipe par défaut**

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD

objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

   ![Créer un utilisateur de test Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-veracode-tutorial/create_aaduser_01.png)

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-veracode-tutorial/create_aaduser_02.png)

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.

    ![bouton Ajouter de Hello](./media/active-directory-saas-veracode-tutorial/create_aaduser_03.png)

4. Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-veracode-tutorial/create_aaduser_04.png)

    a. Bonjour **nom** , tapez **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.

    c. Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.

    d. Cliquez sur **Create**.
 
### <a name="create-a-veracode-test-user"></a>Créer un utilisateur de test Veracode
Dans l’ordre tooenable Azure AD les utilisateurs toolog dans Veracode, vous devez les configurer dans Veracode. Dans les cas de hello de Veracode, cette configuration est une tâche automatique. Vous n’avez rien à faire. Les utilisateurs sont automatiquement créés si nécessaire pendant hello première seule tentative de connexion.

> [!NOTE]
> Vous pouvez utiliser n’importe quel autre Veracode utilisateur compte outil de création ou API fournie par Veracode tooprovision comptes d’utilisateur Azure AD.
> 

### <a name="assign-hello-azure-ad-test-user"></a>Affecter l’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooVeracode.

![Attribuer le rôle d’utilisateur hello][200] 

**tooassign Britta Simon tooVeracode, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Veracode**.

    ![lien de Veracode Hello dans la liste des Applications hello](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_app.png)  

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![lien de « Utilisateurs et groupes » Hello][202]

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![volet d’ajouter l’affectation de Hello][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="test-single-sign-on"></a>Tester l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque Veracode hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Veracode application.
Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_203.png

