---
title: "Didacticiel : intégration d’Azure Active Directory à Freshservice | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Freshservice."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3dd22b1f-445d-45c6-8eda-30207eb9a1a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: d73624b87d058f66885ae72fda69a0aacc89c1ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshservice"></a><span data-ttu-id="a940f-103">Didacticiel : intégration d’Azure Active Directory à Freshservice</span><span class="sxs-lookup"><span data-stu-id="a940f-103">Tutorial: Azure Active Directory integration with Freshservice</span></span>

<span data-ttu-id="a940f-104">Dans ce didacticiel, vous apprendrez comment toointegrate Freshservice avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a940f-104">In this tutorial, you learn how toointegrate Freshservice with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a940f-105">Intégration de Freshservice à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="a940f-105">Integrating Freshservice with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a940f-106">Vous pouvez contrôler dans Azure AD qui a accès tooFreshservice</span><span class="sxs-lookup"><span data-stu-id="a940f-106">You can control in Azure AD who has access tooFreshservice</span></span>
- <span data-ttu-id="a940f-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooFreshservice (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="a940f-107">You can enable your users tooautomatically get signed-on tooFreshservice (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a940f-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="a940f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a940f-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a940f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a940f-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a940f-110">Prerequisites</span></span>

<span data-ttu-id="a940f-111">tooconfigure intégration d’Azure AD à Freshservice, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a940f-111">tooconfigure Azure AD integration with Freshservice, you need hello following items:</span></span>

- <span data-ttu-id="a940f-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="a940f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a940f-113">Un abonnement Freshservice pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="a940f-113">A Freshservice single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a940f-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="a940f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a940f-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="a940f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a940f-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="a940f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a940f-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a940f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a940f-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="a940f-118">Scenario description</span></span>
<span data-ttu-id="a940f-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="a940f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a940f-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="a940f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a940f-121">Ajout de Freshservice à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="a940f-121">Adding Freshservice from hello gallery</span></span>
2. <span data-ttu-id="a940f-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a940f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshservice-from-hello-gallery"></a><span data-ttu-id="a940f-123">Ajout de Freshservice à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="a940f-123">Adding Freshservice from hello gallery</span></span>
<span data-ttu-id="a940f-124">intégration de hello tooconfigure de Freshservice dans Azure AD, vous devez tooadd Freshservice à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="a940f-124">tooconfigure hello integration of Freshservice into Azure AD, you need tooadd Freshservice from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a940f-125">**tooadd Freshservice à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a940f-125">**tooadd Freshservice from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a940f-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="a940f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a940f-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="a940f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a940f-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a940f-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="a940f-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a940f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="a940f-133">Dans la zone de recherche de hello, tapez **Freshservice**.</span><span class="sxs-lookup"><span data-stu-id="a940f-133">In hello search box, type **Freshservice**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_search.png)

5. <span data-ttu-id="a940f-135">Dans le volet de résultats hello, sélectionnez **Freshservice**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="a940f-135">In hello results panel, select **Freshservice**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a940f-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a940f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a940f-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Freshservice, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="a940f-138">In this section, you configure and test Azure AD single sign-on with Freshservice based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a940f-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Freshservice est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a940f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Freshservice is tooa user in Azure AD.</span></span> <span data-ttu-id="a940f-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Freshservice doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="a940f-140">In other words, a link relationship between an Azure AD user and hello related user in Freshservice needs toobe established.</span></span>

<span data-ttu-id="a940f-141">En l’occurrence, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="a940f-141">In Freshservice, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a940f-142">tooconfigure et test Azure AD l’authentification unique à Freshservice, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="a940f-142">tooconfigure and test Azure AD single sign-on with Freshservice, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a940f-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="a940f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a940f-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a940f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a940f-145">**[Création d’un utilisateur de test de Freshservice](#creating-a-freshservice-test-user)**  -toohave un équivalent de Britta Simon dans Freshservice est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a940f-145">**[Creating a Freshservice test user](#creating-a-freshservice-test-user)** - toohave a counterpart of Britta Simon in Freshservice that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a940f-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="a940f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a940f-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="a940f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a940f-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a940f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a940f-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Freshservice.</span><span class="sxs-lookup"><span data-stu-id="a940f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Freshservice application.</span></span>

<span data-ttu-id="a940f-150">**tooconfigure Azure AD single sign-on avec Freshservice, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a940f-150">**tooconfigure Azure AD single sign-on with Freshservice, perform hello following steps:**</span></span>

1. <span data-ttu-id="a940f-151">Bonjour portail Azure, sur hello **Freshservice** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="a940f-151">In hello Azure portal, on hello **Freshservice** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="a940f-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="a940f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_samlbase.png)

