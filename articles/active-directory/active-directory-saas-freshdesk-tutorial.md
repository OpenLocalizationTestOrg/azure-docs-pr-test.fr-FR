---
title: "Didacticiel : Intégration d’Azure Active Directory avec FreshDesk | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de FreshDesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2a3e5aa-7b5a-4fe4-9285-45dbe6e8efcc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 577a5eb6d9b1bc03030a2b47f63d375869c903bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshdesk"></a>Didacticiel : Intégration d’Azure Active Directory à FreshDesk

Dans ce didacticiel, vous apprendrez comment toointegrate FreshDesk avec Azure Active Directory (Azure AD).

Intégration de FreshDesk à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooFreshDesk
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooFreshDesk (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central - portail de gestion Azure hello

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD à FreshDesk, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement FreshDesk pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de FreshDesk à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-freshdesk-from-hello-gallery"></a>Ajout de FreshDesk à partir de la galerie de hello
intégration de hello tooconfigure de FreshDesk dans Azure AD, vous devez tooadd FreshDesk à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd FreshDesk à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour ** [portail de gestion Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. Cliquez sur **ajouter** bouton en haut de hello de boîte de dialogue hello.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **FreshDesk**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_search.png)

5. Dans le volet de résultats hello, sélectionnez **FreshDesk**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous configurez et testez l’authentification unique Azure AD avec FreshDesk avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans FreshDesk est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans FreshDesk doit toobe établie.

Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans FreshDesk.

tooconfigure et test Azure AD l’authentification unique à FreshDesk, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user) ** -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test de FreshDesk](#creating-a-freshdesk-test-user) ** -toohave de Britta Simon dans FreshDesk qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on) ** -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique dans le portail de gestion Azure hello et configurez l’authentification unique dans votre application FreshDesk.

**tooconfigure Azure AD single sign-on avec FreshDesk, procédez hello comme suit :**

1. Dans le portail de gestion Azure hello, sur hello **FreshDesk** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, en tant que **Mode** sélectionnez **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_samlbase.png)

3. Sur hello **FreshDesk domaine et les URL** section, Veuillez entrer hello **URL de connexion** en tant que : `https://<tenant-name>.freshdesk.com` ou toute autre valeur Freshdesk a suggéré.

    ![Configurer l’authentification unique](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_url.png)

    > [!NOTE] 
    > Notez qu’il ne s’agit pas de la valeur réelle. Vous devez mettre à jour la valeur avec l’URL de connexion réelle. Contactez [l’équipe de support FreshDesk](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg) pour obtenir cette valeur.  

4. Sur hello **le certificat de signature SAML** , cliquez sur **certificat** , puis enregistrez le certificat de hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-freshdesk-tutorial/tutorial_general_400.png)

6. Sur hello **FreshDesk Configuration** , cliquez sur **FreshDesk de configuration** tooopen configurer l’authentification sur fenêtre. Copier hello SAML Sign-On URL du Service unique et les URL de déconnexion de hello **aide-mémoire** section.

    ![Configurer l’authentification unique](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_configure.png)

7. Dans une autre fenêtre de navigateur web, connectez-vous au site de votre entreprise Freshdesk en tant qu’administrateur.

8. Dans le menu hello haut de hello, cliquez sur **Admin**.
   
   ![Administrateur](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "Administrateur")

9. Bonjour **paramètres généraux** , cliquez sur **sécurité**.
   
   ![Sécurité](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "Sécurité")

10. Bonjour **sécurité** section, effectuer hello comme suit :
   
    ![Single Sign On](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "Single Sign On")
   
    a. Pour **Single Sign On (SSO)**, sélectionnez **On**.

    b. Sélectionnez **SAML SSO**.

    c. Hello de type **SAML Sign-On URL du Service unique** vous avez copié à partir du portail Azure dans hello **URL de connexion SAML** zone de texte.

    d. Hello de type **URL de déconnexion** vous avez copié à partir du portail Azure dans hello **URL de déconnexion** zone de texte.

    e. Hello de copie **l’empreinte numérique** à partir du certificat hello téléchargé à partir du portail Azure et collez-le dans hello **Security Certificate Fingerprint** zone de texte.  
 
    >[!TIP]
    >Pour plus d’informations, consultez [comment tooretrieve valeur d’empreinte numérique d’un certificat](http://youtu.be/YKQF266SAxI). 
    
    f. Cliquez sur **Save**.


### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate un utilisateur de test dans le portail de gestion Azure hello appelé Britta Simon.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail de gestion Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_01.png) 

2. Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_02.png) 

3. En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-freshdesk-test-user"></a>Création d’un utilisateur de test FreshDesk

Dans l’ordre tooenable le toolog d’utilisateurs Azure AD à FreshDesk, vous devez les configurer dans FreshDesk.  
Dans les cas de hello de FreshDesk, cette configuration est une tâche manuelle.

**effectuer des comptes d’utilisateur, tooprovision hello comme suit :**

1. Connectez-vous à tooyour **Freshdesk** client.
2. Dans le menu hello haut de hello, cliquez sur **Admin**.
   
   ![Administrateur](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "Administrateur")

3. Bonjour **paramètres généraux** , cliquez sur **Agents**.
   
   ![Agents](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "Agents")

4. Cliquez sur **New Agent**.
   
    ![New Agent](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "New Agent")

5. Dans la boîte de dialogue informations d’Agent hello, procédez hello comme suit :
   
   ![Agent Information](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "Agent Information")
   
   a. Bonjour **nom complet** zone de texte, nom du compte Azure AD de hello tooprovision hello du type.

   b. Bonjour **messagerie** zone de texte, hello de type Azure AD adresse de messagerie du compte Azure AD de hello tooprovision.

   c. Bonjour **titre** zone de texte, taper un titre du compte Azure AD de hello tooprovision hello.

   d. Sélectionnez **Agents role**, puis cliquez sur **Assign**.
       
   e. Cliquez sur **Enregistrer**.     
   
    >[!NOTE]
    >détenteur du compte de Hello Azure AD reçoit un message électronique qui inclut un compte de hello tooconfirm lien avant d’être activé. 
    > 
    
    >[!NOTE]
    >Vous pouvez utiliser n’importe quel autre Freshdesk utilisateur compte outil de création ou API fournie par Freshdesk tooprovision des comptes d’utilisateur AAD. tooFreshDesk.

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant tooBox de son accès.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooFreshDesk, effectuez hello comme suit :**

1. Dans le portail de gestion Azure hello, ouvrez la vue des applications hello, puis naviguez toohello les vue de répertoire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **FreshDesk**.

    ![Configurer l’authentification unique](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque FreshDesk hello hello volet d’accès, vous devez obtenir login page tooget connecté tooyour leur application FreshDesk.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_203.png

