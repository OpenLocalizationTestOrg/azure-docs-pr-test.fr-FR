---
title: "Didacticiel : Intégration d’Azure Active Directory à New Relic | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et New Relic."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3186b9a8-f4d8-45e2-ad82-6275f95e7aa6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: dc8f0df3b18a32bde155e8911a581fc5f91af217
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-new-relic"></a><span data-ttu-id="37e5a-103">Didacticiel : Intégration d’Azure Active Directory à New Relic</span><span class="sxs-lookup"><span data-stu-id="37e5a-103">Tutorial: Azure Active Directory integration with New Relic</span></span>

<span data-ttu-id="37e5a-104">Dans ce didacticiel, vous apprendrez comment toointegrate New Relic avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="37e5a-104">In this tutorial, you learn how toointegrate New Relic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="37e5a-105">Intégration de New Relic avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="37e5a-105">Integrating New Relic with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="37e5a-106">Vous pouvez contrôler dans Azure AD qui a accès tooNew Relic</span><span class="sxs-lookup"><span data-stu-id="37e5a-106">You can control in Azure AD who has access tooNew Relic</span></span>
- <span data-ttu-id="37e5a-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooNew Relic (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="37e5a-107">You can enable your users tooautomatically get signed-on tooNew Relic (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="37e5a-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="37e5a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="37e5a-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="37e5a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37e5a-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="37e5a-110">Prerequisites</span></span>

<span data-ttu-id="37e5a-111">tooconfigure intégration d’Azure AD avec New Relic, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="37e5a-111">tooconfigure Azure AD integration with New Relic, you need hello following items:</span></span>

- <span data-ttu-id="37e5a-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="37e5a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="37e5a-113">Un abonnement New Relic pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="37e5a-113">A New Relic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="37e5a-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="37e5a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="37e5a-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="37e5a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="37e5a-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="37e5a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="37e5a-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="37e5a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="37e5a-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="37e5a-118">Scenario description</span></span>
<span data-ttu-id="37e5a-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="37e5a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="37e5a-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="37e5a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="37e5a-121">Ajout de New Relic à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="37e5a-121">Adding New Relic from hello gallery</span></span>
2. <span data-ttu-id="37e5a-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="37e5a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-new-relic-from-hello-gallery"></a><span data-ttu-id="37e5a-123">Ajout de New Relic à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="37e5a-123">Adding New Relic from hello gallery</span></span>
<span data-ttu-id="37e5a-124">tooconfigure hello intégration de New Relic dans Azure AD, vous devez tooadd New Relic à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="37e5a-124">tooconfigure hello integration of New Relic into Azure AD, you need tooadd New Relic from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="37e5a-125">**tooadd New Relic à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="37e5a-125">**tooadd New Relic from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="37e5a-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="37e5a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="37e5a-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="37e5a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="37e5a-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="37e5a-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="37e5a-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="37e5a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="37e5a-133">Dans la zone de recherche de hello, tapez **New Relic**.</span><span class="sxs-lookup"><span data-stu-id="37e5a-133">In hello search box, type **New Relic**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_search.png)

5. <span data-ttu-id="37e5a-135">Dans le volet de résultats hello, sélectionnez **New Relic**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="37e5a-135">In hello results panel, select **New Relic**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="37e5a-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="37e5a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="37e5a-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec New Relic, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="37e5a-138">In this section, you configure and test Azure AD single sign-on with New Relic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="37e5a-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans New Relic est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="37e5a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in New Relic is tooa user in Azure AD.</span></span> <span data-ttu-id="37e5a-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans New Relic doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="37e5a-140">In other words, a link relationship between an Azure AD user and hello related user in New Relic needs toobe established.</span></span>

