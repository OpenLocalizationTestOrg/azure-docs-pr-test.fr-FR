---
title: "Didacticiel : Intégration d’Azure Active Directory à Canvas Lms | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Canvas LMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfed291c-a33e-410d-b919-5b965a631d45
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: jeedes
ms.openlocfilehash: 8f4a09266a108e2c92326b0909dd0650b1c84d6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-canvas-lms"></a><span data-ttu-id="dd526-103">Didacticiel : Intégration d’Azure Active Directory à Canvas LMS</span><span class="sxs-lookup"><span data-stu-id="dd526-103">Tutorial: Azure Active Directory integration with Canvas LMS</span></span>

<span data-ttu-id="dd526-104">Dans ce didacticiel, vous apprendrez comment toointegrate canevas avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dd526-104">In this tutorial, you learn how toointegrate Canvas with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dd526-105">Intégration de zone de dessin à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="dd526-105">Integrating Canvas with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="dd526-106">Vous pouvez contrôler dans Azure AD qui a accès tooCanvas</span><span class="sxs-lookup"><span data-stu-id="dd526-106">You can control in Azure AD who has access tooCanvas</span></span>
- <span data-ttu-id="dd526-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooCanvas (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd526-107">You can enable your users tooautomatically get signed-on tooCanvas (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dd526-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="dd526-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="dd526-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dd526-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd526-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="dd526-110">Prerequisites</span></span>

<span data-ttu-id="dd526-111">tooconfigure intégration d’Azure AD à Canvas, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="dd526-111">tooconfigure Azure AD integration with Canvas, you need hello following items:</span></span>

- <span data-ttu-id="dd526-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd526-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dd526-113">Un abonnement Canvas pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="dd526-113">A Canvas single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dd526-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="dd526-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dd526-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="dd526-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dd526-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="dd526-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dd526-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dd526-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dd526-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="dd526-118">Scenario description</span></span>
<span data-ttu-id="dd526-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="dd526-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dd526-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="dd526-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dd526-121">Ajout de zone de dessin à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="dd526-121">Adding Canvas from hello gallery</span></span>
2. <span data-ttu-id="dd526-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd526-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-canvas-from-hello-gallery"></a><span data-ttu-id="dd526-123">Ajout de zone de dessin à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="dd526-123">Adding Canvas from hello gallery</span></span>
<span data-ttu-id="dd526-124">intégration de hello tooconfigure de zone de dessin dans Azure AD, vous devez tooadd zone de dessin à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="dd526-124">tooconfigure hello integration of Canvas into Azure AD, you need tooadd Canvas from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="dd526-125">**tooadd zone à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dd526-125">**tooadd Canvas from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="dd526-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="dd526-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dd526-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="dd526-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="dd526-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="dd526-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="dd526-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="dd526-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="dd526-133">Dans la zone de recherche de hello, tapez **canevas**.</span><span class="sxs-lookup"><span data-stu-id="dd526-133">In hello search box, type **Canvas**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_search.png)

5. <span data-ttu-id="dd526-135">Dans le volet de résultats hello, sélectionnez **canevas**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="dd526-135">In hello results panel, select **Canvas**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dd526-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd526-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dd526-138">Dans cette section, vous configurez et testez l’authentification unique Azure AD avec Canvas au moyen d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="dd526-138">In this section, you configure and test Azure AD single sign-on with Canvas based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="dd526-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans la zone de dessin est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd526-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Canvas is tooa user in Azure AD.</span></span> <span data-ttu-id="dd526-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans la zone de dessin hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="dd526-140">In other words, a link relationship between an Azure AD user and hello related user in Canvas needs toobe established.</span></span>

<span data-ttu-id="dd526-141">Dans la zone de dessin, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="dd526-141">In Canvas, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="dd526-142">tooconfigure et test Azure AD l’authentification unique avec une zone de dessin, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="dd526-142">tooconfigure and test Azure AD single sign-on with Canvas, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="dd526-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="dd526-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="dd526-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dd526-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dd526-145">**[Création d’un utilisateur de test canevas](#creating-a-canvas-test-user)**  -toohave un équivalent de Britta Simon dans la zone de dessin qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="dd526-145">**[Creating a Canvas test user](#creating-a-canvas-test-user)** - toohave a counterpart of Britta Simon in Canvas that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="dd526-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="dd526-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dd526-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="dd526-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dd526-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd526-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dd526-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de la zone de dessin.</span><span class="sxs-lookup"><span data-stu-id="dd526-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Canvas application.</span></span>

<span data-ttu-id="dd526-150">**tooconfigure Azure AD authentification unique avec une zone de dessin, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dd526-150">**tooconfigure Azure AD single sign-on with Canvas, perform hello following steps:**</span></span>

1. <span data-ttu-id="dd526-151">Bonjour portail Azure, sur hello **canevas** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="dd526-151">In hello Azure portal, on hello **Canvas** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="dd526-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="dd526-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_samlbase.png)

