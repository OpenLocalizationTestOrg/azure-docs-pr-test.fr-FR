---
title: "Didacticiel : Intégration d’Azure Active Directory à Sprinklr | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Sprinklr."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b33938a1-25a5-484c-8e75-7dc6de2d534d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 6e1622cd55e3b0e8063604ac9dc0cb0673fa9753
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sprinklr"></a><span data-ttu-id="ffbc0-103">Didacticiel : Intégration d’Azure Active Directory à Sprinklr</span><span class="sxs-lookup"><span data-stu-id="ffbc0-103">Tutorial: Azure Active Directory integration with Sprinklr</span></span>

<span data-ttu-id="ffbc0-104">Dans ce didacticiel, vous allez apprendre à intégrer Sprinklr à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ffbc0-104">In this tutorial, you learn how to integrate Sprinklr with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ffbc0-105">L’intégration de Sprinklr dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="ffbc0-105">Integrating Sprinklr with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ffbc0-106">Dans Azure AD, vous pouvez contrôler qui a accès à Sprinklr</span><span class="sxs-lookup"><span data-stu-id="ffbc0-106">You can control in Azure AD who has access to Sprinklr</span></span>
- <span data-ttu-id="ffbc0-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Sprinklr (par le biais de l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="ffbc0-107">You can enable your users to automatically get signed-on to Sprinklr (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ffbc0-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="ffbc0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ffbc0-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ffbc0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ffbc0-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ffbc0-110">Prerequisites</span></span>

<span data-ttu-id="ffbc0-111">Pour configurer l’intégration d’Azure AD à Sprinklr, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ffbc0-111">To configure Azure AD integration with Sprinklr, you need the following items:</span></span>

- <span data-ttu-id="ffbc0-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="ffbc0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ffbc0-113">Un abonnement Sprinklr pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="ffbc0-113">A Sprinklr single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ffbc0-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ffbc0-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ffbc0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ffbc0-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ffbc0-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ffbc0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ffbc0-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="ffbc0-118">Scenario description</span></span>
<span data-ttu-id="ffbc0-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ffbc0-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="ffbc0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ffbc0-121">Ajout de Sprinklr à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="ffbc0-121">Adding Sprinklr from the gallery</span></span>
2. <span data-ttu-id="ffbc0-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ffbc0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sprinklr-from-the-gallery"></a><span data-ttu-id="ffbc0-123">Ajout de Sprinklr à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="ffbc0-123">Adding Sprinklr from the gallery</span></span>
<span data-ttu-id="ffbc0-124">Pour configurer l’intégration de Sprinklr avec Azure AD, vous devez ajouter Sprinklr, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-124">To configure the integration of Sprinklr into Azure AD, you need to add Sprinklr from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ffbc0-125">**Pour ajouter Sprinklr à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ffbc0-125">**To add Sprinklr from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ffbc0-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ffbc0-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ffbc0-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="ffbc0-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="ffbc0-133">Dans la zone de recherche, entrez **Sprinklr**.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-133">In the search box, type **Sprinklr**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_search.png)

5. <span data-ttu-id="ffbc0-135">Dans le volet de résultats, sélectionnez **Sprinklr**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-135">In the results panel, select **Sprinklr**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ffbc0-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ffbc0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ffbc0-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Sprinklr, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="ffbc0-138">In this section, you configure and test Azure AD single sign-on with Sprinklr based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ffbc0-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Sprinklr correspondant dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Sprinklr is to a user in Azure AD.</span></span> <span data-ttu-id="ffbc0-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Sprinklr associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-140">In other words, a link relationship between an Azure AD user and the related user in Sprinklr needs to be established.</span></span>

<span data-ttu-id="ffbc0-141">Dans Sprinklr, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-141">In Sprinklr, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ffbc0-142">Pour configurer et tester l’authentification unique Azure AD avec Sprinklr, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="ffbc0-142">To configure and test Azure AD single sign-on with Sprinklr, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ffbc0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ffbc0-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ffbc0-145">**[Création d’un utilisateur de test Sprinklr](#creating-a-sprinklr-test-user)** pour avoir un équivalent de Britta Simon dans Sprinklr lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-145">**[Creating a Sprinklr test user](#creating-a-sprinklr-test-user)** - to have a counterpart of Britta Simon in Sprinklr that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ffbc0-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ffbc0-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ffbc0-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ffbc0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ffbc0-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Sprinklr.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Sprinklr application.</span></span>

<span data-ttu-id="ffbc0-150">**Pour configurer l’authentification unique Azure AD avec Sprinklr, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ffbc0-150">**To configure Azure AD single sign-on with Sprinklr, perform the following steps:**</span></span>

1. <span data-ttu-id="ffbc0-151">Dans le portail Azure, sur la page d’intégration de l’application **Sprinklr**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-151">In the Azure portal, on the **Sprinklr** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="ffbc0-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_samlbase.png)

