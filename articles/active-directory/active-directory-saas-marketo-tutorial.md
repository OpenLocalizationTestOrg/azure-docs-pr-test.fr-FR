---
title: "Didacticiel : Intégration d’Azure Active Directory à Marketo | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Marketo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b88c45f5-d288-4717-835c-ca965add8735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 87f88cde4f027f99a83c1ab3b318247bb4d658ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-marketo"></a><span data-ttu-id="4483a-103">Didacticiel : Intégration d’Azure Active Directory à Marketo</span><span class="sxs-lookup"><span data-stu-id="4483a-103">Tutorial: Azure Active Directory integration with Marketo</span></span>

<span data-ttu-id="4483a-104">Dans ce didacticiel, vous apprendrez comment toointegrate Marketo avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4483a-104">In this tutorial, you learn how toointegrate Marketo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4483a-105">Intégration de Marketo avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="4483a-105">Integrating Marketo with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4483a-106">Vous pouvez contrôler dans Azure AD qui a accès tooMarketo</span><span class="sxs-lookup"><span data-stu-id="4483a-106">You can control in Azure AD who has access tooMarketo</span></span>
- <span data-ttu-id="4483a-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooMarketo (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="4483a-107">You can enable your users tooautomatically get signed-on tooMarketo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4483a-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="4483a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4483a-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4483a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4483a-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4483a-110">Prerequisites</span></span>

<span data-ttu-id="4483a-111">tooconfigure intégration d’Azure AD avec Marketo, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="4483a-111">tooconfigure Azure AD integration with Marketo, you need hello following items:</span></span>

- <span data-ttu-id="4483a-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="4483a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4483a-113">Un abonnement Marketo pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="4483a-113">A Marketo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4483a-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="4483a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4483a-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="4483a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4483a-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="4483a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4483a-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4483a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4483a-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="4483a-118">Scenario description</span></span>
<span data-ttu-id="4483a-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="4483a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4483a-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="4483a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4483a-121">Ajout de Marketo à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="4483a-121">Adding Marketo from hello gallery</span></span>
2. <span data-ttu-id="4483a-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4483a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-marketo-from-hello-gallery"></a><span data-ttu-id="4483a-123">Ajout de Marketo à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="4483a-123">Adding Marketo from hello gallery</span></span>
<span data-ttu-id="4483a-124">intégration de hello tooconfigure de Marketo dans Azure AD, vous devez tooadd Marketo à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="4483a-124">tooconfigure hello integration of Marketo into Azure AD, you need tooadd Marketo from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4483a-125">**tooadd Marketo à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4483a-125">**tooadd Marketo from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4483a-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="4483a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4483a-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="4483a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4483a-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="4483a-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="4483a-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="4483a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="4483a-133">Dans la zone de recherche de hello, tapez **Marketo**.</span><span class="sxs-lookup"><span data-stu-id="4483a-133">In hello search box, type **Marketo**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_search.png)

5. <span data-ttu-id="4483a-135">Dans le volet de résultats hello, sélectionnez **Marketo**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="4483a-135">In hello results panel, select **Marketo**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4483a-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4483a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4483a-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Marketo grâce à un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="4483a-138">In this section, you configure and test Azure AD single sign-on with Marketo based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4483a-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Marketo est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4483a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Marketo is tooa user in Azure AD.</span></span> <span data-ttu-id="4483a-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Marketo doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="4483a-140">In other words, a link relationship between an Azure AD user and hello related user in Marketo needs toobe established.</span></span>

<span data-ttu-id="4483a-141">Dans Marketo, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="4483a-141">In Marketo, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4483a-142">tooconfigure et test Azure AD l’authentification unique avec Marketo, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="4483a-142">tooconfigure and test Azure AD single sign-on with Marketo, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4483a-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="4483a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4483a-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4483a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4483a-145">**[Création d’un utilisateur de test de Marketo](#creating-a-marketo-test-user)**  -toohave un équivalent de Britta Simon dans Marketo est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4483a-145">**[Creating a Marketo test user](#creating-a-marketo-test-user)** - toohave a counterpart of Britta Simon in Marketo that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4483a-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="4483a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4483a-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="4483a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4483a-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4483a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4483a-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de Marketo.</span><span class="sxs-lookup"><span data-stu-id="4483a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Marketo application.</span></span>

<span data-ttu-id="4483a-150">**tooconfigure Azure AD single sign-on avec Marketo, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4483a-150">**tooconfigure Azure AD single sign-on with Marketo, perform hello following steps:**</span></span>

1. <span data-ttu-id="4483a-151">Bonjour portail Azure, sur hello **Marketo** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="4483a-151">In hello Azure portal, on hello **Marketo** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="4483a-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="4483a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_samlbase.png)

