---
title: "Didacticiel : intégration d’Azure Active Directory à Google Apps dans Azure | Documents Microsoft"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Google Apps."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 38a6ca75-7fd0-4cdc-9b9f-fae080c5a016
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 065841d6b4fe50e953f01bba4d3f23de82b82726
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-google-apps"></a><span data-ttu-id="ca063-103">Didacticiel : Intégration d’Azure Active Directory à Google Apps</span><span class="sxs-lookup"><span data-stu-id="ca063-103">Tutorial: Azure Active Directory integration with Google Apps</span></span>

<span data-ttu-id="ca063-104">Dans ce didacticiel, vous allez apprendre à intégrer Google Apps à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ca063-104">In this tutorial, you learn how to integrate Google Apps with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ca063-105">L’intégration de Google Apps dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="ca063-105">Integrating Google Apps with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ca063-106">Dans Azure AD, vous pouvez contrôler qui a accès à Google Apps</span><span class="sxs-lookup"><span data-stu-id="ca063-106">You can control in Azure AD who has access to Google Apps</span></span>
- <span data-ttu-id="ca063-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Google Apps (via l’authentification unique) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="ca063-107">You can enable your users to automatically get signed-on to Google Apps (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ca063-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="ca063-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ca063-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ca063-109">If you want to know more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ca063-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ca063-110">Prerequisites</span></span>

<span data-ttu-id="ca063-111">Pour configurer l’intégration d’Azure AD avec Google Apps, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ca063-111">To configure Azure AD integration with Google Apps, you need the following items:</span></span>

