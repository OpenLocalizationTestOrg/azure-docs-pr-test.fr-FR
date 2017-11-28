---
title: "Didacticiel : Intégration d’Azure Active Directory à Bynder | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Bynder."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 4fb0ab26-b3b9-420a-8072-a0be80ea021e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: a2a8477580d28fe422f2836f483dff286bc71c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bynder"></a><span data-ttu-id="ad4c9-103">Didacticiel : Intégration d’Azure Active Directory avec Bynder</span><span class="sxs-lookup"><span data-stu-id="ad4c9-103">Tutorial: Azure Active Directory integration with Bynder</span></span>
<span data-ttu-id="ad4c9-104">objectif Hello de ce didacticiel est tooshow vous comment toointegrate Bynder avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ad4c9-104">hello objective of this tutorial is tooshow you how toointegrate Bynder with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ad4c9-105">Intégration Bynder à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="ad4c9-105">Integrating Bynder with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="ad4c9-106">Vous pouvez contrôler dans Azure AD qui a accès tooBynder</span><span class="sxs-lookup"><span data-stu-id="ad4c9-106">You can control in Azure AD who has access tooBynder</span></span>
* <span data-ttu-id="ad4c9-107">Vous pouvez activer vos utilisateurs tooautomatically get tooBynder connecté-session unique (SSO) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad4c9-107">You can enable your users tooautomatically get signed-on tooBynder single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="ad4c9-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure classic</span><span class="sxs-lookup"><span data-stu-id="ad4c9-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="ad4c9-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ad4c9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad4c9-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ad4c9-110">Prerequisites</span></span>
<span data-ttu-id="ad4c9-111">tooconfigure intégration d’Azure AD avec Bynder, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ad4c9-111">tooconfigure Azure AD integration with Bynder, you need hello following items:</span></span>

* <span data-ttu-id="ad4c9-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad4c9-112">An Azure AD subscription</span></span>
* <span data-ttu-id="ad4c9-113">Un abonnement Bynder pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="ad4c9-113">A Bynder single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="ad4c9-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="ad4c9-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="ad4c9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="ad4c9-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="ad4c9-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ad4c9-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ad4c9-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="ad4c9-118">Scenario description</span></span>
<span data-ttu-id="ad4c9-119">objectif Hello de ce didacticiel est tooenable vous tootest Microsoft Azure AD SSO dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-119">hello objective of this tutorial is tooenable you tootest Microsoft Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="ad4c9-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="ad4c9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ad4c9-121">Ajout de Bynder à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="ad4c9-121">Adding Bynder from hello gallery</span></span>
2. <span data-ttu-id="ad4c9-122">Configuration et test de l’authentification unique Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad4c9-122">Configuring and testing Microsoft Azure AD SSO</span></span>

## <a name="add-bynder-from-hello-gallery"></a><span data-ttu-id="ad4c9-123">Ajouter des Bynder à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="ad4c9-123">Add Bynder from hello gallery</span></span>
<span data-ttu-id="ad4c9-124">intégration de hello tooconfigure de Bynder dans Azure AD, vous devez tooadd Bynder à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-124">tooconfigure hello integration of Bynder into Azure AD, you need tooadd Bynder from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ad4c9-125">**tooadd Bynder à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ad4c9-125">**tooadd Bynder from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad4c9-126">Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-126">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="ad4c9-128">À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="ad4c9-129">vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="ad4c9-131">Cliquez sur **ajouter** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="ad4c9-133">Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application à partir de la galerie de hello**.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="ad4c9-135">Dans la zone de recherche de hello, tapez **Bynder**.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-135">In hello search box, type **Bynder**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_01.png)
7. <span data-ttu-id="ad4c9-137">Dans le volet de résultats hello, sélectionnez **Bynder**, puis cliquez sur **Complete** application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-137">In hello results panel, select **Bynder**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Sélection d’application hello dans la galerie de hello](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_001.png)

