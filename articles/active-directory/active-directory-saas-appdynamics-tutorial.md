---
title: "Didacticiel : Intégration d’Azure Active Directory à AppDynamics | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et AppDynamics."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 25fd1df0-411c-4f55-8be3-4273b543100f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 9b63afec73d7442e6ac1ce34b511beea6f43ffe4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-appdynamics"></a><span data-ttu-id="bae52-103">Didacticiel : Intégration d’Azure Active Directory à AppDynamics</span><span class="sxs-lookup"><span data-stu-id="bae52-103">Tutorial: Azure Active Directory integration with AppDynamics</span></span>

<span data-ttu-id="bae52-104">Dans ce didacticiel, vous apprendrez comment toointegrate AppDynamics avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bae52-104">In this tutorial, you learn how toointegrate AppDynamics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bae52-105">Intégration d’AppDynamics à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="bae52-105">Integrating AppDynamics with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bae52-106">Vous pouvez contrôler dans Azure AD qui a accès tooAppDynamics</span><span class="sxs-lookup"><span data-stu-id="bae52-106">You can control in Azure AD who has access tooAppDynamics</span></span>
- <span data-ttu-id="bae52-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooAppDynamics (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="bae52-107">You can enable your users tooautomatically get signed-on tooAppDynamics (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bae52-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="bae52-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bae52-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bae52-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bae52-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="bae52-110">Prerequisites</span></span>

<span data-ttu-id="bae52-111">tooconfigure intégration d’Azure AD à AppDynamics, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="bae52-111">tooconfigure Azure AD integration with AppDynamics, you need hello following items:</span></span>

- <span data-ttu-id="bae52-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="bae52-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bae52-113">Un abonnement AppDynamics pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="bae52-113">An AppDynamics single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bae52-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="bae52-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bae52-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="bae52-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bae52-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="bae52-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bae52-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bae52-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bae52-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="bae52-118">Scenario description</span></span>
<span data-ttu-id="bae52-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="bae52-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bae52-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="bae52-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bae52-121">Ajout d’AppDynamics à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="bae52-121">Adding AppDynamics from hello gallery</span></span>
2. <span data-ttu-id="bae52-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="bae52-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-appdynamics-from-hello-gallery"></a><span data-ttu-id="bae52-123">Ajout d’AppDynamics à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="bae52-123">Adding AppDynamics from hello gallery</span></span>
<span data-ttu-id="bae52-124">intégration de hello tooconfigure de AppDynamics dans Azure AD, vous devez tooadd AppDynamics à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="bae52-124">tooconfigure hello integration of AppDynamics into Azure AD, you need tooadd AppDynamics from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bae52-125">**tooadd AppDynamics à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bae52-125">**tooadd AppDynamics from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bae52-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="bae52-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bae52-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="bae52-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bae52-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="bae52-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="bae52-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="bae52-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="bae52-133">Dans la zone de recherche de hello, tapez **AppDynamics**.</span><span class="sxs-lookup"><span data-stu-id="bae52-133">In hello search box, type **AppDynamics**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_search.png)

5. <span data-ttu-id="bae52-135">Dans le volet de résultats hello, sélectionnez **AppDynamics**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="bae52-135">In hello results panel, select **AppDynamics**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bae52-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="bae52-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bae52-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec AppDynamics, en tirant parti d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="bae52-138">In this section, you configure and test Azure AD single sign-on with AppDynamics based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bae52-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent Bonjour dans AppDynamics est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bae52-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in AppDynamics is tooa user in Azure AD.</span></span> <span data-ttu-id="bae52-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur Bonjour dans AppDynamics doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="bae52-140">In other words, a link relationship between an Azure AD user and hello related user in AppDynamics needs toobe established.</span></span>

