---
title: "Didacticiel : Intégration d’Azure Active Directory à UserEcho | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et UserEcho."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bedd916b-8f69-4b50-9b8d-56f4ee3bd3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: efe4a94ed6e5d22d153565d4782850eac4dff37b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-userecho"></a><span data-ttu-id="5f9fa-103">Didacticiel : Intégration d’Azure Active Directory à UserEcho</span><span class="sxs-lookup"><span data-stu-id="5f9fa-103">Tutorial: Azure Active Directory integration with UserEcho</span></span>

<span data-ttu-id="5f9fa-104">Dans ce didacticiel, vous apprendrez comment toointegrate UserEcho avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5f9fa-104">In this tutorial, you learn how toointegrate UserEcho with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5f9fa-105">Intégration UserEcho à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="5f9fa-105">Integrating UserEcho with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5f9fa-106">Vous pouvez contrôler dans Azure AD qui a accès tooUserEcho</span><span class="sxs-lookup"><span data-stu-id="5f9fa-106">You can control in Azure AD who has access tooUserEcho</span></span>
- <span data-ttu-id="5f9fa-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooUserEcho (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f9fa-107">You can enable your users tooautomatically get signed-on tooUserEcho (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5f9fa-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="5f9fa-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5f9fa-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5f9fa-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5f9fa-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5f9fa-110">Prerequisites</span></span>

<span data-ttu-id="5f9fa-111">tooconfigure intégration d’Azure AD avec UserEcho, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5f9fa-111">tooconfigure Azure AD integration with UserEcho, you need hello following items:</span></span>

- <span data-ttu-id="5f9fa-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f9fa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5f9fa-113">Un abonnement UserEcho pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="5f9fa-113">A UserEcho single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5f9fa-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5f9fa-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="5f9fa-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5f9fa-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5f9fa-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois ici : [offre d’essai](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5f9fa-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5f9fa-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="5f9fa-118">Scenario description</span></span>
<span data-ttu-id="5f9fa-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5f9fa-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="5f9fa-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5f9fa-121">Ajout de UserEcho à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="5f9fa-121">Adding UserEcho from hello gallery</span></span>
2. <span data-ttu-id="5f9fa-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f9fa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-userecho-from-hello-gallery"></a><span data-ttu-id="5f9fa-123">Ajout de UserEcho à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="5f9fa-123">Adding UserEcho from hello gallery</span></span>
<span data-ttu-id="5f9fa-124">intégration de hello tooconfigure de UserEcho dans Azure AD, vous devez tooadd UserEcho à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-124">tooconfigure hello integration of UserEcho into Azure AD, you need tooadd UserEcho from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5f9fa-125">**tooadd UserEcho à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5f9fa-125">**tooadd UserEcho from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5f9fa-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5f9fa-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5f9fa-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="5f9fa-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="5f9fa-133">Dans la zone de recherche de hello, tapez **UserEcho**.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-133">In hello search box, type **UserEcho**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_search.png)

5. <span data-ttu-id="5f9fa-135">Dans le volet de résultats hello, sélectionnez **UserEcho**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-135">In hello results panel, select **UserEcho**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5f9fa-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f9fa-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5f9fa-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec UserEcho pour un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="5f9fa-138">In this section, you configure and test Azure AD single sign-on with UserEcho based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5f9fa-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans UserEcho est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in UserEcho is tooa user in Azure AD.</span></span> <span data-ttu-id="5f9fa-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans UserEcho doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-140">In other words, a link relationship between an Azure AD user and hello related user in UserEcho needs toobe established.</span></span>

<span data-ttu-id="5f9fa-141">Dans UserEcho, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-141">In UserEcho, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5f9fa-142">tooconfigure et test Azure AD l’authentification unique avec UserEcho, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="5f9fa-142">tooconfigure and test Azure AD single sign-on with UserEcho, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5f9fa-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5f9fa-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5f9fa-145">**[Création d’un utilisateur de test UserEcho](#creating-a-userecho-test-user)**  -toohave un équivalent de Britta Simon dans UserEcho est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-145">**[Creating a UserEcho test user](#creating-a-userecho-test-user)** - toohave a counterpart of Britta Simon in UserEcho that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5f9fa-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5f9fa-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5f9fa-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f9fa-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5f9fa-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application UserEcho.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your UserEcho application.</span></span>

<span data-ttu-id="5f9fa-150">**tooconfigure Azure AD single sign-on avec UserEcho, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5f9fa-150">**tooconfigure Azure AD single sign-on with UserEcho, perform hello following steps:**</span></span>

1. <span data-ttu-id="5f9fa-151">Bonjour portail Azure, sur hello **UserEcho** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-151">In hello Azure portal, on hello **UserEcho** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="5f9fa-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_samlbase.png)

3. <span data-ttu-id="5f9fa-155">Sur hello **UserEcho domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5f9fa-155">On hello **UserEcho Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_url.png)

    <span data-ttu-id="5f9fa-157">a.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-157">a.</span></span> <span data-ttu-id="5f9fa-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.userecho.com/`</span><span class="sxs-lookup"><span data-stu-id="5f9fa-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.userecho.com/`</span></span>

    <span data-ttu-id="5f9fa-159">b.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-159">b.</span></span> <span data-ttu-id="5f9fa-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.userecho.com/saml/metadata/`</span><span class="sxs-lookup"><span data-stu-id="5f9fa-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.userecho.com/saml/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5f9fa-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-161">These values are not real.</span></span> <span data-ttu-id="5f9fa-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5f9fa-163">Contact [équipe de support Client de UserEcho](https://feedback.userecho.com/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-163">Contact [UserEcho Client support team](https://feedback.userecho.com/) tooget these values.</span></span> 

4. <span data-ttu-id="5f9fa-164">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_certificate.png) 

5. <span data-ttu-id="5f9fa-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="5f9fa-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-userecho-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5f9fa-168">Sur hello **UserEcho Configuration** , cliquez sur **UserEcho de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-168">On hello **UserEcho Configuration** section, click **Configure UserEcho** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5f9fa-169">Hello de copie **URL de déconnexion et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="5f9fa-169">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_configure.png) 

7. <span data-ttu-id="5f9fa-171">Dans une autre fenêtre de navigateur, connectez-vous sur le site d’entreprise tooyour UserEcho en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-171">In another browser window, sign on tooyour UserEcho company site as an administrator.</span></span>

8. <span data-ttu-id="5f9fa-172">Dans la barre d’outils de hello en haut de hello, cliquez sur le menu hello tooexpand de votre nom utilisateur, puis cliquez sur **le programme d’installation**.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-172">In hello toolbar on hello top, click your user name tooexpand hello menu, and then click **Setup**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_06.png) 

9. <span data-ttu-id="5f9fa-174">Cliquez sur **Integrations**.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-174">Click **Integrations**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_07.png) 

10. <span data-ttu-id="5f9fa-176">Cliquez sur **Website**, puis sur **Single sign-on (SAML2)**.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-176">Click **Website**, and then click **Single sign-on (SAML2)**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_08.png) 

11. <span data-ttu-id="5f9fa-178">Sur hello **l’authentification unique (SAML)** page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5f9fa-178">On hello **Single sign-on (SAML)** page, perform hello following steps:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_09.png)
    
    <span data-ttu-id="5f9fa-180">a.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-180">a.</span></span> <span data-ttu-id="5f9fa-181">Pour **SAML-enabled**, sélectionnez **Yes**.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-181">As **SAML-enabled**, select **Yes**.</span></span>
    
    <span data-ttu-id="5f9fa-182">b.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-182">b.</span></span> <span data-ttu-id="5f9fa-183">Coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir de hello portail Azure en hello **URL SSO SAML** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-183">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **SAML SSO URL** textbox.</span></span>
    
    <span data-ttu-id="5f9fa-184">c.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-184">c.</span></span> <span data-ttu-id="5f9fa-185">Coller **URL de déconnexion**, lequel vous avez copié à partir de hello portail Azure en hello **logoout distant URL** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-185">Paste **Sign-Out URL**, which you have copied from hello Azure portal into hello **Remote logoout URL** textbox.</span></span>
    
    <span data-ttu-id="5f9fa-186">d.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-186">d.</span></span> <span data-ttu-id="5f9fa-187">Ouvrez votre certificat téléchargé dans le bloc-notes, hello copie le contenu et le coller ensuite dans hello **certificat X.509** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-187">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **X.509 Certificate** textbox.</span></span>
    
    <span data-ttu-id="5f9fa-188">e.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-188">e.</span></span> <span data-ttu-id="5f9fa-189">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-189">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="5f9fa-190">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="5f9fa-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5f9fa-191">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5f9fa-192">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5f9fa-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5f9fa-193">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f9fa-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="5f9fa-194">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="5f9fa-196">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5f9fa-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5f9fa-197">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-userecho-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5f9fa-199">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-userecho-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5f9fa-201">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-userecho-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5f9fa-203">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5f9fa-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-userecho-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5f9fa-205">a.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-205">a.</span></span> <span data-ttu-id="5f9fa-206">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5f9fa-207">b.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-207">b.</span></span> <span data-ttu-id="5f9fa-208">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5f9fa-209">c.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-209">c.</span></span> <span data-ttu-id="5f9fa-210">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5f9fa-211">d.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-211">d.</span></span> <span data-ttu-id="5f9fa-212">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-212">Click **Create**.</span></span>
 
### <a name="creating-a-userecho-test-user"></a><span data-ttu-id="5f9fa-213">Création d’un utilisateur de test UserEcho</span><span class="sxs-lookup"><span data-stu-id="5f9fa-213">Creating a UserEcho test user</span></span>

<span data-ttu-id="5f9fa-214">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans UserEcho.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-214">hello objective of this section is toocreate a user called Britta Simon in UserEcho.</span></span>

<span data-ttu-id="5f9fa-215">**toocreate un utilisateur appelé Britta Simon dans UserEcho, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5f9fa-215">**toocreate a user called Britta Simon in UserEcho, perform hello following steps:**</span></span>

1. <span data-ttu-id="5f9fa-216">Site d’entreprise UserEcho tooyour ouverture de session en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-216">Sign-on tooyour UserEcho company site as an administrator.</span></span>

2. <span data-ttu-id="5f9fa-217">Dans la barre d’outils de hello en haut de hello, cliquez sur le menu hello tooexpand de votre nom utilisateur, puis cliquez sur **le programme d’installation**.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-217">In hello toolbar on hello top, click your user name tooexpand hello menu, and then click **Setup**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_06.png)

3. <span data-ttu-id="5f9fa-219">Cliquez sur **utilisateurs**, tooexpand hello **utilisateurs** section.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-219">Click **Users**, tooexpand hello **Users** section.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_10.png)

4. <span data-ttu-id="5f9fa-221">Cliquez sur **Utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-221">Click **Users**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_11.png)

5. <span data-ttu-id="5f9fa-223">Cliquez sur **Invite a new user**.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-223">Click **Invite a new user**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_12.png)

6. <span data-ttu-id="5f9fa-225">Sur hello **inviter un nouvel utilisateur** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5f9fa-225">On hello **Invite a new user** dialog, perform hello following steps:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_13.png)

    <span data-ttu-id="5f9fa-227">a.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-227">a.</span></span> <span data-ttu-id="5f9fa-228">Bonjour **nom** zone de texte, nom du type d’utilisateur hello comme Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-228">In hello **Name** textbox, type name of hello user like Britta Simon.</span></span>
    
    <span data-ttu-id="5f9fa-229">b.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-229">b.</span></span>  <span data-ttu-id="5f9fa-230">Bonjour **messagerie** adresse de messagerie de type hello d’utilisateur de zone de texte, comme Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-230">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="5f9fa-231">c.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-231">c.</span></span> <span data-ttu-id="5f9fa-232">Cliquez sur **Invite**.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-232">Click **Invite**.</span></span>

<span data-ttu-id="5f9fa-233">Une invitation est envoyée tooBritta, ce qui permet son toostart à l’aide de UserEcho.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-233">An invitation is sent tooBritta, which enables her toostart using UserEcho.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5f9fa-234">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f9fa-234">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5f9fa-235">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooUserEcho.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooUserEcho.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="5f9fa-237">**tooassign Britta Simon tooUserEcho, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5f9fa-237">**tooassign Britta Simon tooUserEcho, perform hello following steps:**</span></span>

1. <span data-ttu-id="5f9fa-238">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-238">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="5f9fa-240">Dans la liste des applications hello, sélectionnez **UserEcho**.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-240">In hello applications list, select **UserEcho**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_app.png) 

3. <span data-ttu-id="5f9fa-242">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="5f9fa-244">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-244">Click **Add** button.</span></span> <span data-ttu-id="5f9fa-245">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="5f9fa-247">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5f9fa-248">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5f9fa-249">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5f9fa-250">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="5f9fa-250">Testing single sign-on</span></span>

<span data-ttu-id="5f9fa-251">objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-251">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="5f9fa-252">Lorsque vous cliquez sur mosaïque UserEcho hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour UserEcho application.</span><span class="sxs-lookup"><span data-stu-id="5f9fa-252">When you click hello UserEcho tile in hello Access Panel, you should get automatically signed-on tooyour UserEcho application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5f9fa-253">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="5f9fa-253">Additional resources</span></span>

* [<span data-ttu-id="5f9fa-254">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5f9fa-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5f9fa-255">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="5f9fa-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_203.png
