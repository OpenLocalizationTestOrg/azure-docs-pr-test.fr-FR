---
title: "Didacticiel : Intégration d’Azure Active Directory à Nexonia | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Nexonia."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a93b771a-9bc3-444a-bdc0-457f8bb7e780
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/1/2017
ms.author: jeedes
ms.openlocfilehash: 1370fa64c2ddc25d3121c567ceea4828b1e50921
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-nexonia"></a><span data-ttu-id="a852d-103">Didacticiel : Intégration d’Azure Active Directory à Nexonia</span><span class="sxs-lookup"><span data-stu-id="a852d-103">Tutorial: Azure Active Directory integration with Nexonia</span></span>

<span data-ttu-id="a852d-104">Dans ce didacticiel, vous allez apprendre à intégrer Azure Active Directory (Azure AD) dans Nexonia.</span><span class="sxs-lookup"><span data-stu-id="a852d-104">In this tutorial, you learn how to integrate Nexonia with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a852d-105">L’intégration de Nexonia dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="a852d-105">Integrating Nexonia with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a852d-106">Dans Azure AD, vous pouvez contrôler qui a accès à Nexonia</span><span class="sxs-lookup"><span data-stu-id="a852d-106">You can control in Azure AD who has access to Nexonia</span></span>
- <span data-ttu-id="a852d-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Nexonia (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="a852d-107">You can enable your users to automatically get signed-on to Nexonia (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a852d-108">Vous pouvez gérer vos comptes depuis un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="a852d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a852d-109">Pour en savoir plus sur l’intégration de l’application SaaS avec Azure AD, consultez</span><span class="sxs-lookup"><span data-stu-id="a852d-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="a852d-110">[Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a852d-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a852d-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a852d-111">Prerequisites</span></span>

<span data-ttu-id="a852d-112">Pour configurer l’intégration d’Azure AD à Nexonia, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a852d-112">To configure Azure AD integration with Nexonia, you need the following items:</span></span>

- <span data-ttu-id="a852d-113">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="a852d-113">An Azure AD subscription</span></span>
- <span data-ttu-id="a852d-114">Un abonnement Nexonia avec authentification unique activée</span><span class="sxs-lookup"><span data-stu-id="a852d-114">A Nexonia single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a852d-115">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="a852d-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a852d-116">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="a852d-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a852d-117">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="a852d-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a852d-118">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a852d-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a852d-119">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="a852d-119">Scenario description</span></span>
<span data-ttu-id="a852d-120">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="a852d-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a852d-121">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="a852d-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a852d-122">Ajout de Nexonia à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="a852d-122">Adding Nexonia from the gallery</span></span>
2. <span data-ttu-id="a852d-123">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a852d-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-nexonia-from-the-gallery"></a><span data-ttu-id="a852d-124">Ajout de Nexonia à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="a852d-124">Adding Nexonia from the gallery</span></span>
<span data-ttu-id="a852d-125">Pour configurer l’intégration de Nexonia à Azure AD, vous devez ajouter Nexonia à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="a852d-125">To configure the integration of Nexonia into Azure AD, you need to add Nexonia from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a852d-126">**Pour ajouter Nexonia à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a852d-126">**To add Nexonia from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a852d-127">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a852d-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a852d-129">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="a852d-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a852d-130">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a852d-130">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="a852d-132">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a852d-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="a852d-134">Dans la zone de recherche, tapez **Nexonia**.</span><span class="sxs-lookup"><span data-stu-id="a852d-134">In the search box, type **Nexonia**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_search.png)

5. <span data-ttu-id="a852d-136">Dans le panneau des résultats, sélectionnez **Nexonia**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="a852d-136">In the results panel, select **Nexonia**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a852d-138">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a852d-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a852d-139">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Nexonia, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="a852d-139">In this section, you configure and test Azure AD single sign-on with Nexonia based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a852d-140">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Nexonia équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a852d-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Nexonia is to a user in Azure AD.</span></span> <span data-ttu-id="a852d-141">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Nexonia associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="a852d-141">In other words, a link relationship between an Azure AD user and the related user in Nexonia needs to be established.</span></span>

