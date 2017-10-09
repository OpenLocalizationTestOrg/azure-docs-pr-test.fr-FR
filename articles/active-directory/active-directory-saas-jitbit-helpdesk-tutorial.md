---
title: "Didacticiel : Intégration d’Azure Active Directory avec Jitbit Helpdesk | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory à Jitbit Helpdesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 15ce27d4-0621-4103-8a34-e72c98d72ec3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 0f6c837bbb910c1e84f7ed9da676c5ab40f75338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jitbit-helpdesk"></a><span data-ttu-id="c50f9-103">Didacticiel : Intégration d’Azure Active Directory avec Jitbit Helpdesk</span><span class="sxs-lookup"><span data-stu-id="c50f9-103">Tutorial: Azure Active Directory integration with Jitbit Helpdesk</span></span>

<span data-ttu-id="c50f9-104">Dans ce didacticiel, vous apprendrez comment toointegrate Jitbit Helpdesk avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c50f9-104">In this tutorial, you learn how toointegrate Jitbit Helpdesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c50f9-105">Intégration de Jitbit Helpdesk à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="c50f9-105">Integrating Jitbit Helpdesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c50f9-106">Vous pouvez contrôler dans Azure AD qui a accès tooJitbit du support technique</span><span class="sxs-lookup"><span data-stu-id="c50f9-106">You can control in Azure AD who has access tooJitbit Helpdesk</span></span>
- <span data-ttu-id="c50f9-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooJitbit du support technique (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="c50f9-107">You can enable your users tooautomatically get signed-on tooJitbit Helpdesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c50f9-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="c50f9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c50f9-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c50f9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c50f9-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c50f9-110">Prerequisites</span></span>

<span data-ttu-id="c50f9-111">tooconfigure intégration d’Azure AD à Jitbit Helpdesk, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c50f9-111">tooconfigure Azure AD integration with Jitbit Helpdesk, you need hello following items:</span></span>

- <span data-ttu-id="c50f9-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="c50f9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c50f9-113">Un abonnement Jitbit Helpdesk pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="c50f9-113">A Jitbit Helpdesk single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c50f9-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="c50f9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c50f9-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="c50f9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c50f9-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="c50f9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c50f9-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c50f9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c50f9-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="c50f9-118">Scenario description</span></span>
<span data-ttu-id="c50f9-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="c50f9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c50f9-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="c50f9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c50f9-121">Ajout de Jitbit Helpdesk à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="c50f9-121">Adding Jitbit Helpdesk from hello gallery</span></span>
2. <span data-ttu-id="c50f9-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c50f9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jitbit-helpdesk-from-hello-gallery"></a><span data-ttu-id="c50f9-123">Ajout de Jitbit Helpdesk à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="c50f9-123">Adding Jitbit Helpdesk from hello gallery</span></span>
<span data-ttu-id="c50f9-124">intégration de hello tooconfigure de Jitbit Helpdesk dans Azure AD, vous devez tooadd Jitbit Helpdesk à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="c50f9-124">tooconfigure hello integration of Jitbit Helpdesk into Azure AD, you need tooadd Jitbit Helpdesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c50f9-125">**tooadd Jitbit Helpdesk à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c50f9-125">**tooadd Jitbit Helpdesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c50f9-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="c50f9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c50f9-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="c50f9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c50f9-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c50f9-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="c50f9-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c50f9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="c50f9-133">Dans la zone de recherche de hello, tapez **Jitbit Helpdesk**.</span><span class="sxs-lookup"><span data-stu-id="c50f9-133">In hello search box, type **Jitbit Helpdesk**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_search.png)

5. <span data-ttu-id="c50f9-135">Dans le volet de résultats hello, sélectionnez **Jitbit Helpdesk**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c50f9-135">In hello results panel, select **Jitbit Helpdesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c50f9-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c50f9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c50f9-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Jitbit Helpdesk avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="c50f9-138">In this section, you configure and test Azure AD single sign-on with Jitbit Helpdesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c50f9-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Jitbit Helpdesk est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c50f9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Jitbit Helpdesk is tooa user in Azure AD.</span></span> <span data-ttu-id="c50f9-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur de Jitbit Helpdesk hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="c50f9-140">In other words, a link relationship between an Azure AD user and hello related user in Jitbit Helpdesk needs toobe established.</span></span>

