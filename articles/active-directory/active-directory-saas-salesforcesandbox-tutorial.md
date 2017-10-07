---
title: "Didacticiel : intégration d’Azure Active Directory à Salesforce Sandbox | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Salesforce Sandbox."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 7539f08356568a17ebfcee2764bbbefa129b0553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a>Didacticiel : Intégration d’Azure Active Directory à Salesforce Sandbox

Dans ce didacticiel, vous apprendrez comment toointegrate Salesforce Sandbox avec Azure Active Directory (Azure AD).

Intégration de Salesforce Sandbox avec Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooSalesforce bac à sable
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSalesforce bac à sable (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD à Salesforce Sandbox, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Salesforce Sandbox pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de bac à sable Salesforce à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-salesforce-sandbox-from-hello-gallery"></a>Ajout de bac à sable Salesforce à partir de la galerie de hello
tooconfigure hello intégration de Salesforce Sandbox dans Azure AD, vous devez tooadd bac à sable Salesforce à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd bac à sable Salesforce à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. Cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue hello.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **Salesforce Sandbox**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_search.png)

5. Dans le volet de résultats hello, sélectionnez **Salesforce Sandbox**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Salesforce Sandbox sur un utilisateur de test nommé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Salesforce Sandbox est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans un bac à sable Salesforce hello doit toobe établie.

Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Salesforce Sandbox.

tooconfigure et test Azure AD l’authentification unique avec Salesforce Sandbox, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test de Salesforce Sandbox](#creating-a-salesforce-sandbox-test-user)**  -toohave un équivalent de Britta Simon dans Salesforce Sandbox qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Salesforce Sandbox.

**tooconfigure Azure AD single sign-on avec Salesforce Sandbox, procédez hello comme suit :**

1. Bonjour portail Azure, sur hello **Salesforce Sandbox** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_samlbase.png)

3. Sur hello **URL et le domaine de bac à sable Salesforce** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_url.png)

     Bonjour **URL de connexion** zone de texte, valeur hello de type hello suivant le modèle à l’aide de :`https://<subdomain>.my.salesforce.com`

    > [!NOTE] 
    > Cette valeur n’est pas hello réel. Mettre à jour cette valeur avec l’URL de connexion réel hello. Contact [équipe de support Client de bac à sable Salesforce](https://help.salesforce.com/support) tooget cette valeur.


4. Si vous avez déjà configuré l’authentification unique pour une autre instance Salesforce Sandbox dans votre annuaire, vous devez également configurer hello **identificateur** toohave hello la même valeur que hello **URL de connexion**. 
    
    >[!Note]
    >Hello **identificateur** champ sont accessibles en vérifiant hello **afficher les paramètres avancés** case à cocher sur hello **Configure App URL** page de boîte de dialogue hello 


5. Sur hello **le certificat de signature SAML** , cliquez sur **certificat** , puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_certificate.png) 

6. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_400.png)

7. Sur hello **Configuration du bac à sable Salesforce** , cliquez sur **configurer Salesforce Sandbox** tooopen **configurer l’authentification** fenêtre. Hello de copie **ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS>
8. Ouvrez un nouvel onglet dans votre navigateur et connectez-vous à tooyour compte d’administrateur Salesforce Sandbox.

9. Dans le menu hello haut de hello, cliquez sur **le programme d’installation**.

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforcesandbox-tutorial/IC781024.png)
10. Dans le volet de navigation hello hello gauche, cliquez sur **des contrôles de sécurité**, puis cliquez sur **paramètres d’authentification unique**.

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforcesandbox-tutorial/IC781025.png)
11. Sur hello section de paramètres d’authentification unique, procédez hello comme suit : ![configurer l’authentification unique](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)
     
     a.  Sélectionnez **SAML Enabled**. 

     b.  Cliquez sur **Nouveau**.

12. Sur hello section de paramètres d’authentification unique SAML, procédez hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforcesandbox-tutorial/IC781027.png)

    zone de texte nom a.In hello, entrez un nom hello de configuration de hello (par exemple : *SPSSOWAAD\_Test*). 

    b. Coller **ID d’entité SMAL** valeur hello **émetteur** zone de texte.

    c. Bonjour **Id d’entité** zone de texte, type **https://test.salesforce.com** s’il s’agit de hello première instance Salesforce Sandbox que vous ajoutez tooyour active. Si vous avez déjà ajouté une instance de bac à sable Salesforce, puis pour hello **ID d’entité** type Bonjour **URL de connexion**, qui doit être au format suivant :`http://company.my.salesforce.com`  
 
    d. Cliquez sur **Parcourir** hello de tooupload téléchargé le certificat.  

    e. En tant que **SAML Identity Type**, sélectionnez **Assertion contient hello ID de fédération à partir de l’objet utilisateur de hello**.
 
    f. En tant que **emplacement d’identité SAML**, sélectionnez **identité figure dans l’élément NameIdentifier de hello Hello Subject statement**.

    g. Coller **-Service URL d’authentification** dans hello **Identity Provider Login URL** zone de texte. 

    h. SFDC ne prend pas en charge la déconnexion SAML.  Pour résoudre ce problème, collez 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' dans hello **Identity Provider Logout URL** zone de texte.

    i. Pour **Service Provider Initiated Request Binding (Liaison de demande initiée par le fournisseur de services)**, sélectionnez **HTTP POST**. 

    j. Cliquez sur **Enregistrer**.

### <a name="enable-your-domain"></a>Activer votre domaine
Cette section suppose que vous avez déjà créé un domaine.  Pour plus d’informations, voir [Définition de votre nom de domaine](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).

**tooenable votre domaine, effectuer hello comme suit :**

1. Dans le volet de navigation gauche hello, cliquez sur **gestion des domaines**, puis cliquez sur **mon domaine.**
   
     ![Configurer l’authentification unique](./media/active-directory-saas-salesforcesandbox-tutorial/IC781029.png)
   
   >[!NOTE]
   >Vérifiez que votre domaine a été correctement configuré. 

2. Bonjour **les paramètres de Page de connexion** , cliquez sur **modifier**, puis, en tant que **Service d’authentification**, sélectionnez nom hello Hello SAML unique Sign-On Setting de hello précédente et enfin cliquez sur **enregistrer**.
   
   ![Configurer l’authentification unique](./media/active-directory-saas-salesforcesandbox-tutorial/IC781030.png)

Dès que vous avez un domaine configuré, vos utilisateurs doivent utiliser le bac à sable hello domaine URL toologin toohello Salesforce.  

valeur hello tooget hello URL, cliquez sur profil d’authentification unique hello que vous avez créé dans la section précédente de hello.    

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_02.png) 

3. En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-salesforce-sandbox-test-user"></a>Création d’un utilisateur de test Salesforce Sandbox

Dans cette section, un utilisateur nommé Britta Simon est créé dans Salesforce Sandbox. Salesforce Sandbox prend en charge l’approvisionnement juste-à-temps, option activée par défaut.
Vous n’avez aucune opération à effectuer dans cette section. Si un utilisateur n’existe pas déjà dans le bac à sable Salesforce, un nouveau est créé lorsque vous essayez de tooaccess Salesforce Sandbox.

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooSalesforce Sandbox.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooSalesforce bac à sable, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Salesforce Sandbox**.

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Si vous souhaitez tootest vos paramètres d’authentification unique, ouvrez hello panneau d’accès. Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)
* [Configurer l’approvisionnement de l’utilisateur](active-directory-saas-salesforce-sandbox-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_203.png

