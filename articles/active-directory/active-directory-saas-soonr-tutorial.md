---
title: "Didacticiel : Intégration d’Azure Active Directory à Soonr Workplace | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et l’espace de travail Soonr."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
editor: na
ms.assetid: b75f5f00-ea8b-4850-ae2e-134e5d678d97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: f950b45d0beceab2fa17b7690c9de81ec6603089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-soonr-workplace"></a><span data-ttu-id="92308-103">Didacticiel : Intégration d’Azure Active Directory à Soonr Workplace</span><span class="sxs-lookup"><span data-stu-id="92308-103">Tutorial: Azure Active Directory integration with Soonr Workplace</span></span>

<span data-ttu-id="92308-104">objectif Hello de ce didacticiel est tooshow vous comment toointegrate Soonr espace de travail avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="92308-104">hello objective of this tutorial is tooshow you how toointegrate Soonr Workplace with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="92308-105">Intégration d’espace de travail Soonr à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="92308-105">Integrating Soonr Workplace with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="92308-106">Vous pouvez contrôler dans Azure AD qui a accès tooSoonr espace de travail</span><span class="sxs-lookup"><span data-stu-id="92308-106">You can control in Azure AD who has access tooSoonr Workplace</span></span>
- <span data-ttu-id="92308-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSoonr espace de travail (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="92308-107">You can enable your users tooautomatically get signed-on tooSoonr Workplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="92308-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure classic</span><span class="sxs-lookup"><span data-stu-id="92308-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="92308-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="92308-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92308-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="92308-110">Prerequisites</span></span>

<span data-ttu-id="92308-111">tooconfigure intégration d’Azure AD avec l’espace de travail Soonr, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="92308-111">tooconfigure Azure AD integration with Soonr Workplace, you need hello following items:</span></span>

- <span data-ttu-id="92308-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="92308-112">An Azure AD subscription</span></span>
- <span data-ttu-id="92308-113">Un abonnement Soonr Workplace pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="92308-113">A Soonr Workplace single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="92308-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="92308-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="92308-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="92308-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="92308-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="92308-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="92308-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="92308-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="92308-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="92308-118">Scenario description</span></span>
<span data-ttu-id="92308-119">objectif Hello de ce didacticiel est tooenable vous tootest Azure AD l’authentification unique dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="92308-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="92308-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="92308-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="92308-121">Ajout d’espace de travail Soonr à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="92308-121">Adding Soonr Workplace from hello gallery</span></span>
2. <span data-ttu-id="92308-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="92308-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-soonr-workplace-from-hello-gallery"></a><span data-ttu-id="92308-123">Ajout d’espace de travail Soonr à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="92308-123">Adding Soonr Workplace from hello gallery</span></span>
<span data-ttu-id="92308-124">intégration de hello tooconfigure Soonr espace de travail dans Azure AD, vous devez tooadd Soonr espace de travail à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="92308-124">tooconfigure hello integration of Soonr Workplace into Azure AD, you need tooadd Soonr Workplace from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="92308-125">**tooadd Soonr espace de travail à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="92308-125">**tooadd Soonr Workplace from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="92308-126">Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="92308-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="92308-128">À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="92308-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="92308-129">vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.</span><span class="sxs-lookup"><span data-stu-id="92308-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Applications][2]

4. <span data-ttu-id="92308-131">Cliquez sur **ajouter** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="92308-131">Click **Add** at hello bottom of hello page.</span></span>

    ![Applications][3]

5. <span data-ttu-id="92308-133">Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application à partir de la galerie de hello**.</span><span class="sxs-lookup"><span data-stu-id="92308-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
 
    ![Applications][4]

6. <span data-ttu-id="92308-135">Dans la zone de recherche de hello, tapez **espace de travail Soonr**.</span><span class="sxs-lookup"><span data-stu-id="92308-135">In hello search box, type **Soonr Workplace**.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_01.png)

7. <span data-ttu-id="92308-137">Dans le volet de résultats hello, sélectionnez **espace de travail Soonr**, puis cliquez sur **Complete** application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="92308-137">In hello results pane, select **Soonr Workplace**, and then click **Complete** tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="92308-139">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="92308-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="92308-140">objectif Hello de cette section est tooshow comment tooconfigure et test Azure AD l’authentification unique avec l’espace de travail Soonr en fonction d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="92308-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with Soonr Workplace based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="92308-141">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello utilisateur de tooan Soonr espace de travail dans Azure AD est.</span><span class="sxs-lookup"><span data-stu-id="92308-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Soonr Workplace tooan user in Azure AD is.</span></span> <span data-ttu-id="92308-142">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans l’espace de travail Soonr hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="92308-142">In other words, a link relationship between an Azure AD user and hello related user in Soonr Workplace needs toobe established.</span></span>  

