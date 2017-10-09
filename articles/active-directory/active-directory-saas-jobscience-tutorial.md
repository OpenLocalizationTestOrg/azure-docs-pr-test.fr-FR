---
title: "Didacticiel : Intégration d’Azure Active Directory avec Jobscience | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Jobscience."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 77282dcc-bbe2-4728-953d-adb4ab6a713b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 4a4c78aad6d324795a15a9569542afc23b4716d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobscience"></a><span data-ttu-id="2be50-103">Didacticiel : Intégration d’Azure Active Directory à Jobscience</span><span class="sxs-lookup"><span data-stu-id="2be50-103">Tutorial: Azure Active Directory integration with Jobscience</span></span>

<span data-ttu-id="2be50-104">Dans ce didacticiel, vous apprendrez comment toointegrate Jobscience avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2be50-104">In this tutorial, you learn how toointegrate Jobscience with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2be50-105">Intégration de Jobscience à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="2be50-105">Integrating Jobscience with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2be50-106">Vous pouvez contrôler dans Azure AD qui a accès tooJobscience</span><span class="sxs-lookup"><span data-stu-id="2be50-106">You can control in Azure AD who has access tooJobscience</span></span>
- <span data-ttu-id="2be50-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooJobscience (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="2be50-107">You can enable your users tooautomatically get signed-on tooJobscience (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2be50-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="2be50-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2be50-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2be50-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2be50-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="2be50-110">Prerequisites</span></span>

<span data-ttu-id="2be50-111">tooconfigure intégration d’Azure AD avec Jobscience, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2be50-111">tooconfigure Azure AD integration with Jobscience, you need hello following items:</span></span>

- <span data-ttu-id="2be50-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="2be50-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2be50-113">Un abonnement Jobscience pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="2be50-113">A Jobscience single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2be50-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="2be50-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2be50-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="2be50-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2be50-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="2be50-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2be50-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois ici : [offre d’essai](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2be50-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2be50-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="2be50-118">Scenario description</span></span>
<span data-ttu-id="2be50-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="2be50-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2be50-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="2be50-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2be50-121">Ajout de Jobscience à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="2be50-121">Adding Jobscience from hello gallery</span></span>
2. <span data-ttu-id="2be50-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2be50-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jobscience-from-hello-gallery"></a><span data-ttu-id="2be50-123">Ajout de Jobscience à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="2be50-123">Adding Jobscience from hello gallery</span></span>
<span data-ttu-id="2be50-124">intégration de hello tooconfigure de Jobscience dans Azure AD, vous devez tooadd Jobscience à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="2be50-124">tooconfigure hello integration of Jobscience into Azure AD, you need tooadd Jobscience from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2be50-125">**tooadd Jobscience à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2be50-125">**tooadd Jobscience from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2be50-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="2be50-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2be50-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="2be50-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2be50-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="2be50-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="2be50-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="2be50-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="2be50-133">Dans la zone de recherche de hello, tapez **Jobscience**.</span><span class="sxs-lookup"><span data-stu-id="2be50-133">In hello search box, type **Jobscience**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_search.png)

5. <span data-ttu-id="2be50-135">Dans le volet de résultats hello, sélectionnez **Jobscience**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="2be50-135">In hello results panel, select **Jobscience**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2be50-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2be50-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2be50-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Jobscience avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="2be50-138">In this section, you configure and test Azure AD single sign-on with Jobscience based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2be50-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Jobscience est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2be50-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Jobscience is tooa user in Azure AD.</span></span> <span data-ttu-id="2be50-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Jobscience doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="2be50-140">In other words, a link relationship between an Azure AD user and hello related user in Jobscience needs toobe established.</span></span>

<span data-ttu-id="2be50-141">En l’occurrence, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="2be50-141">In Jobscience, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2be50-142">tooconfigure et test Azure AD l’authentification unique avec Jobscience, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="2be50-142">tooconfigure and test Azure AD single sign-on with Jobscience, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2be50-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="2be50-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2be50-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2be50-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2be50-145">**[Création d’un utilisateur de test de Jobscience](#creating-a-jobscience-test-user)**  -toohave un équivalent de Britta Simon dans Jobscience est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2be50-145">**[Creating a Jobscience test user](#creating-a-jobscience-test-user)** - toohave a counterpart of Britta Simon in Jobscience that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2be50-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="2be50-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2be50-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="2be50-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2be50-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2be50-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2be50-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de Jobscience.</span><span class="sxs-lookup"><span data-stu-id="2be50-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Jobscience application.</span></span>

<span data-ttu-id="2be50-150">**tooconfigure Azure AD single sign-on avec Jobscience, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2be50-150">**tooconfigure Azure AD single sign-on with Jobscience, perform hello following steps:**</span></span>

1. <span data-ttu-id="2be50-151">Bonjour portail Azure, sur hello **Jobscience** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="2be50-151">In hello Azure portal, on hello **Jobscience** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="2be50-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="2be50-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_samlbase.png)

3. <span data-ttu-id="2be50-155">Sur hello **Jobscience domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="2be50-155">On hello **Jobscience Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_url.png)

    <span data-ttu-id="2be50-157">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`http://<company name>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="2be50-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern:  `http://<company name>.my.salesforce.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="2be50-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="2be50-158">This value is not real.</span></span> <span data-ttu-id="2be50-159">Mettre à jour de cette valeur avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="2be50-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="2be50-160">Obtenir cette valeur en [équipe de support Client de Jobscience](https://www.jobscience.com/support) ou à partir du profil d’authentification unique hello, vous allez créer qui est expliqué plus loin dans le didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="2be50-160">Get this value by [Jobscience Client support team](https://www.jobscience.com/support) or from hello SSO profile you will create which is explained later in hello tutorial.</span></span> 
 
