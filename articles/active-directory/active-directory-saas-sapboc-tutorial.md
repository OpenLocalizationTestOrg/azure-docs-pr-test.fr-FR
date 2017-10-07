---
title: "Didacticiel : Intégration d’Azure Active Directory avec SAP Business Object Cloud | Microsoft Docs)"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et SAP Business objet Cloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 6c5e44f0-4e52-463f-b879-834d80a55cdf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: a3e9bd93897271531f91bcbc50cd361e8a20551e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-object-cloud"></a>Didacticiel : Intégration d’Azure Active Directory avec SAP Business Object Cloud

Dans ce didacticiel, vous apprendrez comment toointegrate SAP Cloud d’objet métier avec Azure Active Directory (Azure AD).

Vous obtenez hello avantages suivants lorsque vous intégrez SAP Business objet Cloud avec Azure AD :

- Dans Azure AD, vous pouvez contrôler qui a accès tooSAP Cloud d’objet métier.
- Vous pouvez signer automatiquement dans votre tooSAP utilisateurs Cloud d’objet métier à l’aide de l’authentification unique et un compte d’utilisateur Azure AD.
- Vous pouvez gérer vos comptes dans un emplacement central, hello portail Azure.

toolearn savoir plus sur le logiciel en tant qu’une intégration d’application de service (SaaS) avec Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooset d’intégration avec SAP Business objet Cloud d’Azure AD, vous devez hello éléments suivants :

- Un abonnement Azure AD
- SAP Business Object Cloud pour lequel l’authentification unique est activée

> [!NOTE]
> Si vous testez les étapes hello dans ce didacticiel, nous vous recommandons de ne pas les tester dans un environnement de production.

Recommandations pour le test des étapes de hello dans ce didacticiel :

