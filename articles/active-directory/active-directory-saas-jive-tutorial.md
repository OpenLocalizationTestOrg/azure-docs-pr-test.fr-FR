---
title: "Didacticiel : Intégration d’Azure Active Directory à Jive | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Jive."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9fc5659a-c116-4a1b-a601-333325a26b46
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: f22bf78a55e8a4a9ea2f0020ef2f535be88b6302
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jive"></a><span data-ttu-id="036cd-103">Didacticiel : Intégration d’Azure Active Directory avec Jive</span><span class="sxs-lookup"><span data-stu-id="036cd-103">Tutorial: Azure Active Directory integration with Jive</span></span>

<span data-ttu-id="036cd-104">Dans ce didacticiel, vous apprendrez comment toointegrate Jive avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="036cd-104">In this tutorial, you learn how toointegrate Jive with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="036cd-105">Intégration Jive à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="036cd-105">Integrating Jive with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="036cd-106">Vous pouvez contrôler dans Azure AD qui a accès tooJive</span><span class="sxs-lookup"><span data-stu-id="036cd-106">You can control in Azure AD who has access tooJive</span></span>
- <span data-ttu-id="036cd-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooJive (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="036cd-107">You can enable your users tooautomatically get signed-on tooJive (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="036cd-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="036cd-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="036cd-109">Si vous souhaitez tooknow plus d’informations sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="036cd-109">If you want tooknow more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="036cd-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="036cd-110">Prerequisites</span></span>

<span data-ttu-id="036cd-111">tooconfigure intégration d’Azure AD à Jive, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="036cd-111">tooconfigure Azure AD integration with Jive, you need hello following items:</span></span>

- <span data-ttu-id="036cd-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="036cd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="036cd-113">Un abonnement Jive pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="036cd-113">A Jive single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="036cd-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="036cd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="036cd-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="036cd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="036cd-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="036cd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="036cd-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="036cd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="036cd-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="036cd-118">Scenario description</span></span>
<span data-ttu-id="036cd-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="036cd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="036cd-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="036cd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="036cd-121">Ajout de Jive à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="036cd-121">Adding Jive from hello gallery</span></span>
2. <span data-ttu-id="036cd-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="036cd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jive-from-hello-gallery"></a><span data-ttu-id="036cd-123">Ajout de Jive à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="036cd-123">Adding Jive from hello gallery</span></span>
<span data-ttu-id="036cd-124">intégration de hello tooconfigure de Jive dans Azure AD, vous devez tooadd Jive à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="036cd-124">tooconfigure hello integration of Jive into Azure AD, you need tooadd Jive from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="036cd-125">**tooadd Jive à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="036cd-125">**tooadd Jive from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="036cd-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="036cd-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="036cd-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="036cd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="036cd-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="036cd-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="036cd-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="036cd-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="036cd-133">Dans la zone de recherche de hello, tapez **Jive**.</span><span class="sxs-lookup"><span data-stu-id="036cd-133">In hello search box, type **Jive**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jive-tutorial/tutorial_jive_search.png)

5. <span data-ttu-id="036cd-135">Dans le volet de résultats hello, sélectionnez **Jive**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="036cd-135">In hello results panel, select **Jive**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jive-tutorial/tutorial_jive_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="036cd-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="036cd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="036cd-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Jive avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="036cd-138">In this section, you configure and test Azure AD single sign-on with Jive based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="036cd-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Jive est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="036cd-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Jive is tooa user in Azure AD.</span></span> <span data-ttu-id="036cd-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Jive doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="036cd-140">In other words, a link relationship between an Azure AD user and hello related user in Jive needs toobe established.</span></span>

<span data-ttu-id="036cd-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Jive.</span><span class="sxs-lookup"><span data-stu-id="036cd-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Jive.</span></span>

<span data-ttu-id="036cd-142">tooconfigure et test Azure AD l’authentification unique à Jive, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="036cd-142">tooconfigure and test Azure AD single sign-on with Jive, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="036cd-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="036cd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="036cd-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="036cd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="036cd-145">**[Création d’un utilisateur de test Jive](#creating-a-jive-test-user)**  -toohave un équivalent de Britta Simon dans Jive est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="036cd-145">**[Creating a Jive test user](#creating-a-jive-test-user)** - toohave a counterpart of Britta Simon in Jive that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="036cd-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="036cd-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="036cd-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="036cd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="036cd-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="036cd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="036cd-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de Jive.</span><span class="sxs-lookup"><span data-stu-id="036cd-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Jive application.</span></span>

<span data-ttu-id="036cd-150">**tooconfigure Azure AD l’authentification unique à Jive, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="036cd-150">**tooconfigure Azure AD single sign-on with Jive, perform hello following steps:**</span></span>

1. <span data-ttu-id="036cd-151">Bonjour portail Azure, sur hello **Jive** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="036cd-151">In hello Azure portal, on hello **Jive** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="036cd-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="036cd-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-jive-tutorial/tutorial_jive_samlbase.png)

