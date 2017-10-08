---
title: "Tutoriel : intégration d’Azure Active Directory à LCVista | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et LCVista."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8db80d6e-3275-419f-aa39-6115a7bc9800
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: 5a4c7eb7d54b8b68c8241a97b9e516a3f6e55c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lcvista"></a><span data-ttu-id="42175-103">Tutoriel : Intégration d’Azure Active Directory à LCVista</span><span class="sxs-lookup"><span data-stu-id="42175-103">Tutorial: Azure Active Directory integration with LCVista</span></span>

<span data-ttu-id="42175-104">Dans ce didacticiel, vous apprendrez comment toointegrate LCVista avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="42175-104">In this tutorial, you learn how toointegrate LCVista with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="42175-105">Intégration LCVista à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="42175-105">Integrating LCVista with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="42175-106">Vous pouvez contrôler dans Azure AD qui a accès tooLCVista</span><span class="sxs-lookup"><span data-stu-id="42175-106">You can control in Azure AD who has access tooLCVista</span></span>
- <span data-ttu-id="42175-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooLCVista (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="42175-107">You can enable your users tooautomatically get signed-on tooLCVista (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="42175-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="42175-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="42175-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="42175-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42175-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="42175-110">Prerequisites</span></span>

<span data-ttu-id="42175-111">tooconfigure intégration d’Azure AD avec LCVista, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="42175-111">tooconfigure Azure AD integration with LCVista, you need hello following items:</span></span>

- <span data-ttu-id="42175-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="42175-112">An Azure AD subscription</span></span>
- <span data-ttu-id="42175-113">Un abonnement LCVista pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="42175-113">A LCVista single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="42175-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="42175-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="42175-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="42175-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="42175-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="42175-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="42175-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="42175-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="42175-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="42175-118">Scenario description</span></span>
<span data-ttu-id="42175-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="42175-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="42175-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="42175-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="42175-121">Ajout de LCVista à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="42175-121">Adding LCVista from hello gallery</span></span>
2. <span data-ttu-id="42175-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="42175-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lcvista-from-hello-gallery"></a><span data-ttu-id="42175-123">Ajout de LCVista à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="42175-123">Adding LCVista from hello gallery</span></span>
<span data-ttu-id="42175-124">intégration de hello tooconfigure de LCVista dans Azure AD, vous devez tooadd LCVista à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="42175-124">tooconfigure hello integration of LCVista into Azure AD, you need tooadd LCVista from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="42175-125">**tooadd LCVista à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="42175-125">**tooadd LCVista from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="42175-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="42175-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="42175-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="42175-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="42175-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="42175-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="42175-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="42175-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="42175-133">Dans la zone de recherche de hello, tapez **LCVista**.</span><span class="sxs-lookup"><span data-stu-id="42175-133">In hello search box, type **LCVista**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_search.png)

5. <span data-ttu-id="42175-135">Dans le volet de résultats hello, sélectionnez **LCVista**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="42175-135">In hello results panel, select **LCVista**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="42175-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="42175-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="42175-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec LCVista, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="42175-138">In this section, you configure and test Azure AD single sign-on with LCVista based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="42175-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans LCVista est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42175-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LCVista is tooa user in Azure AD.</span></span> <span data-ttu-id="42175-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans LCVista doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="42175-140">In other words, a link relationship between an Azure AD user and hello related user in LCVista needs toobe established.</span></span>

<span data-ttu-id="42175-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans LCVista.</span><span class="sxs-lookup"><span data-stu-id="42175-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LCVista.</span></span>

<span data-ttu-id="42175-142">tooconfigure et test Azure AD l’authentification unique avec LCVista, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="42175-142">tooconfigure and test Azure AD single sign-on with LCVista, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="42175-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="42175-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="42175-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="42175-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="42175-145">**[Création d’un utilisateur de test LCVista](#creating-a-lcvista-test-user)**  -toohave un équivalent de Britta Simon dans LCVista est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="42175-145">**[Creating a LCVista test user](#creating-a-lcvista-test-user)** - toohave a counterpart of Britta Simon in LCVista that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="42175-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="42175-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="42175-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="42175-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="42175-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="42175-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="42175-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application LCVista.</span><span class="sxs-lookup"><span data-stu-id="42175-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LCVista application.</span></span>

<span data-ttu-id="42175-150">**tooconfigure Azure AD single sign-on avec LCVista, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="42175-150">**tooconfigure Azure AD single sign-on with LCVista, perform hello following steps:**</span></span>

1. <span data-ttu-id="42175-151">Bonjour portail Azure, sur hello **LCVista** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="42175-151">In hello Azure portal, on hello **LCVista** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="42175-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="42175-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_samlbase.png)