3. <span data-ttu-id="4483a-155">Sur hello **Marketo domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="4483a-155">On hello **Marketo Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_url.png)

    <span data-ttu-id="4483a-157">a.</span><span class="sxs-lookup"><span data-stu-id="4483a-157">a.</span></span> <span data-ttu-id="4483a-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://saml.marketo.com/sp`</span><span class="sxs-lookup"><span data-stu-id="4483a-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://saml.marketo.com/sp`</span></span>

    <span data-ttu-id="4483a-159">b.</span><span class="sxs-lookup"><span data-stu-id="4483a-159">b.</span></span> <span data-ttu-id="4483a-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://login.marketo.com/saml/assertion/\<munchkinid\>`</span><span class="sxs-lookup"><span data-stu-id="4483a-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://login.marketo.com/saml/assertion/\<munchkinid\>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4483a-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="4483a-161">These values are not real.</span></span> <span data-ttu-id="4483a-162">Mettre à jour ces valeurs hello URL d’identificateur et de réponse réelle.</span><span class="sxs-lookup"><span data-stu-id="4483a-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="4483a-163">Contact [équipe de support technique de Marketo](http://investors.marketo.com/contactus.cfm) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="4483a-163">Contact [Marketo support team](http://investors.marketo.com/contactus.cfm) tooget these values.</span></span>
 
4. <span data-ttu-id="4483a-164">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="4483a-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_certificate.png) 

5. <span data-ttu-id="4483a-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="4483a-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4483a-168">Sur hello **Marketo Configuration** , cliquez sur **configurer de Marketo** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="4483a-168">On hello **Marketo Configuration** section, click **Configure Marketo** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4483a-169">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="4483a-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_configure.png) 

7. <span data-ttu-id="4483a-171">tooget Munchkin des Id de votre application, connectez-vous en tooMarketo à l’aide des informations d’identification d’administrateur et procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="4483a-171">tooget Munchkin Id of your application, log in tooMarketo using admin credentials and perform following actions:</span></span>
   
    <span data-ttu-id="4483a-172">a.</span><span class="sxs-lookup"><span data-stu-id="4483a-172">a.</span></span> <span data-ttu-id="4483a-173">Ouvrez une session dans l’application tooMarketo à l’aide des informations d’identification d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="4483a-173">Log in tooMarketo app using admin credentials.</span></span>
   
    <span data-ttu-id="4483a-174">b.</span><span class="sxs-lookup"><span data-stu-id="4483a-174">b.</span></span> <span data-ttu-id="4483a-175">Cliquez sur hello **Admin** bouton du volet de navigation supérieure hello.</span><span class="sxs-lookup"><span data-stu-id="4483a-175">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="4483a-177">c.</span><span class="sxs-lookup"><span data-stu-id="4483a-177">c.</span></span> <span data-ttu-id="4483a-178">Parcourir les menus d’intégration toohello, cliquez sur hello **lien de Munchkin**.</span><span class="sxs-lookup"><span data-stu-id="4483a-178">Navigate toohello Integration menu and click hello **Munchkin link**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_11.png)
   
    <span data-ttu-id="4483a-180">d.</span><span class="sxs-lookup"><span data-stu-id="4483a-180">d.</span></span> <span data-ttu-id="4483a-181">Copiez hello Id Munchkin indiqué sur l’écran hello et terminer votre URL de réponse dans l’Assistant de configuration hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4483a-181">Copy hello Munchkin Id shown on hello screen and complete your Reply URL in hello Azure AD configuration wizard.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_12.png) 

