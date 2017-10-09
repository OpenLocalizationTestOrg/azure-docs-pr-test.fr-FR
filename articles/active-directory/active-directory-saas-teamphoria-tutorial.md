---
title: "Didacticiel : intégration d’Azure Active Directory à Teamphoria | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Teamphoria."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d569c705-6f0f-4ec1-b485-ba82526b5d32
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: f32be9742b76f7fe464036dadc108c62e4a787a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamphoria"></a><span data-ttu-id="81f78-103">Didacticiel : Intégration d’Azure Active Directory à Teamphoria</span><span class="sxs-lookup"><span data-stu-id="81f78-103">Tutorial: Azure Active Directory integration with Teamphoria</span></span>

<span data-ttu-id="81f78-104">Dans ce didacticiel, vous apprendrez comment toointegrate Teamphoria avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="81f78-104">In this tutorial, you learn how toointegrate Teamphoria with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="81f78-105">Intégration Teamphoria à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="81f78-105">Integrating Teamphoria with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="81f78-106">Vous pouvez contrôler dans Azure AD qui a accès tooTeamphoria</span><span class="sxs-lookup"><span data-stu-id="81f78-106">You can control in Azure AD who has access tooTeamphoria</span></span>
- <span data-ttu-id="81f78-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooTeamphoria (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="81f78-107">You can enable your users tooautomatically get signed-on tooTeamphoria (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="81f78-108">Vous pouvez gérer vos comptes dans un emplacement central - portail de gestion Azure hello</span><span class="sxs-lookup"><span data-stu-id="81f78-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="81f78-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="81f78-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with Teamphoria, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Teamphoria.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="81f78-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="81f78-110">Prerequisites</span></span>

<span data-ttu-id="81f78-111">tooconfigure intégration d’Azure AD avec Teamphoria, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="81f78-111">tooconfigure Azure AD integration with Teamphoria, you need hello following items:</span></span>

- <span data-ttu-id="81f78-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="81f78-112">An Azure AD subscription</span></span>
- <span data-ttu-id="81f78-113">Un abonnement Teamphoria pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="81f78-113">A Teamphoria single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="81f78-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="81f78-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="81f78-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="81f78-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="81f78-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="81f78-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="81f78-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="81f78-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="81f78-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="81f78-118">Scenario description</span></span>
<span data-ttu-id="81f78-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="81f78-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="81f78-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="81f78-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="81f78-121">Ajout de Teamphoria à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="81f78-121">Adding Teamphoria from hello gallery</span></span>
2. <span data-ttu-id="81f78-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="81f78-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamphoria-from-hello-gallery"></a><span data-ttu-id="81f78-123">Ajout de Teamphoria à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="81f78-123">Adding Teamphoria from hello gallery</span></span>
<span data-ttu-id="81f78-124">intégration de hello tooconfigure de Teamphoria dans Azure AD, vous devez tooadd Teamphoria à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="81f78-124">tooconfigure hello integration of Teamphoria into Azure AD, you need tooadd Teamphoria from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="81f78-125">**tooadd Teamphoria à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="81f78-125">**tooadd Teamphoria from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="81f78-126">Bonjour  **[portail de gestion Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="81f78-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="81f78-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="81f78-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="81f78-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="81f78-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="81f78-131">Cliquez sur **ajouter** bouton en haut de hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="81f78-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="81f78-133">Dans la zone de recherche de hello, tapez **Teamphoria**.</span><span class="sxs-lookup"><span data-stu-id="81f78-133">In hello search box, type **Teamphoria**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_search.png)

5. <span data-ttu-id="81f78-135">Dans le volet de résultats hello, sélectionnez **Teamphoria**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="81f78-135">In hello results panel, select **Teamphoria**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="81f78-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="81f78-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="81f78-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Teamphoria avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="81f78-138">In this section, you configure and test Azure AD single sign-on with Teamphoria based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="81f78-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Teamphoria est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81f78-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Teamphoria is tooa user in Azure AD.</span></span> <span data-ttu-id="81f78-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Teamphoria doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="81f78-140">In other words, a link relationship between an Azure AD user and hello related user in Teamphoria needs toobe established.</span></span>

<span data-ttu-id="81f78-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="81f78-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Teamphoria.</span></span>

