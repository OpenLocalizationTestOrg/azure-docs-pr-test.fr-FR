---
title: "Didacticiel : Intégration d’Azure Active Directory à Marketo | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Marketo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b88c45f5-d288-4717-835c-ca965add8735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: e146fd5a8075bc9c7ba049b25e5f301fc2645ed9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-marketo"></a><span data-ttu-id="537d3-103">Didacticiel : Intégration d’Azure Active Directory à Marketo</span><span class="sxs-lookup"><span data-stu-id="537d3-103">Tutorial: Azure Active Directory integration with Marketo</span></span>

<span data-ttu-id="537d3-104">Dans ce didacticiel, vous allez apprendre à intégrer Marketo à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="537d3-104">In this tutorial, you learn how to integrate Marketo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="537d3-105">L’intégration de Marketo à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="537d3-105">Integrating Marketo with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="537d3-106">Dans Azure AD, vous pouvez contrôler qui a accès Marketo.</span><span class="sxs-lookup"><span data-stu-id="537d3-106">You can control in Azure AD who has access to Marketo</span></span>
- <span data-ttu-id="537d3-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Marketo (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="537d3-107">You can enable your users to automatically get signed-on to Marketo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="537d3-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="537d3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="537d3-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="537d3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="537d3-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="537d3-110">Prerequisites</span></span>

<span data-ttu-id="537d3-111">Pour configurer l’intégration d’Azure AD à Marketo, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="537d3-111">To configure Azure AD integration with Marketo, you need the following items:</span></span>

- <span data-ttu-id="537d3-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="537d3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="537d3-113">Un abonnement Marketo pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="537d3-113">A Marketo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="537d3-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="537d3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="537d3-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="537d3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="537d3-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="537d3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="537d3-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="537d3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="537d3-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="537d3-118">Scenario description</span></span>
<span data-ttu-id="537d3-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="537d3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="537d3-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="537d3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="537d3-121">Ajout de Marketo depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="537d3-121">Adding Marketo from the gallery</span></span>
2. <span data-ttu-id="537d3-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="537d3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-marketo-from-the-gallery"></a><span data-ttu-id="537d3-123">Ajout de Marketo depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="537d3-123">Adding Marketo from the gallery</span></span>
<span data-ttu-id="537d3-124">Pour configurer l’intégration de Marketo à Azure AD, vous devez ajouter Marketo, depuis la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="537d3-124">To configure the integration of Marketo into Azure AD, you need to add Marketo from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="537d3-125">**Pour ajouter Marketo depuis la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="537d3-125">**To add Marketo from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="537d3-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="537d3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="537d3-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="537d3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="537d3-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="537d3-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="537d3-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="537d3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="537d3-133">Dans la zone de recherche, tapez **Marketo**.</span><span class="sxs-lookup"><span data-stu-id="537d3-133">In the search box, type **Marketo**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_search.png)

5. <span data-ttu-id="537d3-135">Dans le panneau des résultats, sélectionnez **Marketo**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="537d3-135">In the results panel, select **Marketo**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="537d3-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="537d3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="537d3-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Marketo grâce à un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="537d3-138">In this section, you configure and test Azure AD single sign-on with Marketo based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="537d3-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Marketo équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="537d3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Marketo is to a user in Azure AD.</span></span> <span data-ttu-id="537d3-140">En d’autres termes, il faut établir une relation entre l’utilisateur Azure AD et l’utilisateur Marketo associé.</span><span class="sxs-lookup"><span data-stu-id="537d3-140">In other words, a link relationship between an Azure AD user and the related user in Marketo needs to be established.</span></span>