8. <span data-ttu-id="4483a-183">tooconfigure hello SSO dans l’application hello, procédez comme hello étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="4483a-183">tooconfigure hello SSO in hello application, follow hello below steps:</span></span>
   
    <span data-ttu-id="4483a-184">a.</span><span class="sxs-lookup"><span data-stu-id="4483a-184">a.</span></span> <span data-ttu-id="4483a-185">Ouvrez une session dans l’application tooMarketo à l’aide des informations d’identification d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="4483a-185">Log in tooMarketo app using admin credentials.</span></span>
   
    <span data-ttu-id="4483a-186">b.</span><span class="sxs-lookup"><span data-stu-id="4483a-186">b.</span></span> <span data-ttu-id="4483a-187">Cliquez sur hello **Admin** bouton du volet de navigation supérieure hello.</span><span class="sxs-lookup"><span data-stu-id="4483a-187">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="4483a-189">c.</span><span class="sxs-lookup"><span data-stu-id="4483a-189">c.</span></span> <span data-ttu-id="4483a-190">Parcourir les menus d’intégration toohello, cliquez sur **Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="4483a-190">Navigate toohello Integration menu and click **Single Sign On**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_07.png) 
   
    <span data-ttu-id="4483a-192">d.</span><span class="sxs-lookup"><span data-stu-id="4483a-192">d.</span></span> <span data-ttu-id="4483a-193">tooenable hello paramètres SAML, cliquez sur **modifier** bouton.</span><span class="sxs-lookup"><span data-stu-id="4483a-193">tooenable hello SAML Settings, click **Edit** button.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_08.png) 
   
    <span data-ttu-id="4483a-195">e.</span><span class="sxs-lookup"><span data-stu-id="4483a-195">e.</span></span> <span data-ttu-id="4483a-196">**Activez** les paramètres d’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="4483a-196">**Enabled** Single Sign-On settings.</span></span>
   
    <span data-ttu-id="4483a-197">f.</span><span class="sxs-lookup"><span data-stu-id="4483a-197">f.</span></span> <span data-ttu-id="4483a-198">Hello de coller **ID d’entité SAML**, Bonjour **ID de l’émetteur** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="4483a-198">Paste hello **SAML Entity ID**, in hello **Issuer ID** textbox.</span></span>
   
    <span data-ttu-id="4483a-199">g.</span><span class="sxs-lookup"><span data-stu-id="4483a-199">g.</span></span> <span data-ttu-id="4483a-200">Bonjour **ID d’entité** zone de texte, entrez l’URL hello `http://saml.marketo.com/sp`.</span><span class="sxs-lookup"><span data-stu-id="4483a-200">In hello **Entity ID** textbox, enter hello URL as `http://saml.marketo.com/sp`.</span></span>
   
    <span data-ttu-id="4483a-201">h.</span><span class="sxs-lookup"><span data-stu-id="4483a-201">h.</span></span> <span data-ttu-id="4483a-202">Sélectionnez hello emplacement de l’ID d’utilisateur en tant que **élément identificateur de nom**.</span><span class="sxs-lookup"><span data-stu-id="4483a-202">Select hello User ID Location as **Name Identifier element**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_09.png)
   
    > [!NOTE]
    > <span data-ttu-id="4483a-204">Si votre identificateur de l’utilisateur n’est pas valeur UPN puis modifier la valeur dans l’onglet d’attributs hello hello.</span><span class="sxs-lookup"><span data-stu-id="4483a-204">If your User Identifier is not UPN value then change hello value in hello Attribute tab.</span></span>
   
    <span data-ttu-id="4483a-205">i.</span><span class="sxs-lookup"><span data-stu-id="4483a-205">i.</span></span> <span data-ttu-id="4483a-206">Téléchargez le certificat hello, qui vous avez téléchargé à partir de l’Assistant de configuration d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4483a-206">Upload hello certificate, which you have downloaded from Azure AD configuration wizard.</span></span> <span data-ttu-id="4483a-207">**Enregistrer** hello paramètres.</span><span class="sxs-lookup"><span data-stu-id="4483a-207">**Save** hello settings.</span></span>
   
    <span data-ttu-id="4483a-208">j.</span><span class="sxs-lookup"><span data-stu-id="4483a-208">j.</span></span> <span data-ttu-id="4483a-209">Modifier les paramètres des Pages de redirection hello.</span><span class="sxs-lookup"><span data-stu-id="4483a-209">Edit hello Redirect Pages settings.</span></span>
   
    <span data-ttu-id="4483a-210">k.</span><span class="sxs-lookup"><span data-stu-id="4483a-210">k.</span></span> <span data-ttu-id="4483a-211">Hello de coller **SAML Sign-On URL du Service unique** Bonjour **URL de connexion** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="4483a-211">Paste hello **SAML Single Sign-On Service URL** in hello **Login URL** textbox.</span></span>
   
    <span data-ttu-id="4483a-212">l.</span><span class="sxs-lookup"><span data-stu-id="4483a-212">l.</span></span> <span data-ttu-id="4483a-213">Hello de coller **URL de déconnexion** Bonjour **URL de déconnexion** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="4483a-213">Paste hello **Sign-Out URL** in hello **Logout URL** textbox.</span></span>
   
    <span data-ttu-id="4483a-214">m.</span><span class="sxs-lookup"><span data-stu-id="4483a-214">m.</span></span> <span data-ttu-id="4483a-215">Bonjour **URL d’erreur**, copie votre **URL de l’instance Marketo** et cliquez sur **enregistrer** bouton toosave paramètres.</span><span class="sxs-lookup"><span data-stu-id="4483a-215">In hello **Error URL**, copy your **Marketo instance URL** and click **Save** button toosave settings.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_10.png)

