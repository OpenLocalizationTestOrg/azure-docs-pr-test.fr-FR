---
title: "Didacticiel : intégration d’Azure Active Directory avec Kintone | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Kintone."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2b947dc-e1a8-4f5f-b40e-2c5180648e4f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 4f61fb95c643743504699b175beeff06e01c95c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kintone"></a><span data-ttu-id="a5f26-103">Didacticiel : intégration d’Azure Active Directory avec Kintone</span><span class="sxs-lookup"><span data-stu-id="a5f26-103">Tutorial: Azure Active Directory integration with Kintone</span></span>

<span data-ttu-id="a5f26-104">Dans ce didacticiel, vous apprendrez comment toointegrate Kintone avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a5f26-104">In this tutorial, you learn how toointegrate Kintone with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a5f26-105">Intégration de Kintone à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="a5f26-105">Integrating Kintone with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a5f26-106">Vous pouvez contrôler dans Azure AD qui a accès tooKintone</span><span class="sxs-lookup"><span data-stu-id="a5f26-106">You can control in Azure AD who has access tooKintone</span></span>
- <span data-ttu-id="a5f26-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooKintone (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5f26-107">You can enable your users tooautomatically get signed-on tooKintone (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a5f26-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="a5f26-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a5f26-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a5f26-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5f26-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a5f26-110">Prerequisites</span></span>

<span data-ttu-id="a5f26-111">tooconfigure intégration d’Azure AD à Kintone, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a5f26-111">tooconfigure Azure AD integration with Kintone, you need hello following items:</span></span>

- <span data-ttu-id="a5f26-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5f26-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a5f26-113">Un abonnement Kintone pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="a5f26-113">A Kintone single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a5f26-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="a5f26-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a5f26-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="a5f26-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a5f26-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="a5f26-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a5f26-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a5f26-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a5f26-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="a5f26-118">Scenario description</span></span>
<span data-ttu-id="a5f26-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="a5f26-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a5f26-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="a5f26-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a5f26-121">Ajout de Kintone à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="a5f26-121">Adding Kintone from hello gallery</span></span>
2. <span data-ttu-id="a5f26-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5f26-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kintone-from-hello-gallery"></a><span data-ttu-id="a5f26-123">Ajout de Kintone à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="a5f26-123">Adding Kintone from hello gallery</span></span>
<span data-ttu-id="a5f26-124">intégration de hello tooconfigure de Kintone dans Azure AD, vous devez tooadd Kintone à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="a5f26-124">tooconfigure hello integration of Kintone into Azure AD, you need tooadd Kintone from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a5f26-125">**tooadd Kintone à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a5f26-125">**tooadd Kintone from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a5f26-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="a5f26-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a5f26-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="a5f26-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a5f26-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a5f26-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="a5f26-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a5f26-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="a5f26-133">Dans la zone de recherche de hello, tapez **Kintone**.</span><span class="sxs-lookup"><span data-stu-id="a5f26-133">In hello search box, type **Kintone**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_search.png)

5. <span data-ttu-id="a5f26-135">Dans le volet de résultats hello, sélectionnez **Kintone**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="a5f26-135">In hello results panel, select **Kintone**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a5f26-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5f26-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a5f26-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Kintone, grâce à un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="a5f26-138">In this section, you configure and test Azure AD single sign-on with Kintone based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a5f26-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Kintone est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a5f26-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kintone is tooa user in Azure AD.</span></span> <span data-ttu-id="a5f26-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Kintone doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="a5f26-140">In other words, a link relationship between an Azure AD user and hello related user in Kintone needs toobe established.</span></span>

<span data-ttu-id="a5f26-141">En l’occurrence, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="a5f26-141">In Kintone, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a5f26-142">tooconfigure et test Azure AD l’authentification unique avec Kintone, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="a5f26-142">tooconfigure and test Azure AD single sign-on with Kintone, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a5f26-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="a5f26-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a5f26-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a5f26-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a5f26-145">**[Création d’un utilisateur de test de Kintone](#creating-a-kintone-test-user)**  -toohave un équivalent de Britta Simon dans Kintone est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a5f26-145">**[Creating a Kintone test user](#creating-a-kintone-test-user)** - toohave a counterpart of Britta Simon in Kintone that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a5f26-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="a5f26-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a5f26-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="a5f26-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a5f26-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5f26-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a5f26-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de Kintone.</span><span class="sxs-lookup"><span data-stu-id="a5f26-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kintone application.</span></span>

<span data-ttu-id="a5f26-150">**tooconfigure Azure AD single sign-on avec Kintone, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a5f26-150">**tooconfigure Azure AD single sign-on with Kintone, perform hello following steps:**</span></span>

1. <span data-ttu-id="a5f26-151">Bonjour portail Azure, sur hello **Kintone** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="a5f26-151">In hello Azure portal, on hello **Kintone** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="a5f26-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="a5f26-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_samlbase.png)

3. <span data-ttu-id="a5f26-155">Sur hello **Kintone domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="a5f26-155">On hello **Kintone Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_url.png)

    <span data-ttu-id="a5f26-157">a.</span><span class="sxs-lookup"><span data-stu-id="a5f26-157">a.</span></span> <span data-ttu-id="a5f26-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.kintone.com`</span><span class="sxs-lookup"><span data-stu-id="a5f26-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.kintone.com`</span></span>

    <span data-ttu-id="a5f26-159">b.</span><span class="sxs-lookup"><span data-stu-id="a5f26-159">b.</span></span> <span data-ttu-id="a5f26-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :</span><span class="sxs-lookup"><span data-stu-id="a5f26-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.cybozu.com`|
    | `https://<companyname>.kintone.com`|

    > [!NOTE] 
    > <span data-ttu-id="a5f26-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="a5f26-161">These values are not real.</span></span> <span data-ttu-id="a5f26-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="a5f26-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a5f26-163">Contact [équipe de support Client de Kintone](https://www.kintone.com/contact/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="a5f26-163">Contact [Kintone Client support team](https://www.kintone.com/contact/) tooget these values.</span></span> 
 
4. <span data-ttu-id="a5f26-164">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="a5f26-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_certificate.png) 

5. <span data-ttu-id="a5f26-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="a5f26-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kintone-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a5f26-168">Sur hello **Kintone Configuration** , cliquez sur **configurer de Kintone** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="a5f26-168">On hello **Kintone Configuration** section, click **Configure Kintone** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a5f26-169">Hello de copie **URL de déconnexion et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="a5f26-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_configure.png) 

7. <span data-ttu-id="a5f26-171">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise **Kintone** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="a5f26-171">In a different web browser window, log into your **Kintone** company site as an administrator.</span></span>

8. <span data-ttu-id="a5f26-172">Cliquez sur **Settings**.</span><span class="sxs-lookup"><span data-stu-id="a5f26-172">Click **Settings**.</span></span>
   
    <span data-ttu-id="a5f26-173">![Paramètres](./media/active-directory-saas-kintone-tutorial/ic785879.png "Paramètres")</span><span class="sxs-lookup"><span data-stu-id="a5f26-173">![Settings](./media/active-directory-saas-kintone-tutorial/ic785879.png "Settings")</span></span>

9. <span data-ttu-id="a5f26-174">Cliquez sur **Users & System Administration**.</span><span class="sxs-lookup"><span data-stu-id="a5f26-174">Click **Users & System Administration**.</span></span>
   
    <span data-ttu-id="a5f26-175">![Administration système et utilisateurs](./media/active-directory-saas-kintone-tutorial/ic785880.png "Administration système et utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="a5f26-175">![Users & System Administration](./media/active-directory-saas-kintone-tutorial/ic785880.png "Users & System Administration")</span></span>

10. <span data-ttu-id="a5f26-176">Sous **System Administration \> Security**, cliquez sur **Login**.</span><span class="sxs-lookup"><span data-stu-id="a5f26-176">Under **System Administration \> Security** click **Login**.</span></span>
   
    <span data-ttu-id="a5f26-177">![Connexion](./media/active-directory-saas-kintone-tutorial/ic785881.png "Connexion")</span><span class="sxs-lookup"><span data-stu-id="a5f26-177">![Login](./media/active-directory-saas-kintone-tutorial/ic785881.png "Login")</span></span>

11. <span data-ttu-id="a5f26-178">Cliquez sur **Enable SAML authentication**.</span><span class="sxs-lookup"><span data-stu-id="a5f26-178">Click **Enable SAML authentication**.</span></span>
   
    <span data-ttu-id="a5f26-179">![Authentification SAML](./media/active-directory-saas-kintone-tutorial/ic785882.png "Authentification SAML")</span><span class="sxs-lookup"><span data-stu-id="a5f26-179">![SAML Authentication](./media/active-directory-saas-kintone-tutorial/ic785882.png "SAML Authentication")</span></span>

12. <span data-ttu-id="a5f26-180">Dans la section authentification SAML de hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="a5f26-180">In hello SAML Authentication section, perform hello following steps:</span></span>
    
    <span data-ttu-id="a5f26-181">![Authentification SAML](./media/active-directory-saas-kintone-tutorial/ic785883.png "Authentification SAML")</span><span class="sxs-lookup"><span data-stu-id="a5f26-181">![SAML Authentication](./media/active-directory-saas-kintone-tutorial/ic785883.png "SAML Authentication")</span></span>
    
    <span data-ttu-id="a5f26-182">a.</span><span class="sxs-lookup"><span data-stu-id="a5f26-182">a.</span></span> <span data-ttu-id="a5f26-183">Bonjour **URL de connexion** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a5f26-183">In hello **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="a5f26-184">b.</span><span class="sxs-lookup"><span data-stu-id="a5f26-184">b.</span></span> <span data-ttu-id="a5f26-185">Bonjour **URL de déconnexion** zone de texte, valeur hello coller **URL de déconnexion** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a5f26-185">In hello **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="a5f26-186">c.</span><span class="sxs-lookup"><span data-stu-id="a5f26-186">c.</span></span> <span data-ttu-id="a5f26-187">Cliquez sur **Parcourir** tooupload votre certificat téléchargé.</span><span class="sxs-lookup"><span data-stu-id="a5f26-187">Click **Browse** tooupload your downloaded certificate.</span></span>
    
    <span data-ttu-id="a5f26-188">d.</span><span class="sxs-lookup"><span data-stu-id="a5f26-188">d.</span></span> <span data-ttu-id="a5f26-189">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="a5f26-189">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="a5f26-190">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="a5f26-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a5f26-191">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="a5f26-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a5f26-192">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a5f26-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a5f26-193">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5f26-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="a5f26-194">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="a5f26-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="a5f26-196">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a5f26-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a5f26-197">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="a5f26-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a5f26-199">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="a5f26-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a5f26-201">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="a5f26-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a5f26-203">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="a5f26-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a5f26-205">a.</span><span class="sxs-lookup"><span data-stu-id="a5f26-205">a.</span></span> <span data-ttu-id="a5f26-206">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a5f26-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a5f26-207">b.</span><span class="sxs-lookup"><span data-stu-id="a5f26-207">b.</span></span> <span data-ttu-id="a5f26-208">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a5f26-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a5f26-209">c.</span><span class="sxs-lookup"><span data-stu-id="a5f26-209">c.</span></span> <span data-ttu-id="a5f26-210">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="a5f26-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a5f26-211">d.</span><span class="sxs-lookup"><span data-stu-id="a5f26-211">d.</span></span> <span data-ttu-id="a5f26-212">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="a5f26-212">Click **Create**.</span></span>
 
### <a name="creating-a-kintone-test-user"></a><span data-ttu-id="a5f26-213">Création d’un utilisateur de test Kintone</span><span class="sxs-lookup"><span data-stu-id="a5f26-213">Creating a Kintone test user</span></span>

<span data-ttu-id="a5f26-214">tooenable Azure AD les utilisateurs toolog dans tooKintone, vous devez les configurer dans Kintone.</span><span class="sxs-lookup"><span data-stu-id="a5f26-214">tooenable Azure AD users toolog in tooKintone, they must be provisioned into Kintone.</span></span>  
<span data-ttu-id="a5f26-215">Dans les cas de hello d’occurrence, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="a5f26-215">In hello case of Kintone, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="a5f26-216">tooprovision un compte d’utilisateur, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="a5f26-216">tooprovision a user account, perform hello following steps:</span></span>

1. <span data-ttu-id="a5f26-217">Connectez-vous à tooyour **Kintone** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="a5f26-217">Log in tooyour **Kintone** company site as an administrator.</span></span>

2. <span data-ttu-id="a5f26-218">Cliquez sur **Setting**.</span><span class="sxs-lookup"><span data-stu-id="a5f26-218">Click **Setting**.</span></span>
   
    <span data-ttu-id="a5f26-219">![Paramètres](./media/active-directory-saas-kintone-tutorial/ic785879.png "Paramètres")</span><span class="sxs-lookup"><span data-stu-id="a5f26-219">![Settings](./media/active-directory-saas-kintone-tutorial/ic785879.png "Settings")</span></span>

3. <span data-ttu-id="a5f26-220">Cliquez sur **Users & System Administration**.</span><span class="sxs-lookup"><span data-stu-id="a5f26-220">Click **Users & System Administration**.</span></span>
   
    <span data-ttu-id="a5f26-221">![Administration système et utilisateur](./media/active-directory-saas-kintone-tutorial/ic785880.png "Administration système et utilisateur")</span><span class="sxs-lookup"><span data-stu-id="a5f26-221">![User & System Administration](./media/active-directory-saas-kintone-tutorial/ic785880.png "User & System Administration")</span></span>

4. <span data-ttu-id="a5f26-222">Sous **User Administration**, cliquez sur **Departments & Users**.</span><span class="sxs-lookup"><span data-stu-id="a5f26-222">Under **User Administration**, click **Departments & Users**.</span></span>
   
    <span data-ttu-id="a5f26-223">![Département et utilisateurs](./media/active-directory-saas-kintone-tutorial/ic785888.png "Département et utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="a5f26-223">![Department & Users](./media/active-directory-saas-kintone-tutorial/ic785888.png "Department & Users")</span></span>

5. <span data-ttu-id="a5f26-224">Cliquez sur **New User**.</span><span class="sxs-lookup"><span data-stu-id="a5f26-224">Click **New User**.</span></span>
   
    <span data-ttu-id="a5f26-225">![Nouveaux utilisateurs](./media/active-directory-saas-kintone-tutorial/ic785889.png "Nouveaux utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="a5f26-225">![New Users](./media/active-directory-saas-kintone-tutorial/ic785889.png "New Users")</span></span>

6. <span data-ttu-id="a5f26-226">Bonjour **nouvel utilisateur** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="a5f26-226">In hello **New User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="a5f26-227">![Nouveaux utilisateurs](./media/active-directory-saas-kintone-tutorial/ic785890.png "Nouveaux utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="a5f26-227">![New Users](./media/active-directory-saas-kintone-tutorial/ic785890.png "New Users")</span></span>
   
    <span data-ttu-id="a5f26-228">a.</span><span class="sxs-lookup"><span data-stu-id="a5f26-228">a.</span></span> <span data-ttu-id="a5f26-229">Tapez un **nom d’affichage**, **nom de connexion**, **nouveau mot de passe**, **confirmer le mot de passe**, **adresse de messagerie**, et autres détails d’un compte AAD valide que vous voulez tooprovision dans hello les zones de texte.</span><span class="sxs-lookup"><span data-stu-id="a5f26-229">Type a **Display Name**, **Login Name**, **New Password**, **Confirm Password**, **E-mail Address**, and other details of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
 
    <span data-ttu-id="a5f26-230">b.</span><span class="sxs-lookup"><span data-stu-id="a5f26-230">b.</span></span> <span data-ttu-id="a5f26-231">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="a5f26-231">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="a5f26-232">Vous pouvez utiliser n’importe quel autre occurrence utilisateur compte outil de création ou API fournie par Kintone tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="a5f26-232">You can use any other Kintone user account creation tools or APIs provided by Kintone tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a5f26-233">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5f26-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a5f26-234">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooKintone.</span><span class="sxs-lookup"><span data-stu-id="a5f26-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKintone.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="a5f26-236">**tooassign Britta Simon tooKintone, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a5f26-236">**tooassign Britta Simon tooKintone, perform hello following steps:**</span></span>

1. <span data-ttu-id="a5f26-237">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a5f26-237">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="a5f26-239">Dans la liste des applications hello, sélectionnez **Kintone**.</span><span class="sxs-lookup"><span data-stu-id="a5f26-239">In hello applications list, select **Kintone**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_app.png) 

3. <span data-ttu-id="a5f26-241">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a5f26-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="a5f26-243">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="a5f26-243">Click **Add** button.</span></span> <span data-ttu-id="a5f26-244">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a5f26-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="a5f26-246">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="a5f26-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a5f26-247">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a5f26-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a5f26-248">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a5f26-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a5f26-249">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="a5f26-249">Testing single sign-on</span></span>

<span data-ttu-id="a5f26-250">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="a5f26-250">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a5f26-251">Lorsque vous cliquez sur mosaïque Kintone hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Kintone application.</span><span class="sxs-lookup"><span data-stu-id="a5f26-251">When you click hello Kintone tile in hello Access Panel, you should get automatically signed-on tooyour Kintone application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a5f26-252">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="a5f26-252">Additional resources</span></span>

* [<span data-ttu-id="a5f26-253">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a5f26-253">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a5f26-254">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="a5f26-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_203.png

