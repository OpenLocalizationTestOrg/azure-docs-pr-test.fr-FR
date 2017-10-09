---
title: "Didacticiel : Intégration d’Azure Active Directory avec TOPdesk - Public | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de TOPdesk - Public."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0873299f-ce70-457b-addc-e57c5801275f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: ef0dd06157ecc3b33814590039f5cbae64e8c916
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---public"></a><span data-ttu-id="5a1f4-103">Didacticiel : Intégration d’Azure Active Directory à TOPdesk - Public</span><span class="sxs-lookup"><span data-stu-id="5a1f4-103">Tutorial: Azure Active Directory integration with TOPdesk - Public</span></span>

<span data-ttu-id="5a1f4-104">Dans ce didacticiel, vous apprendrez comment toointegrate TOPdesk - Public avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5a1f4-104">In this tutorial, you learn how toointegrate TOPdesk - Public with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5a1f4-105">Intégration de TOPdesk - Public auprès d’Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="5a1f4-105">Integrating TOPdesk - Public with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5a1f4-106">Vous pouvez contrôler dans Azure AD qui a accès tooTOPdesk - Public.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-106">You can control in Azure AD who has access tooTOPdesk - Public.</span></span>
- <span data-ttu-id="5a1f4-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooTOPdesk - Public (Single Sign-On) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-107">You can enable your users tooautomatically get signed-on tooTOPdesk - Public (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="5a1f4-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="5a1f4-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5a1f4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5a1f4-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5a1f4-110">Prerequisites</span></span>

<span data-ttu-id="5a1f4-111">tooconfigure intégration d’Azure AD à TOPdesk - Public, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5a1f4-111">tooconfigure Azure AD integration with TOPdesk - Public, you need hello following items:</span></span>

- <span data-ttu-id="5a1f4-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a1f4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5a1f4-113">Un abonnement TOPdesk - Public pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="5a1f4-113">A TOPdesk - Public single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5a1f4-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5a1f4-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="5a1f4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5a1f4-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5a1f4-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5a1f4-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5a1f4-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="5a1f4-118">Scenario description</span></span>
<span data-ttu-id="5a1f4-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5a1f4-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="5a1f4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5a1f4-121">Ajout de TOPdesk - Public à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="5a1f4-121">Adding TOPdesk - Public from hello gallery</span></span>
2. <span data-ttu-id="5a1f4-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a1f4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-topdesk---public-from-hello-gallery"></a><span data-ttu-id="5a1f4-123">Ajout de TOPdesk - Public à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="5a1f4-123">Adding TOPdesk - Public from hello gallery</span></span>
<span data-ttu-id="5a1f4-124">intégration de hello tooconfigure de TOPdesk - Public dans Azure AD, vous devez tooadd TOPdesk - Public à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-124">tooconfigure hello integration of TOPdesk - Public into Azure AD, you need tooadd TOPdesk - Public from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5a1f4-125">**tooadd TOPdesk - Public à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5a1f4-125">**tooadd TOPdesk - Public from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5a1f4-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="5a1f4-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5a1f4-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="5a1f4-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="5a1f4-133">Dans la zone de recherche de hello, tapez **TOPdesk - Public**, sélectionnez **TOPdesk - Public** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-133">In hello search box, type **TOPdesk - Public**, select **TOPdesk - Public** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Liste des résultats de TOPdesk - Public Bonjour](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5a1f4-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a1f4-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="5a1f4-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec TOPdesk - Public avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="5a1f4-136">In this section, you configure and test Azure AD single sign-on with TOPdesk - Public based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5a1f4-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans TOPdesk - Public est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TOPdesk - Public is tooa user in Azure AD.</span></span> <span data-ttu-id="5a1f4-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans TOPdesk - Public doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-138">In other words, a link relationship between an Azure AD user and hello related user in TOPdesk - Public needs toobe established.</span></span>

<span data-ttu-id="5a1f4-139">Dans TOPdesk - Public, attribuer une valeur hello Hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-139">In TOPdesk - Public, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5a1f4-140">tooconfigure et tester Azure AD single sign-on avec TOPdesk - Public, que vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="5a1f4-140">tooconfigure and test Azure AD single sign-on with TOPdesk - Public, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5a1f4-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5a1f4-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5a1f4-143">**[Créer un TOPdesk - Public test utilisateur](#create-a-topdesk---public-test-user)**  - toohave un équivalent de Britta Simon dans TOPdesk - Public qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-143">**[Create a TOPdesk - Public test user](#create-a-topdesk---public-test-user)** - toohave a counterpart of Britta Simon in TOPdesk - Public that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5a1f4-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5a1f4-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5a1f4-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a1f4-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="5a1f4-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application TOPdesk - Public.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TOPdesk - Public application.</span></span>

<span data-ttu-id="5a1f4-148">**tooconfigure Azure AD l’authentification unique à TOPdesk - Public, effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5a1f4-148">**tooconfigure Azure AD single sign-on with TOPdesk - Public, perform hello following steps:**</span></span>

1. <span data-ttu-id="5a1f4-149">Bonjour portail Azure, sur hello **TOPdesk - Public** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-149">In hello Azure portal, on hello **TOPdesk - Public** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="5a1f4-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_samlbase.png)

3. <span data-ttu-id="5a1f4-153">Sur hello **TOPdesk - URL et du domaine Public** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5a1f4-153">On hello **TOPdesk - Public Domain and URLs** section, perform hello following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL TOPdesk - Public](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_url.png)

    <span data-ttu-id="5a1f4-155">a.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-155">a.</span></span> <span data-ttu-id="5a1f4-156">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.topdesk.net`</span><span class="sxs-lookup"><span data-stu-id="5a1f4-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.topdesk.net`</span></span>
    
    <span data-ttu-id="5a1f4-157">b.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-157">b.</span></span> <span data-ttu-id="5a1f4-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.topdesk.net/tas/public/login/verify`</span><span class="sxs-lookup"><span data-stu-id="5a1f4-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.topdesk.net/tas/public/login/verify`</span></span>

    <span data-ttu-id="5a1f4-159">c.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-159">c.</span></span> <span data-ttu-id="5a1f4-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.topdesk.net/tas/public/login/saml`</span><span class="sxs-lookup"><span data-stu-id="5a1f4-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.topdesk.net/tas/public/login/saml`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="5a1f4-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-161">These values are not real.</span></span> <span data-ttu-id="5a1f4-162">Mettre à jour ces valeurs avec hello réel identificateur, URL de réponse et URL de connexion.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-162">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="5a1f4-163">L’URL de réponse est expliquée plus loin dans le didacticiel.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-163">Reply URL is explaned later in tutorial.</span></span> <span data-ttu-id="5a1f4-164">Contact [TOPdesk - équipe de support Client Public](https://help.topdesk.com/saas/enterprise/user/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-164">Contact [TOPdesk - Public Client support team](https://help.topdesk.com/saas/enterprise/user/) tooget these values.</span></span>  

4. <span data-ttu-id="5a1f4-165">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_certificate.png) 

5. <span data-ttu-id="5a1f4-167">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="5a1f4-167">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="5a1f4-169">Sur hello **TOPdesk - Public Configuration** , cliquez sur **configurer TOPdesk - Public** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-169">On hello **TOPdesk - Public Configuration** section, click **Configure TOPdesk - Public** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5a1f4-170">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="5a1f4-170">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuration de TOPdesk - Public](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_configure.png) 

