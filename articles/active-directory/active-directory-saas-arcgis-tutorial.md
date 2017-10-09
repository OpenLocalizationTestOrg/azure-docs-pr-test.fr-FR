---
title: "Didacticiel : Intégration d’Azure Active Directory à ArcGIS Online | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de ArcGIS en ligne."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9e132a4-29e7-48bf-beb9-4148e617c8a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: f3dd55d798cf3256fb2758e011f33946baa405ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-arcgis-online"></a>Didacticiel : Intégration d’Azure Active Directory à ArcGIS Online

Dans ce didacticiel, vous apprendrez comment toointegrate ArcGIS en ligne avec Azure Active Directory (Azure AD).

Intégration de ArcGIS en ligne auprès d’Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooArcGIS en ligne
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooArcGIS en ligne (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

<!--## Overview

tooenable single sign-on with ArcGIS Online, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in ArcGIS Online.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec ArcGIS en ligne, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement ArcGIS Online pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de ArcGIS en ligne à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-arcgis-online-from-hello-gallery"></a>Ajout de ArcGIS en ligne à partir de la galerie de hello
intégration de hello tooconfigure de ArcGIS en ligne dans Azure AD, vous devez tooadd ArcGIS en ligne à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd ArcGIS en ligne à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. Cliquez sur **nouvelle application** bouton en haut de hello de nouvelle application hello dialogue tooadd.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **ArcGIS en ligne**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_search.png)

5. Dans le volet de résultats hello, sélectionnez **ArcGIS en ligne**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec ArcGIS Online sur un utilisateur de test nommé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans ArcGIS en ligne est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans ArcGIS en ligne doit toobe établie.

Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans ArcGIS en ligne.

tooconfigure et test Azure AD l’authentification unique avec ArcGIS en ligne, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test en ligne de ArcGIS](#creating-an-arcgis-online-test-user)**  -toohave un équivalent de Britta Simon dans ArcGIS en ligne qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application en ligne de ArcGIS.

**tooconfigure Azure AD l’authentification unique sur ArcGIS Online, effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **ArcGIS en ligne** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_samlbase.png)

3. Sur hello **URL et domaine en ligne de ArcGIS** section, effectuer hello suivant l’étape :

    ![Configurer l’authentification unique](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_url.png)

    Bonjour **URL de connexion** zone de texte, valeur hello de type hello suivant le modèle à l’aide de :`https://<company>.maps.arcgis.com`

    > [!NOTE] 
    > Cette valeur n’est pas hello réel. Mettre à jour de cette valeur avec hello URL de connexion réel. Contact [équipe de support Client en ligne de ArcGIS](http://support.esri.com/) tooget cette valeur. 

4. Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier XML de hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-arcgis-tutorial/tutorial_general_400.png)

6. Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise ArcGIS en tant qu’administrateur.

7. Cliquez sur **Edit Settings** (Modifier les paramètres).

    ![Modifier les paramètres](./media/active-directory-saas-arcgis-tutorial/ic784742.png "Modifier les paramètres")

8. Cliquez sur **Sécurité**.

    ![Sécurité](./media/active-directory-saas-arcgis-tutorial/ic784743.png "Sécurité")

9. Sous **Enterprise Logins** (Informations de connexion entreprise), cliquez sur **Set Identity Provider** (Définir un fournisseur d’identité).

    ![Connexions de l’entreprise](./media/active-directory-saas-arcgis-tutorial/ic784744.png "Connexions de l’entreprise")

10. Sur hello **définir le fournisseur d’identité** configuration page, effectuer hello comme suit :
   
    ![Définir le fournisseur d’identité](./media/active-directory-saas-arcgis-tutorial/ic784745.png "Définir le fournisseur d’identité")
   
    a. Bonjour **nom** zone de texte, tapez le nom de votre organisation.

    b. Pour **métadonnées pour hello fournisseur d’identité d’entreprise sont fournies à l’aide de**, sélectionnez **un fichier**.

    c. tooupload votre fichier de métadonnées téléchargé, cliquez sur **choisir un fichier**.

    d. Cliquez sur **Set Identity Provider** (Définir un fournisseur d’identité).

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_01.png) 

2. Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_02.png) 

3. En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de Britta Simon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-an-arcgis-online-test-user"></a>Création d’un utilisateur de test ArcGIS Online

Dans l’ordre tooenable Azure AD les utilisateurs toolog dans ArcGIS en ligne, vous devez les configurer dans ArcGIS en ligne.  
Dans les cas de hello de ArcGIS en ligne, cette configuration est une tâche manuelle.

**tooprovision un compte d’utilisateur, effectuez hello comme suit :**

1. Connectez-vous à tooyour **ArcGIS** client.

2. Cliquez sur **Invite Members** (Inviter des membres).
   
    ![Inviter des membres](./media/active-directory-saas-arcgis-tutorial/ic784747.png "Inviter des membres")

3. Sélectionnez **Add members automatically without sending an email** (Ajouter des membres automatiquement sans envoyer d’e-mail), puis cliquez sur **Next** (Suivant).
   
    ![Ajouter des membres automatiquement](./media/active-directory-saas-arcgis-tutorial/ic784748.png "Ajouter des membres automatiquement")

4. Sur hello **membres** boîte de dialogue de page, effectuer hello comme suit :
   
     ![Ajouter et vérifier](./media/active-directory-saas-arcgis-tutorial/ic784749.png "Ajouter et vérifier")
    
     a. Entrez hello **messagerie**, **prénom**, et **nom** d’un compte AAD valide que vous souhaitez tooprovision.
  
     b. Cliquez sur **Add And Review** (Ajouter et vérifier).
5. Passez en revue les données hello vous avez entrées, puis cliquez sur **ajouter des membres**.
   
    ![Ajouter un membre](./media/active-directory-saas-arcgis-tutorial/ic784750.png "Ajouter un membre")
        
    > [!NOTE]
    > titulaire du compte Azure Active Directory Hello sera reçoivent un e-mail et suivez les leur compte d’un tooconfirm lien avant son activation.

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant tooArcGIS accès en ligne.

![Affecter des utilisateurs][200] 

**tooassign tooArcGIS Britta Simon en ligne, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **ArcGIS en ligne**.

    ![Configurer l’authentification unique](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque ArcGIS en ligne hello hello volet d’accès, vous devez obtenir tooyour automatiquement signé sur des applications ArcGIS en ligne.
Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_203.png

