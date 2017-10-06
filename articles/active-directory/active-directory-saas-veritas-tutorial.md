---
title: "Didacticiel : intégration d’Azure Active Directory à Veritas Enterprise Vault.cloud SSO | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et l’authentification unique de Veritas Enterprise Vault.cloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c47894b1-f5df-4755-845d-f12f4c602dc4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 1037e70515686091460ac41e9e5a7951639bb520
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-veritas-enterprise-vaultcloud-sso"></a><span data-ttu-id="3f2e7-103">Didacticiel : intégration d’Azure Active Directory à Veritas Enterprise Vault.cloud SSO</span><span class="sxs-lookup"><span data-stu-id="3f2e7-103">Tutorial: Azure Active Directory integration with Veritas Enterprise Vault.cloud SSO</span></span>

<span data-ttu-id="3f2e7-104">Dans ce didacticiel, vous apprendrez comment toointegrate Veritas Enterprise Vault.cloud SSO avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3f2e7-104">In this tutorial, you learn how toointegrate Veritas Enterprise Vault.cloud SSO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3f2e7-105">Intégration Veritas Enterprise Vault.cloud SSO avec AD Azure vous offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="3f2e7-105">Integrating Veritas Enterprise Vault.cloud SSO with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3f2e7-106">Vous pouvez contrôler dans Azure AD qui a accès tooVeritas Vault.cloud de Enterprise SSO</span><span class="sxs-lookup"><span data-stu-id="3f2e7-106">You can control in Azure AD who has access tooVeritas Enterprise Vault.cloud SSO</span></span>
- <span data-ttu-id="3f2e7-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooVeritas Enterprise Vault.cloud SSO (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f2e7-107">You can enable your users tooautomatically get signed-on tooVeritas Enterprise Vault.cloud SSO (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3f2e7-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="3f2e7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3f2e7-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3f2e7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3f2e7-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="3f2e7-110">Prerequisites</span></span>

<span data-ttu-id="3f2e7-111">tooconfigure intégration d’Azure AD avec l’authentification unique de Vault.cloud Veritas Enterprise, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="3f2e7-111">tooconfigure Azure AD integration with Veritas Enterprise Vault.cloud SSO, you need hello following items:</span></span>

- <span data-ttu-id="3f2e7-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f2e7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3f2e7-113">Un abonnement Veritas Enterprise Vault.cloud SSO pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="3f2e7-113">A Veritas Enterprise Vault.cloud SSO single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3f2e7-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3f2e7-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="3f2e7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3f2e7-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3f2e7-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3f2e7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3f2e7-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="3f2e7-118">Scenario description</span></span>
<span data-ttu-id="3f2e7-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3f2e7-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="3f2e7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3f2e7-121">Ajout de l’authentification unique de Veritas Enterprise Vault.cloud à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="3f2e7-121">Adding Veritas Enterprise Vault.cloud SSO from hello gallery</span></span>
2. <span data-ttu-id="3f2e7-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f2e7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-veritas-enterprise-vaultcloud-sso-from-hello-gallery"></a><span data-ttu-id="3f2e7-123">Ajout de l’authentification unique de Veritas Enterprise Vault.cloud à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="3f2e7-123">Adding Veritas Enterprise Vault.cloud SSO from hello gallery</span></span>
<span data-ttu-id="3f2e7-124">tooconfigure hello intégration de l’authentification unique de Veritas Enterprise Vault.cloud dans Azure AD, vous devez tooadd Veritas Enterprise Vault.cloud SSO à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-124">tooconfigure hello integration of Veritas Enterprise Vault.cloud SSO into Azure AD, you need tooadd Veritas Enterprise Vault.cloud SSO from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3f2e7-125">**tooadd Veritas Enterprise Vault.cloud SSO à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3f2e7-125">**tooadd Veritas Enterprise Vault.cloud SSO from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3f2e7-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3f2e7-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3f2e7-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="3f2e7-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="3f2e7-133">Dans la zone de recherche de hello, tapez **Vault.cloud SSO de l’entreprise Veritas**.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-133">In hello search box, type **Veritas Enterprise Vault.cloud SSO**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_search.png)

5. <span data-ttu-id="3f2e7-135">Dans le volet de résultats hello, sélectionnez **Veritas Enterprise SSO de Vault.cloud**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-135">In hello results panel, select **Veritas Enterprise Vault.cloud SSO**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3f2e7-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f2e7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3f2e7-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Veritas Enterprise Vault.cloud SSO, en tirant parti d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="3f2e7-138">In this section, you configure and test Azure AD single sign-on with Veritas Enterprise Vault.cloud SSO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3f2e7-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Veritas Enterprise Vault.cloud SSO est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Veritas Enterprise Vault.cloud SSO is tooa user in Azure AD.</span></span> <span data-ttu-id="3f2e7-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans l’authentification unique de Veritas Enterprise Vault.cloud hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-140">In other words, a link relationship between an Azure AD user and hello related user in Veritas Enterprise Vault.cloud SSO needs toobe established.</span></span>

<span data-ttu-id="3f2e7-141">Dans l’entreprise Veritas Vault.cloud SSO, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-141">In Veritas Enterprise Vault.cloud SSO, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3f2e7-142">tooconfigure et test Azure AD l’authentification unique avec l’authentification unique de Vault.cloud Veritas Enterprise, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="3f2e7-142">tooconfigure and test Azure AD single sign-on with Veritas Enterprise Vault.cloud SSO, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3f2e7-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3f2e7-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3f2e7-145">**[Création d’un utilisateur de test de l’authentification unique de Veritas Enterprise Vault.cloud](#creating-a-veritas-enterprise-vaultcloud-sso-test-user)**  -toohave un équivalent de Britta Simon dans Veritas Enterprise Vault.cloud l’authentification unique qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-145">**[Creating a Veritas Enterprise Vault.cloud SSO test user](#creating-a-veritas-enterprise-vaultcloud-sso-test-user)** - toohave a counterpart of Britta Simon in Veritas Enterprise Vault.cloud SSO that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3f2e7-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3f2e7-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3f2e7-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f2e7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3f2e7-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Veritas Enterprise Vault.cloud SSO.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Veritas Enterprise Vault.cloud SSO application.</span></span>

<span data-ttu-id="3f2e7-150">**tooconfigure Azure AD l’authentification unique avec l’authentification unique de Veritas Enterprise Vault.cloud, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3f2e7-150">**tooconfigure Azure AD single sign-on with Veritas Enterprise Vault.cloud SSO, perform hello following steps:**</span></span>

1. <span data-ttu-id="3f2e7-151">Bonjour portail Azure, sur hello **Veritas Enterprise SSO de Vault.cloud** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-151">In hello Azure portal, on hello **Veritas Enterprise Vault.cloud SSO** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="3f2e7-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_samlbase.png)

3. <span data-ttu-id="3f2e7-155">Sur hello **URL et le domaine de l’authentification unique de Veritas Enterprise Vault.cloud** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="3f2e7-155">On hello **Veritas Enterprise Vault.cloud SSO Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_url.png)

    <span data-ttu-id="3f2e7-157">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://personal.ap.archive.veritas.com/CID=<CUSTOMERID>`</span><span class="sxs-lookup"><span data-stu-id="3f2e7-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://personal.ap.archive.veritas.com/CID=<CUSTOMERID>`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="3f2e7-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-158">This value is not real.</span></span> <span data-ttu-id="3f2e7-159">Mettre à jour de cette valeur avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="3f2e7-160">Contact [équipe de support Client de SSO Veritas Enterprise Vault.cloud](https://www.veritas.com/support/.html) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-160">Contact [Veritas Enterprise Vault.cloud SSO Client support team](https://www.veritas.com/support/.html) tooget this value.</span></span> 

