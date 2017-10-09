---
title: "Didacticiel : Intégration d’Azure Active Directory à ScreenSteps | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de ScreenSteps."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4563fe94-a88f-4895-a07f-79df44889cf9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: fd041e5fe4552727eeda2dabc1773d8043d410f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-screensteps"></a><span data-ttu-id="16860-103">Didacticiel : Intégration d’Azure AD à ScreenSteps</span><span class="sxs-lookup"><span data-stu-id="16860-103">Tutorial: Azure Active Directory integration with ScreenSteps</span></span>

<span data-ttu-id="16860-104">Dans ce didacticiel, vous apprendrez comment toointegrate ScreenSteps avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="16860-104">In this tutorial, you learn how toointegrate ScreenSteps with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="16860-105">Intégration de ScreenSteps à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="16860-105">Integrating ScreenSteps with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="16860-106">Vous pouvez contrôler dans Azure AD qui a accès tooScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="16860-106">You can control in Azure AD who has access tooScreenSteps.</span></span>
- <span data-ttu-id="16860-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooScreenSteps (Single Sign-On) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="16860-107">You can enable your users tooautomatically get signed-on tooScreenSteps (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="16860-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="16860-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="16860-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="16860-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16860-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="16860-110">Prerequisites</span></span>

<span data-ttu-id="16860-111">tooconfigure intégration d’Azure AD à ScreenSteps, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="16860-111">tooconfigure Azure AD integration with ScreenSteps, you need hello following items:</span></span>

