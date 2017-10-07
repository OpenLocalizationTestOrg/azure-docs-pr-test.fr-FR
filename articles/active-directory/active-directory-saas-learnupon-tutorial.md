---
title: "Didacticiel : Intégration d’Azure Active Directory à LearnUpon | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et LearnUpon."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b11c6315-c79d-4f34-9610-bd17070ab7c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: fdb9c62172327a539f0459c98aa20e63fa441e4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learnupon"></a><span data-ttu-id="4bb57-103">Didacticiel : intégration d’Azure Active Directory à LearnUpon</span><span class="sxs-lookup"><span data-stu-id="4bb57-103">Tutorial: Azure Active Directory integration with LearnUpon</span></span>

<span data-ttu-id="4bb57-104">Dans ce didacticiel, vous apprendrez comment toointegrate LearnUpon avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4bb57-104">In this tutorial, you learn how toointegrate LearnUpon with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4bb57-105">Intégration LearnUpon à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="4bb57-105">Integrating LearnUpon with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4bb57-106">Vous pouvez contrôler dans Azure AD qui a accès tooLearnUpon</span><span class="sxs-lookup"><span data-stu-id="4bb57-106">You can control in Azure AD who has access tooLearnUpon</span></span>
- <span data-ttu-id="4bb57-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooLearnUpon (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="4bb57-107">You can enable your users tooautomatically get signed-on tooLearnUpon (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4bb57-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="4bb57-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4bb57-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4bb57-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4bb57-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4bb57-110">Prerequisites</span></span>

<span data-ttu-id="4bb57-111">tooconfigure intégration d’Azure AD avec LearnUpon, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="4bb57-111">tooconfigure Azure AD integration with LearnUpon, you need hello following items:</span></span>

- <span data-ttu-id="4bb57-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="4bb57-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4bb57-113">Un abonnement LearnUpon pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="4bb57-113">A LearnUpon single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4bb57-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="4bb57-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4bb57-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="4bb57-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4bb57-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="4bb57-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4bb57-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4bb57-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4bb57-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="4bb57-118">Scenario description</span></span>
<span data-ttu-id="4bb57-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="4bb57-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4bb57-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="4bb57-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4bb57-121">Ajout de LearnUpon à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="4bb57-121">Adding LearnUpon from hello gallery</span></span>
2. <span data-ttu-id="4bb57-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4bb57-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learnupon-from-hello-gallery"></a><span data-ttu-id="4bb57-123">Ajout de LearnUpon à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="4bb57-123">Adding LearnUpon from hello gallery</span></span>
<span data-ttu-id="4bb57-124">intégration de hello tooconfigure de LearnUpon dans Azure AD, vous devez tooadd LearnUpon à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="4bb57-124">tooconfigure hello integration of LearnUpon into Azure AD, you need tooadd LearnUpon from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4bb57-125">**tooadd LearnUpon à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4bb57-125">**tooadd LearnUpon from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4bb57-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="4bb57-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4bb57-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="4bb57-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4bb57-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="4bb57-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="4bb57-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="4bb57-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="4bb57-133">Dans la zone de recherche de hello, tapez **LearnUpon**.</span><span class="sxs-lookup"><span data-stu-id="4bb57-133">In hello search box, type **LearnUpon**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_search.png)

5. <span data-ttu-id="4bb57-135">Dans le volet de résultats hello, sélectionnez **LearnUpon**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="4bb57-135">In hello results panel, select **LearnUpon**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4bb57-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4bb57-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4bb57-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec LearnUpon à l’aide d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="4bb57-138">In this section, you configure and test Azure AD single sign-on with LearnUpon based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4bb57-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans LearnUpon est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4bb57-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LearnUpon is tooa user in Azure AD.</span></span> <span data-ttu-id="4bb57-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans LearnUpon doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="4bb57-140">In other words, a link relationship between an Azure AD user and hello related user in LearnUpon needs toobe established.</span></span>