3. <span data-ttu-id="036cd-155">Sur hello **Jive domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="036cd-155">On hello **Jive Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jive-tutorial/tutorial_jive_url.png)

    <span data-ttu-id="036cd-157">a.</span><span class="sxs-lookup"><span data-stu-id="036cd-157">a.</span></span> <span data-ttu-id="036cd-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<instance name>.jivecustom.com`</span><span class="sxs-lookup"><span data-stu-id="036cd-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instance name>.jivecustom.com`</span></span>

    <span data-ttu-id="036cd-159">b.</span><span class="sxs-lookup"><span data-stu-id="036cd-159">b.</span></span> <span data-ttu-id="036cd-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<instance name>.jiveon.com`</span><span class="sxs-lookup"><span data-stu-id="036cd-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instance name>.jiveon.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="036cd-161">Ces valeurs ne sont pas hello réel.</span><span class="sxs-lookup"><span data-stu-id="036cd-161">These values are not hello real.</span></span> <span data-ttu-id="036cd-162">Mettre à jour ces valeurs avec l’URL de connexion réel hello et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="036cd-162">Update these values with hello actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="036cd-163">Contact [équipe de support Client de Jive](https://www.jivesoftware.com/services-support/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="036cd-163">Contact [Jive Client support team](https://www.jivesoftware.com/services-support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="036cd-164">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier XML de hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="036cd-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jive-tutorial/tutorial_jive_certificate.png) 

5. <span data-ttu-id="036cd-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="036cd-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jive-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="036cd-168">tooconfigure l’authentification unique sur **Jive** client Jive de tooyour part, la session en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="036cd-168">tooconfigure single sign-on on **Jive** side, sign-on tooyour Jive tenant as an administrator.</span></span>

7. <span data-ttu-id="036cd-169">Dans le menu hello haut de hello, cliquez sur «**Saml**. »</span><span class="sxs-lookup"><span data-stu-id="036cd-169">In hello menu on hello top, Click "**Saml**."</span></span>

    ![Configurer l’authentification unique côté application](./media/active-directory-saas-jive-tutorial/tutorial_jive_002.png)

    <span data-ttu-id="036cd-171">a.</span><span class="sxs-lookup"><span data-stu-id="036cd-171">a.</span></span> <span data-ttu-id="036cd-172">Sélectionnez **activé** sous hello **général** onglet.</span><span class="sxs-lookup"><span data-stu-id="036cd-172">Select **Enabled** under hello **General** tab.</span></span>   
    <span data-ttu-id="036cd-173">b.</span><span class="sxs-lookup"><span data-stu-id="036cd-173">b.</span></span> <span data-ttu-id="036cd-174">Cliquez sur hello »**enregistrer tous les paramètres saml**» bouton.</span><span class="sxs-lookup"><span data-stu-id="036cd-174">Click hello "**Save all saml settings**" button.</span></span>

8. <span data-ttu-id="036cd-175">Accédez toohello «**Idp Metadata**« onglet.</span><span class="sxs-lookup"><span data-stu-id="036cd-175">Navigate toohello "**Idp Metadata**" tab.</span></span>
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-jive-tutorial/tutorial_jive_003.png)
   
    <span data-ttu-id="036cd-177">a.</span><span class="sxs-lookup"><span data-stu-id="036cd-177">a.</span></span> <span data-ttu-id="036cd-178">Copier le contenu du fichier XML de métadonnées téléchargé de hello hello et collez-le à hello **métadonnées du fournisseur d’identité (IDP)** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="036cd-178">Copy hello content of hello downloaded metadata XML file, and then paste it into hello **Identity Provider (IDP) Metadata** textbox.</span></span>
    
    <span data-ttu-id="036cd-179">b.</span><span class="sxs-lookup"><span data-stu-id="036cd-179">b.</span></span> <span data-ttu-id="036cd-180">Cliquez sur hello »**enregistrer tous les paramètres saml**» bouton.</span><span class="sxs-lookup"><span data-stu-id="036cd-180">Click hello "**Save all saml settings**" button.</span></span> 