3. <span data-ttu-id="dd526-155">Sur hello **URL et le domaine de la zone de dessin** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="dd526-155">On hello **Canvas Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_url.png)

    <span data-ttu-id="dd526-157">a.</span><span class="sxs-lookup"><span data-stu-id="dd526-157">a.</span></span> <span data-ttu-id="dd526-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<tenant-name>.instructure.com`</span><span class="sxs-lookup"><span data-stu-id="dd526-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.instructure.com`</span></span>

    <span data-ttu-id="dd526-159">b.</span><span class="sxs-lookup"><span data-stu-id="dd526-159">b.</span></span> <span data-ttu-id="dd526-160">Bonjour **identificateur** zone de texte, valeur hello de type hello suivant le modèle à l’aide de :`https://<tenant-name>.instructure.com/saml2`</span><span class="sxs-lookup"><span data-stu-id="dd526-160">In hello **Identifier** textbox, type hello value using hello following pattern: `https://<tenant-name>.instructure.com/saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dd526-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="dd526-161">These values are not real.</span></span> <span data-ttu-id="dd526-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="dd526-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="dd526-163">Contact [équipe de support Client de la zone de dessin](https://community.canvaslms.com/community/help) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="dd526-163">Contact [Canvas Client support team](https://community.canvaslms.com/community/help) tooget these values.</span></span> 
 
4. <span data-ttu-id="dd526-164">Sur hello **le certificat de signature SAML** section, hello de copie **l’empreinte numérique** valeur du certificat.</span><span class="sxs-lookup"><span data-stu-id="dd526-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_certificate.png) 

5. <span data-ttu-id="dd526-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="dd526-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="dd526-168">Sur hello **Configuration de la zone de dessin** , cliquez sur **configurer la zone de dessin** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="dd526-168">On hello **Canvas Configuration** section, click **Configure Canvas** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="dd526-169">Hello de copie **URL de modification du mot de passe, l’URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="dd526-169">Copy hello **Change Password URL, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_configure.png) 
 
7. <span data-ttu-id="dd526-171">Dans une fenêtre de navigateur web, ouvrez une session dans le site d’entreprise tooyour canevas en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="dd526-171">In a different web browser window, log in tooyour Canvas company site as an administrator.</span></span>

8. <span data-ttu-id="dd526-172">Accédez trop**cours \> comptes gérés \> Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="dd526-172">Go too**Courses \> Managed Accounts \> Microsoft**.</span></span>
   
    <span data-ttu-id="dd526-173">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span><span class="sxs-lookup"><span data-stu-id="dd526-173">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span></span>

9. <span data-ttu-id="dd526-174">Dans le volet de navigation hello hello gauche, sélectionnez **authentification**, puis cliquez sur **Add New SAML Config**.</span><span class="sxs-lookup"><span data-stu-id="dd526-174">In hello navigation pane on hello left, select **Authentication**, and then click **Add New SAML Config**.</span></span>
   
    <span data-ttu-id="dd526-175">![Authentication](./media/active-directory-saas-canvas-lms-tutorial/IC775991.png "Authentication")</span><span class="sxs-lookup"><span data-stu-id="dd526-175">![Authentication](./media/active-directory-saas-canvas-lms-tutorial/IC775991.png "Authentication")</span></span>