4. <span data-ttu-id="2be50-161">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="2be50-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_certificate.png) 

5. <span data-ttu-id="2be50-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="2be50-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jobscience-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2be50-165">Sur hello **Jobscience Configuration** , cliquez sur **configurer de Jobscience** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="2be50-165">On hello **Jobscience Configuration** section, click **Configure Jobscience** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2be50-166">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="2be50-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_configure.png) 

7. <span data-ttu-id="2be50-168">Ouvrez une session dans tooyour site d’entreprise Jobscience en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="2be50-168">Log in tooyour Jobscience company site as an administrator.</span></span>

8. <span data-ttu-id="2be50-169">Accédez trop**le programme d’installation**.</span><span class="sxs-lookup"><span data-stu-id="2be50-169">Go too**Setup**.</span></span>
   
   <span data-ttu-id="2be50-170">![Configuration](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Configuration")</span><span class="sxs-lookup"><span data-stu-id="2be50-170">![Setup](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Setup")</span></span>

9. <span data-ttu-id="2be50-171">Dans le volet de navigation gauche hello Bonjour **administrer** , cliquez sur **gestion des domaines** tooexpand hello section associée, puis cliquez sur **mon domaine** tooopen hello  **Mon domaine** page.</span><span class="sxs-lookup"><span data-stu-id="2be50-171">On hello left navigation pane, in hello **Administer** section, click **Domain Management** tooexpand hello related section, and then click **My Domain** tooopen hello **My Domain** page.</span></span> 
   
   <span data-ttu-id="2be50-172">![Mon domaine](./media/active-directory-saas-jobscience-tutorial/ic767825.png "mon domaine")</span><span class="sxs-lookup"><span data-stu-id="2be50-172">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span></span>

10. <span data-ttu-id="2be50-173">tooverify votre domaine a été correctement configuré, assurez-vous qu’il s’agit de «**tooUsers de déploiement d’étape 4**» et passez en revue votre «**mes paramètres de domaine**».</span><span class="sxs-lookup"><span data-stu-id="2be50-173">tooverify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed tooUsers**” and review your “**My Domain Settings**”.</span></span>

    <span data-ttu-id="2be50-174">![Domaine déployé tooUser](./media/active-directory-saas-jobscience-tutorial/ic784377.png "tooUser de domaine déployés")</span><span class="sxs-lookup"><span data-stu-id="2be50-174">![Domain Deployed tooUser](./media/active-directory-saas-jobscience-tutorial/ic784377.png "Domain Deployed tooUser")</span></span>

