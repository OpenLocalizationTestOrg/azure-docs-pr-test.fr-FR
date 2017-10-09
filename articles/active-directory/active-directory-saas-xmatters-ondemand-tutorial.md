---
title: "Didacticiel : Intégration d’Azure Active Directory à XMatters OnDemand | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de xMatters OnDemand."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ca0633db-4f95-432e-b3db-0168193b5ce9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 7cc8f9f0d8cefc8a60b9514027437ced50c66242
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-xmatters-ondemand"></a><span data-ttu-id="31a83-103">Didacticiel : Intégration d’Azure Active Directory à xMatters OnDemand</span><span class="sxs-lookup"><span data-stu-id="31a83-103">Tutorial: Azure Active Directory integration with xMatters OnDemand</span></span>

<span data-ttu-id="31a83-104">Dans ce didacticiel, vous apprendrez comment toointegrate xMatters OnDemand avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="31a83-104">In this tutorial, you learn how toointegrate xMatters OnDemand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="31a83-105">Intégration de xMatters OnDemand à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="31a83-105">Integrating xMatters OnDemand with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="31a83-106">Vous pouvez contrôler dans Azure AD qui a tooxMatters d’accès à la demande</span><span class="sxs-lookup"><span data-stu-id="31a83-106">You can control in Azure AD who has access tooxMatters OnDemand</span></span>
- <span data-ttu-id="31a83-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooxMatters OnDemand (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="31a83-107">You can enable your users tooautomatically get signed-on tooxMatters OnDemand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="31a83-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="31a83-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="31a83-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="31a83-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31a83-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="31a83-110">Prerequisites</span></span>

<span data-ttu-id="31a83-111">tooconfigure intégration d’Azure AD à xMatters OnDemand, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="31a83-111">tooconfigure Azure AD integration with xMatters OnDemand, you need hello following items:</span></span>

- <span data-ttu-id="31a83-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="31a83-112">An Azure AD subscription</span></span>
- <span data-ttu-id="31a83-113">Un abonnement xMatters OnDemand pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="31a83-113">A xMatters OnDemand single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="31a83-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="31a83-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="31a83-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="31a83-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="31a83-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="31a83-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="31a83-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="31a83-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="31a83-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="31a83-118">Scenario description</span></span>
<span data-ttu-id="31a83-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="31a83-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="31a83-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="31a83-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="31a83-121">Ajout de xMatters OnDemand à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="31a83-121">Adding xMatters OnDemand from hello gallery</span></span>
2. <span data-ttu-id="31a83-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="31a83-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-xmatters-ondemand-from-hello-gallery"></a><span data-ttu-id="31a83-123">Ajout de xMatters OnDemand à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="31a83-123">Adding xMatters OnDemand from hello gallery</span></span>
<span data-ttu-id="31a83-124">intégration de hello tooconfigure de xMatters OnDemand dans Azure AD, vous devez tooadd xMatters OnDemand à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="31a83-124">tooconfigure hello integration of xMatters OnDemand into Azure AD, you need tooadd xMatters OnDemand from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="31a83-125">**tooadd xMatters OnDemand à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="31a83-125">**tooadd xMatters OnDemand from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="31a83-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="31a83-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="31a83-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="31a83-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="31a83-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="31a83-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="31a83-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="31a83-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="31a83-133">Dans la zone de recherche de hello, tapez **xMatters OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="31a83-133">In hello search box, type **xMatters OnDemand**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_search.png)

5. <span data-ttu-id="31a83-135">Dans le volet de résultats hello, sélectionnez **xMatters OnDemand**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="31a83-135">In hello results panel, select **xMatters OnDemand**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="31a83-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="31a83-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="31a83-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec xMatters OnDemand avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="31a83-138">In this section, you configure and test Azure AD single sign-on with xMatters OnDemand based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="31a83-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel hello utilisateur équivalent dans xMatters OnDemand est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="31a83-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in xMatters OnDemand is tooa user in Azure AD.</span></span> <span data-ttu-id="31a83-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans xMatters OnDemand doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="31a83-140">In other words, a link relationship between an Azure AD user and hello related user in xMatters OnDemand needs toobe established.</span></span>

