---
title: "Didacticiel : Intégration d’Azure Active Directory à SAP HANA Cloud Platform Identity Authentication | Microsoft Docs"
description: "Découvrez comment tooconfigure sur l’authentification unique entre Azure Active Directory et SAP HANA Cloud Platform Identity authentification."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c1320d1-7ba4-4b5f-926f-4996b44d9b5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 2142770779ddb745555b47fc85b5457b573f9506
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform-identity-authentication"></a>Didacticiel : Intégration d’Azure Active Directory à SAP HANA Cloud Platform Identity Authentication

Dans ce didacticiel, vous apprendrez comment toointegrate SAP HANA Cloud Platform Identity authentification avec Azure Active Directory (Azure AD). Authentification d’identité SAP HANA Cloud Platform est utilisée comme un proxy IdP tooaccess SAP les applications à l’aide d’Azure AD comme hello IdP principal.

Intégration d’authentification d’identité SAP HANA Cloud Platform à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooSAP application
- Vous pouvez activer vos utilisateurs tooautomatically get tooSAP signé sur applications-session unique (SSO) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure classic

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).


## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec l’authentification d’identité SAP HANA Cloud Platform, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement **SAP HANA Cloud Platform Identity Authentication** compatible avec l’authentification unique


>[!NOTE] 
>tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.
>

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.

scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout d’authentification d’identité plateforme Cloud SAP HANA à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

Avant de plonger dans les détails techniques hello, il est concepts de hello toounderstand vital que vous allez toolook à. Hello fédération d’authentification d’identité SAP HANA Cloud Platform et Azure Active Directory vous permet de tooimplement l’authentification unique entre les applications ou services protégés par AAD (comme un IdP) avec les applications SAP et les services protégés par identité de plateforme Cloud SAP HANA Authentification.

Actuellement, l’authentification de SAP HANA Cloud Platform Identity agit comme un fournisseur d’identité Proxy tooSAP-applications. Azure Active Directory joue à son tour hello début du fournisseur d’identité dans ce programme d’installation. 

Hello suivant le diagramme illustre ce comportement :    

![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/architecture-01.png)

Avec cette configuration, votre client SAP HANA Cloud Platform Identity Authentication sera configuré en tant qu’application approuvée dans Azure Active Directory. 

Toutes les applications SAP et les services souhaités tooprotect par le biais de cette manière sont configurés par la suite dans la console de gestion de l’authentification de SAP HANA Cloud Platform Identity hello !

Cela signifie que cette autorisation pour accorder l’accès tooSAP applications et services tootake de besoins sur place de l’authentification d’identité SAP HANA Cloud Platform pour ce type de configuration (comme autorisation tooconfiguring exécutée dans Azure Active Directory).

En configurant l’authentification d’identité plateforme Cloud SAP HANA en tant qu’application via hello Azure Active Directory Marketplace, vous n’avez pas besoin tootake administration de la configuration des revendications individuelles nécessaires / assertions SAML et les transformations nécessaires tooproduce un jeton d’authentification valide pour les applications SAP.

>[!NOTE] 
>Actuellement, l’authentification unique web n’a été testée que par les deux parties. Les flux nécessaires à la communication application-API ou API-API devraient fonctionner mais n’ont pas encore été testés. Ils seront testés dans le cadre des activités à venir.
>

## <a name="add-sap-hana-cloud-platform-identity-authentication-from-hello-gallery"></a>Ajouter l’authentification d’identité plateforme Cloud SAP HANA à partir de la galerie de hello
intégration de hello tooconfigure d’authentification d’identité plateforme Cloud SAP HANA dans Azure AD, vous devez tooadd authentification d’identité plateforme Cloud SAP HANA à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd SAP HANA Cloud Platform authentification de l’identité à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour [ **portail de gestion Azure**](https://portal.azure.com)sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. Cliquez sur **ajouter** bouton en haut de hello de boîte de dialogue hello.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **authentification d’identité SAP HANA Cloud Platform**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_01.png)

5. Dans le volet de résultats hello, sélectionnez **authentification d’identité SAP HANA Cloud Platform**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_02.png)


##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec SAP HANA Cloud Platform Identity Authentication, à partir d’un utilisateur de test appelé « Britta Simon ».

Pour l’authentification unique toowork, Azure AD doit tooknow quel utilisateur d’équivalent hello dans l’authentification de SAP HANA Cloud Platform Identity est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur de l’authentification d’identité SAP HANA Cloud Platform hello doit toobe établie.

Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans l’authentification d’identité SAP HANA Cloud Platform.

tooconfigure et l’authentification unique d’Azure AD avec l’authentification d’identité SAP HANA Cloud Platform de test, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD l’authentification unique sur](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test de l’authentification de SAP HANA Cloud Platform Identity](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)**  -toohave de Britta Simon dans SAP HANA Cloud Platform authentification d’identité qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-sso"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez l’authentification unique de Azure AD dans le portail de gestion Azure hello et configurez l’authentification unique dans votre application d’authentification d’identité SAP HANA Cloud Platform.

Application d’authentification d’identité SAP HANA Cloud Platform attend les assertions SAML hello dans un format spécifique. Vous pouvez gérer les valeurs de ces attributs hello depuis hello »**attributs utilisateur**« section sur la page d’intégration d’application. Hello suivant capture d’écran montre un exemple de cela.

![Configurer l’authentification unique](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_03.png)

**tooconfigure l’authentification unique d’Azure AD avec l’authentification SAP HANA Cloud Platform Identity, effectuez hello comme suit :**