<span data-ttu-id="a852d-142">Dans Nexonia, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="a852d-142">In Nexonia, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a852d-143">Pour configurer et tester l’authentification unique Azure AD avec Nexonia, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="a852d-143">To configure and test Azure AD single sign-on with Nexonia, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a852d-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="a852d-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a852d-145">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a852d-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a852d-146">**[Création d’un utilisateur de test Nexonia](#creating-a-nexonia-test-user)** pour avoir un équivalent de Britta Simon dans Nexonia lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a852d-146">**[Creating a Nexonia test user](#creating-a-nexonia-test-user)** - to have a counterpart of Britta Simon in Nexonia that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a852d-147">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a852d-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a852d-148">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="a852d-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a852d-149">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a852d-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a852d-150">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Nexonia.</span><span class="sxs-lookup"><span data-stu-id="a852d-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Nexonia application.</span></span>

>[!Note]
><span data-ttu-id="a852d-151">Si vous rencontrez des problèmes d’intégration, consultez ce [lien](https://docs.microsoft.com/azure/active-directory/application-sign-in-problem-federated-sso-gallery?WT.mc_id=UI_AAD_Enterprise_Apps_SupportOrTroubleshooting) pour trouver une solution de dépannage.</span><span class="sxs-lookup"><span data-stu-id="a852d-151">If you have issues in the integration then refer this [link](https://docs.microsoft.com/azure/active-directory/application-sign-in-problem-federated-sso-gallery?WT.mc_id=UI_AAD_Enterprise_Apps_SupportOrTroubleshooting) for troubleshooting guide.</span></span> <span data-ttu-id="a852d-152">Si vous ne trouvez toujours pas de solution, soumettez une demande de support à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a852d-152">If you still have not found the solution, then raise the support request from Azure portal.</span></span>

<span data-ttu-id="a852d-153">**Pour configurer l’authentification unique Azure AD avec Nexonia, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a852d-153">**To configure Azure AD single sign-on with Nexonia, perform the following steps:**</span></span>

1. <span data-ttu-id="a852d-154">Dans le portail Azure, sur la page d’intégration de l’application **Nexonia**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="a852d-154">In the Azure portal, on the **Nexonia** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="a852d-156">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="a852d-156">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_samlbase.png)

3. <span data-ttu-id="a852d-158">Dans la section **Domaine et URL Nexonia**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="a852d-158">On the **Nexonia Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_url.png)

    <span data-ttu-id="a852d-160">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://system.nexonia.com/assistant/saml.do?orgCode=<organizationcode>`</span><span class="sxs-lookup"><span data-stu-id="a852d-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://system.nexonia.com/assistant/saml.do?orgCode=<organizationcode>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a852d-161">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="a852d-161">This value is not real.</span></span> <span data-ttu-id="a852d-162">Mettez à jour la valeur avec l’URL de réponse réelle.</span><span class="sxs-lookup"><span data-stu-id="a852d-162">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="a852d-163">Contactez [l’équipe de support technique de Nexonia](https://nexonia.zendesk.com/hc/requests/new) pour obtenir cette valeur.</span><span class="sxs-lookup"><span data-stu-id="a852d-163">Contact [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) to get this value.</span></span> 


4. <span data-ttu-id="a852d-164">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="a852d-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_certificate.png) 

5. <span data-ttu-id="a852d-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="a852d-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-nexonia-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a852d-168">Dans la section **Configuration de Nexonia**, cliquez sur **Configurer Nexonia** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="a852d-168">On the **Nexonia Configuration** section, click **Configure Nexonia** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a852d-169">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="a852d-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_configure.png) 

