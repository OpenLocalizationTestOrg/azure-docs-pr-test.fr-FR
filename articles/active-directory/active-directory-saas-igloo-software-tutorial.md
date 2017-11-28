---
title: "Didacticiel : Intégration d’Azure Active Directory avec Igloo Software | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Igloo Software."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2eb625c1-d3fc-4ae1-a304-6a6733a10e6e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: ab3891e11eb33b4d233e4fc967a40c7df06e4f4e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-igloo-software"></a><span data-ttu-id="6cecb-103">Didacticiel : Intégration d’Azure Active Directory avec Igloo Software</span><span class="sxs-lookup"><span data-stu-id="6cecb-103">Tutorial: Azure Active Directory integration with Igloo Software</span></span>

<span data-ttu-id="6cecb-104">Dans ce didacticiel, vous allez apprendre à intégrer Igloo Software à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6cecb-104">In this tutorial, you learn how to integrate Igloo Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6cecb-105">L’intégration d’Igloo Software à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="6cecb-105">Integrating Igloo Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6cecb-106">Dans Azure AD, vous pouvez contrôler qui a accès à Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="6cecb-106">You can control in Azure AD who has access to Igloo Software</span></span>
- <span data-ttu-id="6cecb-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Igloo Software (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6cecb-107">You can enable your users to automatically get signed-on to Igloo Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6cecb-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="6cecb-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6cecb-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6cecb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6cecb-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6cecb-110">Prerequisites</span></span>

<span data-ttu-id="6cecb-111">Pour configurer l’intégration d’Azure AD à Igloo Software, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="6cecb-111">To configure Azure AD integration with Igloo Software, you need the following items:</span></span>

- <span data-ttu-id="6cecb-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="6cecb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6cecb-113">Un abonnement Igloo Software pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="6cecb-113">An Igloo Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6cecb-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="6cecb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6cecb-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="6cecb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6cecb-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="6cecb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6cecb-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6cecb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6cecb-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="6cecb-118">Scenario description</span></span>
<span data-ttu-id="6cecb-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="6cecb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6cecb-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="6cecb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6cecb-121">Ajout d’Igloo Software à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="6cecb-121">Adding Igloo Software from the gallery</span></span>
2. <span data-ttu-id="6cecb-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="6cecb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-igloo-software-from-the-gallery"></a><span data-ttu-id="6cecb-123">Ajout d’Igloo Software à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="6cecb-123">Adding Igloo Software from the gallery</span></span>
<span data-ttu-id="6cecb-124">Pour configurer l’intégration d’Igloo Software à Azure AD, vous devez ajouter Igloo Software à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="6cecb-124">To configure the integration of Igloo Software into Azure AD, you need to add Igloo Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6cecb-125">**Pour ajouter Igloo Software à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6cecb-125">**To add Igloo Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6cecb-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6cecb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6cecb-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="6cecb-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6cecb-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="6cecb-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="6cecb-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="6cecb-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="6cecb-133">Dans la zone de recherche, tapez **Igloo Software**.</span><span class="sxs-lookup"><span data-stu-id="6cecb-133">In the search box, type **Igloo Software**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_search.png)

5. <span data-ttu-id="6cecb-135">Dans le panneau de résultats, sélectionnez **Igloo Software**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="6cecb-135">In the results panel, select **Igloo Software**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6cecb-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="6cecb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6cecb-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Igloo Software à l’aide d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="6cecb-138">In this section, you configure and test Azure AD single sign-on with Igloo Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6cecb-139">Pour que l’authentification unique fonctionne, Azure AD a besoin de savoir qui est l’utilisateur Igloo Software équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6cecb-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Igloo Software is to a user in Azure AD.</span></span> <span data-ttu-id="6cecb-140">En d’autres termes, un lien entre un utilisateur Azure AD et l’utilisateur Igloo Software associé doit être établi.</span><span class="sxs-lookup"><span data-stu-id="6cecb-140">In other words, a link relationship between an Azure AD user and the related user in Igloo Software needs to be established.</span></span>