<span data-ttu-id="bae52-141">En l’occurrence, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="bae52-141">In AppDynamics, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="bae52-142">tooconfigure et test Azure AD l’authentification unique avec AppDynamics, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="bae52-142">tooconfigure and test Azure AD single sign-on with AppDynamics, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bae52-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="bae52-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bae52-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bae52-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bae52-145">**[Création d’un utilisateur de test AppDynamics](#creating-an-appdynamics-test-user)**  -toohave un équivalent de Britta Simon dans AppDynamics est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="bae52-145">**[Creating an AppDynamics test user](#creating-an-appdynamics-test-user)** - toohave a counterpart of Britta Simon in AppDynamics that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bae52-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="bae52-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bae52-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="bae52-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bae52-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="bae52-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bae52-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="bae52-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your AppDynamics application.</span></span>

<span data-ttu-id="bae52-150">**tooconfigure Azure AD single sign-on avec AppDynamics, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bae52-150">**tooconfigure Azure AD single sign-on with AppDynamics, perform hello following steps:**</span></span>

1. <span data-ttu-id="bae52-151">Bonjour portail Azure, sur hello **AppDynamics** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="bae52-151">In hello Azure portal, on hello **AppDynamics** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="bae52-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="bae52-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_samlbase.png)

3. <span data-ttu-id="bae52-155">Sur hello **AppDynamics domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="bae52-155">On hello **AppDynamics Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_url.png)

    <span data-ttu-id="bae52-157">a.</span><span class="sxs-lookup"><span data-stu-id="bae52-157">a.</span></span> <span data-ttu-id="bae52-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.saas.appdynamics.com`</span><span class="sxs-lookup"><span data-stu-id="bae52-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.saas.appdynamics.com`</span></span>

    <span data-ttu-id="bae52-159">b.</span><span class="sxs-lookup"><span data-stu-id="bae52-159">b.</span></span> <span data-ttu-id="bae52-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.saas.appdynamics.com/controller`</span><span class="sxs-lookup"><span data-stu-id="bae52-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.saas.appdynamics.com/controller`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bae52-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="bae52-161">These values are not real.</span></span> <span data-ttu-id="bae52-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="bae52-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="bae52-163">Contact [équipe de support Client de AppDynamics](https://www.appdynamics.com/support/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="bae52-163">Contact [AppDynamics Client support team](https://www.appdynamics.com/support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="bae52-164">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="bae52-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_certificate.png) 

5. <span data-ttu-id="bae52-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="bae52-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-appdynamics-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bae52-168">Sur hello **AppDynamics Configuration** , cliquez sur **AppDynamics de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="bae52-168">On hello **AppDynamics Configuration** section, click **Configure AppDynamics** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="bae52-169">Hello de copie **URL de déconnexion et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="bae52-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_configure.png) 

7. <span data-ttu-id="bae52-171">Dans une fenêtre de navigateur web, ouvrez une session dans le site d’entreprise AppDynamics tooyour en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="bae52-171">In a different web browser window, log in tooyour AppDynamics company site as an administrator.</span></span>