3. <span data-ttu-id="42175-155">Sur hello **LCVista domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="42175-155">On hello **LCVista Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_url.png)

    <span data-ttu-id="42175-157">a.</span><span class="sxs-lookup"><span data-stu-id="42175-157">a.</span></span> <span data-ttu-id="42175-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.lcvista.com/rainier/login`</span><span class="sxs-lookup"><span data-stu-id="42175-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.lcvista.com/rainier/login`</span></span>

    <span data-ttu-id="42175-159">b.</span><span class="sxs-lookup"><span data-stu-id="42175-159">b.</span></span> <span data-ttu-id="42175-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.lcvista.com`</span><span class="sxs-lookup"><span data-stu-id="42175-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.lcvista.com`</span></span> 
     
    > [!NOTE] 
    > <span data-ttu-id="42175-161">Ces valeurs ne sont pas hello réel.</span><span class="sxs-lookup"><span data-stu-id="42175-161">These values are not hello real.</span></span> <span data-ttu-id="42175-162">Mettre à jour les valeurs de hello réel identificateur et l’URL de connexion.</span><span class="sxs-lookup"><span data-stu-id="42175-162">Update these values with hello actual Identifier and Sign-On URL.</span></span> <span data-ttu-id="42175-163">Contact [équipe de support Client de LCVista](https://lcvista.com/contact) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="42175-163">Contact [LCVista Client support team](https://lcvista.com/contact) tooget these values.</span></span> 

4. <span data-ttu-id="42175-164">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="42175-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_certificate.png) 

5. <span data-ttu-id="42175-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="42175-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lcvista-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="42175-168">Sur hello **LCVista Configuration** , cliquez sur **LCVista de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="42175-168">On hello **LCVista Configuration** section, click **Configure LCVista** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="42175-169">Hello de copie **ID d’entité SAML** et **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="42175-169">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_configure.png) 

7.  <span data-ttu-id="42175-171">Ouverture de session tooyour application LCVista en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="42175-171">Sign on tooyour LCVista application as an administrator.</span></span>

8. <span data-ttu-id="42175-172">Bonjour **SAML Config** section, vérifiez hello **connexion SAML d’activer** et entrez les détails de hello comme indiqué dans sous l’image.</span><span class="sxs-lookup"><span data-stu-id="42175-172">In hello **SAML Config** section, check hello **Enable SAML login** and enter hello details as mentioned in below image.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_config.png)

    <span data-ttu-id="42175-174">a.</span><span class="sxs-lookup"><span data-stu-id="42175-174">a.</span></span> <span data-ttu-id="42175-175">Hello de coller **URL de l’émetteur** dont vous avez copié à partir d’Azure AD dans hello **ID d’entité** section.</span><span class="sxs-lookup"><span data-stu-id="42175-175">Paste hello **Issuer URL** which you have copied from Azure AD in hello **Entity ID** section.</span></span> 

    <span data-ttu-id="42175-176">b.</span><span class="sxs-lookup"><span data-stu-id="42175-176">b.</span></span> <span data-ttu-id="42175-177">Hello de coller **-Service URL d’authentification** dont vous avez copié à partir d’Azure AD dans hello **URL** section.</span><span class="sxs-lookup"><span data-stu-id="42175-177">Paste hello **Single Sign-On Service URL** which you have copied from Azure AD in hello **URL** section.</span></span>

    <span data-ttu-id="42175-178">c.</span><span class="sxs-lookup"><span data-stu-id="42175-178">c.</span></span> <span data-ttu-id="42175-179">À partir de métadonnées (XML) qui vous avez téléchargé à partir du portail Azure, copiez la valeur de la hello **X509Certificate** et collez-le dans hello **x509 certificat** section.</span><span class="sxs-lookup"><span data-stu-id="42175-179">From Metadata (XML) which you have downloaded from Azure portal, copy hello value **X509Certificate** and paste it in hello **x509 Certificate** section.</span></span>

    <span data-ttu-id="42175-180">d.</span><span class="sxs-lookup"><span data-stu-id="42175-180">d.</span></span> <span data-ttu-id="42175-181">Bonjour **prénom attribut** zone de texte, valeur hello `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="42175-181">In hello **First name attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>

    <span data-ttu-id="42175-182">e.</span><span class="sxs-lookup"><span data-stu-id="42175-182">e.</span></span> <span data-ttu-id="42175-183">Bonjour **attribut de nom** zone de texte, valeur hello `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="42175-183">In hello **Last name attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>

    <span data-ttu-id="42175-184">f.</span><span class="sxs-lookup"><span data-stu-id="42175-184">f.</span></span> <span data-ttu-id="42175-185">Bonjour **attribut Email** zone de texte, valeur hello `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="42175-185">In hello **Email attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="42175-186">g.</span><span class="sxs-lookup"><span data-stu-id="42175-186">g.</span></span> <span data-ttu-id="42175-187">Bonjour **attribut Username** zone de texte, valeur hello `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="42175-187">In hello **Username attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>

    <span data-ttu-id="42175-188">e.</span><span class="sxs-lookup"><span data-stu-id="42175-188">e.</span></span> <span data-ttu-id="42175-189">Cliquez sur **enregistrer** toosave les paramètres hello.</span><span class="sxs-lookup"><span data-stu-id="42175-189">Click **Save** toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="42175-190">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="42175-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="42175-191">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="42175-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="42175-192">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="42175-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="42175-193">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="42175-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="42175-194">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="42175-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="42175-196">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="42175-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="42175-197">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="42175-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="42175-199">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="42175-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="42175-201">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="42175-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="42175-203">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="42175-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="42175-205">a.</span><span class="sxs-lookup"><span data-stu-id="42175-205">a.</span></span> <span data-ttu-id="42175-206">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="42175-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="42175-207">b.</span><span class="sxs-lookup"><span data-stu-id="42175-207">b.</span></span> <span data-ttu-id="42175-208">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="42175-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="42175-209">c.</span><span class="sxs-lookup"><span data-stu-id="42175-209">c.</span></span> <span data-ttu-id="42175-210">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="42175-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="42175-211">d.</span><span class="sxs-lookup"><span data-stu-id="42175-211">d.</span></span> <span data-ttu-id="42175-212">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="42175-212">Click **Create**.</span></span>
 
