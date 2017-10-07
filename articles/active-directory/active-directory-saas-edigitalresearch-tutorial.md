---
title: "Didacticiel : Intégration d’Azure Active Directory avec eDigitalResearch | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et eDigitalResearch."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: c6b66ea0-16ba-45b4-b550-e81c56262b1f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 6dd3cafb25ef8ede3a4c16902ed8da69cb7b715f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-edigitalresearch"></a><span data-ttu-id="190f2-103">Didacticiel : Intégration d’Azure Active Directory avec eDigitalResearch</span><span class="sxs-lookup"><span data-stu-id="190f2-103">Tutorial: Azure Active Directory integration with eDigitalResearch</span></span>

<span data-ttu-id="190f2-104">Dans ce didacticiel, vous apprendrez comment eDigitalResearch toointegrate avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="190f2-104">In this tutorial, you learn how toointegrate eDigitalResearch with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="190f2-105">Intégration eDigitalResearch à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="190f2-105">Integrating eDigitalResearch with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="190f2-106">Vous pouvez contrôler dans Azure AD qui a accès tooeDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="190f2-106">You can control in Azure AD who has access tooeDigitalResearch.</span></span>
- <span data-ttu-id="190f2-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooeDigitalResearch (Single Sign-On) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="190f2-107">You can enable your users tooautomatically get signed-on tooeDigitalResearch (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="190f2-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="190f2-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="190f2-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="190f2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="190f2-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="190f2-110">Prerequisites</span></span>

<span data-ttu-id="190f2-111">tooconfigure intégration d’Azure AD avec eDigitalResearch, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="190f2-111">tooconfigure Azure AD integration with eDigitalResearch, you need hello following items:</span></span>