<span data-ttu-id="6cecb-141">Dans Igloo Software, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="6cecb-141">In Igloo Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6cecb-142">Pour configurer et tester l’authentification unique Azure AD avec Igloo Software, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="6cecb-142">To configure and test Azure AD single sign-on with Igloo Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6cecb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="6cecb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6cecb-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6cecb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6cecb-145">**[Création d’un utilisateur de test Igloo Software](#creating-an-igloo-software-test-user)** pour avoir un équivalent de Britta Simon dans Igloo Software lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6cecb-145">**[Creating an Igloo Software test user](#creating-an-igloo-software-test-user)** - to have a counterpart of Britta Simon in Igloo Software that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6cecb-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6cecb-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6cecb-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="6cecb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6cecb-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="6cecb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6cecb-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="6cecb-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Igloo Software application.</span></span>

<span data-ttu-id="6cecb-150">**Pour configurer l’authentification unique Azure AD avec Igloo Software, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6cecb-150">**To configure Azure AD single sign-on with Igloo Software, perform the following steps:**</span></span>

1. <span data-ttu-id="6cecb-151">Dans le portail Azure, sur la page d’intégration de l’application **Igloo Software**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="6cecb-151">In the Azure portal, on the **Igloo Software** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="6cecb-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="6cecb-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_samlbase.png)