<span data-ttu-id="537d3-141">Dans Marketo, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **Nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="537d3-141">In Marketo, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="537d3-142">Pour configurer et tester l’authentification unique Azure AD avec Marketo, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="537d3-142">To configure and test Azure AD single sign-on with Marketo, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="537d3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="537d3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="537d3-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="537d3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="537d3-145">**[Création d’un utilisateur de test Marketo](#creating-a-marketo-test-user)** pour avoir un équivalent de Britta Simon dans Marketo qui est lié à la représentation d’un utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="537d3-145">**[Creating a Marketo test user](#creating-a-marketo-test-user)** - to have a counterpart of Britta Simon in Marketo that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="537d3-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="537d3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="537d3-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="537d3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="537d3-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="537d3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="537d3-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Marketo.</span><span class="sxs-lookup"><span data-stu-id="537d3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Marketo application.</span></span>

<span data-ttu-id="537d3-150">**Pour configurer l’authentification unique Azure AD avec Marketo, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="537d3-150">**To configure Azure AD single sign-on with Marketo, perform the following steps:**</span></span>

1. <span data-ttu-id="537d3-151">Dans le portail Azure, sur la page d’intégration de l’application **Marketo**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="537d3-151">In the Azure portal, on the **Marketo** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="537d3-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="537d3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_samlbase.png)

3. <span data-ttu-id="537d3-155">Dans la section **Marketo Domain and URLs** (Domaine et URL Marketo), réalisez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="537d3-155">On the **Marketo Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_url.png)

    <span data-ttu-id="537d3-157">a.</span><span class="sxs-lookup"><span data-stu-id="537d3-157">a.</span></span> <span data-ttu-id="537d3-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://saml.marketo.com/sp`</span><span class="sxs-lookup"><span data-stu-id="537d3-158">In the **Identifier** textbox, type a URL using the following pattern: `https://saml.marketo.com/sp`</span></span>

    <span data-ttu-id="537d3-159">b.</span><span class="sxs-lookup"><span data-stu-id="537d3-159">b.</span></span> <span data-ttu-id="537d3-160">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://login.marketo.com/saml/assertion/\<munchkinid\>`</span><span class="sxs-lookup"><span data-stu-id="537d3-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://login.marketo.com/saml/assertion/\<munchkinid\>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="537d3-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="537d3-161">These values are not real.</span></span> <span data-ttu-id="537d3-162">Mettez à jour ces valeurs avec l’identificateur et l’URL de réponse réels.</span><span class="sxs-lookup"><span data-stu-id="537d3-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="537d3-163">Pour obtenir ces valeurs, contactez [l’équipe de support Marketo](http://investors.marketo.com/contactus.cfm).</span><span class="sxs-lookup"><span data-stu-id="537d3-163">Contact [Marketo support team](http://investors.marketo.com/contactus.cfm) to get these values.</span></span>
 
4. <span data-ttu-id="537d3-164">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="537d3-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_certificate.png) 

5. <span data-ttu-id="537d3-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="537d3-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="537d3-168">Pour ouvrir la fenêtre **Configurer l’authentification**, dans la section **Configuration de Marketo**, cliquez sur **Configurer Marketo**.</span><span class="sxs-lookup"><span data-stu-id="537d3-168">On the **Marketo Configuration** section, click **Configure Marketo** to open **Configure sign-on** window.</span></span> <span data-ttu-id="537d3-169">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="537d3-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_configure.png) 

