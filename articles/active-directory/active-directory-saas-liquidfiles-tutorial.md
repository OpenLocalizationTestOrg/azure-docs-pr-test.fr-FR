---
title: "Didacticiel : Intégration d’Azure Active Directory avec LiquidFiles | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et LiquidFiles."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cb517134-0b34-4a74-b40c-5a3223ca81b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 67eb888090f81e0ceb791ed45d564b98fe1eb6d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-liquidfiles"></a><span data-ttu-id="bc4db-103">Didacticiel : Intégration d’Azure Active Directory avec LiquidFiles</span><span class="sxs-lookup"><span data-stu-id="bc4db-103">Tutorial: Azure Active Directory integration with LiquidFiles</span></span>

<span data-ttu-id="bc4db-104">Dans ce didacticiel, vous apprendrez comment toointegrate LiquidFiles avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bc4db-104">In this tutorial, you learn how toointegrate LiquidFiles with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bc4db-105">Intégration LiquidFiles à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="bc4db-105">Integrating LiquidFiles with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bc4db-106">Vous pouvez contrôler dans Azure AD qui a accès tooLiquidFiles</span><span class="sxs-lookup"><span data-stu-id="bc4db-106">You can control in Azure AD who has access tooLiquidFiles</span></span>
- <span data-ttu-id="bc4db-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooLiquidFiles (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="bc4db-107">You can enable your users tooautomatically get signed-on tooLiquidFiles (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bc4db-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="bc4db-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bc4db-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bc4db-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bc4db-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="bc4db-110">Prerequisites</span></span>

<span data-ttu-id="bc4db-111">tooconfigure intégration d’Azure AD avec LiquidFiles, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="bc4db-111">tooconfigure Azure AD integration with LiquidFiles, you need hello following items:</span></span>

- <span data-ttu-id="bc4db-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="bc4db-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bc4db-113">Un abonnement LiquidFiles pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="bc4db-113">A LiquidFiles single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bc4db-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="bc4db-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bc4db-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="bc4db-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bc4db-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="bc4db-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bc4db-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bc4db-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bc4db-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="bc4db-118">Scenario description</span></span>
<span data-ttu-id="bc4db-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="bc4db-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bc4db-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="bc4db-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bc4db-121">Ajout de LiquidFiles à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="bc4db-121">Adding LiquidFiles from hello gallery</span></span>
2. <span data-ttu-id="bc4db-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="bc4db-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-liquidfiles-from-hello-gallery"></a><span data-ttu-id="bc4db-123">Ajout de LiquidFiles à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="bc4db-123">Adding LiquidFiles from hello gallery</span></span>
<span data-ttu-id="bc4db-124">intégration de hello tooconfigure de LiquidFiles dans Azure AD, vous devez tooadd LiquidFiles à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="bc4db-124">tooconfigure hello integration of LiquidFiles into Azure AD, you need tooadd LiquidFiles from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bc4db-125">**tooadd LiquidFiles à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bc4db-125">**tooadd LiquidFiles from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bc4db-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="bc4db-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bc4db-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="bc4db-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bc4db-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="bc4db-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="bc4db-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="bc4db-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="bc4db-133">Dans la zone de recherche de hello, tapez **LiquidFiles**.</span><span class="sxs-lookup"><span data-stu-id="bc4db-133">In hello search box, type **LiquidFiles**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_search.png)

5. <span data-ttu-id="bc4db-135">Dans le volet de résultats hello, sélectionnez **LiquidFiles**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="bc4db-135">In hello results panel, select **LiquidFiles**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bc4db-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="bc4db-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bc4db-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec LiquidFiles sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="bc4db-138">In this section, you configure and test Azure AD single sign-on with LiquidFiles based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bc4db-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans LiquidFiles est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bc4db-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LiquidFiles is tooa user in Azure AD.</span></span> <span data-ttu-id="bc4db-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans LiquidFiles doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="bc4db-140">In other words, a link relationship between an Azure AD user and hello related user in LiquidFiles needs toobe established.</span></span>

<span data-ttu-id="bc4db-141">Dans LiquidFiles, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="bc4db-141">In LiquidFiles, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="bc4db-142">tooconfigure et test Azure AD l’authentification unique avec LiquidFiles, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="bc4db-142">tooconfigure and test Azure AD single sign-on with LiquidFiles, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bc4db-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="bc4db-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bc4db-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bc4db-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bc4db-145">**[Création d’un utilisateur de test LiquidFiles](#creating-a-liquidfiles-test-user)**  -toohave un équivalent de Britta Simon dans LiquidFiles est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="bc4db-145">**[Creating a LiquidFiles test user](#creating-a-liquidfiles-test-user)** - toohave a counterpart of Britta Simon in LiquidFiles that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bc4db-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="bc4db-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bc4db-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="bc4db-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bc4db-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="bc4db-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bc4db-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application LiquidFiles.</span><span class="sxs-lookup"><span data-stu-id="bc4db-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LiquidFiles application.</span></span>

<span data-ttu-id="bc4db-150">**tooconfigure Azure AD single sign-on avec LiquidFiles, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bc4db-150">**tooconfigure Azure AD single sign-on with LiquidFiles, perform hello following steps:**</span></span>

1. <span data-ttu-id="bc4db-151">Bonjour portail Azure, sur hello **LiquidFiles** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="bc4db-151">In hello Azure portal, on hello **LiquidFiles** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="bc4db-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="bc4db-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_samlbase.png)

