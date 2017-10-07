---
title: "Didacticiel : Intégration d’Azure Active Directory à SAP Cloud pour le client | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Cloud de SAP pour le client."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 90154dab-eba2-4563-bcf0-f2acc797ea97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 0525ea81122458ab3ac24a5bdb0b5f628405dd05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-cloud-for-customer"></a>Didacticiel : Intégration d’Azure Active Directory avec SAP Cloud pour le client

Dans ce didacticiel, vous apprendrez comment toointegrate SAP Cloud pour le client avec Azure Active Directory (Azure AD).

Intégration de Cloud de SAP pour le client auprès d’Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooSAP Cloud pour le client
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSAP Cloud pour le client (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec SAP Cloud pour le client, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement SAP Cloud for Customer pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois ici : [offre d’essai](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de Cloud de SAP pour le client à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-sap-cloud-for-customer-from-hello-gallery"></a>Ajout de Cloud de SAP pour le client à partir de la galerie de hello
tooconfigure hello intégration de Cloud de SAP pour le client dans Azure AD, vous devez tooadd SAP Cloud pour le client à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Cloud SAP pour le client à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **Cloud SAP pour le client**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_search.png)

5. Dans le volet de résultats hello, sélectionnez **Cloud SAP pour le client**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec SAP Cloud pour le client, en tirant parti d’un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans le Cloud de SAP pour le client est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans le Cloud de SAP pour le client doit toobe établie.

Dans le Cloud de SAP pour le client, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec SAP Cloud pour le client, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un Cloud de SAP pour l’utilisateur de test client](#creating-a-sap-cloud-for-customer-test-user)**  -toohave un équivalent de Britta Simon dans le Cloud de SAP pour le client qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre Cloud de SAP pour l’application du client.

**tooconfigure Azure AD l’authentification unique avec le Cloud de SAP pour le client, exécutez hello comme suit :**

1. Bonjour portail Azure, sur hello **Cloud SAP pour le client** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_samlbase.png)

3. Sur hello **Cloud SAP pour le domaine du client et les URL** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_url.png)

    a. Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<server name>.crm.ondemand.com`

    b. Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<server name>.crm.ondemand.com`

    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur. Contact [Cloud SAP pour l’équipe de support technique Client](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooget ces valeurs. 

4. Sur hello **attributs utilisateur** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_attribute.png)

    a. Dans **identificateur de l’utilisateur** liste, sélectionnez hello **ExtractMailPrefix()** (fonction).

    b. À partir de hello **Mail** liste, sélectionnez hello utilisateur attribut toouse pour votre implémentation.
    Par exemple, si vous voulez toouse hello EmployeeID comme identificateur d’utilisateur unique et si vous avez stocké la valeur de l’attribut hello Bonjour ExtensionAttribute2, puis sélectionnez user.extensionattribute2.  

5. Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_certificate.png) 

6. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_400.png)

7. Sur hello **Cloud SAP pour la Configuration de client** , cliquez sur **configurer le Cloud SAP pour le client** tooopen **configurer l’authentification** fenêtre. Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_configure.png) 

8. tooget l’authentification unique configurée, procédez hello comme suit :
   
    a. Connectez-vous au portail SAP Cloud pour le client avec des droits d’administrateur.
   
    b. Accédez toohello **Application et la tâche courante de gestion utilisateur** et cliquez sur hello **fournisseur d’identité** onglet.
   
    c. Cliquez sur **nouveau fournisseur d’identité** et le fichier XML des métadonnées hello select que vous avez téléchargé à partir de hello portail Azure. En important des métadonnées de hello, système de hello télécharge automatiquement le certificat de signature requis hello et certificat de chiffrement.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_54.png)
   
    d. Azure Active Directory requiert élément hello Assertion Consumer Service URL dans la demande SAML hello, afin de le sélectionner hello **inclure l’URL Assertion Consumer Service** case à cocher.
   
    e. Cliquez sur **Activate Single Sign-On**(Activer l’authentification unique).
   
    f. Enregistrez vos modifications.
   
    g. Cliquez sur hello **mon système** onglet.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_52.png)
   
    h. Dans la zone de texte **Azure AD Sign On URL** (URL de connexion Azure AD), collez l’**URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_53.png)
   
    i. Spécifier si les employés hello peuvent manuellement choisir entre l’ouverture de session avec l’ID d’utilisateur et mot de passe ou l’authentification unique en sélectionnant hello **sélection de fournisseur d’identité manuelle**.
   
    j. Bonjour **URL SSO** section, spécifiez les URL hello qui doit être utilisé par votre toosign employés sur toohello système. 
    Bonjour **tooEmployee d’URL envoyée** la liste, vous pouvez choisir entre hello options suivantes :
   
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

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-sap-cloud-for-customer-test-user"></a>Création d’un utilisateur de test SAP Cloud for Customer

Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans SAP Cloud pour le client. Collaborez avec [Cloud SAP pour l’équipe du support technique](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) utilisateurs hello tooadd hello SAP Cloud pour la plateforme du client. 

> [!NOTE]
> Assurez-vous que NameID valeur doit correspondre au champ de nom d’utilisateur hello Bonjour SAP Cloud pour la plateforme du client.

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooSAP Cloud pour le client.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooSAP Cloud pour le client, exécutez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Cloud SAP pour le client**.

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur hello SAP Cloud pour mosaïque hello volet d’accès client, vous devez obtenir automatiquement signé sur tooyour SAP Cloud pour l’application du client.
Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_203.png