7. <span data-ttu-id="5a1f4-172">Ouverture de session tooyour **TOPdesk - Public** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-172">Sign on tooyour **TOPdesk - Public** company site as an administrator.</span></span>

8. <span data-ttu-id="5a1f4-173">Bonjour **TOPdesk** menu, cliquez sur **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-173">In hello **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="5a1f4-174">![Paramètres](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "Paramètres")</span><span class="sxs-lookup"><span data-stu-id="5a1f4-174">![Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "Settings")</span></span>

9. <span data-ttu-id="5a1f4-175">Cliquez sur **Login Settings**.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-175">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="5a1f4-176">![Paramètres de connexion](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "Paramètres de connexion")</span><span class="sxs-lookup"><span data-stu-id="5a1f4-176">![Login Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "Login Settings")</span></span>

10. <span data-ttu-id="5a1f4-177">Développez hello **les paramètres de connexion** menu, puis sur **général**.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-177">Expand hello **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="5a1f4-178">![Général](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "Général")</span><span class="sxs-lookup"><span data-stu-id="5a1f4-178">![General](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "General")</span></span>

11. <span data-ttu-id="5a1f4-179">Bonjour **Public** section Hello **connexion SAML** configuration section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5a1f4-179">In hello **Public** section of hello **SAML login** configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="5a1f4-180">![Paramètres techniques](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "Paramètres techniques")</span><span class="sxs-lookup"><span data-stu-id="5a1f4-180">![Technical Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "Technical Settings")</span></span>
   
    <span data-ttu-id="5a1f4-181">a.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-181">a.</span></span> <span data-ttu-id="5a1f4-182">Cliquez sur **télécharger** toodownload hello du fichier de métadonnées publiques et les enregistrer localement sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-182">Click **Download** toodownload hello public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="5a1f4-183">b.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-183">b.</span></span> <span data-ttu-id="5a1f4-184">Ouvrez le fichier de métadonnées hello téléchargé et recherchez hello **AssertionConsumerService** nœud.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-184">Open hello downloaded metadata file, and then locate hello **AssertionConsumerService** node.</span></span>

    <span data-ttu-id="5a1f4-185">![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")</span><span class="sxs-lookup"><span data-stu-id="5a1f4-185">![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")</span></span>
   
    <span data-ttu-id="5a1f4-186">c.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-186">c.</span></span> <span data-ttu-id="5a1f4-187">Hello de copie **AssertionConsumerService** valeur, collez cette valeur Bonjour **URL de réponse** zone de texte dans **TOPdesk - URL et du domaine Public** section.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-187">Copy hello **AssertionConsumerService** value, paste this value in hello **Reply URL** textbox in **TOPdesk - Public Domain and URLs** section.</span></span>      
   