3. <span data-ttu-id="bc4db-155">Sur hello **LiquidFiles domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="bc4db-155">On hello **LiquidFiles Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_url.png)

    <span data-ttu-id="bc4db-157">a.</span><span class="sxs-lookup"><span data-stu-id="bc4db-157">a.</span></span> <span data-ttu-id="bc4db-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<YOUR_SERVER_URL>/saml/init`</span><span class="sxs-lookup"><span data-stu-id="bc4db-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<YOUR_SERVER_URL>/saml/init`</span></span>

    <span data-ttu-id="bc4db-159">b.</span><span class="sxs-lookup"><span data-stu-id="bc4db-159">b.</span></span> <span data-ttu-id="bc4db-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<YOUR_SERVER_URL>`</span><span class="sxs-lookup"><span data-stu-id="bc4db-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<YOUR_SERVER_URL>`</span></span>

    <span data-ttu-id="bc4db-161">c.</span><span class="sxs-lookup"><span data-stu-id="bc4db-161">c.</span></span> <span data-ttu-id="bc4db-162">b.</span><span class="sxs-lookup"><span data-stu-id="bc4db-162">b.</span></span> <span data-ttu-id="bc4db-163">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<YOUR_SERVER_URL>/saml/consume`</span><span class="sxs-lookup"><span data-stu-id="bc4db-163">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<YOUR_SERVER_URL>/saml/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bc4db-164">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="bc4db-164">These values are not real.</span></span> <span data-ttu-id="bc4db-165">Mise à jour ces valeurs avec hello Sign-On URL réelle, identificateur et URL de réponse.</span><span class="sxs-lookup"><span data-stu-id="bc4db-165">Update these values with hello actual Sign-On URL, Identifier and, Reply URL.</span></span> <span data-ttu-id="bc4db-166">Contact [équipe de support Client de LiquidFiles](https://www.liquidfiles.com/support.html) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="bc4db-166">Contact [LiquidFiles Client support team](https://www.liquidfiles.com/support.html) tooget these values.</span></span> 
 
4. <span data-ttu-id="bc4db-167">Sur hello **le certificat de signature SAML** section, hello de copie **l’empreinte numérique** valeur du certificat.</span><span class="sxs-lookup"><span data-stu-id="bc4db-167">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_certificate.png) 

5. <span data-ttu-id="bc4db-169">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="bc4db-169">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bc4db-171">Sur hello **LiquidFiles Configuration** , cliquez sur **LiquidFiles de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="bc4db-171">On hello **LiquidFiles Configuration** section, click **Configure LiquidFiles** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="bc4db-172">Hello de copie **URL de déconnexion et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="bc4db-172">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_configure.png)
 
7. <span data-ttu-id="bc4db-174">Site d’entreprise LiquidFiles tooyour ouverture de session en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="bc4db-174">Sign-on tooyour LiquidFiles company site as administrator.</span></span>

8. <span data-ttu-id="bc4db-175">Cliquez sur **Single Sign-On** Bonjour **administration > Configuration** à partir du menu de hello.</span><span class="sxs-lookup"><span data-stu-id="bc4db-175">Click **Single Sign-On** in hello **Admin > Configuration** from hello menu.</span></span>

9. <span data-ttu-id="bc4db-176">Sur hello **Configuration de l’authentification unique** page, effectuer hello comme suit</span><span class="sxs-lookup"><span data-stu-id="bc4db-176">On hello **Single Sign-On Configuration** page, perform hello following steps</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-liquidfiles-tutorial/tutorial_single_01.png)

    <span data-ttu-id="bc4db-178">a.</span><span class="sxs-lookup"><span data-stu-id="bc4db-178">a.</span></span> <span data-ttu-id="bc4db-179">Pour **Single Sign On Method** (Méthode d’authentification unique), sélectionnez **SAML 2**.</span><span class="sxs-lookup"><span data-stu-id="bc4db-179">As **Single Sign On Method**, select **SAML 2**.</span></span>

    <span data-ttu-id="bc4db-180">b.</span><span class="sxs-lookup"><span data-stu-id="bc4db-180">b.</span></span> <span data-ttu-id="bc4db-181">Bonjour **URL de connexion IDP** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="bc4db-181">In hello **IDP Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="bc4db-182">c.</span><span class="sxs-lookup"><span data-stu-id="bc4db-182">c.</span></span> <span data-ttu-id="bc4db-183">Bonjour **URL de déconnexion IDP** zone de texte, valeur hello coller **URL de déconnexion**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="bc4db-183">In hello **IDP Logout URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="bc4db-184">d.</span><span class="sxs-lookup"><span data-stu-id="bc4db-184">d.</span></span> <span data-ttu-id="bc4db-185">Bonjour **IDP Cert Fingerprint** zone de texte, collez hello **l’empreinte numérique** valeur sur laquelle vous avez copié à partir du portail Azure...</span><span class="sxs-lookup"><span data-stu-id="bc4db-185">In hello **IDP Cert Fingerprint** textbox, paste hello **THUMBPRINT** value which you have copied from Azure portal..</span></span>

    <span data-ttu-id="bc4db-186">e.</span><span class="sxs-lookup"><span data-stu-id="bc4db-186">e.</span></span> <span data-ttu-id="bc4db-187">Dans la zone de texte Nom du Format d’identificateur hello, tapez la valeur de hello **urn : oasis : noms : tc : SAML:1.1:nameid-format : emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="bc4db-187">In hello Name Identifier Format textbox, type hello value **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="bc4db-188">f.</span><span class="sxs-lookup"><span data-stu-id="bc4db-188">f.</span></span> <span data-ttu-id="bc4db-189">Type de hello contexte d’authentification de zone de texte, valeur de hello **urn : oasis : noms : tc : SAML:2.0:ac:classes:PasswordProtectedTransport**.</span><span class="sxs-lookup"><span data-stu-id="bc4db-189">In hello Authn Context textbox, type hello value **urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport**.</span></span>

    <span data-ttu-id="bc4db-190">g.</span><span class="sxs-lookup"><span data-stu-id="bc4db-190">g.</span></span> <span data-ttu-id="bc4db-191">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="bc4db-191">Click **Save**.</span></span>  

> [!TIP]
> <span data-ttu-id="bc4db-192">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="bc4db-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bc4db-193">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="bc4db-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bc4db-194">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bc4db-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bc4db-195">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="bc4db-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="bc4db-196">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="bc4db-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="bc4db-198">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bc4db-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bc4db-199">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="bc4db-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bc4db-201">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="bc4db-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bc4db-203">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="bc4db-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bc4db-205">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="bc4db-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bc4db-207">a.</span><span class="sxs-lookup"><span data-stu-id="bc4db-207">a.</span></span> <span data-ttu-id="bc4db-208">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bc4db-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bc4db-209">b.</span><span class="sxs-lookup"><span data-stu-id="bc4db-209">b.</span></span> <span data-ttu-id="bc4db-210">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bc4db-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bc4db-211">c.</span><span class="sxs-lookup"><span data-stu-id="bc4db-211">c.</span></span> <span data-ttu-id="bc4db-212">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="bc4db-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bc4db-213">d.</span><span class="sxs-lookup"><span data-stu-id="bc4db-213">d.</span></span> <span data-ttu-id="bc4db-214">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="bc4db-214">Click **Create**.</span></span>
 
### <a name="creating-a-liquidfiles-test-user"></a><span data-ttu-id="bc4db-215">Création d’un utilisateur de test LiquidFiles</span><span class="sxs-lookup"><span data-stu-id="bc4db-215">Creating a LiquidFiles test user</span></span>

<span data-ttu-id="bc4db-216">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans LiquidFiles.</span><span class="sxs-lookup"><span data-stu-id="bc4db-216">hello objective of this section is toocreate a user called Britta Simon in LiquidFiles.</span></span> <span data-ttu-id="bc4db-217">Travailler avec votre tooget administrateur du serveur LiquidFiles vous-même ajoutés en tant qu’utilisateur avant de vous connecter tooyour LiquidFiles application.</span><span class="sxs-lookup"><span data-stu-id="bc4db-217">Work with your LiquidFiles server administrator tooget yourself added as a user before logging in tooyour LiquidFiles application.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bc4db-218">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="bc4db-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bc4db-219">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooLiquidFiles.</span><span class="sxs-lookup"><span data-stu-id="bc4db-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLiquidFiles.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="bc4db-221">**tooassign Britta Simon tooLiquidFiles, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bc4db-221">**tooassign Britta Simon tooLiquidFiles, perform hello following steps:**</span></span>

1. <span data-ttu-id="bc4db-222">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="bc4db-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="bc4db-224">Dans la liste des applications hello, sélectionnez **LiquidFiles**.</span><span class="sxs-lookup"><span data-stu-id="bc4db-224">In hello applications list, select **LiquidFiles**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_app.png) 

3. <span data-ttu-id="bc4db-226">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="bc4db-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="bc4db-228">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="bc4db-228">Click **Add** button.</span></span> <span data-ttu-id="bc4db-229">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="bc4db-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="bc4db-231">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="bc4db-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bc4db-232">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="bc4db-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bc4db-233">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="bc4db-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bc4db-234">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="bc4db-234">Testing single sign-on</span></span>

<span data-ttu-id="bc4db-235">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="bc4db-235">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bc4db-236">Lorsque vous cliquez sur hello LiquidFiles vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour LiquidFiles application.</span><span class="sxs-lookup"><span data-stu-id="bc4db-236">When you click hello LiquidFiles tile in hello Access Panel, you should get automatically signed-on tooyour LiquidFiles application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bc4db-237">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="bc4db-237">Additional resources</span></span>

* [<span data-ttu-id="bc4db-238">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bc4db-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bc4db-239">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="bc4db-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_203.png