- <span data-ttu-id="ca063-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="ca063-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ca063-113">Un abonnement Google pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="ca063-113">A Google Apps single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ca063-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="ca063-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ca063-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ca063-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ca063-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ca063-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ca063-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez bénéficier de l’essai d’un mois ici : [Offre d’essai](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ca063-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="video-tutorial"></a><span data-ttu-id="ca063-118">Didacticiel vidéo</span><span class="sxs-lookup"><span data-stu-id="ca063-118">Video tutorial</span></span>
<span data-ttu-id="ca063-119">Comment activer l'authentification unique pour Google Apps en 2 minutes :</span><span class="sxs-lookup"><span data-stu-id="ca063-119">How to Enable Single Sign-On to Google Apps in 2 Minutes:</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Enable-single-sign-on-to-Google-Apps-in-2-minutes-with-Azure-AD/player]

## <a name="frequently-asked-questions"></a><span data-ttu-id="ca063-120">Forum Aux Questions (FAQ)</span><span class="sxs-lookup"><span data-stu-id="ca063-120">Frequently Asked Questions</span></span>
1. <span data-ttu-id="ca063-121">**Q : Les Chromebooks et les autres appareils Chrome sont-ils compatibles avec l’authentification unique Azure AD ?**</span><span class="sxs-lookup"><span data-stu-id="ca063-121">**Q: Are Chromebooks and other Chrome devices compatible with Azure AD single sign-on?**</span></span>
   
    <span data-ttu-id="ca063-122">R : Oui, les utilisateurs pourront se connecter à leurs périphériques Chromebook en saisissant leurs informations d’identification Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ca063-122">A: Yes, users are able to sign into their Chromebook devices using their Azure AD credentials.</span></span> <span data-ttu-id="ca063-123">Consultez cet [article du support technique Google Apps](https://support.google.com/chrome/a/answer/6060880) pour en savoir plus sur les raisons de la double demande de saisie des informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="ca063-123">See this [Google Apps support article](https://support.google.com/chrome/a/answer/6060880) for information on why users may get prompted for credentials twice.</span></span>

2. <span data-ttu-id="ca063-124">**Q : Si j’ai activé l’authentification unique, les utilisateurs pourront-ils utiliser leurs informations d’identification Azure AD pour se connecter à un produit Google, comme Google Classroom, Gmail, Google Drive, YouTube, etc. ?**</span><span class="sxs-lookup"><span data-stu-id="ca063-124">**Q: If I enable single sign-on, will users be able to use their Azure AD credentials to sign into any Google product, such as Google Classroom, GMail, Google Drive, YouTube, and so on?**</span></span>
   
    <span data-ttu-id="ca063-125">R : Oui, en fonction des [Google apps](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) que vous choisissez d’activer et de désactiver pour votre organisation.</span><span class="sxs-lookup"><span data-stu-id="ca063-125">A: Yes, depending on [which Google apps](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) you choose to enable or disable for your organization.</span></span>

3. <span data-ttu-id="ca063-126">**Q : Puis-je activer l’authentification unique pour uniquement un sous-ensemble de mes utilisateurs Google Apps ?**</span><span class="sxs-lookup"><span data-stu-id="ca063-126">**Q: Can I enable single sign-on for only a subset of my Google Apps users?**</span></span>
   
    <span data-ttu-id="ca063-127">R : Non, si vous activez l’authentification unique, l’ensemble des utilisateurs Google Apps devront s’authentifier avec leurs informations d’identification Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ca063-127">A: No, turning on single sign-on immediately requires all your Google Apps users to authenticate with their Azure AD credentials.</span></span> <span data-ttu-id="ca063-128">Google Apps ne prenant pas en charge plusieurs fournisseurs d’identité, le fournisseur associé à votre environnement Google Apps peut être Azure AD ou Google, mais pas les deux.</span><span class="sxs-lookup"><span data-stu-id="ca063-128">Because Google Apps doesn't support having multiple identity providers, the identity provider for your Google Apps environment can either be Azure AD or Google -- but not both at the same time.</span></span>

4. <span data-ttu-id="ca063-129">**Q : Si un utilisateur est connecté via Windows, est-il automatiquement authentifié sur Google Apps sans qu’il ne lui soit demandé de saisir un mot de passe ?**</span><span class="sxs-lookup"><span data-stu-id="ca063-129">**Q: If a user is signed in through Windows, are they automatically authenticate to Google Apps without getting prompted for a password?**</span></span>
   
    <span data-ttu-id="ca063-130">R : Ce scénario peut être activé par le biais de deux options.</span><span class="sxs-lookup"><span data-stu-id="ca063-130">A: There are two options for enabling this scenario.</span></span> <span data-ttu-id="ca063-131">Tout d’abord, les utilisateurs peuvent se connecter aux appareils Windows 10 via [Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ca063-131">First, users could sign into Windows 10 devices via [Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span></span> <span data-ttu-id="ca063-132">Sinon, les utilisateurs peuvent se connecter aux appareils Windows joints à un domaine au sein d’un répertoire Active Directory sur lequel est activée l’authentification unique à Azure AD via un déploiement [Active Directory Federation Services (AD FS)](active-directory-aadconnect-user-signin.md) .</span><span class="sxs-lookup"><span data-stu-id="ca063-132">Alternatively, users could sign into Windows devices that are domain-joined to an on-premises Active Directory that has been enabled for single sign-on to Azure AD via an [Active Directory Federation Services (AD FS)](active-directory-aadconnect-user-signin.md) deployment.</span></span> <span data-ttu-id="ca063-133">Quelle que soit l’option choisie, vous devez suivre le didacticiel ci-dessous pour activer l’authentification unique entre Azure AD et Google Apps.</span><span class="sxs-lookup"><span data-stu-id="ca063-133">Both options require you to perform the steps in the following tutorial to enable single sign-on between Azure AD and Google Apps.</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ca063-134">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="ca063-134">Scenario description</span></span>
<span data-ttu-id="ca063-135">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="ca063-135">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ca063-136">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="ca063-136">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ca063-137">Ajout de Google Apps à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="ca063-137">Adding Google Apps from the gallery</span></span>
2. <span data-ttu-id="ca063-138">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ca063-138">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-google-apps-from-the-gallery"></a><span data-ttu-id="ca063-139">Ajout de Google Apps à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="ca063-139">Adding Google Apps from the gallery</span></span>
<span data-ttu-id="ca063-140">Pour configurer l’intégration de Google Apps à Azure AD, vous devez ajouter Google Apps à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="ca063-140">To configure the integration of Google Apps into Azure AD, you need to add Google Apps from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ca063-141">**Pour ajouter Google Apps à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ca063-141">**To add Google Apps from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ca063-142">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ca063-142">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ca063-144">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="ca063-144">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ca063-145">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ca063-145">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="ca063-147">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ca063-147">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="ca063-149">Dans la zone de recherche entrez **Google Apps**.</span><span class="sxs-lookup"><span data-stu-id="ca063-149">In the search box, type **Google Apps**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_search.png)

5. <span data-ttu-id="ca063-151">Dans le panneau de résultats, sélectionnez **Google Apps**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="ca063-151">In the results panel, select **Google Apps**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ca063-153">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ca063-153">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ca063-154">Dans cette section, configurez et testez l’authentification unique Azure AD avec Google Apps sur un utilisateur test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="ca063-154">In this section, you configure and test Azure AD single sign-on with Google Apps based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ca063-155">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Google Apps équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ca063-155">For single sign-on to work, Azure AD needs to know what the counterpart user in Google Apps is to a user in Azure AD.</span></span> <span data-ttu-id="ca063-156">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Google Apps associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="ca063-156">In other words, a link relationship between an Azure AD user and the related user in Google Apps needs to be established.</span></span>

<span data-ttu-id="ca063-157">Cette relation est établie en attribuant la valeur du **nom d’utilisateur** dans Azure AD comme valeur **Nom d’utilisateur** dans Google Apps.</span><span class="sxs-lookup"><span data-stu-id="ca063-157">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Google Apps.</span></span>

<span data-ttu-id="ca063-158">Pour configurer et tester l’authentification unique Azure AD avec Google Apps, vous devez terminer les sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="ca063-158">To configure and test Azure AD single sign-on with Google Apps, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ca063-159">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="ca063-159">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ca063-160">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ca063-160">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ca063-161">**[Création d’un utilisateur de test Google Apps](#creating-a-google-apps-test-user)** : pour avoir un équivalent de Britta Simon dans Google Apps, lié à la représentation de l’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ca063-161">**[Creating a Google Apps test user](#creating-a-google-apps-test-user)** - to have a counterpart of Britta Simon in Google Apps that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ca063-162">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ca063-162">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ca063-163">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="ca063-163">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ca063-164">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ca063-164">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ca063-165">Dans cette section, activez l’authentification unique Azure AD dans le portail Azure et configurez l’authentification unique dans votre application Google Apps.</span><span class="sxs-lookup"><span data-stu-id="ca063-165">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Google Apps application.</span></span>

<span data-ttu-id="ca063-166">**Pour configurer l’authentification unique Azure AD avec Google Apps, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ca063-166">**To configure Azure AD single sign-on with Google Apps, perform the following steps:**</span></span>

1. <span data-ttu-id="ca063-167">Dans le portail Azure, sur la page d’intégration de l’application **Google Apps**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="ca063-167">In the Azure portal, on the **Google Apps** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="ca063-169">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ca063-169">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_samlbase.png)

3. <span data-ttu-id="ca063-171">Dans la section **Domaine et URL Google Apps**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ca063-171">On the **Google Apps Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_url.png)

    <span data-ttu-id="ca063-173">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://mail.google.com/a/<yourdomain>`</span><span class="sxs-lookup"><span data-stu-id="ca063-173">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://mail.google.com/a/<yourdomain>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ca063-174">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="ca063-174">This value is not real.</span></span> <span data-ttu-id="ca063-175">Mettez à jour la valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="ca063-175">Update the value with the actual Sign-on URL.</span></span> <span data-ttu-id="ca063-176">Contactez [l’équipe de support technique de Google](https://www.google.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="ca063-176">contact the [Google support team](https://www.google.com/contact/).</span></span>
 
4. <span data-ttu-id="ca063-177">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat** puis enregistrez le certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="ca063-177">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_certificate.png) 

5. <span data-ttu-id="ca063-179">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="ca063-179">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-google-apps-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ca063-181">Dans la section **Configuration de Google Apps**, cliquez sur **Configurer Google Apps** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="ca063-181">On the **Google Apps Configuration** section, click **Configure Google Apps** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ca063-182">Copiez **l’URL de déconnexion, l’URL de modification du mot de passe et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="ca063-182">Copy the **Sign-Out URL, SAML Single Sign-On Service URL and Change password URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_configure.png) 