7. <span data-ttu-id="537d3-171">Pour obtenir l’ID Munchkin de votre application, connectez-vous à Marketo à l’aide des informations d’identification d’administrateur et procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="537d3-171">To get Munchkin Id of your application, log in to Marketo using admin credentials and perform following actions:</span></span>
   
    <span data-ttu-id="537d3-172">a.</span><span class="sxs-lookup"><span data-stu-id="537d3-172">a.</span></span> <span data-ttu-id="537d3-173">Connectez-vous à l’application Marketo à l’aide des informations d’identification de l’administrateur.</span><span class="sxs-lookup"><span data-stu-id="537d3-173">Log in to Marketo app using admin credentials.</span></span>
   
    <span data-ttu-id="537d3-174">b.</span><span class="sxs-lookup"><span data-stu-id="537d3-174">b.</span></span> <span data-ttu-id="537d3-175">Dans le volet de navigation supérieur, cliquez sur le bouton **Administrateur**.</span><span class="sxs-lookup"><span data-stu-id="537d3-175">Click the **Admin** button on the top navigation pane.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="537d3-177">c.</span><span class="sxs-lookup"><span data-stu-id="537d3-177">c.</span></span> <span data-ttu-id="537d3-178">Accédez au menu Intégration et cliquez sur le **lien Munchkin**.</span><span class="sxs-lookup"><span data-stu-id="537d3-178">Navigate to the Integration menu and click the **Munchkin link**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_11.png)
   
    <span data-ttu-id="537d3-180">d.</span><span class="sxs-lookup"><span data-stu-id="537d3-180">d.</span></span> <span data-ttu-id="537d3-181">Copiez l’ID Munchkin indiqué sur l’écran et complétez votre URL de réponse dans l’Assistant de configuration Azure AD.</span><span class="sxs-lookup"><span data-stu-id="537d3-181">Copy the Munchkin Id shown on the screen and complete your Reply URL in the Azure AD configuration wizard.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_12.png) 