3. <span data-ttu-id="a940f-155">Sur hello **Freshservice domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="a940f-155">On hello **Freshservice Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_url.png)

    <span data-ttu-id="a940f-157">a.</span><span class="sxs-lookup"><span data-stu-id="a940f-157">a.</span></span> <span data-ttu-id="a940f-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<democompany>.freshservice.com`</span><span class="sxs-lookup"><span data-stu-id="a940f-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<democompany>.freshservice.com`</span></span>

    <span data-ttu-id="a940f-159">b.</span><span class="sxs-lookup"><span data-stu-id="a940f-159">b.</span></span> <span data-ttu-id="a940f-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<democompany>.freshservice.com`</span><span class="sxs-lookup"><span data-stu-id="a940f-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<democompany>.freshservice.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a940f-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="a940f-161">These values are not real.</span></span> <span data-ttu-id="a940f-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="a940f-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a940f-163">Contact [équipe de support Client de Freshservice](https://support.freshservice.com/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="a940f-163">Contact [Freshservice Client support team](https://support.freshservice.com/) tooget these values.</span></span> 
 
4. <span data-ttu-id="a940f-164">Sur hello **le certificat de signature SAML** section, copiez **l’empreinte numérique** valeur du certificat.</span><span class="sxs-lookup"><span data-stu-id="a940f-164">On hello **SAML Signing Certificate** section, copy **THUMBPRINT** value of certificate.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_certificate.png) 

5. <span data-ttu-id="a940f-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="a940f-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-freshservice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a940f-168">Sur hello **Freshservice Configuration** , cliquez sur **configurer de Freshservice** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="a940f-168">On hello **Freshservice Configuration** section, click **Configure Freshservice** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a940f-169">Hello de copie **URL de déconnexion et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="a940f-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_configure.png) 

7. <span data-ttu-id="a940f-171">Dans une fenêtre de navigateur web, ouvrez une session dans le site d’entreprise Freshservice tooyour en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="a940f-171">In a different web browser window, log in tooyour Freshservice company site as an administrator.</span></span>

