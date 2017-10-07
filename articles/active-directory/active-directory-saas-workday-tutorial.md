---
title: "Didacticiel : Intégration d’Azure Active Directory à Workday | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de la journée de travail."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e9da692e-4a65-4231-8ab3-bc9a87b10bca
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: aaa41e372e45f464c4540a70fc79c98dbc06d6b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workday"></a><span data-ttu-id="065f3-103">Didacticiel : Intégration d’Azure Active Directory à Workday</span><span class="sxs-lookup"><span data-stu-id="065f3-103">Tutorial: Azure Active Directory integration with Workday</span></span>

<span data-ttu-id="065f3-104">Dans ce didacticiel, vous apprendrez comment toointegrate Workday avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="065f3-104">In this tutorial, you learn how toointegrate Workday with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="065f3-105">Intégration de Workday à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="065f3-105">Integrating Workday with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="065f3-106">Vous pouvez contrôler dans Azure AD qui a accès tooWorkday</span><span class="sxs-lookup"><span data-stu-id="065f3-106">You can control in Azure AD who has access tooWorkday</span></span>
- <span data-ttu-id="065f3-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooWorkday (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="065f3-107">You can enable your users tooautomatically get signed-on tooWorkday (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="065f3-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="065f3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="065f3-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="065f3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="065f3-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="065f3-110">Prerequisites</span></span>

<span data-ttu-id="065f3-111">tooconfigure intégration d’Azure AD à Workday, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="065f3-111">tooconfigure Azure AD integration with Workday, you need hello following items:</span></span>

- <span data-ttu-id="065f3-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="065f3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="065f3-113">Un abonnement Workday pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="065f3-113">A Workday single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="065f3-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="065f3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="065f3-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="065f3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="065f3-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="065f3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="065f3-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="065f3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="065f3-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="065f3-118">Scenario description</span></span>
<span data-ttu-id="065f3-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="065f3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="065f3-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="065f3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="065f3-121">Ajout de journée de travail à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="065f3-121">Adding Workday from hello gallery</span></span>
2. <span data-ttu-id="065f3-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="065f3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workday-from-hello-gallery"></a><span data-ttu-id="065f3-123">Ajout de journée de travail à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="065f3-123">Adding Workday from hello gallery</span></span>
<span data-ttu-id="065f3-124">tooconfigure hello intégration de Workday dans Azure AD, vous devez tooadd journée de travail à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="065f3-124">tooconfigure hello integration of Workday into Azure AD, you need tooadd Workday from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="065f3-125">**tooadd journée de travail à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="065f3-125">**tooadd Workday from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="065f3-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="065f3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="065f3-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="065f3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="065f3-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="065f3-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="065f3-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="065f3-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="065f3-133">Dans la zone de recherche de hello, tapez **Workday**.</span><span class="sxs-lookup"><span data-stu-id="065f3-133">In hello search box, type **Workday**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workday-tutorial/tutorial_workday_search.png)

5. <span data-ttu-id="065f3-135">Dans le volet de résultats hello, sélectionnez **Workday**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="065f3-135">In hello results panel, select **Workday**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workday-tutorial/tutorial_workday_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="065f3-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="065f3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="065f3-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Workday avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="065f3-138">In this section, you configure and test Azure AD single sign-on with Workday based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="065f3-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Workday est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="065f3-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workday is tooa user in Azure AD.</span></span> <span data-ttu-id="065f3-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Workday doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="065f3-140">In other words, a link relationship between an Azure AD user and hello related user in Workday needs toobe established.</span></span>

<span data-ttu-id="065f3-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans la journée de travail.</span><span class="sxs-lookup"><span data-stu-id="065f3-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Workday.</span></span>