3. <span data-ttu-id="ffbc0-155">Dans la section **Domaine et URL Sprinklr**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ffbc0-155">On the **Sprinklr Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_url.png)

    <span data-ttu-id="ffbc0-157">a.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-157">a.</span></span> <span data-ttu-id="ffbc0-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<subdomain>.sprinklr.com`</span><span class="sxs-lookup"><span data-stu-id="ffbc0-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    <span data-ttu-id="ffbc0-159">b.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-159">b.</span></span> <span data-ttu-id="ffbc0-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<subdomain>.sprinklr.com`</span><span class="sxs-lookup"><span data-stu-id="ffbc0-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ffbc0-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-161">These values are not real.</span></span> <span data-ttu-id="ffbc0-162">Mettez à jour les valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-162">Update the value with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ffbc0-163">Pour obtenir ces valeurs, contactez l’[équipe de support technique Sprinklr](https://www.sprinklr.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="ffbc0-163">Contact [Sprinklr Client support team](https://www.sprinklr.com/contact-us/) to get these values.</span></span> 
 
4. <span data-ttu-id="ffbc0-164">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_certificate.png) 

5. <span data-ttu-id="ffbc0-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="ffbc0-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sprinklr-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ffbc0-168">Dans la section **Configuration de Sprinklr**, cliquez sur **Configurer Sprinklr** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-168">On the **Sprinklr Configuration** section, click **Configure Sprinklr** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ffbc0-169">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="ffbc0-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

7. <span data-ttu-id="ffbc0-170">Dans une autre fenêtre de navigateur web, connectez-vous au site de votre entreprise Sprinklr en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-170">In a different web browser window, log in to your Sprinklr company site as an administrator.</span></span>

8. <span data-ttu-id="ffbc0-171">Accédez à **Administration \> Settings**.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-171">Go to **Administration \> Settings**.</span></span>
   
    <span data-ttu-id="ffbc0-172">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="ffbc0-172">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span></span>

9. <span data-ttu-id="ffbc0-173">Accédez à **Manager Partner \> Single Sign** dans le volet gauche.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-173">Go to **Manage Partner \> Single Sign** on from the left pane.</span></span>
   
    <span data-ttu-id="ffbc0-174">![Gérer les partenaires](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "Gérer les partenaires")</span><span class="sxs-lookup"><span data-stu-id="ffbc0-174">![Manage Partner](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "Manage Partner")</span></span>

10. <span data-ttu-id="ffbc0-175">Cliquez sur **+Add Single Sign Ons**.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-175">Click **+Add Single Sign Ons**.</span></span>
   
    <span data-ttu-id="ffbc0-176">![Authentification unique](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "Authentification unique")</span><span class="sxs-lookup"><span data-stu-id="ffbc0-176">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "Single Sign-Ons")</span></span>

