---
title: "Didacticiel : Intégration d’Azure Active Directory avec @Task| Documents Microsoft"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et @Task."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 0840763622086a02a27cfafff3b741bc66cec498
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-task"></a><span data-ttu-id="7247a-103">Didacticiel : Intégration d'Azure Active Directory à @Task</span><span class="sxs-lookup"><span data-stu-id="7247a-103">Tutorial: Azure Active Directory integration with @Task</span></span>
<span data-ttu-id="7247a-104">objectif Hello de ce didacticiel est tooshow vous comment toointegrate @Task avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7247a-104">hello objective of this tutorial is tooshow you how toointegrate @Task with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="7247a-105">Intégration @Task avec Azure AD vous fournit hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="7247a-105">Integrating @Task with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="7247a-106">Vous pouvez contrôler dans Azure AD qui a accèstoo@Task</span><span class="sxs-lookup"><span data-stu-id="7247a-106">You can control in Azure AD who has access too@Task</span></span>
* <span data-ttu-id="7247a-107">Vous pouvez activer vos utilisateurs tooautomatically obtenir connecté too@Task (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="7247a-107">You can enable your users tooautomatically get signed-on too@Task (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="7247a-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure classic</span><span class="sxs-lookup"><span data-stu-id="7247a-108">You can manage your accounts in one central location - hello Azure classic Portal</span></span>

<span data-ttu-id="7247a-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7247a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7247a-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7247a-110">Prerequisites</span></span>
<span data-ttu-id="7247a-111">intégration tooconfigure Azure AD avec @Task, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="7247a-111">tooconfigure Azure AD integration with @Task, you need hello following items:</span></span>

* <span data-ttu-id="7247a-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="7247a-112">An Azure AD subscription</span></span>
* <span data-ttu-id="7247a-113">Un abonnement @Task pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="7247a-113">An @Task single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7247a-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="7247a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="7247a-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="7247a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="7247a-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="7247a-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="7247a-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7247a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="7247a-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="7247a-118">Scenario Description</span></span>
<span data-ttu-id="7247a-119">objectif Hello de ce didacticiel est tooenable vous tootest Azure AD l’authentification unique dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="7247a-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="7247a-120">scénario Hello décrite dans ce didacticiel se compose de trois blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="7247a-120">hello scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="7247a-121">Ajout de @Task à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="7247a-121">Adding @Task from hello gallery</span></span> 
2. <span data-ttu-id="7247a-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7247a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-task-from-hello-gallery"></a><span data-ttu-id="7247a-123">Ajout de @Task à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="7247a-123">Adding @Task from hello gallery</span></span>
<span data-ttu-id="7247a-124">intégration de hello tooconfigure de @Task dans Azure AD, vous devez tooadd @Task à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="7247a-124">tooconfigure hello integration of @Task into Azure AD, you need tooadd @Task from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7247a-125">**tooadd @Task à partir de la galerie hello, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7247a-125">**tooadd @Task from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7247a-126">Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7247a-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1] 
2. <span data-ttu-id="7247a-128">À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="7247a-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="7247a-129">vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.</span><span class="sxs-lookup"><span data-stu-id="7247a-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Applications][2] 
4. <span data-ttu-id="7247a-131">Cliquez sur **ajouter** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="7247a-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Applications][3] 
5. <span data-ttu-id="7247a-133">Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application à partir de la galerie de hello**.</span><span class="sxs-lookup"><span data-stu-id="7247a-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Applications][4] 
6. <span data-ttu-id="7247a-135">Dans la zone de recherche de hello, tapez  **@Task** .</span><span class="sxs-lookup"><span data-stu-id="7247a-135">In hello search box, type **@Task**.</span></span>
   
    ![Applications][5] 
7. <span data-ttu-id="7247a-137">Dans le volet de résultats hello, sélectionnez  **@Task** , puis cliquez sur **Complete** application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="7247a-137">In hello results pane, select **@Task**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Applications][30] 

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7247a-139">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7247a-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7247a-140">objectif de cette section Hello est tooshow vous comment tooconfigure et test Azure AD unique authentification avec @Task basé sur un utilisateur de test appelé « Brian Simon ».</span><span class="sxs-lookup"><span data-stu-id="7247a-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with @Task based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7247a-141">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello @Task utilisateur tooan dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7247a-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in @Task tooan user in Azure AD is.</span></span> <span data-ttu-id="7247a-142">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans @Task doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="7247a-142">In other words, a link relationship between an Azure AD user and hello related user in @Task needs toobe established.</span></span>   
<span data-ttu-id="7247a-143">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans @Task.</span><span class="sxs-lookup"><span data-stu-id="7247a-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in @Task.</span></span>

