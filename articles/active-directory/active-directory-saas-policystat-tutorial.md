---
title: "Didacticiel : Intégration d’Azure Active Directory avec PolicyStat | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et PolicyStat."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: af5eb0f1-1c8e-4809-b0c4-8ccfb915ca42
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 868053cd0d37359fd9b4aeb93dba42cbbaa09845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-policystat"></a><span data-ttu-id="91835-103">Didacticiel : Intégration d’Azure Active Directory avec PolicyStat</span><span class="sxs-lookup"><span data-stu-id="91835-103">Tutorial: Azure Active Directory integration with PolicyStat</span></span>

<span data-ttu-id="91835-104">Dans ce didacticiel, vous apprendrez comment toointegrate PolicyStat avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="91835-104">In this tutorial, you learn how toointegrate PolicyStat with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="91835-105">Intégration PolicyStat à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="91835-105">Integrating PolicyStat with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="91835-106">Vous pouvez contrôler dans Azure AD qui a accès tooPolicyStat</span><span class="sxs-lookup"><span data-stu-id="91835-106">You can control in Azure AD who has access tooPolicyStat</span></span>
- <span data-ttu-id="91835-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooPolicyStat (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="91835-107">You can enable your users tooautomatically get signed-on tooPolicyStat (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="91835-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="91835-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="91835-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="91835-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91835-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="91835-110">Prerequisites</span></span>

<span data-ttu-id="91835-111">tooconfigure intégration d’Azure AD avec PolicyStat, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="91835-111">tooconfigure Azure AD integration with PolicyStat, you need hello following items:</span></span>

- <span data-ttu-id="91835-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="91835-112">An Azure AD subscription</span></span>
- <span data-ttu-id="91835-113">Un abonnement PolicyStat pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="91835-113">A PolicyStat single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="91835-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="91835-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="91835-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="91835-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="91835-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="91835-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="91835-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="91835-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="91835-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="91835-118">Scenario description</span></span>
<span data-ttu-id="91835-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="91835-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="91835-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="91835-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="91835-121">Ajout de PolicyStat à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="91835-121">Adding PolicyStat from hello gallery</span></span>
2. <span data-ttu-id="91835-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="91835-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-policystat-from-hello-gallery"></a><span data-ttu-id="91835-123">Ajout de PolicyStat à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="91835-123">Adding PolicyStat from hello gallery</span></span>
<span data-ttu-id="91835-124">intégration de hello tooconfigure de PolicyStat dans Azure AD, vous devez tooadd PolicyStat à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="91835-124">tooconfigure hello integration of PolicyStat into Azure AD, you need tooadd PolicyStat from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="91835-125">**tooadd PolicyStat à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="91835-125">**tooadd PolicyStat from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="91835-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="91835-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="91835-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="91835-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="91835-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="91835-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="91835-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="91835-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="91835-133">Dans la zone de recherche de hello, tapez **PolicyStat**.</span><span class="sxs-lookup"><span data-stu-id="91835-133">In hello search box, type **PolicyStat**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_search.png)

5. <span data-ttu-id="91835-135">Dans le volet de résultats hello, sélectionnez **PolicyStat**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="91835-135">In hello results panel, select **PolicyStat**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="91835-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="91835-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="91835-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec PolicyStat sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="91835-138">In this section, you configure and test Azure AD single sign-on with PolicyStat based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="91835-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans PolicyStat est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="91835-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PolicyStat is tooa user in Azure AD.</span></span> <span data-ttu-id="91835-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans PolicyStat doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="91835-140">In other words, a link relationship between an Azure AD user and hello related user in PolicyStat needs toobe established.</span></span>

<span data-ttu-id="91835-141">Dans PolicyStat, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="91835-141">In PolicyStat, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="91835-142">tooconfigure et test Azure AD l’authentification unique avec PolicyStat, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="91835-142">tooconfigure and test Azure AD single sign-on with PolicyStat, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="91835-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="91835-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="91835-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="91835-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="91835-145">**[Création d’un utilisateur de test PolicyStat](#creating-a-policystat-test-user)**  -toohave un équivalent de Britta Simon dans PolicyStat est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="91835-145">**[Creating a PolicyStat test user](#creating-a-policystat-test-user)** - toohave a counterpart of Britta Simon in PolicyStat that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="91835-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="91835-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="91835-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="91835-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="91835-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="91835-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="91835-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="91835-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your PolicyStat application.</span></span>

<span data-ttu-id="91835-150">**tooconfigure Azure AD single sign-on avec PolicyStat, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="91835-150">**tooconfigure Azure AD single sign-on with PolicyStat, perform hello following steps:**</span></span>

1. <span data-ttu-id="91835-151">Bonjour portail Azure, sur hello **PolicyStat** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="91835-151">In hello Azure portal, on hello **PolicyStat** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="91835-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="91835-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_samlbase.png)

