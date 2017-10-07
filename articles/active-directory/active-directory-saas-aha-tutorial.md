---
title: "Didacticiel : Intégration d’Azure Active Directory à Aha! | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Aha !."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ad955d3d-896a-41bb-800d-68e8cb5ff48d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: d844db3c0a035560e6fb275017215171743fba56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-aha"></a><span data-ttu-id="8a19e-104">Didacticiel : Intégration d’Azure Active Directory à Aha!</span><span class="sxs-lookup"><span data-stu-id="8a19e-104">Tutorial: Azure Active Directory integration with Aha!</span></span>

<span data-ttu-id="8a19e-105">Dans ce didacticiel, vous apprendrez comment toointegrate Aha !</span><span class="sxs-lookup"><span data-stu-id="8a19e-105">In this tutorial, you learn how toointegrate Aha!</span></span> <span data-ttu-id="8a19e-106">à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8a19e-106">with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8a19e-107">L’intégration d’Aha!</span><span class="sxs-lookup"><span data-stu-id="8a19e-107">Integrating Aha!</span></span> <span data-ttu-id="8a19e-108">avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="8a19e-108">with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8a19e-109">Vous pouvez contrôler dans Azure AD qui a accès tooAha !</span><span class="sxs-lookup"><span data-stu-id="8a19e-109">You can control in Azure AD who has access tooAha!</span></span>
- <span data-ttu-id="8a19e-110">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooAha !</span><span class="sxs-lookup"><span data-stu-id="8a19e-110">You can enable your users tooautomatically get signed-on tooAha!</span></span> <span data-ttu-id="8a19e-111">(par le biais de l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a19e-111">(Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8a19e-112">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="8a19e-112">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8a19e-113">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8a19e-113">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a19e-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8a19e-114">Prerequisites</span></span>

<span data-ttu-id="8a19e-115">tooconfigure intégration d’Azure AD à Aha !, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="8a19e-115">tooconfigure Azure AD integration with Aha!, you need hello following items:</span></span>

- <span data-ttu-id="8a19e-116">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a19e-116">An Azure AD subscription</span></span>
- <span data-ttu-id="8a19e-117">Un abonnement Aha!</span><span class="sxs-lookup"><span data-stu-id="8a19e-117">An Aha!</span></span> <span data-ttu-id="8a19e-118">Un abonnement pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="8a19e-118">single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8a19e-119">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="8a19e-119">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8a19e-120">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="8a19e-120">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8a19e-121">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="8a19e-121">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8a19e-122">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8a19e-122">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8a19e-123">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="8a19e-123">Scenario description</span></span>
<span data-ttu-id="8a19e-124">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="8a19e-124">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8a19e-125">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="8a19e-125">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8a19e-126">Ajout d’Aha!</span><span class="sxs-lookup"><span data-stu-id="8a19e-126">Adding Aha!</span></span> <span data-ttu-id="8a19e-127">à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="8a19e-127">from hello gallery</span></span>
2. <span data-ttu-id="8a19e-128">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a19e-128">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-aha-from-hello-gallery"></a><span data-ttu-id="8a19e-129">Ajout d’Aha!</span><span class="sxs-lookup"><span data-stu-id="8a19e-129">Adding Aha!</span></span> <span data-ttu-id="8a19e-130">à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="8a19e-130">from hello gallery</span></span>
<span data-ttu-id="8a19e-131">intégration de hello tooconfigure de Aha !</span><span class="sxs-lookup"><span data-stu-id="8a19e-131">tooconfigure hello integration of Aha!</span></span> <span data-ttu-id="8a19e-132">dans Azure AD, vous devez tooadd Aha !</span><span class="sxs-lookup"><span data-stu-id="8a19e-132">into Azure AD, you need tooadd Aha!</span></span> <span data-ttu-id="8a19e-133">à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="8a19e-133">from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8a19e-134">**tooadd Aha ! à partir de la galerie hello, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8a19e-134">**tooadd Aha! from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8a19e-135">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="8a19e-135">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8a19e-137">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="8a19e-137">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8a19e-138">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8a19e-138">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="8a19e-140">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8a19e-140">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="8a19e-142">Dans la zone de recherche de hello, tapez **Aha !**.</span><span class="sxs-lookup"><span data-stu-id="8a19e-142">In hello search box, type **Aha!**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-aha-tutorial/tutorial_aha_search.png)

5. <span data-ttu-id="8a19e-144">Dans le volet de résultats hello, sélectionnez **Aha !**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="8a19e-144">In hello results panel, select **Aha!**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-aha-tutorial/tutorial_aha_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8a19e-146">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a19e-146">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8a19e-147">Dans cette section, vous configurez et testez l’authentification unique Azure AD avec Aha!</span><span class="sxs-lookup"><span data-stu-id="8a19e-147">In this section, you configure and test Azure AD single sign-on with Aha!</span></span> <span data-ttu-id="8a19e-148">au moyen d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="8a19e-148">based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8a19e-149">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Aha !</span><span class="sxs-lookup"><span data-stu-id="8a19e-149">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Aha!</span></span> <span data-ttu-id="8a19e-150">est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8a19e-150">is tooa user in Azure AD.</span></span> <span data-ttu-id="8a19e-151">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Aha !</span><span class="sxs-lookup"><span data-stu-id="8a19e-151">In other words, a link relationship between an Azure AD user and hello related user in Aha!</span></span> <span data-ttu-id="8a19e-152">doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="8a19e-152">needs toobe established.</span></span>

<span data-ttu-id="8a19e-153">Dans Aha !, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="8a19e-153">In Aha!, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8a19e-154">tooconfigure et test Azure AD sur l’authentification unique avec Aha !, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="8a19e-154">tooconfigure and test Azure AD single sign-on with Aha!, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8a19e-155">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="8a19e-155">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8a19e-156">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8a19e-156">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8a19e-157">**[Création d’un sentiment ! utilisateur de test](#creating-an-aha-test-user)**  -toohave un équivalent de Britta Simon dans Aha !</span><span class="sxs-lookup"><span data-stu-id="8a19e-157">**[Creating an Aha! test user](#creating-an-aha-test-user)** - toohave a counterpart of Britta Simon in Aha!</span></span> <span data-ttu-id="8a19e-158">qui est lié toohello la représentation sous forme de Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8a19e-158">that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8a19e-159">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="8a19e-159">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8a19e-160">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="8a19e-160">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8a19e-161">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a19e-161">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8a19e-162">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Aha !</span><span class="sxs-lookup"><span data-stu-id="8a19e-162">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Aha!</span></span> <span data-ttu-id="8a19e-163">application Aha!.</span><span class="sxs-lookup"><span data-stu-id="8a19e-163">application.</span></span>

<span data-ttu-id="8a19e-164">**tooconfigure Azure AD l’authentification unique avec Aha !, effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8a19e-164">**tooconfigure Azure AD single sign-on with Aha!, perform hello following steps:**</span></span>

1. <span data-ttu-id="8a19e-165">Bonjour portail Azure, sur hello **Aha !**</span><span class="sxs-lookup"><span data-stu-id="8a19e-165">In hello Azure portal, on hello **Aha!**</span></span> <span data-ttu-id="8a19e-166">cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="8a19e-166">application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="8a19e-168">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="8a19e-168">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-aha-tutorial/tutorial_aha_samlbase.png)