8. <span data-ttu-id="537d3-183">Pour configurer l’authentification unique de l’application, suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="537d3-183">To configure the SSO in the application, follow the below steps:</span></span>
   
    <span data-ttu-id="537d3-184">a.</span><span class="sxs-lookup"><span data-stu-id="537d3-184">a.</span></span> <span data-ttu-id="537d3-185">Connectez-vous à l’application Marketo à l’aide des informations d’identification de l’administrateur.</span><span class="sxs-lookup"><span data-stu-id="537d3-185">Log in to Marketo app using admin credentials.</span></span>
   
    <span data-ttu-id="537d3-186">b.</span><span class="sxs-lookup"><span data-stu-id="537d3-186">b.</span></span> <span data-ttu-id="537d3-187">Dans le volet de navigation supérieur, cliquez sur le bouton **Administrateur**.</span><span class="sxs-lookup"><span data-stu-id="537d3-187">Click the **Admin** button on the top navigation pane.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="537d3-189">c.</span><span class="sxs-lookup"><span data-stu-id="537d3-189">c.</span></span> <span data-ttu-id="537d3-190">Accédez au menu Intégration et cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="537d3-190">Navigate to the Integration menu and click **Single Sign On**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_07.png) 
   
    <span data-ttu-id="537d3-192">d.</span><span class="sxs-lookup"><span data-stu-id="537d3-192">d.</span></span> <span data-ttu-id="537d3-193">Pour activer les paramètres SAML, cliquez sur le bouton **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="537d3-193">To enable the SAML Settings, click **Edit** button.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_08.png) 
   
    <span data-ttu-id="537d3-195">e.</span><span class="sxs-lookup"><span data-stu-id="537d3-195">e.</span></span> <span data-ttu-id="537d3-196">**Activez** les paramètres d’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="537d3-196">**Enabled** Single Sign-On settings.</span></span>
   
    <span data-ttu-id="537d3-197">f.</span><span class="sxs-lookup"><span data-stu-id="537d3-197">f.</span></span> <span data-ttu-id="537d3-198">Collez l’**ID d’entité SAML** dans la zone de texte **ID de l’émetteur**.</span><span class="sxs-lookup"><span data-stu-id="537d3-198">Paste the **SAML Entity ID**, in the **Issuer ID** textbox.</span></span>
   
    <span data-ttu-id="537d3-199">g.</span><span class="sxs-lookup"><span data-stu-id="537d3-199">g.</span></span> <span data-ttu-id="537d3-200">Dans la zone de texte **ID d’entité**, tapez l’URL `http://saml.marketo.com/sp`.</span><span class="sxs-lookup"><span data-stu-id="537d3-200">In the **Entity ID** textbox, enter the URL as `http://saml.marketo.com/sp`.</span></span>
   
    <span data-ttu-id="537d3-201">h.</span><span class="sxs-lookup"><span data-stu-id="537d3-201">h.</span></span> <span data-ttu-id="537d3-202">Sélectionnez l’emplacement d’ID utilisateur en tant **qu’élément Identificateur de nom**.</span><span class="sxs-lookup"><span data-stu-id="537d3-202">Select the User ID Location as **Name Identifier element**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_09.png)
   
    > [!NOTE]
    > <span data-ttu-id="537d3-204">Si votre identificateur d’utilisateur n’est pas une valeur UPN, alors changez la valeur dans l’onglet Attribut.</span><span class="sxs-lookup"><span data-stu-id="537d3-204">If your User Identifier is not UPN value then change the value in the Attribute tab.</span></span>
   
    <span data-ttu-id="537d3-205">i.</span><span class="sxs-lookup"><span data-stu-id="537d3-205">i.</span></span> <span data-ttu-id="537d3-206">Chargez le certificat que vous avez téléchargé à partir de l’Assistant de configuration Azure AD.</span><span class="sxs-lookup"><span data-stu-id="537d3-206">Upload the certificate, which you have downloaded from Azure AD configuration wizard.</span></span> <span data-ttu-id="537d3-207">**Enregistrez** les paramètres.</span><span class="sxs-lookup"><span data-stu-id="537d3-207">**Save** the settings.</span></span>
   
    <span data-ttu-id="537d3-208">j.</span><span class="sxs-lookup"><span data-stu-id="537d3-208">j.</span></span> <span data-ttu-id="537d3-209">Modifiez les paramètres des pages de redirection.</span><span class="sxs-lookup"><span data-stu-id="537d3-209">Edit the Redirect Pages settings.</span></span>
   
    <span data-ttu-id="537d3-210">k.</span><span class="sxs-lookup"><span data-stu-id="537d3-210">k.</span></span> <span data-ttu-id="537d3-211">Collez l’**URL du service d’authentification unique SAML** dans la zone de texte **URL de connexion**.</span><span class="sxs-lookup"><span data-stu-id="537d3-211">Paste the **SAML Single Sign-On Service URL** in the **Login URL** textbox.</span></span>
   
    <span data-ttu-id="537d3-212">l.</span><span class="sxs-lookup"><span data-stu-id="537d3-212">l.</span></span> <span data-ttu-id="537d3-213">Collez l’**URL de déconnexion** dans la zone de texte **URL de déconnexion**.</span><span class="sxs-lookup"><span data-stu-id="537d3-213">Paste the **Sign-Out URL** in the **Logout URL** textbox.</span></span>
   
    <span data-ttu-id="537d3-214">m.</span><span class="sxs-lookup"><span data-stu-id="537d3-214">m.</span></span> <span data-ttu-id="537d3-215">Dans l’**URL d’erreur**, copiez l’**URL de votre instance Marketo**, puis cliquez sur le bouton **Enregistrer** pour enregistrer les paramètres.</span><span class="sxs-lookup"><span data-stu-id="537d3-215">In the **Error URL**, copy your **Marketo instance URL** and click **Save** button to save settings.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_10.png)

9. <span data-ttu-id="537d3-217">Pour activer l’authentification unique pour les utilisateurs, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="537d3-217">To enable the SSO for users, complete the following actions:</span></span>
   
    <span data-ttu-id="537d3-218">a.</span><span class="sxs-lookup"><span data-stu-id="537d3-218">a.</span></span> <span data-ttu-id="537d3-219">Connectez-vous à l’application Marketo à l’aide des informations d’identification de l’administrateur.</span><span class="sxs-lookup"><span data-stu-id="537d3-219">Log in to Marketo app using admin credentials.</span></span>
   
    <span data-ttu-id="537d3-220">b.</span><span class="sxs-lookup"><span data-stu-id="537d3-220">b.</span></span> <span data-ttu-id="537d3-221">Dans le volet de navigation supérieur, cliquez sur le bouton **Administrateur**.</span><span class="sxs-lookup"><span data-stu-id="537d3-221">Click the **Admin** button on the top navigation pane.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="537d3-223">c.</span><span class="sxs-lookup"><span data-stu-id="537d3-223">c.</span></span> <span data-ttu-id="537d3-224">Accédez au menu **Sécurité** et cliquez sur **Paramètres de connexion**.</span><span class="sxs-lookup"><span data-stu-id="537d3-224">Navigate to the **Security** menu and click **Login Settings**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_13.png)
   
    <span data-ttu-id="537d3-226">d.</span><span class="sxs-lookup"><span data-stu-id="537d3-226">d.</span></span> <span data-ttu-id="537d3-227">Vérifiez l’option **Exiger l’authentification unique** et **enregistrez** les paramètres.</span><span class="sxs-lookup"><span data-stu-id="537d3-227">Check the **Require SSO** option and **Save** the settings.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_14.png)