3. <span data-ttu-id="6cecb-155">Dans la section **Igloo Software Domain and URLs** (Domaine et URL Igloo Software), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6cecb-155">On the **Igloo Software Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_url.png)
    
    <span data-ttu-id="6cecb-157">a.</span><span class="sxs-lookup"><span data-stu-id="6cecb-157">a.</span></span> <span data-ttu-id="6cecb-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<company name>.igloocommmunities.com`</span><span class="sxs-lookup"><span data-stu-id="6cecb-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.igloocommmunities.com`</span></span>

    <span data-ttu-id="6cecb-159">b.</span><span class="sxs-lookup"><span data-stu-id="6cecb-159">b.</span></span> <span data-ttu-id="6cecb-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<company name>.igloocommmunities.com/saml.digest`</span><span class="sxs-lookup"><span data-stu-id="6cecb-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span></span>

    <span data-ttu-id="6cecb-161">c.</span><span class="sxs-lookup"><span data-stu-id="6cecb-161">c.</span></span> <span data-ttu-id="6cecb-162">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<company name>.igloocommmunities.com/saml.digest`</span><span class="sxs-lookup"><span data-stu-id="6cecb-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6cecb-163">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="6cecb-163">These values are not real.</span></span> <span data-ttu-id="6cecb-164">Mettez à jour ces valeurs avec l’identificateur, l’URL de réponse et l’URL de connexion réels.</span><span class="sxs-lookup"><span data-stu-id="6cecb-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="6cecb-165">Pour obtenir ces valeurs, contactez [l’équipe de support technique Igloo Software](https://www.igloosoftware.com/services/support).</span><span class="sxs-lookup"><span data-stu-id="6cecb-165">Contact [Igloo Software Client support team](https://www.igloosoftware.com/services/support) to get these values.</span></span> 

4. <span data-ttu-id="6cecb-166">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="6cecb-166">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_certificate.png) 

5. <span data-ttu-id="6cecb-168">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="6cecb-168">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-igloo-software-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="6cecb-170">Dans la section **Igloo Software Configuration** (Configuration d’Igloo Software), cliquez sur **Configure Igloo Software** (Configurer Igloo Software) pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="6cecb-170">On the **Igloo Software Configuration** section, click **Configure Igloo Software** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6cecb-171">Copiez **l’URL de déconnexion et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="6cecb-171">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_configure.png) 

7. <span data-ttu-id="6cecb-173">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Igloo Software en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="6cecb-173">In a different web browser window, log in to your Igloo Software company site as an administrator.</span></span>

8. <span data-ttu-id="6cecb-174">Accédez à **Control panel**.</span><span class="sxs-lookup"><span data-stu-id="6cecb-174">Go to the **Control Panel**.</span></span>
   
     <span data-ttu-id="6cecb-175">![Control Panel (Panneau de configuration)](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Control Panel (Panneau de configuration)")</span><span class="sxs-lookup"><span data-stu-id="6cecb-175">![Control Panel](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Control Panel")</span></span>

9. <span data-ttu-id="6cecb-176">Sous l’onglet **Membership** (Appartenance), cliquez sur **Paramètres de connexion**.</span><span class="sxs-lookup"><span data-stu-id="6cecb-176">In the **Membership** tab, click **Sign In Settings**.</span></span>
   
    <span data-ttu-id="6cecb-177">![Sign in Settings (Paramètres de connexion)](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "Sign in Settings (Paramètres de connexion)")</span><span class="sxs-lookup"><span data-stu-id="6cecb-177">![Sign in Settings](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "Sign in Settings")</span></span>

10. <span data-ttu-id="6cecb-178">Dans la section SAML Configuration, cliquez sur **Configure SAML Authentication**.</span><span class="sxs-lookup"><span data-stu-id="6cecb-178">In the SAML Configuration section, click **Configure SAML Authentication**.</span></span>
   
    <span data-ttu-id="6cecb-179">![Configuration SAML](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "Configuration SAML")</span><span class="sxs-lookup"><span data-stu-id="6cecb-179">![SAML Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "SAML Configuration")</span></span>
   
11. <span data-ttu-id="6cecb-180">Dans la section **General Configuration** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6cecb-180">In the **General Configuration** section, perform the following steps:</span></span>
   
    <span data-ttu-id="6cecb-181">![General Configuration (Configuration générale)](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "General Configuration (Configuration générale)")</span><span class="sxs-lookup"><span data-stu-id="6cecb-181">![General Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "General Configuration")</span></span>

    <span data-ttu-id="6cecb-182">a.</span><span class="sxs-lookup"><span data-stu-id="6cecb-182">a.</span></span> <span data-ttu-id="6cecb-183">Dans la zone de texte **Connection Name** , entrez un nom personnalisé pour votre configuration.</span><span class="sxs-lookup"><span data-stu-id="6cecb-183">In the **Connection Name** textbox, type a custom name for your configuration.</span></span>
   
    <span data-ttu-id="6cecb-184">b.</span><span class="sxs-lookup"><span data-stu-id="6cecb-184">b.</span></span> <span data-ttu-id="6cecb-185">Dans la zone de texte **IdP Login URL** (URL de connexion de fournisseur d’identité), collez la valeur de **l’URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6cecb-185">In the **IdP Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="6cecb-186">c.</span><span class="sxs-lookup"><span data-stu-id="6cecb-186">c.</span></span> <span data-ttu-id="6cecb-187">Dans la zone de texte **IdP Logout URL** (URL de déconnexion de fournisseur d’identité), collez la valeur de **l’URL de déconnexion** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6cecb-187">In the **IdP Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="6cecb-188">d.</span><span class="sxs-lookup"><span data-stu-id="6cecb-188">d.</span></span> <span data-ttu-id="6cecb-189">Pour **Logout Response and Request HTTP Type** (Type de réponse de déconnexion et de requête HTTP), sélectionnez **POST**.</span><span class="sxs-lookup"><span data-stu-id="6cecb-189">Select **Logout Response and Request HTTP Type** as **POST**.</span></span>
   
    <span data-ttu-id="6cecb-190">e.</span><span class="sxs-lookup"><span data-stu-id="6cecb-190">e.</span></span> <span data-ttu-id="6cecb-191">Ouvrez dans le Bloc-notes votre certificat codé en **base 64** téléchargé à partir du portail Azure, copiez son contenu dans le Presse-papiers, puis collez-le dans la zone de texte **Certificat public**.</span><span class="sxs-lookup"><span data-stu-id="6cecb-191">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **Public Certificate** textbox.</span></span>
    
12. <span data-ttu-id="6cecb-192">Dans **Response and Authentication Configuration**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6cecb-192">In the **Response and Authentication Configuration**, perform the following steps:</span></span>
    
    <span data-ttu-id="6cecb-193">![Response and Authentication Configuration (Configuration de la réponse et de l’authentification)](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "Response and Authentication Configuration (Configuration de la réponse et de l’authentification)")</span><span class="sxs-lookup"><span data-stu-id="6cecb-193">![Response and Authentication Configuration](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "Response and Authentication Configuration")</span></span>
  
      <span data-ttu-id="6cecb-194">a.</span><span class="sxs-lookup"><span data-stu-id="6cecb-194">a.</span></span> <span data-ttu-id="6cecb-195">Pour **Fournisseur d’identité**, sélectionnez **Microsoft ADFS**.</span><span class="sxs-lookup"><span data-stu-id="6cecb-195">As **Identity Provider**, select **Microsoft ADFS**.</span></span>
      
      <span data-ttu-id="6cecb-196">b.</span><span class="sxs-lookup"><span data-stu-id="6cecb-196">b.</span></span> <span data-ttu-id="6cecb-197">Pour **Type d’identificateur**, sélectionnez **Adresse de messagerie**.</span><span class="sxs-lookup"><span data-stu-id="6cecb-197">As **Identifier Type**, select **Email Address**.</span></span> 

      <span data-ttu-id="6cecb-198">c.</span><span class="sxs-lookup"><span data-stu-id="6cecb-198">c.</span></span> <span data-ttu-id="6cecb-199">Dans la zone de texte **Email Attribute**, entrez **emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="6cecb-199">In the **Email Attribute** textbox, type **emailaddress**.</span></span>

      <span data-ttu-id="6cecb-200">d.</span><span class="sxs-lookup"><span data-stu-id="6cecb-200">d.</span></span> <span data-ttu-id="6cecb-201">Dans la zone de texte **Attribut de prénom**, saisissez **givenname**.</span><span class="sxs-lookup"><span data-stu-id="6cecb-201">In the **First Name Attribute** textbox, type **givenname**.</span></span>

      <span data-ttu-id="6cecb-202">e.</span><span class="sxs-lookup"><span data-stu-id="6cecb-202">e.</span></span> <span data-ttu-id="6cecb-203">Dans la zone de texte **Attribut de nom**, saisissez **surname**.</span><span class="sxs-lookup"><span data-stu-id="6cecb-203">In the **Last Name Attribute** textbox, type **surname**.</span></span>

13. <span data-ttu-id="6cecb-204">Pour terminer la configuration, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6cecb-204">Perform the following steps to complete the configuration:</span></span>
    
    <span data-ttu-id="6cecb-205">![Création d’utilisateurs à l’authentification](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "Création d’utilisateurs à l’authentification")</span><span class="sxs-lookup"><span data-stu-id="6cecb-205">![User creation on Sign in](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "User creation on Sign in")</span></span> 

     <span data-ttu-id="6cecb-206">a.</span><span class="sxs-lookup"><span data-stu-id="6cecb-206">a.</span></span> <span data-ttu-id="6cecb-207">Pour **Création d’utilisateurs à l’authentification**, sélectionnez **Create a new user in your site when they sign in** (Créer un nouvel utilisateur sur votre site au moment de la connexion).</span><span class="sxs-lookup"><span data-stu-id="6cecb-207">As **User creation on Sign in**, select **Create a new user in your site when they sign in**.</span></span>

     <span data-ttu-id="6cecb-208">b.</span><span class="sxs-lookup"><span data-stu-id="6cecb-208">b.</span></span> <span data-ttu-id="6cecb-209">Pour **Paramètres de connexion**, sélectionnez **Use SAML button on “Sign in” screen** (Utiliser le bouton SAML sur l’écran de connexion).</span><span class="sxs-lookup"><span data-stu-id="6cecb-209">As **Sign in Settings**, select **Use SAML button on “Sign in” screen**.</span></span>

     <span data-ttu-id="6cecb-210">c.</span><span class="sxs-lookup"><span data-stu-id="6cecb-210">c.</span></span> <span data-ttu-id="6cecb-211">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="6cecb-211">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="6cecb-212">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="6cecb-212">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6cecb-213">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="6cecb-213">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6cecb-214">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6cecb-214">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6cecb-215">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="6cecb-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="6cecb-216">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6cecb-216">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="6cecb-218">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6cecb-218">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6cecb-219">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6cecb-219">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6cecb-221">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="6cecb-221">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6cecb-223">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="6cecb-223">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6cecb-225">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6cecb-225">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6cecb-227">a.</span><span class="sxs-lookup"><span data-stu-id="6cecb-227">a.</span></span> <span data-ttu-id="6cecb-228">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6cecb-228">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6cecb-229">b.</span><span class="sxs-lookup"><span data-stu-id="6cecb-229">b.</span></span> <span data-ttu-id="6cecb-230">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6cecb-230">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6cecb-231">c.</span><span class="sxs-lookup"><span data-stu-id="6cecb-231">c.</span></span> <span data-ttu-id="6cecb-232">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="6cecb-232">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6cecb-233">d.</span><span class="sxs-lookup"><span data-stu-id="6cecb-233">d.</span></span> <span data-ttu-id="6cecb-234">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="6cecb-234">Click **Create**.</span></span>
 
### <a name="creating-an-igloo-software-test-user"></a><span data-ttu-id="6cecb-235">Création d’un utilisateur de test Igloo Software</span><span class="sxs-lookup"><span data-stu-id="6cecb-235">Creating an Igloo Software test user</span></span>

<span data-ttu-id="6cecb-236">Aucun élément d’action ne vous permet de configurer l’approvisionnement des utilisateurs dans Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="6cecb-236">There is no action item for you to configure user provisioning to Igloo Software.</span></span>  

<span data-ttu-id="6cecb-237">Lorsqu’un utilisateur assigné tente de se connecter à Igloo Software à l’aide du panneau d’accès, Igloo Software vérifie si cet utilisateur existe.</span><span class="sxs-lookup"><span data-stu-id="6cecb-237">When an assigned user tries to log in to Igloo Software using the access panel, Igloo Software checks whether the user exists.</span></span>  <span data-ttu-id="6cecb-238">Si aucun compte d’utilisateur n’est disponible, Igloo Software le crée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="6cecb-238">If there is no user account available yet, it is automatically created by Igloo Software.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6cecb-239">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="6cecb-239">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6cecb-240">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="6cecb-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Igloo Software.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="6cecb-242">**Pour attribuer Britta Simon à Igloo Software, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6cecb-242">**To assign Britta Simon to Igloo Software, perform the following steps:**</span></span>

1. <span data-ttu-id="6cecb-243">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="6cecb-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="6cecb-245">Dans la liste des applications, sélectionnez **Igloo Software**.</span><span class="sxs-lookup"><span data-stu-id="6cecb-245">In the applications list, select **Igloo Software**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_app.png) 

3. <span data-ttu-id="6cecb-247">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="6cecb-247">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="6cecb-249">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="6cecb-249">Click **Add** button.</span></span> <span data-ttu-id="6cecb-250">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="6cecb-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="6cecb-252">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="6cecb-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6cecb-253">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="6cecb-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6cecb-254">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="6cecb-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6cecb-255">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="6cecb-255">Testing single sign-on</span></span>

<span data-ttu-id="6cecb-256">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="6cecb-256">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6cecb-257">Lorsque vous cliquez sur la vignette Igloo Software dans le panneau d’accès, vous devez être connecté automatiquement à votre application Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="6cecb-257">When you click the Igloo Software tile in the Access Panel, you should get automatically signed-on to your Igloo Software application.</span></span>
<span data-ttu-id="6cecb-258">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6cecb-258">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6cecb-259">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="6cecb-259">Additional resources</span></span>

* [<span data-ttu-id="6cecb-260">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6cecb-260">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6cecb-261">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="6cecb-261">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_203.png

