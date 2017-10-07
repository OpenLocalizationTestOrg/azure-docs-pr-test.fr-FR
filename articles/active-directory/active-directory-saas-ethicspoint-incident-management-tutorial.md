---
title: "Didacticiel : Intégration d’Azure Active Directory avec EthicsPoint Incident Management (EPIM) | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et gestion d’Incident EthicsPoint (EPIM)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8cb31a4c-9309-469b-93ac-daf0d3c7a3e6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 73ef5fab815cddb3728f4b23173f99e62aec5bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ethicspoint-incident-management-epim"></a><span data-ttu-id="ca5fa-103">Didacticiel : Intégration d’Azure Active Directory avec EthicsPoint Incident Management (EPIM)</span><span class="sxs-lookup"><span data-stu-id="ca5fa-103">Tutorial: Azure Active Directory integration with EthicsPoint Incident Management (EPIM)</span></span>

<span data-ttu-id="ca5fa-104">Dans ce didacticiel, vous apprendrez comment toointegrate EthicsPoint Incident Management (EPIM) avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ca5fa-104">In this tutorial, you learn how toointegrate EthicsPoint Incident Management (EPIM) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ca5fa-105">Intégration de gestion d’Incident EthicsPoint (EPIM) avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="ca5fa-105">Integrating EthicsPoint Incident Management (EPIM) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ca5fa-106">Vous pouvez contrôler dans Azure AD qui a accès tooEthicsPoint gestion de l’Incident (EPIM)</span><span class="sxs-lookup"><span data-stu-id="ca5fa-106">You can control in Azure AD who has access tooEthicsPoint Incident Management (EPIM)</span></span>
- <span data-ttu-id="ca5fa-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooEthicsPoint gestion d’Incident (EPIM) (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="ca5fa-107">You can enable your users tooautomatically get signed-on tooEthicsPoint Incident Management (EPIM) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ca5fa-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="ca5fa-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ca5fa-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ca5fa-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ca5fa-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ca5fa-110">Prerequisites</span></span>

<span data-ttu-id="ca5fa-111">tooconfigure intégration d’Azure AD avec EthicsPoint Incident Management (EPIM), vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ca5fa-111">tooconfigure Azure AD integration with EthicsPoint Incident Management (EPIM), you need hello following items:</span></span>

- <span data-ttu-id="ca5fa-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="ca5fa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ca5fa-113">Un abonnement EthicsPoint Incident Management (EPIM) pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="ca5fa-113">A EthicsPoint Incident Management (EPIM) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ca5fa-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ca5fa-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="ca5fa-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ca5fa-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ca5fa-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ca5fa-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ca5fa-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="ca5fa-118">Scenario description</span></span>
<span data-ttu-id="ca5fa-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ca5fa-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="ca5fa-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ca5fa-121">Ajout de gestion d’Incident EthicsPoint (EPIM) à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="ca5fa-121">Adding EthicsPoint Incident Management (EPIM) from hello gallery</span></span>
2. <span data-ttu-id="ca5fa-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ca5fa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ethicspoint-incident-management-epim-from-hello-gallery"></a><span data-ttu-id="ca5fa-123">Ajout de gestion d’Incident EthicsPoint (EPIM) à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="ca5fa-123">Adding EthicsPoint Incident Management (EPIM) from hello gallery</span></span>
<span data-ttu-id="ca5fa-124">intégration de hello tooconfigure de EthicsPoint Incident Management (EPIM) dans Azure AD, vous devez tooadd EthicsPoint Incident Management (EPIM) à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-124">tooconfigure hello integration of EthicsPoint Incident Management (EPIM) into Azure AD, you need tooadd EthicsPoint Incident Management (EPIM) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ca5fa-125">**tooadd EthicsPoint Incident Management (EPIM) à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ca5fa-125">**tooadd EthicsPoint Incident Management (EPIM) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ca5fa-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ca5fa-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ca5fa-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="ca5fa-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="ca5fa-133">Dans la zone de recherche de hello, tapez **EthicsPoint Incident Management (EPIM)**.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-133">In hello search box, type **EthicsPoint Incident Management (EPIM)**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_search.png)

