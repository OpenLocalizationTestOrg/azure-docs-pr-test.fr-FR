---
title: "Didacticiel : Intégration d’Azure Active Directory avec Five9 Plus Adapter(CTI, agents de centre de contacts) | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Five9 ainsi que l’adaptateur (CTI, Agents de centre de Contact)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 88dc82ab-be0b-4017-8335-c47d00775d7b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: jeedes
ms.openlocfilehash: 2e3ea8b5f2a6eaa8ad17d39e03fa490038b14561
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-five9-plus-adapter-cti-contact-center-agents"></a><span data-ttu-id="8108d-103">Didacticiel : Intégration d’Azure Active Directory avec Five9 Plus Adapter(CTI, agents de centre de contacts)</span><span class="sxs-lookup"><span data-stu-id="8108d-103">Tutorial: Azure Active Directory integration with Five9 Plus Adapter (CTI, Contact Center Agents)</span></span>

<span data-ttu-id="8108d-104">Dans ce didacticiel, vous apprendrez comment toointegrate Five9 ainsi que l’adaptateur (CTI, Contact Center Agents) avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8108d-104">In this tutorial, you learn how toointegrate Five9 Plus Adapter (CTI, Contact Center Agents) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8108d-105">Intégration Five9 ainsi que l’adaptateur (CTI, Agents de Contact Center) à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="8108d-105">Integrating Five9 Plus Adapter (CTI, Contact Center Agents) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8108d-106">Vous pouvez contrôler dans Azure AD qui a accès tooFive9 ainsi que l’adaptateur (CTI, Contact Center Agents)</span><span class="sxs-lookup"><span data-stu-id="8108d-106">You can control in Azure AD who has access tooFive9 Plus Adapter (CTI, Contact Center Agents)</span></span>
- <span data-ttu-id="8108d-107">Vous pouvez activer votre get tooautomatically d’utilisateurs authentifiés sur tooFive9 Plus de la carte (CTI, Contact Center Agents) (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="8108d-107">You can enable your users tooautomatically get signed-on tooFive9 Plus Adapter (CTI, Contact Center Agents) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8108d-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="8108d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8108d-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8108d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8108d-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8108d-110">Prerequisites</span></span>

<span data-ttu-id="8108d-111">intégration tooconfigure Azure AD avec Five9 ainsi que l’adaptateur (CTI, Agents de centre de Contact), vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="8108d-111">tooconfigure Azure AD integration with Five9 Plus Adapter (CTI, Contact Center Agents), you need hello following items:</span></span>

- <span data-ttu-id="8108d-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="8108d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8108d-113">Un abonnement Five9 Plus Adapter (CTI, agents de centre de contacts) pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="8108d-113">A Five9 Plus Adapter (CTI, Contact Center Agents) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8108d-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="8108d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8108d-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="8108d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8108d-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="8108d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8108d-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois ici : [offre d’essai](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8108d-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8108d-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="8108d-118">Scenario description</span></span>
<span data-ttu-id="8108d-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="8108d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8108d-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="8108d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8108d-121">Ajout de Five9 ainsi que l’adaptateur (CTI, Agents de Contact Center) à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="8108d-121">Adding Five9 Plus Adapter (CTI, Contact Center Agents) from hello gallery</span></span>
2. <span data-ttu-id="8108d-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8108d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-five9-plus-adapter-cti-contact-center-agents-from-hello-gallery"></a><span data-ttu-id="8108d-123">Ajout de Five9 ainsi que l’adaptateur (CTI, Agents de Contact Center) à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="8108d-123">Adding Five9 Plus Adapter (CTI, Contact Center Agents) from hello gallery</span></span>
<span data-ttu-id="8108d-124">tooconfigure hello intégration de Five9 ainsi que l’adaptateur (CTI, Contact Center Agents) dans Azure AD, vous devez tooadd Five9 ainsi que l’adaptateur (CTI, Agents de Contact Center) à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="8108d-124">tooconfigure hello integration of Five9 Plus Adapter (CTI, Contact Center Agents) into Azure AD, you need tooadd Five9 Plus Adapter (CTI, Contact Center Agents) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8108d-125">**tooadd Five9 ainsi que l’adaptateur (CTI, Agents de Contact Center) à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8108d-125">**tooadd Five9 Plus Adapter (CTI, Contact Center Agents) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8108d-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="8108d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8108d-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="8108d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8108d-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8108d-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="8108d-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8108d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="8108d-133">Dans la zone de recherche de hello, tapez **Five9 ainsi que l’adaptateur (CTI, Agents de centre de Contact)**.</span><span class="sxs-lookup"><span data-stu-id="8108d-133">In hello search box, type **Five9 Plus Adapter (CTI, Contact Center Agents)**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-five9-tutorial/tutorial_five9_search.png)

5. <span data-ttu-id="8108d-135">Dans le volet de résultats hello, sélectionnez **Five9 ainsi que l’adaptateur (CTI, Agents de centre de Contact)**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="8108d-135">In hello results panel, select **Five9 Plus Adapter (CTI, Contact Center Agents)**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-five9-tutorial/tutorial_five9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8108d-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8108d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8108d-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Five9 Plus Adapter (CTI, agents de centre de contacts), avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="8108d-138">In this section, you configure and test Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8108d-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Five9 ainsi que l’adaptateur (CTI, Agents de Contact Center) est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8108d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Five9 Plus Adapter (CTI, Contact Center Agents) is tooa user in Azure AD.</span></span> <span data-ttu-id="8108d-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Five9 ainsi que l’adaptateur (CTI, Contact Center Agents) doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="8108d-140">In other words, a link relationship between an Azure AD user and hello related user in Five9 Plus Adapter (CTI, Contact Center Agents) needs toobe established.</span></span>

<span data-ttu-id="8108d-141">Dans Five9 ainsi que l’adaptateur (CTI, Agents de centre de Contact), affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="8108d-141">In Five9 Plus Adapter (CTI, Contact Center Agents), assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8108d-142">tooconfigure et test Azure AD l’authentification unique avec Five9 ainsi que l’adaptateur (CTI, Agents de centre de Contact), vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="8108d-142">tooconfigure and test Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8108d-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="8108d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8108d-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8108d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8108d-145">**[Création d’un utilisateur de test Five9 ainsi que l’adaptateur (CTI, Agents de centre de Contact)](#creating-a-five9-plus-adapter-cti-contact-center-agents-test-user)**  -toohave un équivalent de Britta Simon dans Five9 ainsi que l’adaptateur (CTI, Contact Center Agents) qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8108d-145">**[Creating a Five9 Plus Adapter (CTI, Contact Center Agents) test user](#creating-a-five9-plus-adapter-cti-contact-center-agents-test-user)** - toohave a counterpart of Britta Simon in Five9 Plus Adapter (CTI, Contact Center Agents) that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8108d-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="8108d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8108d-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="8108d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8108d-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8108d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8108d-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de carte réseau Plus Five9 (CTI, Agents de centre de Contact).</span><span class="sxs-lookup"><span data-stu-id="8108d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Five9 Plus Adapter (CTI, Contact Center Agents) application.</span></span>

<span data-ttu-id="8108d-150">**tooconfigure Azure AD l’authentification unique avec Five9 ainsi que l’adaptateur (CTI, Agents de centre de Contact), effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8108d-150">**tooconfigure Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents), perform hello following steps:**</span></span>

1. <span data-ttu-id="8108d-151">Bonjour portail Azure, sur hello **Five9 ainsi que l’adaptateur (CTI, Agents de centre de Contact)** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="8108d-151">In hello Azure portal, on hello **Five9 Plus Adapter (CTI, Contact Center Agents)** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="8108d-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="8108d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-five9-tutorial/tutorial_five9_samlbase.png)

3. <span data-ttu-id="8108d-155">Sur hello **Five9 ainsi que l’adaptateur (CTI, Agents de centre de Contact) domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8108d-155">On hello **Five9 Plus Adapter (CTI, Contact Center Agents) Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-five9-tutorial/tutorial_five9_url.png)
    
    <span data-ttu-id="8108d-157">a.</span><span class="sxs-lookup"><span data-stu-id="8108d-157">a.</span></span> <span data-ttu-id="8108d-158">Bonjour **identificateur** modèles de zone de texte, tapez une URL à l’aide de hello suivant :</span><span class="sxs-lookup"><span data-stu-id="8108d-158">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span>

    |    <span data-ttu-id="8108d-159">Environnement</span><span class="sxs-lookup"><span data-stu-id="8108d-159">Environment</span></span>      |       <span data-ttu-id="8108d-160">URL</span><span class="sxs-lookup"><span data-stu-id="8108d-160">URL</span></span>      |
    | :-- | :-- |
    | <span data-ttu-id="8108d-161">Pour « Five9 Plus Adapter for Microsoft Dynamics CRM »</span><span class="sxs-lookup"><span data-stu-id="8108d-161">For “Five9 Plus Adapter for Microsoft Dynamics CRM”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/msdc` |
    | <span data-ttu-id="8108d-162">Pour « Five9 Plus Adapter for Zendesk »</span><span class="sxs-lookup"><span data-stu-id="8108d-162">For “Five9 Plus Adapter for Zendesk”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/zd` |
    | <span data-ttu-id="8108d-163">Pour « Five9 Plus Adapter for Agent Desktop Toolkit »</span><span class="sxs-lookup"><span data-stu-id="8108d-163">For “Five9 Plus Adapter for Agent Desktop Toolkit”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/adt` |

    <span data-ttu-id="8108d-164">b.</span><span class="sxs-lookup"><span data-stu-id="8108d-164">b.</span></span> <span data-ttu-id="8108d-165">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :</span><span class="sxs-lookup"><span data-stu-id="8108d-165">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>

    |      <span data-ttu-id="8108d-166">Environnement</span><span class="sxs-lookup"><span data-stu-id="8108d-166">Environment</span></span>     |      <span data-ttu-id="8108d-167">URL</span><span class="sxs-lookup"><span data-stu-id="8108d-167">URL</span></span>      |
    | :--                  | :--           |
    | <span data-ttu-id="8108d-168">Pour « Five9 Plus Adapter for Microsoft Dynamics CRM »</span><span class="sxs-lookup"><span data-stu-id="8108d-168">For “Five9 Plus Adapter for Microsoft Dynamics CRM”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/msdc` |
    | <span data-ttu-id="8108d-169">Pour « Five9 Plus Adapter for Zendesk »</span><span class="sxs-lookup"><span data-stu-id="8108d-169">For “Five9 Plus Adapter for Zendesk”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/zd` |
    | <span data-ttu-id="8108d-170">Pour « Five9 Plus Adapter for Agent Desktop Toolkit »</span><span class="sxs-lookup"><span data-stu-id="8108d-170">For “Five9 Plus Adapter for Agent Desktop Toolkit”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/adt` |

4. <span data-ttu-id="8108d-171">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="8108d-171">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-five9-tutorial/tutorial_five9_certificate.png) 

5. <span data-ttu-id="8108d-173">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="8108d-173">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-five9-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8108d-175">Sur hello **Five9 ainsi que l’adaptateur (CTI, Agents de centre de Contact) Configuration** , cliquez sur **configurer Five9 ainsi que l’adaptateur (CTI, Agents de centre de Contact)** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="8108d-175">On hello **Five9 Plus Adapter (CTI, Contact Center Agents) Configuration** section, click **Configure Five9 Plus Adapter (CTI, Contact Center Agents)** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8108d-176">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="8108d-176">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-five9-tutorial/tutorial_five9_configure.png) 

