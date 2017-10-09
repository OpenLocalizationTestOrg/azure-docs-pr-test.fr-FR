---
title: "Didacticiel : Intégration d’Azure Active Directory à Nexonia | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Nexonia."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a93b771a-9bc3-444a-bdc0-457f8bb7e780
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/1/2017
ms.author: jeedes
ms.openlocfilehash: 3778804084a7989414260bae5654cf76e9ccca6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-nexonia"></a><span data-ttu-id="cf6d4-103">Didacticiel : Intégration d’Azure Active Directory à Nexonia</span><span class="sxs-lookup"><span data-stu-id="cf6d4-103">Tutorial: Azure Active Directory integration with Nexonia</span></span>

<span data-ttu-id="cf6d4-104">Dans ce didacticiel, vous apprendrez comment toointegrate Nexonia avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cf6d4-104">In this tutorial, you learn how toointegrate Nexonia with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cf6d4-105">Intégration Nexonia à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="cf6d4-105">Integrating Nexonia with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cf6d4-106">Vous pouvez contrôler dans Azure AD qui a accès tooNexonia</span><span class="sxs-lookup"><span data-stu-id="cf6d4-106">You can control in Azure AD who has access tooNexonia</span></span>
- <span data-ttu-id="cf6d4-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooNexonia (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf6d4-107">You can enable your users tooautomatically get signed-on tooNexonia (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cf6d4-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="cf6d4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cf6d4-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="cf6d4-110">[Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cf6d4-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cf6d4-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="cf6d4-111">Prerequisites</span></span>

<span data-ttu-id="cf6d4-112">tooconfigure intégration d’Azure AD avec Nexonia, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="cf6d4-112">tooconfigure Azure AD integration with Nexonia, you need hello following items:</span></span>

- <span data-ttu-id="cf6d4-113">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf6d4-113">An Azure AD subscription</span></span>
- <span data-ttu-id="cf6d4-114">Un abonnement Nexonia avec authentification unique activée</span><span class="sxs-lookup"><span data-stu-id="cf6d4-114">A Nexonia single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cf6d4-115">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cf6d4-116">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="cf6d4-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cf6d4-117">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cf6d4-118">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cf6d4-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cf6d4-119">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="cf6d4-119">Scenario description</span></span>
<span data-ttu-id="cf6d4-120">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cf6d4-121">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="cf6d4-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cf6d4-122">Ajout de Nexonia à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="cf6d4-122">Adding Nexonia from hello gallery</span></span>
2. <span data-ttu-id="cf6d4-123">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf6d4-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-nexonia-from-hello-gallery"></a><span data-ttu-id="cf6d4-124">Ajout de Nexonia à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="cf6d4-124">Adding Nexonia from hello gallery</span></span>
<span data-ttu-id="cf6d4-125">intégration de hello tooconfigure de Nexonia dans Azure AD, vous devez tooadd Nexonia à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-125">tooconfigure hello integration of Nexonia into Azure AD, you need tooadd Nexonia from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cf6d4-126">**tooadd Nexonia à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="cf6d4-126">**tooadd Nexonia from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cf6d4-127">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cf6d4-129">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cf6d4-130">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-130">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="cf6d4-132">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="cf6d4-134">Dans la zone de recherche de hello, tapez **Nexonia**.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-134">In hello search box, type **Nexonia**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_search.png)

5. <span data-ttu-id="cf6d4-136">Dans le volet de résultats hello, sélectionnez **Nexonia**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-136">In hello results panel, select **Nexonia**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cf6d4-138">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf6d4-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cf6d4-139">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Nexonia, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="cf6d4-139">In this section, you configure and test Azure AD single sign-on with Nexonia based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cf6d4-140">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Nexonia est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Nexonia is tooa user in Azure AD.</span></span> <span data-ttu-id="cf6d4-141">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Nexonia doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-141">In other words, a link relationship between an Azure AD user and hello related user in Nexonia needs toobe established.</span></span>

<span data-ttu-id="cf6d4-142">Dans Nexonia, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-142">In Nexonia, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="cf6d4-143">tooconfigure et test Azure AD l’authentification unique avec Nexonia, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="cf6d4-143">tooconfigure and test Azure AD single sign-on with Nexonia, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cf6d4-144">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cf6d4-145">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cf6d4-146">**[Création d’un utilisateur de test Nexonia](#creating-a-nexonia-test-user)**  -toohave un équivalent de Britta Simon dans Nexonia est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-146">**[Creating a Nexonia test user](#creating-a-nexonia-test-user)** - toohave a counterpart of Britta Simon in Nexonia that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cf6d4-147">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cf6d4-148">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cf6d4-149">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf6d4-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cf6d4-150">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Nexonia.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Nexonia application.</span></span>

>[!Note]
><span data-ttu-id="cf6d4-151">Si vous rencontrez des problèmes dans l’intégration de hello, puis faire référence à cette [lien](https://docs.microsoft.com/azure/active-directory/application-sign-in-problem-federated-sso-gallery?WT.mc_id=UI_AAD_Enterprise_Apps_SupportOrTroubleshooting) guide de dépannage.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-151">If you have issues in hello integration then refer this [link](https://docs.microsoft.com/azure/active-directory/application-sign-in-problem-federated-sso-gallery?WT.mc_id=UI_AAD_Enterprise_Apps_SupportOrTroubleshooting) for troubleshooting guide.</span></span> <span data-ttu-id="cf6d4-152">Si vous ne trouvez toujours pas de solution de hello, puis déclenchez demande de support hello à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-152">If you still have not found hello solution, then raise hello support request from Azure portal.</span></span>

<span data-ttu-id="cf6d4-153">**tooconfigure Azure AD single sign-on avec Nexonia, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="cf6d4-153">**tooconfigure Azure AD single sign-on with Nexonia, perform hello following steps:**</span></span>

1. <span data-ttu-id="cf6d4-154">Bonjour portail Azure, sur hello **Nexonia** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-154">In hello Azure portal, on hello **Nexonia** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="cf6d4-156">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-156">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_samlbase.png)

3. <span data-ttu-id="cf6d4-158">Sur hello **Nexonia domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="cf6d4-158">On hello **Nexonia Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_url.png)

    <span data-ttu-id="cf6d4-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://system.nexonia.com/assistant/saml.do?orgCode=<organizationcode>`</span><span class="sxs-lookup"><span data-stu-id="cf6d4-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://system.nexonia.com/assistant/saml.do?orgCode=<organizationcode>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cf6d4-161">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-161">This value is not real.</span></span> <span data-ttu-id="cf6d4-162">Mettre à jour cette valeur avec l’URL de réponse réelle hello.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-162">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="cf6d4-163">Contact [équipe de support Nexonia](https://nexonia.zendesk.com/hc/requests/new) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-163">Contact [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) tooget this value.</span></span> 


4. <span data-ttu-id="cf6d4-164">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_certificate.png) 

