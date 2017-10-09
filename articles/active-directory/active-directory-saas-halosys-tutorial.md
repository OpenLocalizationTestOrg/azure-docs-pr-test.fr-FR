---
title: "Didacticiel : intégration d’Azure Active Directory à Halosys | Microsoft Docs"
description: "Découvrez comment toouse Halosys avec Azure Active Directory tooenable single sign-on, l’approvisionnement automatisé et bien plus encore !"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 42a0eb7c-5cb7-44a9-b00b-b0e7df4b63e8
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 18043ed1b6f7ab45c59cfd36252bef1621618e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halosys"></a><span data-ttu-id="eb0ed-103">Didacticiel : intégration d’Azure Active Directory à Halosys</span><span class="sxs-lookup"><span data-stu-id="eb0ed-103">Tutorial: Azure Active Directory integration with Halosys</span></span>

<span data-ttu-id="eb0ed-104">Dans ce didacticiel, vous apprendrez comment toointegrate Halosys avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="eb0ed-104">In this tutorial, you learn how toointegrate Halosys with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="eb0ed-105">Intégration Halosys à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="eb0ed-105">Integrating Halosys with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="eb0ed-106">Vous pouvez contrôler dans Azure AD qui a accès tooHalosys</span><span class="sxs-lookup"><span data-stu-id="eb0ed-106">You can control in Azure AD who has access tooHalosys</span></span>
- <span data-ttu-id="eb0ed-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooHalosys (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb0ed-107">You can enable your users tooautomatically get signed-on tooHalosys (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="eb0ed-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure classic</span><span class="sxs-lookup"><span data-stu-id="eb0ed-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="eb0ed-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="eb0ed-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eb0ed-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="eb0ed-110">Prerequisites</span></span>

<span data-ttu-id="eb0ed-111">tooconfigure intégration d’Azure AD avec Halosys, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="eb0ed-111">tooconfigure Azure AD integration with Halosys, you need hello following items:</span></span>

- <span data-ttu-id="eb0ed-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb0ed-112">An Azure AD subscription</span></span>
- <span data-ttu-id="eb0ed-113">Un abonnement Halosys pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="eb0ed-113">A Halosys single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="eb0ed-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="eb0ed-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="eb0ed-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="eb0ed-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="eb0ed-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eb0ed-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="eb0ed-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="eb0ed-118">Scenario description</span></span>
<span data-ttu-id="eb0ed-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="eb0ed-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="eb0ed-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="eb0ed-121">Ajout de Halosys à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="eb0ed-121">Adding Halosys from hello gallery</span></span>
2. <span data-ttu-id="eb0ed-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb0ed-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-halosys-from-hello-gallery"></a><span data-ttu-id="eb0ed-123">Ajout de Halosys à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="eb0ed-123">Adding Halosys from hello gallery</span></span>
<span data-ttu-id="eb0ed-124">intégration de hello tooconfigure de Halosys dans Azure AD, vous devez tooadd Halosys à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-124">tooconfigure hello integration of Halosys into Azure AD, you need tooadd Halosys from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="eb0ed-125">**tooadd Halosys à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="eb0ed-125">**tooadd Halosys from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb0ed-126">Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]
2. <span data-ttu-id="eb0ed-128">À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="eb0ed-129">vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Applications][2]

4. <span data-ttu-id="eb0ed-131">Cliquez sur **ajouter** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-131">Click **Add** at hello bottom of hello page.</span></span>

    ![Applications][3]

5. <span data-ttu-id="eb0ed-133">Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application à partir de la galerie de hello**.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>

    ![Applications][4]

6. <span data-ttu-id="eb0ed-135">Dans la zone de recherche de hello, tapez **Halosys**.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-135">In hello search box, type **Halosys**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_01.png)
    
7. <span data-ttu-id="eb0ed-137">Dans le volet de résultats hello, sélectionnez **Halosys**, puis cliquez sur **Complete** application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-137">In hello results pane, select **Halosys**, and then click **Complete** tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_011.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="eb0ed-139">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb0ed-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="eb0ed-140">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Halosys avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="eb0ed-140">In this section, you configure and test Azure AD single sign-on with Halosys based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="eb0ed-141">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Halosys est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Halosys is tooa user in Azure AD.</span></span> <span data-ttu-id="eb0ed-142">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Halosys doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-142">In other words, a link relationship between an Azure AD user and hello related user in Halosys needs toobe established.</span></span>

<span data-ttu-id="eb0ed-143">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Halosys.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Halosys.</span></span>

