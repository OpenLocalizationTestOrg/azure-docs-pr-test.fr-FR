---
title: "Didacticiel : Intégration d’Azure Active Directory à Workplace par Facebook | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et l’espace de travail par Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f71a59527394730757d501a973251dc293fd3683
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a>Didacticiel : Intégration d’Azure Active Directory à Workplace by Facebook

Dans ce didacticiel, vous apprendrez comment toointegrate espace de travail par Facebook avec Azure Active Directory (Azure AD).

Intégration d’espace de travail par Facebook à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a tooWorkplace d’accès par Facebook
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooWorkplace par Facebook (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec l’espace de travail par Facebook, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Workplace by Facebook pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout d’espace de travail par Facebook à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-workplace-by-facebook-from-hello-gallery"></a>Ajout d’espace de travail par Facebook à partir de la galerie de hello
intégration de hello tooconfigure du poste de travail par Facebook dans Azure AD, vous devez tooadd espace de travail par Facebook à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd espace de travail par Facebook à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **espace de travail par Facebook**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_search.png)

5. Dans le volet de résultats hello, sélectionnez **espace de travail par Facebook**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Workplace by Facebook, avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans l’espace de travail par Facebook est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans l’espace de travail par Facebook hello doit toobe établie.

Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans l’espace de travail par Facebook.

tooconfigure et test Azure AD l’authentification unique avec l’espace de travail par Facebook, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Configuration de la fréquence de la réauthentification](#configuring-reauthentication-frequency)**  -tooprompt d’espace de travail tooconfigure pour une vérification SAML.
3. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
4. **[Création d’un espace de travail par l’utilisateur de test Facebook](#creating-a-workplace-by-facebook-test-user)**  -toohave un équivalent de Britta Simon dans l’espace de travail par Facebook est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
5. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
6. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre espace de travail par application Facebook.

**tooconfigure Azure AD authentification unique avec l’espace de travail par Facebook, effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **espace de travail par Facebook** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. Sur hello **espace de travail par le domaine de Facebook et URL** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_url.png)

    a. Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<instancename>.facebook.com`

    b. Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://www.facebook.com/company/<instancename>`

    > [!NOTE] 
    > Ces valeurs ne sont pas hello réel. Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur. Contact [espace de travail par équipe de support Facebook Client](https://workplace.fb.com/faq/) tooget ces valeurs. 

4. Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_400.png)

6. Sur hello **espace de travail par la Configuration de Facebook** , cliquez sur **configurer le poste de travail par Facebook** tooopen **configurer l’authentification** fenêtre. Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-workplacebyfacebook-tutorial/config.png) 

7. Dans une fenêtre de navigateur web, connexion tooyour espace de travail par site d’entreprise Facebook en tant qu’administrateur.
  
   > [!NOTE] 
   > Dans le cadre du processus d’authentification SAML de hello, espace de travail peut-être utiliser des chaînes de requête de configuration taille dans l’ordre toopass paramètres tooAzure AD too2.5 kilo-octets.

8. Bonjour **tableau de bord entreprise**, accédez toohello **authentification** onglet.

9. Sous **l’authentification SAML**, sélectionnez **SSO uniquement** à partir de la liste déroulante de hello.

10. Les valeurs d’entrée hello copiés à partir de **espace de travail par la Configuration de Facebook** section Hello Azure portal dans les champs correspondants hello :

    *   Dans **URL SAML** zone de texte, valeur hello coller **-Service URL d’authentification**, lequel vous avez copié à partir du portail Azure.
    *   Dans **zone de texte URL de l’émetteur SAML**, collez la valeur hello **ID d’entité SAML**, lequel vous avez copié à partir du portail Azure.
    *   Dans **redirection de déconnexion SAML** (facultatif), collez la valeur hello **URL de déconnexion**, lequel vous avez copié à partir du portail Azure.
    *   Ouvrez votre **certificat codé en base 64** dans le bloc-notes est téléchargé à partir du portail Azure, copiez le contenu de hello de celui-ci dans le Presse-papiers, puis collez-la toothe **certificat SAML** zone de texte.

11. Vous devrez peut-être tooenter hello Audience URL, URL de destinataire, et les URL des services ACS (Assertion Consumer Service) répertoriées sous hello **Configuration SAML** section.

12. Faites défiler bas toohello de section de hello, puis cliquez sur hello **Test SSO** bouton. Une fenêtre contextuelle apparaît, avec la page de connexion Azure AD. Entrez vos informations d’identification dans tooauthenticate normal. 

    **Résolution des problèmes :** adresse de messagerie Vérifiez hello renvoyé à partir d’Azure AD est hello identique hello compte espace de travail que vous êtes connecté.

13. Une fois le test de hello a été effectuée correctement, faites défiler bas toohello de page de hello, puis cliquez sur hello **enregistrer** bouton.

14. La page de connexion à Azure AD sera désormais présentée à tous les utilisateurs de Workplace pour qu’ils s’authentifient.

15. **Redirection de déconnexion SAML (facultatif)** - 

    Vous pouvez choisir toooptionally configurer une Url de déconnexion SAML, qui peut être utilisé toopoint à la page de déconnexion d’Azure AD. Lorsque ce paramètre est activé et configuré, les utilisateurs hello ne pourra plus être page de déconnexion toohello un espace de travail. Au lieu de cela, utilisateur de hello sera redirigé toohello url qui a été ajoutée dans le paramètre de redirection de déconnexion SAML hello.


> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="configuring-reauthentication-frequency"></a>Configuration de la fréquence de réauthentification

Vous pouvez configurer tooprompt d’espace de travail pour une vérification SAML chaque jour, trois jours, semaine, deux semaines, mois ou jamais.

> [!NOTE] 
>Hello valeur minimale pour la vérification de SAML hello sur des applications mobiles est définie tooone semaine.

Vous pouvez également forcer une réinitialisation de tous les utilisateurs à l’aide du bouton de hello SAML : exiger l’authentification SAML pour tous les utilisateurs désormais.


### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-workplace-by-facebook-test-user"></a>Création d’un utilisateur de test Workplace by Facebook

Dans cette section, un utilisateur appelé Britta Simon est créé dans Workplace by Facebook. Workplace by Facebook prend en charge l’approvisionnement juste-à-temps, qui est activé par défaut.

Vous n’avez aucune opération à effectuer dans cette section. Si un utilisateur n’existe pas dans l’espace de travail par Facebook, un nouveau est créé lors de l’espace de travail de tooaccess par Facebook.

>[!Note]
>Si vous avez besoin de toocreate un utilisateur manuellement, contactez [espace de travail par équipe de support Facebook Client](https://workplace.fb.com/faq/)

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès des tooWorkplace par Facebook.

![Affecter des utilisateurs][200] 

**tooassign tooWorkplace Britta Simon par Facebook, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **espace de travail par Facebook**.

    ![Configurer l’authentification unique](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Si vous souhaitez tootest vos paramètres d’authentification unique, ouvrez hello panneau d’accès.
Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).


## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)
* [Configurer l’approvisionnement de l’utilisateur](active-directory-saas-workplacebyfacebook-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_203.png