<span data-ttu-id="7247a-144">tooconfigure et test Azure AD sur l’authentification unique avec @Task, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="7247a-144">tooconfigure and test Azure AD single sign-on with @Task, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7247a-145">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="7247a-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7247a-146">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7247a-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7247a-147">**[Création d’un @Tasktest utilisateur](#creating-a-halogen-software-test-user)**  -toohave un équivalent de Britta Simon dans @Taskthat est de sa représentation sous forme de toohello lié Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7247a-147">**[Creating a @Tasktest user](#creating-a-halogen-software-test-user)** - toohave a counterpart of Britta Simon in @Taskthat is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="7247a-148">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="7247a-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7247a-149">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="7247a-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7247a-150">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7247a-150">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="7247a-151">Hello cette section vise tooenable Azure AD l’authentification unique sur Bonjour portail Azure classic et tooconfigure l’authentification unique dans votre @Task application.</span><span class="sxs-lookup"><span data-stu-id="7247a-151">hello objective of this section is tooenable Azure AD single sign-on in hello Azure classic portal and tooconfigure single sign-on in your @Task application.</span></span>

<span data-ttu-id="7247a-152">**tooconfigure Azure AD l’authentification unique avec @Task, effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7247a-152">**tooconfigure Azure AD single sign-on with @Task, perform hello following steps:**</span></span>

1. <span data-ttu-id="7247a-153">Bonjour portail Azure classic sur hello  **@Task**  page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello **configurer l’authentification unique sur**  boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="7247a-153">In hello Azure classic portal, on hello **@Task** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configurer l’authentification unique][6] 
2. <span data-ttu-id="7247a-155">Sur hello **Comment voulez-vous telles que les utilisateurs toosign sur too@Task**  page, sélectionnez **Azure AD Single Sign-On**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="7247a-155">On hello **How would you like users toosign on too@Task** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Authentification unique Azure AD][7] 
3. <span data-ttu-id="7247a-157">Sur hello **configurer les paramètres de l’application** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="7247a-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>
   
    ![Configurer les paramètres d’application][8] 
   
     <span data-ttu-id="7247a-159">a.</span><span class="sxs-lookup"><span data-stu-id="7247a-159">a.</span></span> <span data-ttu-id="7247a-160">Bonjour **URL de connexion** zone de texte, tapez l’URL hello utilisée par vos utilisateurs sur toosign tooyour @Task application (par exemple :*https://<Tenant name>.attask-ondemand.com*).</span><span class="sxs-lookup"><span data-stu-id="7247a-160">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour @Task application (e.g.:*https://<Tenant name>.attask-ondemand.com*).</span></span>
   
     <span data-ttu-id="7247a-161">b.</span><span class="sxs-lookup"><span data-stu-id="7247a-161">b.</span></span> <span data-ttu-id="7247a-162">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="7247a-162">Click **Next**.</span></span>
4. <span data-ttu-id="7247a-163">Sur hello **configurer l’authentification unique à @Task**  , cliquez sur **télécharger des métadonnées**, enregistrez le fichier de métadonnées hello localement sur votre ordinateur, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="7247a-163">On hello **Configure single sign-on at @Task** page, click **Download metadata**, save hello metadata file locally on your computer, and then click **Next**.</span></span>
   
    ![Qu’est-ce qu’Azure AD Connect ?][9] 
5. <span data-ttu-id="7247a-165">Authentification tooyour @Task site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="7247a-165">Sign-on tooyour @Task company site as administrator.</span></span>
6. <span data-ttu-id="7247a-166">Accédez trop**l’authentification unique sur la Configuration**.</span><span class="sxs-lookup"><span data-stu-id="7247a-166">Go too**Single Sign On Configuration**.</span></span>
7. <span data-ttu-id="7247a-167">Sur hello **Single Sign-On** boîte de dialogue, effectuer hello comme suit</span><span class="sxs-lookup"><span data-stu-id="7247a-167">On hello **Single Sign-On** dialog, perform hello following steps</span></span>
   
    ![Configurer l’authentification unique][23]
   
    <span data-ttu-id="7247a-169">a.</span><span class="sxs-lookup"><span data-stu-id="7247a-169">a.</span></span> <span data-ttu-id="7247a-170">Comme **Type**, sélectionnez **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="7247a-170">As **Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="7247a-171">b.</span><span class="sxs-lookup"><span data-stu-id="7247a-171">b.</span></span> <span data-ttu-id="7247a-172">Sélectionnez **///ID fournisseur de services**.</span><span class="sxs-lookup"><span data-stu-id="7247a-172">Select **Service Provider ID**.</span></span>
   
    <span data-ttu-id="7247a-173">c.</span><span class="sxs-lookup"><span data-stu-id="7247a-173">c.</span></span> <span data-ttu-id="7247a-174">Sur hello portail Azure classic, copiez hello **URL de connexion distante**, puis collez-la dans hello **URL du portail de compte de connexion** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="7247a-174">On hello Azure classic portal, copy hello **Remote Login URL**, and then paste it into hello **Login Portal URL** textbox.</span></span>
   
    <span data-ttu-id="7247a-175">d.</span><span class="sxs-lookup"><span data-stu-id="7247a-175">d.</span></span> <span data-ttu-id="7247a-176">Sur hello portail Azure classic, copiez hello **URL de Service de déconnexion unique**, puis collez-la dans hello **URL de déconnexion** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="7247a-176">On hello Azure classic portal, copy hello **Single Sign-Out Service URL**, and then paste it into hello **Sign-Out URL** textbox.</span></span>
   
    <span data-ttu-id="7247a-177">e.</span><span class="sxs-lookup"><span data-stu-id="7247a-177">e.</span></span> <span data-ttu-id="7247a-178">Sur hello portail Azure classic, copiez hello **URL de modification du mot de passe**, puis collez-la dans hello **URL de modification du mot de passe** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="7247a-178">On hello Azure classic portal, copy hello **Change Password URL**, and then paste it into hello **Change Password URL** textbox.</span></span>
   
    <span data-ttu-id="7247a-179">f.</span><span class="sxs-lookup"><span data-stu-id="7247a-179">f.</span></span> <span data-ttu-id="7247a-180">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="7247a-180">Click **Save**.</span></span>
8. <span data-ttu-id="7247a-181">Sur le portail Azure classic de hello, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="7247a-181">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![Qu’est-ce qu’Azure AD Connect ?][10]
9. <span data-ttu-id="7247a-183">Sur hello **Single sign-on confirmation** , cliquez sur **Complete**.</span><span class="sxs-lookup"><span data-stu-id="7247a-183">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Qu’est-ce qu’Azure AD Connect ?][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7247a-185">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="7247a-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="7247a-186">objectif Hello de cette section est toocreate un utilisateur de test dans le portail Azure classic appelé Britta Simon de hello.</span><span class="sxs-lookup"><span data-stu-id="7247a-186">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>  

![Créer un utilisateur Azure AD][20]

<span data-ttu-id="7247a-188">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7247a-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7247a-189">Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7247a-189">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_02.png) 
2. <span data-ttu-id="7247a-191">À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="7247a-191">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="7247a-192">liste de hello toodisplay d’utilisateurs, dans le menu hello haut de hello, cliquez sur **utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="7247a-192">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="7247a-194">tooopen hello **ajouter un utilisateur** boîte de dialogue, dans la barre d’outils de hello en bas de hello, cliquez sur **ajouter un utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="7247a-194">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="7247a-196">Sur hello **faites-nous part de cet utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="7247a-196">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span> 
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="7247a-198">a.</span><span class="sxs-lookup"><span data-stu-id="7247a-198">a.</span></span> <span data-ttu-id="7247a-199">Dans Type d’utilisateur, sélectionnez Nouvel utilisateur dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="7247a-199">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="7247a-200">b.</span><span class="sxs-lookup"><span data-stu-id="7247a-200">b.</span></span> <span data-ttu-id="7247a-201">Bonjour, nom d’utilisateur **zone de texte**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7247a-201">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="7247a-202">c.</span><span class="sxs-lookup"><span data-stu-id="7247a-202">c.</span></span> <span data-ttu-id="7247a-203">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="7247a-203">Click **Next**.</span></span>
6. <span data-ttu-id="7247a-204">Sur hello **profil utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="7247a-204">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="7247a-206">a.</span><span class="sxs-lookup"><span data-stu-id="7247a-206">a.</span></span> <span data-ttu-id="7247a-207">Bonjour **prénom** zone de texte, type **Brian**.</span><span class="sxs-lookup"><span data-stu-id="7247a-207">In hello **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="7247a-208">b.</span><span class="sxs-lookup"><span data-stu-id="7247a-208">b.</span></span> <span data-ttu-id="7247a-209">Bonjour **nom** zone de texte, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="7247a-209">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="7247a-210">c.</span><span class="sxs-lookup"><span data-stu-id="7247a-210">c.</span></span> <span data-ttu-id="7247a-211">Bonjour **nom d’affichage** zone de texte, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="7247a-211">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="7247a-212">d.</span><span class="sxs-lookup"><span data-stu-id="7247a-212">d.</span></span> <span data-ttu-id="7247a-213">Bonjour **rôle** liste, sélectionnez **utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="7247a-213">In hello **Role** list, select **User**.</span></span>

    <span data-ttu-id="7247a-214">e.</span><span class="sxs-lookup"><span data-stu-id="7247a-214">e.</span></span> <span data-ttu-id="7247a-215">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="7247a-215">Click **Next**.</span></span>

