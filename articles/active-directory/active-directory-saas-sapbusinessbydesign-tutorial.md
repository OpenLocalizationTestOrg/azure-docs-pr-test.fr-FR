---
title: "Didacticiel : intégration d’Azure Active Directory à SAP Business ByDesign | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et SAP Business ByDesign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 82938920-33ba-47cb-b141-511b46d19e66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: c14714fd27f8d7fc555f25c7be83fad2b0d7f333
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-bydesign"></a>Didacticiel : Intégration d’Azure Active Directory à SAP Business ByDesign

Dans ce didacticiel, vous apprendrez comment toointegrate SAP ByDesign d’entreprise avec Azure Active Directory (Azure AD).

Intégration de SAP Business ByDesign avec Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooSAP ByDesign de l’entreprise.
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSAP ByDesign entreprise (SSO) avec leurs comptes Azure AD.
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec SAP Business ByDesign, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement SAP Business ByDesign pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de SAP Business ByDesign à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-sap-business-bydesign-from-hello-gallery"></a>Ajout de SAP Business ByDesign à partir de la galerie de hello
tooconfigure hello intégration de SAP Business ByDesign dans Azure AD, vous devez tooadd SAP Business ByDesign à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd ByDesign d’entreprise SAP à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![bouton d’Azure Active Directory Hello][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![panneau des applications Enterprise Hello][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Nouveau bouton d’application Hello][3]

4. Dans la zone de recherche de hello, tapez **SAP Business ByDesign**, sélectionnez **SAP Business ByDesign** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.

    ![ByDesign d’entreprise SAP dans la liste des résultats hello](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD

Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec SAP Business ByDesign, en tirant parti d’un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans SAP Business ByDesign est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans SAP Business ByDesign doit toobe établie.

Dans SAP Business ByDesign, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec SAP Business ByDesign, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Créer un utilisateur de test SAP Business ByDesign](#create-an-sap-business-bydesign-test-user)**  -toohave un équivalent de Britta Simon dans SAP Business ByDesign qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configure-azure-ad-single-sign-on"></a>Configurer l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application SAP Business ByDesign.

**tooconfigure Azure AD l’authentification unique avec SAP Business ByDesign, effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **SAP Business ByDesign** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Lien Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_samlbase.png)

3. Sur hello **URL et le domaine de SAP Business ByDesign** section, effectuer hello comme suit :

    ![Informations d’authentification unique dans la section Domaine et URL SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_url.png)

    a. Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<servername>.sapbydesign.com`

    b. Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<servername>.sapbydesign.com`

    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur. Contact [équipe de support SAP Business ByDesign Client](https://www.sap.com/products/cloud-analytics.support.html) tooget ces valeurs.

4. Sur hello **attributs utilisateur** section, effectuer hello comme suit :

    ![Section d’attribut de SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_attribute.png)
    
    a. Dans **identificateur de l’utilisateur** liste, sélectionnez hello **ExtractMailPrefix()** (fonction).
    
    b. À partir de hello **Mail** liste, sélectionnez hello utilisateur attribut toouse pour votre implémentation. Par exemple, si vous voulez toouse hello EmployeeID comme identificateur d’utilisateur unique et si vous avez stocké la valeur de l’attribut hello Bonjour ExtensionAttribute2, puis sélectionnez user.extensionattribute2.   

5. Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_certificate.png) 

6. Cliquez sur le bouton **Enregistrer** .

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_400.png)

7. Sur hello **SAP Business ByDesign Configuration** , cliquez sur **configurer de SAP Business ByDesign** tooopen **configurer l’authentification** fenêtre. Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configuration de SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_configure.png) 

8. tooget SSO configuré pour votre application, effectuez hello comme suit :
   
    a. Se connecter sur le portail SAP Business ByDesign tooyour avec des droits d’administrateur.
   
    b. Accédez trop**Application et la tâche courante de gestion utilisateur** et cliquez sur hello **fournisseur d’identité** onglet.
   
    c. Cliquez sur **nouveau fournisseur d’identité** et le fichier XML de métadonnées hello select que vous avez téléchargé à partir de hello portail Azure. En important des métadonnées de hello, système de hello télécharge automatiquement le certificat de signature requis hello et certificat de chiffrement.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_54.png)
   
    d. tooinclude hello **Assertion Consumer Service URL** dans la demande SAML hello, sélectionnez **inclure l’URL Assertion Consumer Service**.
   
    e. Cliquez sur **Activate Single Sign-On**(Activer l’authentification unique).
   
    f. Enregistrez vos modifications.
   
    g. Cliquez sur hello **mon système** onglet.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_52.png)
   
    h. Coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir de hello portail Azure il dans hello **Azure AD l’URL de connexion** zone de texte.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_53.png)
   
    i. Spécifier si les employés hello peuvent manuellement choisir entre l’ouverture de session avec l’ID d’utilisateur et mot de passe ou l’authentification unique en sélectionnant **sélection de fournisseur d’identité manuelle**.
   
    j. Bonjour **URL SSO** section, spécifier des URL hello qui doit être utilisée par le système de toohello toologon hello employé. 
    Dans la liste de déroulante tooEmployee URL envoyée hello, vous pouvez choisir entre hello options suivantes :
   
    **Non-SSO URL**
   
    système de Hello envoie employé toohello hello uniquement des URL de normal du système. employé de Hello ne peut pas se connecter à l’aide de l’authentification unique et doit utiliser le mot de passe ou de certificats à la place.
   
    **URL SSO** 
   
    système de Hello envoie uniquement les employés de toohello URL SSO hello. les employés Hello peuvent se connecter à l’aide de l’authentification unique. Demande d’authentification est redirigée via hello IdP.
   
    **Sélection automatique**
   
    Si l’authentification unique n’est pas actif, système de hello envoie employé de toohello URL hello normal du système. Si l’authentification unique est actif, système de hello vérifie si les employés hello a un mot de passe. Si un mot de passe est disponible, les URL d’authentification unique et Non-SSO URL sont envoyées toohello employé. Toutefois, si l’employé de hello n’a aucun mot de passe, uniquement hello URL d’authentification unique est envoyé toohello employé.
   
    k. Enregistrez vos modifications.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD

objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

   ![Créer un utilisateur de test Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_01.png)

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_02.png)

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.

    ![bouton Ajouter de Hello](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_03.png)

4. Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_04.png)

    a. Bonjour **nom** , tapez **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.

    c. Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.

    d. Cliquez sur **Create**.
 
### <a name="create-an-sap-business-bydesign-test-user"></a>Créer un utilisateur de test pour SAP Business ByDesign

Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans SAP Business ByDesign. Collaborez avec [équipe de support SAP Business ByDesign Client](https://www.sap.com/products/cloud-analytics.support.html) tooadd les utilisateurs de hello dans la plateforme de SAP Business ByDesign hello. 

> [!NOTE]
> Assurez-vous que NameID valeur doit correspondre au champ de nom d’utilisateur hello dans la plateforme de SAP Business ByDesign hello.

### <a name="assign-hello-azure-ad-test-user"></a>Affecter l’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooSAP ByDesign de l’entreprise.

![Attribuer le rôle d’utilisateur hello][200] 

**tooassign Britta Simon tooSAP ByDesign de l’entreprise, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **SAP Business ByDesign**.

    ![lien de SAP Business ByDesign Hello dans la liste des Applications hello](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_app.png)  

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![lien de « Utilisateurs et groupes » Hello][202]

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![volet d’ajouter l’affectation de Hello][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="test-single-sign-on"></a>Tester l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque de SAP Business ByDesign hello Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour SAP Business ByDesign application.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_203.png