<span data-ttu-id="92308-143">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans l’espace de travail Soonr.</span><span class="sxs-lookup"><span data-stu-id="92308-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Soonr Workplace.</span></span>

<span data-ttu-id="92308-144">tooconfigure et test Azure AD l’authentification unique avec l’espace de travail Soonr, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="92308-144">tooconfigure and test Azure AD single sign-on with Soonr Workplace, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="92308-145">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="92308-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="92308-146">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="92308-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="92308-147">**[Création d’un utilisateur de test d’espace de travail Soonr](#creating-a-soonr-workplace-test-user)**  -toohave de Britta Simon dans l’espace de travail Soonr qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.</span><span class="sxs-lookup"><span data-stu-id="92308-147">**[Creating a Soonr Workplace test user](#creating-a-soonr-workplace-test-user)** - toohave a counterpart of Britta Simon in Soonr Workplace that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="92308-148">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="92308-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="92308-149">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="92308-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="92308-150">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="92308-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="92308-151">Dans cette section, vous activez Azure AD l’authentification unique dans le portail classique de hello et configurez l’authentification unique dans votre application de l’espace de travail Soonr.</span><span class="sxs-lookup"><span data-stu-id="92308-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your Soonr Workplace application.</span></span>


<span data-ttu-id="92308-152">**tooconfigure Azure AD single sign-on avec Soonr, espace de travail, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="92308-152">**tooconfigure Azure AD single sign-on with Soonr Workplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="92308-153">Bonjour portail Azure classic sur hello **espace de travail Soonr** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello **configurer l’authentification unique sur**  boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="92308-153">In hello Azure classic portal, on hello **Soonr Workplace** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>

    ![Configurer l’authentification unique][6] 

2. <span data-ttu-id="92308-155">Sur hello **Comment souhaitez-vous toosign les utilisateurs sur l’espace de travail de tooSoonr** page, sélectionnez **Azure AD Single Sign-On**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="92308-155">On hello **How would you like users toosign on tooSoonr Workplace** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_03.png) 

3. <span data-ttu-id="92308-157">Sur hello **configurer les paramètres de l’application** boîte de dialogue de page, effectuer hello comme suit :.</span><span class="sxs-lookup"><span data-stu-id="92308-157">On hello **Configure App Settings** dialog page, perform hello following steps:.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_04.png) 

    <span data-ttu-id="92308-159">a.</span><span class="sxs-lookup"><span data-stu-id="92308-159">a.</span></span> <span data-ttu-id="92308-160">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle : `https://<server-name>.soonr.com/singlesignon/saml/SSO`.</span><span class="sxs-lookup"><span data-stu-id="92308-160">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.</span></span>

    <span data-ttu-id="92308-161">b.</span><span class="sxs-lookup"><span data-stu-id="92308-161">b.</span></span> <span data-ttu-id="92308-162">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="92308-162">Click **Next**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="92308-163">Notez qu’il ne s’agit pas de la valeur réelle hello.</span><span class="sxs-lookup"><span data-stu-id="92308-163">Please note that this is not hello real value.</span></span> <span data-ttu-id="92308-164">Vous avez tooupdate URL de connexion cette valeur avec hello réel.</span><span class="sxs-lookup"><span data-stu-id="92308-164">You have tooupdate this value with hello actual Sign On URL.</span></span> <span data-ttu-id="92308-165">Espace de travail Soonr contact prend en charge team tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="92308-165">Contact Soonr Workplace support team tooget this value.</span></span>

4. <span data-ttu-id="92308-166">Sur hello **configurer l’authentification unique à l’espace de travail Soonr** , cliquez sur **télécharger des métadonnées** , puis enregistrez le fichier hello sur votre ordinateur :</span><span class="sxs-lookup"><span data-stu-id="92308-166">On hello **Configure single sign-on at Soonr Workplace** page, click **Download metadata** and then save hello file on your computer:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_05.png) 