> [!TIP]
> <span data-ttu-id="537d3-229">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="537d3-229">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="537d3-230">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="537d3-230">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="537d3-231">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="537d3-231">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="537d3-232">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="537d3-232">Creating an Azure AD test user</span></span>
<span data-ttu-id="537d3-233">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="537d3-233">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="537d3-235">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="537d3-235">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="537d3-236">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="537d3-236">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="537d3-238">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="537d3-238">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="537d3-240">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="537d3-240">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="537d3-242">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="537d3-242">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="537d3-244">a.</span><span class="sxs-lookup"><span data-stu-id="537d3-244">a.</span></span> <span data-ttu-id="537d3-245">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="537d3-245">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="537d3-246">b.</span><span class="sxs-lookup"><span data-stu-id="537d3-246">b.</span></span> <span data-ttu-id="537d3-247">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="537d3-247">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="537d3-248">c.</span><span class="sxs-lookup"><span data-stu-id="537d3-248">c.</span></span> <span data-ttu-id="537d3-249">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="537d3-249">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="537d3-250">d.</span><span class="sxs-lookup"><span data-stu-id="537d3-250">d.</span></span> <span data-ttu-id="537d3-251">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="537d3-251">Click **Create**.</span></span>
 
### <a name="creating-a-marketo-test-user"></a><span data-ttu-id="537d3-252">Créer un utilisateur de test Marketo</span><span class="sxs-lookup"><span data-stu-id="537d3-252">Creating a Marketo test user</span></span>

<span data-ttu-id="537d3-253">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Marketo.</span><span class="sxs-lookup"><span data-stu-id="537d3-253">In this section, you create a user called Britta Simon in Marketo.</span></span> <span data-ttu-id="537d3-254">Pour créer un utilisateur dans la plateforme Marketo, suivez ces étapes.</span><span class="sxs-lookup"><span data-stu-id="537d3-254">follow these steps to create a user in Marketo platform.</span></span>

1. <span data-ttu-id="537d3-255">Connectez-vous à l’application Marketo à l’aide des informations d’identification de l’administrateur.</span><span class="sxs-lookup"><span data-stu-id="537d3-255">Log in to Marketo app using admin credentials.</span></span>

2. <span data-ttu-id="537d3-256">Dans le volet de navigation supérieur, cliquez sur le bouton **Administrateur**.</span><span class="sxs-lookup"><span data-stu-id="537d3-256">Click the **Admin** button on the top navigation pane.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 

3. <span data-ttu-id="537d3-258">Accédez au menu **Sécurité** et cliquez sur **Utilisateurs et rôles**</span><span class="sxs-lookup"><span data-stu-id="537d3-258">Navigate to the **Security** menu and click **Users & Roles**</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_19.png)  

4. <span data-ttu-id="537d3-260">Dans l’onglet Utilisateurs, cliquez sur le lien **Inviter un nouvel utilisateur**</span><span class="sxs-lookup"><span data-stu-id="537d3-260">Click the **Invite New User** link on the Users tab</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_15.png) 