12. <span data-ttu-id="5a1f4-188">toocreate un fichier de certificat, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5a1f4-188">toocreate a certificate file, perform hello following steps:</span></span>
    
    <span data-ttu-id="5a1f4-189">![Certificat](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "Certificat")</span><span class="sxs-lookup"><span data-stu-id="5a1f4-189">![Certificate](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "Certificate")</span></span>
    
    <span data-ttu-id="5a1f4-190">a.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-190">a.</span></span> <span data-ttu-id="5a1f4-191">Hello ouvrir téléchargé le fichier de métadonnées à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-191">Open hello downloaded metadata file from Azure portal.</span></span>
    
    <span data-ttu-id="5a1f4-192">b.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-192">b.</span></span> <span data-ttu-id="5a1f4-193">Développez hello **RoleDescriptor** nœud qui a un **xsi : type** de **fed : ApplicationServiceType**.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-193">Expand hello **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    
    <span data-ttu-id="5a1f4-194">c.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-194">c.</span></span> <span data-ttu-id="5a1f4-195">Copier la valeur hello Hello **X509Certificate** nœud.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-195">Copy hello value of hello **X509Certificate** node.</span></span>
    
    <span data-ttu-id="5a1f4-196">d.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-196">d.</span></span> <span data-ttu-id="5a1f4-197">Hello enregistrer copié **X509Certificate** valeur localement sur votre ordinateur dans un fichier.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-197">Save hello copied **X509Certificate** value locally on your computer in a file.</span></span>