5. <span data-ttu-id="cf6d4-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="cf6d4-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-nexonia-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cf6d4-168">Sur hello **Nexonia Configuration** , cliquez sur **Nexonia de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-168">On hello **Nexonia Configuration** section, click **Configure Nexonia** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="cf6d4-169">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="cf6d4-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_configure.png) 

7. <span data-ttu-id="cf6d4-171">tooget l’authentification unique configurée pour votre application, contactez [équipe de support Nexonia](https://nexonia.zendesk.com/hc/requests/new) et leur fournir des éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="cf6d4-171">tooget SSO configured for your application, contact [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) and provide them with hello following:</span></span>

    <span data-ttu-id="cf6d4-172">hello • téléchargé **certificat**</span><span class="sxs-lookup"><span data-stu-id="cf6d4-172">• hello downloaded **certificate**</span></span>

    <span data-ttu-id="cf6d4-173">• hello **ID d’entité SAML**</span><span class="sxs-lookup"><span data-stu-id="cf6d4-173">• hello **SAML Entity ID**</span></span>

    <span data-ttu-id="cf6d4-174">• hello **SAML Sign-On URL du Service unique**</span><span class="sxs-lookup"><span data-stu-id="cf6d4-174">• hello **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="cf6d4-175">• hello **URL de déconnexion**</span><span class="sxs-lookup"><span data-stu-id="cf6d4-175">• hello **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="cf6d4-176">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="cf6d4-176">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cf6d4-177">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-177">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cf6d4-178">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cf6d4-178">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cf6d4-179">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf6d4-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="cf6d4-180">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-180">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="cf6d4-182">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="cf6d4-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cf6d4-183">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-183">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-nexonia-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cf6d4-185">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-185">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-nexonia-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cf6d4-187">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-187">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-nexonia-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cf6d4-189">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="cf6d4-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-nexonia-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cf6d4-191">a.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-191">a.</span></span> <span data-ttu-id="cf6d4-192">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cf6d4-193">b.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-193">b.</span></span> <span data-ttu-id="cf6d4-194">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cf6d4-195">c.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-195">c.</span></span> <span data-ttu-id="cf6d4-196">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cf6d4-197">d.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-197">d.</span></span> <span data-ttu-id="cf6d4-198">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-198">Click **Create**.</span></span>
 
### <a name="creating-a-nexonia-test-user"></a><span data-ttu-id="cf6d4-199">Création d’un utilisateur de test Nexonia</span><span class="sxs-lookup"><span data-stu-id="cf6d4-199">Creating a Nexonia test user</span></span>

<span data-ttu-id="cf6d4-200">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Nexonia.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-200">In this section, you create a user called Britta Simon in Nexonia.</span></span> <span data-ttu-id="cf6d4-201">Travailler avec [équipe de support Nexonia](https://nexonia.zendesk.com/hc/requests/new) tooadd les utilisateurs de hello dans la plateforme de Nexonia hello.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-201">Work with [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) tooadd hello users in hello Nexonia platform.</span></span> <span data-ttu-id="cf6d4-202">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-202">Users must be created and activated before you use single sign-on.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cf6d4-203">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf6d4-203">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cf6d4-204">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooNexonia.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-204">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNexonia.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="cf6d4-206">**tooassign Britta Simon tooNexonia, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="cf6d4-206">**tooassign Britta Simon tooNexonia, perform hello following steps:**</span></span>

1. <span data-ttu-id="cf6d4-207">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-207">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="cf6d4-209">Dans la liste des applications hello, sélectionnez **Nexonia**.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-209">In hello applications list, select **Nexonia**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_app.png) 

3. <span data-ttu-id="cf6d4-211">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-211">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="cf6d4-213">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-213">Click **Add** button.</span></span> <span data-ttu-id="cf6d4-214">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="cf6d4-216">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-216">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cf6d4-217">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cf6d4-218">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cf6d4-219">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="cf6d4-219">Testing single sign-on</span></span>

<span data-ttu-id="cf6d4-220">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-220">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cf6d4-221">Lorsque vous cliquez sur mosaïque Nexonia hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Nexonia application.</span><span class="sxs-lookup"><span data-stu-id="cf6d4-221">When you click hello Nexonia tile in hello Access Panel, you should get automatically signed-on tooyour Nexonia application.</span></span>
<span data-ttu-id="cf6d4-222">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="cf6d4-222">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cf6d4-223">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="cf6d4-223">Additional resources</span></span>

* [<span data-ttu-id="cf6d4-224">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cf6d4-224">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cf6d4-225">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="cf6d4-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_203.png