<span data-ttu-id="4bb57-141">Dans LearnUpon, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="4bb57-141">In LearnUpon, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4bb57-142">tooconfigure et test Azure AD l’authentification unique avec LearnUpon, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="4bb57-142">tooconfigure and test Azure AD single sign-on with LearnUpon, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4bb57-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="4bb57-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4bb57-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4bb57-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4bb57-145">**[Création d’un utilisateur de test LearnUpon](#creating-a-learnupon-test-user)**  -toohave un équivalent de Britta Simon dans LearnUpon est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4bb57-145">**[Creating a LearnUpon test user](#creating-a-learnupon-test-user)** - toohave a counterpart of Britta Simon in LearnUpon that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4bb57-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="4bb57-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4bb57-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="4bb57-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4bb57-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4bb57-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4bb57-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="4bb57-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LearnUpon application.</span></span>

<span data-ttu-id="4bb57-150">**tooconfigure Azure AD single sign-on avec LearnUpon, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4bb57-150">**tooconfigure Azure AD single sign-on with LearnUpon, perform hello following steps:**</span></span>

1. <span data-ttu-id="4bb57-151">Bonjour portail Azure, sur hello **LearnUpon** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="4bb57-151">In hello Azure portal, on hello **LearnUpon** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="4bb57-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="4bb57-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_samlbase.png)

3. <span data-ttu-id="4bb57-155">Sur hello **LearnUpon domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="4bb57-155">On hello **LearnUpon Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_url.png)

    <span data-ttu-id="4bb57-157">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.learnupon.com/saml/consumer`</span><span class="sxs-lookup"><span data-stu-id="4bb57-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.learnupon.com/saml/consumer`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4bb57-158">Notez qu’il ne s’agit pas de la valeur réelle hello.</span><span class="sxs-lookup"><span data-stu-id="4bb57-158">Please note that this is not hello real value.</span></span> <span data-ttu-id="4bb57-159">vous avez tooupdate cette valeur avec l’URL de réponse réelle hello.</span><span class="sxs-lookup"><span data-stu-id="4bb57-159">you have tooupdate this value with hello actual Reply URL.</span></span> <span data-ttu-id="4bb57-160">Contact de cette valeur tooget [équipe de support LearnUpon](https://www.learnupon.com/features/support/).</span><span class="sxs-lookup"><span data-stu-id="4bb57-160">tooget this value Contact [LearnUpon support team](https://www.learnupon.com/features/support/).</span></span>



4. <span data-ttu-id="4bb57-161">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Raw)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="4bb57-161">On hello **SAML Signing Certificate** section, click **Certificate (Raw)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_certificate.png) 

5. <span data-ttu-id="4bb57-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="4bb57-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-learnupon-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4bb57-165">Sur hello **LearnUpon Configuration** , cliquez sur **LearnUpon de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="4bb57-165">On hello **LearnUpon Configuration** section, click **Configure LearnUpon** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4bb57-166">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="4bb57-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_configure.png) 

7. <span data-ttu-id="4bb57-168">Ouvrez une autre instance du navigateur et connectez-vous à LearnUpon avec un compte d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="4bb57-168">Open another browser instance and login into LearnUpon with an administrator account.</span></span> 

8. <span data-ttu-id="4bb57-169">Cliquez sur hello **paramètres** onglet.</span><span class="sxs-lookup"><span data-stu-id="4bb57-169">Click hello **settings** tab.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_06.png)

9. <span data-ttu-id="4bb57-171">Cliquez sur **Single Sign On - SAML**, puis cliquez sur **paramètres généraux** tooconfigure SAML paramètres.</span><span class="sxs-lookup"><span data-stu-id="4bb57-171">Click **Single Sign On - SAML**, and then click **General Settings** tooconfigure SAML settings.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_07.png) 

