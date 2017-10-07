---
title: "Didacticiel : Intégration d’Azure Active Directory avec Mozy Enterprise | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory à Mozy Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 489b5e62-85c2-45c9-8766-326632d48114
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: bab0df4f3621b784cd8edfda3c8e10fe5a7ced9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mozy-enterprise"></a><span data-ttu-id="62018-103">Didacticiel : Intégration d’Azure Active Directory avec Mozy Enterprise</span><span class="sxs-lookup"><span data-stu-id="62018-103">Tutorial: Azure Active Directory integration with Mozy Enterprise</span></span>

<span data-ttu-id="62018-104">Dans ce didacticiel, vous apprendrez comment toointegrate Mozy Enterprise avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="62018-104">In this tutorial, you learn how toointegrate Mozy Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="62018-105">Intégration de Mozy Enterprise à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="62018-105">Integrating Mozy Enterprise with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="62018-106">Vous pouvez contrôler dans Azure AD qui a accès tooMozy Enterprise</span><span class="sxs-lookup"><span data-stu-id="62018-106">You can control in Azure AD who has access tooMozy Enterprise</span></span>
- <span data-ttu-id="62018-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooMozy entreprise (SSO) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="62018-107">You can enable your users tooautomatically get signed-on tooMozy Enterprise (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="62018-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="62018-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="62018-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="62018-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="62018-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="62018-110">Prerequisites</span></span>

<span data-ttu-id="62018-111">tooconfigure intégration d’Azure AD à Mozy Enterprise, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="62018-111">tooconfigure Azure AD integration with Mozy Enterprise, you need hello following items:</span></span>

- <span data-ttu-id="62018-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="62018-112">An Azure AD subscription</span></span>
- <span data-ttu-id="62018-113">Un abonnement Mozy Enterprise pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="62018-113">A Mozy Enterprise single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="62018-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="62018-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="62018-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="62018-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="62018-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="62018-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="62018-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="62018-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="62018-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="62018-118">Scenario description</span></span>
<span data-ttu-id="62018-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="62018-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="62018-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="62018-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="62018-121">Ajout de Mozy Enterprise à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="62018-121">Adding Mozy Enterprise from hello gallery</span></span>
2. <span data-ttu-id="62018-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="62018-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mozy-enterprise-from-hello-gallery"></a><span data-ttu-id="62018-123">Ajout de Mozy Enterprise à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="62018-123">Adding Mozy Enterprise from hello gallery</span></span>
<span data-ttu-id="62018-124">intégration de hello tooconfigure de Mozy Enterprise à Azure AD, vous devez tooadd Mozy Enterprise à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="62018-124">tooconfigure hello integration of Mozy Enterprise into Azure AD, you need tooadd Mozy Enterprise from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="62018-125">**tooadd Mozy Enterprise à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="62018-125">**tooadd Mozy Enterprise from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="62018-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="62018-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="62018-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="62018-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="62018-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="62018-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="62018-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="62018-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="62018-133">Dans la zone de recherche de hello, tapez **Mozy Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="62018-133">In hello search box, type **Mozy Enterprise**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_search.png)

5. <span data-ttu-id="62018-135">Dans le volet de résultats hello, sélectionnez **Mozy Enterprise**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="62018-135">In hello results panel, select **Mozy Enterprise**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="62018-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="62018-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="62018-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Mozy Enterprise avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="62018-138">In this section, you configure and test Azure AD single sign-on with Mozy Enterprise based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="62018-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Mozy Enterprise est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="62018-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mozy Enterprise is tooa user in Azure AD.</span></span> <span data-ttu-id="62018-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Mozy Enterprise doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="62018-140">In other words, a link relationship between an Azure AD user and hello related user in Mozy Enterprise needs toobe established.</span></span>

<span data-ttu-id="62018-141">Dans Mozy Enterprise, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="62018-141">In Mozy Enterprise, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="62018-142">tooconfigure et test Azure AD l’authentification unique à Mozy Enterprise, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="62018-142">tooconfigure and test Azure AD single sign-on with Mozy Enterprise, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="62018-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="62018-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="62018-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="62018-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="62018-145">**[Création d’un utilisateur de test de Mozy Enterprise](#creating-a-mozy-enterprise-test-user)**  -toohave un équivalent de Britta Simon dans Mozy Enterprise qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="62018-145">**[Creating a Mozy Enterprise test user](#creating-a-mozy-enterprise-test-user)** - toohave a counterpart of Britta Simon in Mozy Enterprise that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="62018-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="62018-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="62018-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="62018-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="62018-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="62018-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="62018-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="62018-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mozy Enterprise application.</span></span>

<span data-ttu-id="62018-150">**tooconfigure Azure AD single sign-on avec Mozy Enterprise, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="62018-150">**tooconfigure Azure AD single sign-on with Mozy Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="62018-151">Bonjour portail Azure, sur hello **Mozy Enterprise** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="62018-151">In hello Azure portal, on hello **Mozy Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="62018-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="62018-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_samlbase.png)