11. <span data-ttu-id="2be50-175">Sur le site d’entreprise hello Jobscience, cliquez sur **des contrôles de sécurité**, puis cliquez sur **paramètres d’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="2be50-175">On hello Jobscience company site, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="2be50-176">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784364.png "Security Controls")</span><span class="sxs-lookup"><span data-stu-id="2be50-176">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784364.png "Security Controls")</span></span>

12. <span data-ttu-id="2be50-177">Bonjour **paramètres d’authentification unique** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="2be50-177">In hello **Single Sign-On Settings** section, perform hello following steps:</span></span>
    
    <span data-ttu-id="2be50-178">![Paramètres d’authentification unique](./media/active-directory-saas-jobscience-tutorial/ic781026.png "paramètres d’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="2be50-178">![Single Sign-On Settings](./media/active-directory-saas-jobscience-tutorial/ic781026.png "Single Sign-On Settings")</span></span>
    
    <span data-ttu-id="2be50-179">a.</span><span class="sxs-lookup"><span data-stu-id="2be50-179">a.</span></span> <span data-ttu-id="2be50-180">Sélectionnez **SAML Enabled**.</span><span class="sxs-lookup"><span data-stu-id="2be50-180">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="2be50-181">b.</span><span class="sxs-lookup"><span data-stu-id="2be50-181">b.</span></span> <span data-ttu-id="2be50-182">Cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="2be50-182">Click **New**.</span></span>

13. <span data-ttu-id="2be50-183">Sur hello **SAML unique Sign-On Setting Edit** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="2be50-183">On hello **SAML Single Sign-On Setting Edit** dialog, perform hello following steps:</span></span>
    
    <span data-ttu-id="2be50-184">![Configuration de l’authentification unique SAML](./media/active-directory-saas-jobscience-tutorial/ic784365.png "Configuration de l’authentification unique SAML")</span><span class="sxs-lookup"><span data-stu-id="2be50-184">![SAML Single Sign-On Setting](./media/active-directory-saas-jobscience-tutorial/ic784365.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="2be50-185">a.</span><span class="sxs-lookup"><span data-stu-id="2be50-185">a.</span></span> <span data-ttu-id="2be50-186">Bonjour **nom** zone de texte, tapez un nom pour votre configuration.</span><span class="sxs-lookup"><span data-stu-id="2be50-186">In hello **Name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="2be50-187">b.</span><span class="sxs-lookup"><span data-stu-id="2be50-187">b.</span></span> <span data-ttu-id="2be50-188">Dans **émetteur** zone de texte, valeur hello coller **ID d’entité SAML**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2be50-188">In **Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="2be50-189">c.</span><span class="sxs-lookup"><span data-stu-id="2be50-189">c.</span></span> <span data-ttu-id="2be50-190">Bonjour **Id d’entité** zone de texte, type`https://salesforce-jobscience.com`</span><span class="sxs-lookup"><span data-stu-id="2be50-190">In hello **Entity Id** textbox, type `https://salesforce-jobscience.com`</span></span>

    <span data-ttu-id="2be50-191">d.</span><span class="sxs-lookup"><span data-stu-id="2be50-191">d.</span></span> <span data-ttu-id="2be50-192">Cliquez sur **Parcourir** tooupload votre certificat Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2be50-192">Click **Browse** tooupload your Azure AD certificate.</span></span>

    <span data-ttu-id="2be50-193">e.</span><span class="sxs-lookup"><span data-stu-id="2be50-193">e.</span></span> <span data-ttu-id="2be50-194">En tant que **SAML Identity Type**, sélectionnez **Assertion contient hello ID de fédération à partir de l’objet utilisateur de hello**.</span><span class="sxs-lookup"><span data-stu-id="2be50-194">As **SAML Identity Type**, select **Assertion contains hello Federation ID from hello User object**.</span></span>

    <span data-ttu-id="2be50-195">f.</span><span class="sxs-lookup"><span data-stu-id="2be50-195">f.</span></span> <span data-ttu-id="2be50-196">En tant que **emplacement d’identité SAML**, sélectionnez **identité figure dans l’élément NameIdentifier de hello Hello Subject statement**.</span><span class="sxs-lookup"><span data-stu-id="2be50-196">As **SAML Identity Location**, select **Identity is in hello NameIdentfier element of hello Subject statement**.</span></span>

    <span data-ttu-id="2be50-197">g.</span><span class="sxs-lookup"><span data-stu-id="2be50-197">g.</span></span> <span data-ttu-id="2be50-198">Dans **Identity Provider Login URL** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2be50-198">In **Identity Provider Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="2be50-199">h.</span><span class="sxs-lookup"><span data-stu-id="2be50-199">h.</span></span> <span data-ttu-id="2be50-200">Dans **Identity Provider Logout URL** zone de texte, valeur hello coller **URL de déconnexion**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2be50-200">In **Identity Provider Logout URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="2be50-201">i.</span><span class="sxs-lookup"><span data-stu-id="2be50-201">i.</span></span> <span data-ttu-id="2be50-202">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="2be50-202">Click **Save**.</span></span>

14. <span data-ttu-id="2be50-203">Dans le volet de navigation gauche hello Bonjour **administrer** , cliquez sur **gestion des domaines** tooexpand hello section associée, puis cliquez sur **mon domaine** tooopen hello  **Mon domaine** page.</span><span class="sxs-lookup"><span data-stu-id="2be50-203">On hello left navigation pane, in hello **Administer** section, click **Domain Management** tooexpand hello related section, and then click **My Domain** tooopen hello **My Domain** page.</span></span> 
    
    <span data-ttu-id="2be50-204">![Mon domaine](./media/active-directory-saas-jobscience-tutorial/ic767825.png "mon domaine")</span><span class="sxs-lookup"><span data-stu-id="2be50-204">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span></span>

15. <span data-ttu-id="2be50-205">Sur hello **mon domaine** page hello **Login Page Branding** , cliquez sur **modifier**.</span><span class="sxs-lookup"><span data-stu-id="2be50-205">On hello **My Domain** page, in hello **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="2be50-206">![Personnalisation de la page de connexion](./media/active-directory-saas-jobscience-tutorial/ic767826.png "personnalisation de la page de connexion")</span><span class="sxs-lookup"><span data-stu-id="2be50-206">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic767826.png "Login Page Branding")</span></span>

16. <span data-ttu-id="2be50-207">Sur hello **Login Page Branding** page hello **Service d’authentification** section et le nom hello votre **SAML SSO Settings** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="2be50-207">On hello **Login Page Branding** page, in hello **Authentication Service** section, hello name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="2be50-208">Sélectionnez-le, puis cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="2be50-208">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="2be50-209">![Personnalisation de la page de connexion](./media/active-directory-saas-jobscience-tutorial/ic784366.png "personnalisation de la page de connexion")</span><span class="sxs-lookup"><span data-stu-id="2be50-209">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic784366.png "Login Page Branding")</span></span>