7. <span data-ttu-id="a852d-171">Pour obtenir la configuration de l’authentification unique pour votre application, contactez [l’équipe de support Nexonia](https://nexonia.zendesk.com/hc/requests/new) et fournissez-lui les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a852d-171">To get SSO configured for your application, contact [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) and provide them with the following:</span></span>

    <span data-ttu-id="a852d-172">• Le **certificat**</span><span class="sxs-lookup"><span data-stu-id="a852d-172">• The downloaded **certificate**</span></span>

    <span data-ttu-id="a852d-173">• **L’ID d’entité SAML**</span><span class="sxs-lookup"><span data-stu-id="a852d-173">• The **SAML Entity ID**</span></span>

    <span data-ttu-id="a852d-174">• **L’URL du service d’authentification unique SAML**</span><span class="sxs-lookup"><span data-stu-id="a852d-174">• The **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="a852d-175">• **L’URL de déconnexion**</span><span class="sxs-lookup"><span data-stu-id="a852d-175">• The **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="a852d-176">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="a852d-176">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a852d-177">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="a852d-177">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a852d-178">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a852d-178">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a852d-179">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="a852d-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="a852d-180">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a852d-180">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="a852d-182">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a852d-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a852d-183">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a852d-183">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-nexonia-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a852d-185">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="a852d-185">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-nexonia-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a852d-187">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a852d-187">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-nexonia-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a852d-189">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="a852d-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-nexonia-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a852d-191">a.</span><span class="sxs-lookup"><span data-stu-id="a852d-191">a.</span></span> <span data-ttu-id="a852d-192">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a852d-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a852d-193">b.</span><span class="sxs-lookup"><span data-stu-id="a852d-193">b.</span></span> <span data-ttu-id="a852d-194">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a852d-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a852d-195">c.</span><span class="sxs-lookup"><span data-stu-id="a852d-195">c.</span></span> <span data-ttu-id="a852d-196">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="a852d-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a852d-197">d.</span><span class="sxs-lookup"><span data-stu-id="a852d-197">d.</span></span> <span data-ttu-id="a852d-198">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="a852d-198">Click **Create**.</span></span>
 
### <a name="creating-a-nexonia-test-user"></a><span data-ttu-id="a852d-199">Création d’un utilisateur de test Nexonia</span><span class="sxs-lookup"><span data-stu-id="a852d-199">Creating a Nexonia test user</span></span>

<span data-ttu-id="a852d-200">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Nexonia.</span><span class="sxs-lookup"><span data-stu-id="a852d-200">In this section, you create a user called Britta Simon in Nexonia.</span></span> <span data-ttu-id="a852d-201">Collaborez avec [l’équipe du support technique Nexonia](https://nexonia.zendesk.com/hc/requests/new) pour ajouter des utilisateurs dans la plateforme Nexonia.</span><span class="sxs-lookup"><span data-stu-id="a852d-201">Work with [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) to add the users in the Nexonia platform.</span></span> <span data-ttu-id="a852d-202">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="a852d-202">Users must be created and activated before you use single sign-on.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a852d-203">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="a852d-203">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a852d-204">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Nexonia.</span><span class="sxs-lookup"><span data-stu-id="a852d-204">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Nexonia.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="a852d-206">**Pour affecter Britta Simon à Nexonia, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a852d-206">**To assign Britta Simon to Nexonia, perform the following steps:**</span></span>

1. <span data-ttu-id="a852d-207">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a852d-207">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="a852d-209">Dans la liste des applications, sélectionnez **Nexonia**.</span><span class="sxs-lookup"><span data-stu-id="a852d-209">In the applications list, select **Nexonia**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_app.png) 

3. <span data-ttu-id="a852d-211">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a852d-211">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="a852d-213">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="a852d-213">Click **Add** button.</span></span> <span data-ttu-id="a852d-214">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a852d-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="a852d-216">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="a852d-216">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a852d-217">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a852d-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a852d-218">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a852d-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a852d-219">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="a852d-219">Testing single sign-on</span></span>

<span data-ttu-id="a852d-220">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="a852d-220">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a852d-221">Lorsque vous cliquez sur la vignette Nexonia dans le volet d’accès, vous devez être connecté automatiquement à votre application Nexonia.</span><span class="sxs-lookup"><span data-stu-id="a852d-221">When you click the Nexonia tile in the Access Panel, you should get automatically signed-on to your Nexonia application.</span></span>
<span data-ttu-id="a852d-222">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="a852d-222">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a852d-223">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="a852d-223">Additional resources</span></span>

* [<span data-ttu-id="a852d-224">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a852d-224">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a852d-225">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="a852d-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_203.png