<span data-ttu-id="c50f9-141">Dans Jitbit Helpdesk, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="c50f9-141">In Jitbit Helpdesk, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c50f9-142">tooconfigure et test Azure AD l’authentification unique à Jitbit Helpdesk, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="c50f9-142">tooconfigure and test Azure AD single sign-on with Jitbit Helpdesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c50f9-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="c50f9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c50f9-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c50f9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c50f9-145">**[Création d’un utilisateur de test de Jitbit Helpdesk](#creating-a-jitbit-helpdesk-test-user)**  -toohave un équivalent de Britta Simon dans Jitbit Helpdesk qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c50f9-145">**[Creating a Jitbit Helpdesk test user](#creating-a-jitbit-helpdesk-test-user)** - toohave a counterpart of Britta Simon in Jitbit Helpdesk that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c50f9-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c50f9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c50f9-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="c50f9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c50f9-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c50f9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c50f9-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="c50f9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Jitbit Helpdesk application.</span></span>

<span data-ttu-id="c50f9-150">**tooconfigure Azure AD single sign-on avec Jitbit Helpdesk, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c50f9-150">**tooconfigure Azure AD single sign-on with Jitbit Helpdesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="c50f9-151">Bonjour portail Azure, sur hello **Jitbit Helpdesk** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="c50f9-151">In hello Azure portal, on hello **Jitbit Helpdesk** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="c50f9-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c50f9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_samlbase.png)