<span data-ttu-id="81f78-142">tooconfigure et test Azure AD l’authentification unique avec Teamphoria, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="81f78-142">tooconfigure and test Azure AD single sign-on with Teamphoria, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="81f78-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="81f78-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="81f78-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="81f78-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="81f78-145">**[Création d’un utilisateur de test Teamphoria](#creating-a-teamphoria-test-user)**  -toohave de Britta Simon dans Teamphoria qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.</span><span class="sxs-lookup"><span data-stu-id="81f78-145">**[Creating a Teamphoria test user](#creating-a-teamphoria-test-user)** - toohave a counterpart of Britta Simon in Teamphoria that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="81f78-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="81f78-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="81f78-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="81f78-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="81f78-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="81f78-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="81f78-149">Dans cette section, vous activez Azure AD l’authentification unique dans le portail de gestion Azure hello et configurez l’authentification unique dans votre application Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="81f78-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Teamphoria application.</span></span>

<span data-ttu-id="81f78-150">**tooconfigure Azure AD single sign-on avec Teamphoria, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="81f78-150">**tooconfigure Azure AD single sign-on with Teamphoria, perform hello following steps:**</span></span>

1. <span data-ttu-id="81f78-151">Dans le portail de gestion Azure hello, sur hello **Teamphoria** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="81f78-151">In hello Azure Management portal, on hello **Teamphoria** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="81f78-153">Sur hello **l’authentification unique** boîte de dialogue, en tant que **Mode** sélectionnez **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="81f78-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_samlbase.png)

3. <span data-ttu-id="81f78-155">Sur hello **Teamphoria domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="81f78-155">On hello **Teamphoria Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_url.png)

    <span data-ttu-id="81f78-157">a.</span><span class="sxs-lookup"><span data-stu-id="81f78-157">a.</span></span> <span data-ttu-id="81f78-158">Bonjour **URL de connexion** zone de texte, tapez l’URL hello hello suivant le modèle à l’aide de :`https://<sub-domain>.teamphoria.com/login`</span><span class="sxs-lookup"><span data-stu-id="81f78-158">In hello **Sign-on URL** textbox, type hello URL using hello following pattern: `https://<sub-domain>.teamphoria.com/login`</span></span>  

    > [!NOTE] 
    > <span data-ttu-id="81f78-159">Notez qu’il s’agit pas des valeurs réelles hello.</span><span class="sxs-lookup"><span data-stu-id="81f78-159">Please note that these are not hello real values.</span></span> <span data-ttu-id="81f78-160">Vous avez défini ces valeurs avec hello tooupdate URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="81f78-160">You have tooupdate these values with hello actual Sign-On URL.</span></span> <span data-ttu-id="81f78-161">Contact [équipe de support Client de Teamphoria](https://www.teamphoria.com/) tooget hello Sign-on URL.</span><span class="sxs-lookup"><span data-stu-id="81f78-161">Contact [Teamphoria Client support team](https://www.teamphoria.com/) tooget hello Sign-on URL.</span></span> 

4. <span data-ttu-id="81f78-162">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le certificat de hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="81f78-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_certificate.png) 

5. <span data-ttu-id="81f78-164">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="81f78-164">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-teamphoria-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="81f78-166">Sur hello **Teamphoria Configuration** , cliquez sur **Teamphoria de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="81f78-166">On hello **Teamphoria Configuration** section, click **Configure Teamphoria** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="81f78-167">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="81f78-167">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_configure.png) 

7. <span data-ttu-id="81f78-169">tooconfigure l’authentification unique sur **Teamphoria** côté, l’application de Teamphoria tooyour de connexion en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="81f78-169">tooconfigure single sign-on on **Teamphoria** side, Login tooyour Teamphoria application as an administrator.</span></span>

8. <span data-ttu-id="81f78-170">Accédez trop**administrateur paramètres** option dans la barre d’outils de gauche hello et sous hello hello configurer un onglet cliquez sur **l’authentification unique** fenêtre de configuration de l’authentification unique tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="81f78-170">Go too**ADMIN SETTINGS** option in hello left toolbar and under hello hello Configure Tab click on **SINGLE SIGN-ON** tooopen hello SSO configuration window.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-teamphoria-tutorial/admin_sso_configure.png)

9. <span data-ttu-id="81f78-172">Cliquez sur **Ajouter nouveau fournisseur d’identité** option sous forme de hello tooopen hello coin supérieur droit pour ajouter des paramètres hello pour l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="81f78-172">Click on **ADD NEW IDENTITY PROVIDER** option in hello top right corner tooopen hello form for adding hello settings for SSO.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-teamphoria-tutorial/add_new_identity_provider.png)

