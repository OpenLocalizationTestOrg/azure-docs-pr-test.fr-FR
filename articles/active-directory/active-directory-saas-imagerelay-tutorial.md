---
title: "Didacticiel : Intégration d’Azure Active Directory à Image Relay | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de relais de l’Image."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 65bb5990-07ef-4244-9f41-cd28fc2cb5a2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: baf39e4437b85c2de5b524984ad5ca39badbab63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-image-relay"></a>Didacticiel : Intégration d’Azure Active Directory à ImageRelay

Dans ce didacticiel, vous apprendrez comment toointegrate relais Image avec Azure Active Directory (Azure AD).

Intégration de relais d’Image avec Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooImage relais
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooImage relais (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec l’Image de relais, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Image Relay pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de relais de l’Image à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-image-relay-from-hello-gallery"></a>Ajout de relais de l’Image à partir de la galerie de hello
tooconfigure hello intégration de relais d’Image dans Azure AD, vous devez tooadd relais de l’Image à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd relais d’Image à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **Image relais**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_search.png)

5. Dans le volet de résultats hello, sélectionnez **Image relais**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Image Relay, en tirant parti d’un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans l’Image de relais est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans l’Image de relais hello doit toobe établie.

Dans l’Image de relais, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec l’Image de relais, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test de relais d’Image](#creating-an-image-relay-test-user)**  -toohave un équivalent de Britta Simon de relais d’Image qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de relais d’Image.

**tooconfigure Azure AD authentification unique avec l’Image de relais, effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **Image relais** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_samlbase.png)

3. Sur hello **domaine de relais d’Image et les URL** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_url.png)

    a. Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.imagerelay.com/`

    b. Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.imagerelay.com/sso/metadata`

    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur. Contact [équipe de support Client de relais d’Image](http://support.imagerelay.com/) tooget ces valeurs. 
 


4. Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_general_400.png)

6. Sur hello **Image relais Configuration** , cliquez sur **configurer le relais Image** tooopen **configurer l’authentification** fenêtre. Hello de copie **URL du Service de déconnexion et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_configure.png) 

7. Dans une autre fenêtre de navigateur, connectez-vous dans un site d’entreprise tooyour relais de l’Image en tant qu’administrateur.

8. Dans la barre d’outils de hello en haut de hello, cliquez sur hello **utilisateurs et autorisations** la charge de travail.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_06.png) 

9. Cliquez sur **Créer une nouvelle autorisation**.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_08.png)

10. Bonjour **Single Sign On Settings** la charge de travail, sélectionnez hello **ce groupe peut uniquement se connecter à l’aide de l’authentification unique** case à cocher, puis cliquez sur **enregistrer**.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_09.png) 

11. Accédez trop**les paramètres de compte**.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_10.png) 

12. Accédez toohello **Single Sign On Settings** la charge de travail.
    
     ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_11.png)

13. Sur hello **paramètres SAML** boîte de dialogue, effectuer hello comme suit :
    
    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_12.png)
    
    a. Dans **URL de connexion** zone de texte, valeur hello coller **-Service URL d’authentification** dont vous avez copié à partir du portail Azure.

    b. Dans **URL de déconnexion** zone de texte, valeur hello coller **URL de Service de déconnexion unique** dont vous avez copié à partir du portail Azure.

    c. Sous **Name Id Format** (Format d’ID de nom), sélectionnez **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.

    d. En tant que **les Options de liaison pour les demandes de hello fournisseur de services (Image relais)**, sélectionnez **POST liaison**.

    e. Sous **Certificat x.509**, cliquez sur **Mettre à jour le certificat**.

    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_17.png)

    f. Ouvrir le certificat de hello téléchargé dans le bloc-notes, copier le contenu de hello, puis collez-la dans la zone de texte hello x.509 certificat.

    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_18.png)

    g. Dans **juste à temps de configuration de l’utilisateur** section, sélectionnez hello **activer l’approvisionnement des utilisateurs juste à temps**.

    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_19.png)

    h. Groupe d’autorisations SELECT hello (par exemple, **base SSO**) qui n’est autorisé toosign dans via l’authentification unique.

    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_20.png)

    i. Cliquez sur **Enregistrer**.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-an-image-relay-test-user"></a>Création d’un utilisateur de test Image Relay

objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans l’Image de relais.

**toocreate un utilisateur appelé Britta Simon dans l’Image de relais, effectuez hello comme suit :**

1. Site d’entreprise tooyour authentification relais de l’Image en tant qu’administrateur.

2. Accédez trop**utilisateurs et autorisations** et sélectionnez **créer un utilisateur SSO**.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_21.png) 

3. Entrez hello **messagerie**, **prénom**, **nom**, et **société** d’utilisateur de hello souhaité tooprovision et le groupe d’autorisations select hello (par exemple, l’authentification unique de base) qui est le groupe hello qui peut se connecter via l’authentification unique.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_22.png) 

4. Cliquez sur **Créer**.

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooImage relais.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooImage relais, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Image relais**.

    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.    

Lorsque vous cliquez sur hello relais de l’Image de vignette dans hello volet d’accès, vous devez obtenir l’application d’Image relais automatiquement signé sur tooyour.


## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_04.png


[100]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_203.png

