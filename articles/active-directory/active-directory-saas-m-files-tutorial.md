---
title: "Didacticiel : Intégration d’Azure Active Directory dans M-Files | Documentation Microsoft"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et des millions de fichiers."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4536fd49-3a65-4cff-9620-860904f726d0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: e1d268da53312b1d2c12e29d66b1a5b66d0cdcce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-m-files"></a>Didacticiel : Intégration d’Azure AD à M-Files

Dans ce didacticiel, vous apprendrez comment toointegrate millions de fichiers avec Azure Active Directory (Azure AD).

Intégration des millions de fichiers avec Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès aux fichiers tooM
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooM-fichiers (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec des millions de fichiers, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement à M-Files pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout des millions de fichiers à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-m-files-from-hello-gallery"></a>Ajout des millions de fichiers à partir de la galerie de hello
tooconfigure hello intégration des millions de fichiers dans Azure AD, vous devez tooadd millions de fichiers à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd millions de fichiers à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **millions de fichiers**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_search.png)

5. Dans le volet de résultats hello, sélectionnez **millions de fichiers**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec M-Files avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans les fichiers de M est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et l’utilisateur dans les fichiers de M hello doit toobe établie.

Dans les fichiers-M, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec des millions de fichiers, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test de millions de fichiers](#creating-a-m-files-test-user)**  -toohave un équivalent de Britta Simon dans des millions de fichiers qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de millions de fichiers.

**tooconfigure Azure AD authentification unique avec des millions de fichiers, effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **millions de fichiers** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_samlbase.png)

3. Sur hello **domaine des millions de fichiers et les URL** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_url.png)

    a. Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`

    b. Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<tenantname>.cloudvault.m-files.com`

    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur. Contact [équipe de support Client de millions de fichiers](mailto:support@m-files.com) tooget ces valeurs. 
 
4. Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-m-files-tutorial/tutorial_general_400.png)

6. tooget l’authentification unique configurée pour votre application, contactez [équipe de support des millions de fichiers](mailto:support@m-files.com) et les fournir hello téléchargé les métadonnées.
   
    >[!NOTE]
    >Suivez les instructions hello si vous souhaitez tooconfigure SSO pour vous, application de bureau M de fichier. Aucune étape supplémentaire est requise si vous souhaitez uniquement tooconfigure l’authentification unique pour la version web de millions de fichiers.  

7. Suivez hello suivant étapes tooconfigure hello M-fichier application de bureau tooenable SSO avec AD Azure. toodownload millions de fichiers, accédez trop[millions de fichiers téléchargement](https://www.m-files.com/en/download-latest-version) page.

8. Ouvrez hello **paramètres du bureau millions de fichiers** fenêtre. Cliquez ensuite sur **Ajouter**.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_10.png)

9. Sur hello **propriétés de connexion de coffre Document** fenêtre, effectuez hello comme suit :
   
    ![Configurer l’authentification unique](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_11.png)  

    Sous type de serveur de section de hello, hello valeurs comme suit :  

    a. Pour **Nom**, saisissez `<tenant-name>.cloudvault.m-files.com`. 
 
    b. Pour **Numéro de port**, saisissez **4466**. 

    c. Pour **Protocole**, sélectionnez **HTTPS**. 

    d. Bonjour **authentification** champ, sélectionnez **utilisateur Windows spécifique**. Ensuite, une page de signature s’affiche. Entrez vos informations d’identification Azure AD. 

    e. Pourquoi **coffre sur serveur**, sélectionnez hello coffre correspondant sur le serveur.
 
    f. Cliquez sur **OK**.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-m-files-test-user"></a>Création d’un utilisateur de test M-Files

objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans les fichiers de M. Travailler avec [équipe de support des millions de fichiers](mailto:support@m-files.com) utilisateurs hello tooadd hello millions de fichiers.

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès aux fichiers tooM.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooM-Files, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **millions de fichiers**.

    ![Configurer l’authentification unique](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur hello millions de fichiers vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour millions de fichiers application.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_203.png