<span data-ttu-id="31a83-141">Dans xMatters OnDemand, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="31a83-141">In xMatters OnDemand, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="31a83-142">tooconfigure et test Azure AD l’authentification unique à xMatters OnDemand, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="31a83-142">tooconfigure and test Azure AD single sign-on with xMatters OnDemand, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="31a83-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="31a83-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="31a83-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="31a83-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="31a83-145">**[Création d’un utilisateur de test de xMatters OnDemand](#creating-a-xmatters-ondemand-test-user)**  -toohave un homologue de Britta Simon dans xMatters OnDemand est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="31a83-145">**[Creating a xMatters OnDemand test user](#creating-a-xmatters-ondemand-test-user)** - toohave a counterpart of Britta Simon in xMatters OnDemand that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="31a83-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="31a83-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="31a83-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="31a83-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="31a83-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="31a83-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="31a83-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre xMatters OnDemand application.</span><span class="sxs-lookup"><span data-stu-id="31a83-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your xMatters OnDemand application.</span></span>

<span data-ttu-id="31a83-150">**tooconfigure Azure AD single sign-on avec xMatters OnDemand, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="31a83-150">**tooconfigure Azure AD single sign-on with xMatters OnDemand, perform hello following steps:**</span></span>

1. <span data-ttu-id="31a83-151">Bonjour portail Azure, sur hello **xMatters OnDemand** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="31a83-151">In hello Azure portal, on hello **xMatters OnDemand** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="31a83-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="31a83-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_samlbase.png)