<span data-ttu-id="37e5a-141">Dans New Relic, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="37e5a-141">In New Relic, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="37e5a-142">tooconfigure et test Azure AD l’authentification unique avec New Relic, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="37e5a-142">tooconfigure and test Azure AD single sign-on with New Relic, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="37e5a-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="37e5a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="37e5a-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="37e5a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="37e5a-145">**[Création d’un utilisateur de test New Relic](#creating-a-new-relic-test-user)**  -toohave un équivalent de Britta Simon dans New Relic est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="37e5a-145">**[Creating a New Relic test user](#creating-a-new-relic-test-user)** - toohave a counterpart of Britta Simon in New Relic that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="37e5a-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="37e5a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="37e5a-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="37e5a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="37e5a-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="37e5a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="37e5a-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application New Relic.</span><span class="sxs-lookup"><span data-stu-id="37e5a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your New Relic application.</span></span>

<span data-ttu-id="37e5a-150">**tooconfigure Azure AD single sign-on avec New Relic, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="37e5a-150">**tooconfigure Azure AD single sign-on with New Relic, perform hello following steps:**</span></span>

1. <span data-ttu-id="37e5a-151">Bonjour portail Azure, sur hello **New Relic** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="37e5a-151">In hello Azure portal, on hello **New Relic** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="37e5a-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="37e5a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_samlbase.png)

