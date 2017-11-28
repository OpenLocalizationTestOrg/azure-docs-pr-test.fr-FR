---
title: "Didacticiel : Intégration d’Azure Active Directory à BGS Online | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et BGS en ligne."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4fd6b29b-1b46-4fd1-9f5e-16b1c9d892cd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: b728606ded7687d424a8175d0602b6b00f398497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bgs-online"></a><span data-ttu-id="a7049-103">Didacticiel : Intégration d’Azure Active Directory à BGS Online</span><span class="sxs-lookup"><span data-stu-id="a7049-103">Tutorial: Azure Active Directory integration with BGS Online</span></span>

<span data-ttu-id="a7049-104">Dans ce didacticiel, vous apprendrez comment toointegrate BGS Online avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a7049-104">In this tutorial, you learn how toointegrate BGS Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a7049-105">Intégration BGS Online à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="a7049-105">Integrating BGS Online with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a7049-106">Vous pouvez contrôler dans Azure AD qui a accès tooBGS en ligne</span><span class="sxs-lookup"><span data-stu-id="a7049-106">You can control in Azure AD who has access tooBGS Online</span></span>
- <span data-ttu-id="a7049-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooBGS en ligne (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7049-107">You can enable your users tooautomatically get signed-on tooBGS Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a7049-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="a7049-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a7049-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a7049-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7049-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a7049-110">Prerequisites</span></span>

<span data-ttu-id="a7049-111">tooconfigure intégration d’Azure AD avec BGS en ligne, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a7049-111">tooconfigure Azure AD integration with BGS Online, you need hello following items:</span></span>

- <span data-ttu-id="a7049-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7049-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a7049-113">Un abonnement BGS Online pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="a7049-113">A BGS Online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a7049-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="a7049-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a7049-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="a7049-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a7049-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="a7049-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a7049-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a7049-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a7049-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="a7049-118">Scenario description</span></span>
<span data-ttu-id="a7049-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="a7049-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a7049-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="a7049-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a7049-121">Ajout de BGS en ligne à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="a7049-121">Adding BGS Online from hello gallery</span></span>
2. <span data-ttu-id="a7049-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7049-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bgs-online-from-hello-gallery"></a><span data-ttu-id="a7049-123">Ajout de BGS en ligne à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="a7049-123">Adding BGS Online from hello gallery</span></span>
<span data-ttu-id="a7049-124">intégration de hello tooconfigure BGS en ligne dans Azure AD, vous devez tooadd BGS en ligne à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="a7049-124">tooconfigure hello integration of BGS Online into Azure AD, you need tooadd BGS Online from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a7049-125">**tooadd BGS Online à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a7049-125">**tooadd BGS Online from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a7049-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="a7049-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a7049-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="a7049-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a7049-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a7049-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="a7049-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a7049-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="a7049-133">Dans la zone de recherche de hello, tapez **BGS Online**.</span><span class="sxs-lookup"><span data-stu-id="a7049-133">In hello search box, type **BGS Online**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_search.png)

5. <span data-ttu-id="a7049-135">Dans le volet de résultats hello, sélectionnez **BGS en ligne**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="a7049-135">In hello results panel, select **BGS Online**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a7049-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7049-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a7049-138">Dans cette section, vous configurez et testez l’authentification unique Azure AD avec BGS Online au moyen d’un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="a7049-138">In this section, you configure and test Azure AD single sign-on with BGS Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a7049-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans BGS en ligne est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7049-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BGS Online is tooa user in Azure AD.</span></span> <span data-ttu-id="a7049-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans BGS en ligne doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="a7049-140">In other words, a link relationship between an Azure AD user and hello related user in BGS Online needs toobe established.</span></span>