3. <span data-ttu-id="31a83-155">Sur hello **xMatters OnDemand domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="31a83-155">On hello **xMatters OnDemand Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_url.png)
    
    <span data-ttu-id="31a83-157">a.</span><span class="sxs-lookup"><span data-stu-id="31a83-157">a.</span></span> <span data-ttu-id="31a83-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :</span><span class="sxs-lookup"><span data-stu-id="31a83-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>   
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au/`|
    | `https://<companyname>.cs1.xmatters.com/`|
    | `https://<companyname>.xmatters.com/`|
    | `https://www.xmatters.com`|
    | `https://<companyname>.xmatters.com.au/`|

    <span data-ttu-id="31a83-159">b.</span><span class="sxs-lookup"><span data-stu-id="31a83-159">b.</span></span> <span data-ttu-id="31a83-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :</span><span class="sxs-lookup"><span data-stu-id="31a83-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au`|
    | `https://<companyname>.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.cs1.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.au1.xmatters.com.au/<instancename>`|

    > [!NOTE] 
    > <span data-ttu-id="31a83-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="31a83-161">These values are not real.</span></span> <span data-ttu-id="31a83-162">Mettre à jour ces valeurs hello URL d’identificateur et de réponse réelle.</span><span class="sxs-lookup"><span data-stu-id="31a83-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="31a83-163">Contact [équipe de support technique xMatters OnDemand](https://www.xmatters.com/company/contact-us/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="31a83-163">Contact [xMatters OnDemand support team](https://www.xmatters.com/company/contact-us/) tooget these values.</span></span>

4. <span data-ttu-id="31a83-164">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier certificat hello localement en tant que **c:\\XMatters OnDemand.cer**.</span><span class="sxs-lookup"><span data-stu-id="31a83-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file locally as **c:\\XMatters OnDemand.cer**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_certificate.png)
    
    > [!IMPORTANT]
    > <span data-ttu-id="31a83-166">Vous devez tooforward hello certificat toohello [équipe de support technique xMatters OnDemand](https://www.xmatters.com/company/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="31a83-166">You need tooforward hello certificate toohello [xMatters OnDemand support team](https://www.xmatters.com/company/contact-us/).</span></span> <span data-ttu-id="31a83-167">certificat de Hello doit toobe téléchargé par l’équipe de support technique xMatters hello que vous puissiez finaliser la configuration de l’authentification unique de l’hello.</span><span class="sxs-lookup"><span data-stu-id="31a83-167">hello certificate needs toobe uploaded by hello xMatters support team before you can finalize hello single sign-on configuration.</span></span> 

5. <span data-ttu-id="31a83-168">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="31a83-168">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="31a83-170">Sur hello **xMatters OnDemand Configuration** , cliquez sur **configurer xMatters OnDemand** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="31a83-170">On hello **xMatters OnDemand Configuration** section, click **Configure xMatters OnDemand** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="31a83-171">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="31a83-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_configure.png) 

7. <span data-ttu-id="31a83-173">Dans une fenêtre de navigateur web, connectez-vous tooyour site de société XMatters OnDemand en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="31a83-173">In a different web browser window, log in tooyour XMatters OnDemand company site as an administrator.</span></span>

8. <span data-ttu-id="31a83-174">Dans la barre d’outils de hello en haut de hello, cliquez sur **Admin**, puis cliquez sur **détails de la société** dans la barre de navigation hello hello côté gauche.</span><span class="sxs-lookup"><span data-stu-id="31a83-174">In hello toolbar on hello top, click **Admin**, and then click **Company Details** in hello navigation bar on hello left side.</span></span>
   
    <span data-ttu-id="31a83-175">![Administrateur](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "Administrateur")</span><span class="sxs-lookup"><span data-stu-id="31a83-175">![Admin](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "Admin")</span></span>

9. <span data-ttu-id="31a83-176">Sur hello **Configuration SAML** page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="31a83-176">On hello **SAML Configuration** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="31a83-177">![Configuration SAML](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "Configuration SAML")</span><span class="sxs-lookup"><span data-stu-id="31a83-177">![SAML configuration](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "SAML configuration")</span></span>
   
    <span data-ttu-id="31a83-178">a.</span><span class="sxs-lookup"><span data-stu-id="31a83-178">a.</span></span> <span data-ttu-id="31a83-179">Sélectionnez **Enable SAML**.</span><span class="sxs-lookup"><span data-stu-id="31a83-179">Select **Enable SAML**.</span></span>
   
    <span data-ttu-id="31a83-180">b.</span><span class="sxs-lookup"><span data-stu-id="31a83-180">b.</span></span> <span data-ttu-id="31a83-181">Coller **ID d’entité SAML**, lequel vous avez copié à partir de hello portail Azure en hello **ID fournisseur d’identité** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="31a83-181">Paste **SAML Entity ID**, which you have copied from hello Azure portal into hello **Identity Provider ID** textbox.</span></span>
   
    <span data-ttu-id="31a83-182">c.</span><span class="sxs-lookup"><span data-stu-id="31a83-182">c.</span></span> <span data-ttu-id="31a83-183">Coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir de hello portail Azure en hello **URL d’authentification unique** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="31a83-183">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **Single Sign On URL** textbox.</span></span>
   
    <span data-ttu-id="31a83-184">d.</span><span class="sxs-lookup"><span data-stu-id="31a83-184">d.</span></span> <span data-ttu-id="31a83-185">Coller **URL de déconnexion**, lequel vous avez copié à partir de hello portail Azure en hello **URL de déconnexion unique** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="31a83-185">Paste **Sign-Out URL**, which you have copied from hello Azure portal into hello **Single Logout URL** textbox.</span></span>
   
    <span data-ttu-id="31a83-186">e.</span><span class="sxs-lookup"><span data-stu-id="31a83-186">e.</span></span> <span data-ttu-id="31a83-187">Dans la page de détails de la société hello, en haut hello, cliquez sur **enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="31a83-187">On hello Company Details page, at hello top, click **Save Changes**.</span></span>
    
    <span data-ttu-id="31a83-188">![Détails sur la société](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "Détails sur la société")</span><span class="sxs-lookup"><span data-stu-id="31a83-188">![Company details](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "Company details")</span></span>

> [!TIP]
> <span data-ttu-id="31a83-189">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="31a83-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="31a83-190">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="31a83-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="31a83-191">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="31a83-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="31a83-192">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="31a83-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="31a83-193">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="31a83-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="31a83-195">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="31a83-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="31a83-196">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="31a83-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="31a83-198">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="31a83-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="31a83-200">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="31a83-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="31a83-202">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="31a83-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="31a83-204">a.</span><span class="sxs-lookup"><span data-stu-id="31a83-204">a.</span></span> <span data-ttu-id="31a83-205">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="31a83-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="31a83-206">b.</span><span class="sxs-lookup"><span data-stu-id="31a83-206">b.</span></span> <span data-ttu-id="31a83-207">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="31a83-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="31a83-208">c.</span><span class="sxs-lookup"><span data-stu-id="31a83-208">c.</span></span> <span data-ttu-id="31a83-209">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="31a83-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="31a83-210">d.</span><span class="sxs-lookup"><span data-stu-id="31a83-210">d.</span></span> <span data-ttu-id="31a83-211">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="31a83-211">Click **Create**.</span></span>
 
### <a name="creating-a-xmatters-ondemand-test-user"></a><span data-ttu-id="31a83-212">Création d’un utilisateur de test xMatters OnDemand</span><span class="sxs-lookup"><span data-stu-id="31a83-212">Creating a xMatters OnDemand test user</span></span>

<span data-ttu-id="31a83-213">Dans l’ordre tooenable Azure AD les utilisateurs toolog dans tooXMatters à la demande, vous devez les configurer dans XMatters OnDemand.</span><span class="sxs-lookup"><span data-stu-id="31a83-213">In order tooenable Azure AD users toolog in tooXMatters OnDemand, they must be provisioned into XMatters OnDemand.</span></span> <span data-ttu-id="31a83-214">Dans les cas de hello de XMatters OnDemand, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="31a83-214">In hello case of XMatters OnDemand, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a><span data-ttu-id="31a83-215">effectuer des comptes d’utilisateur, tooprovision hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="31a83-215">tooprovision a user accounts, perform hello following steps:</span></span>
1. <span data-ttu-id="31a83-216">Connectez-vous à tooyour **XMatters OnDemand** client.</span><span class="sxs-lookup"><span data-stu-id="31a83-216">Log in tooyour **XMatters OnDemand** tenant.</span></span>

2.  <span data-ttu-id="31a83-217">Cliquez sur **utilisateurs** onglet, puis cliquez sur **ajouter un utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="31a83-217">Click **Users** tab. and then click **Add User**.</span></span>
  
    <span data-ttu-id="31a83-218">![Utilisateurs](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "Utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="31a83-218">![Users](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "Users")</span></span>

3. <span data-ttu-id="31a83-219">Bonjour **ajouter un utilisateur** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="31a83-219">In hello **Add a User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="31a83-220">![Ajouter un utilisateur](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "Ajouter un utilisateur")</span><span class="sxs-lookup"><span data-stu-id="31a83-220">![Add a User](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "Add a User")</span></span>

    <span data-ttu-id="31a83-221">a.</span><span class="sxs-lookup"><span data-stu-id="31a83-221">a.</span></span> <span data-ttu-id="31a83-222">Sélectionnez **Active**.</span><span class="sxs-lookup"><span data-stu-id="31a83-222">Select **Active**.</span></span>

    <span data-ttu-id="31a83-223">b.</span><span class="sxs-lookup"><span data-stu-id="31a83-223">b.</span></span> <span data-ttu-id="31a83-224">Bonjour **ID utilisateur** zone de texte, id d’utilisateur comme type hello Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="31a83-224">In hello **User ID** textbox, type hello user id of user like Brittasimon@contoso.com.</span></span>
   
    <span data-ttu-id="31a83-225">c.</span><span class="sxs-lookup"><span data-stu-id="31a83-225">c.</span></span> <span data-ttu-id="31a83-226">Bonjour **prénom** prénom type d’utilisateur hello comme Brian zone de texte.</span><span class="sxs-lookup"><span data-stu-id="31a83-226">In hello **First Name** textbox, type first name of hello user like Britta.</span></span>

    <span data-ttu-id="31a83-227">d.</span><span class="sxs-lookup"><span data-stu-id="31a83-227">d.</span></span> <span data-ttu-id="31a83-228">Bonjour **nom** zone de texte, tapez nom de famille de l’utilisateur hello comme Simon.</span><span class="sxs-lookup"><span data-stu-id="31a83-228">In hello **Last Name** textbox, type last name of hello user like Simon.</span></span>
    
    <span data-ttu-id="31a83-229">e.</span><span class="sxs-lookup"><span data-stu-id="31a83-229">e.</span></span> <span data-ttu-id="31a83-230">Bonjour **Site** zone de texte, site valide de hello entrée d’un Azure valide compte AD tooprovision.</span><span class="sxs-lookup"><span data-stu-id="31a83-230">In hello **Site** textbox, Enter hello valid site of a valid Azure AD account you want tooprovision.</span></span>
    
    <span data-ttu-id="31a83-231">f.</span><span class="sxs-lookup"><span data-stu-id="31a83-231">f.</span></span> <span data-ttu-id="31a83-232">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="31a83-232">Click **Save**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="31a83-233">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="31a83-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="31a83-234">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooxMatters à la demande.</span><span class="sxs-lookup"><span data-stu-id="31a83-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooxMatters OnDemand.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="31a83-236">**tooassign Britta Simon tooxMatters OnDemand, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="31a83-236">**tooassign Britta Simon tooxMatters OnDemand, perform hello following steps:**</span></span>

1. <span data-ttu-id="31a83-237">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="31a83-237">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="31a83-239">Dans la liste des applications hello, sélectionnez **xMatters OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="31a83-239">In hello applications list, select **xMatters OnDemand**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_app.png) 

3. <span data-ttu-id="31a83-241">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="31a83-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="31a83-243">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="31a83-243">Click **Add** button.</span></span> <span data-ttu-id="31a83-244">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="31a83-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="31a83-246">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="31a83-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="31a83-247">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="31a83-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="31a83-248">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="31a83-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="31a83-249">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="31a83-249">Testing single sign-on</span></span>

<span data-ttu-id="31a83-250">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="31a83-250">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="31a83-251">Lorsque vous cliquez sur hello xMatters OnDemand mosaïque hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour xMatters OnDemand application.</span><span class="sxs-lookup"><span data-stu-id="31a83-251">When you click hello xMatters OnDemand tile in hello Access Panel, you should get automatically signed-on tooyour xMatters OnDemand application.</span></span>
<span data-ttu-id="31a83-252">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="31a83-252">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="31a83-253">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="31a83-253">Additional resources</span></span>

* [<span data-ttu-id="31a83-254">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="31a83-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="31a83-255">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="31a83-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_203.png

