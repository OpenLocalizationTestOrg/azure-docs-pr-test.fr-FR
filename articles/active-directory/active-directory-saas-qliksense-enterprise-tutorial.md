---
title: "Didacticiel : Intégration d’Azure Active Directory à Qlik Sense Enterprise | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Qlik Sense Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8c27e340-2b25-47b6-bf1f-438be4c14f93
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 153edb3f8cd41790d4e9a74f15cfb806e5e9e3b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qlik-sense-enterprise"></a>Didacticiel : Intégration d’Azure Active Directory à Qlik Sense Enterprise

Dans ce didacticiel, vous apprendrez comment toointegrate Qlik Sense Enterprise avec Azure Active Directory (Azure AD).

Intégration Qlik Sense Enterprise à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooQlik Sense Enterprise.
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooQlik Sense Enterprise (Single Sign-On) avec leurs comptes Azure AD.
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec Qlik logique d’entreprise, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Qlik Sense Enterprise pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois ici : [offre d’essai](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de Qlik Sense Enterprise à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-qlik-sense-enterprise-from-hello-gallery"></a>Ajout de Qlik Sense Enterprise à partir de la galerie de hello
tooconfigure hello intégration d’entreprise de sens Qlik dans Azure AD, vous devez tooadd Qlik Sense Enterprise à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Qlik Sense Enterprise à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![bouton d’Azure Active Directory Hello][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![panneau des applications Enterprise Hello][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Nouveau bouton d’application Hello][3]

4. Dans la zone de recherche de hello, tapez **Qlik Sense Enterprise**, sélectionnez **Qlik Sense Enterprise** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.

    ![Qlik Sense Enterprise dans la liste des résultats hello](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD

Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Qlik Sense Enterprise avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello Qlik Sense Enterprise est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Qlik Sense Enterprise doit toobe établie.

Dans Qlik Sense Enterprise, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec Qlik logique d’entreprise, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Créer un utilisateur de test Qlik Sense Enterprise](#create-a-qlik-sense-enterprise-test-user)**  -toohave un équivalent de Britta Simon dans Qlik Sense Enterprise est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configure-azure-ad-single-sign-on"></a>Configurer l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application d’entreprise de sens Qlik.

**tooconfigure Azure AD l’authentification unique avec Qlik logique d’entreprise, effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **Qlik Sense Enterprise** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Lien Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_samlbase.png)

3. Sur hello **URL et le domaine d’entreprise logique Qlik** section, effectuer hello comme suit :

    ![Informations d’authentification unique de domaine et d’URL Qlik Sense Enterprise](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_url.png)

    a. Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`
    
    > [!NOTE]
    > Notez hello oblique à fin hello de cet URI. Elle est obligatoire.
    
    b. Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :
    | |
    |--|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qlikpoc.com`|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qliksense.com`|

    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mise à jour ces valeurs avec hello réel Sign-On URL et l’identificateur, qui vous seront expliquées plus loin dans ce didacticiel ou le contact [équipe de support Client d’entreprise logique Qlik](https://www.qlik.com/us/services/support) tooget ces valeurs. 

4. Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_400.png)

6. Préparez le fichier XML des métadonnées de fédération de hello afin que vous pouvez télécharger ce serveur de détection tooQlik.
   
    > [!NOTE]
    > Avant de télécharger hello IdP métadonnées toohello serveur de détection de Qlik, fichier de hello doit toobe modifié tooremove informations tooensure un bon fonctionnement entre Azure AD et le serveur de détection de Qlik.
    
    ![QlikSense][qs24]
   
    a. Ouvrez le fichier FederationMetaData.xml hello, qui vous avez téléchargé à partir du portail Azure dans un éditeur de texte.
   
    b. Recherchez la valeur de hello **RoleDescriptor**.  Il en existe quatre entrées (deux paires de balises d’élément d’ouverture et de fermeture).
   
    c. Supprimez les balises RoleDescriptor hello et toutes les informations entre hello fichier.
   
    d. Enregistrez le fichier de hello et conserver à proximité pour l’utiliser ultérieurement dans ce document.

7. Accédez toohello Qlik sens Qlik Management Console (QMC) en tant qu’utilisateur qui peut créer des configurations de proxy virtuel.

8. Bonjour QMC, cliquez sur hello **proxys virtuel** élément de menu.
   
    ![QlikSense][qs6] 

9. Bas hello écran hello, cliquez sur hello **nouvel** bouton.
   
    ![QlikSense][qs7]

10. écran de modification du proxy Hello virtuel s’affiche.  Sur hello à droite de l’écran hello est un menu pour rendre des options de configuration visibles.
   
    ![QlikSense][qs9]

11. Avec l’option de menu hello d’Identification vérifiée, entrez les informations d’identification pour la configuration de proxy virtuel Azure hello hello.
    
    ![QlikSense][qs8]  
    
    a. Hello **Description** champ est un nom convivial pour la configuration du proxy virtuel hello.  Entrez une valeur pour la description.
    
    b. Hello **préfixe** champ identifie le point de terminaison de proxy virtuel hello pour la connexion tooQlik sens avec Azure AD Single Sign-On.  Entrez un nom de préfixe unique pour ce proxy virtuel.
    
    c. **Délai d’inactivité de session (minutes)** est le délai d’attente hello pour les connexions via ce proxy virtuel.
    
    d. Hello **nom d’en-tête de cookie de Session** est un stockage de nom de cookie hello hello identificateur de session pour hello session Qlik sens un utilisateur reçoit après une authentification réussie.  Ce nom doit être unique.

12. Cliquez sur hello authentification menu option toomake il est visible.  écran de l’authentification Hello s’affiche.
    
    ![QlikSense][qs10]
    
    a. Hello **mode d’accès anonyme** liste déroulante détermine si les utilisateurs anonymes peuvent accéder Qlik sens via le proxy virtuel hello.  option de Hello par défaut n’est aucun utilisateur anonyme.
    
    b. Hello **méthode d’authentification** déroulante détermine hello authentification schéma hello virtuel proxy utilisera.  Sélectionnez SAML à partir de la liste déroulante de hello.  À la suite de cette sélection, d’autres options s’affichent.
    
    c. Bonjour **champ URI de l’hôte SAML**, les utilisateurs du nom d’hôte d’entrée hello entrent tooaccess Qlik sens via ce proxy virtuel SAML.  nom d’hôte Hello est uri hello Hello serveur de détection de Qlik.
    
    d. Bonjour **ID d’entité SAML**, entrez hello même valeur entrée pour le champ URI de hello SAML hôte.
    
    e. Hello **SAML IdP metadata** est le fichier hello modifié précédemment dans hello **modifier les métadonnées de fédération à partir de la Configuration d’Azure AD** section.  **Avant de télécharger des métadonnées IdP de hello, fichier de hello doit toobe modifié** tooremove informations tooensure fonctionnement entre Azure AD et le serveur de détection de Qlik.  **Si les fichiers hello a encore toobe modifié, consultez instructions toohello ci-dessus.**  Si hello fichier a été modifié cliquez sur Parcourir hello et tooupload de fichier de métadonnées modifiées hello sélectionnez il configuration du proxy virtuel toohello.
    
    f. Entrez la référence de schéma ou le nom de l’attribut hello pour l’attribut SAML de hello représentant hello **UserID** Azure AD envoie toohello serveur de détection de Qlik.  Informations de référence de schéma sont disponibles dans hello application Azure écrans après la configuration.  attribut de nom hello toouse, entrez `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.
    
    g. Entrez la valeur de hello pour hello **répertoire utilisateur** qui sera jointe toousers lors de l’authentification du serveur de détection de tooQlik via Azure AD.  Les valeurs codées en dur doivent être entourées de **crochets []**.  toouse un attribut envoyé Bonjour assertion Azure AD SAML, entrez le nom hello d’attribut de hello dans cette zone de texte **sans** entre crochets.
    
    h. Hello **algorithme de signature SAML** jeux hello pour la configuration du proxy virtuel hello de signature de certificat de fournisseur (dans ce cas server de Qlik sens) de service.  Si le serveur de détection de Qlik utilise un certificat approuvé est généré à l’aide de Microsoft Enhanced RSA et AES Cryptographic Provider, algorithme de signature SAML hello également modifier**SHA-256**.
    
    i. Hello section de mappage d’attribut SAML permet des attributs supplémentaires tels que des groupes toobe envoyé tooQlik sens pour une utilisation dans les règles de sécurité.

13. Cliquez sur hello **l’équilibrage de charge** toomake d’option de menu il est visible.  écran de l’équilibrage de charge Hello s’affiche.
    
    ![QlikSense][qs11]

14. Cliquez sur hello **ajouter un nœud de serveur** sélectionnez moteur nœud, du bouton ou nœuds Qlik sens envoyer à des fins d’équilibrage de la charge de sessions toofor, cliquez sur hello **ajouter** bouton.
    
    ![QlikSense][qs12]

15. Cliquez sur hello menu Avancé option toomake il est visible. écran Avancé Hello s’affiche.
    
    ![QlikSense][qs13]
    
    liste d’autorisation Hello hôte identifie les noms d’hôtes qui sont acceptées lors de la connexion toohello serveur de détection de Qlik.  **Entrez le nom d’hôte de l’hello les utilisateurs spécifieront lors de la connexion du serveur de détection de tooQlik.** nom d’hôte Hello est hello même valeur que hello SAML uri de l’hôte sans hello https://.

16. Cliquez sur hello **appliquer** bouton.
    
    ![QlikSense][qs14]

17. Cliquez sur OK tooaccept hello avertissement indiquant des proxys toohello lié des proxy virtuel doit être redémarré.
    
    ![QlikSense][qs15]

18. Sur la droite de l’écran hello hello hello associés éléments apparaît.  Cliquez sur hello **proxys** option de menu.
    
    ![QlikSense][qs16]

19. écran de proxy Hello s’affiche.  Cliquez sur hello **lien** bouton à hello bas toolink un toohello virtuel le proxy.
    
    ![QlikSense][qs17]

20. Nœud de proxy hello SELECT qui prend en charge cette connexion proxy virtuel cliquez sur hello **lien** bouton.  Après la liaison, le proxy de hello s’afficheront sous proxys associés.
    
    ![QlikSense][qs18]
  
    ![QlikSense][qs19]

21. Après que environ cinq secondes de tooten, hello message d’actualisation de QMC seront affiche.  Cliquez sur hello **QMC d’actualiser** bouton.
    
    ![QlikSense][qs20]

22. Lorsque hello QMC est actualisé, cliquez sur hello **virtuel proxys** élément de menu. nouvelle entrée de proxy virtuel SAML Hello est répertoriée dans la table hello sur l’écran hello.  Clic sur l’entrée de proxy virtuel hello.
    
    ![QlikSense][qs51]

23. Bouton de métadonnées de télécharger le Service Pack hello activera bas hello écran hello.  Cliquez sur hello **SP de télécharger des métadonnées** fichier tooa de bouton toosave hello métadonnées.
    
    ![QlikSense][qs52]

24. Fichier de métadonnées sp hello ouvert.  Observez hello **entityID** entrée et hello **AssertionConsumerService** entrée.  Ces valeurs sont équivalent toohello **identificateur** et hello **URL de connexion** dans la configuration de l’application hello Azure AD. Collez ces valeurs Bonjour **URL et le domaine d’entreprise logique Qlik** section de configuration de l’application hello Azure AD si elles ne correspondent pas, puis vous devez les remplacer dans l’Assistant de configuration de l’application Azure AD hello.
    
    ![QlikSense][qs53]

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur de test Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.

   ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_01.png)

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.

   ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_02.png)

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.

   ![bouton Ajouter de Hello](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_03.png)

4. Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :

   ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_04.png)

   a. Bonjour **nom** , tapez **BrittaSimon**.

   b. Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.

   c. Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.

   d. Cliquez sur **Create**.
 
### <a name="create-a-qlik-sense-enterprise-test-user"></a>Créer un utilisateur de test Qlik Sense Enterprise

Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Qlik Sense Enterprise. Travailler avec [équipe de support Client d’entreprise logique Qlik](https://www.qlik.com/us/services/support) pour ajouter des utilisateurs de hello en hello Qlik sens plate-forme. Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique. 

### <a name="assign-hello-azure-ad-test-user"></a>Affecter l’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooQlik Sense Enterprise.

![Attribuer le rôle d’utilisateur hello][200] 

**tooassign Britta Simon tooQlik Sense Enterprise, procédez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Qlik Sense Enterprise**.

    ![lien d’entreprise de sens Qlik Hello dans la liste des Applications hello](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_app.png)  

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![lien de « Utilisateurs et groupes » Hello][202]

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![volet d’ajouter l’affectation de Hello][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="test-single-sign-on"></a>Tester l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque Qlik Sense Enterprise hello hello volet d’accès, vous devez obtenir l’application d’entreprise de sens de Qlik automatiquement signé sur tooyour. 

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_203.png

[qs6]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_06.png
[qs7]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_07.png
[qs8]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_08.png
[qs9]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_09.png
[qs10]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_10.png
[qs11]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_11.png
[qs12]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_12.png
[qs13]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_13.png
[qs14]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_14.png
[qs15]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_15.png
[qs16]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_16.png
[qs17]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_17.png
[qs18]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_18.png
[qs19]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_19.png
[qs20]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_20.png
[qs24]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_24.png
[qs51]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_51.png
[qs52]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_52.png
[qs53]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_53.png