10. <span data-ttu-id="81f78-174">Entrez les détails de hello dans les champs de hello comme décrit ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="81f78-174">Enter hello details in hello fields as described below-</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-teamphoria-tutorial/Teamphoria_sso_save.png)

    <span data-ttu-id="81f78-176">a.</span><span class="sxs-lookup"><span data-stu-id="81f78-176">a.</span></span> <span data-ttu-id="81f78-177">**Le nom complet** : entrez le nom d’affichage de hello du plug-in hello sur la page d’administration hello.</span><span class="sxs-lookup"><span data-stu-id="81f78-177">**DISPLAY NAME** : Enter hello display name of hello plugin on hello admin page.</span></span>

    <span data-ttu-id="81f78-178">b.</span><span class="sxs-lookup"><span data-stu-id="81f78-178">b.</span></span> <span data-ttu-id="81f78-179">**NOM du bouton** : nom hello d’onglet hello qui s’affiche sur la page de connexion hello pour la connexion via l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="81f78-179">**BUTTON NAME** : hello name of hello tab which will display on hello login page for logging in via SSO.</span></span>

    <span data-ttu-id="81f78-180">c.</span><span class="sxs-lookup"><span data-stu-id="81f78-180">c.</span></span> <span data-ttu-id="81f78-181">**CERTIFICAT** : hello ouvrir certificat précédemment téléchargés de hello portail Azure dans le bloc-notes, copiez le contenu de hello du hello même et collez-le ici dans la zone de hello.</span><span class="sxs-lookup"><span data-stu-id="81f78-181">**CERTIFICATE** : Open hello Certificate downloaded earlier from hello Azure portal in notepad, copy hello contents of hello same and paste it here in hello box.</span></span>

    <span data-ttu-id="81f78-182">d.</span><span class="sxs-lookup"><span data-stu-id="81f78-182">d.</span></span> <span data-ttu-id="81f78-183">**POINT d’entrée** : hello de coller **SAML Sign-On URL du Service unique** copiés hello formulaire antérieur portail Azure.</span><span class="sxs-lookup"><span data-stu-id="81f78-183">**ENTRY POINT** : Paste hello **SAML Single Sign-On Service URL** copied earlier form hello Azure portal.</span></span>

    <span data-ttu-id="81f78-184">e.</span><span class="sxs-lookup"><span data-stu-id="81f78-184">e.</span></span> <span data-ttu-id="81f78-185">Basculer les option hello trop**ON** , puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="81f78-185">Switch hello option too**ON** and click on **SAVE**.</span></span> 

<!--### Next steps

tooensure users can sign-in tooTeamphoria after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Teamphoria prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooTeamphoria in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Teamphoria users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="81f78-186">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="81f78-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="81f78-187">objectif Hello de cette section est toocreate un utilisateur de test dans le portail de gestion Azure hello appelé Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="81f78-187">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="81f78-189">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="81f78-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="81f78-190">Bonjour **portail de gestion Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="81f78-190">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="81f78-192">Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="81f78-192">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="81f78-194">En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="81f78-194">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="81f78-196">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="81f78-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="81f78-198">a.</span><span class="sxs-lookup"><span data-stu-id="81f78-198">a.</span></span> <span data-ttu-id="81f78-199">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="81f78-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="81f78-200">b.</span><span class="sxs-lookup"><span data-stu-id="81f78-200">b.</span></span> <span data-ttu-id="81f78-201">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="81f78-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="81f78-202">c.</span><span class="sxs-lookup"><span data-stu-id="81f78-202">c.</span></span> <span data-ttu-id="81f78-203">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="81f78-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="81f78-204">d.</span><span class="sxs-lookup"><span data-stu-id="81f78-204">d.</span></span> <span data-ttu-id="81f78-205">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="81f78-205">Click **Create**.</span></span>
 
### <a name="creating-a-teamphoria-test-user"></a><span data-ttu-id="81f78-206">Création d’un utilisateur de test Teamphoria</span><span class="sxs-lookup"><span data-stu-id="81f78-206">Creating a Teamphoria test user</span></span>

<span data-ttu-id="81f78-207">Dans l’ordre tooenable Azure AD les utilisateurs toolog dans Teamphoria, ils doivent être configurés dans Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="81f78-207">In order tooenable Azure AD users toolog into Teamphoria, they must be provisioned into Teamphoria.</span></span> <span data-ttu-id="81f78-208">Dans les cas de hello de Teamphoria, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="81f78-208">In hello case of Teamphoria, provisioning is a manual task.</span></span>

<span data-ttu-id="81f78-209">**effectuer des comptes d’utilisateur, tooprovision hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="81f78-209">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="81f78-210">Ouvrez une session dans tooyour Teamphoria site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="81f78-210">Log in tooyour Teamphoria company site as an administrator.</span></span>

