---
title: "Didacticiel : intégration d’Azure Active Directory à Small Improvements | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de petites améliorations."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 59c8a112-41e1-4337-9ef3-3d7029780d61
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 33213fe4b61f5005cf78bee2c05b2b1e5e71ae8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-small-improvements"></a><span data-ttu-id="f2d2a-103">Didacticiel : intégration d’Azure Active Directory avec Small Improvements</span><span class="sxs-lookup"><span data-stu-id="f2d2a-103">Tutorial: Azure Active Directory integration with Small Improvements</span></span>

<span data-ttu-id="f2d2a-104">Dans ce didacticiel, vous apprendrez comment toointegrate petites améliorations avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f2d2a-104">In this tutorial, you learn how toointegrate Small Improvements with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f2d2a-105">Intégration de petites améliorations à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="f2d2a-105">Integrating Small Improvements with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f2d2a-106">Vous pouvez contrôler dans Azure AD qui a accès tooSmall améliorations</span><span class="sxs-lookup"><span data-stu-id="f2d2a-106">You can control in Azure AD who has access tooSmall Improvements</span></span>
- <span data-ttu-id="f2d2a-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSmall améliorations (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="f2d2a-107">You can enable your users tooautomatically get signed-on tooSmall Improvements (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f2d2a-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="f2d2a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f2d2a-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f2d2a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f2d2a-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f2d2a-110">Prerequisites</span></span>

<span data-ttu-id="f2d2a-111">tooconfigure intégration d’Azure AD avec petites améliorations, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f2d2a-111">tooconfigure Azure AD integration with Small Improvements, you need hello following items:</span></span>

