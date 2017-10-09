---
title: "Didacticiel : intégration d’Azure Active Directory à SAP HANA | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et SAP HANA."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: cef4a146-f4b0-4e94-82de-f5227a4b462c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 5ff6bfde0b1d7ab14025a4bc45199f9f826affd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana"></a>Didacticiel : Intégration d’Azure Active Directory à SAP HANA

Dans ce didacticiel, vous apprendrez comment toointegrate SAP HANA avec Azure Active Directory (Azure AD).

Intégration de SAP HANA à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooSAP HANA
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSAP HANA (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec SAP HANA, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement SAP HANA pour lequel l’authentification unique est activée
- Une instance HANA en cours d’exécution sur une IaaS publique, sur site, sur une machine virtuelle Azure ou sur une grande instance SAP dans Azure
- Hello Interface Web d’Administration de XSA ainsi HANA Studio est installé sur l’instance HANA hello.

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production de SAP HANA. Tester l’intégration hello d’abord dans le développement ou l’environnement d’application hello, puis utilisez hello production environnement de mise en lots.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de SAP HANA à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-sap-hana-from-hello-gallery"></a>Ajout de SAP HANA à partir de la galerie de hello
tooconfigure hello intégration de SAP HANA dans Azure AD, vous devez tooadd SAP HANA à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd SAP HANA à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![bouton d’Azure Active Directory Hello][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![panneau des applications Enterprise Hello][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Nouveau bouton d’application Hello][3]

4. Dans la zone de recherche de hello, tapez **SAP HANA**, sélectionnez **SAP HANA** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd. 

    ![Hello nouvelle application](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec SAP HANA, avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans SAP HANA est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans SAP HANA doit toobe établie.

Dans SAP HANA, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec SAP HANA, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test SAP HANA](#creating-a-sap-hana-test-user)**  -toohave un équivalent de Britta Simon dans SAP HANA qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application SAP HANA.

**tooconfigure Azure AD single sign-on avec SAP HANA, effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **SAP HANA** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_samlbase.png)

3. Sur hello **SAP HANA domaine et les URL** section, effectuer hello comme suit :

    ![Informations d’authentification unique dans Domaine et URL](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_url.png)

    a. Bonjour **identificateur** type en tant que zone de texte :`HA100` 

    b. Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`

    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettre à jour ces valeurs hello URL d’identificateur et de réponse réelle. Contact [équipe de support SAP HANA Client](https://cloudplatform.sap.com/contact.html) tooget ces valeurs. 

4. Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_certificate.png) 

    >[!Note]
    >Si le certificat n’est pas actif puis activez-le en cliquant sur hello Vérifiez de nouveau certificat » active » la case à cocher Bonjour Azure AD. 

5. Les applications SAP HANA attend les assertions SAML hello dans un format spécifique. Hello suivant capture d’écran montre un exemple de cela. Ici, nous avons mappé hello **identificateur de l’utilisateur** avec **ExtractMailPrefix()** fonction de **user.mail**. Cela donne la valeur hello préfixe par courrier électronique des utilisateur hello qui est hello ID utilisateur unique. Ceci est envoyé toohello les applications SAP HANA chaque réponse correcte.

    ![Configurer l’authentification unique](./media/active-directory-saas-saphana-tutorial/attribute.png)

6. Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue :

    a. Bonjour **identificateur de l’utilisateur** liste déroulante, sélectionnez **ExtractMailPrefix**.
    
    b. Bonjour **Mail** liste déroulante, sélectionnez **user.mail**.

7. Cliquez sur le bouton **Enregistrer** .

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-saphana-tutorial/tutorial_general_400.png)
    
8. tooconfigure l’authentification unique sur **SAP HANA** côté, connexion tooyour **HANA XSA Web Console** en parcourant toohello respectif-point de terminaison HTTPS.

    > [!Note]
    > Dans la configuration par défaut de hello, URL de hello redirige hello demande tooa écran de connexion, ce qui nécessite des informations d’identification hello d’un processus d’ouverture de session utilisateur toocomplete hello SAP HANA de base de données authentifié. utilisateur de Hello qui se connecte doit disposer des tâches d’administration hello des privilèges requis tooperform SAML.

9. Dans l’Interface Web XSA de hello, accédez trop**fournisseur d’identité SAML** à partir de là, cliquez sur hello **« + »** -bouton bas hello du volet de hello écran toodisplay hello ajouter les informations sur le fournisseur d’identité et d’effectuer Hello comme suit :

    ![Ajouter un fournisseur d’identité](./media/active-directory-saas-saphana-tutorial/sap1.png)

    a. Bonjour **ajouter les informations sur le fournisseur d’identité** volet, le contenu de hello coller Hello Metadata XML, que vous avez téléchargé à partir du portail Azure en hello **métadonnées** zone de texte.

    ![Paramètres d’ajout d’un fournisseur d’identité](./media/active-directory-saas-saphana-tutorial/sap2.png)

    b. Si le contenu de hello du document XML de hello est valides, hello l’analyse de processus extrait tooinsert des informations requises hello dans hello **sujet, ID d’entité et l’émetteur** champs Bonjour données générales zone d’écran et hello champs URL Bonjour Zone d’écran de destination, par exemple,  **URL de Base et SingleSignOn (*)**.

    ![Paramètres d’ajout d’un fournisseur d’identité](./media/active-directory-saas-saphana-tutorial/sap3.png)

    c. Dans la zone de nom hello Hello données générales écran zone, entrez un nom pour le nouveau fournisseur d’identité SAML SSO hello.

    > [!Note]
    > nom de Hello Hello SAML IDP est obligatoire et doit être unique ; il apparaît dans la liste hello de IDPs SAML disponibles qui s’affiche, si vous sélectionnez SAML comme méthode d’authentification hello pour toouse d’applications SAP HANA XS, par exemple, dans la zone d’écran hello d’authentification de l’outil d’Administration d’artefact XS hello.

10. Enregistrer les détails de hello du nouveau fournisseur d’identité SAML hello. Choisissez **enregistrer** toosave hello détails du fournisseur d’identité SAML hello et ajouter hello SAML IDP toohello liste de connus SAML IDPs.

    ![Bouton Enregistrer](./media/active-directory-saas-saphana-tutorial/sap4.png)

11. Dans Studio HANA dans Propriétés du système hello Hello **Configuration** , onglet de la filtrer uniquement les paramètres par **saml** et ajustez hello **assertion_timeout** de **10 s** trop**120 s**.

    ![Paramètre assertion_timeout](./media/active-directory-saas-saphana-tutorial/sap7.png)

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-saphana-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-saphana-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![bouton Ajouter de Hello](./media/active-directory-saas-saphana-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-saphana-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-sap-hana-test-user"></a>Création d’un utilisateur de test SAP HANA

tooenable Azure AD les utilisateurs toolog dans tooSAP HANA, vous devez les configurer dans SAP HANA.
SAP HANA prend en charge l’approvisionnement juste-à-temps, option activée par défaut.

Si vous devez manuellement toocreate un utilisateur, effectuez hello comme suit :

>[!Note]
>Vous pouvez modifier l’authentification externe hello utilisée par l’utilisateur de hello.
Les utilisateurs externes sont authentifiés à l’aide d’un système externe, par exemple un système Kerberos. Pour plus d’informations sur les identités externes, contactez votre [administrateur de domaine](https://cloudplatform.sap.com/contact.html).

1. Ouvrez hello [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) comme administrateur et activer hello utilisateur de base de données de SSO SAML.

    ![créer un utilisateur](./media/active-directory-saas-saphana-tutorial/sap5.png)

2. Toohello de graduation hello invisible de case à cocher à gauche de **SAML** et suivez le lien de configurer hello.

3. Cliquez sur **ajouter** tooadd hello SAML IDP, puis cliquez sur **OK** en sélectionnant hello fournisseur d’identité SAML approprié.

4. Ajouter hello **identité externe** (ex. BrittaSimon dans le cas présent) ou choisissez **« Quelconque »** et cliquez sur **OK**.

    >[!Note]
    >Si « Tout » case à cocher n’est pas activée, puis nom d’utilisateur hello HANA a besoin de nom de hello tooexactly correspondance d’utilisateur hello Bonjour UPN avant le suffixe de domaine hello (c'est-à-dire BrittaSimon@contoso.com deviendrait BrittaSimon dans HANA).

5. À des fins de test, affectez-les **« XS »** utilisateur toohello de rôles.

    ![attribution de rôles](./media/active-directory-saas-saphana-tutorial/sap6.png)

    > [!TIP]
    > Vous devez donner les autorisations appropriées pour vos cas d’usage, uniquement.

6. Enregistrer l’utilisateur de hello.

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooSAP HANA.

![Attribuer le rôle d’utilisateur hello][200] 

**tooassign Britta Simon tooSAP HANA, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **SAP HANA**.

    ![Affecter des utilisateurs](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![lien de « Utilisateurs et groupes » Hello][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![volet d’ajouter l’affectation de Hello][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque de SAP HANA hello Bonjour volet d’accès, vous devez obtenir l’application de SAP HANA automatiquement signé sur tooyour.
Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_203.png