5. <span data-ttu-id="ca5fa-135">Dans le volet de résultats hello, sélectionnez **EthicsPoint Incident Management (EPIM)**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-135">In hello results panel, select **EthicsPoint Incident Management (EPIM)**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ca5fa-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ca5fa-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ca5fa-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec EthicsPoint Incident Management (EPIM) avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="ca5fa-138">In this section, you configure and test Azure AD single sign-on with EthicsPoint Incident Management (EPIM) based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ca5fa-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans EthicsPoint Incident Management (EPIM) est tooa dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in EthicsPoint Incident Management (EPIM) is tooa user in Azure AD.</span></span> <span data-ttu-id="ca5fa-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans EthicsPoint Incident Management (EPIM) doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-140">In other words, a link relationship between an Azure AD user and hello related user in EthicsPoint Incident Management (EPIM) needs toobe established.</span></span>

<span data-ttu-id="ca5fa-141">Dans Gestion de Incident EthicsPoint (EPIM), affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-141">In EthicsPoint Incident Management (EPIM), assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ca5fa-142">tooconfigure et test Azure AD l’authentification unique avec EthicsPoint Incident Management (EPIM), vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="ca5fa-142">tooconfigure and test Azure AD single sign-on with EthicsPoint Incident Management (EPIM), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ca5fa-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ca5fa-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ca5fa-145">**[Création d’un utilisateur de test EthicsPoint Incident Management (EPIM)](#creating-a-ethicspoint-incident-management-epim-test-user)**  -toohave un équivalent de Britta Simon dans EthicsPoint Incident Management (EPIM) qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-145">**[Creating a EthicsPoint Incident Management (EPIM) test user](#creating-a-ethicspoint-incident-management-epim-test-user)** - toohave a counterpart of Britta Simon in EthicsPoint Incident Management (EPIM) that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ca5fa-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ca5fa-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ca5fa-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ca5fa-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ca5fa-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de gestion d’Incident EthicsPoint (EPIM).</span><span class="sxs-lookup"><span data-stu-id="ca5fa-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your EthicsPoint Incident Management (EPIM) application.</span></span>

<span data-ttu-id="ca5fa-150">**tooconfigure Azure AD l’authentification unique avec EthicsPoint Incident Management (EPIM), exécutez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ca5fa-150">**tooconfigure Azure AD single sign-on with EthicsPoint Incident Management (EPIM), perform hello following steps:**</span></span>

1. <span data-ttu-id="ca5fa-151">Bonjour portail Azure, sur hello **EthicsPoint Incident Management (EPIM)** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-151">In hello Azure portal, on hello **EthicsPoint Incident Management (EPIM)** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="ca5fa-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_samlbase.png)

3. <span data-ttu-id="ca5fa-155">Sur hello **URL et le domaine de la gestion d’Incident EthicsPoint (EPIM)** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="ca5fa-155">On hello **EthicsPoint Incident Management (EPIM) Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_url.png)

    <span data-ttu-id="ca5fa-157">a.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-157">a.</span></span> <span data-ttu-id="ca5fa-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :</span><span class="sxs-lookup"><span data-stu-id="ca5fa-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.navexglobal.com`|
    | `https://<companyname>.ethicspointvp.com`|

    <span data-ttu-id="ca5fa-159">b.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-159">b.</span></span> <span data-ttu-id="ca5fa-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.navexglobal.com/adfs/services/trust`</span><span class="sxs-lookup"><span data-stu-id="ca5fa-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.navexglobal.com/adfs/services/trust`</span></span>

    <span data-ttu-id="ca5fa-161">c.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-161">c.</span></span> <span data-ttu-id="ca5fa-162">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<servername>.navexglobal.com/adfs/ls/`</span><span class="sxs-lookup"><span data-stu-id="ca5fa-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<servername>.navexglobal.com/adfs/ls/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ca5fa-163">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-163">These values are not real.</span></span> <span data-ttu-id="ca5fa-164">Mettre à jour ces valeurs avec des URL de réponse réelle hello, identificateur et URL de connexion.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-164">Update these values with hello actual Reply URL, Identifier, and Sign-On URL.</span></span> <span data-ttu-id="ca5fa-165">Contact [équipe de support Client de gestion d’Incident EthicsPoint (EPIM)](http://www.navexglobal.com/company/contact-us) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-165">Contact [EthicsPoint Incident Management (EPIM) Client support team](http://www.navexglobal.com/company/contact-us) tooget these values.</span></span> 

4. <span data-ttu-id="ca5fa-166">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_certificate.png) 