5. <span data-ttu-id="92308-168">tooget SSO configuré pour votre application, contactez votre équipe de support Soonr espace de travail et leur fournir des éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="92308-168">tooget SSO configured for your application, contact your Soonr Workplace support team and provide them with hello following:</span></span> 

    <span data-ttu-id="92308-169">hello • téléchargé **métadonnées** fichier</span><span class="sxs-lookup"><span data-stu-id="92308-169">•  hello downloaded **Metadata** file</span></span>

    <span data-ttu-id="92308-170">• hello **URL de l’émetteur**</span><span class="sxs-lookup"><span data-stu-id="92308-170">•  hello **Issuer URL**</span></span>

    <span data-ttu-id="92308-171">• hello **URL SSO SAML**</span><span class="sxs-lookup"><span data-stu-id="92308-171">•  hello **SAML SSO URL**</span></span>

    <span data-ttu-id="92308-172">• hello **URL de Service de déconnexion unique**</span><span class="sxs-lookup"><span data-stu-id="92308-172">•  hello **Single Sign-Out Service URL**</span></span>

    >[!NOTE]
    ><span data-ttu-id="92308-173">Cette application est remplacée par <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">espace de travail Autotask</a> et vous pouvez faire référence <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">cela</a> didacticiel pour la configuration d’application hello avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92308-173">This application is superseded by <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask Workplace</a> and you can refer <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">this</a> tutorial for configuring hello application with Azure AD.</span></span>
   
6. <span data-ttu-id="92308-174">Bonjour portail Azure classic, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="92308-174">In hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>

    ![Authentification unique Azure AD][10]

7. <span data-ttu-id="92308-176">Sur hello **Single sign-on confirmation** , cliquez sur **Complete**.</span><span class="sxs-lookup"><span data-stu-id="92308-176">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
  
    ![Authentification unique Azure AD][11]



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="92308-178">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="92308-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="92308-179">objectif Hello de cette section est toocreate un utilisateur de test dans le portail Azure classic appelé Britta Simon de hello.</span><span class="sxs-lookup"><span data-stu-id="92308-179">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>  

![Créer un utilisateur Azure AD][20]

<span data-ttu-id="92308-181">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="92308-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="92308-182">Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="92308-182">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="92308-184">À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="92308-184">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="92308-185">liste de hello toodisplay d’utilisateurs, dans le menu hello haut de hello, cliquez sur **utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="92308-185">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="92308-187">tooopen hello **ajouter un utilisateur** boîte de dialogue, dans la barre d’outils de hello en bas de hello, cliquez sur **ajouter un utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="92308-187">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="92308-189">Sur hello **faites-nous part de cet utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="92308-189">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_05.png) 

    <span data-ttu-id="92308-191">a.</span><span class="sxs-lookup"><span data-stu-id="92308-191">a.</span></span> <span data-ttu-id="92308-192">Dans Type d’utilisateur, sélectionnez Nouvel utilisateur dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="92308-192">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="92308-193">b.</span><span class="sxs-lookup"><span data-stu-id="92308-193">b.</span></span> <span data-ttu-id="92308-194">Bonjour, nom d’utilisateur **zone de texte**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="92308-194">In hello User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="92308-195">c.</span><span class="sxs-lookup"><span data-stu-id="92308-195">c.</span></span> <span data-ttu-id="92308-196">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="92308-196">Click **Next**.</span></span>

6.  <span data-ttu-id="92308-197">Sur hello **profil utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="92308-197">On hello **User Profile** dialog page, perform hello following steps:</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_06.png) 

    <span data-ttu-id="92308-199">a.</span><span class="sxs-lookup"><span data-stu-id="92308-199">a.</span></span> <span data-ttu-id="92308-200">Bonjour **prénom** zone de texte, type **Brian**.</span><span class="sxs-lookup"><span data-stu-id="92308-200">In hello **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="92308-201">b.</span><span class="sxs-lookup"><span data-stu-id="92308-201">b.</span></span> <span data-ttu-id="92308-202">Bonjour **nom** zone de texte, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="92308-202">In hello **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="92308-203">c.</span><span class="sxs-lookup"><span data-stu-id="92308-203">c.</span></span> <span data-ttu-id="92308-204">Bonjour **nom d’affichage** zone de texte, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="92308-204">In hello **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="92308-205">d.</span><span class="sxs-lookup"><span data-stu-id="92308-205">d.</span></span> <span data-ttu-id="92308-206">Bonjour **rôle** liste, sélectionnez **utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="92308-206">In hello **Role** list, select **User**.</span></span>

    <span data-ttu-id="92308-207">e.</span><span class="sxs-lookup"><span data-stu-id="92308-207">e.</span></span> <span data-ttu-id="92308-208">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="92308-208">Click **Next**.</span></span>