- N’utilisez pas votre environnement de production, à moins que cela ne soit nécessaire.
- Si vous ne disposez pas d’un environnement d’essai Azure AD, vous pouvez [obtenir un essai gratuit d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. 

scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajouter des SAP Business objet Cloud à partir de la galerie de hello.
2. Configurez et testez l’authentification unique Azure AD.

## <a name="add-sap-business-object-cloud-from-hello-gallery"></a>Ajouter des SAP Business objet Cloud à partir de la galerie de hello
tooset intégration hello de SAP Business objet Cloud avec Azure AD, dans la galerie hello, ajouter la liste de tooyour SAP Business objet Cloud des applications SaaS gérées.

tooadd SAP Business objet Cloud à partir de la galerie de hello :

1. Bonjour [portail Azure](https://portal.azure.com)hello du menu de gauche, dans Sélectionnez **Azure Active Directory**. 

    ![bouton d’Azure Active Directory Hello][1]

2. Sélectionnez **Applications d’entreprise**, puis **Toutes les applications**.

    ![page des applications Enterprise Hello][2]
    
3. tooadd une nouvelle application, sélectionnez **nouvelle application**.

    ![Nouveau bouton d’application Hello][3]

4. Dans la zone de recherche de hello, entrez **SAP Business objet Cloud**.

    ![zone de recherche Hello](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_search.png)

5. Dans le volet de résultats hello, sélectionnez **SAP Business objet Cloud**, puis sélectionnez **ajouter**.

    ![Liste des résultats de SAP Business objet Cloud Bonjour](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_addfromgallery.png)

##  <a name="set-up-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD

Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec SAP Business Object Cloud, grâce à un utilisateur de test appelé *Britta Simon*.

Pour toowork de l’authentification unique, Azure AD doit utilisateur d’homologue tooknow hello Azure AD dans SAP Business objet Cloud. Une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans SAP Business objet Cloud doit être établie.

relation, dans SAP Business objet Cloud, de liens tooestablish hello pour **nom d’utilisateur**, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD.

tooconfigure et test Azure AD l’authentification unique avec le Cloud d’objet SAP Business, hello complète tâches suivantes :

1. [Configurer l’authentification unique Azure AD](#set-up-azure-ad-single-sign-on). Définit un toouse utilisateur cette fonctionnalité.
2. [Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user). Tests AD Azure authentification unique avec l’utilisateur hello Britta Simon.
3. [Créer un utilisateur de test pour SAP Business Object Cloud](#create-an-sap-business-object-cloud-test-user). Crée un équivalent de Britta Simon dans SAP Business objet Cloud qui est lié toohello la représentation sous forme de Azure AD de l’utilisateur de hello.
4. [Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user). Définit les toouse Britta Simon Azure AD l’authentification unique.
5. [Tester l’authentification unique](#test-single-sign-on). Vérifie que la configuration hello fonctionne.

### <a name="set-up-azure-ad-single-sign-on"></a>Configurer l’authentification unique Azure AD

Dans cette section, vous activez Azure AD unique signe sur Bonjour portail Azure. Ensuite, configurez l’authentification unique dans votre application SAP Business objet Cloud.

tooset d’Azure AD single sign-on avec SAP Business objet Cloud :

1. Bonjour portail Azure, sur hello **SAP Business objet Cloud** page d’intégration d’application, sélectionnez **l’authentification unique**.

    ![Sélectionner l’authentification unique][4]

2. Sur hello **l’authentification unique** page, pour **Mode**, sélectionnez **SAML-authentification**.
 
    ![Sélectionner l’authentification basée sur SAML](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_samlbase.png)

3. Sous **URL et le domaine de SAP Business objet Cloud**complète hello comme suit :

    1. Bonjour **URL de connexion** , entrez une URL qui pointe hello modèle : 
    | |
    |-|-|
    | `https://<sub-domain>.sapanalytics.cloud/` |
    | `https://<sub-domain>.sapbusinessobjects.cloud/` |

    2. Bonjour **identificateur** , entrez une URL qui pointe hello modèle :
    | |
    |-|-|
    | `<sub-domain>.sapbusinessobjects.cloud` |
    | `<sub-domain>.sapanalytics.cloud` |

    ![URL de la page URL et domaine SAP Business Object Cloud](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_url.png)
 
    > [!NOTE] 
    > les valeurs Hello dans ces URL sont fins de démonstration uniquement. Mise à jour des valeurs de hello avec hello réel authentification URL URL et l’identificateur. tooget hello URL de connexion, contact hello [équipe de support SAP Business objet Cloud Client](https://www.sap.com/product/analytics/cloud-analytics.support.html). Vous pouvez obtenir l’URL d’identificateur hello en téléchargeant des métadonnées du Cloud d’objet SAP Business hello à partir de la console d’administration hello. Cela est expliqué plus loin dans le didacticiel de hello. 

4. Sous **le certificat de signature SAML**, sélectionnez **XML des métadonnées**. Ensuite, enregistrez le fichier de métadonnées hello sur votre ordinateur.

    ![Sélectionnez XML des métadonnées](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_certificate.png) 

5. Sélectionnez **Enregistrer**.

    ![Sélectionner Enregistrer](./media/active-directory-saas-sapboc-tutorial/tutorial_general_400.png)

6. Dans une fenêtre de navigateur web, connectez-vous dans un site d’entreprise tooyour SAP Business objet Cloud en tant qu’administrateur.

7. Sélectionnez **Menu** > **Système** > **Administration**.
    
    ![Sélectionner Menu, puis Système et Administration](./media/active-directory-saas-sapboc-tutorial/config1.png)

8. Sur hello **sécurité** onglet, sélectionnez hello **modifier** icône (stylet).
    
    ![Sur l’onglet sécurité de hello, sélectionnez l’icône de modification hello](./media/active-directory-saas-sapboc-tutorial/config2.png)  

9. Sélectionnez **Méthode d’authentification unique SAML (SSO)** comme **Méthode d’authentification**.

    ![Sélectionnez SAML Single Sign-On pour la méthode d’authentification hello](./media/active-directory-saas-sapboc-tutorial/config3.png)  

10. toodownload hello fournisseur métadonnées de service (étape 1), sélectionnez **télécharger**. Dans le fichier de métadonnées hello, recherchez et copiez hello **entityID** valeur. Bonjour Azure portail, sous **URL et le domaine de SAP Business objet Cloud**, collez la valeur de hello Bonjour **identificateur** boîte.

    ![Copiez et collez la valeur entityID de hello](./media/active-directory-saas-sapboc-tutorial/config4.png)  

11. tooupload hello fournisseur métadonnées de service (étape 2) dans le fichier hello que vous avez téléchargé à partir de hello portail Azure, sous **les métadonnées de télécharger le fournisseur d’identité**, sélectionnez **télécharger**.  

    ![Sous Charger les métadonnées du fournisseur d’identité, sélectionnez Charger](./media/active-directory-saas-sapboc-tutorial/config5.png)

12. Bonjour **attribut utilisateur** répertorier, attribut d’utilisateur Sélectionnez hello (étape 3) que vous souhaitez toouse pour votre implémentation. Cet attribut utilisateur mappe toohello fournisseur d’identité. tooenter un attribut personnalisé sur la page de l’utilisateur hello, utilisez hello **de mappage SAML personnalisées** option. Ou bien, vous pouvez sélectionner **messagerie** ou **ID utilisateur** en tant qu’attribut de l’utilisateur hello. Dans notre exemple, nous avons sélectionné **messagerie** , car nous avons mappé la revendication d’identificateur hello utilisateur avec hello **userprincipalname** attribut Bonjour **attributs utilisateur** section Bonjour Portail Azure. Cela fournit une messagerie de l’utilisateur unique, ce qui est envoyé toohello application SAP Business objet Cloud chaque réponse SAML correcte.

    ![Sélectionner un attribut utilisateur](./media/active-directory-saas-sapboc-tutorial/config6.png)

13. compte de hello tooverify avec le fournisseur d’identité (étape 4), hello Bonjour **informations d’identification de connexion (courrier électronique)** , entrez l’adresse de messagerie de l’utilisateur hello. Ensuite, sélectionnez **Vérifier le compte**. système de Hello ajoute le compte d’utilisateur toohello informations de connexion.

    ![Entrer l’e-mail et sélectionner Vérifier le compte](./media/active-directory-saas-sapboc-tutorial/config7.png)

14. Sélectionnez hello **enregistrer** icône.

    ![Icône Enregistrer](./media/active-directory-saas-sapboc-tutorial/save.png)

> [!TIP]
> Vous pouvez lire une version concise de ces instructions Bonjour [portail Azure](https://portal.azure.com), alors que vous configurez votre application ! Après avoir ajouté l’application hello en sélectionnant **Active Directory** > **des Applications d’entreprise**, sélectionnez hello **Single Sign-On** onglet. Vous pouvez accéder à documentation hello incorporé Bonjour **Configuration** section, au bas de hello de page de hello. Pour plus d’informations, consultez la page [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD
Dans cette section, vous créez un utilisateur de test nommé Britta Simon Bonjour portail Azure.

toocreate un utilisateur test dans Azure AD :

1. Bonjour portail Azure, dans le menu de gauche hello, sélectionnez **Azure Active Directory**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay d’utilisateurs, sélectionnez **utilisateurs et groupes**, puis sélectionnez **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, sélectionnez **ajouter**.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_03.png) 

4. Bonjour **utilisateur** boîte de dialogue, hello complète comme suit :
 
    1. Bonjour **nom** , entrez **BrittaSimon**.

    2. Bonjour **nom d’utilisateur** , entrez l’adresse de messagerie hello de l’utilisateur hello Britta Simon.

    3. Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.

    4. Sélectionnez **Créer**.

        ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-sapboc-tutorial/create_aaduser_04.png) 

    ![Créer un utilisateur Azure AD][100]

### <a name="create-an-sap-business-object-cloud-test-user"></a>Créer un utilisateur de test SAP Business Object Cloud

Les utilisateurs Active Directory Azure doivent être configurés dans le Cloud d’objet SAP Business pour pouvoir se connecter dans tooSAP Cloud d’objet métier. Dans SAP Business Object Cloud, l’approvisionnement est une tâche manuelle.

tooprovision un compte d’utilisateur :

1. Se connecter tooyour site SAP Business objet Cloud d’entreprise en tant qu’administrateur.

2. Sélectionnez **Menu** > **Sécurité** > **Utilisateurs**.

    ![Ajouter un employé](./media/active-directory-saas-sapboc-tutorial/user1.png)

3. Sur hello **utilisateurs** , tooadd nouveau détails d’utilisateur, sélectionnez  **+** . 

    ![Page Ajouter des utilisateurs](./media/active-directory-saas-sapboc-tutorial/user4.png)

    Ensuite, effectuez hello comme suit :

    1. Bonjour **ID utilisateur** , entrez le code hello d’utilisateur de hello, tel que **Brian**.

    2. Bonjour **prénom** , entrez le nom d’utilisateur de hello, hello comme **Brian**.

    3. Bonjour **nom** , entrez le nom d’utilisateur de hello, hello comme **Simon**.

    4. Bonjour **nom d’affichage** zone, entrez le nom complet de hello d’utilisateur de hello, tel que **Britta Simon**.

    5. Bonjour **messagerie** zone, entrez les adresse de messagerie hello d’utilisateur de hello, tel que  **brittasimon@contoso.com** .

    6. Sur hello **sélectionner des rôles** page, sélectionnez hello le rôle approprié pour l’utilisateur de hello, puis sélectionnez **OK**.

      ![Sélectionner un rôle](./media/active-directory-saas-sapboc-tutorial/user3.png)

    7. Sélectionnez hello **enregistrer** icône.  


### <a name="assign-hello-azure-ad-test-user"></a>Affecter l’utilisateur de test hello Azure AD

Dans cette section, vous permettre à l’utilisateur hello Britta Simon toouse Azure AD l’authentification unique en accordant hello utilisateur compte accès tooSAP Cloud d’objet métier.

tooassign Britta Simon tooSAP Cloud d’objet métier :

1. Bonjour portail Azure, ouvrez la vue des applications hello et passez toohello vue d’annuaire. Sélectionnez **Applications d’entreprise**, puis **Toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **SAP Business objet Cloud**.

    ![Configurer l’authentification unique](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_app.png) 

3. Dans le menu de gauche hello, sélectionnez **utilisateurs et groupes**.

    ![Sélectionner Utilisateurs et groupes][202] 

4. Sélectionnez **Ajouter**. Ensuite, sous hello **ajouter l’affectation** page, sélectionnez **utilisateurs et groupes**.

    ![page Ajouter une attribution de Hello][203]

5. Sur hello **utilisateurs et groupes** page, dans la liste de hello des utilisateurs, sélectionnez **Britta Simon**.

6. Sur hello **utilisateurs et groupes** page, sélectionnez **sélectionnez**.

7. Sur hello **ajouter l’affectation** page, sélectionnez **affecter**.

![Attribuer le rôle d’utilisateur hello][200] 
    
### <a name="test-single-sign-on"></a>Tester l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide du volet d’accès hello.

Lorsque vous sélectionnez la vignette de SAP Business objet Cloud hello hello panneau d’accès, vous devez être connecté automatiquement dans tooyour application SAP Business objet Cloud.

Pour plus d’informations sur le volet d’accès hello, consultez [volet d’accès toohello Introduction](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de toointegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_203.png