4. <span data-ttu-id="3f2e7-161">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_certificate.png) 

5. <span data-ttu-id="3f2e7-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="3f2e7-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-veritas-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3f2e7-165">Sur hello **Configuration de SSO Veritas Enterprise Vault.cloud** , cliquez sur **configurer Veritas Enterprise Vault.cloud SSO** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-165">On hello **Veritas Enterprise Vault.cloud SSO Configuration** section, click **Configure Veritas Enterprise Vault.cloud SSO** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="3f2e7-166">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="3f2e7-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_configure.png) 

7. <span data-ttu-id="3f2e7-168">tooconfigure l’authentification unique sur **Veritas Enterprise SSO de Vault.cloud** côté, vous devez hello toosend téléchargé **Certificate(Base64)** et **SAML Sign-On URL du Service unique**trop[équipe de support technique de l’authentification unique de Veritas Enterprise Vault.cloud](https://www.veritas.com/support/.html).</span><span class="sxs-lookup"><span data-stu-id="3f2e7-168">tooconfigure single sign-on on **Veritas Enterprise Vault.cloud SSO** side, you need toosend hello downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** too[Veritas Enterprise Vault.cloud SSO support team](https://www.veritas.com/support/.html).</span></span>

> [!TIP]
> <span data-ttu-id="3f2e7-169">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="3f2e7-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3f2e7-170">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3f2e7-171">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3f2e7-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3f2e7-172">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f2e7-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="3f2e7-173">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="3f2e7-175">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3f2e7-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3f2e7-176">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-veritas-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3f2e7-178">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-veritas-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3f2e7-180">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-veritas-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3f2e7-182">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="3f2e7-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-veritas-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3f2e7-184">a.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-184">a.</span></span> <span data-ttu-id="3f2e7-185">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3f2e7-186">b.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-186">b.</span></span> <span data-ttu-id="3f2e7-187">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3f2e7-188">c.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-188">c.</span></span> <span data-ttu-id="3f2e7-189">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3f2e7-190">d.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-190">d.</span></span> <span data-ttu-id="3f2e7-191">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-191">Click **Create**.</span></span>
 
### <a name="creating-a-veritas-enterprise-vaultcloud-sso-test-user"></a><span data-ttu-id="3f2e7-192">Création d’un utilisateur de test Veritas Enterprise Vault.cloud SSO</span><span class="sxs-lookup"><span data-stu-id="3f2e7-192">Creating a Veritas Enterprise Vault.cloud SSO test user</span></span>

<span data-ttu-id="3f2e7-193">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Enterprise Vault.cloud SSO.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-193">In this section, you create a user called Britta Simon in Enterprise Vault.cloud SSO.</span></span> <span data-ttu-id="3f2e7-194">Travailler avec [équipe de support technique de l’authentification unique de Veritas Enterprise Vault.cloud](https://www.veritas.com/support/.html) pour ajouter des utilisateurs de hello dans la plateforme de l’entreprise Vault.cloud SSO hello.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-194">Work with [Veritas Enterprise Vault.cloud SSO support team](https://www.veritas.com/support/.html) to add hello users in hello Enterprise Vault.cloud SSO platform.</span></span> <span data-ttu-id="3f2e7-195">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-195">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3f2e7-196">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f2e7-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3f2e7-197">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooVeritas Vault.cloud SSO de l’entreprise.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooVeritas Enterprise Vault.cloud SSO.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="3f2e7-199">**tooassign Britta Simon tooVeritas Enterprise Vault.cloud SSO, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3f2e7-199">**tooassign Britta Simon tooVeritas Enterprise Vault.cloud SSO, perform hello following steps:**</span></span>

1. <span data-ttu-id="3f2e7-200">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="3f2e7-202">Dans la liste des applications hello, sélectionnez **Vault.cloud SSO de l’entreprise Veritas**.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-202">In hello applications list, select **Veritas Enterprise Vault.cloud SSO**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_app.png) 

3. <span data-ttu-id="3f2e7-204">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="3f2e7-206">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-206">Click **Add** button.</span></span> <span data-ttu-id="3f2e7-207">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="3f2e7-209">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3f2e7-210">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3f2e7-211">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3f2e7-212">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="3f2e7-212">Testing single sign-on</span></span>

<span data-ttu-id="3f2e7-213">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-213">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3f2e7-214">Lorsque vous cliquez sur mosaïque de Veritas Enterprise Vault.cloud SSO hello Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour application Veritas Enterprise Vault.cloud SSO.</span><span class="sxs-lookup"><span data-stu-id="3f2e7-214">When you click hello Veritas Enterprise Vault.cloud SSO tile in hello Access Panel, you should get automatically signed-on tooyour Veritas Enterprise Vault.cloud SSO application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3f2e7-215">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="3f2e7-215">Additional resources</span></span>

* [<span data-ttu-id="3f2e7-216">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3f2e7-216">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3f2e7-217">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="3f2e7-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_203.png