7. <span data-ttu-id="7247a-216">Sur hello **mot de passe temporaire Get** page de boîte de dialogue, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="7247a-216">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="7247a-218">Sur hello **mot de passe temporaire Get** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="7247a-218">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="7247a-220">a.</span><span class="sxs-lookup"><span data-stu-id="7247a-220">a.</span></span> <span data-ttu-id="7247a-221">Notez la valeur hello hello **nouveau mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="7247a-221">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="7247a-222">b.</span><span class="sxs-lookup"><span data-stu-id="7247a-222">b.</span></span> <span data-ttu-id="7247a-223">Cliquez sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="7247a-223">Click **Complete**.</span></span>   

### <a name="creating-an-task-test-user"></a><span data-ttu-id="7247a-224">Création d’un utilisateur de test @Task</span><span class="sxs-lookup"><span data-stu-id="7247a-224">Creating an @Task test user</span></span>
<span data-ttu-id="7247a-225">objectif Hello de cette section est toocreate un utilisateur nommé Britta Simon dans @Task.</span><span class="sxs-lookup"><span data-stu-id="7247a-225">hello objective of this section is toocreate a user called Britta Simon in @Task.</span></span>

<span data-ttu-id="7247a-226">**toocreate un utilisateur nommé Britta Simon dans @Task, effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7247a-226">**toocreate a user called Britta Simon in @Task, perform hello following steps:**</span></span>