10. <span data-ttu-id="dd526-176">Sur la page d’intégration en cours de hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="dd526-176">On hello Current Integration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="dd526-177">![Intégration actuelle](./media/active-directory-saas-canvas-lms-tutorial/IC775992.png "Intégration actuelle")</span><span class="sxs-lookup"><span data-stu-id="dd526-177">![Current Integration](./media/active-directory-saas-canvas-lms-tutorial/IC775992.png "Current Integration")</span></span>

    <span data-ttu-id="dd526-178">a.</span><span class="sxs-lookup"><span data-stu-id="dd526-178">a.</span></span> <span data-ttu-id="dd526-179">Dans **IdP Entity ID** zone de texte, valeur hello coller **ID d’entité SAML** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="dd526-179">In **IdP Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="dd526-180">b.</span><span class="sxs-lookup"><span data-stu-id="dd526-180">b.</span></span> <span data-ttu-id="dd526-181">Dans **Log On URL** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="dd526-181">In **Log On URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal .</span></span>

    <span data-ttu-id="dd526-182">c.</span><span class="sxs-lookup"><span data-stu-id="dd526-182">c.</span></span> <span data-ttu-id="dd526-183">Dans **URL de déconnexion** zone de texte, valeur hello coller **URL de déconnexion** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="dd526-183">In **Log Out URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="dd526-184">d.</span><span class="sxs-lookup"><span data-stu-id="dd526-184">d.</span></span> <span data-ttu-id="dd526-185">Dans **Change Password Link** zone de texte, valeur hello coller **URL de modification du mot de passe** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="dd526-185">In **Change Password Link** textbox, paste hello value of **Change Password URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="dd526-186">e.</span><span class="sxs-lookup"><span data-stu-id="dd526-186">e.</span></span> <span data-ttu-id="dd526-187">Dans **empreinte numérique du certificat** zone de texte, collez hello **l’empreinte numérique** valeur de certificat que vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="dd526-187">In **Certificate Fingerprint** textbox, paste hello **Thumbprint** value of certificate which you have copied from Azure portal.</span></span>      
        
    <span data-ttu-id="dd526-188">f.</span><span class="sxs-lookup"><span data-stu-id="dd526-188">f.</span></span> <span data-ttu-id="dd526-189">À partir de hello **Login Attribute** liste, sélectionnez **NameID**.</span><span class="sxs-lookup"><span data-stu-id="dd526-189">From hello **Login Attribute** list, select **NameID**.</span></span>

    <span data-ttu-id="dd526-190">g.</span><span class="sxs-lookup"><span data-stu-id="dd526-190">g.</span></span> <span data-ttu-id="dd526-191">À partir de hello **Identifier Format** liste, sélectionnez **emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="dd526-191">From hello **Identifier Format** list, select **emailAddress**.</span></span>

    <span data-ttu-id="dd526-192">h.</span><span class="sxs-lookup"><span data-stu-id="dd526-192">h.</span></span> <span data-ttu-id="dd526-193">Cliquez sur **Save Authentication Settings**.</span><span class="sxs-lookup"><span data-stu-id="dd526-193">Click **Save Authentication Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="dd526-194">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="dd526-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="dd526-195">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="dd526-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="dd526-196">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dd526-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dd526-197">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd526-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="dd526-198">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="dd526-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="dd526-200">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dd526-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="dd526-201">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="dd526-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dd526-203">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="dd526-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dd526-205">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="dd526-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dd526-207">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="dd526-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dd526-209">a.</span><span class="sxs-lookup"><span data-stu-id="dd526-209">a.</span></span> <span data-ttu-id="dd526-210">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dd526-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dd526-211">b.</span><span class="sxs-lookup"><span data-stu-id="dd526-211">b.</span></span> <span data-ttu-id="dd526-212">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dd526-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dd526-213">c.</span><span class="sxs-lookup"><span data-stu-id="dd526-213">c.</span></span> <span data-ttu-id="dd526-214">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="dd526-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="dd526-215">d.</span><span class="sxs-lookup"><span data-stu-id="dd526-215">d.</span></span> <span data-ttu-id="dd526-216">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="dd526-216">Click **Create**.</span></span>
 
### <a name="creating-a-canvas-test-user"></a><span data-ttu-id="dd526-217">Création d’un utilisateur de test Canvas</span><span class="sxs-lookup"><span data-stu-id="dd526-217">Creating a Canvas test user</span></span>

<span data-ttu-id="dd526-218">tooenable Azure AD les utilisateurs toolog dans tooCanvas, vous devez les configurer dans la zone de dessin.</span><span class="sxs-lookup"><span data-stu-id="dd526-218">tooenable Azure AD users toolog in tooCanvas, they must be provisioned into Canvas.</span></span>

<span data-ttu-id="dd526-219">En l’occurrence, cet approvisionnement d’utilisateur est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="dd526-219">In case of Canvas, user provisioning is a manual task.</span></span>

<span data-ttu-id="dd526-220">**tooprovision un compte d’utilisateur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dd526-220">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="dd526-221">Connectez-vous à tooyour **canevas** client.</span><span class="sxs-lookup"><span data-stu-id="dd526-221">Log in tooyour **Canvas** tenant.</span></span>

2. <span data-ttu-id="dd526-222">Accédez trop**cours \> comptes gérés \> Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="dd526-222">Go too**Courses \> Managed Accounts \> Microsoft**.</span></span>
   
   <span data-ttu-id="dd526-223">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span><span class="sxs-lookup"><span data-stu-id="dd526-223">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span></span>

