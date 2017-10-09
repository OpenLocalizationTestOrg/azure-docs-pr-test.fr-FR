---
title: "Didacticiel : Intégration d’Azure Active Directory à O.C. Tanner - AppreciateHub | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et O.C. Tanner - AppreciateHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dee8fbca-0b60-4a21-8917-1fb6919de5a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: 45052cf56e35746d7df5910162e40e3bbcad1aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-oc-tanner---appreciatehub"></a><span data-ttu-id="dd6ee-105">Didacticiel : Intégration d’Azure Active Directory à O.C.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-105">Tutorial: Azure Active Directory integration with O.C.</span></span> <span data-ttu-id="dd6ee-106">Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-106">Tanner - AppreciateHub</span></span>

<span data-ttu-id="dd6ee-107">Dans ce didacticiel, vous apprendrez comment toointegrate O.C.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-107">In this tutorial, you learn how toointegrate O.C.</span></span> <span data-ttu-id="dd6ee-108">Tanner - AppreciateHub à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dd6ee-108">Tanner - AppreciateHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dd6ee-109">L’intégration d’O.C.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-109">Integrating O.C.</span></span> <span data-ttu-id="dd6ee-110">Tanner - AppreciateHub avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="dd6ee-110">Tanner - AppreciateHub with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="dd6ee-111">Vous pouvez contrôler dans Azure AD qui a accès tooO.C.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-111">You can control in Azure AD who has access tooO.C.</span></span> <span data-ttu-id="dd6ee-112">Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-112">Tanner - AppreciateHub</span></span>
- <span data-ttu-id="dd6ee-113">Vous pouvez activer vos utilisateurs tooautomatically get signé sur tooO.C.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-113">You can enable your users tooautomatically get signed-on tooO.C.</span></span> <span data-ttu-id="dd6ee-114">Tanner - AppreciateHub (par le biais de l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-114">Tanner - AppreciateHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dd6ee-115">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="dd6ee-115">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="dd6ee-116">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dd6ee-116">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd6ee-117">Composants requis</span><span class="sxs-lookup"><span data-stu-id="dd6ee-117">Prerequisites</span></span>

<span data-ttu-id="dd6ee-118">intégration d’Azure AD avec O.C. de tooconfigure</span><span class="sxs-lookup"><span data-stu-id="dd6ee-118">tooconfigure Azure AD integration with O.C.</span></span> <span data-ttu-id="dd6ee-119">Tanner - AppreciateHub, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="dd6ee-119">Tanner - AppreciateHub, you need hello following items:</span></span>

- <span data-ttu-id="dd6ee-120">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd6ee-120">An Azure AD subscription</span></span>
- <span data-ttu-id="dd6ee-121">Un abonnement O.C.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-121">A O.C.</span></span> <span data-ttu-id="dd6ee-122">Un abonnement Tanner - AppreciateHub pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="dd6ee-122">Tanner - AppreciateHub single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dd6ee-123">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-123">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dd6ee-124">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="dd6ee-124">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dd6ee-125">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-125">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dd6ee-126">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dd6ee-126">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dd6ee-127">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="dd6ee-127">Scenario description</span></span>
<span data-ttu-id="dd6ee-128">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-128">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dd6ee-129">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="dd6ee-129">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dd6ee-130">Ajout d’O.C.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-130">Adding O.C.</span></span> <span data-ttu-id="dd6ee-131">Tanner - AppreciateHub à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="dd6ee-131">Tanner - AppreciateHub from hello gallery</span></span>
2. <span data-ttu-id="dd6ee-132">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd6ee-132">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-oc-tanner---appreciatehub-from-hello-gallery"></a><span data-ttu-id="dd6ee-133">Ajout d’O.C.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-133">Adding O.C.</span></span> <span data-ttu-id="dd6ee-134">Tanner - AppreciateHub à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="dd6ee-134">Tanner - AppreciateHub from hello gallery</span></span>
<span data-ttu-id="dd6ee-135">intégration de hello tooconfigure de O.C.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-135">tooconfigure hello integration of O.C.</span></span> <span data-ttu-id="dd6ee-136">Tanner - AppreciateHub dans Azure AD, vous devez tooadd O.C.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-136">Tanner - AppreciateHub into Azure AD, you need tooadd O.C.</span></span> <span data-ttu-id="dd6ee-137">Tanner - AppreciateHub à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-137">Tanner - AppreciateHub from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="dd6ee-138">**tooadd O.C. Tanner - AppreciateHub à partir de la galerie hello, effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dd6ee-138">**tooadd O.C. Tanner - AppreciateHub from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="dd6ee-139">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-139">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dd6ee-141">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-141">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="dd6ee-142">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-142">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="dd6ee-144">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-144">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="dd6ee-146">Dans la zone de recherche de hello, tapez **O.C. Tanner - AppreciateHub**.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-146">In hello search box, type **O.C. Tanner - AppreciateHub**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_search.png)