<span data-ttu-id="eb0ed-144">tooconfigure et test Azure AD l’authentification unique avec Halosys, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="eb0ed-144">tooconfigure and test Azure AD single sign-on with Halosys, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="eb0ed-145">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="eb0ed-146">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="eb0ed-147">**[Création d’un utilisateur de test Halosys](#creating-a-halosys-test-user)**  -toohave de Britta Simon dans Halosys qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-147">**[Creating a Halosys test user](#creating-a-halosys-test-user)** - toohave a counterpart of Britta Simon in Halosys that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="eb0ed-148">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="eb0ed-149">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="eb0ed-150">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb0ed-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="eb0ed-151">Dans cette section, vous activez Azure AD l’authentification unique dans le portail classique de hello et configurez l’authentification unique dans votre application Halosys.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your Halosys application.</span></span>


<span data-ttu-id="eb0ed-152">**tooconfigure Azure AD single sign-on avec Halosys, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="eb0ed-152">**tooconfigure Azure AD single sign-on with Halosys, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb0ed-153">Dans le portail classique hello, sur hello **Halosys** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello **configurer l’authentification unique sur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-153">In hello classic portal, on hello **Halosys** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
     
    ![Configurer l’authentification unique][6] 

2. <span data-ttu-id="eb0ed-155">Sur hello **Comment souhaitez-vous toosign utilisateurs sur tooHalosys** page, sélectionnez **Azure AD Single Sign-On**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-155">On hello **How would you like users toosign on tooHalosys** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_03.png) 

3. <span data-ttu-id="eb0ed-157">Sur hello **configurer les paramètres de l’application** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="eb0ed-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_04.png) 

    <span data-ttu-id="eb0ed-159">a.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-159">a.</span></span> <span data-ttu-id="eb0ed-160">Bonjour **URL de connexion** zone de texte, tapez l’URL hello utilisée par votre application de Halosys tooyour toosign sur les utilisateurs à l’aide de hello modèle : `https://<company-name>.Halosys.com/client-api/api`.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-160">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour Halosys application using hello following pattern: `https://<company-name>.Halosys.com/client-api/api`.</span></span>

    <span data-ttu-id="eb0ed-161">b.In hello **URL d’identificateur** zone de texte, tapez l’URL hello Bonjour modèle : `https://<company-name>.Halosys.com`.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-161">b.In hello **Identifier URL** textbox, type hello URL in hello following pattern: `https://<company-name>.Halosys.com`.</span></span> 
         
4. <span data-ttu-id="eb0ed-162">Sur hello **configurer l’authentification unique sur Halosys** , cliquez sur **télécharger des métadonnées**, puis enregistrez le fichier hello sur votre ordinateur :</span><span class="sxs-lookup"><span data-stu-id="eb0ed-162">On hello **Configure single sign-on at Halosys** page, click **Download metadata**, and then save hello file on your computer:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_05.png)
   
5. <span data-ttu-id="eb0ed-164">tooget SSO configuré pour votre application, contactez l’équipe de support Halosys et leur fournir des éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="eb0ed-164">tooget SSO configured for your application, contact Halosys support team and provide them with hello following:</span></span>

    <span data-ttu-id="eb0ed-165">hello • téléchargé **fichier de métadonnées**</span><span class="sxs-lookup"><span data-stu-id="eb0ed-165">• hello downloaded **metadata file**</span></span>
    
    <span data-ttu-id="eb0ed-166">• hello **URL SSO SAML**</span><span class="sxs-lookup"><span data-stu-id="eb0ed-166">• hello **SAML SSO URL**</span></span>
    

6. <span data-ttu-id="eb0ed-167">Dans le portail classique hello, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-167">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Authentification unique Azure AD][10]

7. <span data-ttu-id="eb0ed-169">Sur hello **Single sign-on confirmation** , cliquez sur **Complete**.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-169">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Authentification unique Azure AD][11]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="eb0ed-171">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb0ed-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="eb0ed-172">Dans cette section, vous créez un utilisateur de test dans le portail classique de hello appelé Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-172">In this section, you create a test user in hello classic portal called Britta Simon.</span></span>


![Créer un utilisateur Azure AD][20]

<span data-ttu-id="eb0ed-174">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="eb0ed-174">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb0ed-175">Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-175">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="eb0ed-177">À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-177">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="eb0ed-178">liste de hello toodisplay d’utilisateurs, dans le menu hello haut de hello, cliquez sur **utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-178">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="eb0ed-180">tooopen hello **ajouter un utilisateur** boîte de dialogue, dans la barre d’outils de hello en bas de hello, cliquez sur **ajouter un utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-180">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="eb0ed-182">Sur hello **faites-nous part de cet utilisateur** boîte de dialogue de page, effectuer hello comme suit : ![création d’un utilisateur de test Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png)</span><span class="sxs-lookup"><span data-stu-id="eb0ed-182">On hello **Tell us about this user** dialog page, perform hello following steps:  ![Creating an Azure AD test user](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png)</span></span> 

    <span data-ttu-id="eb0ed-183">a.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-183">a.</span></span> <span data-ttu-id="eb0ed-184">Dans Type d’utilisateur, sélectionnez Nouvel utilisateur dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-184">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="eb0ed-185">b.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-185">b.</span></span> <span data-ttu-id="eb0ed-186">Bonjour, nom d’utilisateur **zone de texte**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-186">In hello User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="eb0ed-187">c.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-187">c.</span></span> <span data-ttu-id="eb0ed-188">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-188">Click **Next**.</span></span>