3. <span data-ttu-id="91835-155">Sur hello **PolicyStat domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="91835-155">On hello **PolicyStat Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_url.png)

    <span data-ttu-id="91835-157">a.</span><span class="sxs-lookup"><span data-stu-id="91835-157">a.</span></span> <span data-ttu-id="91835-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.policystat.com`</span><span class="sxs-lookup"><span data-stu-id="91835-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.policystat.com`</span></span>

    <span data-ttu-id="91835-159">b.</span><span class="sxs-lookup"><span data-stu-id="91835-159">b.</span></span> <span data-ttu-id="91835-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.policystat.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="91835-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.policystat.com/saml2/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="91835-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="91835-161">These values are not real.</span></span> <span data-ttu-id="91835-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="91835-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="91835-163">Contact [équipe de support Client de PolicyStat](http://www.policystat.com/support/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="91835-163">Contact [PolicyStat Client support team](http://www.policystat.com/support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="91835-164">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="91835-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_certificate.png) 

5. <span data-ttu-id="91835-166">objectif Hello de cette section est toooutline comment tooenable utilisateurs tooauthenticate tooPolicyStat avec leur compte dans Azure AD en utilisant la fédération basée sur le protocole SAML de hello.</span><span class="sxs-lookup"><span data-stu-id="91835-166">hello objective of this section is toooutline how tooenable users tooauthenticate tooPolicyStat with their account in Azure AD using federation based on hello SAML protocol.</span></span>

    <span data-ttu-id="91835-167">Hello PolicyStat application attend les assertions SAML hello dans un format spécifique, ce qui vous oblige à tooyour de mappages d’attributs personnalisés tooadd **attributs du jeton SAML** configuration.</span><span class="sxs-lookup"><span data-stu-id="91835-167">hello PolicyStat application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **SAML Token Attributes** configuration.</span></span>  

     <span data-ttu-id="91835-168">Hello suivant capture d’écran montre un exemple de cela.</span><span class="sxs-lookup"><span data-stu-id="91835-168">hello following screenshot shows an example of this.</span></span>

     <span data-ttu-id="91835-169">![Attributs](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "Attributs")</span><span class="sxs-lookup"><span data-stu-id="91835-169">![Attributes](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "Attributes")</span></span>

6. <span data-ttu-id="91835-170">mappages d’attributs tooadd hello requis, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="91835-170">tooadd hello required attribute mappings, perform hello following steps:</span></span>

    | <span data-ttu-id="91835-171">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="91835-171">Attribute Name</span></span>    |   <span data-ttu-id="91835-172">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="91835-172">Attribute Value</span></span> |
    |------------------- | -------------------- |
    | <span data-ttu-id="91835-173">uid</span><span class="sxs-lookup"><span data-stu-id="91835-173">uid</span></span> | <span data-ttu-id="91835-174">ExtractMailPrefix([mail])</span><span class="sxs-lookup"><span data-stu-id="91835-174">ExtractMailPrefix([mail])</span></span> |
    
    <span data-ttu-id="91835-175">a.</span><span class="sxs-lookup"><span data-stu-id="91835-175">a.</span></span> <span data-ttu-id="91835-176">Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="91835-176">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addatribute.png)
    
    <span data-ttu-id="91835-179">b.</span><span class="sxs-lookup"><span data-stu-id="91835-179">b.</span></span> <span data-ttu-id="91835-180">Bonjour **nom de l’attribut** zone de texte, type **uid**.</span><span class="sxs-lookup"><span data-stu-id="91835-180">In hello **Attribute Name** textbox, type **uid**.</span></span>

    <span data-ttu-id="91835-181">c.</span><span class="sxs-lookup"><span data-stu-id="91835-181">c.</span></span> <span data-ttu-id="91835-182">Bonjour **valeur d’attribut** zone de texte, sélectionnez **ExtractMailPrefix()**.</span><span class="sxs-lookup"><span data-stu-id="91835-182">In hello **Attribute Value** textbox, select **ExtractMailPrefix()**.</span></span>    
   
    <span data-ttu-id="91835-183">d.</span><span class="sxs-lookup"><span data-stu-id="91835-183">d.</span></span> <span data-ttu-id="91835-184">À partir de hello **Mail** liste, sélectionnez **User.mail**.</span><span class="sxs-lookup"><span data-stu-id="91835-184">From hello **Mail** list, select **User.mail**.</span></span>
    
    <span data-ttu-id="91835-185">e.</span><span class="sxs-lookup"><span data-stu-id="91835-185">e.</span></span> <span data-ttu-id="91835-186">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="91835-186">Click **Ok**</span></span>

7. <span data-ttu-id="91835-187">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="91835-187">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-policystat-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="91835-189">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise PolicyStat en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="91835-189">In a different web browser window, log into your PolicyStat company site as an administrator.</span></span>

9. <span data-ttu-id="91835-190">Cliquez sur hello **Admin** onglet, puis cliquez sur **Configuration de l’authentification unique** dans le volet de navigation gauche.</span><span class="sxs-lookup"><span data-stu-id="91835-190">Click hello **Admin** tab, and then click **Single Sign-On Configuration** in left navigation pane.</span></span>
   
    <span data-ttu-id="91835-191">![Menu administrateur](./media/active-directory-saas-policystat-tutorial/ic808633.png "Menu administrateur")</span><span class="sxs-lookup"><span data-stu-id="91835-191">![Administrator Menu](./media/active-directory-saas-policystat-tutorial/ic808633.png "Administrator Menu")</span></span>

10. <span data-ttu-id="91835-192">Bonjour **le programme d’installation** section, sélectionnez **activer l’authentification intégration de l’unique**.</span><span class="sxs-lookup"><span data-stu-id="91835-192">In hello **Setup** section, select **Enable Single Sign-on Integration**.</span></span>
   
    <span data-ttu-id="91835-193">![Configuration de l’authentification unique](./media/active-directory-saas-policystat-tutorial/ic808634.png "Configuration de l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="91835-193">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808634.png "Single Sign-On Configuration")</span></span>

11. <span data-ttu-id="91835-194">Cliquez sur **configurer les attributs**, puis, dans hello **configurer les attributs** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="91835-194">Click **Configure Attributes**, and then, in hello **Configure Attributes** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="91835-195">![Configuration de l’authentification unique](./media/active-directory-saas-policystat-tutorial/ic808635.png "Configuration de l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="91835-195">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808635.png "Single Sign-On Configuration")</span></span>
   
    <span data-ttu-id="91835-196">a.</span><span class="sxs-lookup"><span data-stu-id="91835-196">a.</span></span> <span data-ttu-id="91835-197">Bonjour **attribut Username** zone de texte, type **uid**.</span><span class="sxs-lookup"><span data-stu-id="91835-197">In hello **Username Attribute** textbox, type **uid**.</span></span>

    <span data-ttu-id="91835-198">b.</span><span class="sxs-lookup"><span data-stu-id="91835-198">b.</span></span> <span data-ttu-id="91835-199">Bonjour **prénom attribut** zone de texte, type **firstname** d’utilisateur **Brian**.</span><span class="sxs-lookup"><span data-stu-id="91835-199">In hello **First Name Attribute** textbox, type **firstname** of user **Britta**.</span></span>

    <span data-ttu-id="91835-200">c.</span><span class="sxs-lookup"><span data-stu-id="91835-200">c.</span></span> <span data-ttu-id="91835-201">Bonjour **attribut de nom** zone de texte, type **lastname** d’utilisateur **Simon**.</span><span class="sxs-lookup"><span data-stu-id="91835-201">In hello **Last Name Attribute** textbox, type **lastname** of user **Simon**.</span></span>

    <span data-ttu-id="91835-202">d.</span><span class="sxs-lookup"><span data-stu-id="91835-202">d.</span></span> <span data-ttu-id="91835-203">Bonjour **attribut Email** zone de texte, type **emailaddress** d’utilisateur  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="91835-203">In hello **Email Attribute** textbox, type **emailaddress** of user **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="91835-204">e.</span><span class="sxs-lookup"><span data-stu-id="91835-204">e.</span></span> <span data-ttu-id="91835-205">Cliquez sur **Enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="91835-205">Click **Save Changes**.</span></span>

12. <span data-ttu-id="91835-206">Cliquez sur **votre IDP Metadata**, puis, dans hello **votre IDP Metadata** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="91835-206">Click **Your IDP Metadata**, and then, in hello **Your IDP Metadata** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="91835-207">![Configuration de l’authentification unique](./media/active-directory-saas-policystat-tutorial/ic808636.png "Configuration de l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="91835-207">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808636.png "Single Sign-On Configuration")</span></span>
   
    <span data-ttu-id="91835-208">a.</span><span class="sxs-lookup"><span data-stu-id="91835-208">a.</span></span> <span data-ttu-id="91835-209">Ouvrez votre fichier de métadonnées téléchargé, les hello copie contenu, puis collez-le dans hello **vos métadonnées du fournisseur d’identité** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="91835-209">Open your downloaded metadata file, copy hello content, and  then paste it into hello **Your Identity Provider Metadata** textbox.</span></span>

    <span data-ttu-id="91835-210">b.</span><span class="sxs-lookup"><span data-stu-id="91835-210">b.</span></span> <span data-ttu-id="91835-211">Cliquez sur **Enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="91835-211">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="91835-212">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="91835-212">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="91835-213">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="91835-213">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="91835-214">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="91835-214">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="91835-215">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="91835-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="91835-216">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="91835-216">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="91835-218">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="91835-218">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="91835-219">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="91835-219">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="91835-221">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="91835-221">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="91835-223">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="91835-223">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="91835-225">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="91835-225">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="91835-227">a.</span><span class="sxs-lookup"><span data-stu-id="91835-227">a.</span></span> <span data-ttu-id="91835-228">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="91835-228">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="91835-229">b.</span><span class="sxs-lookup"><span data-stu-id="91835-229">b.</span></span> <span data-ttu-id="91835-230">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="91835-230">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="91835-231">c.</span><span class="sxs-lookup"><span data-stu-id="91835-231">c.</span></span> <span data-ttu-id="91835-232">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="91835-232">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="91835-233">d.</span><span class="sxs-lookup"><span data-stu-id="91835-233">d.</span></span> <span data-ttu-id="91835-234">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="91835-234">Click **Create**.</span></span>
 
### <a name="creating-a-policystat-test-user"></a><span data-ttu-id="91835-235">Création d’un utilisateur de test PolicyStat</span><span class="sxs-lookup"><span data-stu-id="91835-235">Creating a PolicyStat test user</span></span>

<span data-ttu-id="91835-236">Dans l’ordre tooenable Azure AD les utilisateurs toolog dans PolicyStat, ils doivent être configurés dans PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="91835-236">In order tooenable Azure AD users toolog into PolicyStat, they must be provisioned into PolicyStat.</span></span>  

<span data-ttu-id="91835-237">PolicyStat prend en charge l’approvisionnement juste-à-temps des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="91835-237">PolicyStat supports just in time user provisioning.</span></span> <span data-ttu-id="91835-238">Cela signifie, vous ne devez pas manuellement les utilisateurs de hello tooadd tooPolicyStat.</span><span class="sxs-lookup"><span data-stu-id="91835-238">This means, you do not need tooadd hello users manually tooPolicyStat.</span></span> <span data-ttu-id="91835-239">les utilisateurs de Hello seront ajoutés automatiquement lors de leur première connexion via l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="91835-239">hello users will get added automatically on their first login through SSO.</span></span>

>[!NOTE]
><span data-ttu-id="91835-240">Vous pouvez utiliser n’importe quel autre PolicyStat utilisateur compte outil de création ou API fournie par PolicyStat tooprovision comptes d’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="91835-240">You can use any other PolicyStat user account creation tools or APIs provided by PolicyStat tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="91835-241">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="91835-241">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="91835-242">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooPolicyStat.</span><span class="sxs-lookup"><span data-stu-id="91835-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPolicyStat.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="91835-244">**tooassign Britta Simon tooPolicyStat, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="91835-244">**tooassign Britta Simon tooPolicyStat, perform hello following steps:**</span></span>

1. <span data-ttu-id="91835-245">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="91835-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="91835-247">Dans la liste des applications hello, sélectionnez **PolicyStat**.</span><span class="sxs-lookup"><span data-stu-id="91835-247">In hello applications list, select **PolicyStat**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_app.png) 

3. <span data-ttu-id="91835-249">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="91835-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="91835-251">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="91835-251">Click **Add** button.</span></span> <span data-ttu-id="91835-252">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="91835-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="91835-254">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="91835-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="91835-255">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="91835-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="91835-256">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="91835-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="91835-257">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="91835-257">Testing single sign-on</span></span>

<span data-ttu-id="91835-258">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="91835-258">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="91835-259">Lorsque vous cliquez sur mosaïque PolicyStat hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour PolicyStat application.</span><span class="sxs-lookup"><span data-stu-id="91835-259">When you click hello PolicyStat tile in hello Access Panel, you should get automatically signed-on tooyour PolicyStat application.</span></span>
<span data-ttu-id="91835-260">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="91835-260">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="91835-261">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="91835-261">Additional resources</span></span>

* [<span data-ttu-id="91835-262">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="91835-262">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="91835-263">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="91835-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_203.png