5. <span data-ttu-id="dd6ee-148">Dans le volet de résultats hello, sélectionnez **O.C. Tanner - AppreciateHub**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-148">In hello results panel, select **O.C. Tanner - AppreciateHub**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dd6ee-150">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd6ee-150">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dd6ee-151">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec O.C.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-151">In this section, you configure and test Azure AD single sign-on with O.C.</span></span> <span data-ttu-id="dd6ee-152">Tanner - AppreciateHub au moyen d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="dd6ee-152">Tanner - AppreciateHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dd6ee-153">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans O.C.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-153">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in O.C.</span></span> <span data-ttu-id="dd6ee-154">Tanner - AppreciateHub est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-154">Tanner - AppreciateHub is tooa user in Azure AD.</span></span> <span data-ttu-id="dd6ee-155">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans O.C.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-155">In other words, a link relationship between an Azure AD user and hello related user in O.C.</span></span> <span data-ttu-id="dd6ee-156">Tanner - AppreciateHub doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-156">Tanner - AppreciateHub needs toobe established.</span></span>

<span data-ttu-id="dd6ee-157">Dans O.C.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-157">In O.C.</span></span> <span data-ttu-id="dd6ee-158">Valeur hello Tanner - AppreciateHub, affecter hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-158">Tanner - AppreciateHub, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="dd6ee-159">tooconfigure et test Azure AD l’authentification unique avec O.C.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-159">tooconfigure and test Azure AD single sign-on with O.C.</span></span> <span data-ttu-id="dd6ee-160">Tanner - AppreciateHub, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="dd6ee-160">Tanner - AppreciateHub, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="dd6ee-161">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-161">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="dd6ee-162">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-162">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dd6ee-163">**[Création d’un utilisateur de test O.C. Tanner - utilisateur de test AppreciateHub](#creating-a-oc-tanner---appreciatehub-test-user)**  -toohave un équivalent de Britta Simon dans O.C.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-163">**[Creating a O.C. Tanner - AppreciateHub test user](#creating-a-oc-tanner---appreciatehub-test-user)** - toohave a counterpart of Britta Simon in O.C.</span></span> <span data-ttu-id="dd6ee-164">Tanner - AppreciateHub est lié toohello la représentation sous forme de Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-164">Tanner - AppreciateHub that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="dd6ee-165">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-165">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dd6ee-166">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-166">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dd6ee-167">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd6ee-167">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dd6ee-168">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurer l’authentification unique dans votre O.C.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-168">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your O.C.</span></span> <span data-ttu-id="dd6ee-169">Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-169">Tanner - AppreciateHub application.</span></span>

<span data-ttu-id="dd6ee-170">**tooconfigure Azure AD single sign-on avec O.C. Tanner - AppreciateHub, effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dd6ee-170">**tooconfigure Azure AD single sign-on with O.C. Tanner - AppreciateHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="dd6ee-171">Bonjour portail Azure, sur hello **O.C. Tanner - AppreciateHub** cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-171">In hello Azure portal, on hello **O.C. Tanner - AppreciateHub** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="dd6ee-173">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-173">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_samlbase.png)

3. <span data-ttu-id="dd6ee-175">Sur hello **O.C. Tanner - AppreciateHub domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="dd6ee-175">On hello **O.C. Tanner - AppreciateHub Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_url.png)

    <span data-ttu-id="dd6ee-177">a.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-177">a.</span></span> <span data-ttu-id="dd6ee-178">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.appreciatehub.com/fed/sp/authnResponse20`</span><span class="sxs-lookup"><span data-stu-id="dd6ee-178">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.appreciatehub.com/fed/sp/authnResponse20`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dd6ee-179">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-179">This value is not real.</span></span> <span data-ttu-id="dd6ee-180">Mettre à jour cette valeur avec l’URL de réponse réelle hello.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-180">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="dd6ee-181">Pour obtenir cette valeur, contactez [l’équipe du support technique O.C. Tanner - équipe de support AppreciateHub](mailto:sso@octanner.com) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-181">Contact [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com) tooget this value.</span></span>

    <span data-ttu-id="dd6ee-182">b.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-182">b.</span></span> <span data-ttu-id="dd6ee-183">Fichier de métadonnées hello ouverte à l’aide du lien de hello : [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).</span><span class="sxs-lookup"><span data-stu-id="dd6ee-183">Open hello metadata file using hello following link: [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).</span></span>
   
    <span data-ttu-id="dd6ee-184">c.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-184">c.</span></span> <span data-ttu-id="dd6ee-185">Recherchez hello **md:AssertionConsumerService** nœud.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-185">Locate hello **md:AssertionConsumerService** node.</span></span> 
   
    <span data-ttu-id="dd6ee-186">d.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-186">d.</span></span> <span data-ttu-id="dd6ee-187">Copier la valeur hello Hello **emplacement** attribut.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-187">Copy hello value of hello **Location** attribute.</span></span> 
   
    ![Configurer les paramètres d’application][12]
   
    <span data-ttu-id="dd6ee-189">e.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-189">e.</span></span> <span data-ttu-id="dd6ee-190">Bonjour **URL de connexion** zone de texte, juste après valeur hello que vous avez obtenu à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-190">In hello **Sign On URL** textbox, past hello value you have obtained in hello previous step.</span></span>