9. <span data-ttu-id="036cd-181">Accédez toohello «**un mappage d’attribut utilisateur**« onglet.</span><span class="sxs-lookup"><span data-stu-id="036cd-181">Go toohello "**User Attribute Mapping**" tab.</span></span>
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-jive-tutorial/tutorial_jive_004.png)
   
    <span data-ttu-id="036cd-183">a.</span><span class="sxs-lookup"><span data-stu-id="036cd-183">a.</span></span> <span data-ttu-id="036cd-184">Bonjour **messagerie** zone de texte, copiez et collez nom d’attribut hello de **mail** valeur.</span><span class="sxs-lookup"><span data-stu-id="036cd-184">In hello **Email** textbox, copy and paste hello attribute name of **mail** value.</span></span>
   
    <span data-ttu-id="036cd-185">b.</span><span class="sxs-lookup"><span data-stu-id="036cd-185">b.</span></span> <span data-ttu-id="036cd-186">Bonjour **prénom** zone de texte, copiez et collez nom d’attribut hello de **givenname** valeur.</span><span class="sxs-lookup"><span data-stu-id="036cd-186">In hello **First Name** textbox, copy and paste hello attribute name of **givenname** value.</span></span>
   
    <span data-ttu-id="036cd-187">c.</span><span class="sxs-lookup"><span data-stu-id="036cd-187">c.</span></span> <span data-ttu-id="036cd-188">Bonjour **nom** zone de texte, copiez et collez nom d’attribut hello de **surname** valeur.</span><span class="sxs-lookup"><span data-stu-id="036cd-188">In hello **Last Name** textbox, copy and paste hello attribute name of **surname** value.</span></span>

> [!TIP]
> <span data-ttu-id="036cd-189">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="036cd-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="036cd-190">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="036cd-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="036cd-191">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="036cd-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="036cd-192">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="036cd-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="036cd-193">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="036cd-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="036cd-195">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="036cd-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="036cd-196">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="036cd-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jive-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="036cd-198">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="036cd-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jive-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="036cd-200">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="036cd-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jive-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="036cd-202">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="036cd-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jive-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="036cd-204">a.</span><span class="sxs-lookup"><span data-stu-id="036cd-204">a.</span></span> <span data-ttu-id="036cd-205">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="036cd-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="036cd-206">b.</span><span class="sxs-lookup"><span data-stu-id="036cd-206">b.</span></span> <span data-ttu-id="036cd-207">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="036cd-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="036cd-208">c.</span><span class="sxs-lookup"><span data-stu-id="036cd-208">c.</span></span> <span data-ttu-id="036cd-209">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="036cd-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="036cd-210">d.</span><span class="sxs-lookup"><span data-stu-id="036cd-210">d.</span></span> <span data-ttu-id="036cd-211">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="036cd-211">Click **Create**.</span></span>
 
### <a name="creating-a-jive-test-user"></a><span data-ttu-id="036cd-212">Création d’un utilisateur de test Jive</span><span class="sxs-lookup"><span data-stu-id="036cd-212">Creating a Jive test user</span></span>

<span data-ttu-id="036cd-213">Travailler avec [équipe de support Client de Jive](https://www.jivesoftware.com/services-support/) tooadd les utilisateurs de hello dans la plateforme de Jive hello.</span><span class="sxs-lookup"><span data-stu-id="036cd-213">Work with [Jive Client support team](https://www.jivesoftware.com/services-support/) tooadd hello users in hello Jive platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="036cd-214">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="036cd-214">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="036cd-215">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooJive.</span><span class="sxs-lookup"><span data-stu-id="036cd-215">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJive.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="036cd-217">**tooassign Britta Simon tooJive, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="036cd-217">**tooassign Britta Simon tooJive, perform hello following steps:**</span></span>

1. <span data-ttu-id="036cd-218">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="036cd-218">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="036cd-220">Dans la liste des applications hello, sélectionnez **Jive**.</span><span class="sxs-lookup"><span data-stu-id="036cd-220">In hello applications list, select **Jive**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jive-tutorial/tutorial_jive_app.png) 

3. <span data-ttu-id="036cd-222">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="036cd-222">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="036cd-224">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="036cd-224">Click **Add** button.</span></span> <span data-ttu-id="036cd-225">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="036cd-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="036cd-227">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="036cd-227">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="036cd-228">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="036cd-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="036cd-229">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="036cd-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="036cd-230">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="036cd-230">Testing single sign-on</span></span>

<span data-ttu-id="036cd-231">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="036cd-231">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="036cd-232">Lorsque vous cliquez sur mosaïque Jive hello hello volet d’accès, vous devez obtenir l’application de Jive automatiquement signé sur tooyour.</span><span class="sxs-lookup"><span data-stu-id="036cd-232">When you click hello Jive tile in hello Access Panel, you should get automatically signed-on tooyour Jive application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="036cd-233">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="036cd-233">Additional resources</span></span>

* [<span data-ttu-id="036cd-234">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="036cd-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="036cd-235">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="036cd-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="036cd-236">Configurer l’approvisionnement de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="036cd-236">Configure User Provisioning</span></span>](active-directory-saas-jive-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jive-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jive-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jive-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jive-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jive-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jive-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jive-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jive-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jive-tutorial/tutorial_general_203.png