17. <span data-ttu-id="2be50-210">tooget hello SP initiée par l’authentification unique de, cliquez sur l’URL de connexion sur hello **Single Sign On paramètres** Bonjour **des contrôles de sécurité** section de menu.</span><span class="sxs-lookup"><span data-stu-id="2be50-210">tooget hello SP initiated Single Sign on Login URL click on hello **Single Sign On settings** in hello **Security Controls** menu section.</span></span>

    <span data-ttu-id="2be50-211">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784368.png "Security Controls")</span><span class="sxs-lookup"><span data-stu-id="2be50-211">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784368.png "Security Controls")</span></span>
    
    <span data-ttu-id="2be50-212">Cliquez sur le profil d’authentification unique hello que vous avez créé à l’étape hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="2be50-212">Click hello SSO profile you have created in hello step above.</span></span> <span data-ttu-id="2be50-213">Cette page affiche hello l’authentification unique sur l’URL de votre société (par exemple, [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).</span><span class="sxs-lookup"><span data-stu-id="2be50-213">This page shows hello Single Sign on URL for your company (for example, [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).</span></span>    

> [!TIP]
> <span data-ttu-id="2be50-214">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="2be50-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2be50-215">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="2be50-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2be50-216">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2be50-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2be50-217">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="2be50-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="2be50-218">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="2be50-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="2be50-220">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2be50-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2be50-221">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="2be50-221">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2be50-223">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="2be50-223">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2be50-225">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="2be50-225">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2be50-227">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="2be50-227">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2be50-229">a.</span><span class="sxs-lookup"><span data-stu-id="2be50-229">a.</span></span> <span data-ttu-id="2be50-230">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2be50-230">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2be50-231">b.</span><span class="sxs-lookup"><span data-stu-id="2be50-231">b.</span></span> <span data-ttu-id="2be50-232">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2be50-232">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2be50-233">c.</span><span class="sxs-lookup"><span data-stu-id="2be50-233">c.</span></span> <span data-ttu-id="2be50-234">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="2be50-234">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2be50-235">d.</span><span class="sxs-lookup"><span data-stu-id="2be50-235">d.</span></span> <span data-ttu-id="2be50-236">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="2be50-236">Click **Create**.</span></span>
 
### <a name="creating-a-jobscience-test-user"></a><span data-ttu-id="2be50-237">Création d’un utilisateur de test Jobscience</span><span class="sxs-lookup"><span data-stu-id="2be50-237">Creating a Jobscience test user</span></span>

<span data-ttu-id="2be50-238">Dans l’ordre tooenable Azure AD les utilisateurs toolog dans tooJobscience, vous devez les configurer dans Jobscience.</span><span class="sxs-lookup"><span data-stu-id="2be50-238">In order tooenable Azure AD users toolog in tooJobscience, they must be provisioned into Jobscience.</span></span> <span data-ttu-id="2be50-239">Dans les cas de hello de Jobscience, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="2be50-239">In hello case of Jobscience, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="2be50-240">Vous pouvez utiliser n’importe quel autre occurrence utilisateur compte outil de création ou API fournie par Jobscience tooprovision Azure Active Directory des comptes d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2be50-240">You can use any other Jobscience user account creation tools or APIs provided by Jobscience tooprovision Azure Active Directory user accounts.</span></span>
>  
        
<span data-ttu-id="2be50-241">**configuration, de l’utilisateur tooconfigure effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2be50-241">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="2be50-242">Connectez-vous à tooyour **Jobscience** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="2be50-242">Log in tooyour **Jobscience** company site as administrator.</span></span>

2. <span data-ttu-id="2be50-243">Accédez à tooSetup.</span><span class="sxs-lookup"><span data-stu-id="2be50-243">Go tooSetup.</span></span>
   
   <span data-ttu-id="2be50-244">![Configuration](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Configuration")</span><span class="sxs-lookup"><span data-stu-id="2be50-244">![Setup](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Setup")</span></span>
3. <span data-ttu-id="2be50-245">Accédez trop**gérer les utilisateurs \> utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="2be50-245">Go too**Manage Users \> Users**.</span></span>
   
   <span data-ttu-id="2be50-246">![Utilisateurs](./media/active-directory-saas-jobscience-tutorial/ic784369.png "Utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="2be50-246">![Users](./media/active-directory-saas-jobscience-tutorial/ic784369.png "Users")</span></span>
4. <span data-ttu-id="2be50-247">Cliquez sur **New User**.</span><span class="sxs-lookup"><span data-stu-id="2be50-247">Click **New User**.</span></span>
   
   <span data-ttu-id="2be50-248">![Tous les utilisateurs](./media/active-directory-saas-jobscience-tutorial/ic784370.png "Tous les utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="2be50-248">![All Users](./media/active-directory-saas-jobscience-tutorial/ic784370.png "All Users")</span></span>
5. <span data-ttu-id="2be50-249">Sur hello **modifier un utilisateur** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="2be50-249">On hello **Edit User** dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="2be50-250">![Modification de l’utilisateur](./media/active-directory-saas-jobscience-tutorial/ic784371.png "modification de l’utilisateur")</span><span class="sxs-lookup"><span data-stu-id="2be50-250">![User Edit](./media/active-directory-saas-jobscience-tutorial/ic784371.png "User Edit")</span></span>
   
   <span data-ttu-id="2be50-251">a.</span><span class="sxs-lookup"><span data-stu-id="2be50-251">a.</span></span> <span data-ttu-id="2be50-252">Bonjour **prénom** zone de texte, tapez un prénom de l’utilisateur hello comme Brian.</span><span class="sxs-lookup"><span data-stu-id="2be50-252">In hello **First Name** textbox, type a first name of hello user like Britta.</span></span>
   
   <span data-ttu-id="2be50-253">b.</span><span class="sxs-lookup"><span data-stu-id="2be50-253">b.</span></span> <span data-ttu-id="2be50-254">Bonjour **nom** zone de texte, tapez un nom d’utilisateur hello comme Simon.</span><span class="sxs-lookup"><span data-stu-id="2be50-254">In hello **Last Name** textbox, type a last name of hello user like Simon.</span></span>
   
   <span data-ttu-id="2be50-255">c.</span><span class="sxs-lookup"><span data-stu-id="2be50-255">c.</span></span> <span data-ttu-id="2be50-256">Bonjour **Alias** zone de texte, tapez un nom d’alias d’utilisateur hello comme brittas.</span><span class="sxs-lookup"><span data-stu-id="2be50-256">In hello **Alias** textbox, type an alias name of hello user like brittas.</span></span>

   <span data-ttu-id="2be50-257">d.</span><span class="sxs-lookup"><span data-stu-id="2be50-257">d.</span></span> <span data-ttu-id="2be50-258">Bonjour **messagerie** adresse de messagerie de type hello d’utilisateur de zone de texte, comme Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="2be50-258">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="2be50-259">e.</span><span class="sxs-lookup"><span data-stu-id="2be50-259">e.</span></span> <span data-ttu-id="2be50-260">Bonjour **nom d’utilisateur** zone de texte, tapez un nom d’utilisateur de l’utilisateur comme Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="2be50-260">In hello **User Name** textbox, type a user name of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="2be50-261">f.</span><span class="sxs-lookup"><span data-stu-id="2be50-261">f.</span></span> <span data-ttu-id="2be50-262">Bonjour **surnom** zone de texte, tapez le nom d’utilisateur comme Simon nick.</span><span class="sxs-lookup"><span data-stu-id="2be50-262">In hello **Nick Name** textbox, type a nick name of user like Simon.</span></span>

   <span data-ttu-id="2be50-263">g.</span><span class="sxs-lookup"><span data-stu-id="2be50-263">g.</span></span> <span data-ttu-id="2be50-264">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="2be50-264">Click **Save**.</span></span>

    
> [!NOTE]
> <span data-ttu-id="2be50-265">titulaire du compte Azure Active Directory Hello reçoit un message électronique et suit un tooconfirm de lier leur compte avant son activation.</span><span class="sxs-lookup"><span data-stu-id="2be50-265">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2be50-266">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2be50-266">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2be50-267">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooJobscience.</span><span class="sxs-lookup"><span data-stu-id="2be50-267">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJobscience.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="2be50-269">**tooassign Britta Simon tooJobscience, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2be50-269">**tooassign Britta Simon tooJobscience, perform hello following steps:**</span></span>

1. <span data-ttu-id="2be50-270">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="2be50-270">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="2be50-272">Dans la liste des applications hello, sélectionnez **Jobscience**.</span><span class="sxs-lookup"><span data-stu-id="2be50-272">In hello applications list, select **Jobscience**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_app.png) 

3. <span data-ttu-id="2be50-274">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="2be50-274">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="2be50-276">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="2be50-276">Click **Add** button.</span></span> <span data-ttu-id="2be50-277">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="2be50-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="2be50-279">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="2be50-279">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2be50-280">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="2be50-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2be50-281">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="2be50-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2be50-282">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="2be50-282">Testing single sign-on</span></span>

<span data-ttu-id="2be50-283">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="2be50-283">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2be50-284">Lorsque vous cliquez sur mosaïque de Jobscience hello Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour Jobscience application.</span><span class="sxs-lookup"><span data-stu-id="2be50-284">When you click hello Jobscience tile in hello Access Panel, you should get automatically signed-on tooyour Jobscience application.</span></span>
<span data-ttu-id="2be50-285">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2be50-285">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2be50-286">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="2be50-286">Additional resources</span></span>

* [<span data-ttu-id="2be50-287">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2be50-287">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2be50-288">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="2be50-288">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_203.png