1. <span data-ttu-id="7247a-227">Ouverture de session tooyour @Task site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="7247a-227">Sign on tooyour @Task company site as administrator.</span></span>
2. <span data-ttu-id="7247a-228">Dans le menu hello haut de hello, cliquez sur **personnes**.</span><span class="sxs-lookup"><span data-stu-id="7247a-228">In hello menu on hello top, click **People**.</span></span>
3. <span data-ttu-id="7247a-229">Cliquez sur **New Person**.</span><span class="sxs-lookup"><span data-stu-id="7247a-229">Click **New Person**.</span></span> 
4. <span data-ttu-id="7247a-230">Dans la boîte de dialogue nouvelle personne hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="7247a-230">On hello New Person dialog, perform hello following steps:</span></span>
   
    ![Création d’un utilisateur de test @Task][21] 
   
    <span data-ttu-id="7247a-232">a.</span><span class="sxs-lookup"><span data-stu-id="7247a-232">a.</span></span> <span data-ttu-id="7247a-233">Bonjour **prénom** zone de texte, tapez « Brian ».</span><span class="sxs-lookup"><span data-stu-id="7247a-233">In hello **First Name** textbox, type "Britta".</span></span>
   
    <span data-ttu-id="7247a-234">b.</span><span class="sxs-lookup"><span data-stu-id="7247a-234">b.</span></span> <span data-ttu-id="7247a-235">Bonjour **nom** zone de texte, tapez « Simon ».</span><span class="sxs-lookup"><span data-stu-id="7247a-235">In hello **Last Name** textbox, type "Simon".</span></span>
   
    <span data-ttu-id="7247a-236">c.</span><span class="sxs-lookup"><span data-stu-id="7247a-236">c.</span></span> <span data-ttu-id="7247a-237">Bonjour **adresse de messagerie** zone de texte, tapez l’adresse de messagerie Britta Simon dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7247a-237">In hello **Email Address** textbox, type Britta Simon's email address in Azure Active Directory.</span></span>
   
    <span data-ttu-id="7247a-238">d.</span><span class="sxs-lookup"><span data-stu-id="7247a-238">d.</span></span> <span data-ttu-id="7247a-239">Cliquez sur **Add Person**.</span><span class="sxs-lookup"><span data-stu-id="7247a-239">Click **Add Person**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7247a-240">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="7247a-240">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="7247a-241">objectif Hello de cette section est tooenabling toouse Britta Simon Azure l’authentification unique en accordant l’accès too@Task.</span><span class="sxs-lookup"><span data-stu-id="7247a-241">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access too@Task.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="7247a-243">**tooassign Britta Simon too@Task, effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7247a-243">**tooassign Britta Simon too@Task, perform hello following steps:**</span></span>