## <a name="configure-and-test-microsoft-azure-ad-sso"></a><span data-ttu-id="ad4c9-139">Configurer et tester l’authentification unique Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad4c9-139">Configure and test Microsoft Azure AD SSO</span></span>
<span data-ttu-id="ad4c9-140">objectif Hello de cette section est tooshow comment tooconfigure et test Microsoft Azure AD SSO avec Bynder en fonction d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="ad4c9-140">hello objective of this section is tooshow you how tooconfigure and test Microsoft Azure AD SSO with Bynder based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ad4c9-141">Pour l’authentification unique toowork, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Bynder tooan l’utilisateur dans Azure AD est.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-141">For SSO toowork, Azure AD needs tooknow what hello counterpart user in Bynder tooan user in Azure AD is.</span></span> <span data-ttu-id="ad4c9-142">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Bynder doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-142">In other words, a link relationship between an Azure AD user and hello related user in Bynder needs toobe established.</span></span>

<span data-ttu-id="ad4c9-143">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Bynder.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Bynder.</span></span>

<span data-ttu-id="ad4c9-144">tooconfigure et test Microsoft Azure AD SSO avec Bynder, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="ad4c9-144">tooconfigure and test Microsoft Azure AD SSO with Bynder, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ad4c9-145">**[Configuration de Microsoft Azure AD l’authentification unique sur](#configuring-azure-ad-single-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-145">**[Configuring Microsoft Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ad4c9-146">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Microsoft Azure AD Single Sign-On with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Microsoft Azure AD Single Sign-On with Britta Simon.</span></span>
3. <span data-ttu-id="ad4c9-147">**[Création d’un utilisateur de test Bynder](#creating-a-bynder-test-user)**  -toohave de Britta Simon dans Bynder qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-147">**[Creating a Bynder test user](#creating-a-bynder-test-user)** - toohave a counterpart of Britta Simon in Bynder that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="ad4c9-148">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable toouse Britta Simon Microsoft Azure AD Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Microsoft Azure AD Single Sign-On.</span></span>
5. <span data-ttu-id="ad4c9-149">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-149">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-microsoft-azure-ad-sso"></a><span data-ttu-id="ad4c9-150">Configuration de l’authentification unique Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad4c9-150">Configuring Microsoft Azure AD SSO</span></span>
<span data-ttu-id="ad4c9-151">Dans cette section, vous activez l’authentification unique de Microsoft Azure AD dans le portail classique de hello et configurez l’authentification unique dans votre application Bynder.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-151">In this section, you enable Microsoft Azure AD SSO in hello classic portal and configure SSO in your Bynder application.</span></span>

<span data-ttu-id="ad4c9-152">**tooconfigure l’authentification unique de Microsoft Azure AD avec Bynder, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ad4c9-152">**tooconfigure Microsoft Azure AD SSO with Bynder, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad4c9-153">Dans le portail classique hello, sur hello **Bynder** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello **configurer l’authentification unique sur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-153">In hello classic portal, on hello **Bynder** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configurer l’authentification unique][6] 
2. <span data-ttu-id="ad4c9-155">Sur hello **Comment souhaitez-vous toosign utilisateurs sur tooBynder** page, sélectionnez **Microsoft Azure AD Single Sign-On**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-155">On hello **How would you like users toosign on tooBynder** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_03.png)
3. <span data-ttu-id="ad4c9-157">Sur hello **configurer les paramètres de l’application** page de boîte de dialogue, si vous le souhaitez application hello tooconfigure **mode initialisée par IDP**, effectuer hello comme suit, puis cliquez sur **suivant**:</span><span class="sxs-lookup"><span data-stu-id="ad4c9-157">On hello **Configure App Settings** dialog page, If you wish tooconfigure hello application in **IDP initiated mode**, perform hello following steps and click **Next**:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_04.png)
  1. <span data-ttu-id="ad4c9-159">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company name>.getbynder.com/sso/SAML/authenticate/`</span><span class="sxs-lookup"><span data-stu-id="ad4c9-159">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.getbynder.com/sso/SAML/authenticate/`</span></span>
  2. <span data-ttu-id="ad4c9-160">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-160">Click **Next**.</span></span>
4. <span data-ttu-id="ad4c9-161">Si vous le souhaitez application hello tooconfigure **mode initiée par SP** sur hello **configurer les paramètres de l’application** page de boîte de dialogue, puis cliquez sur hello **« (facultatifs) des paramètres avancé afficher »**, puis entrez hello **URL de connexion** et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-161">If you wish tooconfigure hello application in **SP initiated mode** on hello **Configure App Settings** dialog page, then click on hello **“Show advanced settings (optional)”** and then enter hello **Sign On URL** and click **Next**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_10.png)
  1. <span data-ttu-id="ad4c9-163">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company name>.getbynder.com/login/`</span><span class="sxs-lookup"><span data-stu-id="ad4c9-163">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<company name>.getbynder.com/login/`</span></span>
  2. <span data-ttu-id="ad4c9-164">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-164">Click **Next**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="ad4c9-165">valeur Hello hello URL de connexion de ce didacticiel est simplement un placeholfer.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-165">hello value for hello Sign On URL in this tutorial is just a placeholfer.</span></span> <span data-ttu-id="ad4c9-166">valeur réelle de tooget hello pour votre environnement, contactez Bynder.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-166">tooget hello actual vlaue for your environment, contact Bynder.</span></span>
   >

5. <span data-ttu-id="ad4c9-167">Sur hello **configurer l’authentification unique sur Bynder** page, effectuer hello comme suit, puis cliquez sur **suivant**:</span><span class="sxs-lookup"><span data-stu-id="ad4c9-167">On hello **Configure single sign-on at Bynder** page, perform hello following steps and click **Next**:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_05.png)  
  1. <span data-ttu-id="ad4c9-169">Cliquez sur **télécharger des métadonnées**, puis enregistrez le fichier hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-169">Click **Download metadata**, and then save hello file on your computer.</span></span>
  2. <span data-ttu-id="ad4c9-170">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-170">Click **Next**.</span></span>