3. <span data-ttu-id="8a19e-170">Sur hello **Aha ! Domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8a19e-170">On hello **Aha! Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-aha-tutorial/tutorial_aha_url.png)

    <span data-ttu-id="8a19e-172">a.</span><span class="sxs-lookup"><span data-stu-id="8a19e-172">a.</span></span> <span data-ttu-id="8a19e-173">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.aha.io/session/new`</span><span class="sxs-lookup"><span data-stu-id="8a19e-173">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.aha.io/session/new`</span></span>

    <span data-ttu-id="8a19e-174">b.</span><span class="sxs-lookup"><span data-stu-id="8a19e-174">b.</span></span> <span data-ttu-id="8a19e-175">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.aha.io`</span><span class="sxs-lookup"><span data-stu-id="8a19e-175">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.aha.io`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8a19e-176">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="8a19e-176">These values are not real.</span></span> <span data-ttu-id="8a19e-177">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="8a19e-177">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8a19e-178">Pour obtenir ces valeurs, contactez [ Équipe de support client](https://www.aha.io/company/contact) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="8a19e-178">Contact [Aha! Client support team](https://www.aha.io/company/contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="8a19e-179">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="8a19e-179">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-aha-tutorial/tutorial_aha_certificate.png) 

5. <span data-ttu-id="8a19e-181">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="8a19e-181">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-aha-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8a19e-183">Dans une fenêtre de navigateur web, connectez-vous tooyour Aha !</span><span class="sxs-lookup"><span data-stu-id="8a19e-183">In a different web browser window, log in tooyour Aha!</span></span> <span data-ttu-id="8a19e-184">en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="8a19e-184">company site as an administrator.</span></span>

7. <span data-ttu-id="8a19e-185">Dans le menu hello haut de hello, cliquez sur **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="8a19e-185">In hello menu on hello top, click **Settings**.</span></span>

    <span data-ttu-id="8a19e-186">![Paramètres](./media/active-directory-saas-aha-tutorial/IC798950.png "Paramètres")</span><span class="sxs-lookup"><span data-stu-id="8a19e-186">![Settings](./media/active-directory-saas-aha-tutorial/IC798950.png "Settings")</span></span>

8. <span data-ttu-id="8a19e-187">Cliquez sur **Account**.</span><span class="sxs-lookup"><span data-stu-id="8a19e-187">Click **Account**.</span></span>
   
    <span data-ttu-id="8a19e-188">![Profil](./media/active-directory-saas-aha-tutorial/IC798951.png "Profil")</span><span class="sxs-lookup"><span data-stu-id="8a19e-188">![Profile](./media/active-directory-saas-aha-tutorial/IC798951.png "Profile")</span></span>

9. <span data-ttu-id="8a19e-189">Cliquez sur **Security and single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="8a19e-189">Click **Security and single sign-on**.</span></span>
   
    <span data-ttu-id="8a19e-190">![Sécurité et authentification unique](./media/active-directory-saas-aha-tutorial/IC798952.png "Sécurité et authentification unique")</span><span class="sxs-lookup"><span data-stu-id="8a19e-190">![Security and single sign-on](./media/active-directory-saas-aha-tutorial/IC798952.png "Security and single sign-on")</span></span>

10. <span data-ttu-id="8a19e-191">Dans la section **Single Sign-On**, pour **Identity Provider**, sélectionnez **SAML2.0**.</span><span class="sxs-lookup"><span data-stu-id="8a19e-191">In **Single Sign-On** section, as **Identity Provider**, select **SAML2.0**.</span></span>
   
    <span data-ttu-id="8a19e-192">![Sécurité et authentification unique](./media/active-directory-saas-aha-tutorial/IC798953.png "Sécurité et authentification unique")</span><span class="sxs-lookup"><span data-stu-id="8a19e-192">![Security and single sign-on](./media/active-directory-saas-aha-tutorial/IC798953.png "Security and single sign-on")</span></span>

11. <span data-ttu-id="8a19e-193">Sur hello **Single Sign-On** configuration page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8a19e-193">On hello **Single Sign-On** configuration page, perform hello following steps:</span></span>
    
    <span data-ttu-id="8a19e-194">![Authentification unique](./media/active-directory-saas-aha-tutorial/IC798954.png "Authentification unique")</span><span class="sxs-lookup"><span data-stu-id="8a19e-194">![Single Sign-On](./media/active-directory-saas-aha-tutorial/IC798954.png "Single Sign-On")</span></span>
    
       <span data-ttu-id="8a19e-195">a.</span><span class="sxs-lookup"><span data-stu-id="8a19e-195">a.</span></span> <span data-ttu-id="8a19e-196">Bonjour **nom** zone de texte, tapez un nom pour votre configuration.</span><span class="sxs-lookup"><span data-stu-id="8a19e-196">In hello **Name** textbox, type a name for your configuration.</span></span>

       <span data-ttu-id="8a19e-197">b.</span><span class="sxs-lookup"><span data-stu-id="8a19e-197">b.</span></span> <span data-ttu-id="8a19e-198">Pour **Configure using**, sélectionnez **Metadata File**.</span><span class="sxs-lookup"><span data-stu-id="8a19e-198">For **Configure using**, select **Metadata File**.</span></span>
   
       <span data-ttu-id="8a19e-199">c.</span><span class="sxs-lookup"><span data-stu-id="8a19e-199">c.</span></span> <span data-ttu-id="8a19e-200">tooupload votre fichier de métadonnées téléchargé, cliquez sur **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="8a19e-200">tooupload your downloaded metadata file, click **Browse**.</span></span>
   
       <span data-ttu-id="8a19e-201">d.</span><span class="sxs-lookup"><span data-stu-id="8a19e-201">d.</span></span> <span data-ttu-id="8a19e-202">Cliquez sur **Update**.</span><span class="sxs-lookup"><span data-stu-id="8a19e-202">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="8a19e-203">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="8a19e-203">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8a19e-204">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="8a19e-204">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8a19e-205">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8a19e-205">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8a19e-206">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a19e-206">Creating an Azure AD test user</span></span>
<span data-ttu-id="8a19e-207">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="8a19e-207">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="8a19e-209">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8a19e-209">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8a19e-210">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="8a19e-210">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8a19e-212">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="8a19e-212">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8a19e-214">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="8a19e-214">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8a19e-216">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8a19e-216">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8a19e-218">a.</span><span class="sxs-lookup"><span data-stu-id="8a19e-218">a.</span></span> <span data-ttu-id="8a19e-219">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8a19e-219">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8a19e-220">b.</span><span class="sxs-lookup"><span data-stu-id="8a19e-220">b.</span></span> <span data-ttu-id="8a19e-221">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8a19e-221">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8a19e-222">c.</span><span class="sxs-lookup"><span data-stu-id="8a19e-222">c.</span></span> <span data-ttu-id="8a19e-223">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="8a19e-223">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8a19e-224">d.</span><span class="sxs-lookup"><span data-stu-id="8a19e-224">d.</span></span> <span data-ttu-id="8a19e-225">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="8a19e-225">Click **Create**.</span></span>
 
### <a name="creating-an-aha-test-user"></a><span data-ttu-id="8a19e-226">Création</span><span class="sxs-lookup"><span data-stu-id="8a19e-226">Creating an Aha!</span></span> <span data-ttu-id="8a19e-227">d’un utilisateur de test Aha!</span><span class="sxs-lookup"><span data-stu-id="8a19e-227">test user</span></span>

<span data-ttu-id="8a19e-228">toolog d’utilisateurs tooenable Azure AD dans tooAha !, vous devez les configurer dans Aha !.</span><span class="sxs-lookup"><span data-stu-id="8a19e-228">tooenable Azure AD users toolog in tooAha!, they must be provisioned into Aha!.</span></span>  

<span data-ttu-id="8a19e-229">Dans le cas de hello de Aha !, cette configuration est une tâche automatique.</span><span class="sxs-lookup"><span data-stu-id="8a19e-229">In hello case of Aha!, provisioning is an automated task.</span></span> <span data-ttu-id="8a19e-230">Vous n’avez rien à faire.</span><span class="sxs-lookup"><span data-stu-id="8a19e-230">There is no action item for you.</span></span>

<span data-ttu-id="8a19e-231">Les utilisateurs sont automatiquement créés si nécessaire pendant hello première seule tentative de connexion.</span><span class="sxs-lookup"><span data-stu-id="8a19e-231">Users are automatically created if necessary during hello first single sign-on attempt.</span></span>

>[!NOTE]
><span data-ttu-id="8a19e-232">Vous pouvez utiliser n’importe quel autre outil de création de</span><span class="sxs-lookup"><span data-stu-id="8a19e-232">You can use any other Aha!</span></span> <span data-ttu-id="8a19e-233">compte utilisateur Aha! ou toute API fournie par Aha!</span><span class="sxs-lookup"><span data-stu-id="8a19e-233">user account creation tools or APIs provided by Aha!</span></span> <span data-ttu-id="8a19e-234">tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="8a19e-234">tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8a19e-235">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a19e-235">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8a19e-236">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooAha !.</span><span class="sxs-lookup"><span data-stu-id="8a19e-236">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAha!.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="8a19e-238">**tooassign Britta Simon tooAha !, effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8a19e-238">**tooassign Britta Simon tooAha!, perform hello following steps:**</span></span>

1. <span data-ttu-id="8a19e-239">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8a19e-239">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="8a19e-241">Dans la liste des applications hello, sélectionnez **Aha !**.</span><span class="sxs-lookup"><span data-stu-id="8a19e-241">In hello applications list, select **Aha!**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-aha-tutorial/tutorial_aha_app.png) 

3. <span data-ttu-id="8a19e-243">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8a19e-243">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="8a19e-245">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="8a19e-245">Click **Add** button.</span></span> <span data-ttu-id="8a19e-246">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="8a19e-246">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="8a19e-248">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="8a19e-248">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8a19e-249">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8a19e-249">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8a19e-250">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="8a19e-250">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8a19e-251">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="8a19e-251">Testing single sign-on</span></span>

<span data-ttu-id="8a19e-252">Si vous souhaitez tootest vos paramètres d’authentification unique, ouvrez hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="8a19e-252">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="8a19e-253">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8a19e-253">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8a19e-254">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="8a19e-254">Additional resources</span></span>

* [<span data-ttu-id="8a19e-255">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8a19e-255">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8a19e-256">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="8a19e-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-aha-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-aha-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-aha-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-aha-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-aha-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-aha-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-aha-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-aha-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-aha-tutorial/tutorial_general_203.png