5. <span data-ttu-id="ca5fa-168">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="ca5fa-168">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="ca5fa-170">tooconfigure l’authentification unique sur **EthicsPoint Incident Management (EPIM)** côté, vous devez hello toosend téléchargé **Metadata XML** trop[prise en charge de la gestion d’Incident EthicsPoint (EPIM) équipe](http://www.navexglobal.com/company/contact-us).</span><span class="sxs-lookup"><span data-stu-id="ca5fa-170">tooconfigure single sign-on on **EthicsPoint Incident Management (EPIM)** side, you need toosend hello downloaded **Metadata XML** too[EthicsPoint Incident Management (EPIM) support team](http://www.navexglobal.com/company/contact-us).</span></span>

> [!TIP]
> <span data-ttu-id="ca5fa-171">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="ca5fa-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ca5fa-172">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ca5fa-173">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ca5fa-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ca5fa-174">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="ca5fa-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="ca5fa-175">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="ca5fa-177">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ca5fa-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ca5fa-178">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ca5fa-180">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ca5fa-182">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ca5fa-184">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="ca5fa-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ca5fa-186">a.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-186">a.</span></span> <span data-ttu-id="ca5fa-187">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ca5fa-188">b.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-188">b.</span></span> <span data-ttu-id="ca5fa-189">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ca5fa-190">c.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-190">c.</span></span> <span data-ttu-id="ca5fa-191">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ca5fa-192">d.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-192">d.</span></span> <span data-ttu-id="ca5fa-193">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-193">Click **Create**.</span></span>
 
### <a name="creating-a-ethicspoint-incident-management-epim-test-user"></a><span data-ttu-id="ca5fa-194">Création d’un utilisateur de test d’EthicsPoint Incident Management (EPIM)</span><span class="sxs-lookup"><span data-stu-id="ca5fa-194">Creating a EthicsPoint Incident Management (EPIM) test user</span></span>

<span data-ttu-id="ca5fa-195">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans EthicsPoint Incident Management (EPIM).</span><span class="sxs-lookup"><span data-stu-id="ca5fa-195">In this section, you create a user called Britta Simon in EthicsPoint Incident Management (EPIM).</span></span> <span data-ttu-id="ca5fa-196">Collaborez avec [équipe de support technique de gestion d’Incident EthicsPoint (EPIM)](http://www.navexglobal.com/company/contact-us) tooadd les utilisateurs de hello dans la plateforme de gestion d’Incident EthicsPoint (EPIM) hello.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-196">Please work with [EthicsPoint Incident Management (EPIM) support team](http://www.navexglobal.com/company/contact-us) tooadd hello users in hello EthicsPoint Incident Management (EPIM) platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ca5fa-197">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ca5fa-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ca5fa-198">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooEthicsPoint gestion de l’Incident (EPIM).</span><span class="sxs-lookup"><span data-stu-id="ca5fa-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEthicsPoint Incident Management (EPIM).</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="ca5fa-200">**tooassign Britta Simon tooEthicsPoint gestion de l’Incident (EPIM), exécutez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ca5fa-200">**tooassign Britta Simon tooEthicsPoint Incident Management (EPIM), perform hello following steps:**</span></span>

1. <span data-ttu-id="ca5fa-201">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="ca5fa-203">Dans la liste des applications hello, sélectionnez **EthicsPoint Incident Management (EPIM)**.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-203">In hello applications list, select **EthicsPoint Incident Management (EPIM)**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_app.png) 

3. <span data-ttu-id="ca5fa-205">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="ca5fa-207">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-207">Click **Add** button.</span></span> <span data-ttu-id="ca5fa-208">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="ca5fa-210">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ca5fa-211">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ca5fa-212">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ca5fa-213">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="ca5fa-213">Testing single sign-on</span></span>

<span data-ttu-id="ca5fa-214">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
<span data-ttu-id="ca5fa-215">Lorsque vous cliquez sur vignette de gestion d’Incident EthicsPoint (EPIM) hello Bonjour volet d’accès, vous devez obtenir l’application de gestion d’Incident EthicsPoint (EPIM) automatiquement signé sur tooyour.</span><span class="sxs-lookup"><span data-stu-id="ca5fa-215">When you click hello EthicsPoint Incident Management (EPIM) tile in hello Access Panel, you should get automatically signed-on tooyour EthicsPoint Incident Management (EPIM) application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ca5fa-216">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="ca5fa-216">Additional resources</span></span>

* [<span data-ttu-id="ca5fa-217">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ca5fa-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ca5fa-218">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="ca5fa-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_203.png

