---
title: "Didacticiel : intégration d’Azure Active Directory à Thoughtworks Mingle | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et l’occurrence."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 69d859d9-b7f7-4c42-bc8c-8036138be586
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: c17f8e13d2db3de7d228d9b27128d134f98d6cdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thoughtworks-mingle"></a>Didacticiel : Intégration d’Azure AD à Thoughtworks Mingle

Dans ce didacticiel, vous apprendrez comment toointegrate l’occurrence avec Azure Active Directory (Azure AD).

Intégration de l’occurrence avec Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooThoughtworks Mingle
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooThoughtworks Mingle (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec l’occurrence, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Thoughtworks Mingle pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de l’occurrence de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-thoughtworks-mingle-from-hello-gallery"></a>Ajout de l’occurrence de la galerie de hello
tooconfigure hello intégration de l’occurrence dans Azure AD, vous devez tooadd Thoughtworks Mingle à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Thoughtworks Mingle à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![bouton d’Azure Active Directory Hello][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![panneau des applications Enterprise Hello][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Nouveau bouton d’application Hello][3]

4. Dans la zone de recherche de hello, tapez **Thoughtworks Mingle**, sélectionnez **Thoughtworks Mingle** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.

    ![Liste des résultats de l’occurrence Bonjour](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Thoughtworks Mingle avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent de hello en l’occurrence est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello en l’occurrence doit toobe établie.

En l’occurrence, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec l’occurrence, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Créer un utilisateur test Thoughtworks Mingle](#create-a-thoughtworks-mingle-test-user)**  -toohave un équivalent de Britta Simon en l’occurrence qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configure-azure-ad-single-sign-on"></a>Configurer l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application l’occurrence.

**tooconfigure Azure AD single sign-on avec l’occurrence, effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **Thoughtworks Mingle** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_samlbase.png)

3. Sur hello **URL et le domaine de Thoughtworks Mingle** section, effectuer hello comme suit :

    ![Informations d’authentification unique dans Domaine et URL Thoughtworks Mingle](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_url.png)

    Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.mingle.thoughtworks.com`

    > [!NOTE] 
    > valeur de Hello n’est pas réelle. Valeur de hello de mise à jour avec hello URL de connexion réel. Contact [équipe de support Client de Thoughtworks Mingle](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support) valeur hello de tooget. 
 
4. Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_400.png)

6. Connectez-vous à tooyour **Thoughtworks Mingle** site d’entreprise en tant qu’administrateur.

7. Cliquez sur hello **Admin** onglet et cliquez ensuite sur **SSO Config**.
   
    ![Onglet Admin](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "Configuration SSO")

8. Bonjour **SSO Config** section, effectuer hello comme suit :
   
    ![Configuration de l’authentification unique](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "Configuration de l’authentification unique")
    
    a. fichier de métadonnées tooupload hello, cliquez sur **choisir un fichier**. 

    b. Cliquez sur **Enregistrer les modifications**.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur de test Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![bouton Ajouter de Hello](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="create-a-thoughtworks-mingle-test-user"></a>Créer un utilisateur de test Thoughtworks Mingle

Pour Azure AD les utilisateurs toobe en mesure de toosign dans, ils doivent être mis en service toohello application Thoughtworks Mingle à l’aide de leur nom d’utilisateur Azure Active Directory. Dans les cas de hello de l’occurrence, cette configuration est une tâche manuelle.

**configuration, de l’utilisateur tooconfigure effectuer hello comme suit :**

1. Ouvrez une session dans tooyour site d’entreprise Thoughtworks Mingle en tant qu’administrateur.

2. Cliquez sur **Profile**.
   
    ![Votre premier projet](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "Votre premier projet")

3. Cliquez sur hello **Admin** onglet, puis cliquez sur **utilisateurs**.
   
    ![Utilisateurs](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "Utilisateurs")

4. Cliquez sur **New User**.
   
    ![Nouvel utilisateur](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "Nouvel utilisateur")

5. Sur hello **nouvel utilisateur** boîte de dialogue de page, effectuer hello comme suit :
   
    ![Boîte de dialogue Nouvel utilisateur](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "Nouvel utilisateur")  
 
    a. Hello de type **nom de connexion**, **nom d’affichage**, **choisir un mot de passe**, **confirmer le mot de passe** d’un Azure valide compte AD tooprovision dans hello liés les zones de texte. 

    b. Dans **User type (Type d’utilisateur)**, sélectionnez **Full user (Utilisateur complet)**.

    c. Cliquez sur **Create This Profile**.

>[!NOTE]
>Vous pouvez utiliser n’importe quel autre Thoughtworks Mingle utilisateur compte outil de création ou API fournie par Thoughtworks Mingle de tooprovision des comptes d’utilisateur AAD.
> 

### <a name="assign-hello-azure-ad-test-user"></a>Affecter l’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooThoughtworks Mingle.

![Attribuer le rôle d’utilisateur hello][200] 

**tooassign Britta Simon tooThoughtworks Mingle, procédez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Thoughtworks Mingle**.

    ![lien de l’occurrence Hello dans la liste des Applications hello](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![lien de « Utilisateurs et groupes » Hello][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![volet d’ajouter l’affectation de Hello][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="test-single-sign-on"></a>Tester l’authentification unique

objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque de l’occurrence hello Bonjour volet d’accès, vous devez obtenir l’application de l’occurrence tooyour automatiquement signé sur.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_203.png