### <a name="creating-a-lcvista-test-user"></a><span data-ttu-id="42175-213">Création d’un utilisateur de test LCVista</span><span class="sxs-lookup"><span data-stu-id="42175-213">Creating a LCVista test user</span></span>

<span data-ttu-id="42175-214">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans LCVista.</span><span class="sxs-lookup"><span data-stu-id="42175-214">In this section, you create a user called Britta Simon in LCVista.</span></span> <span data-ttu-id="42175-215">Vous devez toocontact [équipe de support Client de LCVista](https://lcvista.com/contact) utilisateurs hello tooadd hello LCVista application.</span><span class="sxs-lookup"><span data-stu-id="42175-215">You need toocontact [LCVista Client support team](https://lcvista.com/contact) tooadd hello users in hello LCVista application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="42175-216">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="42175-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="42175-217">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooLCVista.</span><span class="sxs-lookup"><span data-stu-id="42175-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLCVista.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="42175-219">**tooassign Britta Simon tooLCVista, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="42175-219">**tooassign Britta Simon tooLCVista, perform hello following steps:**</span></span>

1. <span data-ttu-id="42175-220">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="42175-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="42175-222">Dans la liste des applications hello, sélectionnez **LCVista**.</span><span class="sxs-lookup"><span data-stu-id="42175-222">In hello applications list, select **LCVista**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_app.png) 

3. <span data-ttu-id="42175-224">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="42175-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="42175-226">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="42175-226">Click **Add** button.</span></span> <span data-ttu-id="42175-227">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="42175-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="42175-229">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="42175-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="42175-230">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="42175-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="42175-231">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="42175-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="42175-232">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="42175-232">Testing single sign-on</span></span>

<span data-ttu-id="42175-233">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="42175-233">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span> <span data-ttu-id="42175-234">Cliquez sur la vignette de LCVista hello Bonjour volet d’accès, vous serez redirigé tooOrganization page d’authentification.</span><span class="sxs-lookup"><span data-stu-id="42175-234">Click hello LCVista tile in hello Access Panel, you will be redirected tooOrganization sign on page.</span></span> <span data-ttu-id="42175-235">Connexion réussie, vous serez connecté tooyour LCVista application.</span><span class="sxs-lookup"><span data-stu-id="42175-235">After successful login, you will be signed-on tooyour LCVista application.</span></span> <span data-ttu-id="42175-236">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="42175-236">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="42175-237">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="42175-237">Additional resources</span></span>

* [<span data-ttu-id="42175-238">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="42175-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="42175-239">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="42175-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_203.png

