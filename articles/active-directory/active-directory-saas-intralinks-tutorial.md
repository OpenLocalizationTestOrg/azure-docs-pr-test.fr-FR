---
title: "Didacticiel : intégration d’Azure Active Directory à Intralinks | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Intralinks."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 147f2bf9-166b-402e-adc4-4b19dd336883
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: ee7fd5b88ac806104002ffb41af11bab4fd1b2dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intralinks"></a>Didacticiel : intégration d’Azure Active Directory à Intralinks

Dans ce didacticiel, vous allez apprendre à intégrer Intralinks à Azure Active Directory (Azure AD).

L’intégration d’Intralinks à Azure AD vous offre les avantages suivants :

- Dans Azure AD, vous pouvez déterminer qui a accès à Intralinks.
- Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Intralinks (via l’authentification unique) avec leur compte Azure AD.
- Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure

Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

Pour configurer l’intégration d’Azure AD à Intralinks, vous avez besoin des éléments suivants :

- Un abonnement Azure AD
- Un abonnement Intralinks pour lequel l’authentification unique est activée

> [!NOTE]
> Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.

Vous devez en outre suivre les recommandations ci-dessous :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :

1. Ajout d’Intralinks à partir de la galerie
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-intralinks-from-the-gallery"></a>Ajout d’Intralinks à partir de la galerie
Pour configurer son intégration à Azure AD, vous devez ajouter Intralinks à votre liste d’applications SaaS gérées, à partir de la galerie.

**Pour ajouter Intralinks à partir de la galerie, procédez comme suit :**

1. Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**. 

    ![Active Directory][1]

2. Accédez à **Applications d’entreprise**. Accédez ensuite à **Toutes les applications**.

    ![Applications][2]
    
3. Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche, saisissez **Intralinks**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. Dans le volet de résultats, sélectionnez **Intralinks**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Intralinks, en tirant parti d’un utilisateur de test appelé « Britta Simon ».

Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Intralinks équivalent dans Azure AD. En d’autres termes, une relation doit être établie entre l’utilisateur Azure AD et l’utilisateur Intralinks associé.

Dans Intralinks, attribuez la valeur du **nom d’utilisateur** dans Azure AD comme valeur **Nom d’utilisateur** pour établir la relation.

Pour configurer et tester l’authentification unique Azure AD avec Intralinks, vous devez suivre les indications des sections suivantes :

1. **[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.
3. **[Création d’un utilisateur de test Intralinks](#creating-an-intralinks-test-user)** : pour avoir un équivalent de l’utilisateur Britta Simon dans Intralinks qui soit lié à la représentation de l’utilisateur Azure AD.
4. **[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.
5. **[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Intralinks.

**Pour configurer l’authentification unique Azure AD avec Intralinks, procédez comme suit :**

1. Dans le Portail Azure, sur la page d’intégration de l’application **Intralinks**, cliquez sur **Authentification unique**.

    ![Configurer l’authentification unique][4]

2. Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_samlbase.png)

3. Dans la section **Domaine et URL Intralinks**, procédez comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_url.png)

    Dans la zone de texte **URL d’authentification**, tapez une URL en utilisant le modèle suivant : `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`

    > [!NOTE] 
    > Cette valeur n’est pas la valeur réelle. Mettez à jour cette valeur avec l’URL d’authentification réelle. Contactez [l’équipe de support client Intralinks](https://www.intralinks.com/contact-1) pour obtenir cette valeur. 
 
4. Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

6. Pour configurer l’authentification unique du côté de **Intralinks**, vous devez envoyer le **XML de métadonnées** téléchargé à [l’équipe de support d’Intralinks](https://www.intralinks.com/contact-1). Celle-ci configure ensuite ce paramètre pour que la connexion SSO SAML soit définie correctement des deux côtés.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.  Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas. Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.

![Créer un utilisateur Azure AD][100]

**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**

1. Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_01.png) 

2. Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_02.png) 

3. Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_03.png) 

4. Dans la boîte de dialogue **Utilisateur**, procédez comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_04.png) 

    a. Dans la zone de texte **Nom**, entrez **BrittaSimon**.

    b. Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.

    c. Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-an-intralinks-test-user"></a>Création d’un utilisateur de test Intralinks

Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Intralinks. Collaborez avec [l’équipe du support technique Intralinks](https://www.intralinks.com/contact-1) pour ajouter des utilisateurs sur la plateforme Intralinks.

### <a name="assigning-the-azure-ad-test-user"></a>Affectation de l’utilisateur de test Azure AD

Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Intralinks.

![Affecter des utilisateurs][200] 

**Pour affecter Britta Simon à Intralinks, procédez comme suit :**

1. Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications, sélectionnez **Intralinks**.

    ![Configurer l’authentification unique](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_app.png) 

3. Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.

### <a name="add-intralinks-via-or-elite-application"></a>Ajouter une application Intralinks VIA ou Elite

Intralinks utilise la même plateforme d’identité pour l’authentification unique quelle que soit l’application Intralinks, à l’exception de Dealnexus. Par conséquent, si vous envisagez d’utiliser une autre application Intralinks, vous devez d’abord configurer l’authentification unique pour une application Intralinks principale, en suivant la procédure décrite ci-dessus.

Après cela, vous pouvez suivre la procédure ci-dessous pour ajouter une autre application Intralinks dans votre client, afin de pouvoir tirer parti de cette application principale pour l’authentification unique. 

>[!NOTE]
>Cette fonctionnalité est uniquement disponible pour les clients de la référence SKU Azure AD Premium. Les clients dotés de la SKU gratuite ou de base du logiciel ne peuvent pas l’utiliser.

1. Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**. 

    ![Active Directory][1]


2. Accédez à **Applications d’entreprise**. Accédez ensuite à **Toutes les applications**.

    ![Applications][2]
    
3. Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche, saisissez **Intralinks**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. Sur **l’application Ajout Intralinks** procédez comme suit :

    ![Ajout d’une application Intralinks VIA ou Elite](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addapp.png)

    a. Dans la zone de texte **Nom**, entrez un nom de l’application approprié, par exemple **Intralinks Elite**.

    b. Cliquez sur le bouton **Ajouter**.

6.  Dans le Portail Azure, sur la page d’intégration de l’application **Intralinks**, cliquez sur **Authentification unique**.

    ![Configurer l’authentification unique][4]

7. Dans la boîte de dialogue **Authentification unique**, sélectionnez **Mode** en tant que **Authentification liée**.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_linkedsignon.png)

8. Récupérez l’URL d’authentification unique initiée par le fournisseur de services depuis [l’équipe Intralinks](https://www.intralinks.com/contact-1) pour l’autre application Intralinks. Saisissez l’URL ainsi obtenue dans **Configurer l’URL d’authentification** comme indiqué ci-dessous. 
    
     ![Configurer l’authentification unique](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_customappurl.png)
    
     Dans la zone de texte URL de connexion, saisissez l’URL utilisée par les utilisateurs pour se connecter à votre application Intralinks en utilisant le modèle suivant :
   
    `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`

9. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

10. Affectez l’application à un utilisateur ou à un groupe, comme l’indique la section **[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)**.

### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.

Lorsque vous cliquez sur la vignette Intralinks dans le volet d’accès, vous devez être connecté automatiquement à votre application Intralinks.
Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_203.png