1. <span data-ttu-id="7247a-244">Dans hello Azure portail classique, la vue applications hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.</span><span class="sxs-lookup"><span data-stu-id="7247a-244">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Affecter des utilisateurs][201] 
2. <span data-ttu-id="7247a-246">Dans la liste des applications hello, sélectionnez  **@Task** .</span><span class="sxs-lookup"><span data-stu-id="7247a-246">In hello applications list, select **@Task**.</span></span>
   
    ![Affecter des utilisateurs][202] 
3. <span data-ttu-id="7247a-248">Dans le menu hello haut de hello, cliquez sur **utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="7247a-248">In hello menu on hello top, click **Users**.</span></span>
   
    ![Affecter des utilisateurs][203] 
4. <span data-ttu-id="7247a-250">Dans la liste des utilisateurs hello, sélectionnez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="7247a-250">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="7247a-251">Dans la barre d’outils de hello en bas de hello, cliquez sur **affecter**.</span><span class="sxs-lookup"><span data-stu-id="7247a-251">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Affecter des utilisateurs][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="7247a-253">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="7247a-253">Testing Single Sign-On</span></span>
<span data-ttu-id="7247a-254">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="7247a-254">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="7247a-255">Lorsque vous cliquez sur hello @Task vignette dans hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour @Task application.</span><span class="sxs-lookup"><span data-stu-id="7247a-255">When you click hello @Task tile in hello Access Panel, you should get automatically signed-on tooyour @Task application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7247a-256">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="7247a-256">Additional Resources</span></span>
* [<span data-ttu-id="7247a-257">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7247a-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7247a-258">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="7247a-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-attask-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-attask-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-attask-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-attask-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_01.png
[30]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_02.png


[6]: ./media/active-directory-saas-attask-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_03.png
[8]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_04.png
[9]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_05.png
[10]: ./media/active-directory-saas-attask-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-attask-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-attask-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_08.png


[23]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_06.png

[200]: ./media/active-directory-saas-attask-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-attask-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_09.png
[203]: ./media/active-directory-saas-attask-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-attask-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-attask-tutorial/tutorial_general_205.png