3. <span data-ttu-id="dd526-224">Cliquez sur **Utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="dd526-224">Click **Users**.</span></span>
   
   <span data-ttu-id="dd526-225">![Utilisateurs](./media/active-directory-saas-canvas-lms-tutorial/IC775995.png "Utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="dd526-225">![Users](./media/active-directory-saas-canvas-lms-tutorial/IC775995.png "Users")</span></span>

4. <span data-ttu-id="dd526-226">Cliquez sur **Add New User**.</span><span class="sxs-lookup"><span data-stu-id="dd526-226">Click **Add New User**.</span></span>
   
   <span data-ttu-id="dd526-227">![Utilisateurs](./media/active-directory-saas-canvas-lms-tutorial/IC775996.png "Utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="dd526-227">![Users](./media/active-directory-saas-canvas-lms-tutorial/IC775996.png "Users")</span></span>

5. <span data-ttu-id="dd526-228">Dans Ajouter une page de boîte de dialogue Nouvel utilisateur de hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="dd526-228">On hello Add a New User dialog page, perform hello following steps:</span></span>
   
   <span data-ttu-id="dd526-229">![Ajouter un utilisateur](./media/active-directory-saas-canvas-lms-tutorial/IC775997.png "Ajouter un utilisateur")</span><span class="sxs-lookup"><span data-stu-id="dd526-229">![Add User](./media/active-directory-saas-canvas-lms-tutorial/IC775997.png "Add User")</span></span>
   
   <span data-ttu-id="dd526-230">a.</span><span class="sxs-lookup"><span data-stu-id="dd526-230">a.</span></span> <span data-ttu-id="dd526-231">Bonjour **nom complet** zone de texte, entrez hello les nom d’utilisateur comme **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dd526-231">In hello **Full Name** textbox, enter hello name of user like **BrittaSimon**.</span></span>

   <span data-ttu-id="dd526-232">b.</span><span class="sxs-lookup"><span data-stu-id="dd526-232">b.</span></span> <span data-ttu-id="dd526-233">Bonjour **messagerie** zone de texte, entrez hello adresse de messagerie de l’utilisateur comme  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="dd526-233">In hello **Email** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

   <span data-ttu-id="dd526-234">c.</span><span class="sxs-lookup"><span data-stu-id="dd526-234">c.</span></span> <span data-ttu-id="dd526-235">Bonjour **connexion** zone de texte, entrez l’adresse de messagerie de l’utilisateur hello Azure AD comme  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="dd526-235">In hello **Login** textbox, enter hello user’s Azure AD email address like **brittasimon@contoso.com**.</span></span>

   <span data-ttu-id="dd526-236">d.</span><span class="sxs-lookup"><span data-stu-id="dd526-236">d.</span></span> <span data-ttu-id="dd526-237">Sélectionnez **E-mail de l’utilisateur sur la création de ce compte hello**.</span><span class="sxs-lookup"><span data-stu-id="dd526-237">Select **Email hello user about this account creation**.</span></span>

   <span data-ttu-id="dd526-238">e.</span><span class="sxs-lookup"><span data-stu-id="dd526-238">e.</span></span> <span data-ttu-id="dd526-239">Cliquez sur **Add User**.</span><span class="sxs-lookup"><span data-stu-id="dd526-239">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="dd526-240">Vous pouvez utiliser n’importe quel autre zone de dessin utilisateur compte outil de création ou API fournie par Canvas tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="dd526-240">You can use any other Canvas user account creation tools or APIs provided by Canvas tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="dd526-241">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd526-241">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="dd526-242">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooCanvas.</span><span class="sxs-lookup"><span data-stu-id="dd526-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCanvas.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="dd526-244">**tooassign Britta Simon tooCanvas, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dd526-244">**tooassign Britta Simon tooCanvas, perform hello following steps:**</span></span>

1. <span data-ttu-id="dd526-245">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="dd526-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="dd526-247">Dans la liste des applications hello, sélectionnez **canevas**.</span><span class="sxs-lookup"><span data-stu-id="dd526-247">In hello applications list, select **Canvas**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_app.png) 

3. <span data-ttu-id="dd526-249">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="dd526-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="dd526-251">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="dd526-251">Click **Add** button.</span></span> <span data-ttu-id="dd526-252">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="dd526-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="dd526-254">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="dd526-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="dd526-255">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="dd526-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dd526-256">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="dd526-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dd526-257">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="dd526-257">Testing single sign-on</span></span>

<span data-ttu-id="dd526-258">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="dd526-258">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="dd526-259">Lorsque vous cliquez sur mosaïque du canevas hello Bonjour volet d’accès, vous devez obtenir l’application de zone de dessin tooyour automatiquement signé sur.</span><span class="sxs-lookup"><span data-stu-id="dd526-259">When you click hello Canvas tile in hello Access Panel, you should get automatically signed-on tooyour Canvas application.</span></span>
<span data-ttu-id="dd526-260">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dd526-260">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dd526-261">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="dd526-261">Additional resources</span></span>

* [<span data-ttu-id="dd526-262">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dd526-262">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dd526-263">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="dd526-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_203.png