<span data-ttu-id="065f3-142">tooconfigure et test Azure AD l’authentification unique avec une journée de travail, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="065f3-142">tooconfigure and test Azure AD single sign-on with Workday, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="065f3-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="065f3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="065f3-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="065f3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="065f3-145">**[Création d’un utilisateur de test Workday](#creating-a-workday-test-user)**  -toohave un équivalent de Britta Simon dans Workday est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="065f3-145">**[Creating a Workday test user](#creating-a-workday-test-user)** - toohave a counterpart of Britta Simon in Workday that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="065f3-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="065f3-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="065f3-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="065f3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="065f3-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="065f3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="065f3-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de la journée de travail.</span><span class="sxs-lookup"><span data-stu-id="065f3-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workday application.</span></span>

<span data-ttu-id="065f3-150">**tooconfigure Azure AD single sign-on avec Workday, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="065f3-150">**tooconfigure Azure AD single sign-on with Workday, perform hello following steps:**</span></span>

1. <span data-ttu-id="065f3-151">Bonjour portail Azure, sur hello **Workday** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="065f3-151">In hello Azure portal, on hello **Workday** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="065f3-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="065f3-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-workday-tutorial/tutorial_workday_samlbase.png)

3. <span data-ttu-id="065f3-155">Sur hello **domaine de la journée de travail et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="065f3-155">On hello **Workday Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-workday-tutorial/tutorial_workday_url.png)

    <span data-ttu-id="065f3-157">a.</span><span class="sxs-lookup"><span data-stu-id="065f3-157">a.</span></span> <span data-ttu-id="065f3-158">Bonjour **URL de connexion** valeur hello de type en tant que zone de texte :`https://impl.workday.com/<tenant>/login-saml2.htmld`</span><span class="sxs-lookup"><span data-stu-id="065f3-158">In hello **Sign-on URL** textbox, type hello value as: `https://impl.workday.com/<tenant>/login-saml2.htmld`</span></span>

    <span data-ttu-id="065f3-159">b.</span><span class="sxs-lookup"><span data-stu-id="065f3-159">b.</span></span> <span data-ttu-id="065f3-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://impl.workday.com/<tenant>/login-saml.htmld`</span><span class="sxs-lookup"><span data-stu-id="065f3-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://impl.workday.com/<tenant>/login-saml.htmld`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="065f3-161">Ces valeurs ne sont pas hello réel.</span><span class="sxs-lookup"><span data-stu-id="065f3-161">These values are not hello real.</span></span> <span data-ttu-id="065f3-162">Mettre à jour ces valeurs avec l’URL de connexion réel hello et URL de réponse.</span><span class="sxs-lookup"><span data-stu-id="065f3-162">Update these values with hello actual Sign-on URL and Reply URL.</span></span> <span data-ttu-id="065f3-163">Votre URL de réponse doit avoir un sous-domaine (par exemple, www, wd2, wd3, wd3-impl, wd5, wd5-impl).</span><span class="sxs-lookup"><span data-stu-id="065f3-163">Your reply URL must have a subdomain for example: www, wd2, wd3, wd3-impl, wd5, wd5-impl).</span></span> <span data-ttu-id="065f3-164">Quelque chose comme « *http://www.myworkday.com* » fonctionnera, mais pas « *http://myworkday.com* ».</span><span class="sxs-lookup"><span data-stu-id="065f3-164">Using something like "*http://www.myworkday.com*" works but "*http://myworkday.com*" does not.</span></span> <span data-ttu-id="065f3-165">Contact [équipe de support Workday Client](https://www.workday.com/en-us/partners-services/services/support.html) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="065f3-165">Contact [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) tooget these values.</span></span> 
 

4. <span data-ttu-id="065f3-166">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="065f3-166">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-workday-tutorial/tutorial_workday_certificate.png) 

5. <span data-ttu-id="065f3-168">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="065f3-168">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-workday-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="065f3-170">Sur hello **Workday Configuration** , cliquez sur **configurer de Workday** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="065f3-170">On hello **Workday Configuration** section, click **Configure Workday** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="065f3-171">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="065f3-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    <span data-ttu-id="065f3-172">![Configurer l’authentification unique](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="065f3-172">![Configure Single Sign-On](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS></span></span>
7. <span data-ttu-id="065f3-173">Dans une fenêtre de navigateur web, ouvrez une session dans le site d’entreprise Workday tooyour en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="065f3-173">In a different web browser window, log in tooyour Workday company site as an administrator.</span></span>

8. <span data-ttu-id="065f3-174">Accédez trop**Menu \> banc d’essai**.</span><span class="sxs-lookup"><span data-stu-id="065f3-174">Go too**Menu \> Workbench**.</span></span>
   
    <span data-ttu-id="065f3-175">![Workbench](./media/active-directory-saas-workday-tutorial/IC782923.png "Workbench")</span><span class="sxs-lookup"><span data-stu-id="065f3-175">![Workbench](./media/active-directory-saas-workday-tutorial/IC782923.png "Workbench")</span></span>