11. <span data-ttu-id="ffbc0-177">Dans la page **Single Sign on** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ffbc0-177">On the **Single Sign on** page, perform the following steps:</span></span>
   
    <span data-ttu-id="ffbc0-178">![Authentification unique](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "Authentification unique")</span><span class="sxs-lookup"><span data-stu-id="ffbc0-178">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "Single Sign-Ons")</span></span>

    <span data-ttu-id="ffbc0-179">a.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-179">a.</span></span> <span data-ttu-id="ffbc0-180">Dans la zone de texte **Name**, indiquez le nom de votre configuration (par exemple, *WAADSSOTest*).</span><span class="sxs-lookup"><span data-stu-id="ffbc0-180">In the **Name** textbox, type a name for your configuration (for example: *WAADSSOTest*).</span></span>

    <span data-ttu-id="ffbc0-181">b.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-181">b.</span></span> <span data-ttu-id="ffbc0-182">Sélectionnez **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-182">Select **Enabled**.</span></span>

    <span data-ttu-id="ffbc0-183">c.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-183">c.</span></span> <span data-ttu-id="ffbc0-184">Sélectionnez **Use new SSO Certificate**.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-184">Select **Use new SSO Certificate**.</span></span>
             
    <span data-ttu-id="ffbc0-185">e.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-185">e.</span></span> <span data-ttu-id="ffbc0-186">Ouvrez votre certificat codé en base 64 dans le Bloc-notes, copiez son contenu dans le Presse-papiers, puis collez-le dans la zone de texte **Identity provider certificate (Certificat du fournisseur d’identité)**.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-186">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Identity Provider Certificate** textbox.</span></span>

    <span data-ttu-id="ffbc0-187">f.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-187">f.</span></span> <span data-ttu-id="ffbc0-188">Dans la zone de texte **ID d’entité**, collez la valeur **ID d’entité SAML** que vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-188">Paste the **SAML Entity ID** value which you have copied from Azure Portal into the **Entity Id** textbox.</span></span>

    <span data-ttu-id="ffbc0-189">g.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-189">g.</span></span> <span data-ttu-id="ffbc0-190">Collez la valeur **URL du service d’authentification unique SAML** copiée à partir du portail Azure dans la zone de texte **URL d’identification du fournisseur d’identité**.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-190">Paste the **SAML Single Sign-On Service URL** value which you have copied from Azure Portal into the **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="ffbc0-191">h.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-191">h.</span></span> <span data-ttu-id="ffbc0-192">Collez la valeur **URL de déconnexion** copiée à partir du portail Azure dans la zone de texte **URL de déconnexion du fournisseur d’identité**.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-192">Paste the **Sign-Out URL** value which you have copied from Azure Portal into the **Identity Provider Logout URL** textbox.</span></span>
     
    <span data-ttu-id="ffbc0-193">i.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-193">i.</span></span> <span data-ttu-id="ffbc0-194">Dans **SAML User ID Type**, sélectionnez **Assertion contains User’s sprinklr.com username**.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-194">As **SAML User ID Type**, select **Assertion contains User”s sprinklr.com username**.</span></span>

    <span data-ttu-id="ffbc0-195">j.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-195">j.</span></span> <span data-ttu-id="ffbc0-196">Dans **SAML User ID Location**, sélectionnez **User ID is in the Name Identifier element of the Subject statement**.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-196">As **SAML User ID Location**, select **User ID is in the Name Identifier element of the Subject statement**.</span></span>

    <span data-ttu-id="ffbc0-197">k.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-197">k.</span></span> <span data-ttu-id="ffbc0-198">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-198">Click **Save**.</span></span>
       
    <span data-ttu-id="ffbc0-199">![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="ffbc0-199">![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")</span></span>

> [!TIP]
> <span data-ttu-id="ffbc0-200">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ffbc0-201">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ffbc0-202">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ffbc0-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ffbc0-203">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="ffbc0-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="ffbc0-204">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="ffbc0-206">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ffbc0-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ffbc0-207">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-207">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ffbc0-209">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-209">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ffbc0-211">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-211">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ffbc0-213">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ffbc0-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ffbc0-215">a.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-215">a.</span></span> <span data-ttu-id="ffbc0-216">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ffbc0-217">b.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-217">b.</span></span> <span data-ttu-id="ffbc0-218">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ffbc0-219">c.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-219">c.</span></span> <span data-ttu-id="ffbc0-220">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ffbc0-221">d.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-221">d.</span></span> <span data-ttu-id="ffbc0-222">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-222">Click **Create**.</span></span>
 
### <a name="creating-a-sprinklr-test-user"></a><span data-ttu-id="ffbc0-223">Création d’un utilisateur de test Sprinklr</span><span class="sxs-lookup"><span data-stu-id="ffbc0-223">Creating a Sprinklr test user</span></span>

1. <span data-ttu-id="ffbc0-224">Connectez-vous à votre site d’entreprise Sprinklr en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-224">Log in to your Sprinklr company site as an administrator.</span></span>

2. <span data-ttu-id="ffbc0-225">Accédez à **Administration \> Settings**.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-225">Go to **Administration \> Settings**.</span></span>
   
    <span data-ttu-id="ffbc0-226">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="ffbc0-226">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span></span>

3. <span data-ttu-id="ffbc0-227">Accédez à **Manage Client \> Users** dans le volet gauche.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-227">Go to **Manage Client \> Users** from the left pane.</span></span>
   
    <span data-ttu-id="ffbc0-228">![Paramètres](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "Paramètres")</span><span class="sxs-lookup"><span data-stu-id="ffbc0-228">![Settings](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "Settings")</span></span>

4. <span data-ttu-id="ffbc0-229">Cliquez sur **Add User**.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-229">Click **Add User**.</span></span>
   
    <span data-ttu-id="ffbc0-230">![Paramètres](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "Paramètres")</span><span class="sxs-lookup"><span data-stu-id="ffbc0-230">![Settings](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "Settings")</span></span>

5. <span data-ttu-id="ffbc0-231">Dans la page **Edit User** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ffbc0-231">On the **Edit user** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="ffbc0-232">![Modifier l’utilisateur](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "Modifier l’utilisateur")</span><span class="sxs-lookup"><span data-stu-id="ffbc0-232">![Edit user](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "Edit user")</span></span> 

    <span data-ttu-id="ffbc0-233">a.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-233">a.</span></span> <span data-ttu-id="ffbc0-234">Dans les zones de texte **Email**, **First Name** et **Last Name**, saisissez les informations du compte utilisateur Azure AD que vous souhaitez approvisionner.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-234">In the **Email**, **First Name** and **Last Name** textboxes, type the information of an Azure AD user account you want to provision.</span></span>

    <span data-ttu-id="ffbc0-235">b.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-235">b.</span></span> <span data-ttu-id="ffbc0-236">Sélectionnez **Password Disabled**.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-236">Select **Password Disabled**.</span></span>

    <span data-ttu-id="ffbc0-237">c.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-237">c.</span></span> <span data-ttu-id="ffbc0-238">Sélectionner une **Langue**.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-238">Select **Language**.</span></span>

    <span data-ttu-id="ffbc0-239">d.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-239">d.</span></span> <span data-ttu-id="ffbc0-240">Sélectionnez un **Type d’utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-240">Select **User Type**.</span></span>

    <span data-ttu-id="ffbc0-241">e.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-241">e.</span></span> <span data-ttu-id="ffbc0-242">Cliquez sur **Mettre à jour**.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-242">Click **Update**.</span></span>
   
     >[!IMPORTANT]
     ><span data-ttu-id="ffbc0-243">**Password Disabled** pour permettre à un utilisateur de se connecter par le biais d’un fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-243">**Password Disabled** must be selected to enable a user to log in via an Identity provider.</span></span> 
     
6. <span data-ttu-id="ffbc0-244">Accédez à **Role**, puis procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ffbc0-244">Go to **Role**, and then perform the following steps:</span></span>
   
    <span data-ttu-id="ffbc0-245">![Rôles de partenaires](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "Rôles de partenaires")</span><span class="sxs-lookup"><span data-stu-id="ffbc0-245">![Partner Roles](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "Partner Roles")</span></span>

    <span data-ttu-id="ffbc0-246">a.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-246">a.</span></span> <span data-ttu-id="ffbc0-247">Dans la liste **Global**, sélectionnez **ALL\_Permissions**.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-247">From the **Global** list, select **ALL\_Permissions**.</span></span>  

    <span data-ttu-id="ffbc0-248">b.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-248">b.</span></span> <span data-ttu-id="ffbc0-249">Cliquez sur **Mettre à jour**.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-249">Click **Update**.</span></span>

>[!NOTE]
><span data-ttu-id="ffbc0-250">Vous pouvez utiliser n’importe quel outil ou API de création de compte utilisateur, fourni par Sprinklr, pour approvisionner des comptes utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-250">You can use any other Sprinklr user account creation tools or APIs provided by Sprinklr to provision Azure AD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ffbc0-251">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="ffbc0-251">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ffbc0-252">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Sprinklr.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-252">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Sprinklr.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="ffbc0-254">**Pour affecter Britta Simon à Sprinklr, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ffbc0-254">**To assign Britta Simon to Sprinklr, perform the following steps:**</span></span>

1. <span data-ttu-id="ffbc0-255">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-255">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="ffbc0-257">Dans la liste des applications, sélectionnez **Sprinklr**.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-257">In the applications list, select **Sprinklr**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_app.png) 

3. <span data-ttu-id="ffbc0-259">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-259">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="ffbc0-261">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-261">Click **Add** button.</span></span> <span data-ttu-id="ffbc0-262">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-262">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="ffbc0-264">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-264">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ffbc0-265">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-265">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ffbc0-266">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-266">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ffbc0-267">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="ffbc0-267">Testing single sign-on</span></span>

<span data-ttu-id="ffbc0-268">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="ffbc0-268">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ffbc0-269">Lorsque vous cliquez sur la vignette Sprinklr dans le volet d'accès, vous serez connecté automatiquement à votre application Sprinklr. Pour en savoir plus sur le volet d’accès, consultez l’article [Présentation du volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ffbc0-269">When you click the Sprinklr tile in the Access Panel, you should get automatically signed-on to your Sprinklr application For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ffbc0-270">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="ffbc0-270">Additional resources</span></span>

* [<span data-ttu-id="ffbc0-271">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ffbc0-271">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ffbc0-272">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="ffbc0-272">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_203.png