7. <span data-ttu-id="92308-209">Sur hello **mot de passe temporaire Get** page de boîte de dialogue, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="92308-209">On hello **Get temporary password** dialog page, click **create**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="92308-211">Sur hello **mot de passe temporaire Get** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="92308-211">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="92308-213">a.</span><span class="sxs-lookup"><span data-stu-id="92308-213">a.</span></span> <span data-ttu-id="92308-214">Notez la valeur hello hello **nouveau mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="92308-214">Write down hello value of hello **New Password**.</span></span>

    <span data-ttu-id="92308-215">b.</span><span class="sxs-lookup"><span data-stu-id="92308-215">b.</span></span> <span data-ttu-id="92308-216">Cliquez sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="92308-216">Click **Complete**.</span></span>   



### <a name="creating-a-soonr-workplace-test-user"></a><span data-ttu-id="92308-217">Création d’un utilisateur de test Soonr Workplace</span><span class="sxs-lookup"><span data-stu-id="92308-217">Creating a Soonr Workplace test user</span></span>

<span data-ttu-id="92308-218">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans l’espace de travail Soonr.</span><span class="sxs-lookup"><span data-stu-id="92308-218">hello objective of this section is toocreate a user called Britta Simon in Soonr Workplace.</span></span> <span data-ttu-id="92308-219">Collaborez avec l’espace de travail Soonr prise en charge team toocreate un utilisateur dans la plateforme de hello.</span><span class="sxs-lookup"><span data-stu-id="92308-219">Please work with Soonr Workplace support team toocreate a user in hello platform.</span></span> <span data-ttu-id="92308-220">Vous pouvez augmenter le ticket de support hello avec Soonr de <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">ici</a>.</span><span class="sxs-lookup"><span data-stu-id="92308-220">You can raise hello support ticket with Soonr from <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">here</a>.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="92308-221">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="92308-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="92308-222">objectif Hello de cette section est tooenabling toouse Britta Simon Azure l’authentification unique en accordant son tooSoonr accès espace de travail.</span><span class="sxs-lookup"><span data-stu-id="92308-222">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooSoonr Workplace.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="92308-224">**tooassign Britta Simon tooSoonr espace de travail, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="92308-224">**tooassign Britta Simon tooSoonr Workplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="92308-225">Dans hello Azure portail classique, la vue applications hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.</span><span class="sxs-lookup"><span data-stu-id="92308-225">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="92308-227">Dans la liste des applications hello, sélectionnez **espace de travail Soonr**.</span><span class="sxs-lookup"><span data-stu-id="92308-227">In hello applications list, select **Soonr Workplace**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_50.png) 

1. <span data-ttu-id="92308-229">Dans le menu hello haut de hello, cliquez sur **utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="92308-229">In hello menu on hello top, click **Users**.</span></span>

    ![Affecter des utilisateurs][203] 

1. <span data-ttu-id="92308-231">Dans la liste des utilisateurs hello, sélectionnez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="92308-231">In hello Users list, select **Britta Simon**.</span></span>

2. <span data-ttu-id="92308-232">Dans la barre d’outils de hello en bas de hello, cliquez sur **affecter**.</span><span class="sxs-lookup"><span data-stu-id="92308-232">In hello toolbar on hello bottom, click **Assign**.</span></span>

    ![Affecter des utilisateurs][205]



### <a name="testing-single-sign-on"></a><span data-ttu-id="92308-234">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="92308-234">Testing single sign-on</span></span>

<span data-ttu-id="92308-235">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="92308-235">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="92308-236">Lorsque vous cliquez sur hello espace de travail Soonr vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur application de l’espace de travail Soonr tooyour.</span><span class="sxs-lookup"><span data-stu-id="92308-236">When you click hello Soonr Workplace tile in hello Access Panel, you should get automatically signed-on tooyour Soonr Workplace application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="92308-237">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="92308-237">Additional resources</span></span>

* [<span data-ttu-id="92308-238">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="92308-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="92308-239">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="92308-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_205.png