- <span data-ttu-id="f2d2a-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="f2d2a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f2d2a-113">Un abonnement Small Improvements pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="f2d2a-113">A Small Improvements single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f2d2a-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f2d2a-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="f2d2a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f2d2a-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f2d2a-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois ici [Offre d’essai](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f2d2a-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f2d2a-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="f2d2a-118">Scenario description</span></span>
<span data-ttu-id="f2d2a-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f2d2a-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="f2d2a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f2d2a-121">Ajout de petites améliorations à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="f2d2a-121">Adding Small Improvements from hello gallery</span></span>
2. <span data-ttu-id="f2d2a-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f2d2a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-small-improvements-from-hello-gallery"></a><span data-ttu-id="f2d2a-123">Ajout de petites améliorations à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="f2d2a-123">Adding Small Improvements from hello gallery</span></span>
<span data-ttu-id="f2d2a-124">tooconfigure hello intégration de petites améliorations dans Azure AD, vous devez tooadd petites améliorations à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-124">tooconfigure hello integration of Small Improvements into Azure AD, you need tooadd Small Improvements from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f2d2a-125">**tooadd petites améliorations à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f2d2a-125">**tooadd Small Improvements from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f2d2a-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f2d2a-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f2d2a-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="f2d2a-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="f2d2a-133">Dans la zone de recherche de hello, tapez **petites améliorations**.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-133">In hello search box, type **Small Improvements**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_search.png)

5. <span data-ttu-id="f2d2a-135">Dans le volet de résultats hello, sélectionnez **petites améliorations**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-135">In hello results panel, select **Small Improvements**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f2d2a-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f2d2a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f2d2a-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD après de Small Improvements, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="f2d2a-138">In this section, you configure and test Azure AD single sign-on with Small Improvements based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f2d2a-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans les petites améliorations est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Small Improvements is tooa user in Azure AD.</span></span> <span data-ttu-id="f2d2a-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et l’utilisateur dans les petites améliorations hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-140">In other words, a link relationship between an Azure AD user and hello related user in Small Improvements needs toobe established.</span></span>

<span data-ttu-id="f2d2a-141">Dans les petites améliorations, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-141">In Small Improvements, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f2d2a-142">tooconfigure et test Azure AD l’authentification unique avec petites améliorations, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="f2d2a-142">tooconfigure and test Azure AD single sign-on with Small Improvements, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f2d2a-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f2d2a-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f2d2a-145">**[Création d’un utilisateur de test de petites améliorations](#creating-a-small-improvements-test-user)**  -toohave un équivalent de Britta Simon petites améliorations qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-145">**[Creating a Small Improvements test user](#creating-a-small-improvements-test-user)** - toohave a counterpart of Britta Simon in Small Improvements that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f2d2a-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f2d2a-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f2d2a-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f2d2a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f2d2a-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de petites améliorations.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Small Improvements application.</span></span>

<span data-ttu-id="f2d2a-150">**tooconfigure Azure AD single sign-on avec petites améliorations, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f2d2a-150">**tooconfigure Azure AD single sign-on with Small Improvements, perform hello following steps:**</span></span>

1. <span data-ttu-id="f2d2a-151">Bonjour portail Azure, sur hello **petites améliorations** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-151">In hello Azure portal, on hello **Small Improvements** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="f2d2a-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_samlbase.png)

3. <span data-ttu-id="f2d2a-155">Sur hello **petites améliorations de domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f2d2a-155">On hello **Small Improvements Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_url.png)

    <span data-ttu-id="f2d2a-157">a.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-157">a.</span></span> <span data-ttu-id="f2d2a-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.small-improvements.com`</span><span class="sxs-lookup"><span data-stu-id="f2d2a-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.small-improvements.com`</span></span>

    <span data-ttu-id="f2d2a-159">b.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-159">b.</span></span> <span data-ttu-id="f2d2a-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.small-improvements.com`</span><span class="sxs-lookup"><span data-stu-id="f2d2a-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.small-improvements.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f2d2a-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-161">These values are not real.</span></span> <span data-ttu-id="f2d2a-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f2d2a-163">Contact [équipe de support technique de petites améliorations Client](mailto:support@small-improvements.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-163">Contact [Small Improvements Client support team](mailto:support@small-improvements.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="f2d2a-164">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_certificate.png) 

5. <span data-ttu-id="f2d2a-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="f2d2a-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f2d2a-168">Sur hello **petites améliorations Configuration** , cliquez sur **configurer petites améliorations** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-168">On hello **Small Improvements Configuration** section, click **Configure Small Improvements** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f2d2a-169">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="f2d2a-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_configure.png) 

7. <span data-ttu-id="f2d2a-171">Dans une autre fenêtre de navigateur, connectez-vous sur le site d’entreprise tooyour petites améliorations en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-171">In another browser window, sign on tooyour Small Improvements company site as an administrator.</span></span>

8. <span data-ttu-id="f2d2a-172">À partir de la page du tableau de bord principal hello, cliquez sur **Administration** sur bouton hello gauche.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-172">From hello main dashboard page, click **Administration** button on hello left.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_06.png) 

9. <span data-ttu-id="f2d2a-174">Cliquez sur hello **SSO SAML** bouton **intégrations** section.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-174">Click hello **SAML SSO** button from **Integrations** section.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_07.png) 

10. <span data-ttu-id="f2d2a-176">Sur la page de configuration de l’authentification unique de hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f2d2a-176">On hello SSO Setup page, perform hello following steps:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_08.png)  

    <span data-ttu-id="f2d2a-178">a.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-178">a.</span></span> <span data-ttu-id="f2d2a-179">Bonjour **point de terminaison HTTP** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-179">In hello **HTTP Endpoint** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="f2d2a-180">b.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-180">b.</span></span> <span data-ttu-id="f2d2a-181">Ouvrez votre certificat téléchargé dans le bloc-notes, hello copie le contenu et le coller ensuite dans hello **x509 certificat** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-181">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **x509 Certificate** textbox.</span></span> 

    <span data-ttu-id="f2d2a-182">c.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-182">c.</span></span> <span data-ttu-id="f2d2a-183">Si vous le souhaitez toohave SSO et connexion formulaire option d’authentification disponible pour les utilisateurs, puis vérifiez hello **activer un accès via une connexion/mot de passe trop** option.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-183">If you wish toohave SSO and Login form authentication option available for users, then check hello **Enable access via login/password too** option.</span></span>  

    <span data-ttu-id="f2d2a-184">d.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-184">d.</span></span> <span data-ttu-id="f2d2a-185">Entrez le bouton connexion SSO hello hello valeur appropriée tooName Bonjour **SAML invite** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-185">Enter hello appropriate value tooName hello SSO Login button in hello **SAML Prompt** textbox.</span></span>  

    <span data-ttu-id="f2d2a-186">e.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-186">e.</span></span> <span data-ttu-id="f2d2a-187">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="f2d2a-188">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="f2d2a-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f2d2a-189">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f2d2a-190">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f2d2a-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f2d2a-191">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="f2d2a-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="f2d2a-192">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="f2d2a-194">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f2d2a-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f2d2a-195">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f2d2a-197">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f2d2a-199">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f2d2a-201">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f2d2a-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f2d2a-203">a.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-203">a.</span></span> <span data-ttu-id="f2d2a-204">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f2d2a-205">b.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-205">b.</span></span> <span data-ttu-id="f2d2a-206">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f2d2a-207">c.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-207">c.</span></span> <span data-ttu-id="f2d2a-208">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f2d2a-209">d.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-209">d.</span></span> <span data-ttu-id="f2d2a-210">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-210">Click **Create**.</span></span>
 
### <a name="creating-a-small-improvements-test-user"></a><span data-ttu-id="f2d2a-211">Création d'un utilisateur de test Small Improvements</span><span class="sxs-lookup"><span data-stu-id="f2d2a-211">Creating a Small Improvements test user</span></span>

<span data-ttu-id="f2d2a-212">tooenable Azure AD les utilisateurs toolog dans tooSmall améliorations, vous devez les configurer dans les petites améliorations.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-212">tooenable Azure AD users toolog in tooSmall Improvements, they must be provisioned into Small Improvements.</span></span> <span data-ttu-id="f2d2a-213">Dans les cas de hello de petites améliorations, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-213">In hello case of Small Improvements, provisioning is a manual task.</span></span>

<span data-ttu-id="f2d2a-214">**tooprovision un compte d’utilisateur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f2d2a-214">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="f2d2a-215">Site d’entreprise petites améliorations tooyour ouverture de session en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-215">Sign-on tooyour Small Improvements company site as an administrator.</span></span>

2. <span data-ttu-id="f2d2a-216">À partir de la page d’accueil hello, passez toohello menu hello gauche, cliquez sur **Administration**.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-216">From hello Home page, go toohello menu on hello left, click **Administration**.</span></span>

3. <span data-ttu-id="f2d2a-217">Cliquez sur hello **répertoire utilisateur** bouton à partir de la section Gestion de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-217">Click hello **User Directory** button from User Management section.</span></span> 
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_10.png) 

4. <span data-ttu-id="f2d2a-219">Cliquez sur **Add Users**.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-219">Click **Add users**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_11.png) 

5. <span data-ttu-id="f2d2a-221">Sur hello **ajouter des utilisateurs** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f2d2a-221">On hello **Add Users** dialog, perform hello following steps:</span></span> 

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_12.png)
    
    <span data-ttu-id="f2d2a-223">a.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-223">a.</span></span> <span data-ttu-id="f2d2a-224">Entrez hello **prénom** d’utilisateur comme **Brian**.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-224">Enter hello **first name** of user like **Britta**.</span></span>

    <span data-ttu-id="f2d2a-225">b.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-225">b.</span></span> <span data-ttu-id="f2d2a-226">Entrez hello **nom** d’utilisateur comme **Simon**.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-226">Enter hello **Last name** of user like **Simon**.</span></span>

    <span data-ttu-id="f2d2a-227">c.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-227">c.</span></span> <span data-ttu-id="f2d2a-228">Entrez hello **messagerie** d’utilisateur comme  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="f2d2a-228">Enter hello **Email** of user like **brittasimon@contoso.com**.</span></span> 

    <span data-ttu-id="f2d2a-229">d.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-229">d.</span></span> <span data-ttu-id="f2d2a-230">Vous pouvez également choisir le message de personnel tooenter hello Bonjour **envoyer un courrier électronique de notification** boîte.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-230">You can also choose tooenter hello personal message in hello **Send notification email** box.</span></span> <span data-ttu-id="f2d2a-231">Si vous ne souhaitez pas de notification de hello toosend, puis désactivez cette case à cocher.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-231">If you do not wish toosend hello notification, then uncheck this checkbox.</span></span>

    <span data-ttu-id="f2d2a-232">e.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-232">e.</span></span> <span data-ttu-id="f2d2a-233">Cliquez sur **Créer des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-233">Click **Create Users**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f2d2a-234">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f2d2a-234">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f2d2a-235">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooSmall améliorations.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSmall Improvements.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="f2d2a-237">**tooassign Britta Simon tooSmall améliorations, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f2d2a-237">**tooassign Britta Simon tooSmall Improvements, perform hello following steps:**</span></span>

1. <span data-ttu-id="f2d2a-238">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-238">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="f2d2a-240">Dans la liste des applications hello, sélectionnez **petites améliorations**.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-240">In hello applications list, select **Small Improvements**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_app.png) 

3. <span data-ttu-id="f2d2a-242">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="f2d2a-244">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-244">Click **Add** button.</span></span> <span data-ttu-id="f2d2a-245">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="f2d2a-247">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f2d2a-248">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f2d2a-249">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f2d2a-250">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="f2d2a-250">Testing single sign-on</span></span>

<span data-ttu-id="f2d2a-251">objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-251">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="f2d2a-252">Lorsque vous cliquez sur hello petites améliorations vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour application de petites améliorations.</span><span class="sxs-lookup"><span data-stu-id="f2d2a-252">When you click hello Small Improvements tile in hello Access Panel, you should get automatically signed-on tooyour Small Improvements application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f2d2a-253">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="f2d2a-253">Additional resources</span></span>

* [<span data-ttu-id="f2d2a-254">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f2d2a-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f2d2a-255">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="f2d2a-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_203.png