2. <span data-ttu-id="81f78-211">Cliquez sur **ADMIN** les paramètres de barre d’outils de gauche hello et sous hello **gérer** onglet cliquez **utilisateurs** page d’administration tooopen hello pour les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="81f78-211">Click on **ADMIN** settings on hello left toolbar and under hello **MANAGE** tab Click on **USERS** tooopen hello admin page for users.</span></span>

    ![Ajouter un employé](./media/active-directory-saas-teamphoria-tutorial/admin_manage_users.png)

3. <span data-ttu-id="81f78-213">Cliquez sur hello **manuel inviter** option.</span><span class="sxs-lookup"><span data-stu-id="81f78-213">Click on hello **MANUAL INVITE** option.</span></span>

    ![Inviter des personnes](./media/active-directory-saas-teamphoria-tutorial/admin_manage_add_users.png)  

4. <span data-ttu-id="81f78-215">Dans cette page, effectuez l’action suivante.</span><span class="sxs-lookup"><span data-stu-id="81f78-215">On this page, perform following action.</span></span> 
    
    ![Inviter des personnes](./media/active-directory-saas-teamphoria-tutorial/manual_user_invite.png)  

    <span data-ttu-id="81f78-217">a.</span><span class="sxs-lookup"><span data-stu-id="81f78-217">a.</span></span> <span data-ttu-id="81f78-218">Bonjour **adresse de messagerie** zone de texte, hello **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="81f78-218">In hello **EMAIL ADDRESS** textbox, hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="81f78-219">b.</span><span class="sxs-lookup"><span data-stu-id="81f78-219">b.</span></span> <span data-ttu-id="81f78-220">Bonjour **prénom** zone de texte, type **Brian**.</span><span class="sxs-lookup"><span data-stu-id="81f78-220">In hello **FIRST NAME** textbox, type **Britta**.</span></span>

    <span data-ttu-id="81f78-221">c.</span><span class="sxs-lookup"><span data-stu-id="81f78-221">c.</span></span> <span data-ttu-id="81f78-222">Bonjour **nom** zone de texte, type **Simon**.</span><span class="sxs-lookup"><span data-stu-id="81f78-222">In hello **LAST NAME** textbox, type **Simon**.</span></span>

    <span data-ttu-id="81f78-223">d.</span><span class="sxs-lookup"><span data-stu-id="81f78-223">d.</span></span> <span data-ttu-id="81f78-224">Cliquez sur **INVITE 1 USER** (Inviter l’utilisateur 1).</span><span class="sxs-lookup"><span data-stu-id="81f78-224">Click **INVITE 1 USER**.</span></span> <span data-ttu-id="81f78-225">L’utilisateur doit tooaccept hello invitation tooget est créé dans le système de hello.</span><span class="sxs-lookup"><span data-stu-id="81f78-225">User needs tooaccept hello invite tooget created in hello system.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="81f78-226">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="81f78-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="81f78-227">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant tooTeamphoria de son accès.</span><span class="sxs-lookup"><span data-stu-id="81f78-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooTeamphoria.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="81f78-229">**tooassign Britta Simon tooTeamphoria, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="81f78-229">**tooassign Britta Simon tooTeamphoria, perform hello following steps:**</span></span>

1. <span data-ttu-id="81f78-230">Dans le portail de gestion Azure hello, ouvrez la vue des applications hello, puis naviguez toohello les vue de répertoire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="81f78-230">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="81f78-232">Dans la liste des applications hello, sélectionnez **Teamphoria**.</span><span class="sxs-lookup"><span data-stu-id="81f78-232">In hello applications list, select **Teamphoria**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_app.png) 

3. <span data-ttu-id="81f78-234">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="81f78-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="81f78-236">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="81f78-236">Click **Add** button.</span></span> <span data-ttu-id="81f78-237">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="81f78-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="81f78-239">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="81f78-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="81f78-240">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="81f78-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="81f78-241">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="81f78-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="81f78-242">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="81f78-242">Testing single sign-on</span></span>

<span data-ttu-id="81f78-243">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="81f78-243">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="81f78-244">Si vous souhaitez tester vos paramètres d’authentification unique, ouvrez le volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="81f78-244">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="81f78-245">Pour plus d'informations sur le panneau d'accès, consultez [Présentation du panneau d’accès](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="81f78-245">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="81f78-246">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="81f78-246">Additional resources</span></span>

* [<span data-ttu-id="81f78-247">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="81f78-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="81f78-248">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="81f78-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_203.png