3. <span data-ttu-id="62018-155">Sur hello **URL et le domaine d’entreprise Mozy** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="62018-155">On hello **Mozy Enterprise Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_url.png)

    <span data-ttu-id="62018-157">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<tenantname>.Mozyenterprise.com`</span><span class="sxs-lookup"><span data-stu-id="62018-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.Mozyenterprise.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="62018-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="62018-158">This value is not real.</span></span> <span data-ttu-id="62018-159">Mettre à jour de cette valeur avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="62018-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="62018-160">Contact [équipe de support technique de Mozy Enterprise Client](http://support.mozy.com/) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="62018-160">Contact [Mozy Enterprise Client support team](http://support.mozy.com/) tooget this value.</span></span>

4. <span data-ttu-id="62018-161">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="62018-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_certificate.png) 

5. <span data-ttu-id="62018-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="62018-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="62018-165">Sur hello **Mozy Enterprise Configuration** , cliquez sur **configurer Mozy Enterprise** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="62018-165">On hello **Mozy Enterprise Configuration** section, click **Configure Mozy Enterprise** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="62018-166">Hello de copie **ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="62018-166">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_configure.png) 

7. <span data-ttu-id="62018-168">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Mozy Enterprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="62018-168">In a different web browser window, log into your Mozy Enterprise company site as an administrator.</span></span>

8. <span data-ttu-id="62018-169">Bonjour **Configuration** , cliquez sur **stratégie d’authentification**.</span><span class="sxs-lookup"><span data-stu-id="62018-169">In hello **Configuration** section, click **Authentication Policy**.</span></span>
   
   <span data-ttu-id="62018-170">![Stratégie d’authentification](./media/active-directory-saas-mozy-enterprise-tutorial/ic777314.png "Stratégie d’authentification")</span><span class="sxs-lookup"><span data-stu-id="62018-170">![Authentication policy](./media/active-directory-saas-mozy-enterprise-tutorial/ic777314.png "Authentication policy")</span></span>

9. <span data-ttu-id="62018-171">Sur hello **stratégie d’authentification** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="62018-171">On hello **Authentication Policy** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="62018-172">![Stratégie d’authentification](./media/active-directory-saas-mozy-enterprise-tutorial/ic777315.png "Stratégie d’authentification")</span><span class="sxs-lookup"><span data-stu-id="62018-172">![Authentication policy](./media/active-directory-saas-mozy-enterprise-tutorial/ic777315.png "Authentication policy")</span></span>
   
   <span data-ttu-id="62018-173">a.</span><span class="sxs-lookup"><span data-stu-id="62018-173">a.</span></span> <span data-ttu-id="62018-174">Sélectionnez **Directory Service** comme **Provider**.</span><span class="sxs-lookup"><span data-stu-id="62018-174">Select **Directory Service** as **Provider**.</span></span>
   
   <span data-ttu-id="62018-175">b.</span><span class="sxs-lookup"><span data-stu-id="62018-175">b.</span></span> <span data-ttu-id="62018-176">Sélectionnez **Use LDAP Push**.</span><span class="sxs-lookup"><span data-stu-id="62018-176">Select **Use LDAP Push**.</span></span>
   
   <span data-ttu-id="62018-177">c.</span><span class="sxs-lookup"><span data-stu-id="62018-177">c.</span></span> <span data-ttu-id="62018-178">Cliquez sur hello **l’authentification SAML** onglet.</span><span class="sxs-lookup"><span data-stu-id="62018-178">Click hello **SAML Authentication** tab.</span></span>
   
   <span data-ttu-id="62018-179">d.</span><span class="sxs-lookup"><span data-stu-id="62018-179">d.</span></span> <span data-ttu-id="62018-180">Coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir de hello portail Azure en hello **URL d’authentification** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="62018-180">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **Authentication URL** textbox.</span></span>
   
   <span data-ttu-id="62018-181">e.</span><span class="sxs-lookup"><span data-stu-id="62018-181">e.</span></span> <span data-ttu-id="62018-182">Coller **ID d’entité SAML**, lequel vous avez copié à partir de hello portail Azure en hello **point de terminaison SAML** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="62018-182">Paste **SAML Entity ID**, which you have copied from hello Azure portal into hello **SAML Endpoint** textbox.</span></span>
   
   <span data-ttu-id="62018-183">f.</span><span class="sxs-lookup"><span data-stu-id="62018-183">f.</span></span> <span data-ttu-id="62018-184">Ouvrez votre certificat codé en base 64 dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et collez hello l’intégralité du certificat dans **certificat SAML** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="62018-184">Open your downloaded base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste hello entire Certificate into **SAML Certificate** textbox.</span></span>
   
   <span data-ttu-id="62018-185">g.</span><span class="sxs-lookup"><span data-stu-id="62018-185">g.</span></span> <span data-ttu-id="62018-186">Sélectionnez **activer authentification unique pour les administrateurs des toolog avec leurs informations d’identification réseau**.</span><span class="sxs-lookup"><span data-stu-id="62018-186">Select **Enable SSO for Admins toolog in with their network credentials**.</span></span>
   
   <span data-ttu-id="62018-187">h.</span><span class="sxs-lookup"><span data-stu-id="62018-187">h.</span></span> <span data-ttu-id="62018-188">Cliquez sur **Enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="62018-188">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="62018-189">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="62018-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="62018-190">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="62018-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="62018-191">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="62018-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="62018-192">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="62018-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="62018-193">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="62018-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="62018-195">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="62018-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="62018-196">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="62018-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="62018-198">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="62018-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="62018-200">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="62018-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="62018-202">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="62018-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="62018-204">a.</span><span class="sxs-lookup"><span data-stu-id="62018-204">a.</span></span> <span data-ttu-id="62018-205">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="62018-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="62018-206">b.</span><span class="sxs-lookup"><span data-stu-id="62018-206">b.</span></span> <span data-ttu-id="62018-207">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="62018-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="62018-208">c.</span><span class="sxs-lookup"><span data-stu-id="62018-208">c.</span></span> <span data-ttu-id="62018-209">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="62018-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="62018-210">d.</span><span class="sxs-lookup"><span data-stu-id="62018-210">d.</span></span> <span data-ttu-id="62018-211">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="62018-211">Click **Create**.</span></span>
 
### <a name="creating-a-mozy-enterprise-test-user"></a><span data-ttu-id="62018-212">Création d’un utilisateur de test Mozy Enterprise</span><span class="sxs-lookup"><span data-stu-id="62018-212">Creating a Mozy Enterprise test user</span></span>

<span data-ttu-id="62018-213">Dans l’ordre tooenable le toolog d’utilisateurs Azure AD à Mozy Enterprise, vous devez les configurer dans Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="62018-213">In order tooenable Azure AD users toolog into Mozy Enterprise, they must be provisioned into Mozy Enterprise.</span></span> <span data-ttu-id="62018-214">Dans les cas de hello de Mozy Enterprise, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="62018-214">In hello case of Mozy Enterprise, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="62018-215">Vous pouvez utiliser n’importe quel autre Mozy Enterprise utilisateur compte outil de création ou API fournie par Mozy Enterprise tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="62018-215">You can use any other Mozy Enterprise user account creation tools or APIs provided by Mozy Enterprise tooprovision AAD user accounts.</span></span>

<span data-ttu-id="62018-216">**effectuer des comptes d’utilisateur, tooprovision hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="62018-216">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="62018-217">Connectez-vous à tooyour **Mozy Enterprise** client.</span><span class="sxs-lookup"><span data-stu-id="62018-217">Log in tooyour **Mozy Enterprise** tenant.</span></span>

2. <span data-ttu-id="62018-218">Cliquez sur **Users**, puis sur **Add New User**.</span><span class="sxs-lookup"><span data-stu-id="62018-218">Click **Users**, and then click **Add New User**.</span></span>
   
   <span data-ttu-id="62018-219">![Utilisateurs](./media/active-directory-saas-mozy-enterprise-tutorial/ic777317.png "Utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="62018-219">![Users](./media/active-directory-saas-mozy-enterprise-tutorial/ic777317.png "Users")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="62018-220">Hello **ajouter un nouvel utilisateur** option n’est affichée uniquement si **Mozy** est sélectionné en tant que fournisseur hello sous **stratégie d’authentification**.</span><span class="sxs-lookup"><span data-stu-id="62018-220">hello **Add New User** option is only displayed only if **Mozy** is selected as hello provider under **Authentication policy**.</span></span> <span data-ttu-id="62018-221">Si l’authentification SAML est configurée, puis hello utilisateurs sont ajoutés automatiquement lors de leur première connexion via l’authentification unique sur.</span><span class="sxs-lookup"><span data-stu-id="62018-221">If SAML Authentication is configured, then hello users are added automatically on their first login through Single sign on.</span></span>
    
3. <span data-ttu-id="62018-222">Sur hello nouvelle boîte de dialogue utilisateur, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="62018-222">On hello new user dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="62018-223">![Ajouter des utilisateurs](./media/active-directory-saas-mozy-enterprise-tutorial/ic777318.png "ajouter des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="62018-223">![Add Users](./media/active-directory-saas-mozy-enterprise-tutorial/ic777318.png "Add Users")</span></span>
   
   <span data-ttu-id="62018-224">a.</span><span class="sxs-lookup"><span data-stu-id="62018-224">a.</span></span> <span data-ttu-id="62018-225">À partir de hello **choisir un groupe** , sélectionnez un groupe.</span><span class="sxs-lookup"><span data-stu-id="62018-225">From hello **Choose a Group** list, select a group.</span></span>
   
   <span data-ttu-id="62018-226">b.</span><span class="sxs-lookup"><span data-stu-id="62018-226">b.</span></span> <span data-ttu-id="62018-227">À partir de hello **quel type d’utilisateur** , sélectionnez un type.</span><span class="sxs-lookup"><span data-stu-id="62018-227">From hello **What type of user** list, select a type.</span></span>
   
   <span data-ttu-id="62018-228">c.</span><span class="sxs-lookup"><span data-stu-id="62018-228">c.</span></span> <span data-ttu-id="62018-229">Bonjour **nom d’utilisateur** zone de texte Nom hello du type d’utilisateur de hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="62018-229">In hello **Username** textbox, type hello name of hello Azure AD user.</span></span>
   
   <span data-ttu-id="62018-230">d.</span><span class="sxs-lookup"><span data-stu-id="62018-230">d.</span></span> <span data-ttu-id="62018-231">Bonjour **messagerie** zone de texte, tapez Bonjour adresse de messagerie de l’utilisateur de hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="62018-231">In hello **Email** textbox, type hello email address of hello Azure AD user.</span></span>
   
   <span data-ttu-id="62018-232">e.</span><span class="sxs-lookup"><span data-stu-id="62018-232">e.</span></span> <span data-ttu-id="62018-233">Sélectionnez **Send user instruction email**.</span><span class="sxs-lookup"><span data-stu-id="62018-233">Select **Send user instruction email**.</span></span>
   
   <span data-ttu-id="62018-234">f.</span><span class="sxs-lookup"><span data-stu-id="62018-234">f.</span></span> <span data-ttu-id="62018-235">Cliquez sur **Add User(s)**.</span><span class="sxs-lookup"><span data-stu-id="62018-235">Click **Add User(s)**.</span></span>

     >[!NOTE]
     > <span data-ttu-id="62018-236">Après avoir créé un utilisateur de hello, un e-mail sera envoyé utilisateur Azure AD toohello qui inclut un compte de hello tooconfirm lien avant son activation.</span><span class="sxs-lookup"><span data-stu-id="62018-236">After creating hello user, an email will be sent toohello Azure AD user that includes a link tooconfirm hello account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="62018-237">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="62018-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="62018-238">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooMozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="62018-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMozy Enterprise.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="62018-240">**tooassign Britta Simon tooMozy Enterprise, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="62018-240">**tooassign Britta Simon tooMozy Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="62018-241">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="62018-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="62018-243">Dans la liste des applications hello, sélectionnez **Mozy Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="62018-243">In hello applications list, select **Mozy Enterprise**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_app.png) 

3. <span data-ttu-id="62018-245">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="62018-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="62018-247">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="62018-247">Click **Add** button.</span></span> <span data-ttu-id="62018-248">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="62018-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="62018-250">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="62018-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="62018-251">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="62018-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="62018-252">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="62018-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="62018-253">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="62018-253">Testing single sign-on</span></span>

<span data-ttu-id="62018-254">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="62018-254">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="62018-255">Lorsque vous cliquez sur hello Mozy Enterprise vignette Bonjour volet d’accès, vous devez obtenir la page de connexion de l’application de Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="62018-255">When you click hello Mozy Enterprise tile in hello Access Panel, you should get login page of Mozy Enterprise application.</span></span>
<span data-ttu-id="62018-256">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="62018-256">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="62018-257">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="62018-257">Additional resources</span></span>

* [<span data-ttu-id="62018-258">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="62018-258">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="62018-259">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="62018-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_203.png