6. <span data-ttu-id="ad4c9-171">tooget SSO configuré pour votre application, contactez votre équipe de support Bynder.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-171">tooget SSO configured for your application, contact your Bynder support team.</span></span> <span data-ttu-id="ad4c9-172">Attacher le fichier de métadonnées téléchargé hello et partagez-le avec tooset d’équipe Bynder configuration de SSO sur son côté.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-172">Attach hello downloaded metadata file and share it with Bynder team tooset up SSO on their side.</span></span>
7. <span data-ttu-id="ad4c9-173">Dans le portail classique hello, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-173">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Authentification unique Azure AD][10]
8. <span data-ttu-id="ad4c9-175">Sur hello **Single sign-on confirmation** , cliquez sur **Complete**.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-175">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Authentification unique Azure AD][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ad4c9-177">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad4c9-177">Create an Azure AD test user</span></span>
<span data-ttu-id="ad4c9-178">objectif Hello de cette section est toocreate un utilisateur de test dans le portail classique de hello appelé Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-178">hello objective of this section is toocreate a test user in hello classic portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][20]

<span data-ttu-id="ad4c9-180">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ad4c9-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad4c9-181">Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-181">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="ad4c9-183">À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-183">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="ad4c9-184">liste de hello toodisplay d’utilisateurs, dans le menu hello haut de hello, cliquez sur **utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-184">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="ad4c9-186">tooopen hello **ajouter un utilisateur** boîte de dialogue, dans la barre d’outils de hello en bas de hello, cliquez sur **ajouter un utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-186">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="ad4c9-188">Sur hello **faites-nous part de cet utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="ad4c9-188">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_05.png)
  1. <span data-ttu-id="ad4c9-190">Dans Type d’utilisateur, sélectionnez Nouvel utilisateur dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="ad4c9-191">Bonjour, nom d’utilisateur **zone de texte**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-191">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="ad4c9-192">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-192">Click **Next**.</span></span>