10. <span data-ttu-id="4bb57-173">Bonjour **paramètres généraux** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="4bb57-173">In hello **General Settings** section, perform hello following steps:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_08.png)  
  
    <span data-ttu-id="4bb57-175">a.</span><span class="sxs-lookup"><span data-stu-id="4bb57-175">a.</span></span> <span data-ttu-id="4bb57-176">Sélectionnez **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="4bb57-176">Select **Enabled**.</span></span>

    <span data-ttu-id="4bb57-177">b.</span><span class="sxs-lookup"><span data-stu-id="4bb57-177">b.</span></span> <span data-ttu-id="4bb57-178">Sélectionnez **2.0** pour **Version**.</span><span class="sxs-lookup"><span data-stu-id="4bb57-178">Select **Version** as **2.0**.</span></span>

    <span data-ttu-id="4bb57-179">c.</span><span class="sxs-lookup"><span data-stu-id="4bb57-179">c.</span></span> <span data-ttu-id="4bb57-180">Sélectionnez **Non** pour **Skip conditions** (Ignorer les conditions).</span><span class="sxs-lookup"><span data-stu-id="4bb57-180">Select **Skip conditions** as **No**.</span></span>

    <span data-ttu-id="4bb57-181">d.</span><span class="sxs-lookup"><span data-stu-id="4bb57-181">d.</span></span> <span data-ttu-id="4bb57-182">Bonjour **SAML Token valider le nom param** zone de texte Nom hello du type de demande post paramètre toohello SAML consommateur URL indiquée ci-dessus contenant toobe d’Assertion SAML hello vérifiées et authentifié -  **SAMLResponse**.</span><span class="sxs-lookup"><span data-stu-id="4bb57-182">In hello **SAML Token Post param name** textbox, type hello name of request post parameter toohello SAML consumer URL indicated above that contains hello SAML Assertion toobe verified and authenticated - for example **SAMLResponse**.</span></span>

    <span data-ttu-id="4bb57-183">e.</span><span class="sxs-lookup"><span data-stu-id="4bb57-183">e.</span></span> <span data-ttu-id="4bb57-184">Bonjour **Name Identifier Format** zone de texte, valeur type hello qui indique où vos utilisateurs de hello Assertion SAML identificateur (adresse électronique) réside - par exemple **urn : oasis : noms : tc : SAML:1.1:nameid-format : emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="4bb57-184">In hello **Name Identifier Format** textbox, type hello value that indicates where in your SAML Assertion hello users identifier (Email address) resides - for example **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>
  
    <span data-ttu-id="4bb57-185">f.</span><span class="sxs-lookup"><span data-stu-id="4bb57-185">f.</span></span> <span data-ttu-id="4bb57-186">Bonjour **emplacement du fournisseur identifier** zone de texte, de type hello indiquant où hello les utilisateurs sont envoyés tooif ils cliquent sur l’icône de téléchargé à partir de l’écran de connexion au portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4bb57-186">In hello **Identify Provider Location** textbox, type hello value that indicates where hello users are sent tooif they click on your uploaded icon from your Azure portal login screen.</span></span>
  
    <span data-ttu-id="4bb57-187">g.</span><span class="sxs-lookup"><span data-stu-id="4bb57-187">g.</span></span> <span data-ttu-id="4bb57-188">Bonjour **se déconnecter URL** zone de texte, collez hello **URL de déconnexion** dont vous avez copié à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4bb57-188">In hello **Sign out URL** textbox, paste hello **Sign-Out URL** which you have copied from hello Azure portal.</span></span>
    
    <span data-ttu-id="4bb57-189">h.</span><span class="sxs-lookup"><span data-stu-id="4bb57-189">h.</span></span> <span data-ttu-id="4bb57-190">Cliquez sur **gérer les empreintes digitales**, puis téléchargez empreintes hello de votre certificat téléchargé.</span><span class="sxs-lookup"><span data-stu-id="4bb57-190">Click **Manage finger prints**, and then upload hello finger print of your downloaded certificate.</span></span>

11. <span data-ttu-id="4bb57-191">Cliquez sur **paramètres utilisateur**, puis exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="4bb57-191">Click **User Settings**, and then perform hello following steps:</span></span>
   
     ![Configurer l’authentification unique](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_11.png)  
 
    <span data-ttu-id="4bb57-193">a.</span><span class="sxs-lookup"><span data-stu-id="4bb57-193">a.</span></span> <span data-ttu-id="4bb57-194">Bonjour **First Name Identifier Format** zone de texte, type hello valeur qui indique où dans votre prénom d’utilisateurs de hello Assertion SAML réside - par exemple : **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="4bb57-194">In hello **First Name Identifier Format** textbox, type hello value that tells us where in your SAML Assertion hello users firstname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>
  
    <span data-ttu-id="4bb57-195">b.</span><span class="sxs-lookup"><span data-stu-id="4bb57-195">b.</span></span> <span data-ttu-id="4bb57-196">Bonjour **dernier Format d’identificateur de nom** zone de texte, type hello valeur qui indique où dans votre nom d’utilisateurs de hello Assertion SAML réside - par exemple : **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span><span class="sxs-lookup"><span data-stu-id="4bb57-196">In hello **Last Name Identifier Format** textbox, type hello value that tells us where in your SAML Assertion hello users lastname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>