8. <span data-ttu-id="bae52-172">Dans la barre d’outils de hello en haut de hello, cliquez sur **paramètres**, puis cliquez sur **Administration**.</span><span class="sxs-lookup"><span data-stu-id="bae52-172">In hello toolbar on hello top, click **Settings**, and then click **Administration**.</span></span>
   
    <span data-ttu-id="bae52-173">![Administration](./media/active-directory-saas-appdynamics-tutorial/ic790216.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="bae52-173">![Administration](./media/active-directory-saas-appdynamics-tutorial/ic790216.png "Administration")</span></span>

9. <span data-ttu-id="bae52-174">Cliquez sur hello **fournisseur d’authentification** onglet.</span><span class="sxs-lookup"><span data-stu-id="bae52-174">Click hello **Authentication Provider** tab.</span></span>
   
    <span data-ttu-id="bae52-175">![Fournisseur d’authentification](./media/active-directory-saas-appdynamics-tutorial/ic790224.png "Fournisseur d’authentification")</span><span class="sxs-lookup"><span data-stu-id="bae52-175">![Authentication Provider](./media/active-directory-saas-appdynamics-tutorial/ic790224.png "Authentication Provider")</span></span>

10. <span data-ttu-id="bae52-176">Bonjour **fournisseur d’authentification** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="bae52-176">In hello **Authentication Provider** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="bae52-177">![Configuration SAML](./media/active-directory-saas-appdynamics-tutorial/ic790225.png "Configuration SAML")</span><span class="sxs-lookup"><span data-stu-id="bae52-177">![SAML Configuration](./media/active-directory-saas-appdynamics-tutorial/ic790225.png "SAML Configuration")</span></span>   

    <span data-ttu-id="bae52-178">a.</span><span class="sxs-lookup"><span data-stu-id="bae52-178">a.</span></span> <span data-ttu-id="bae52-179">Dans **Fournisseur d’authentification**, sélectionnez **SAML**.</span><span class="sxs-lookup"><span data-stu-id="bae52-179">As **Authentication Provider**, select **SAML**.</span></span>

    <span data-ttu-id="bae52-180">b.</span><span class="sxs-lookup"><span data-stu-id="bae52-180">b.</span></span> <span data-ttu-id="bae52-181">Bonjour **URL de connexion** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="bae52-181">In hello **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="bae52-182">c.</span><span class="sxs-lookup"><span data-stu-id="bae52-182">c.</span></span> <span data-ttu-id="bae52-183">Bonjour **URL de déconnexion** zone de texte, valeur hello coller **URL de déconnexion** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="bae52-183">In hello **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
       
    <span data-ttu-id="bae52-184">d.</span><span class="sxs-lookup"><span data-stu-id="bae52-184">d.</span></span> <span data-ttu-id="bae52-185">Ouvrez votre certificat codé en base 64 dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite toohello **certificat** zone de texte</span><span class="sxs-lookup"><span data-stu-id="bae52-185">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Certificate** textbox</span></span>

    <span data-ttu-id="bae52-186">e.</span><span class="sxs-lookup"><span data-stu-id="bae52-186">e.</span></span> <span data-ttu-id="bae52-187">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="bae52-187">Click **Save**.</span></span>

     <span data-ttu-id="bae52-188">![Enregistrer](./media/active-directory-saas-appdynamics-tutorial/ic777673.png "enregistrer")</span><span class="sxs-lookup"><span data-stu-id="bae52-188">![Save](./media/active-directory-saas-appdynamics-tutorial/ic777673.png "Save")</span></span>

> [!TIP]
> <span data-ttu-id="bae52-189">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="bae52-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bae52-190">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="bae52-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bae52-191">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bae52-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bae52-192">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="bae52-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="bae52-193">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="bae52-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="bae52-195">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bae52-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bae52-196">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="bae52-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bae52-198">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="bae52-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bae52-200">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="bae52-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bae52-202">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="bae52-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bae52-204">a.</span><span class="sxs-lookup"><span data-stu-id="bae52-204">a.</span></span> <span data-ttu-id="bae52-205">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bae52-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bae52-206">b.</span><span class="sxs-lookup"><span data-stu-id="bae52-206">b.</span></span> <span data-ttu-id="bae52-207">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bae52-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bae52-208">c.</span><span class="sxs-lookup"><span data-stu-id="bae52-208">c.</span></span> <span data-ttu-id="bae52-209">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="bae52-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bae52-210">d.</span><span class="sxs-lookup"><span data-stu-id="bae52-210">d.</span></span> <span data-ttu-id="bae52-211">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="bae52-211">Click **Create**.</span></span>
 
### <a name="creating-an-appdynamics-test-user"></a><span data-ttu-id="bae52-212">Création d’un utilisateur de test AppDynamics</span><span class="sxs-lookup"><span data-stu-id="bae52-212">Creating an AppDynamics test user</span></span>

<span data-ttu-id="bae52-213">tooenable Azure AD les utilisateurs toolog dans tooAppDynamics, vous devez les configurer dans AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="bae52-213">tooenable Azure AD users toolog in tooAppDynamics, they must be provisioned into AppDynamics.</span></span> <span data-ttu-id="bae52-214">Dans le cas de hello d’AppDynamics, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="bae52-214">In hello case of AppDynamics, provisioning is a manual task.</span></span>

<span data-ttu-id="bae52-215">**configuration, de l’utilisateur tooconfigure effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bae52-215">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="bae52-216">Ouvrez une session dans tooyour site d’entreprise AppDynamics en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="bae52-216">Log in tooyour AppDynamics company site as an administrator.</span></span>

2. <span data-ttu-id="bae52-217">Accédez trop**utilisateurs**, puis cliquez sur  **+**  tooopen hello **Create User** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="bae52-217">Go too**Users**, and then click **+** tooopen hello **Create User** dialog.</span></span>
   
    <span data-ttu-id="bae52-218">![Utilisateurs](./media/active-directory-saas-appdynamics-tutorial/ic790229.png "Utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="bae52-218">![Users](./media/active-directory-saas-appdynamics-tutorial/ic790229.png "Users")</span></span>

3. <span data-ttu-id="bae52-219">Bonjour **Create User** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="bae52-219">In hello **Create User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="bae52-220">![Create User](./media/active-directory-saas-appdynamics-tutorial/ic790230.png "Create User")</span><span class="sxs-lookup"><span data-stu-id="bae52-220">![Create User](./media/active-directory-saas-appdynamics-tutorial/ic790230.png "Create User")</span></span>
   
    <span data-ttu-id="bae52-221">a.</span><span class="sxs-lookup"><span data-stu-id="bae52-221">a.</span></span> <span data-ttu-id="bae52-222">Hello de type **nom d’utilisateur**, **nom**, **messagerie**, **nouveau mot de passe**, **Repeat New Password** d’un AAD valide compte tooprovision dans hello relatives des zones de texte.</span><span class="sxs-lookup"><span data-stu-id="bae52-222">Type hello **Username**, **Name**, **Email**, **New Password**, **Repeat New Password** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>

    <span data-ttu-id="bae52-223">b.</span><span class="sxs-lookup"><span data-stu-id="bae52-223">b.</span></span> <span data-ttu-id="bae52-224">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="bae52-224">Click **Save**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="bae52-225">Vous pouvez utiliser n’importe quel autre occurrence utilisateur compte outil de création ou API fournie par AppDynamics tooprovision comptes d’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bae52-225">You can use any other AppDynamics user account creation tools or APIs provided by AppDynamics tooprovision Azure AD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bae52-226">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="bae52-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bae52-227">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooAppDynamics.</span><span class="sxs-lookup"><span data-stu-id="bae52-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAppDynamics.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="bae52-229">**tooassign Britta Simon tooAppDynamics, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bae52-229">**tooassign Britta Simon tooAppDynamics, perform hello following steps:**</span></span>

1. <span data-ttu-id="bae52-230">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="bae52-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="bae52-232">Dans la liste des applications hello, sélectionnez **AppDynamics**.</span><span class="sxs-lookup"><span data-stu-id="bae52-232">In hello applications list, select **AppDynamics**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_app.png) 

3. <span data-ttu-id="bae52-234">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="bae52-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="bae52-236">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="bae52-236">Click **Add** button.</span></span> <span data-ttu-id="bae52-237">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="bae52-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="bae52-239">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="bae52-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bae52-240">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="bae52-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bae52-241">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="bae52-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bae52-242">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="bae52-242">Testing single sign-on</span></span>

<span data-ttu-id="bae52-243">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="bae52-243">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bae52-244">Lorsque vous cliquez sur hello AppDynamics vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour AppDynamics application.</span><span class="sxs-lookup"><span data-stu-id="bae52-244">When you click hello AppDynamics tile in hello Access Panel, you should get automatically signed-on tooyour AppDynamics application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bae52-245">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="bae52-245">Additional resources</span></span>

* [<span data-ttu-id="bae52-246">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bae52-246">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bae52-247">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="bae52-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_203.png