13. <span data-ttu-id="5a1f4-198">Bonjour **Public** , cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-198">In hello **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="5a1f4-199">![Connexion SAML](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "Connexion SAML")</span><span class="sxs-lookup"><span data-stu-id="5a1f4-199">![SAML Login](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "SAML Login")</span></span>

14. <span data-ttu-id="5a1f4-200">Sur hello **l’assistant configuration de SAML** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5a1f4-200">On hello **SAML configuration assistant** dialog page, perform hello following steps:</span></span>
    
    <span data-ttu-id="5a1f4-201">![Assistant de configuration SAML](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "Assistant de configuration SAML")</span><span class="sxs-lookup"><span data-stu-id="5a1f4-201">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="5a1f4-202">a.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-202">a.</span></span> <span data-ttu-id="5a1f4-203">tooupload vos métadonnées téléchargée de fichiers à partir du portail Azure, sous **les métadonnées de fédération**, cliquez sur **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-203">tooupload your downloaded metadata file from Azure portal, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="5a1f4-204">b.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-204">b.</span></span> <span data-ttu-id="5a1f4-205">tooupload fichier de votre certificat, sous **Certificate (RSA)**, cliquez sur **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-205">tooupload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="5a1f4-206">c.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-206">c.</span></span> <span data-ttu-id="5a1f4-207">fichier de logo hello tooupload que vous avez obtenu à partir de l’équipe de support technique TOPdesk hello sous **icône du Logo**, cliquez sur **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-207">tooupload hello logo file you got from hello TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="5a1f4-208">d.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-208">d.</span></span> <span data-ttu-id="5a1f4-209">Bonjour **attribut nom d’utilisateur** zone de texte, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-209">In hello **User name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="5a1f4-210">e.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-210">e.</span></span> <span data-ttu-id="5a1f4-211">Bonjour **nom d’affichage** zone de texte, tapez un nom pour votre configuration.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-211">In hello **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="5a1f4-212">f.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-212">f.</span></span> <span data-ttu-id="5a1f4-213">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-213">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="5a1f4-214">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="5a1f4-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5a1f4-215">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5a1f4-216">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5a1f4-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5a1f4-217">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a1f4-217">Create an Azure AD test user</span></span>

<span data-ttu-id="5a1f4-218">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="5a1f4-220">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5a1f4-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5a1f4-221">Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-221">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="5a1f4-223">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-223">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="5a1f4-225">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-225">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![bouton Ajouter de Hello](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="5a1f4-227">Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5a1f4-227">In hello **User** dialog box, perform hello following steps:</span></span>

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_04.png)

    <span data-ttu-id="5a1f4-229">a.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-229">a.</span></span> <span data-ttu-id="5a1f4-230">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-230">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5a1f4-231">b.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-231">b.</span></span> <span data-ttu-id="5a1f4-232">Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-232">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="5a1f4-233">c.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-233">c.</span></span> <span data-ttu-id="5a1f4-234">Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-234">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="5a1f4-235">d.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-235">d.</span></span> <span data-ttu-id="5a1f4-236">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-236">Click **Create**.</span></span>
 
### <a name="create-a-topdesk---public-test-user"></a><span data-ttu-id="5a1f4-237">Créer un utilisateur de test TOPdesk - Public</span><span class="sxs-lookup"><span data-stu-id="5a1f4-237">Create a TOPdesk - Public test user</span></span>

<span data-ttu-id="5a1f4-238">Dans l’ordre tooenable Azure AD les utilisateurs toolog à TOPdesk - Public, vous devez les configurer dans TOPdesk - Public.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-238">In order tooenable Azure AD users toolog into TOPdesk - Public, they must be provisioned into TOPdesk - Public.</span></span>  
<span data-ttu-id="5a1f4-239">Dans le cas de hello de TOPdesk - Public, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-239">In hello case of TOPdesk - Public, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="5a1f4-240">configuration, de l’utilisateur tooconfigure effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5a1f4-240">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="5a1f4-241">Ouverture de session tooyour **TOPdesk - Public** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-241">Sign on tooyour **TOPdesk - Public** company site as administrator.</span></span>