- <span data-ttu-id="190f2-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="190f2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="190f2-113">Un abonnement eDigitalResearch pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="190f2-113">A eDigitalResearch single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="190f2-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="190f2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="190f2-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="190f2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="190f2-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="190f2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="190f2-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="190f2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="190f2-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="190f2-118">Scenario description</span></span>
<span data-ttu-id="190f2-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="190f2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="190f2-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="190f2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="190f2-121">Ajout d’eDigitalResearch à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="190f2-121">Adding eDigitalResearch from hello gallery</span></span>
2. <span data-ttu-id="190f2-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="190f2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-edigitalresearch-from-hello-gallery"></a><span data-ttu-id="190f2-123">Ajout d’eDigitalResearch à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="190f2-123">Adding eDigitalResearch from hello gallery</span></span>
<span data-ttu-id="190f2-124">tooconfigure hello intégration d’eDigitalResearch dans Azure AD, vous devez eDigitalResearch tooadd à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="190f2-124">tooconfigure hello integration of eDigitalResearch into Azure AD, you need tooadd eDigitalResearch from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="190f2-125">**eDigitalResearch tooadd à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="190f2-125">**tooadd eDigitalResearch from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="190f2-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="190f2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="190f2-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="190f2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="190f2-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="190f2-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="190f2-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="190f2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="190f2-133">Dans la zone de recherche de hello, tapez **eDigitalResearch**, sélectionnez **eDigitalResearch** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="190f2-133">In hello search box, type **eDigitalResearch**, select **eDigitalResearch** from result panel then click **Add** button tooadd hello application.</span></span>

    ![eDigitalResearch dans la liste des résultats hello](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="190f2-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="190f2-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="190f2-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec eDigitalResearch avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="190f2-136">In this section, you configure and test Azure AD single sign-on with eDigitalResearch based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="190f2-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello eDigitalResearch est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="190f2-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in eDigitalResearch is tooa user in Azure AD.</span></span> <span data-ttu-id="190f2-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans eDigitalResearch doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="190f2-138">In other words, a link relationship between an Azure AD user and hello related user in eDigitalResearch needs toobe established.</span></span>

<span data-ttu-id="190f2-139">Dans eDigitalResearch, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="190f2-139">In eDigitalResearch, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="190f2-140">tooconfigure et test Azure AD l’authentification unique avec eDigitalResearch, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="190f2-140">tooconfigure and test Azure AD single sign-on with eDigitalResearch, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="190f2-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="190f2-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="190f2-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="190f2-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="190f2-143">**[Créer un utilisateur de test eDigitalResearch](#create-a-edigitalresearch-test-user)**  -toohave un homologue de Britta Simon dans eDigitalResearch est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="190f2-143">**[Create a eDigitalResearch test user](#create-a-edigitalresearch-test-user)** - toohave a counterpart of Britta Simon in eDigitalResearch that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="190f2-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="190f2-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="190f2-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="190f2-145">**[Test single sign-on](#test-single-sign-on)**  tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="190f2-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="190f2-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="190f2-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application eDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="190f2-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your eDigitalResearch application.</span></span>

<span data-ttu-id="190f2-148">**tooconfigure Azure AD single sign-on avec eDigitalResearch, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="190f2-148">**tooconfigure Azure AD single sign-on with eDigitalResearch, perform hello following steps:**</span></span>

1. <span data-ttu-id="190f2-149">Bonjour portail Azure, sur hello **eDigitalResearch** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="190f2-149">In hello Azure portal, on hello **eDigitalResearch** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="190f2-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="190f2-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_samlbase.png)

3. <span data-ttu-id="190f2-153">Sur hello **eDigitalResearch domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="190f2-153">On hello **eDigitalResearch Domain and URLs** section, perform hello following steps:</span></span>

    ![Informations d’authentification unique dans eDigitalResearch Domain and URLs (Domaine et URL eDigitalResearch)](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_url.png)

    <span data-ttu-id="190f2-155">a.</span><span class="sxs-lookup"><span data-stu-id="190f2-155">a.</span></span> <span data-ttu-id="190f2-156">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company-name>.edigitalresearch.com`</span><span class="sxs-lookup"><span data-stu-id="190f2-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company-name>.edigitalresearch.com`</span></span>

    <span data-ttu-id="190f2-157">b.</span><span class="sxs-lookup"><span data-stu-id="190f2-157">b.</span></span> <span data-ttu-id="190f2-158">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company-name>.edigitalresearch.com/login/consume`</span><span class="sxs-lookup"><span data-stu-id="190f2-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company-name>.edigitalresearch.com/login/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="190f2-159">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="190f2-159">These values are not real.</span></span> <span data-ttu-id="190f2-160">Mettre à jour ces valeurs hello URL d’identificateur et de réponse réelle.</span><span class="sxs-lookup"><span data-stu-id="190f2-160">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="190f2-161">Contact [équipe de support eDigitalResearch](http://www.maruedr.com/contact) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="190f2-161">Contact [eDigitalResearch support team](http://www.maruedr.com/contact) tooget these values.</span></span>
 


4. <span data-ttu-id="190f2-162">Sur hello **le certificat de signature SAML** , cliquez sur **certificat Base(64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="190f2-162">On hello **SAML Signing Certificate** section, click **Certificate Base(64)** and then save hello certificate file on your computer.</span></span>

    <span data-ttu-id="190f2-163">!</span><span class="sxs-lookup"><span data-stu-id="190f2-163">!</span></span>![lien de téléchargement du certificat Hello](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_certificate.png) 

5. <span data-ttu-id="190f2-165">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="190f2-165">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="190f2-167">Sur hello **eDigitalResearch Configuration** , cliquez sur **configurer eDigitalResearch** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="190f2-167">On hello **eDigitalResearch Configuration** section, click **Configure eDigitalResearch** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="190f2-168">Hello de copie **URL de déconnexion, l’ID d’entité SAML** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="190f2-168">Copy hello **Sign-Out URL, SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Configuration d’eDigitalResearch](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_configure.png) 

7. <span data-ttu-id="190f2-170">tooconfigure l’authentification unique sur **eDigitalResearch** côté, vous devez hello toosend téléchargé **fichier de certificat (Base64)**, **ID d’entité SAML**, et  **URL de déconnexion** trop[équipe de support eDigitalResearch](http://www.maruedr.com/contact).</span><span class="sxs-lookup"><span data-stu-id="190f2-170">tooconfigure single sign-on on **eDigitalResearch** side, you need toosend hello downloaded **Certificate (Base64) File**, **SAML Entity ID**, and **Sign-Out URL** too[eDigitalResearch support team](http://www.maruedr.com/contact).</span></span> <span data-ttu-id="190f2-171">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="190f2-171">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="190f2-172">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="190f2-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="190f2-173">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="190f2-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="190f2-174">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="190f2-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="190f2-175">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="190f2-175">Create an Azure AD test user</span></span>

<span data-ttu-id="190f2-176">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="190f2-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="190f2-178">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="190f2-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="190f2-179">Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="190f2-179">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="190f2-181">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="190f2-181">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="190f2-183">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="190f2-183">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![bouton Ajouter de Hello](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="190f2-185">Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="190f2-185">In hello **User** dialog box, perform hello following steps:</span></span>

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_04.png)

    <span data-ttu-id="190f2-187">a.</span><span class="sxs-lookup"><span data-stu-id="190f2-187">a.</span></span> <span data-ttu-id="190f2-188">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="190f2-188">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="190f2-189">b.</span><span class="sxs-lookup"><span data-stu-id="190f2-189">b.</span></span> <span data-ttu-id="190f2-190">Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="190f2-190">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="190f2-191">c.</span><span class="sxs-lookup"><span data-stu-id="190f2-191">c.</span></span> <span data-ttu-id="190f2-192">Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="190f2-192">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="190f2-193">d.</span><span class="sxs-lookup"><span data-stu-id="190f2-193">d.</span></span> <span data-ttu-id="190f2-194">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="190f2-194">Click **Create**.</span></span>
  
### <a name="create-a-edigitalresearch-test-user"></a><span data-ttu-id="190f2-195">Créer un utilisateur de test eDigitalResearch</span><span class="sxs-lookup"><span data-stu-id="190f2-195">Create a eDigitalResearch test user</span></span>

<span data-ttu-id="190f2-196">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans eDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="190f2-196">hello objective of this section is toocreate a user called Britta Simon in eDigitalResearch.</span></span> 

<span data-ttu-id="190f2-197">Travailler avec hello [équipe de support eDigitalResearch](http://www.maruedr.com/contact) tooget les utilisateurs créés.</span><span class="sxs-lookup"><span data-stu-id="190f2-197">Work with hello [eDigitalResearch support team](http://www.maruedr.com/contact) tooget users created.</span></span>       
    
 > [!NOTE]
 > <span data-ttu-id="190f2-198">titulaire du compte Azure Active Directory Hello reçoit un message électronique et suit un tooconfirm de lier leur compte avant son activation.</span><span class="sxs-lookup"><span data-stu-id="190f2-198">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="190f2-199">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="190f2-199">Assign hello Azure AD test user</span></span>

<span data-ttu-id="190f2-200">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooeDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="190f2-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooeDigitalResearch.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="190f2-202">**tooassign Britta Simon tooeDigitalResearch, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="190f2-202">**tooassign Britta Simon tooeDigitalResearch, perform hello following steps:**</span></span>

1. <span data-ttu-id="190f2-203">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="190f2-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="190f2-205">Dans la liste des applications hello, sélectionnez **eDigitalResearch**.</span><span class="sxs-lookup"><span data-stu-id="190f2-205">In hello applications list, select **eDigitalResearch**.</span></span>

    ![lien d’eDigitalResearch Hello dans la liste des Applications hello](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_app.png)  

3. <span data-ttu-id="190f2-207">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="190f2-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202]

4. <span data-ttu-id="190f2-209">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="190f2-209">Click **Add** button.</span></span> <span data-ttu-id="190f2-210">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="190f2-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="190f2-212">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="190f2-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="190f2-213">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="190f2-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="190f2-214">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="190f2-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="190f2-215">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="190f2-215">Test single sign-on</span></span>

<span data-ttu-id="190f2-216">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="190f2-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="190f2-217">Lorsque vous cliquez sur mosaïque eDigitalResearch hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour eDigitalResearch application.</span><span class="sxs-lookup"><span data-stu-id="190f2-217">When you click hello eDigitalResearch tile in hello Access Panel, you should get automatically signed-on tooyour eDigitalResearch application.</span></span>
<span data-ttu-id="190f2-218">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="190f2-218">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="190f2-219">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="190f2-219">Additional resources</span></span>

* [<span data-ttu-id="190f2-220">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="190f2-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="190f2-221">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="190f2-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_203.png

