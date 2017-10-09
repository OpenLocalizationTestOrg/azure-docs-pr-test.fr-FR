---
title: "Didacticiel : Intégration d’Azure Active Directory à Wdesk | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Wdesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 06900a91-a326-4663-8ba6-69ae741a536e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 2c278a5e4f50cc362663efc0f826ff0c0fcf6e7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wdesk"></a>Didacticiel : Intégration d’Azure Active Directory à Wdesk

Dans ce didacticiel, vous apprendrez comment toointegrate Wdesk avec Azure Active Directory (Azure AD).

Intégration Wdesk à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooWdesk
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooWdesk (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez. [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec Wdesk, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Wdesk avec authentification unique activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de Wdesk à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-wdesk-from-hello-gallery"></a>Ajout de Wdesk à partir de la galerie de hello
intégration de hello tooconfigure de Wdesk dans Azure AD, vous devez tooadd Wdesk à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Wdesk à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **Wdesk**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_search.png)

5. Dans le volet de résultats hello, sélectionnez **Wdesk**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Wdesk, avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Wdesk est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Wdesk doit toobe établie.

Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Wdesk.

tooconfigure et test Azure AD l’authentification unique avec Wdesk, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test Wdesk](#creating-a-wdesk-test-user)**  -toohave un équivalent de Britta Simon dans Wdesk est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Wdesk.

**tooconfigure Azure AD single sign-on avec Wdesk, effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **Wdesk** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_samlbase.png)

3. Sur hello **Wdesk domaine et les URL** section, si vous le souhaitez application hello tooconfigure **IDP** mode initié effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url.png)

    a. Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`

    b. Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`

4. Cliquez sur **Afficher les paramètres d’URL avancés**. Si vous le souhaitez application hello tooconfigure **SP** initiée par le mode, effectuer hello suivant l’étape :

    ![Configurer l’authentification unique](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url1.png)

    Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`
     
    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettre à jour ces valeurs avec hello réel identificateur, URL de réponse et URL de connexion. Vous obtenez ces valeurs à partir du portail de WDesk lorsque vous configurez l’authentification unique de hello. 
  
5. Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_certificate.png) 

6. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-wdesk-tutorial/tutorial_general_400.png)
    
7. Dans une fenêtre de navigateur web, tooWdesk de connexion en tant qu’administrateur de sécurité.

8. Dans hello inférieur gauche, cliquez sur **Admin** et choisissez **Admin. compte**:
 
     ![Configurer l’authentification unique](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

9. Dans Wdesk Admin, accédez trop**sécurité**, puis **SAML** > **paramètres SAML**:

    ![Configurer l’authentification unique](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig2.png)

10. Sous **paramètres généraux**, vérifiez hello **activer SAML Single Sign On**:

    ![Configurer l’authentification unique](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig3.png)

11. Sous **détails du fournisseur de Service**, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig4.png)

      a. Hello de copie **URL de connexion** et collez-le dans **Url de connexion** zone de texte sur le portail Azure.
   
      b. Hello de copie **Url de métadonnées** et collez-le dans **identificateur** zone de texte sur le portail Azure.
       
      c. Hello de copie **consommateur url** et collez-le dans **Url de réponse** zone de texte sur le portail Azure.
   
      d. Cliquez sur **enregistrer** sur les modifications de hello toosave portail Azure.      

12. Cliquez sur **configurer les paramètres IdP** tooopen **modifier les paramètres de fournisseurs d’identité** boîte de dialogue. Cliquez sur **choisir un fichier** toolocate hello **Metadata.xml** fichier que vous avez enregistré à partir du portail Azure, puis le télécharger.
    
    ![Configurer l’authentification unique](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig5.png)
  
13. Cliquez sur **Save changes**.

    ![Configurer l’authentification unique](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfigsavebutton.png)

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-wdesk-test-user"></a>Création d’un utilisateur de test Wdesk

tooenable Azure AD les utilisateurs toolog dans tooWdesk, vous devez les configurer dans Wdesk. Dans Wdesk, l’approvisionnement est une tâche manuelle.

**tooprovision un compte d’utilisateur, effectuez hello comme suit :**

1. Connectez-vous en tant qu’administrateur de sécurité tooWdesk.
2. Accédez trop**Admin** > **Admin. compte**.

     ![Configurer l’authentification unique](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

3. Dans **Personnes**, cliquez sur **Membres**.

4. Maintenant, cliquez sur **Add Member** tooopen **Add Member** boîte de dialogue. 
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser1.png)  

5. Dans **utilisateur** texte, entrez le nom d’utilisateur hello d’utilisateur comme  **brittasimon@contoso.com**  et cliquez sur **continuer** bouton.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser3.png)

6.  Entrez les détails de hello comme indiqué ci-dessous :
  
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser4.png)
 
    a. Dans **messagerie** texte, entrez l’e-mail hello d’utilisateur comme  **brittasimon@contoso.com** .

    b. Dans **prénom** texte, entrez le nom d’utilisateur comme hello **Brian**.

    c. Dans **nom** texte, entrez le nom d’utilisateur comme hello **Simon**.

7. Cliquez sur **Enregistrer membre**.  

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser5.png)

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooWdesk.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooWdesk, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Wdesk**.

    ![Configurer l’authentification unique](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque Wdesk hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Wdesk application.
Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).


## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_203.png