3. <span data-ttu-id="37e5a-155">Sur hello **URL et le nouveau domaine Relic** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="37e5a-155">On hello **New Relic Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_url.png)

    <span data-ttu-id="37e5a-157">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.newrelic.com`</span><span class="sxs-lookup"><span data-stu-id="37e5a-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.newrelic.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="37e5a-158">valeur de Hello n’est pas réelle.</span><span class="sxs-lookup"><span data-stu-id="37e5a-158">hello value is not real.</span></span> <span data-ttu-id="37e5a-159">Valeur de hello de mise à jour avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="37e5a-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="37e5a-160">Contact [équipe de support technique de nouveau Client Relic](https://support.newrelic.com/) valeur hello de tooget.</span><span class="sxs-lookup"><span data-stu-id="37e5a-160">Contact [New Relic Client support team](https://support.newrelic.com/) tooget hello value.</span></span> 
 
4. <span data-ttu-id="37e5a-161">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="37e5a-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_certificate.png) 

5. <span data-ttu-id="37e5a-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="37e5a-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-new-relic-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="37e5a-165">Sur hello **nouvelle Configuration Relic** , cliquez sur **configurer New Relic** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="37e5a-165">On hello **New Relic Configuration** section, click **Configure New Relic** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="37e5a-166">Hello de copie **URL de déconnexion et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="37e5a-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_configure.png) 

7. <span data-ttu-id="37e5a-168">Dans une fenêtre de navigateur web, connectez-vous tooyour **New Relic** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="37e5a-168">In a different web browser window, sign on tooyour **New Relic** company site as administrator.</span></span>

8. <span data-ttu-id="37e5a-169">Dans le menu hello haut de hello, cliquez sur **les paramètres de compte**.</span><span class="sxs-lookup"><span data-stu-id="37e5a-169">In hello menu on hello top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="37e5a-170">![Paramètres de compte](./media/active-directory-saas-new-relic-tutorial/ic797036.png "Paramètres de compte")</span><span class="sxs-lookup"><span data-stu-id="37e5a-170">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797036.png "Account Settings")</span></span>

9. <span data-ttu-id="37e5a-171">Cliquez sur hello **sécurité et l’authentification** onglet, puis cliquez sur hello **Single sign-on** onglet.</span><span class="sxs-lookup"><span data-stu-id="37e5a-171">Click hello **Security and authentication** tab, and then click hello **Single sign on** tab.</span></span>
   
    <span data-ttu-id="37e5a-172">![Authentification unique](./media/active-directory-saas-new-relic-tutorial/ic797037.png "Authentification unique")</span><span class="sxs-lookup"><span data-stu-id="37e5a-172">![Single Sign-On](./media/active-directory-saas-new-relic-tutorial/ic797037.png "Single Sign-On")</span></span>

10. <span data-ttu-id="37e5a-173">Sur la page de boîte de dialogue SAML hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="37e5a-173">On hello SAML dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="37e5a-174">![SAML](./media/active-directory-saas-new-relic-tutorial/ic797038.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="37e5a-174">![SAML](./media/active-directory-saas-new-relic-tutorial/ic797038.png "SAML")</span></span>
   
   <span data-ttu-id="37e5a-175">a.</span><span class="sxs-lookup"><span data-stu-id="37e5a-175">a.</span></span> <span data-ttu-id="37e5a-176">Cliquez sur **choisir un fichier** tooupload votre certificat Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="37e5a-176">Click **Choose File** tooupload your downloaded Azure Active Directory certificate.</span></span>

   <span data-ttu-id="37e5a-177">b.</span><span class="sxs-lookup"><span data-stu-id="37e5a-177">b.</span></span> <span data-ttu-id="37e5a-178">Bonjour **URL de connexion à distance** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="37e5a-178">In hello **Remote login URL** textbox,  paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="37e5a-179">c.</span><span class="sxs-lookup"><span data-stu-id="37e5a-179">c.</span></span> <span data-ttu-id="37e5a-180">Bonjour **URL de déconnexion** zone de texte, valeur hello coller **URL de déconnexion**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="37e5a-180">In hello **Logout landing URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

   <span data-ttu-id="37e5a-181">d.</span><span class="sxs-lookup"><span data-stu-id="37e5a-181">d.</span></span> <span data-ttu-id="37e5a-182">Cliquez sur **Save my changes**.</span><span class="sxs-lookup"><span data-stu-id="37e5a-182">Click **Save my changes**.</span></span>

> [!TIP]
> <span data-ttu-id="37e5a-183">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="37e5a-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="37e5a-184">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="37e5a-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="37e5a-185">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="37e5a-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="37e5a-186">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="37e5a-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="37e5a-187">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="37e5a-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="37e5a-189">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="37e5a-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="37e5a-190">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="37e5a-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="37e5a-192">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="37e5a-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="37e5a-194">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="37e5a-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="37e5a-196">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="37e5a-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="37e5a-198">a.</span><span class="sxs-lookup"><span data-stu-id="37e5a-198">a.</span></span> <span data-ttu-id="37e5a-199">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="37e5a-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="37e5a-200">b.</span><span class="sxs-lookup"><span data-stu-id="37e5a-200">b.</span></span> <span data-ttu-id="37e5a-201">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="37e5a-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="37e5a-202">c.</span><span class="sxs-lookup"><span data-stu-id="37e5a-202">c.</span></span> <span data-ttu-id="37e5a-203">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="37e5a-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="37e5a-204">d.</span><span class="sxs-lookup"><span data-stu-id="37e5a-204">d.</span></span> <span data-ttu-id="37e5a-205">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="37e5a-205">Click **Create**.</span></span>
 
### <a name="creating-a-new-relic-test-user"></a><span data-ttu-id="37e5a-206">Création d’un utilisateur de test New Relic</span><span class="sxs-lookup"><span data-stu-id="37e5a-206">Creating a New Relic test user</span></span>

<span data-ttu-id="37e5a-207">Dans l’ordre tooenable Azure Active Directory utilisateurs toolog dans tooNew Relic, ils doivent être configurés dans New Relic.</span><span class="sxs-lookup"><span data-stu-id="37e5a-207">In order tooenable Azure Active Directory users toolog in tooNew Relic, they must be provisioned into New Relic.</span></span> <span data-ttu-id="37e5a-208">Dans les cas de hello de New Relic, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="37e5a-208">In hello case of New Relic, provisioning is a manual task.</span></span>

<span data-ttu-id="37e5a-209">**tooprovision un tooNew de compte d’utilisateur Relic, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="37e5a-209">**tooprovision a user account tooNew Relic, perform hello following steps:**</span></span>

1. <span data-ttu-id="37e5a-210">Connectez-vous à tooyour **New Relic** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="37e5a-210">Log in tooyour **New Relic** company site as administrator.</span></span>

2. <span data-ttu-id="37e5a-211">Dans le menu hello haut de hello, cliquez sur **les paramètres de compte**.</span><span class="sxs-lookup"><span data-stu-id="37e5a-211">In hello menu on hello top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="37e5a-212">![Paramètres de compte](./media/active-directory-saas-new-relic-tutorial/ic797040.png "Paramètres de compte")</span><span class="sxs-lookup"><span data-stu-id="37e5a-212">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797040.png "Account Settings")</span></span>

3. <span data-ttu-id="37e5a-213">Bonjour **compte** hello volet gauche, cliquez sur **Résumé**, puis cliquez sur **ajouter un utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="37e5a-213">In hello **Account** pane on hello left side, click **Summary**, and then click **Add user**.</span></span>
   
    <span data-ttu-id="37e5a-214">![Paramètres de compte](./media/active-directory-saas-new-relic-tutorial/ic797041.png "Paramètres de compte")</span><span class="sxs-lookup"><span data-stu-id="37e5a-214">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797041.png "Account Settings")</span></span>

4. <span data-ttu-id="37e5a-215">Sur hello **utilisateurs actifs** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="37e5a-215">On hello **Active users** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="37e5a-216">![Utilisateurs actifs](./media/active-directory-saas-new-relic-tutorial/ic797042.png "Utilisateurs actifs")</span><span class="sxs-lookup"><span data-stu-id="37e5a-216">![Active Users](./media/active-directory-saas-new-relic-tutorial/ic797042.png "Active Users")</span></span>
   
    <span data-ttu-id="37e5a-217">a.</span><span class="sxs-lookup"><span data-stu-id="37e5a-217">a.</span></span> <span data-ttu-id="37e5a-218">Bonjour **messagerie** zone de texte, hello de type adresse de messagerie d’un utilisateur Azure Active Directory valide que vous souhaitez tooprovision.</span><span class="sxs-lookup"><span data-stu-id="37e5a-218">In hello **Email** textbox, type hello email address of a valid Azure Active Directory user you want tooprovision.</span></span>

    <span data-ttu-id="37e5a-219">b.</span><span class="sxs-lookup"><span data-stu-id="37e5a-219">b.</span></span> <span data-ttu-id="37e5a-220">Pour **Role**, sélectionnez **User**.</span><span class="sxs-lookup"><span data-stu-id="37e5a-220">As **Role** select **User**.</span></span>

    <span data-ttu-id="37e5a-221">c.</span><span class="sxs-lookup"><span data-stu-id="37e5a-221">c.</span></span> <span data-ttu-id="37e5a-222">Cliquez sur **Add this user**.</span><span class="sxs-lookup"><span data-stu-id="37e5a-222">Click **Add this user**.</span></span>

>[!NOTE]
><span data-ttu-id="37e5a-223">Vous pouvez utiliser n’importe quel autre New Relic utilisateur compte outil de création ou API fournie par New Relic tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="37e5a-223">You can use any other New Relic user account creation tools or APIs provided by New Relic tooprovision AAD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="37e5a-224">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="37e5a-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="37e5a-225">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooNew Relic.</span><span class="sxs-lookup"><span data-stu-id="37e5a-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNew Relic.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="37e5a-227">**tooassign Britta Simon tooNew Relic, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="37e5a-227">**tooassign Britta Simon tooNew Relic, perform hello following steps:**</span></span>

1. <span data-ttu-id="37e5a-228">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="37e5a-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="37e5a-230">Dans la liste des applications hello, sélectionnez **New Relic**.</span><span class="sxs-lookup"><span data-stu-id="37e5a-230">In hello applications list, select **New Relic**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_app.png) 

3. <span data-ttu-id="37e5a-232">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="37e5a-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="37e5a-234">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="37e5a-234">Click **Add** button.</span></span> <span data-ttu-id="37e5a-235">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="37e5a-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="37e5a-237">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="37e5a-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="37e5a-238">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="37e5a-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="37e5a-239">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="37e5a-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="37e5a-240">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="37e5a-240">Testing single sign-on</span></span>

<span data-ttu-id="37e5a-241">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="37e5a-241">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="37e5a-242">Lorsque vous cliquez sur mosaïque de New Relic hello Bonjour volet d’accès, vous devez obtenir l’application de New Relic tooyour automatiquement signé sur.</span><span class="sxs-lookup"><span data-stu-id="37e5a-242">When you click hello New Relic tile in hello Access Panel, you should get automatically signed-on tooyour New Relic application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="37e5a-243">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="37e5a-243">Additional resources</span></span>

* [<span data-ttu-id="37e5a-244">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="37e5a-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="37e5a-245">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="37e5a-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_203.png