9. <span data-ttu-id="4483a-217">tooenable hello SSO pour les utilisateurs, hello complet suivant des actions :</span><span class="sxs-lookup"><span data-stu-id="4483a-217">tooenable hello SSO for users, complete hello following actions:</span></span>
   
    <span data-ttu-id="4483a-218">a.</span><span class="sxs-lookup"><span data-stu-id="4483a-218">a.</span></span> <span data-ttu-id="4483a-219">Ouvrez une session dans l’application tooMarketo à l’aide des informations d’identification d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="4483a-219">Log in tooMarketo app using admin credentials.</span></span>
   
    <span data-ttu-id="4483a-220">b.</span><span class="sxs-lookup"><span data-stu-id="4483a-220">b.</span></span> <span data-ttu-id="4483a-221">Cliquez sur hello **Admin** bouton du volet de navigation supérieure hello.</span><span class="sxs-lookup"><span data-stu-id="4483a-221">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="4483a-223">c.</span><span class="sxs-lookup"><span data-stu-id="4483a-223">c.</span></span> <span data-ttu-id="4483a-224">Accédez toohello **sécurité** menu et cliquez sur **les paramètres de connexion**.</span><span class="sxs-lookup"><span data-stu-id="4483a-224">Navigate toohello **Security** menu and click **Login Settings**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_13.png)
   
    <span data-ttu-id="4483a-226">d.</span><span class="sxs-lookup"><span data-stu-id="4483a-226">d.</span></span> <span data-ttu-id="4483a-227">Vérifiez hello **nécessitent la SSO** option et **enregistrer** hello paramètres.</span><span class="sxs-lookup"><span data-stu-id="4483a-227">Check hello **Require SSO** option and **Save** hello settings.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_14.png)

> [!TIP]
> <span data-ttu-id="4483a-229">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="4483a-229">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4483a-230">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="4483a-230">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4483a-231">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4483a-231">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4483a-232">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="4483a-232">Creating an Azure AD test user</span></span>
<span data-ttu-id="4483a-233">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="4483a-233">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="4483a-235">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4483a-235">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4483a-236">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="4483a-236">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4483a-238">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="4483a-238">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4483a-240">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="4483a-240">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4483a-242">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="4483a-242">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4483a-244">a.</span><span class="sxs-lookup"><span data-stu-id="4483a-244">a.</span></span> <span data-ttu-id="4483a-245">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4483a-245">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4483a-246">b.</span><span class="sxs-lookup"><span data-stu-id="4483a-246">b.</span></span> <span data-ttu-id="4483a-247">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4483a-247">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4483a-248">c.</span><span class="sxs-lookup"><span data-stu-id="4483a-248">c.</span></span> <span data-ttu-id="4483a-249">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="4483a-249">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4483a-250">d.</span><span class="sxs-lookup"><span data-stu-id="4483a-250">d.</span></span> <span data-ttu-id="4483a-251">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="4483a-251">Click **Create**.</span></span>
 
### <a name="creating-a-marketo-test-user"></a><span data-ttu-id="4483a-252">Créer un utilisateur de test Marketo</span><span class="sxs-lookup"><span data-stu-id="4483a-252">Creating a Marketo test user</span></span>

<span data-ttu-id="4483a-253">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Marketo.</span><span class="sxs-lookup"><span data-stu-id="4483a-253">In this section, you create a user called Britta Simon in Marketo.</span></span> <span data-ttu-id="4483a-254">Suivez ces étapes de toocreate un utilisateur dans la plateforme de Marketo.</span><span class="sxs-lookup"><span data-stu-id="4483a-254">follow these steps toocreate a user in Marketo platform.</span></span>

1. <span data-ttu-id="4483a-255">Ouvrez une session dans l’application tooMarketo à l’aide des informations d’identification d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="4483a-255">Log in tooMarketo app using admin credentials.</span></span>

2. <span data-ttu-id="4483a-256">Cliquez sur hello **Admin** bouton du volet de navigation supérieure hello.</span><span class="sxs-lookup"><span data-stu-id="4483a-256">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 

3. <span data-ttu-id="4483a-258">Accédez toohello **sécurité** menu et cliquez sur **les utilisateurs et les rôles**</span><span class="sxs-lookup"><span data-stu-id="4483a-258">Navigate toohello **Security** menu and click **Users & Roles**</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_19.png)  