8. <span data-ttu-id="a940f-172">Dans le menu hello haut de hello, cliquez sur **Admin**.</span><span class="sxs-lookup"><span data-stu-id="a940f-172">In hello menu on hello top, click **Admin**.</span></span>
   
    <span data-ttu-id="a940f-173">![Administrateur](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Administrateur")</span><span class="sxs-lookup"><span data-stu-id="a940f-173">![Admin](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span></span>

9. <span data-ttu-id="a940f-174">Bonjour **portail client**, cliquez sur **sécurité**.</span><span class="sxs-lookup"><span data-stu-id="a940f-174">In hello **Customer Portal**, click **Security**.</span></span>
   
    <span data-ttu-id="a940f-175">![Sécurité](./media/active-directory-saas-freshservice-tutorial/ic790815.png "Sécurité")</span><span class="sxs-lookup"><span data-stu-id="a940f-175">![Security](./media/active-directory-saas-freshservice-tutorial/ic790815.png "Security")</span></span>

10. <span data-ttu-id="a940f-176">Bonjour **sécurité** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="a940f-176">In hello **Security** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="a940f-177">![Single Sign On](./media/active-directory-saas-freshservice-tutorial/ic790816.png "Single Sign On")</span><span class="sxs-lookup"><span data-stu-id="a940f-177">![Single Sign On](./media/active-directory-saas-freshservice-tutorial/ic790816.png "Single Sign On")</span></span>
   
    <span data-ttu-id="a940f-178">a.</span><span class="sxs-lookup"><span data-stu-id="a940f-178">a.</span></span> <span data-ttu-id="a940f-179">Activez **Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="a940f-179">Switch **Single Sign On**.</span></span>

    <span data-ttu-id="a940f-180">b.</span><span class="sxs-lookup"><span data-stu-id="a940f-180">b.</span></span> <span data-ttu-id="a940f-181">Sélectionnez **SAML SSO**.</span><span class="sxs-lookup"><span data-stu-id="a940f-181">Select **SAML SSO**.</span></span>

    <span data-ttu-id="a940f-182">c.</span><span class="sxs-lookup"><span data-stu-id="a940f-182">c.</span></span> <span data-ttu-id="a940f-183">Bonjour **URL de connexion SAML** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a940f-183">In hello **SAML Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a940f-184">d.</span><span class="sxs-lookup"><span data-stu-id="a940f-184">d.</span></span> <span data-ttu-id="a940f-185">Bonjour **URL de déconnexion** zone de texte, valeur hello coller **URL de déconnexion** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a940f-185">In hello **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a940f-186">e.</span><span class="sxs-lookup"><span data-stu-id="a940f-186">e.</span></span> <span data-ttu-id="a940f-187">Dans **Security Certificate Fingerprint** zone de texte, collez hello **l’empreinte numérique** valeur de certificat que vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a940f-187">In **Security Certificate Fingerprint** textbox, paste hello **THUMBPRINT** value of certificate which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a940f-188">f.</span><span class="sxs-lookup"><span data-stu-id="a940f-188">f.</span></span> <span data-ttu-id="a940f-189">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="a940f-189">Click **Save**</span></span>
   
> [!TIP]
> <span data-ttu-id="a940f-190">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="a940f-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a940f-191">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="a940f-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a940f-192">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a940f-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a940f-193">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="a940f-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="a940f-194">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="a940f-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="a940f-196">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a940f-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a940f-197">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="a940f-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a940f-199">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="a940f-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a940f-201">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="a940f-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a940f-203">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="a940f-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a940f-205">a.</span><span class="sxs-lookup"><span data-stu-id="a940f-205">a.</span></span> <span data-ttu-id="a940f-206">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a940f-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a940f-207">b.</span><span class="sxs-lookup"><span data-stu-id="a940f-207">b.</span></span> <span data-ttu-id="a940f-208">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a940f-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a940f-209">c.</span><span class="sxs-lookup"><span data-stu-id="a940f-209">c.</span></span> <span data-ttu-id="a940f-210">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="a940f-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a940f-211">d.</span><span class="sxs-lookup"><span data-stu-id="a940f-211">d.</span></span> <span data-ttu-id="a940f-212">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="a940f-212">Click **Create**.</span></span>
 
### <a name="creating-a-freshservice-test-user"></a><span data-ttu-id="a940f-213">Création d’un utilisateur de test Freshservice</span><span class="sxs-lookup"><span data-stu-id="a940f-213">Creating a Freshservice test user</span></span>

<span data-ttu-id="a940f-214">tooenable Azure AD les utilisateurs toolog dans tooFreshService, vous devez les configurer dans FreshService.</span><span class="sxs-lookup"><span data-stu-id="a940f-214">tooenable Azure AD users toolog in tooFreshService, they must be provisioned into FreshService.</span></span> <span data-ttu-id="a940f-215">Dans les cas de hello d’occurrence, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="a940f-215">In hello case of FreshService, provisioning is a manual task.</span></span>

<span data-ttu-id="a940f-216">**tooprovision un compte d’utilisateur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a940f-216">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="a940f-217">Connectez-vous à tooyour **FreshService** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="a940f-217">Log in tooyour **FreshService** company site as an administrator.</span></span>

2. <span data-ttu-id="a940f-218">Dans le menu hello haut de hello, cliquez sur **Admin**.</span><span class="sxs-lookup"><span data-stu-id="a940f-218">In hello menu on hello top, click **Admin**.</span></span>
   
    <span data-ttu-id="a940f-219">![Administrateur](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Administrateur")</span><span class="sxs-lookup"><span data-stu-id="a940f-219">![Admin](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span></span>

3. <span data-ttu-id="a940f-220">Bonjour **gestion des utilisateurs** , cliquez sur **demandeurs**.</span><span class="sxs-lookup"><span data-stu-id="a940f-220">In hello **User Management** section, click **Requesters**.</span></span>
   
    <span data-ttu-id="a940f-221">![Requesters](./media/active-directory-saas-freshservice-tutorial/ic790818.png "Requesters")</span><span class="sxs-lookup"><span data-stu-id="a940f-221">![Requesters](./media/active-directory-saas-freshservice-tutorial/ic790818.png "Requesters")</span></span>

4. <span data-ttu-id="a940f-222">Cliquez sur **New Requester**.</span><span class="sxs-lookup"><span data-stu-id="a940f-222">Click **New Requester**.</span></span>
   
    <span data-ttu-id="a940f-223">![New Requesters](./media/active-directory-saas-freshservice-tutorial/ic790819.png "New Requesters")</span><span class="sxs-lookup"><span data-stu-id="a940f-223">![New Requesters](./media/active-directory-saas-freshservice-tutorial/ic790819.png "New Requesters")</span></span>

5. <span data-ttu-id="a940f-224">Bonjour **nouveau demandeur** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="a940f-224">In hello **New Requester** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="a940f-225">![New Requester](./media/active-directory-saas-freshservice-tutorial/ic790820.png "New Requester")</span><span class="sxs-lookup"><span data-stu-id="a940f-225">![New Requester](./media/active-directory-saas-freshservice-tutorial/ic790820.png "New Requester")</span></span>   

    <span data-ttu-id="a940f-226">a.</span><span class="sxs-lookup"><span data-stu-id="a940f-226">a.</span></span> <span data-ttu-id="a940f-227">Entrez hello **prénom** et **messagerie** les attributs d’un compte Azure Active Directory valide que vous voulez tooprovision dans hello relatives des zones de texte.</span><span class="sxs-lookup"><span data-stu-id="a940f-227">Enter hello **First Name** and **Email** attributes of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>

    <span data-ttu-id="a940f-228">b.</span><span class="sxs-lookup"><span data-stu-id="a940f-228">b.</span></span> <span data-ttu-id="a940f-229">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="a940f-229">Click **Save**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="a940f-230">titulaire du compte Azure Active Directory Hello Obtient un message électronique contenant un compte de hello tooconfirm lien avant son activation</span><span class="sxs-lookup"><span data-stu-id="a940f-230">hello Azure Active Directory account holder gets an email including a link tooconfirm hello account before it becomes active</span></span>
    >  

>[!NOTE]
><span data-ttu-id="a940f-231">Vous pouvez utiliser n’importe quel autre FreshService utilisateur compte outil de création ou API fournie par FreshService tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="a940f-231">You can use any other FreshService user account creation tools or APIs provided by FreshService tooprovision AAD user accounts.</span></span>
>  

![Affecter des utilisateurs][200] 

<span data-ttu-id="a940f-233">**tooassign Britta Simon tooFreshservice, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a940f-233">**tooassign Britta Simon tooFreshservice, perform hello following steps:**</span></span>

1. <span data-ttu-id="a940f-234">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a940f-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="a940f-236">Dans la liste des applications hello, sélectionnez **Freshservice**.</span><span class="sxs-lookup"><span data-stu-id="a940f-236">In hello applications list, select **Freshservice**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_app.png) 

3. <span data-ttu-id="a940f-238">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a940f-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="a940f-240">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="a940f-240">Click **Add** button.</span></span> <span data-ttu-id="a940f-241">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a940f-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="a940f-243">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="a940f-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a940f-244">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a940f-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a940f-245">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a940f-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a940f-246">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="a940f-246">Testing single sign-on</span></span>

<span data-ttu-id="a940f-247">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="a940f-247">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a940f-248">Lorsque vous cliquez sur mosaïque Freshservice hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Freshservice application.</span><span class="sxs-lookup"><span data-stu-id="a940f-248">When you click hello Freshservice tile in hello Access Panel, you should get automatically signed-on tooyour Freshservice application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a940f-249">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="a940f-249">Additional resources</span></span>

* [<span data-ttu-id="a940f-250">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a940f-250">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a940f-251">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="a940f-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_203.png

