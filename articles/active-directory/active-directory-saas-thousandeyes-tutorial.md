---
title: "Didacticiel : intégration d’Azure Active Directory à ThousandEyes | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et ThousandEyes."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 790e3f1e-1591-4dd6-87df-590b7bf8b4ba
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: jeedes
ms.openlocfilehash: fbfbfb71809355b1b138762757a851907737730b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thousandeyes"></a><span data-ttu-id="21667-103">Didacticiel : Intégration d’Azure AD à ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="21667-103">Tutorial: Azure Active Directory integration with ThousandEyes</span></span>

<span data-ttu-id="21667-104">Dans ce didacticiel, vous apprendrez comment toointegrate ThousandEyes avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="21667-104">In this tutorial, you learn how toointegrate ThousandEyes with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="21667-105">Intégration de ThousandEyes avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="21667-105">Integrating ThousandEyes with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="21667-106">Vous pouvez contrôler dans Azure AD qui a accès tooThousandEyes</span><span class="sxs-lookup"><span data-stu-id="21667-106">You can control in Azure AD who has access tooThousandEyes</span></span>
- <span data-ttu-id="21667-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooThousandEyes (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="21667-107">You can enable your users tooautomatically get signed-on tooThousandEyes (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="21667-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="21667-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="21667-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="21667-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="21667-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="21667-110">Prerequisites</span></span>

<span data-ttu-id="21667-111">tooconfigure intégration d’Azure AD à ThousandEyes, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="21667-111">tooconfigure Azure AD integration with ThousandEyes, you need hello following items:</span></span>

- <span data-ttu-id="21667-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="21667-112">An Azure AD subscription</span></span>
- <span data-ttu-id="21667-113">Un abonnement ThousandEyes pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="21667-113">A ThousandEyes single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="21667-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="21667-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="21667-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="21667-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="21667-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="21667-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="21667-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois ici : [offre d’essai](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="21667-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="21667-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="21667-118">Scenario description</span></span>
<span data-ttu-id="21667-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="21667-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="21667-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="21667-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="21667-121">Ajout de ThousandEyes à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="21667-121">Adding ThousandEyes from hello gallery</span></span>
2. <span data-ttu-id="21667-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="21667-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thousandeyes-from-hello-gallery"></a><span data-ttu-id="21667-123">Ajout de ThousandEyes à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="21667-123">Adding ThousandEyes from hello gallery</span></span>
<span data-ttu-id="21667-124">intégration de hello tooconfigure de ThousandEyes dans Azure AD, vous devez tooadd ThousandEyes à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="21667-124">tooconfigure hello integration of ThousandEyes into Azure AD, you need tooadd ThousandEyes from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="21667-125">**tooadd ThousandEyes à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="21667-125">**tooadd ThousandEyes from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="21667-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="21667-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="21667-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="21667-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="21667-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="21667-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="21667-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="21667-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="21667-133">Dans la zone de recherche de hello, tapez **ThousandEyes**.</span><span class="sxs-lookup"><span data-stu-id="21667-133">In hello search box, type **ThousandEyes**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_search.png)

5. <span data-ttu-id="21667-135">Dans le volet de résultats hello, sélectionnez **ThousandEyes**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="21667-135">In hello results panel, select **ThousandEyes**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="21667-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="21667-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="21667-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD auprès de ThousandEyes avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="21667-138">In this section, you configure and test Azure AD single sign-on with ThousandEyes based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="21667-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans ThousandEyes est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="21667-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ThousandEyes is tooa user in Azure AD.</span></span> <span data-ttu-id="21667-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans ThousandEyes doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="21667-140">In other words, a link relationship between an Azure AD user and hello related user in ThousandEyes needs toobe established.</span></span>