4. <span data-ttu-id="4483a-260">Cliquez sur hello **inviter un nouvel utilisateur** lien sur l’onglet utilisateurs de hello</span><span class="sxs-lookup"><span data-stu-id="4483a-260">Click hello **Invite New User** link on hello Users tab</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_15.png) 

5. <span data-ttu-id="4483a-262">Bonjour de remplissage hello inviter un nouvel utilisateur Assistant informations suivantes</span><span class="sxs-lookup"><span data-stu-id="4483a-262">In hello Invite New User wizard fill hello following information</span></span>
   
    <span data-ttu-id="4483a-263">a.</span><span class="sxs-lookup"><span data-stu-id="4483a-263">a.</span></span> <span data-ttu-id="4483a-264">Entrez hello utilisateur **par courrier électronique** adresse dans la zone de texte hello</span><span class="sxs-lookup"><span data-stu-id="4483a-264">Enter hello user **Email** address in hello textbox</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_16.png)
   
    <span data-ttu-id="4483a-266">b.</span><span class="sxs-lookup"><span data-stu-id="4483a-266">b.</span></span> <span data-ttu-id="4483a-267">Entrez hello **prénom** dans la zone de texte hello</span><span class="sxs-lookup"><span data-stu-id="4483a-267">Enter hello **First Name** in hello textbox</span></span>
   
    <span data-ttu-id="4483a-268">c.</span><span class="sxs-lookup"><span data-stu-id="4483a-268">c.</span></span> <span data-ttu-id="4483a-269">Entrez hello **nom** dans la zone de texte hello</span><span class="sxs-lookup"><span data-stu-id="4483a-269">Enter hello **Last Name**  in hello textbox</span></span>
   
    <span data-ttu-id="4483a-270">d.</span><span class="sxs-lookup"><span data-stu-id="4483a-270">d.</span></span> <span data-ttu-id="4483a-271">Cliquez sur **Suivant**</span><span class="sxs-lookup"><span data-stu-id="4483a-271">Click **Next**</span></span>

6. <span data-ttu-id="4483a-272">Bonjour **autorisations** onglet, sélectionnez hello **userRoles** et cliquez sur **suivant**</span><span class="sxs-lookup"><span data-stu-id="4483a-272">In hello **Permissions** tab, select hello **userRoles** and click **Next**</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_17.png)
7. <span data-ttu-id="4483a-274">Cliquez sur hello **envoyer** bouton invitation d’utilisateur toosend hello</span><span class="sxs-lookup"><span data-stu-id="4483a-274">Click hello **Send** button toosend hello user invitation</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_18.png)

8. <span data-ttu-id="4483a-276">Utilisateur reçoit une notification par courrier électronique de hello et a tooclick hello lier et modifier le compte de hello tooactivate hello mot de passe.</span><span class="sxs-lookup"><span data-stu-id="4483a-276">User receives hello email notification and has tooclick hello link and change hello password tooactivate hello account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4483a-277">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4483a-277">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4483a-278">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooMarketo.</span><span class="sxs-lookup"><span data-stu-id="4483a-278">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMarketo.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="4483a-280">**tooassign Britta Simon tooMarketo, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4483a-280">**tooassign Britta Simon tooMarketo, perform hello following steps:**</span></span>

1. <span data-ttu-id="4483a-281">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="4483a-281">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="4483a-283">Dans la liste des applications hello, sélectionnez **Marketo**.</span><span class="sxs-lookup"><span data-stu-id="4483a-283">In hello applications list, select **Marketo**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_app.png) 

3. <span data-ttu-id="4483a-285">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="4483a-285">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="4483a-287">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="4483a-287">Click **Add** button.</span></span> <span data-ttu-id="4483a-288">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="4483a-288">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="4483a-290">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="4483a-290">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4483a-291">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="4483a-291">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4483a-292">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="4483a-292">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4483a-293">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="4483a-293">Testing single sign-on</span></span>

<span data-ttu-id="4483a-294">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="4483a-294">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4483a-295">Lorsque vous cliquez sur mosaïque Marketo hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Marketo application.</span><span class="sxs-lookup"><span data-stu-id="4483a-295">When you click hello Marketo tile in hello Access Panel, you should get automatically signed-on tooyour Marketo application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4483a-296">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="4483a-296">Additional resources</span></span>

* [<span data-ttu-id="4483a-297">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4483a-297">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4483a-298">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="4483a-298">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_203.png