3. <span data-ttu-id="c50f9-155">Sur hello **Jitbit Helpdesk domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c50f9-155">On hello **Jitbit Helpdesk Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_url.png)

    <span data-ttu-id="c50f9-157">a.</span><span class="sxs-lookup"><span data-stu-id="c50f9-157">a.</span></span> <span data-ttu-id="c50f9-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :</span><span class="sxs-lookup"><span data-stu-id="c50f9-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span> 
    | |     
    | ----------------------------------------|
    | `https://<hostname>/helpdesk/User/Login`|
    | `https://<tenant-name>.Jitbit.com`|
    | |
    
    > [!NOTE] 
    > <span data-ttu-id="c50f9-159">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="c50f9-159">This value is not real.</span></span> <span data-ttu-id="c50f9-160">Mettre à jour de cette valeur avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="c50f9-160">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="c50f9-161">Contact [équipe de support technique Jitbit Helpdesk Client](https://www.jitbit.com/support/) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="c50f9-161">Contact [Jitbit Helpdesk Client support team](https://www.jitbit.com/support/) tooget this value.</span></span> 
    
    <span data-ttu-id="c50f9-162">b.</span><span class="sxs-lookup"><span data-stu-id="c50f9-162">b.</span></span>  <span data-ttu-id="c50f9-163">Bonjour **identificateur** zone de texte, tapez une URL comme suit :`https://www.jitbit.com/web-helpdesk/`</span><span class="sxs-lookup"><span data-stu-id="c50f9-163">In hello **Identifier** textbox, type a URL as following: `https://www.jitbit.com/web-helpdesk/`</span></span>

    
 


4. <span data-ttu-id="c50f9-164">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="c50f9-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_certificate.png) 

5. <span data-ttu-id="c50f9-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="c50f9-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c50f9-168">Sur hello **Jitbit Helpdesk Configuration** , cliquez sur **configurer Jitbit Helpdesk** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="c50f9-168">On hello **Jitbit Helpdesk Configuration** section, click **Configure Jitbit Helpdesk** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c50f9-169">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="c50f9-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_configure.png) 

7. <span data-ttu-id="c50f9-171">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Jitbit Helpdesk en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="c50f9-171">In a different web browser window, log into your Jitbit Helpdesk company site as an administrator.</span></span>

8. <span data-ttu-id="c50f9-172">Dans la barre d’outils de hello en haut de hello, cliquez sur **Administration**.</span><span class="sxs-lookup"><span data-stu-id="c50f9-172">In hello toolbar on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="c50f9-173">![Administration](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="c50f9-173">![Administration](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administration")</span></span>

9. <span data-ttu-id="c50f9-174">Cliquez sur **General settings**.</span><span class="sxs-lookup"><span data-stu-id="c50f9-174">Click **General settings**.</span></span>
   
    <span data-ttu-id="c50f9-175">![Utilisateurs, entreprises et autorisations](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "Utilisateurs, entreprises et autorisations")</span><span class="sxs-lookup"><span data-stu-id="c50f9-175">![Users, companies, and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "Users, companies, and permissions")</span></span>

10. <span data-ttu-id="c50f9-176">Bonjour **les paramètres d’authentification** configuration section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c50f9-176">In hello **Authentication settings** configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="c50f9-177">![Authentication settings](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "Authentication settings")</span><span class="sxs-lookup"><span data-stu-id="c50f9-177">![Authentication settings](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "Authentication settings")</span></span>
    
    <span data-ttu-id="c50f9-178">a.</span><span class="sxs-lookup"><span data-stu-id="c50f9-178">a.</span></span> <span data-ttu-id="c50f9-179">Sélectionnez **activer authentification unique SAML 2.0**, toosign Single Sign-On (SSO), l’utilisation avec **OneLogin**.</span><span class="sxs-lookup"><span data-stu-id="c50f9-179">Select **Enable SAML 2.0 single sign on**, toosign in using Single Sign-On (SSO), with **OneLogin**.</span></span>

    <span data-ttu-id="c50f9-180">b.</span><span class="sxs-lookup"><span data-stu-id="c50f9-180">b.</span></span> <span data-ttu-id="c50f9-181">Bonjour **URL de point de terminaison** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c50f9-181">In hello **EndPoint URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="c50f9-182">c.</span><span class="sxs-lookup"><span data-stu-id="c50f9-182">c.</span></span> <span data-ttu-id="c50f9-183">Ouvrez votre **base-64** certificat dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite toohello **certificat X.509** zone de texte</span><span class="sxs-lookup"><span data-stu-id="c50f9-183">Open your **base-64** encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox</span></span>

    <span data-ttu-id="c50f9-184">d.</span><span class="sxs-lookup"><span data-stu-id="c50f9-184">d.</span></span> <span data-ttu-id="c50f9-185">Cliquez sur **Save changes**.</span><span class="sxs-lookup"><span data-stu-id="c50f9-185">Click **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="c50f9-186">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="c50f9-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c50f9-187">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="c50f9-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c50f9-188">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c50f9-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c50f9-189">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="c50f9-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="c50f9-190">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="c50f9-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="c50f9-192">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c50f9-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c50f9-193">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="c50f9-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c50f9-195">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="c50f9-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c50f9-197">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="c50f9-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c50f9-199">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c50f9-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c50f9-201">a.</span><span class="sxs-lookup"><span data-stu-id="c50f9-201">a.</span></span> <span data-ttu-id="c50f9-202">Bonjour **nom** zone de texte, nom du type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c50f9-202">In hello **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="c50f9-203">b.</span><span class="sxs-lookup"><span data-stu-id="c50f9-203">b.</span></span> <span data-ttu-id="c50f9-204">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c50f9-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c50f9-205">c.</span><span class="sxs-lookup"><span data-stu-id="c50f9-205">c.</span></span> <span data-ttu-id="c50f9-206">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="c50f9-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c50f9-207">d.</span><span class="sxs-lookup"><span data-stu-id="c50f9-207">d.</span></span> <span data-ttu-id="c50f9-208">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="c50f9-208">Click **Create**.</span></span>
 
### <a name="creating-a-jitbit-helpdesk-test-user"></a><span data-ttu-id="c50f9-209">Création d’un utilisateur de test Jitbit Helpdesk</span><span class="sxs-lookup"><span data-stu-id="c50f9-209">Creating a Jitbit Helpdesk test user</span></span>

<span data-ttu-id="c50f9-210">Dans l’ordre tooenable le toolog d’utilisateurs Azure AD à Jitbit Helpdesk, vous devez les configurer dans Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="c50f9-210">In order tooenable Azure AD users toolog into Jitbit Helpdesk, they must be provisioned into Jitbit Helpdesk.</span></span>  <span data-ttu-id="c50f9-211">Dans les cas de hello de Jitbit Helpdesk, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="c50f9-211">In hello case of Jitbit Helpdesk, provisioning is a manual task.</span></span>

<span data-ttu-id="c50f9-212">**tooprovision un compte d’utilisateur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c50f9-212">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="c50f9-213">Connectez-vous à tooyour **Jitbit Helpdesk** client.</span><span class="sxs-lookup"><span data-stu-id="c50f9-213">Log in tooyour **Jitbit Helpdesk** tenant.</span></span>

2. <span data-ttu-id="c50f9-214">Dans le menu hello haut de hello, cliquez sur **Administration**.</span><span class="sxs-lookup"><span data-stu-id="c50f9-214">In hello menu on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="c50f9-215">![Administration](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="c50f9-215">![Administration](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administration")</span></span>

3. <span data-ttu-id="c50f9-216">Cliquez sur **Users, companies and permissions**.</span><span class="sxs-lookup"><span data-stu-id="c50f9-216">Click **Users, companies and permissions**.</span></span>
   
    <span data-ttu-id="c50f9-217">![Utilisateurs, entreprises et autorisations](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "Utilisateurs, entreprises et autorisations")</span><span class="sxs-lookup"><span data-stu-id="c50f9-217">![Users, companies, and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "Users, companies, and permissions")</span></span>

4. <span data-ttu-id="c50f9-218">Cliquez sur **Add User**.</span><span class="sxs-lookup"><span data-stu-id="c50f9-218">Click **Add user**.</span></span>
   
    <span data-ttu-id="c50f9-219">![Add user](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "Add user")</span><span class="sxs-lookup"><span data-stu-id="c50f9-219">![Add user](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "Add user")</span></span>
   
5. <span data-ttu-id="c50f9-220">Dans la section Création de hello, de type hello de hello Azure AD compte tooprovision comme suit :</span><span class="sxs-lookup"><span data-stu-id="c50f9-220">In hello Create section, type hello data of hello Azure AD account you want tooprovision as follows:</span></span>

    <span data-ttu-id="c50f9-221">![Créer](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "créer")</span><span class="sxs-lookup"><span data-stu-id="c50f9-221">![Create](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "Create")</span></span>
   
   <span data-ttu-id="c50f9-222">a.</span><span class="sxs-lookup"><span data-stu-id="c50f9-222">a.</span></span> <span data-ttu-id="c50f9-223">Bonjour **nom d’utilisateur** zone de texte, type **BrittaSimon**, nom d’utilisateur hello comme hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c50f9-223">In hello **Username** textbox, type **BrittaSimon**, hello user name as in hello Azure portal.</span></span>

   <span data-ttu-id="c50f9-224">b.</span><span class="sxs-lookup"><span data-stu-id="c50f9-224">b.</span></span> <span data-ttu-id="c50f9-225">Bonjour **messagerie** telles que la messagerie de type d’utilisateur de hello zone de texte,  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="c50f9-225">In hello **Email** textbox, type email of hello user like **BrittaSimon@contoso.com**.</span></span>

   <span data-ttu-id="c50f9-226">c.</span><span class="sxs-lookup"><span data-stu-id="c50f9-226">c.</span></span> <span data-ttu-id="c50f9-227">Bonjour **prénom** zone de texte, type prénom utilisateur hello comme **Brian**.</span><span class="sxs-lookup"><span data-stu-id="c50f9-227">In hello **First Name** textbox, type first name of hello user like **Britta**.</span></span>

   <span data-ttu-id="c50f9-228">d.</span><span class="sxs-lookup"><span data-stu-id="c50f9-228">d.</span></span> <span data-ttu-id="c50f9-229">Bonjour **nom** zone de texte, nom d’utilisateur hello comme type **Simon**.</span><span class="sxs-lookup"><span data-stu-id="c50f9-229">In hello **Last Name** textbox, type last name of hello user like **Simon**.</span></span>
   
   <span data-ttu-id="c50f9-230">e.</span><span class="sxs-lookup"><span data-stu-id="c50f9-230">e.</span></span> <span data-ttu-id="c50f9-231">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="c50f9-231">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="c50f9-232">Vous pouvez utiliser n’importe quel autre Jitbit Helpdesk utilisateur compte outil de création ou API fournie par Jitbit Helpdesk tooprovision comptes d’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c50f9-232">You can use any other Jitbit Helpdesk user account creation tools or APIs provided by Jitbit Helpdesk tooprovision Azure AD user accounts.</span></span>
> 
        

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c50f9-233">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c50f9-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c50f9-234">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooJitbit du support technique.</span><span class="sxs-lookup"><span data-stu-id="c50f9-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJitbit Helpdesk.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="c50f9-236">**tooassign Britta Simon tooJitbit du support technique, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c50f9-236">**tooassign Britta Simon tooJitbit Helpdesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="c50f9-237">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c50f9-237">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="c50f9-239">Dans la liste des applications hello, sélectionnez **Jitbit Helpdesk**.</span><span class="sxs-lookup"><span data-stu-id="c50f9-239">In hello applications list, select **Jitbit Helpdesk**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_app.png) 

3. <span data-ttu-id="c50f9-241">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c50f9-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="c50f9-243">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="c50f9-243">Click **Add** button.</span></span> <span data-ttu-id="c50f9-244">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c50f9-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="c50f9-246">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="c50f9-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c50f9-247">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c50f9-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c50f9-248">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c50f9-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c50f9-249">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="c50f9-249">Testing single sign-on</span></span>

<span data-ttu-id="c50f9-250">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="c50f9-250">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c50f9-251">Lorsque vous cliquez sur hello Jitbit Helpdesk vignette Bonjour volet d’accès, vous devez obtenir la page de connexion de l’application de Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="c50f9-251">When you click hello Jitbit Helpdesk tile in hello Access Panel, you should get login page of Jitbit Helpdesk application.</span></span>
<span data-ttu-id="c50f9-252">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c50f9-252">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c50f9-253">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="c50f9-253">Additional resources</span></span>

* [<span data-ttu-id="c50f9-254">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c50f9-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c50f9-255">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="c50f9-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_203.png