> [!TIP]
> <span data-ttu-id="4bb57-197">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="4bb57-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4bb57-198">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="4bb57-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4bb57-199">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4bb57-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4bb57-200">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="4bb57-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="4bb57-201">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="4bb57-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="4bb57-203">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4bb57-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4bb57-204">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="4bb57-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4bb57-206">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="4bb57-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4bb57-208">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="4bb57-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4bb57-210">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="4bb57-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4bb57-212">a.</span><span class="sxs-lookup"><span data-stu-id="4bb57-212">a.</span></span> <span data-ttu-id="4bb57-213">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4bb57-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4bb57-214">b.</span><span class="sxs-lookup"><span data-stu-id="4bb57-214">b.</span></span> <span data-ttu-id="4bb57-215">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4bb57-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4bb57-216">c.</span><span class="sxs-lookup"><span data-stu-id="4bb57-216">c.</span></span> <span data-ttu-id="4bb57-217">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="4bb57-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4bb57-218">d.</span><span class="sxs-lookup"><span data-stu-id="4bb57-218">d.</span></span> <span data-ttu-id="4bb57-219">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="4bb57-219">Click **Create**.</span></span>
 
### <a name="creating-a-learnupon-test-user"></a><span data-ttu-id="4bb57-220">Création d’un utilisateur de test LearnUpon</span><span class="sxs-lookup"><span data-stu-id="4bb57-220">Creating a LearnUpon test user</span></span>

<span data-ttu-id="4bb57-221">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="4bb57-221">hello objective of this section is toocreate a user called Britta Simon in LearnUpon.</span></span> <span data-ttu-id="4bb57-222">LearnUpon prend en charge l’approvisionnement juste-à-temps, qui est activé par défaut.</span><span class="sxs-lookup"><span data-stu-id="4bb57-222">LearnUpon supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="4bb57-223">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="4bb57-223">There is no action item for you in this section.</span></span> <span data-ttu-id="4bb57-224">Un nouvel utilisateur s’affichera pendant une tentative de tooaccess LearnUpon s’il n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="4bb57-224">A new user will be created during an attempt tooaccess LearnUpon if it doesn't exist yet.</span></span> <span data-ttu-id="4bb57-225">[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="4bb57-225">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="4bb57-226">Si vous devez manuellement toocreate un utilisateur, vous devez toocontact [équipe de support LearnUpon](https://www.learnupon.com/features/support/).</span><span class="sxs-lookup"><span data-stu-id="4bb57-226">If you need toocreate an user manually, you need toocontact [LearnUpon support team](https://www.learnupon.com/features/support/).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4bb57-227">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4bb57-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4bb57-228">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooLearnUpon.</span><span class="sxs-lookup"><span data-stu-id="4bb57-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLearnUpon.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="4bb57-230">**tooassign Britta Simon tooLearnUpon, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4bb57-230">**tooassign Britta Simon tooLearnUpon, perform hello following steps:**</span></span>

1. <span data-ttu-id="4bb57-231">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="4bb57-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="4bb57-233">Dans la liste des applications hello, sélectionnez **LearnUpon**.</span><span class="sxs-lookup"><span data-stu-id="4bb57-233">In hello applications list, select **LearnUpon**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_app.png) 

3. <span data-ttu-id="4bb57-235">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="4bb57-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="4bb57-237">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="4bb57-237">Click **Add** button.</span></span> <span data-ttu-id="4bb57-238">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="4bb57-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="4bb57-240">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="4bb57-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4bb57-241">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="4bb57-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4bb57-242">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="4bb57-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4bb57-243">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="4bb57-243">Testing single sign-on</span></span>

<span data-ttu-id="4bb57-244">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="4bb57-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4bb57-245">Lorsque vous cliquez sur mosaïque LearnUpon hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour LearnUpon application.</span><span class="sxs-lookup"><span data-stu-id="4bb57-245">When you click hello LearnUpon tile in hello Access Panel, you should get automatically signed-on tooyour LearnUpon application.</span></span>
<span data-ttu-id="4bb57-246">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4bb57-246">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4bb57-247">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="4bb57-247">Additional resources</span></span>

* [<span data-ttu-id="4bb57-248">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4bb57-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4bb57-249">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="4bb57-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_203.png

