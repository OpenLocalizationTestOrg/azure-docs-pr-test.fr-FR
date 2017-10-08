---
title: "Didacticiel : Intégration d’Azure Active Directory avec DocuSign | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de DocuSign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a691288b-84c1-40fb-84bd-5b06878865f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: e4ef40b8f5af20d811d8d806d2bd7e2039c55052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-docusign"></a>Didacticiel : Intégration d’Azure Active Directory avec DocuSign

Dans ce didacticiel, vous apprendrez comment toointegrate DocuSign avec Azure Active Directory (Azure AD).

Intégration de DocuSign à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooDocuSign
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooDocuSign (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD à DocuSign, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement DocuSign pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de DocuSign à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-docusign-from-hello-gallery"></a>Ajout de DocuSign à partir de la galerie de hello
intégration de hello tooconfigure de DocuSign dans Azure AD, vous devez tooadd DocuSign à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd DocuSign à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. Cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue hello.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **DocuSign**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_search.png)

5. Dans le volet de résultats hello, sélectionnez **DocuSign**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec DocuSign, avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans DocuSign est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans DocuSign doit toobe établie.

Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans DocuSign.

tooconfigure et test Azure AD l’authentification unique à DocuSign, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test DocuSign](#creating-a-docusign-test-user)**  -toohave un équivalent de Britta Simon dans DocuSign est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de DocuSign.

**tooconfigure Azure AD single sign-on avec DocuSign, procédez hello comme suit :**

1. Bonjour portail Azure, sur hello **DocuSign** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_samlbase.png)

3. Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base 64)** , puis enregistrez le fichier de certificat sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_certificate.png) 

4. Sur hello **DocuSign Configuration** section du portail Azure, cliquez sur **DocuSign de configuration** tooopen configurer l’authentification sur fenêtre. Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**
    
    ![Configurer l’authentification unique](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_configure.png)

5. Dans une fenêtre de navigateur web, connexion tooyour **portail d’administration DocuSign** en tant qu’administrateur.

6. Dans le menu de navigation hello hello gauche, cliquez sur **domaines**.
   
    ![Configuration de l'authentification unique][51]

7. Dans le volet droit de hello, cliquez sur **revendication domaine**.
   
    ![Configuration de l'authentification unique][52]

8. Sur hello **revendication d’un domaine** boîte de dialogue, Bonjour **nom de domaine** zone de texte, tapez le domaine de votre entreprise, puis cliquez sur **revendication**. Assurez-vous que vous vérifiez le domaine de hello et hello état est actif.
   
    ![Configuration de l'authentification unique][53]

9. Dans le menu hello situé à gauche, cliquez sur **fournisseurs d’identité**  
   
    ![Configuration de l'authentification unique][54]
10. Dans le volet droit de hello, cliquez sur **ajouter un fournisseur d’identité**. 
   
    ![Configuration de l'authentification unique][55]

11. Sur hello **paramètres de fournisseur d’identité** page, effectuer hello comme suit :
   
    ![Configuration de l'authentification unique][56]

    a. Bonjour **nom** zone de texte, tapez un nom unique pour votre configuration. N’utilisez pas d’espaces.

    b. Coller **ID d’entité SAML** dans hello **émetteur de fournisseur d’identité** zone de texte.

    c. Coller **SAML Sign-On URL du Service unique** dans hello **Identity Provider Login URL** zone de texte.

    d. Coller **URL de déconnexion** dans hello **Identity Provider Logout URL** zone de texte.

    e. Sélectionnez **Sign AuthN Request**(Signer la demande d’authentification).

    f. Sous **Send AuthN request by** (Envoyer la demande d’authentification par), sélectionnez **POST**.

    g. Sous **Send logout request by** (Envoyer la demande de déconnexion par), sélectionnez **GET**.

12. Bonjour **un mappage d’attribut personnalisé** , choisissez le champ de hello souhaité toomap avec Azure AD revendication. Dans cet exemple, hello **emailaddress** revendication est mappée avec la valeur hello **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**. Il est le nom de la revendication hello par défaut à partir d’Azure AD pour une revendication de courrier électronique. 
   
    > [!NOTE]
    > Hello utilisation appropriée **identificateur de l’utilisateur** utilisateur de hello toomap du mappage d’utilisateur Azure AD tooDocuSign. Sélectionnez hello champ approprié et entrez la valeur appropriée de hello en fonction des paramètres de votre organisation.
          
    ![Configuration de l'authentification unique][57]

13. Bonjour **certificat de fournisseur d’identité** , cliquez sur **ajouter un certificat**, puis téléchargez le certificat hello que vous avez téléchargé à partir du portail Azure AD.   
   
    ![Configuration de l'authentification unique][58]

14. Cliquez sur **Enregistrer**.

15. Bonjour **fournisseurs d’identité** , cliquez sur **Actions**, puis cliquez sur **points de terminaison**.   
   
    ![Configuration de l'authentification unique][59]
 
16. Bonjour **2.0 points de terminaison SAML** section **portail d’administration DocuSign**, effectuer hello comme suit :
   
    ![Configuration de l'authentification unique][60]
   
    a. Hello de copie **URL de l’émetteur de fournisseur de Service**, puis collez dans hello **identificateur** zone de texte sur **DocuSign domaine et les URL** section Hello hello suivant de portail Azure modèle : `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.
   
    b. Hello de copie **Service Provider Login URL**, puis collez dans hello **URL de connexion** zone de texte sur **DocuSign domaine et les URL** section Hello hello suivant de portail Azure modèle : `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.

    ![Configurer l’authentification unique](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_url.png)
      
    c.  Cliquez sur **Fermer**
    
17. Dans hello portail Azure, cliquez sur **enregistrer**.
    
    ![Configurer l’authentification unique](./media/active-directory-saas-docusign-tutorial/tutorial_general_400.png)

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_02.png) 

3. En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-docusign-test-user"></a>Création d’un utilisateur de test DocuSign

Prend en charge de l’application **juste à temps l’approvisionnement des utilisateurs** et une fois que les utilisateurs de l’authentification sont créés automatiquement dans l’application hello.

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant tooDocuSign de son accès.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooDocuSign, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **DocuSign**.

    ![Configurer l’authentification unique](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque DocuSign hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour DocuSign application.
Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)
* [Configurer l’approvisionnement de l’utilisateur](active-directory-saas-docusign-provisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_04.png
[51]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_21.png
[52]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_22.png
[53]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_23.png
[54]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_19.png
[55]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_20.png
[56]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_24.png
[57]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_25.png
[58]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_26.png
[59]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_27.png
[60]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_28.png
[61]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_29.png
[100]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_203.png