6.  <span data-ttu-id="eb0ed-189">Sur hello **profil utilisateur** boîte de dialogue de page, effectuer hello comme suit : ![création d’un utilisateur de test Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png)</span><span class="sxs-lookup"><span data-stu-id="eb0ed-189">On hello **User Profile** dialog page, perform hello following steps: ![Creating an Azure AD test user](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png)</span></span> 

    <span data-ttu-id="eb0ed-190">a.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-190">a.</span></span> <span data-ttu-id="eb0ed-191">Bonjour **prénom** zone de texte, type **Brian**.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-191">In hello **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="eb0ed-192">b.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-192">b.</span></span> <span data-ttu-id="eb0ed-193">Bonjour **nom** zone de texte, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-193">In hello **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="eb0ed-194">c.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-194">c.</span></span> <span data-ttu-id="eb0ed-195">Bonjour **nom d’affichage** zone de texte, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-195">In hello **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="eb0ed-196">d.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-196">d.</span></span> <span data-ttu-id="eb0ed-197">Bonjour **rôle** liste, sélectionnez **utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-197">In hello **Role** list, select **User**.</span></span>

    <span data-ttu-id="eb0ed-198">e.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-198">e.</span></span> <span data-ttu-id="eb0ed-199">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-199">Click **Next**.</span></span>

7. <span data-ttu-id="eb0ed-200">Sur hello **mot de passe temporaire Get** page de boîte de dialogue, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-200">On hello **Get temporary password** dialog page, click **create**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="eb0ed-202">Sur hello **mot de passe temporaire Get** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="eb0ed-202">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="eb0ed-204">a.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-204">a.</span></span> <span data-ttu-id="eb0ed-205">Notez la valeur hello hello **nouveau mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-205">Write down hello value of hello **New Password**.</span></span>

    <span data-ttu-id="eb0ed-206">b.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-206">b.</span></span> <span data-ttu-id="eb0ed-207">Cliquez sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-207">Click **Complete**.</span></span>   



### <a name="creating-a-halosys-test-user"></a><span data-ttu-id="eb0ed-208">Création d’un utilisateur de test Halosys</span><span class="sxs-lookup"><span data-stu-id="eb0ed-208">Creating a Halosys test user</span></span>

<span data-ttu-id="eb0ed-209">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Halosys.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-209">In this section, you create a user called Britta Simon in Halosys.</span></span> <span data-ttu-id="eb0ed-210">Collaborez avec Halosys prise en charge team tooadd hello utilisateurs dans la plateforme de Halosys hello.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-210">Please work with Halosys support team tooadd hello users in hello Halosys platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="eb0ed-211">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb0ed-211">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="eb0ed-212">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant tooHalosys de son accès.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-212">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooHalosys.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="eb0ed-214">**tooassign Britta Simon tooHalosys, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="eb0ed-214">**tooassign Britta Simon tooHalosys, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb0ed-215">Sur le portail classique hello, cliquez sur la vue applications hello tooopen, dans la vue active de hello, **Applications** dans le menu du haut hello.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-215">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="eb0ed-217">Dans la liste des applications hello, sélectionnez **Halosys**.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-217">In hello applications list, select **Halosys**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_50.png) 

3. <span data-ttu-id="eb0ed-219">Dans le menu hello haut de hello, cliquez sur **utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-219">In hello menu on hello top, click **Users**.</span></span>

    ![Affecter des utilisateurs][203]

4. <span data-ttu-id="eb0ed-221">Dans la liste des utilisateurs hello, sélectionnez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-221">In hello Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="eb0ed-222">Dans la barre d’outils de hello en bas de hello, cliquez sur **affecter**.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-222">In hello toolbar on hello bottom, click **Assign**.</span></span>

    ![Affecter des utilisateurs][205]


### <a name="testing-single-sign-on"></a><span data-ttu-id="eb0ed-224">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="eb0ed-224">Testing single sign-on</span></span>

<span data-ttu-id="eb0ed-225">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="eb0ed-226">Lorsque vous cliquez sur hello Halosys vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour Halosys application.</span><span class="sxs-lookup"><span data-stu-id="eb0ed-226">When you click hello Halosys tile in hello Access Panel, you should get automatically signed-on tooyour Halosys application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="eb0ed-227">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="eb0ed-227">Additional resources</span></span>

* [<span data-ttu-id="eb0ed-228">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eb0ed-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="eb0ed-229">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="eb0ed-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_205.png