7. <span data-ttu-id="ca063-184">Ouvrez un nouvel onglet dans votre navigateur et utilisez votre compte d’administrateur pour vous connecter à la [Console d’administration de Google Apps](http://admin.google.com/) .</span><span class="sxs-lookup"><span data-stu-id="ca063-184">Open a new tab in your browser, and sign into the [Google Apps Admin Console](http://admin.google.com/) using your administrator account.</span></span>

8. <span data-ttu-id="ca063-185">Cliquez sur **Sécurité**.</span><span class="sxs-lookup"><span data-stu-id="ca063-185">Click **Security**.</span></span> <span data-ttu-id="ca063-186">Si le lien ne s'affiche pas, il est peut-être masqué par le menu **Autres contrôles** situé en bas de l'écran.</span><span class="sxs-lookup"><span data-stu-id="ca063-186">If you don't see the link, it may be hidden under the **More Controls** menu at the bottom of the screen.</span></span>
   
    ![Cliquez sur Sécurité.][10]

9. <span data-ttu-id="ca063-188">Sur la page **Sécurité**, cliquez sur **Configurer l'authentification unique (SSO).**</span><span class="sxs-lookup"><span data-stu-id="ca063-188">On the **Security** page, click **Set up single sign-on (SSO).**</span></span>
   
    ![Cliquez sur Authentification unique.][11]

10. <span data-ttu-id="ca063-190">Modifiez la configuration comme suit :</span><span class="sxs-lookup"><span data-stu-id="ca063-190">Perform the following configuration changes:</span></span>
   
    ![Configurer l’authentification unique][12]
   
    <span data-ttu-id="ca063-192">a.</span><span class="sxs-lookup"><span data-stu-id="ca063-192">a.</span></span> <span data-ttu-id="ca063-193">Sélectionnez **Configurer l'authentification unique avec un fournisseur d'identité tiers**.</span><span class="sxs-lookup"><span data-stu-id="ca063-193">Select **Setup SSO with third-party identity provider**.</span></span>

    <span data-ttu-id="ca063-194">b.</span><span class="sxs-lookup"><span data-stu-id="ca063-194">b.</span></span> <span data-ttu-id="ca063-195">Dans le champ **URL de la page de connexion**, collez la valeur de **l’URL du service d’authentification unique SAML** que vous avez copiée dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ca063-195">In the **Sign-in page URL** field in Google Apps, paste the value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="ca063-196">c.</span><span class="sxs-lookup"><span data-stu-id="ca063-196">c.</span></span> <span data-ttu-id="ca063-197">Dans le champ **URL de la page de connexion** de Google Apps, collez la valeur de **l’URL de déconnexion** que vous avez copiée dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ca063-197">In the **Sign-out page URL** field in Google Apps, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="ca063-198">d.</span><span class="sxs-lookup"><span data-stu-id="ca063-198">d.</span></span> <span data-ttu-id="ca063-199">Dans le champ **Modifier l’URL du mot de passe** de Google Apps, collez la valeur de **Modifier l’URL du mot de passe** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ca063-199">In the **Change password URL** field in Google Apps, paste the value of **Change password URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="ca063-200">e.</span><span class="sxs-lookup"><span data-stu-id="ca063-200">e.</span></span> <span data-ttu-id="ca063-201">Dans Google Apps, chargez le certificat que vous avez téléchargé dans le portail Azure pour le **Certificat de vérification**.</span><span class="sxs-lookup"><span data-stu-id="ca063-201">In Google Apps, for the **Verification certificate**, upload the certificate that you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="ca063-202">f.</span><span class="sxs-lookup"><span data-stu-id="ca063-202">f.</span></span> <span data-ttu-id="ca063-203">Cliquez sur **Enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="ca063-203">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="ca063-204">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="ca063-204">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ca063-205">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="ca063-205">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ca063-206">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ca063-206">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ca063-207">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="ca063-207">Creating an Azure AD test user</span></span>
<span data-ttu-id="ca063-208">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ca063-208">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="ca063-210">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ca063-210">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ca063-211">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ca063-211">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ca063-213">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="ca063-213">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ca063-215">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ca063-215">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ca063-217">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ca063-217">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ca063-219">a.</span><span class="sxs-lookup"><span data-stu-id="ca063-219">a.</span></span> <span data-ttu-id="ca063-220">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ca063-220">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ca063-221">b.</span><span class="sxs-lookup"><span data-stu-id="ca063-221">b.</span></span> <span data-ttu-id="ca063-222">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ca063-222">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ca063-223">c.</span><span class="sxs-lookup"><span data-stu-id="ca063-223">c.</span></span> <span data-ttu-id="ca063-224">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="ca063-224">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ca063-225">d.</span><span class="sxs-lookup"><span data-stu-id="ca063-225">d.</span></span> <span data-ttu-id="ca063-226">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="ca063-226">Click **Create**.</span></span>
 
### <a name="creating-a-google-apps-test-user"></a><span data-ttu-id="ca063-227">Création d’un utilisateur de test Google Apps</span><span class="sxs-lookup"><span data-stu-id="ca063-227">Creating a Google Apps test user</span></span>

<span data-ttu-id="ca063-228">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans le logiciel Google Apps.</span><span class="sxs-lookup"><span data-stu-id="ca063-228">The objective of this section is to create a user called Britta Simon in Google Apps Software.</span></span> <span data-ttu-id="ca063-229">Google Apps prend en charge l’approvisionnement automatique, qui est activé par défaut.</span><span class="sxs-lookup"><span data-stu-id="ca063-229">Google Apps supports auto provisioning, which is by default enabled.</span></span> <span data-ttu-id="ca063-230">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="ca063-230">There is no action for you in this section.</span></span> <span data-ttu-id="ca063-231">Si un utilisateur n’existe pas déjà dans Google Apps, un nouveau est créé lorsque vous tentez d’accéder au logiciel Google Apps.</span><span class="sxs-lookup"><span data-stu-id="ca063-231">If a user doesn't already exist in Google Apps Software, a new one is created when you attempt to access Google Apps Software.</span></span>

>[!NOTE] 
><span data-ttu-id="ca063-232">Si vous devez créer un utilisateur manuellement, contactez [l’équipe de support Google](https://www.google.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="ca063-232">If you need to create a user manually, contact the [Google support team](https://www.google.com/contact/).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ca063-233">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="ca063-233">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ca063-234">Dans cette section, vous autorisez Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Google Apps.</span><span class="sxs-lookup"><span data-stu-id="ca063-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Google Apps.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="ca063-236">**Pour attribuer Britta Simon à Google Apps, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ca063-236">**To assign Britta Simon to Google Apps, perform the following steps:**</span></span>

1. <span data-ttu-id="ca063-237">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ca063-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="ca063-239">Dans la liste des applications, sélectionnez **Google Apps**.</span><span class="sxs-lookup"><span data-stu-id="ca063-239">In the applications list, select **Google Apps**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_app.png) 

3. <span data-ttu-id="ca063-241">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ca063-241">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="ca063-243">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="ca063-243">Click **Add** button.</span></span> <span data-ttu-id="ca063-244">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="ca063-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="ca063-246">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="ca063-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ca063-247">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ca063-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ca063-248">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="ca063-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ca063-249">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="ca063-249">Testing single sign-on</span></span>

<span data-ttu-id="ca063-250">Dans cette section, pour tester vos paramètres d'authentification unique, ouvrez le volet d'accès à l'adresse [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md), puis connectez-vous au compte de test et cliquez sur la vignette **Google Apps**.</span><span class="sxs-lookup"><span data-stu-id="ca063-250">In this section, to test your single sign-on settings, open the Access Panel at [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md), then sign into the test account, and click **Google Apps** tile in the Access Panel.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ca063-251">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="ca063-251">Additional resources</span></span>

* [<span data-ttu-id="ca063-252">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ca063-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ca063-253">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="ca063-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="ca063-254">Configurer l’approvisionnement de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="ca063-254">Configure User Provisioning</span></span>](active-directory-saas-google-apps-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_203.png

[0]: ./media/active-directory-saas-google-apps-tutorial/azure-active-directory.png

[5]: ./media/active-directory-saas-google-apps-tutorial/gapps-added.png
[6]: ./media/active-directory-saas-google-apps-tutorial/config-sso.png
[7]: ./media/active-directory-saas-google-apps-tutorial/sso-gapps.png
[8]: ./media/active-directory-saas-google-apps-tutorial/sso-url.png
[9]: ./media/active-directory-saas-google-apps-tutorial/download-cert.png
[10]: ./media/active-directory-saas-google-apps-tutorial/gapps-security.png
[11]: ./media/active-directory-saas-google-apps-tutorial/security-gapps.png
[12]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-config.png
[13]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-confirm.png
[14]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-email.png
[15]: ./media/active-directory-saas-google-apps-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-tutorial/gapps-api-enabled.png
[17]: ./media/active-directory-saas-google-apps-tutorial/add-custom-domain.png
[18]: ./media/active-directory-saas-google-apps-tutorial/specify-domain.png
[19]: ./media/active-directory-saas-google-apps-tutorial/verify-domain.png
[20]: ./media/active-directory-saas-google-apps-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-another.png
[23]: ./media/active-directory-saas-google-apps-tutorial/apps-gapps.png
[24]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-tutorial/gapps-auth.png
[29]: ./media/active-directory-saas-google-apps-tutorial/assign-users.png
[30]: ./media/active-directory-saas-google-apps-tutorial/assign-confirm.png