5. <span data-ttu-id="537d3-262">Dans l’Assistant d’invitation d’un nouvel utilisateur, renseignez les informations suivantes.</span><span class="sxs-lookup"><span data-stu-id="537d3-262">In the Invite New User wizard fill the following information</span></span>
   
    <span data-ttu-id="537d3-263">a.</span><span class="sxs-lookup"><span data-stu-id="537d3-263">a.</span></span> <span data-ttu-id="537d3-264">Entrez l’adresse **e-mail** de l’utilisateur dans la zone de texte.</span><span class="sxs-lookup"><span data-stu-id="537d3-264">Enter the user **Email** address in the textbox</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_16.png)
   
    <span data-ttu-id="537d3-266">b.</span><span class="sxs-lookup"><span data-stu-id="537d3-266">b.</span></span> <span data-ttu-id="537d3-267">Entrez le **prénom** dans la zone de texte.</span><span class="sxs-lookup"><span data-stu-id="537d3-267">Enter the **First Name** in the textbox</span></span>
   
    <span data-ttu-id="537d3-268">c.</span><span class="sxs-lookup"><span data-stu-id="537d3-268">c.</span></span> <span data-ttu-id="537d3-269">Entrez le **nom** dans la zone de texte</span><span class="sxs-lookup"><span data-stu-id="537d3-269">Enter the **Last Name**  in the textbox</span></span>
   
    <span data-ttu-id="537d3-270">d.</span><span class="sxs-lookup"><span data-stu-id="537d3-270">d.</span></span> <span data-ttu-id="537d3-271">Cliquez sur **Suivant**</span><span class="sxs-lookup"><span data-stu-id="537d3-271">Click **Next**</span></span>

6. <span data-ttu-id="537d3-272">Dans l’onglet **Autorisations**, sélectionnez les **rôles d’utilisateur** et cliquez sur **Suivant**</span><span class="sxs-lookup"><span data-stu-id="537d3-272">In the **Permissions** tab, select the **userRoles** and click **Next**</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_17.png)
7. <span data-ttu-id="537d3-274">Pour envoyer l’invitation d’utilisateur, cliquez sur le bouton **Envoyer**</span><span class="sxs-lookup"><span data-stu-id="537d3-274">Click the **Send** button to send the user invitation</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_18.png)

8. <span data-ttu-id="537d3-276">L’utilisateur recevra une notification par e-mail. Pour activer le compte, il devra cliquer sur le lien et modifier le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="537d3-276">User receives the email notification and has to click the link and change the password to activate the account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="537d3-277">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="537d3-277">Assigning the Azure AD test user</span></span>

<span data-ttu-id="537d3-278">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Marketo.</span><span class="sxs-lookup"><span data-stu-id="537d3-278">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Marketo.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="537d3-280">**Pour affecter Britta Simon à Marketo, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="537d3-280">**To assign Britta Simon to Marketo, perform the following steps:**</span></span>

1. <span data-ttu-id="537d3-281">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="537d3-281">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="537d3-283">Dans la liste des applications, sélectionnez **Marketo**.</span><span class="sxs-lookup"><span data-stu-id="537d3-283">In the applications list, select **Marketo**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_app.png) 

3. <span data-ttu-id="537d3-285">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="537d3-285">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="537d3-287">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="537d3-287">Click **Add** button.</span></span> <span data-ttu-id="537d3-288">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="537d3-288">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="537d3-290">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="537d3-290">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="537d3-291">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="537d3-291">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="537d3-292">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="537d3-292">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="537d3-293">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="537d3-293">Testing single sign-on</span></span>

<span data-ttu-id="537d3-294">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="537d3-294">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="537d3-295">Lorsque vous cliquez sur la mosaïque Marketo dans le volet d’accès, vous êtes connecté automatiquement à votre application Marketo.</span><span class="sxs-lookup"><span data-stu-id="537d3-295">When you click the Marketo tile in the Access Panel, you should get automatically signed-on to your Marketo application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="537d3-296">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="537d3-296">Additional resources</span></span>

* [<span data-ttu-id="537d3-297">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="537d3-297">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="537d3-298">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="537d3-298">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_203.png