- <span data-ttu-id="16860-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="16860-112">An Azure AD subscription</span></span>
- <span data-ttu-id="16860-113">Un abonnement ScreenSteps pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="16860-113">A ScreenSteps single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="16860-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="16860-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="16860-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="16860-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="16860-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="16860-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="16860-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="16860-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="16860-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="16860-118">Scenario description</span></span>
<span data-ttu-id="16860-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="16860-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="16860-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="16860-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="16860-121">Ajout de ScreenSteps à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="16860-121">Adding ScreenSteps from hello gallery</span></span>
2. <span data-ttu-id="16860-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="16860-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-screensteps-from-hello-gallery"></a><span data-ttu-id="16860-123">Ajout de ScreenSteps à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="16860-123">Adding ScreenSteps from hello gallery</span></span>
<span data-ttu-id="16860-124">intégration de hello tooconfigure de ScreenSteps dans Azure AD, vous devez tooadd ScreenSteps à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="16860-124">tooconfigure hello integration of ScreenSteps into Azure AD, you need tooadd ScreenSteps from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="16860-125">**tooadd ScreenSteps à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="16860-125">**tooadd ScreenSteps from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="16860-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="16860-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="16860-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="16860-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="16860-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="16860-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="16860-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="16860-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="16860-133">Dans la zone de recherche de hello, tapez **ScreenSteps**, sélectionnez **ScreenSteps** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="16860-133">In hello search box, type **ScreenSteps**, select **ScreenSteps** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Liste des résultats de ScreenSteps Bonjour](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="16860-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="16860-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="16860-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec ScreenSteps avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="16860-136">In this section, you configure and test Azure AD single sign-on with ScreenSteps based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="16860-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans ScreenSteps est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="16860-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ScreenSteps is tooa user in Azure AD.</span></span> <span data-ttu-id="16860-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans ScreenSteps doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="16860-138">In other words, a link relationship between an Azure AD user and hello related user in ScreenSteps needs toobe established.</span></span>

<span data-ttu-id="16860-139">Dans ScreenSteps, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="16860-139">In ScreenSteps, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="16860-140">tooconfigure et test Azure AD l’authentification unique à ScreenSteps, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="16860-140">tooconfigure and test Azure AD single sign-on with ScreenSteps, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="16860-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="16860-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="16860-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="16860-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="16860-143">**[Créer un utilisateur de test de ScreenSteps](#create-a-screensteps-test-user)**  -toohave un équivalent de Britta Simon dans ScreenSteps est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="16860-143">**[Create a ScreenSteps test user](#create-a-screensteps-test-user)** - toohave a counterpart of Britta Simon in ScreenSteps that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="16860-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="16860-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="16860-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="16860-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="16860-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="16860-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="16860-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="16860-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ScreenSteps application.</span></span>

<span data-ttu-id="16860-148">**tooconfigure Azure AD single sign-on avec ScreenSteps, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="16860-148">**tooconfigure Azure AD single sign-on with ScreenSteps, perform hello following steps:**</span></span>

1. <span data-ttu-id="16860-149">Bonjour portail Azure, sur hello **ScreenSteps** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="16860-149">In hello Azure portal, on hello **ScreenSteps** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="16860-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="16860-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_samlbase.png)

3. <span data-ttu-id="16860-153">Sur hello **ScreenSteps domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="16860-153">On hello **ScreenSteps Domain and URLs** section, perform hello following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL ScreenSteps](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_url.png)

    <span data-ttu-id="16860-155">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<tenantname>.ScreenSteps.com`</span><span class="sxs-lookup"><span data-stu-id="16860-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.ScreenSteps.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="16860-156">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="16860-156">This value is not real.</span></span> <span data-ttu-id="16860-157">Mettre à jour de cette valeur avec hello Sign-On URL réelle, ce qui est expliqué plus loin dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="16860-157">Update this value with hello actual Sign-On URL, which is explained later in this tutorial.</span></span> 

4. <span data-ttu-id="16860-158">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="16860-158">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_certificate.png) 

5. <span data-ttu-id="16860-160">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="16860-160">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-screensteps-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="16860-162">Sur hello **ScreenSteps Configuration** , cliquez sur **configurer de ScreenSteps** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="16860-162">On hello **ScreenSteps Configuration** section, click **Configure ScreenSteps** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="16860-163">Hello de copie **URL de déconnexion et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="16860-163">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuration de ScreenSteps](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_configure.png) 

7. <span data-ttu-id="16860-165">Dans une autre fenêtre de navigateur web, connectez-vous au site de votre entreprise ScreenSteps en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="16860-165">In a different web browser window, log into your ScreenSteps company site as an administrator.</span></span>

8. <span data-ttu-id="16860-166">Cliquez sur **Account Settings** (Paramètres du compte).</span><span class="sxs-lookup"><span data-stu-id="16860-166">Click **Account Settings**.</span></span>

    <span data-ttu-id="16860-167">![Account management](./media/active-directory-saas-screensteps-tutorial/ic778523.png "Account management")</span><span class="sxs-lookup"><span data-stu-id="16860-167">![Account management](./media/active-directory-saas-screensteps-tutorial/ic778523.png "Account management")</span></span>

9. <span data-ttu-id="16860-168">Cliquez sur **Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="16860-168">Click **Single Sign-on**.</span></span>

    <span data-ttu-id="16860-169">![Remote authentication](./media/active-directory-saas-screensteps-tutorial/ic778524.png "Remote authentication")</span><span class="sxs-lookup"><span data-stu-id="16860-169">![Remote authentication](./media/active-directory-saas-screensteps-tutorial/ic778524.png "Remote authentication")</span></span>

10. <span data-ttu-id="16860-170">Cliquez sur **Créer un point de terminaison d’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="16860-170">Click **Create Single Sign-on Endpoint**.</span></span>

    <span data-ttu-id="16860-171">![Remote authentication](./media/active-directory-saas-screensteps-tutorial/ic778525.png "Remote authentication")</span><span class="sxs-lookup"><span data-stu-id="16860-171">![Remote authentication](./media/active-directory-saas-screensteps-tutorial/ic778525.png "Remote authentication")</span></span>

11. <span data-ttu-id="16860-172">Bonjour **créer de session point de terminaison unique** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="16860-172">In hello **Create Single Sign-on Endpoint** section, perform hello following steps:</span></span>

    <span data-ttu-id="16860-173">![Create an authentication endpoint](./media/active-directory-saas-screensteps-tutorial/ic778526.png "Create an authentication endpoint")</span><span class="sxs-lookup"><span data-stu-id="16860-173">![Create an authentication endpoint](./media/active-directory-saas-screensteps-tutorial/ic778526.png "Create an authentication endpoint")</span></span>
    
    <span data-ttu-id="16860-174">a.</span><span class="sxs-lookup"><span data-stu-id="16860-174">a.</span></span> <span data-ttu-id="16860-175">Bonjour **titre** zone de texte, tapez un titre.</span><span class="sxs-lookup"><span data-stu-id="16860-175">In hello **Title** textbox, type a title.</span></span>
    
    <span data-ttu-id="16860-176">b.</span><span class="sxs-lookup"><span data-stu-id="16860-176">b.</span></span> <span data-ttu-id="16860-177">À partir de hello **Mode** liste, sélectionnez **SAML**.</span><span class="sxs-lookup"><span data-stu-id="16860-177">From hello **Mode** list, select **SAML**.</span></span>
    
    <span data-ttu-id="16860-178">c.</span><span class="sxs-lookup"><span data-stu-id="16860-178">c.</span></span> <span data-ttu-id="16860-179">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="16860-179">Click **Create**.</span></span>

12. <span data-ttu-id="16860-180">**Modifier** hello nouveau point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="16860-180">**Edit** hello new endpoint.</span></span>

    <span data-ttu-id="16860-181">![Modifier un point de terminaison](./media/active-directory-saas-screensteps-tutorial/ic778528.png "Modifier un point de terminaison")</span><span class="sxs-lookup"><span data-stu-id="16860-181">![Edit endpoint](./media/active-directory-saas-screensteps-tutorial/ic778528.png "Edit endpoint")</span></span>

13. <span data-ttu-id="16860-182">Bonjour **modifier l’authentification sur point de terminaison unique** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="16860-182">In hello **Edit Single Sign-on Endpoint** section, perform hello following steps:</span></span>

    <span data-ttu-id="16860-183">![Remote authentication endpoint](./media/active-directory-saas-screensteps-tutorial/ic778527.png "Remote authentication endpoint")</span><span class="sxs-lookup"><span data-stu-id="16860-183">![Remote authentication endpoint](./media/active-directory-saas-screensteps-tutorial/ic778527.png "Remote authentication endpoint")</span></span>

    <span data-ttu-id="16860-184">a.</span><span class="sxs-lookup"><span data-stu-id="16860-184">a.</span></span> <span data-ttu-id="16860-185">Cliquez sur **nouveau fichier de certificat SAML téléchargement**et puis télécharger hello le certificat, laquelle vous avez téléchargé à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="16860-185">Click **Upload new SAML Certificate file**, and then upload hello certificate, which you have downloaded from Azure portal.</span></span>
    
    <span data-ttu-id="16860-186">b.</span><span class="sxs-lookup"><span data-stu-id="16860-186">b.</span></span> <span data-ttu-id="16860-187">Coller **SAML Sign-On URL du Service unique** valeur, ce qui vous avez copié à partir de hello portail Azure en hello **URL de connexion distante** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="16860-187">Paste **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **Remote Login URL** textbox.</span></span>
    
    <span data-ttu-id="16860-188">c.</span><span class="sxs-lookup"><span data-stu-id="16860-188">c.</span></span> <span data-ttu-id="16860-189">Coller **URL de déconnexion** valeur, ce qui vous avez copié à partir de hello portail Azure en hello **URL de déconnexion** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="16860-189">Paste **Sign-Out URL** value, which you have copied from hello Azure portal into hello **Log out URL** textbox.</span></span>
    
    <span data-ttu-id="16860-190">d.</span><span class="sxs-lookup"><span data-stu-id="16860-190">d.</span></span> <span data-ttu-id="16860-191">Sélectionnez un **groupe** toowhen d’utilisateurs tooassign qu’ils sont configurés.</span><span class="sxs-lookup"><span data-stu-id="16860-191">Select a **Group** tooassign users toowhen they are provisioned.</span></span>
    
    <span data-ttu-id="16860-192">e.</span><span class="sxs-lookup"><span data-stu-id="16860-192">e.</span></span> <span data-ttu-id="16860-193">Cliquez sur **Update**.</span><span class="sxs-lookup"><span data-stu-id="16860-193">Click **Update**.</span></span>

    <span data-ttu-id="16860-194">f.</span><span class="sxs-lookup"><span data-stu-id="16860-194">f.</span></span> <span data-ttu-id="16860-195">Hello de copie **SAML consommateur URL** toohello Presse-papiers et coller dans toohello **URL de connexion** zone de texte dans **ScreenSteps domaine et les URL** section.</span><span class="sxs-lookup"><span data-stu-id="16860-195">Copy hello **SAML Consumer URL** toohello clipboard and paste in toohello **Sign-on URL** textbox in **ScreenSteps Domain and URLs** section.</span></span>
    
    <span data-ttu-id="16860-196">g.</span><span class="sxs-lookup"><span data-stu-id="16860-196">g.</span></span> <span data-ttu-id="16860-197">Retourner toohello **modifier l’authentification sur point de terminaison unique**.</span><span class="sxs-lookup"><span data-stu-id="16860-197">Return toohello **Edit Single Sign-on Endpoint**.</span></span>
    
    <span data-ttu-id="16860-198">h.</span><span class="sxs-lookup"><span data-stu-id="16860-198">h.</span></span> <span data-ttu-id="16860-199">Cliquez sur hello **par défaut pour le compte** bouton toouse ce point de terminaison pour tous les utilisateurs qui se connectent à ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="16860-199">Click hello **Make default for account** button toouse this endpoint for all users who log into ScreenSteps.</span></span> <span data-ttu-id="16860-200">Vous pouvez également cliquer sur hello **ajouter tooSite** bouton toouse ce point de terminaison pour des sites spécifiques dans **ScreenSteps**.</span><span class="sxs-lookup"><span data-stu-id="16860-200">Alternatively you can click hello **Add tooSite** button toouse this endpoint for specific sites in **ScreenSteps**.</span></span>

> [!TIP]
> <span data-ttu-id="16860-201">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="16860-201">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="16860-202">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="16860-202">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="16860-203">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="16860-203">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="16860-204">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="16860-204">Create an Azure AD test user</span></span>

<span data-ttu-id="16860-205">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="16860-205">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="16860-207">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="16860-207">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="16860-208">Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="16860-208">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-screensteps-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="16860-210">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="16860-210">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-screensteps-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="16860-212">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="16860-212">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![bouton Ajouter de Hello](./media/active-directory-saas-screensteps-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="16860-214">Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="16860-214">In hello **User** dialog box, perform hello following steps:</span></span>

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-screensteps-tutorial/create_aaduser_04.png)

    <span data-ttu-id="16860-216">a.</span><span class="sxs-lookup"><span data-stu-id="16860-216">a.</span></span> <span data-ttu-id="16860-217">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="16860-217">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="16860-218">b.</span><span class="sxs-lookup"><span data-stu-id="16860-218">b.</span></span> <span data-ttu-id="16860-219">Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="16860-219">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="16860-220">c.</span><span class="sxs-lookup"><span data-stu-id="16860-220">c.</span></span> <span data-ttu-id="16860-221">Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="16860-221">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="16860-222">d.</span><span class="sxs-lookup"><span data-stu-id="16860-222">d.</span></span> <span data-ttu-id="16860-223">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="16860-223">Click **Create**.</span></span>
 
### <a name="create-a-screensteps-test-user"></a><span data-ttu-id="16860-224">Créer un utilisateur de test ScreenSteps</span><span class="sxs-lookup"><span data-stu-id="16860-224">Create a ScreenSteps test user</span></span>

<span data-ttu-id="16860-225">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="16860-225">In this section, you create a user called Britta Simon in ScreenSteps.</span></span> <span data-ttu-id="16860-226">Travailler avec [équipe de support Client de ScreenSteps](https://www.screensteps.com/contact) pour ajouter des utilisateurs de hello de plateforme de ScreenSteps hello.</span><span class="sxs-lookup"><span data-stu-id="16860-226">Work with [ScreenSteps Client support team](https://www.screensteps.com/contact) to add hello users in hello ScreenSteps platform.</span></span> <span data-ttu-id="16860-227">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="16860-227">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="16860-228">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="16860-228">Assign hello Azure AD test user</span></span>

<span data-ttu-id="16860-229">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="16860-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooScreenSteps.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="16860-231">**tooassign Britta Simon tooScreenSteps, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="16860-231">**tooassign Britta Simon tooScreenSteps, perform hello following steps:**</span></span>

1. <span data-ttu-id="16860-232">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="16860-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="16860-234">Dans la liste des applications hello, sélectionnez **ScreenSteps**.</span><span class="sxs-lookup"><span data-stu-id="16860-234">In hello applications list, select **ScreenSteps**.</span></span>

    ![lien de ScreenSteps Hello dans la liste des Applications hello](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_app.png)  

3. <span data-ttu-id="16860-236">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="16860-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202]

4. <span data-ttu-id="16860-238">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="16860-238">Click **Add** button.</span></span> <span data-ttu-id="16860-239">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="16860-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="16860-241">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="16860-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="16860-242">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="16860-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="16860-243">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="16860-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="16860-244">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="16860-244">Test single sign-on</span></span>

<span data-ttu-id="16860-245">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="16860-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="16860-246">Lorsque vous cliquez sur hello ScreenSteps vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour ScreenSteps application.</span><span class="sxs-lookup"><span data-stu-id="16860-246">When you click hello ScreenSteps tile in hello Access Panel, you should get automatically signed-on tooyour ScreenSteps application.</span></span>
<span data-ttu-id="16860-247">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="16860-247">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="16860-248">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="16860-248">Additional resources</span></span>

* [<span data-ttu-id="16860-249">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="16860-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="16860-250">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="16860-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_203.png