9. <span data-ttu-id="065f3-176">Accédez trop**compte Administration**.</span><span class="sxs-lookup"><span data-stu-id="065f3-176">Go too**Account Administration**.</span></span>
   
    <span data-ttu-id="065f3-177">![Compte d’administration](./media/active-directory-saas-workday-tutorial/IC782924.png "Compte d’administration")</span><span class="sxs-lookup"><span data-stu-id="065f3-177">![Account Administration](./media/active-directory-saas-workday-tutorial/IC782924.png "Account Administration")</span></span>

10. <span data-ttu-id="065f3-178">Accédez trop**Edit Tenant Setup – Security**.</span><span class="sxs-lookup"><span data-stu-id="065f3-178">Go too**Edit Tenant Setup – Security**.</span></span>
   
    <span data-ttu-id="065f3-179">![Modifier la sécurité du locataire](./media/active-directory-saas-workday-tutorial/IC782925.png "Modifier la sécurité du locataire")</span><span class="sxs-lookup"><span data-stu-id="065f3-179">![Edit Tenant Security](./media/active-directory-saas-workday-tutorial/IC782925.png "Edit Tenant Security")</span></span>

11. <span data-ttu-id="065f3-180">Bonjour **URL de Redirection** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="065f3-180">In hello **Redirection URLs** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="065f3-181">![URL de redirection](./media/active-directory-saas-workday-tutorial/IC7829581.png "URL de redirection")</span><span class="sxs-lookup"><span data-stu-id="065f3-181">![Redirection URLs](./media/active-directory-saas-workday-tutorial/IC7829581.png "Redirection URLs")</span></span>
   
    <span data-ttu-id="065f3-182">a.</span><span class="sxs-lookup"><span data-stu-id="065f3-182">a.</span></span> <span data-ttu-id="065f3-183">Cliquez sur le **signe plus**pour ajouter une ligne.</span><span class="sxs-lookup"><span data-stu-id="065f3-183">Click **Add Row**.</span></span>
   
    <span data-ttu-id="065f3-184">b.</span><span class="sxs-lookup"><span data-stu-id="065f3-184">b.</span></span> <span data-ttu-id="065f3-185">Bonjour **URL de redirection de connexion** zone de texte et hello **URL de redirection Mobile** hello de type zone de texte **URL de connexion** vous avez entré sur hello **Workday domaine et URL** section Hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="065f3-185">In hello **Login Redirect URL** textbox and hello **Mobile Redirect URL** textbox, type hello **Sign-on URL** you have entered on hello **Workday Domain and URLs** section of hello Azure portal.</span></span>
   
    <span data-ttu-id="065f3-186">c.</span><span class="sxs-lookup"><span data-stu-id="065f3-186">c.</span></span> <span data-ttu-id="065f3-187">Bonjour portail Azure, sur hello **configurer l’authentification** fenêtre, hello de copie **URL de déconnexion**, puis collez-la dans hello **URL de redirection de déconnexion** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="065f3-187">In hello Azure portal, on hello **Configure sign-on** window, copy hello **Sign-Out URL**, and then paste it into hello **Logout Redirect URL** textbox.</span></span>
   
    <span data-ttu-id="065f3-188">d.</span><span class="sxs-lookup"><span data-stu-id="065f3-188">d.</span></span>  <span data-ttu-id="065f3-189">Dans **environnement** zone de texte, nom d’environnement de type hello.</span><span class="sxs-lookup"><span data-stu-id="065f3-189">In **Environment** textbox, type hello environment name.</span></span>  

    >[!NOTE]
    > <span data-ttu-id="065f3-190">Hello valeur d’attribut d’environnement hello est liée toohello valeur URL hello du client :</span><span class="sxs-lookup"><span data-stu-id="065f3-190">hello value of hello Environment attribute is tied toohello value of hello tenant URL:</span></span>  
    ><span data-ttu-id="065f3-191">-Si le nom de domaine hello d’URL de locataire Workday hello commence par impl par exemple : *https://impl.workday.com/\<client\>/login-saml2.htmld*), hello **environnement** attribut doit être défini à tooImplementation.</span><span class="sxs-lookup"><span data-stu-id="065f3-191">-If hello domain name of hello Workday tenant URL starts with impl for example: *https://impl.workday.com/\<tenant\>/login-saml2.htmld*), hello **Environment** attribute must be set tooImplementation.</span></span>  
    ><span data-ttu-id="065f3-192">-Si le nom de domaine hello commence par quelque chose d’autre, vous devez toocontact [équipe de support Workday Client](https://www.workday.com/en-us/partners-services/services/support.html) mise en correspondance hello tooget **environnement** valeur.</span><span class="sxs-lookup"><span data-stu-id="065f3-192">-If hello domain name starts with something else, you need toocontact [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) tooget hello matching **Environment** value.</span></span>

12. <span data-ttu-id="065f3-193">Bonjour **le programme d’installation SAML** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="065f3-193">In hello **SAML Setup** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="065f3-194">![Configuration de SAML](./media/active-directory-saas-workday-tutorial/IC782926.png "Configuration de SAML")</span><span class="sxs-lookup"><span data-stu-id="065f3-194">![SAML Setup](./media/active-directory-saas-workday-tutorial/IC782926.png "SAML Setup")</span></span>
   
    <span data-ttu-id="065f3-195">a.</span><span class="sxs-lookup"><span data-stu-id="065f3-195">a.</span></span>  <span data-ttu-id="065f3-196">Sélectionnez **Enable SAML Authentication**.</span><span class="sxs-lookup"><span data-stu-id="065f3-196">Select **Enable SAML Authentication**.</span></span>
   
    <span data-ttu-id="065f3-197">b.</span><span class="sxs-lookup"><span data-stu-id="065f3-197">b.</span></span>  <span data-ttu-id="065f3-198">Cliquez sur le **signe plus**pour ajouter une ligne.</span><span class="sxs-lookup"><span data-stu-id="065f3-198">Click **Add Row**.</span></span>

13. <span data-ttu-id="065f3-199">Dans la section fournisseurs d’identité SAML de hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="065f3-199">In hello SAML Identity Providers section, perform hello following steps:</span></span>
   
    <span data-ttu-id="065f3-200">![Fournisseurs d’identité SAML](./media/active-directory-saas-workday-tutorial/IC7829271.png "Fournisseurs d’identité SAML")</span><span class="sxs-lookup"><span data-stu-id="065f3-200">![SAML Identity Providers](./media/active-directory-saas-workday-tutorial/IC7829271.png "SAML Identity Providers")</span></span>
   
    <span data-ttu-id="065f3-201">a.</span><span class="sxs-lookup"><span data-stu-id="065f3-201">a.</span></span> <span data-ttu-id="065f3-202">Dans la zone de texte Nom de fournisseur d’identité hello, tapez un nom de fournisseur (par exemple : *SPInitiatedSSO*).</span><span class="sxs-lookup"><span data-stu-id="065f3-202">In hello Identity Provider Name textbox, type a provider name (for example: *SPInitiatedSSO*).</span></span>
   
    <span data-ttu-id="065f3-203">b.</span><span class="sxs-lookup"><span data-stu-id="065f3-203">b.</span></span> <span data-ttu-id="065f3-204">Bonjour portail Azure, sur hello **configurer l’authentification** fenêtre, hello de copie **ID d’entité SAML** valeur, puis collez-le dans hello **émetteur** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="065f3-204">In hello Azure portal, on hello **Configure sign-on** window, copy hello **SAML Entity ID** value, and then paste it into hello **Issuer** textbox.</span></span>
   
    <span data-ttu-id="065f3-205">c.</span><span class="sxs-lookup"><span data-stu-id="065f3-205">c.</span></span> <span data-ttu-id="065f3-206">Sélectionnez **Enable Workday Initiated Logout**.</span><span class="sxs-lookup"><span data-stu-id="065f3-206">Select **Enable Workday Initiated Logout**.</span></span>
   
    <span data-ttu-id="065f3-207">d.</span><span class="sxs-lookup"><span data-stu-id="065f3-207">d.</span></span> <span data-ttu-id="065f3-208">Bonjour portail Azure, sur hello **configurer l’authentification** fenêtre, hello de copie **URL de déconnexion** valeur, puis collez-le dans hello **URL de demande de déconnexion** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="065f3-208">In hello Azure portal, on hello **Configure sign-on** window, copy hello **Sign-Out URL** value, and then paste it into hello **Logout Request URL** textbox.</span></span>

    <span data-ttu-id="065f3-209">e.</span><span class="sxs-lookup"><span data-stu-id="065f3-209">e.</span></span> <span data-ttu-id="065f3-210">Cliquez sur **Certificat de clé publique du fournisseur d’identité**, puis sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="065f3-210">Click **Identity Provider Public Key Certificate**, and then click **Create**.</span></span> 

    <span data-ttu-id="065f3-211">![Créer](./media/active-directory-saas-workday-tutorial/IC782928.png "créer")</span><span class="sxs-lookup"><span data-stu-id="065f3-211">![Create](./media/active-directory-saas-workday-tutorial/IC782928.png "Create")</span></span>

    <span data-ttu-id="065f3-212">f.</span><span class="sxs-lookup"><span data-stu-id="065f3-212">f.</span></span> <span data-ttu-id="065f3-213">Cliquez sur **Créer la clé publique x509**.</span><span class="sxs-lookup"><span data-stu-id="065f3-213">Click **Create x509 Public Key**.</span></span> 

    <span data-ttu-id="065f3-214">![Créer](./media/active-directory-saas-workday-tutorial/IC782929.png "créer")</span><span class="sxs-lookup"><span data-stu-id="065f3-214">![Create](./media/active-directory-saas-workday-tutorial/IC782929.png "Create")</span></span>


14. <span data-ttu-id="065f3-215">Bonjour **x509 d’afficher la clé publique** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="065f3-215">In hello **View x509 Public Key** section, perform hello following steps:</span></span> 
   
    <span data-ttu-id="065f3-216">![Afficher la clé publique x509](./media/active-directory-saas-workday-tutorial/IC782930.png "Afficher la clé publique x509")</span><span class="sxs-lookup"><span data-stu-id="065f3-216">![View x509 Public Key](./media/active-directory-saas-workday-tutorial/IC782930.png "View x509 Public Key")</span></span> 
   
    <span data-ttu-id="065f3-217">a.</span><span class="sxs-lookup"><span data-stu-id="065f3-217">a.</span></span> <span data-ttu-id="065f3-218">Bonjour **nom** zone de texte, tapez un nom pour votre certificat (par exemple : *EPI\_SP*).</span><span class="sxs-lookup"><span data-stu-id="065f3-218">In hello **Name** textbox, type a name for your certificate (for example: *PPE\_SP*).</span></span>
   
    <span data-ttu-id="065f3-219">b.</span><span class="sxs-lookup"><span data-stu-id="065f3-219">b.</span></span> <span data-ttu-id="065f3-220">Bonjour **valide à partir du** zone de texte, hello type valide à partir de la valeur de l’attribut de votre certificat.</span><span class="sxs-lookup"><span data-stu-id="065f3-220">In hello **Valid From** textbox, type hello valid from attribute value of your certificate.</span></span>
   
    <span data-ttu-id="065f3-221">c.</span><span class="sxs-lookup"><span data-stu-id="065f3-221">c.</span></span>  <span data-ttu-id="065f3-222">Bonjour **valide à** zone de texte, type hello valide tooattribute valeur de votre certificat.</span><span class="sxs-lookup"><span data-stu-id="065f3-222">In hello **Valid To** textbox, type hello valid tooattribute value of your certificate.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="065f3-223">Vous pouvez obtenir hello valide à partir de la date et hello toodate valide du certificat de hello téléchargé en double-cliquant dessus.</span><span class="sxs-lookup"><span data-stu-id="065f3-223">You can get hello valid from date and hello valid toodate from hello downloaded certificate by double-clicking it.</span></span>  <span data-ttu-id="065f3-224">dates de Hello sont répertoriés sous hello **détails** onglet.</span><span class="sxs-lookup"><span data-stu-id="065f3-224">hello dates are listed under hello **Details** tab.</span></span>
    > 
    >
   
    <span data-ttu-id="065f3-225">d.</span><span class="sxs-lookup"><span data-stu-id="065f3-225">d.</span></span>  <span data-ttu-id="065f3-226">Ouvrez votre certificat codé en base 64 dans le bloc-notes, puis hello copie contenu de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="065f3-226">Open your base-64 encoded certificate in notepad, and then copy hello content of it.</span></span>
   
    <span data-ttu-id="065f3-227">e.</span><span class="sxs-lookup"><span data-stu-id="065f3-227">e.</span></span>  <span data-ttu-id="065f3-228">Bonjour **certificat** zone de texte, collez le contenu hello du Presse-papiers.</span><span class="sxs-lookup"><span data-stu-id="065f3-228">In hello **Certificate** textbox, paste hello content of your clipboard.</span></span>
   
    <span data-ttu-id="065f3-229">f.</span><span class="sxs-lookup"><span data-stu-id="065f3-229">f.</span></span>  <span data-ttu-id="065f3-230">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="065f3-230">Click **OK**.</span></span>

15. <span data-ttu-id="065f3-231">Effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="065f3-231">Perform hello following steps:</span></span> 
   
    <span data-ttu-id="065f3-232">![Configuration SSO](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "Configuration SSO")</span><span class="sxs-lookup"><span data-stu-id="065f3-232">![SSO configuration](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "SSO configuration")</span></span>
   
    <span data-ttu-id="065f3-233">a.</span><span class="sxs-lookup"><span data-stu-id="065f3-233">a.</span></span>  <span data-ttu-id="065f3-234">Activer hello **x509 paire de clés privée**.</span><span class="sxs-lookup"><span data-stu-id="065f3-234">Enable hello **x509 Private Key Pair**.</span></span>
   
    <span data-ttu-id="065f3-235">b.</span><span class="sxs-lookup"><span data-stu-id="065f3-235">b.</span></span>  <span data-ttu-id="065f3-236">Bonjour **Service Provider ID** zone de texte, type **http://www.workday.com**.</span><span class="sxs-lookup"><span data-stu-id="065f3-236">In hello **Service Provider ID** textbox, type **http://www.workday.com**.</span></span>
   
    <span data-ttu-id="065f3-237">c.</span><span class="sxs-lookup"><span data-stu-id="065f3-237">c.</span></span>  <span data-ttu-id="065f3-238">Sélectionnez **Enable SP Initiated SAML Authentication**.</span><span class="sxs-lookup"><span data-stu-id="065f3-238">Select **Enable SP Initiated SAML Authentication**.</span></span>
   
    <span data-ttu-id="065f3-239">d.</span><span class="sxs-lookup"><span data-stu-id="065f3-239">d.</span></span>  <span data-ttu-id="065f3-240">Bonjour portail Azure, sur hello **configurer l’authentification** fenêtre, hello de copie **SAML Sign-On URL du Service unique** valeur, puis collez-le dans hello **IdP SSO Service URL** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="065f3-240">In hello Azure portal, on hello **Configure sign-on** window, copy hello **SAML Single Sign-On Service URL** value, and then paste it into hello **IdP SSO Service URL** textbox.</span></span>
   
    <span data-ttu-id="065f3-241">e.</span><span class="sxs-lookup"><span data-stu-id="065f3-241">e.</span></span> <span data-ttu-id="065f3-242">Sélectionnez **Ne pas compresser la demande d’authentification initiée par le fournisseur de services**.</span><span class="sxs-lookup"><span data-stu-id="065f3-242">Select **Do Not Deflate SP-initiated Authentication Request**.</span></span>
   
    <span data-ttu-id="065f3-243">f.</span><span class="sxs-lookup"><span data-stu-id="065f3-243">f.</span></span> <span data-ttu-id="065f3-244">Comme **Méthode de signature de la demande d’authentification**, sélectionnez **SHA256**.</span><span class="sxs-lookup"><span data-stu-id="065f3-244">As **Authentication Request Signature Method**, select **SHA256**.</span></span> 
   
    <span data-ttu-id="065f3-245">![Méthode de signature de demande la d’authentification](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "Méthode de signature de la demande d’authentification")</span><span class="sxs-lookup"><span data-stu-id="065f3-245">![Authentication Request Signature Method](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "Authentication Request Signature Method")</span></span> 
   
    <span data-ttu-id="065f3-246">g.</span><span class="sxs-lookup"><span data-stu-id="065f3-246">g.</span></span> <span data-ttu-id="065f3-247">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="065f3-247">Click **OK**.</span></span> 
   
    <span data-ttu-id="065f3-248">![OK](./media/active-directory-saas-workday-tutorial/IC782933.png "OK")
<CE></span><span class="sxs-lookup"><span data-stu-id="065f3-248">![OK](./media/active-directory-saas-workday-tutorial/IC782933.png "OK")
<CE></span></span>

> [!TIP]
> <span data-ttu-id="065f3-249">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="065f3-249">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="065f3-250">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="065f3-250">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="065f3-251">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="065f3-251">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="065f3-252">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="065f3-252">Creating an Azure AD test user</span></span>
<span data-ttu-id="065f3-253">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="065f3-253">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="065f3-255">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="065f3-255">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="065f3-256">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="065f3-256">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="065f3-258">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="065f3-258">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="065f3-260">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="065f3-260">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="065f3-262">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="065f3-262">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="065f3-264">a.</span><span class="sxs-lookup"><span data-stu-id="065f3-264">a.</span></span> <span data-ttu-id="065f3-265">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="065f3-265">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="065f3-266">b.</span><span class="sxs-lookup"><span data-stu-id="065f3-266">b.</span></span> <span data-ttu-id="065f3-267">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="065f3-267">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="065f3-268">c.</span><span class="sxs-lookup"><span data-stu-id="065f3-268">c.</span></span> <span data-ttu-id="065f3-269">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="065f3-269">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="065f3-270">d.</span><span class="sxs-lookup"><span data-stu-id="065f3-270">d.</span></span> <span data-ttu-id="065f3-271">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="065f3-271">Click **Create**.</span></span>
 
### <a name="creating-a-workday-test-user"></a><span data-ttu-id="065f3-272">Création d’un utilisateur de test Workday</span><span class="sxs-lookup"><span data-stu-id="065f3-272">Creating a Workday test user</span></span>

<span data-ttu-id="065f3-273">tooget un utilisateur de test dans Workday, vous devez toocontact hello [équipe de support Workday Client](https://www.workday.com/en-us/partners-services/services/support.html).</span><span class="sxs-lookup"><span data-stu-id="065f3-273">tooget a test user provisioned into Workday, you need toocontact hello [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html).</span></span>
<span data-ttu-id="065f3-274">Hello [équipe de support Workday Client](https://www.workday.com/en-us/partners-services/services/support.html) crée un utilisateur de hello pour vous.</span><span class="sxs-lookup"><span data-stu-id="065f3-274">hello [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) creates hello user for you.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="065f3-275">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="065f3-275">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="065f3-276">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooWorkday.</span><span class="sxs-lookup"><span data-stu-id="065f3-276">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkday.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="065f3-278">**tooassign Britta Simon tooWorkday, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="065f3-278">**tooassign Britta Simon tooWorkday, perform hello following steps:**</span></span>

1. <span data-ttu-id="065f3-279">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="065f3-279">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="065f3-281">Dans la liste des applications hello, sélectionnez **Workday**.</span><span class="sxs-lookup"><span data-stu-id="065f3-281">In hello applications list, select **Workday**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-workday-tutorial/tutorial_workday_app.png) 

3. <span data-ttu-id="065f3-283">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="065f3-283">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="065f3-285">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="065f3-285">Click **Add** button.</span></span> <span data-ttu-id="065f3-286">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="065f3-286">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="065f3-288">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="065f3-288">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="065f3-289">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="065f3-289">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="065f3-290">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="065f3-290">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="065f3-291">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="065f3-291">Testing single sign-on</span></span>

<span data-ttu-id="065f3-292">Si vous souhaitez tootest vos paramètres d’authentification unique, ouvrez hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="065f3-292">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="065f3-293">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="065f3-293">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="065f3-294">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="065f3-294">Additional resources</span></span>

* [<span data-ttu-id="065f3-295">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="065f3-295">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="065f3-296">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="065f3-296">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="065f3-297">Configurer l’approvisionnement de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="065f3-297">Configure User Provisioning</span></span>](active-directory-saas-workday-inbound-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workday-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workday-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workday-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workday-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workday-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workday-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workday-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workday-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workday-tutorial/tutorial_general_203.png