<span data-ttu-id="21667-141">Dans ThousandEyes, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="21667-141">In ThousandEyes, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="21667-142">tooconfigure et test Azure AD l’authentification unique avec ThousandEyes, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="21667-142">tooconfigure and test Azure AD single sign-on with ThousandEyes, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="21667-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="21667-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="21667-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="21667-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="21667-145">**[Création d’un utilisateur de test de ThousandEyes](#creating-a-thousandeyes-test-user)**  -toohave un équivalent de Britta Simon dans ThousandEyes est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="21667-145">**[Creating a ThousandEyes test user](#creating-a-thousandeyes-test-user)** - toohave a counterpart of Britta Simon in ThousandEyes that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="21667-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="21667-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="21667-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="21667-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="21667-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="21667-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="21667-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="21667-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ThousandEyes application.</span></span>

<span data-ttu-id="21667-150">**tooconfigure Azure AD single sign-on avec ThousandEyes, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="21667-150">**tooconfigure Azure AD single sign-on with ThousandEyes, perform hello following steps:**</span></span>

1. <span data-ttu-id="21667-151">Bonjour portail Azure, sur hello **ThousandEyes** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="21667-151">In hello Azure portal, on hello **ThousandEyes** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="21667-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="21667-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_samlbase.png)

3. <span data-ttu-id="21667-155">Sur hello **ThousandEyes domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="21667-155">On hello **ThousandEyes Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_url.png)

    <span data-ttu-id="21667-157">Bonjour **URL de connexion** zone de texte, tapez une URL en tant que :`https://app.thousandeyes.com/login/sso`</span><span class="sxs-lookup"><span data-stu-id="21667-157">In hello **Sign-on URL** textbox, type a URL as: `https://app.thousandeyes.com/login/sso`</span></span>

4. <span data-ttu-id="21667-158">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="21667-158">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_certificate.png) 

5. <span data-ttu-id="21667-160">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="21667-160">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="21667-162">Sur hello **ThousandEyes Configuration** , cliquez sur **configurer de ThousandEyes** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="21667-162">On hello **ThousandEyes Configuration** section, click **Configure ThousandEyes** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="21667-163">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="21667-163">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_configure.png) 

7. <span data-ttu-id="21667-165">Dans une fenêtre de navigateur web, connectez-vous tooyour **ThousandEyes** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="21667-165">In a different web browser window, sign on tooyour **ThousandEyes** company site as an administrator.</span></span>

8. <span data-ttu-id="21667-166">Dans le menu hello haut de hello, cliquez sur **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="21667-166">In hello menu on hello top, click **Settings**.</span></span>
   
    <span data-ttu-id="21667-167">![Paramètres](./media/active-directory-saas-thousandeyes-tutorial/ic790066.png "Paramètres")</span><span class="sxs-lookup"><span data-stu-id="21667-167">![Settings](./media/active-directory-saas-thousandeyes-tutorial/ic790066.png "Settings")</span></span>

9. <span data-ttu-id="21667-168">Cliquez sur **Account**</span><span class="sxs-lookup"><span data-stu-id="21667-168">Click **Account**</span></span>
   
    <span data-ttu-id="21667-169">![Compte](./media/active-directory-saas-thousandeyes-tutorial/ic790067.png "Compte")</span><span class="sxs-lookup"><span data-stu-id="21667-169">![Account](./media/active-directory-saas-thousandeyes-tutorial/ic790067.png "Account")</span></span>

10. <span data-ttu-id="21667-170">Cliquez sur hello **sécurité et authentification** onglet.</span><span class="sxs-lookup"><span data-stu-id="21667-170">Click hello **Security & Authentication** tab.</span></span>
   
    <span data-ttu-id="21667-171">![Sécurité et authentification](./media/active-directory-saas-thousandeyes-tutorial/ic790068.png "Sécurité et authentification")</span><span class="sxs-lookup"><span data-stu-id="21667-171">![Security & Authentication](./media/active-directory-saas-thousandeyes-tutorial/ic790068.png "Security & Authentication")</span></span>