4. <span data-ttu-id="dd6ee-191">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-191">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_certificate.png) 

5. <span data-ttu-id="dd6ee-193">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="dd6ee-193">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="dd6ee-195">tooconfigure l’authentification unique sur **O.C. Tanner - AppreciateHub** côté, vous devez hello toosend téléchargé **Metadata XML** trop[O.C. Tanner - AppreciateHub](mailto:sso@octanner.com).</span><span class="sxs-lookup"><span data-stu-id="dd6ee-195">tooconfigure single sign-on on **O.C. Tanner - AppreciateHub** side, you need toosend hello downloaded **Metadata XML** too[O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com).</span></span>

> [!TIP]
> <span data-ttu-id="dd6ee-196">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="dd6ee-196">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="dd6ee-197">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-197">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="dd6ee-198">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dd6ee-198">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dd6ee-199">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd6ee-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="dd6ee-200">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="dd6ee-202">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dd6ee-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="dd6ee-203">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-203">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dd6ee-205">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-205">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dd6ee-207">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-207">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dd6ee-209">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="dd6ee-209">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dd6ee-211">a.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-211">a.</span></span> <span data-ttu-id="dd6ee-212">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-212">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dd6ee-213">b.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-213">b.</span></span> <span data-ttu-id="dd6ee-214">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dd6ee-215">c.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-215">c.</span></span> <span data-ttu-id="dd6ee-216">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-216">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="dd6ee-217">d.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-217">d.</span></span> <span data-ttu-id="dd6ee-218">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-218">Click **Create**.</span></span>
 
### <a name="creating-a-oc-tanner---appreciatehub-test-user"></a><span data-ttu-id="dd6ee-219">Création d’un utilisateur de test O.C.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-219">Creating a O.C.</span></span> <span data-ttu-id="dd6ee-220">Tanner - AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="dd6ee-220">Tanner - AppreciateHub test user</span></span>

<span data-ttu-id="dd6ee-221">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans O.C.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-221">hello objective of this section is toocreate a user called Britta Simon in O.C.</span></span> <span data-ttu-id="dd6ee-222">Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-222">Tanner - AppreciateHub.</span></span>

<span data-ttu-id="dd6ee-223">**toocreate un utilisateur appelé Britta Simon dans O.C. Tanner - AppreciateHub, effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dd6ee-223">**toocreate a user called Britta Simon in O.C. Tanner - AppreciateHub, perform hello following steps:**</span></span>

<span data-ttu-id="dd6ee-224">Demandez à [l’équipe du support technique O.C. Tanner - équipe de support AppreciateHub](mailto:sso@octanner.com) toocreate un utilisateur qui a comme hello d’attribut nameID même valeur en tant que nom d’utilisateur hello de Britta Simon dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-224">Ask your [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com) toocreate a user that has as nameID attribute hello same value as hello user name of Britta Simon in Azure AD.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="dd6ee-225">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd6ee-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="dd6ee-226">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooO.C.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooO.C.</span></span> <span data-ttu-id="dd6ee-227">Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-227">Tanner - AppreciateHub.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="dd6ee-229">**tooassign Britta Simon tooO.C. Tanner - AppreciateHub, effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dd6ee-229">**tooassign Britta Simon tooO.C. Tanner - AppreciateHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="dd6ee-230">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="dd6ee-232">Dans la liste des applications hello, sélectionnez **O.C. Tanner - AppreciateHub**.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-232">In hello applications list, select **O.C. Tanner - AppreciateHub**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_app.png) 

3. <span data-ttu-id="dd6ee-234">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="dd6ee-236">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-236">Click **Add** button.</span></span> <span data-ttu-id="dd6ee-237">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="dd6ee-239">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="dd6ee-240">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dd6ee-241">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dd6ee-242">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="dd6ee-242">Testing single sign-on</span></span>

<span data-ttu-id="dd6ee-243">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-243">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="dd6ee-244">Lorsque vous cliquez sur hello O.C.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-244">When you click hello O.C.</span></span> <span data-ttu-id="dd6ee-245">Tanner - vignette AppreciateHub dans hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour O.C.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-245">Tanner - AppreciateHub tile in hello Access Panel, you should get automatically signed-on tooyour O.C.</span></span> <span data-ttu-id="dd6ee-246">Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="dd6ee-246">Tanner - AppreciateHub application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dd6ee-247">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="dd6ee-247">Additional resources</span></span>

* [<span data-ttu-id="dd6ee-248">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dd6ee-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dd6ee-249">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="dd6ee-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_08.png

[100]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_203.png