1. Dans le portail de gestion Azure hello, sur hello **authentification d’identité SAP HANA Cloud Platform** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, en tant que **Mode** sélectionnez **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique][5]

3. Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, si votre application SAP attend un attribut, par exemple « firstName ». Boîte de dialogue hello SAML attributs du jeton, ajoutez l’attribut de « firstName » de hello.
 1. Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.
 
    ![Configurer l’authentification unique][6]

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_05.png)
 2. Bonjour **nom de l’attribut** textbox, le nom « firstName » de l’attribut de type hello.
 3. À partir de hello **valeur d’attribut** liste, la valeur d’attribut hello Sélectionnez « user.givenname ».
 4. Cliquez sur **OK**.

4. Sur hello **URL et le domaine d’authentification de l’identité SAP HANA Cloud Platform** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_06.png)
 1. Bonjour **URL de connexion** zone de texte, tapez le signe de hello sur l’URL pour l’application de SAP hello.
 2. Bonjour **identificateur** zone de texte, valeur hello de type modèle :`<entity-id>.accounts.ondemand.com` 
    * Si vous ne connaissez pas cette valeur, veuillez suivre documentation d’authentification d’identité SAP HANA Cloud Platform hello sur [locataire SAML 2.0 Configuration](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).

5. Sur hello **Configuration de l’authentification SAP HANA Cloud Platform Identity** , cliquez sur **configuration SAP HANA Cloud Platform identité de l’authentification** tooopen **configurer l’authentification** boîte de dialogue. Ensuite, cliquez sur **des métadonnées XML SAML** et enregistrez le fichier hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_07.png) 

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_08.png)

6. tooget SSO configuré pour votre application, accédez tooSAP HANA Cloud Platform Identity authentification Console d’Administration. URL de Hello a hello modèle :`https://<tenant-id>.accounts.ondemand.com/admin`
 * Ensuite, suivez les documentation hello sur SAP HANA Cloud Platform Identity authentification trop[configurer Microsoft Azure AD en tant que fournisseur d’identité d’entreprise au niveau d’authentification d’identité SAP HANA Cloud Platform](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html). 

7. Dans le portail de gestion Azure hello, cliquez sur **enregistrer** bouton.
8. Continuer hello suit uniquement si vous souhaitez tooadd et activez l’authentification unique pour une autre application SAP. Répétez les étapes sous hello section « Ajout SAP HANA Cloud Platform authentification d’identité à partir de la galerie de hello » tooadd une autre instance de l’authentification d’identité SAP HANA Cloud Platform.
9. Dans le portail de gestion Azure hello, sur hello **authentification d’identité SAP HANA Cloud Platform** page d’intégration d’application, cliquez sur **lié Sign-on**.

    ![Configurer l’authentification liée](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/linked_sign_on.png)
10. Puis, enregistrez hello configuration.

>[!NOTE] 
>nouvelle application de Hello reposera sur configuration de SSO hello pour l’application SAP précédente hello. Vérifiez que vous utilisez hello même fournisseurs d’identité d’entreprise dans la Console Administration de l’authentification de la plateforme Cloud SAP HANA identité de hello.
>

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD
objectif Hello de cette section est hello nouveau portail appelé Britta Simon toocreate un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail de gestion Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_01.png) 

2. Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_02.png) 

3. En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_04.png) 
  1. Bonjour **nom** zone de texte, type **BrittaSimon**.
  2. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.
  3. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.
  4. Cliquez sur **Créer**. 

### <a name="create-a-sap-hana-cloud-platform-identity-authentication-test-user"></a>Créer un utilisateur de test SAP HANA Cloud Platform Identity Authentication

Vous n’avez pas besoin toocreate un utilisateur sur l’authentification d’identité SAP HANA Cloud Platform. Les utilisateurs qui se trouvent dans le magasin de l’utilisateur hello Azure AD peuvent utiliser la fonctionnalité SSO de hello.

Authentification d’identité SAP HANA Cloud Platform prend en charge l’option de fédération des identités hello. Cette option permet de hello application toocheck si les utilisateurs de hello authentifiés par le fournisseur d’identité d’entreprise hello existent dans hello utilisateur magasin de SAP HANA Cloud Platform authentification d’identité. 

Dans le paramètre par défaut de hello, hello option de fédération d’identité est désactivé. Si la fédération des identités est activée, seuls les utilisateurs hello qui sont importés dans l’authentification d’identité SAP HANA Cloud Platform sont hello à tooaccess en mesure de l’application. 

Pour plus d’informations sur comment tooenable ou désactiver la fédération d’identité avec l’authentification SAP HANA Cloud Platform Identity, consultez Activer la fédération d’identité avec l’authentification SAP HANA Cloud Platform Identity dans [configurer la fédération d’identité avec hello utilisateur magasin de SAP HANA Cloud Platform authentification d’identité. ](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).

### <a name="assign-hello-azure-ad-test-user"></a>Affecter l’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant son tooSAP accès authentification d’identité HANA Cloud Platform.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooSAP authentification d’identité HANA Cloud Platform, procédez hello comme suit :**

1. Dans le portail de gestion Azure hello, ouvrez la vue des applications hello, puis naviguez toohello les vue de répertoire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **authentification d’identité SAP HANA Cloud Platform**.

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_09.png)

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    

### <a name="test-single-sign-on"></a>Tester l’authentification unique

Dans cette section, vous tester votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque d’authentification d’identité SAP HANA Cloud Platform hello Bonjour volet d’accès, vous devez obtenir l’application d’authentification d’identité SAP HANA Cloud Platform automatiquement signé sur tooyour.


## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_06.png

[100]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_203.png