7. <span data-ttu-id="8108d-178">tooconfigure l’authentification unique sur **Five9 ainsi que l’adaptateur (CTI, Agents de centre de Contact)** côté, vous devez hello toosend téléchargé **Certificate(Base64), l’URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** trop[équipe de support Five9 ainsi que l’adaptateur (CTI, Agents de centre de Contact)](https://www.five9.com/about/contact).</span><span class="sxs-lookup"><span data-stu-id="8108d-178">tooconfigure single sign-on on **Five9 Plus Adapter (CTI, Contact Center Agents)** side, you need toosend hello downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Five9 Plus Adapter (CTI, Contact Center Agents) support team](https://www.five9.com/about/contact).</span></span> <span data-ttu-id="8108d-179">Également, en outre, pour la configuration de l’authentification unique plus Veuillez suivre hello étapes en fonction de l’adaptateur toohello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="8108d-179">Also additionally, for configuring SSO further please follow hello below steps according toohello adapter:</span></span>

    <span data-ttu-id="8108d-180">a.</span><span class="sxs-lookup"><span data-stu-id="8108d-180">a.</span></span> <span data-ttu-id="8108d-181">Guide de l’administrateur « Five9 Plus Adapter for Agent Desktop Toolkit » : [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="8108d-181">“Five9 Plus Adapter for Agent Desktop Toolkit” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf)</span></span>
    
    <span data-ttu-id="8108d-182">b.</span><span class="sxs-lookup"><span data-stu-id="8108d-182">b.</span></span> <span data-ttu-id="8108d-183">Guide de l’administrateur « Five9 Plus Adapter for Microsoft Dynamics CRM » : [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="8108d-183">“Five9 Plus Adapter for Microsoft Dynamics CRM” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf)</span></span>
    
    <span data-ttu-id="8108d-184">c.</span><span class="sxs-lookup"><span data-stu-id="8108d-184">c.</span></span> <span data-ttu-id="8108d-185">Guide de l’administrateur « Five9 Plus Adapter for Zendesk » : [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="8108d-185">“Five9 Plus Adapter for Zendesk” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf)</span></span>


> [!TIP]
> <span data-ttu-id="8108d-186">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="8108d-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8108d-187">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="8108d-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8108d-188">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8108d-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8108d-189">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="8108d-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="8108d-190">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="8108d-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="8108d-192">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8108d-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8108d-193">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="8108d-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-five9-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8108d-195">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="8108d-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-five9-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8108d-197">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="8108d-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-five9-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8108d-199">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8108d-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-five9-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8108d-201">a.</span><span class="sxs-lookup"><span data-stu-id="8108d-201">a.</span></span> <span data-ttu-id="8108d-202">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8108d-202">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8108d-203">b.</span><span class="sxs-lookup"><span data-stu-id="8108d-203">b.</span></span> <span data-ttu-id="8108d-204">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8108d-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8108d-205">c.</span><span class="sxs-lookup"><span data-stu-id="8108d-205">c.</span></span> <span data-ttu-id="8108d-206">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="8108d-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8108d-207">d.</span><span class="sxs-lookup"><span data-stu-id="8108d-207">d.</span></span> <span data-ttu-id="8108d-208">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="8108d-208">Click **Create**.</span></span>
 
### <a name="creating-a-five9-plus-adapter-cti-contact-center-agents-test-user"></a><span data-ttu-id="8108d-209">Création d’un utilisateur de test Five9 Plus Adapter (CTI, agents de centre de contacts)</span><span class="sxs-lookup"><span data-stu-id="8108d-209">Creating a Five9 Plus Adapter (CTI, Contact Center Agents) test user</span></span>

<span data-ttu-id="8108d-210">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Five9 Plus Adapter (CTI, agents de centre de contacts).</span><span class="sxs-lookup"><span data-stu-id="8108d-210">In this section, you create a user called Britta Simon in Five9 Plus Adapter (CTI, Contact Center Agents).</span></span> <span data-ttu-id="8108d-211">Travailler avec [équipe de support Five9 ainsi que l’adaptateur (CTI, Agents de centre de Contact)](https://www.five9.com/about/contact) pour ajouter des utilisateurs de hello de plateforme de hello Five9 ainsi que l’adaptateur (CTI, Agents de centre de Contact).</span><span class="sxs-lookup"><span data-stu-id="8108d-211">Work with [Five9 Plus Adapter (CTI, Contact Center Agents) support team](https://www.five9.com/about/contact) to add hello users in hello Five9 Plus Adapter (CTI, Contact Center Agents) platform.</span></span> <span data-ttu-id="8108d-212">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="8108d-212">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8108d-213">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8108d-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8108d-214">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooFive9 ainsi que l’adaptateur (CTI, Agents de centre de Contact).</span><span class="sxs-lookup"><span data-stu-id="8108d-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFive9 Plus Adapter (CTI, Contact Center Agents).</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="8108d-216">**tooassign Britta Simon tooFive9 ainsi que l’adaptateur (CTI, Agents de centre de Contact), effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8108d-216">**tooassign Britta Simon tooFive9 Plus Adapter (CTI, Contact Center Agents), perform hello following steps:**</span></span>

1. <span data-ttu-id="8108d-217">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8108d-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="8108d-219">Dans la liste des applications hello, sélectionnez **Five9 ainsi que l’adaptateur (CTI, Agents de centre de Contact)**.</span><span class="sxs-lookup"><span data-stu-id="8108d-219">In hello applications list, select **Five9 Plus Adapter (CTI, Contact Center Agents)**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-five9-tutorial/tutorial_five9_app.png) 

3. <span data-ttu-id="8108d-221">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8108d-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="8108d-223">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="8108d-223">Click **Add** button.</span></span> <span data-ttu-id="8108d-224">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="8108d-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="8108d-226">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="8108d-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8108d-227">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8108d-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8108d-228">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="8108d-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8108d-229">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="8108d-229">Testing single sign-on</span></span>

<span data-ttu-id="8108d-230">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="8108d-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8108d-231">Lorsque vous cliquez sur mosaïque Five9 ainsi que l’adaptateur (CTI, Agents de centre de Contact) hello hello volet d’accès, vous devez obtenir tooyour automatiquement signé sur demande de l’adaptateur de Plus Five9 (CTI, Agents de centre de Contact).</span><span class="sxs-lookup"><span data-stu-id="8108d-231">When you click hello Five9 Plus Adapter (CTI, Contact Center Agents) tile in hello Access Panel, you should get automatically signed-on tooyour Five9 Plus Adapter (CTI, Contact Center Agents) application.</span></span>
<span data-ttu-id="8108d-232">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8108d-232">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8108d-233">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="8108d-233">Additional resources</span></span>

* [<span data-ttu-id="8108d-234">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8108d-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8108d-235">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="8108d-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-five9-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-five9-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-five9-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-five9-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-five9-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-five9-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-five9-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-five9-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-five9-tutorial/tutorial_general_203.png