6. <span data-ttu-id="ad4c9-193">Sur hello **profil utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="ad4c9-193">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
   ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="ad4c9-195">Bonjour **prénom** zone de texte, type **Brian**.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-195">In hello **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="ad4c9-196">Bonjour **nom** zone de texte, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-196">In hello **Last Name** textbox, type, **Simon**.</span></span> 
  3. <span data-ttu-id="ad4c9-197">Bonjour **nom d’affichage** zone de texte, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-197">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="ad4c9-198">Bonjour **rôle** liste, sélectionnez **utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-198">In hello **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="ad4c9-199">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-199">Click **Next**.</span></span>
7. <span data-ttu-id="ad4c9-200">Sur hello **mot de passe temporaire Get** page de boîte de dialogue, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-200">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="ad4c9-202">Sur hello **mot de passe temporaire Get** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="ad4c9-202">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_08.png)
   1. <span data-ttu-id="ad4c9-204">Notez la valeur hello hello **nouveau mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-204">Write down hello value of hello **New Password**.</span></span>
   2. <span data-ttu-id="ad4c9-205">Cliquez sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-205">Click **Complete**.</span></span>   

### <a name="create-a-bynder-test-user"></a><span data-ttu-id="ad4c9-206">Créer un utilisateur de test Bynder</span><span class="sxs-lookup"><span data-stu-id="ad4c9-206">Create a Bynder test user</span></span>
<span data-ttu-id="ad4c9-207">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans Bynder.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-207">hello objective of this section is toocreate a user called Britta Simon in Bynder.</span></span> <span data-ttu-id="ad4c9-208">Bynder prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-208">Bynder supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="ad4c9-209">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-209">There is no action item for you in this section.</span></span> <span data-ttu-id="ad4c9-210">Un nouvel utilisateur s’affichera pendant une tentative de tooaccess Bynder s’il n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-210">A new user will be created during an attempt tooaccess Bynder if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="ad4c9-211">Si vous devez manuellement toocreate un utilisateur, vous avez besoin d’équipe de support Bynder toocontact hello.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-211">If you need toocreate an user manually, you need toocontact hello Bynder support team.</span></span> 
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="ad4c9-212">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad4c9-212">Assign hello Azure AD test user</span></span>
<span data-ttu-id="ad4c9-213">objectif Hello de cette section est tooenabling Britta Simon toouse Azure SSO en accordant tooBynder de son accès.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-213">hello objective of this section is tooenabling Britta Simon toouse Azure SSO by granting her access tooBynder.</span></span>

   ![Affecter des utilisateurs][200]

<span data-ttu-id="ad4c9-215">**tooassign Britta Simon tooBynder, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ad4c9-215">**tooassign Britta Simon tooBynder, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad4c9-216">Sur le portail classique hello, cliquez sur la vue applications hello tooopen, dans la vue active de hello, **Applications** dans le menu du haut hello.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-216">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Affecter des utilisateurs][201]
2. <span data-ttu-id="ad4c9-218">Dans la liste des applications hello, sélectionnez **Bynder**.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-218">In hello applications list, select **Bynder**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_50.png)
3. <span data-ttu-id="ad4c9-220">Dans le menu hello haut de hello, cliquez sur **utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-220">In hello menu on hello top, click **Users**.</span></span>
   
    ![Affecter des utilisateurs][203]
4. <span data-ttu-id="ad4c9-222">Dans la liste des utilisateurs hello, sélectionnez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-222">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="ad4c9-223">Dans la barre d’outils de hello en bas de hello, cliquez sur **affecter**.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-223">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Affecter des utilisateurs][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="ad4c9-225">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="ad4c9-225">Test single sign-on</span></span>
<span data-ttu-id="ad4c9-226">objectif Hello de cette section est tootest votre configuration de l’authentification unique de Microsoft Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-226">hello objective of this section is tootest your Microsoft Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="ad4c9-227">Lorsque vous cliquez sur mosaïque Bynder hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Bynder application.</span><span class="sxs-lookup"><span data-stu-id="ad4c9-227">When you click hello Bynder tile in hello Access Panel, you should get automatically signed-on tooyour Bynder application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ad4c9-228">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="ad4c9-228">Additional resources</span></span>
* [<span data-ttu-id="ad4c9-229">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ad4c9-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ad4c9-230">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="ad4c9-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_205.png