11. <span data-ttu-id="21667-172">Bonjour **le programme d’installation Single Sign-On** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="21667-172">In hello **Setup Single Sign-On** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="21667-173">![Configurer l’authentification unique](./media/active-directory-saas-thousandeyes-tutorial/ic790069.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="21667-173">![Setup Single Sign-On](./media/active-directory-saas-thousandeyes-tutorial/ic790069.png "Setup Single Sign-On")</span></span>
  
    <span data-ttu-id="21667-174">a.</span><span class="sxs-lookup"><span data-stu-id="21667-174">a.</span></span> <span data-ttu-id="21667-175">Sélectionnez **Activer l'authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="21667-175">Select **Enable Single Sign-On**.</span></span>
  
    <span data-ttu-id="21667-176">b.</span><span class="sxs-lookup"><span data-stu-id="21667-176">b.</span></span> <span data-ttu-id="21667-177">Dans la zone de texte **URL de la page de connexion**, collez l’**URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="21667-177">In **Login Page URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="21667-178">c.</span><span class="sxs-lookup"><span data-stu-id="21667-178">c.</span></span> <span data-ttu-id="21667-179">Dans la zone de texte **URL de la page de déconnexion**, collez la valeur de l’**URL de déconnexion** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="21667-179">In **Logout Page URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="21667-180">d.</span><span class="sxs-lookup"><span data-stu-id="21667-180">d.</span></span> <span data-ttu-id="21667-181">Dans la zone de texte **Émetteur du fournisseur d’identité**, collez l’**ID d’entité SAML** copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="21667-181">**Identity Provider Issuer** textbox, paste **SAML Entity ID** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="21667-182">e.</span><span class="sxs-lookup"><span data-stu-id="21667-182">e.</span></span> <span data-ttu-id="21667-183">Dans **certificat de vérification**, cliquez sur **choisir un fichier**, puis téléchargez le certificat hello que vous avez téléchargé à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="21667-183">In **Verification Certificate**, click **Choose file**, and then upload hello certificate you have downloaded from Azure portal.</span></span>
  
    <span data-ttu-id="21667-184">f.</span><span class="sxs-lookup"><span data-stu-id="21667-184">f.</span></span> <span data-ttu-id="21667-185">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="21667-185">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="21667-186">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="21667-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="21667-187">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="21667-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="21667-188">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="21667-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="21667-189">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="21667-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="21667-190">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="21667-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="21667-192">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="21667-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="21667-193">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="21667-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="21667-195">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="21667-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="21667-197">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="21667-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="21667-199">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="21667-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="21667-201">a.</span><span class="sxs-lookup"><span data-stu-id="21667-201">a.</span></span> <span data-ttu-id="21667-202">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="21667-202">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="21667-203">b.</span><span class="sxs-lookup"><span data-stu-id="21667-203">b.</span></span> <span data-ttu-id="21667-204">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="21667-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="21667-205">c.</span><span class="sxs-lookup"><span data-stu-id="21667-205">c.</span></span> <span data-ttu-id="21667-206">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="21667-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="21667-207">d.</span><span class="sxs-lookup"><span data-stu-id="21667-207">d.</span></span> <span data-ttu-id="21667-208">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="21667-208">Click **Create**.</span></span>
 
### <a name="creating-a-thousandeyes-test-user"></a><span data-ttu-id="21667-209">Création d’un utilisateur de test ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="21667-209">Creating a ThousandEyes test user</span></span>

<span data-ttu-id="21667-210">Dans l’ordre tooenable Azure AD les utilisateurs toolog à ThousandEyes, vous devez les configurer dans ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="21667-210">In order tooenable Azure AD users toolog into ThousandEyes, they must be provisioned into ThousandEyes.</span></span>  
<span data-ttu-id="21667-211">Dans les cas de hello de ThousandEyes, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="21667-211">In hello case of ThousandEyes, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="21667-212">Vous pouvez utiliser n’importe quel autre ThousandEyes utilisateur compte outil de création ou API fournie par ThousandEyes tooprovision Azure Active Directory des comptes d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="21667-212">You can use any other ThousandEyes user account creation tools or APIs provided by ThousandEyes tooprovision Azure Active Directory user accounts.</span></span>

<span data-ttu-id="21667-213">**tooprovision un tooThousandEyes de compte d’utilisateur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="21667-213">**tooprovision a user account tooThousandEyes, perform hello following steps:**</span></span>

1. <span data-ttu-id="21667-214">Connectez-vous à votre site d’entreprise ThousandEyes en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="21667-214">Log into your ThousandEyes company site as an administrator.</span></span>

2. <span data-ttu-id="21667-215">Cliquez sur **Settings**.</span><span class="sxs-lookup"><span data-stu-id="21667-215">Click **Settings**.</span></span>
   
    <span data-ttu-id="21667-216">![Paramètres](./media/active-directory-saas-thousandeyes-tutorial/IC790066.png "Paramètres")</span><span class="sxs-lookup"><span data-stu-id="21667-216">![Settings](./media/active-directory-saas-thousandeyes-tutorial/IC790066.png "Settings")</span></span>

3. <span data-ttu-id="21667-217">Cliquez sur **Account**.</span><span class="sxs-lookup"><span data-stu-id="21667-217">Click **Account**.</span></span>
   
    <span data-ttu-id="21667-218">![Compte](./media/active-directory-saas-thousandeyes-tutorial/IC790067.png "Compte")</span><span class="sxs-lookup"><span data-stu-id="21667-218">![Account](./media/active-directory-saas-thousandeyes-tutorial/IC790067.png "Account")</span></span>

4. <span data-ttu-id="21667-219">Cliquez sur hello **comptes et utilisateurs** onglet.</span><span class="sxs-lookup"><span data-stu-id="21667-219">Click hello **Accounts & Users** tab.</span></span>
   
    <span data-ttu-id="21667-220">![Comptes et utilisateurs](./media/active-directory-saas-thousandeyes-tutorial/IC790073.png "Comptes et utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="21667-220">![Accounts & Users](./media/active-directory-saas-thousandeyes-tutorial/IC790073.png "Accounts & Users")</span></span>

5. <span data-ttu-id="21667-221">Bonjour **ajouter des utilisateurs et comptes** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="21667-221">In hello **Add Users & Accounts** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="21667-222">![Ajouter des comptes d’utilisateurs](./media/active-directory-saas-thousandeyes-tutorial/IC790074.png "Ajouter des comptes d’utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="21667-222">![Add User Accounts](./media/active-directory-saas-thousandeyes-tutorial/IC790074.png "Add User Accounts")</span></span>   
  
    <span data-ttu-id="21667-223">a.</span><span class="sxs-lookup"><span data-stu-id="21667-223">a.</span></span> <span data-ttu-id="21667-224">Dans **nom** zone de texte, nom d’utilisateur comme hello du type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="21667-224">In **Name** textbox, type hello name of user like **Britta Simon**.</span></span>

    <span data-ttu-id="21667-225">b.</span><span class="sxs-lookup"><span data-stu-id="21667-225">b.</span></span> <span data-ttu-id="21667-226">Dans **messagerie** par courrier électronique de type hello d’utilisateur de zone de texte, comme  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="21667-226">In **Email** textbox, type hello email of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="21667-227">b.</span><span class="sxs-lookup"><span data-stu-id="21667-227">b.</span></span> <span data-ttu-id="21667-228">Cliquez sur **tooAccount d’ajouter un nouvel utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="21667-228">Click **Add New User tooAccount**.</span></span>
      
     >[!NOTE]
     ><span data-ttu-id="21667-229">titulaire du compte Azure Active Directory Hello Obtient un message électronique contenant un lien de tooconfirm et activer le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="21667-229">hello Azure Active Directory account holder will get an email including a link tooconfirm and activate hello account.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="21667-230">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="21667-230">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="21667-231">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="21667-231">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooThousandEyes.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="21667-233">**tooassign Britta Simon tooThousandEyes, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="21667-233">**tooassign Britta Simon tooThousandEyes, perform hello following steps:**</span></span>

1. <span data-ttu-id="21667-234">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="21667-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="21667-236">Dans la liste des applications hello, sélectionnez **ThousandEyes**.</span><span class="sxs-lookup"><span data-stu-id="21667-236">In hello applications list, select **ThousandEyes**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_app.png) 

3. <span data-ttu-id="21667-238">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="21667-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="21667-240">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="21667-240">Click **Add** button.</span></span> <span data-ttu-id="21667-241">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="21667-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="21667-243">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="21667-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="21667-244">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="21667-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="21667-245">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="21667-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="21667-246">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="21667-246">Testing single sign-on</span></span>

<span data-ttu-id="21667-247">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="21667-247">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="21667-248">Lorsque vous cliquez sur hello ThousandEyes vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour application ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="21667-248">When you click hello ThousandEyes tile in hello Access Panel, you should get automatically signed-on tooyour ThousandEyes application.</span></span>

<span data-ttu-id="21667-249">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="21667-249">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="21667-250">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="21667-250">Additional resources</span></span>

* [<span data-ttu-id="21667-251">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="21667-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="21667-252">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="21667-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_203.png