<span data-ttu-id="a7049-141">Dans la ligne BGS, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="a7049-141">In BGS Online, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a7049-142">tooconfigure et test Azure AD l’authentification unique avec BGS en ligne, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="a7049-142">tooconfigure and test Azure AD single sign-on with BGS Online, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a7049-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="a7049-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a7049-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a7049-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a7049-145">**[Création d’un utilisateur de test en ligne de BGS](#creating-a-bgs-online-test-user)**  -toohave un équivalent de Britta Simon dans BGS en ligne qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a7049-145">**[Creating a BGS Online test user](#creating-a-bgs-online-test-user)** - toohave a counterpart of Britta Simon in BGS Online that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a7049-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="a7049-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a7049-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="a7049-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a7049-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7049-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a7049-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application BGS en ligne.</span><span class="sxs-lookup"><span data-stu-id="a7049-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BGS Online application.</span></span>

<span data-ttu-id="a7049-150">**tooconfigure Azure AD single sign-on avec BGS Online, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a7049-150">**tooconfigure Azure AD single sign-on with BGS Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="a7049-151">Bonjour portail Azure, sur hello **BGS en ligne** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="a7049-151">In hello Azure portal, on hello **BGS Online** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="a7049-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="a7049-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_samlbase.png)

3. <span data-ttu-id="a7049-155">Sur hello **URL et domaine en ligne de BGS** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="a7049-155">On hello **BGS Online Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_url.png)

    <span data-ttu-id="a7049-157">a.</span><span class="sxs-lookup"><span data-stu-id="a7049-157">a.</span></span> <span data-ttu-id="a7049-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :</span><span class="sxs-lookup"><span data-stu-id="a7049-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>

    <span data-ttu-id="a7049-159">Pour un environnement de production, utilisez ce modèle `https://<company name>.millwardbrown.report`</span><span class="sxs-lookup"><span data-stu-id="a7049-159">For production environment, use this pattern `https://<company name>.millwardbrown.report`</span></span> 

    <span data-ttu-id="a7049-160">Pour un environnement de test, utilisez ce modèle `https://millwardbrown.marketingtracker.nl/mt5/`</span><span class="sxs-lookup"><span data-stu-id="a7049-160">For test environment, use this pattern `https://millwardbrown.marketingtracker.nl/mt5/`</span></span>

    <span data-ttu-id="a7049-161">b.</span><span class="sxs-lookup"><span data-stu-id="a7049-161">b.</span></span> <span data-ttu-id="a7049-162">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :</span><span class="sxs-lookup"><span data-stu-id="a7049-162">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    
    <span data-ttu-id="a7049-163">Pour un environnement de production, utilisez ce modèle `https://<company name>.millwardbrown.report/sso/saml/AssertionConsumerService.aspx`</span><span class="sxs-lookup"><span data-stu-id="a7049-163">For production environment, use this pattern `https://<company name>.millwardbrown.report/sso/saml/AssertionConsumerService.aspx`</span></span> 
      
    <span data-ttu-id="a7049-164">Pour un environnement de test, utilisez ce modèle `https://millwardbrown.marketingtracker.nl/mt5/sso/saml/AssertionConsumerService.aspx`</span><span class="sxs-lookup"><span data-stu-id="a7049-164">For test environment, use this pattern `https://millwardbrown.marketingtracker.nl/mt5/sso/saml/AssertionConsumerService.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a7049-165">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="a7049-165">These values are not real.</span></span> <span data-ttu-id="a7049-166">Mettre à jour ces valeurs hello URL d’identificateur et de réponse réelle.</span><span class="sxs-lookup"><span data-stu-id="a7049-166">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="a7049-167">Contact [équipe de support en ligne de BGS](mailTo:bgsdashboardteam@millwardbrown.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="a7049-167">Contact [BGS Online support team](mailTo:bgsdashboardteam@millwardbrown.com) tooget these values.</span></span>
 

4. <span data-ttu-id="a7049-168">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="a7049-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_certificate.png) 

5. <span data-ttu-id="a7049-170">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="a7049-170">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bgsonline-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a7049-172">Sur hello **Configuration en ligne de BGS** , cliquez sur **configurer un en ligne BGS** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="a7049-172">On hello **BGS Online Configuration** section, click **Configure BGS Online** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a7049-173">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="a7049-173">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_configure.png) 

7. <span data-ttu-id="a7049-175">tooconfigure l’authentification unique sur **BGS en ligne** côté, vous devez hello toosend téléchargé **Metadata XML** et **SAML Sign-On URL du Service unique** trop[BGS Équipe de support en ligne](mailto:bgsdashboardteam@millwardbrown.com).</span><span class="sxs-lookup"><span data-stu-id="a7049-175">tooconfigure single sign-on on **BGS Online** side, you need toosend hello downloaded **Metadata XML** and **SAML Single Sign-On Service URL** too[BGS Online support team](mailto:bgsdashboardteam@millwardbrown.com).</span></span> 


> [!TIP]
> <span data-ttu-id="a7049-176">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="a7049-176">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a7049-177">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="a7049-177">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a7049-178">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a7049-178">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a7049-179">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7049-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="a7049-180">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="a7049-180">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="a7049-182">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a7049-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a7049-183">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="a7049-183">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a7049-185">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="a7049-185">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a7049-187">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="a7049-187">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a7049-189">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="a7049-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a7049-191">a.</span><span class="sxs-lookup"><span data-stu-id="a7049-191">a.</span></span> <span data-ttu-id="a7049-192">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a7049-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a7049-193">b.</span><span class="sxs-lookup"><span data-stu-id="a7049-193">b.</span></span> <span data-ttu-id="a7049-194">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a7049-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a7049-195">c.</span><span class="sxs-lookup"><span data-stu-id="a7049-195">c.</span></span> <span data-ttu-id="a7049-196">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="a7049-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a7049-197">d.</span><span class="sxs-lookup"><span data-stu-id="a7049-197">d.</span></span> <span data-ttu-id="a7049-198">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="a7049-198">Click **Create**.</span></span>
 
### <a name="creating-a-bgs-online-test-user"></a><span data-ttu-id="a7049-199">Création d’un utilisateur de test BGS Online</span><span class="sxs-lookup"><span data-stu-id="a7049-199">Creating a BGS Online test user</span></span>

<span data-ttu-id="a7049-200">Dans cette section, vous allez créer un utilisateur nommé Britta Simon dans BGS Online.</span><span class="sxs-lookup"><span data-stu-id="a7049-200">In this section, you create a user called Britta Simon in BGS Online.</span></span> <span data-ttu-id="a7049-201">Travailler avec [équipe de support en ligne de BGS](mailto:bgsdashboardteam@millwardbrown.com) tooadd les utilisateurs de hello dans la plateforme de BGS en ligne hello.</span><span class="sxs-lookup"><span data-stu-id="a7049-201">Work with [BGS Online support team](mailto:bgsdashboardteam@millwardbrown.com) tooadd hello users in hello BGS Online platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a7049-202">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7049-202">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a7049-203">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant tooBGS accès en ligne.</span><span class="sxs-lookup"><span data-stu-id="a7049-203">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBGS Online.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="a7049-205">**tooassign tooBGS Britta Simon en ligne, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a7049-205">**tooassign Britta Simon tooBGS Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="a7049-206">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a7049-206">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="a7049-208">Dans la liste des applications hello, sélectionnez **BGS Online**.</span><span class="sxs-lookup"><span data-stu-id="a7049-208">In hello applications list, select **BGS Online**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_app.png) 

3. <span data-ttu-id="a7049-210">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a7049-210">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="a7049-212">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="a7049-212">Click **Add** button.</span></span> <span data-ttu-id="a7049-213">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a7049-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="a7049-215">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="a7049-215">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a7049-216">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a7049-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a7049-217">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a7049-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a7049-218">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="a7049-218">Testing single sign-on</span></span>

<span data-ttu-id="a7049-219">Dans cette section, vous tester votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="a7049-219">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="a7049-220">Lorsque vous cliquez sur mosaïque BGS en ligne hello hello volet d’accès, vous devez obtenir tooyour automatiquement signé sur les applications BGS en ligne.</span><span class="sxs-lookup"><span data-stu-id="a7049-220">When you click hello BGS Online tile in hello Access Panel, you should get automatically signed-on tooyour BGS Online application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a7049-221">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="a7049-221">Additional resources</span></span>

* [<span data-ttu-id="a7049-222">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a7049-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a7049-223">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="a7049-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_203.png