2. <span data-ttu-id="5a1f4-242">Dans le menu hello haut de hello, cliquez sur **TOPdesk \> nouveau \> les fichiers de prise en charge \> personne**.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-242">In hello menu on hello top, click **TOPdesk \> New \> Support Files \> Person**.</span></span>
   
    <span data-ttu-id="5a1f4-243">![Personne](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "Personne")</span><span class="sxs-lookup"><span data-stu-id="5a1f4-243">![Person](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "Person")</span></span>

3. <span data-ttu-id="5a1f4-244">Dans la boîte de dialogue nouvelle personne hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5a1f4-244">On hello New Person dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="5a1f4-245">![Nouvelle personne](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "Nouvelle personne")</span><span class="sxs-lookup"><span data-stu-id="5a1f4-245">![New Person](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "New Person")</span></span>
   
    <span data-ttu-id="5a1f4-246">a.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-246">a.</span></span> <span data-ttu-id="5a1f4-247">Cliquez sur Général hello.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-247">Click hello General tab.</span></span>

    <span data-ttu-id="5a1f4-248">b.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-248">b.</span></span> <span data-ttu-id="5a1f4-249">Bonjour **Surname** zone de texte, tapez le nom d’utilisateur hello comme Simon</span><span class="sxs-lookup"><span data-stu-id="5a1f4-249">In hello **Surname** textbox, type Surname of hello user like Simon</span></span>
 
    <span data-ttu-id="5a1f4-250">c.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-250">c.</span></span> <span data-ttu-id="5a1f4-251">Sélectionnez un **Site** pour le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-251">Select a **Site** for hello account.</span></span>
 
    <span data-ttu-id="5a1f4-252">d.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-252">d.</span></span> <span data-ttu-id="5a1f4-253">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-253">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="5a1f4-254">Vous pouvez utiliser n’importe quel autre TOPdesk - outil de création de compte utilisateur publique ou une autre API fournies par TOPdesk - Public tooprovision Azure AD des comptes d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-254">You can use any other TOPdesk - Public user account creation tools or APIs provided by TOPdesk - Public tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="5a1f4-255">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a1f4-255">Assign hello Azure AD test user</span></span>

<span data-ttu-id="5a1f4-256">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooTOPdesk - Public.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-256">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTOPdesk - Public.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="5a1f4-258">**tooassign Britta Simon tooTOPdesk - Public, effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5a1f4-258">**tooassign Britta Simon tooTOPdesk - Public, perform hello following steps:**</span></span>

1. <span data-ttu-id="5a1f4-259">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-259">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="5a1f4-261">Dans la liste des applications hello, sélectionnez **TOPdesk - Public**.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-261">In hello applications list, select **TOPdesk - Public**.</span></span>

    ![Hello TOPdesk - Public de lien dans la liste des Applications hello](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_app.png)  

3. <span data-ttu-id="5a1f4-263">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-263">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202]

4. <span data-ttu-id="5a1f4-265">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-265">Click **Add** button.</span></span> <span data-ttu-id="5a1f4-266">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-266">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="5a1f4-268">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-268">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5a1f4-269">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-269">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5a1f4-270">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-270">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="5a1f4-271">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="5a1f4-271">Test single sign-on</span></span>

<span data-ttu-id="5a1f4-272">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-272">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5a1f4-273">Lorsque vous cliquez sur hello TOPdesk - Public vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour TOPdesk - Public application.</span><span class="sxs-lookup"><span data-stu-id="5a1f4-273">When you click hello TOPdesk - Public tile in hello Access Panel, you should get automatically signed-on tooyour TOPdesk - Public application.</span></span>
<span data-ttu-id="5a1f4-274">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5a1f4-274">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5a1f4-275">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="5a1f4-275">Additional resources</span></span>

* [<span data-ttu-id="5a1f4-276">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5a1f4-276">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5a1f4-277">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="5a1f4-277">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_203.png

