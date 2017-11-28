---
title: "Didacticiel : Intégration d’Azure Active Directory à Zscaler | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Zscaler."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 68c453f7-aff1-4614-92d3-9b86f3ad99dc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 73c81691b68ee820e1d905a17b4f2ab6b6ceb5fd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler"></a><span data-ttu-id="2f145-103">Didacticiel : Intégration d’Azure AD à Zscaler</span><span class="sxs-lookup"><span data-stu-id="2f145-103">Tutorial: Azure Active Directory integration with Zscaler</span></span>

<span data-ttu-id="2f145-104">L’objectif de ce didacticiel est de montrer comment intégrer Zscaler à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2f145-104">In this tutorial, you learn how to integrate Zscaler with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2f145-105">Intégrer Zscaler à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="2f145-105">Integrating Zscaler with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2f145-106">Dans Azure AD, vous pouvez contrôler l’accès à Zscaler.</span><span class="sxs-lookup"><span data-stu-id="2f145-106">You can control in Azure AD who has access to Zscaler</span></span>
- <span data-ttu-id="2f145-107">Vous pouvez autoriser les utilisateurs à être automatiquement connectés à Zscaler (via l’authentification unique) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f145-107">You can enable your users to automatically get signed-on to Zscaler (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2f145-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="2f145-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2f145-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2f145-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f145-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="2f145-110">Prerequisites</span></span>

<span data-ttu-id="2f145-111">Pour configurer l’intégration d’Azure AD à Zscaler, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2f145-111">To configure Azure AD integration with Zscaler, you need the following items:</span></span>

- <span data-ttu-id="2f145-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f145-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2f145-113">Un abonnement Zscaler pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="2f145-113">A Zscaler single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2f145-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="2f145-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2f145-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="2f145-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2f145-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="2f145-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2f145-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2f145-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2f145-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="2f145-118">Scenario description</span></span>
<span data-ttu-id="2f145-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="2f145-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2f145-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="2f145-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2f145-121">Ajouter Zscaler à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="2f145-121">Adding Zscaler from the gallery</span></span>
2. <span data-ttu-id="2f145-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f145-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-from-the-gallery"></a><span data-ttu-id="2f145-123">Ajouter Zscaler à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="2f145-123">Adding Zscaler from the gallery</span></span>
<span data-ttu-id="2f145-124">Pour configurer l’intégration de Zscaler à Azure AD, vous devez ajouter Zscaler, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="2f145-124">To configure the integration of Zscaler into Azure AD, you need to add Zscaler from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2f145-125">**Pour ajouter Zscaler à partir de la galerie, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="2f145-125">**To add Zscaler from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2f145-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2f145-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2f145-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="2f145-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2f145-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="2f145-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="2f145-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="2f145-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="2f145-133">Dans la zone de recherche, tapez **Zscaler**.</span><span class="sxs-lookup"><span data-stu-id="2f145-133">In the search box, type **Zscaler**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_search.png)

5. <span data-ttu-id="2f145-135">Dans le panneau de résultats, sélectionnez **Zscaler**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="2f145-135">In the results panel, select **Zscaler**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2f145-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f145-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2f145-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Zscaler grâce à un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="2f145-138">In this section, you configure and test Azure AD single sign-on with Zscaler based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2f145-139">Pour que l’authentification unique fonctionne, Azure AD doit connaître l’utilisateur Zscaler correspondant à l’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f145-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler is to a user in Azure AD.</span></span> <span data-ttu-id="2f145-140">En d’autres termes, il faut établir une relation entre l’utilisateur Azure AD et l’utilisateur Zscaler qui lui est associé.</span><span class="sxs-lookup"><span data-stu-id="2f145-140">In other words, a link relationship between an Azure AD user and the related user in Zscaler needs to be established.</span></span>

<span data-ttu-id="2f145-141">Dans Zscaler, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="2f145-141">In Zscaler, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2f145-142">Pour configurer et tester l’authentification unique Azure AD avec Zscaler, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="2f145-142">To configure and test Azure AD single sign-on with Zscaler, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2f145-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="2f145-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2f145-144">**[Configuration des paramètres de proxy](#configuring-proxy-settings)** pour configurer les paramètres de proxy dans Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="2f145-144">**[Configuring proxy settings](#configuring-proxy-settings)** - to configure the proxy settings in Internet Explorer</span></span>
3. <span data-ttu-id="2f145-145">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2f145-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="2f145-146">**[Création d’un utilisateur de test Zscaler](#creating-a-zscaler-test-user)** pour avoir un équivalent de Britta Simon dans Zscaler qui est lié à la représentation de l’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f145-146">**[Creating a Zscaler test user](#creating-a-zscaler-test-user)** - to have a counterpart of Britta Simon in Zscaler that is linked to the Azure AD representation of user.</span></span>
5. <span data-ttu-id="2f145-147">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f145-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
6. <span data-ttu-id="2f145-148">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="2f145-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2f145-149">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f145-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2f145-150">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Zscaler.</span><span class="sxs-lookup"><span data-stu-id="2f145-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zscaler application.</span></span>

<span data-ttu-id="2f145-151">**Pour configurer l’authentification unique Azure AD avec Zscaler, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="2f145-151">**To configure Azure AD single sign-on with Zscaler, perform the following steps:**</span></span>

1. <span data-ttu-id="2f145-152">Dans le portail Azure, dans la page d’intégration de l’application **Zscaler**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="2f145-152">In the Azure portal, on the **Zscaler** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="2f145-154">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="2f145-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_samlbase.png)

3. <span data-ttu-id="2f145-156">Dans la section **Domaine et URL Zscaler**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="2f145-156">On the **Zscaler Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_url.png)

    <span data-ttu-id="2f145-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<companyname>.zsclaer.net`</span><span class="sxs-lookup"><span data-stu-id="2f145-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.zsclaer.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2f145-159">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="2f145-159">This value is not real.</span></span> <span data-ttu-id="2f145-160">Mettez à jour cette valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="2f145-160">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="2f145-161">Pour obtenir cette valeur, contactez [l’équipe du support Zscaler](https://www.zscaler.com/company/contact).</span><span class="sxs-lookup"><span data-stu-id="2f145-161">Contact [Zscaler Client support team](https://www.zscaler.com/company/contact) to get this value.</span></span> 

4. <span data-ttu-id="2f145-162">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="2f145-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_certificate.png) 

5. <span data-ttu-id="2f145-164">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="2f145-164">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-zscaler-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2f145-166">Pour ouvrir la fenêtre **Configurer l’authentification**, dans la section **Configuration de Zscaler**, cliquez sur **Configurer Zscaler**.</span><span class="sxs-lookup"><span data-stu-id="2f145-166">On the **Zscaler Configuration** section, click **Configure Zscaler** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2f145-167">Copiez l**’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="2f145-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_configure.png) 

7. <span data-ttu-id="2f145-169">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Zscaler en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="2f145-169">In a different web browser window, log in to your ZScaler company site as an administrator.</span></span>

8. <span data-ttu-id="2f145-170">Dans le menu situé dans la partie supérieure, cliquez sur **Administration**.</span><span class="sxs-lookup"><span data-stu-id="2f145-170">In the menu on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="2f145-171">![Administration](./media/active-directory-saas-zscaler-tutorial/ic800206.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="2f145-171">![Administration](./media/active-directory-saas-zscaler-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="2f145-172">Sous **Manage Administrators & Roles**, cliquez sur **Manage Users & Authentication**.</span><span class="sxs-lookup"><span data-stu-id="2f145-172">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="2f145-173">![Gérer les utilisateurs et l’authentification](./media/active-directory-saas-zscaler-tutorial/ic800207.png "Gérer les utilisateurs et l’authentification")</span><span class="sxs-lookup"><span data-stu-id="2f145-173">![Manage Users & Authentication](./media/active-directory-saas-zscaler-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="2f145-174">Dans la section **Choose Authentication Options for your Organization** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2f145-174">In the **Choose Authentication Options for your Organization** section, perform the following steps:</span></span>   
                
    <span data-ttu-id="2f145-175">![Authentication](./media/active-directory-saas-zscaler-tutorial/ic800208.png "Authentication")</span><span class="sxs-lookup"><span data-stu-id="2f145-175">![Authentication](./media/active-directory-saas-zscaler-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="2f145-176">a.</span><span class="sxs-lookup"><span data-stu-id="2f145-176">a.</span></span> <span data-ttu-id="2f145-177">Sélectionnez **Authenticate using SAML Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="2f145-177">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="2f145-178">b.</span><span class="sxs-lookup"><span data-stu-id="2f145-178">b.</span></span> <span data-ttu-id="2f145-179">Cliquez sur **Configure SAML Single Sign-On Parameters**.</span><span class="sxs-lookup"><span data-stu-id="2f145-179">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="2f145-180">Sur la page de dialogue **Configurer les paramètres d’authentification unique SAML**, procédez comme suit, puis cliquez sur **Terminé**</span><span class="sxs-lookup"><span data-stu-id="2f145-180">On the **Configure SAML Single Sign-On Parameters** dialog page, perform the following steps, and then click **Done**</span></span>

    <span data-ttu-id="2f145-181">![Authentification unique](./media/active-directory-saas-zscaler-tutorial/ic800209.png "Authentification unique")</span><span class="sxs-lookup"><span data-stu-id="2f145-181">![Single Sign-On](./media/active-directory-saas-zscaler-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="2f145-182">a.</span><span class="sxs-lookup"><span data-stu-id="2f145-182">a.</span></span> <span data-ttu-id="2f145-183">Collez **l’URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure dans la zone de texte **URL of the SAML Portal to which users are sent for authentication** (URL du portail SAML vers lequel les utilisateurs sont redirigés afin de s’authentifier).</span><span class="sxs-lookup"><span data-stu-id="2f145-183">Paste the **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **URL of the SAML Portal to which users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="2f145-184">b.</span><span class="sxs-lookup"><span data-stu-id="2f145-184">b.</span></span> <span data-ttu-id="2f145-185">Dans la zone de texte **Attribute containing Login Name**, tapez **NameID**.</span><span class="sxs-lookup"><span data-stu-id="2f145-185">In the **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="2f145-186">c.</span><span class="sxs-lookup"><span data-stu-id="2f145-186">c.</span></span> <span data-ttu-id="2f145-187">Pour charger le certificat téléchargé, cliquez sur **Zscaler pem**.</span><span class="sxs-lookup"><span data-stu-id="2f145-187">To upload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="2f145-188">d.</span><span class="sxs-lookup"><span data-stu-id="2f145-188">d.</span></span> <span data-ttu-id="2f145-189">Sélectionnez **Enable SAML Auto-Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="2f145-189">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="2f145-190">Dans la page **Configure User Authentication** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2f145-190">On the **Configure User Authentication** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="2f145-191">![Administration](./media/active-directory-saas-zscaler-tutorial/ic800210.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="2f145-191">![Administration](./media/active-directory-saas-zscaler-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="2f145-192">a.</span><span class="sxs-lookup"><span data-stu-id="2f145-192">a.</span></span> <span data-ttu-id="2f145-193">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="2f145-193">Click **Save**.</span></span>

    <span data-ttu-id="2f145-194">b.</span><span class="sxs-lookup"><span data-stu-id="2f145-194">b.</span></span> <span data-ttu-id="2f145-195">Cliquez sur **Activate Now**.</span><span class="sxs-lookup"><span data-stu-id="2f145-195">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="2f145-196">Configuration des paramètres de proxy</span><span class="sxs-lookup"><span data-stu-id="2f145-196">Configuring proxy settings</span></span>
### <a name="to-configure-the-proxy-settings-in-internet-explorer"></a><span data-ttu-id="2f145-197">Pour configurer les paramètres de proxy dans Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="2f145-197">To configure the proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="2f145-198">Démarrez **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="2f145-198">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="2f145-199">Pour ouvrir la boîte de dialogue **Options Internet**, sélectionnez **Options Internet** dans le menu **Outils**.</span><span class="sxs-lookup"><span data-stu-id="2f145-199">Select **Internet options** from the **Tools** menu for open the **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="2f145-200">![Options Internet](./media/active-directory-saas-zscaler-tutorial/ic769492.png "Options Internet")</span><span class="sxs-lookup"><span data-stu-id="2f145-200">![Internet Options](./media/active-directory-saas-zscaler-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="2f145-201">Cliquez sur l’onglet **Connexions** .</span><span class="sxs-lookup"><span data-stu-id="2f145-201">Click the **Connections** tab.</span></span>   
  
     <span data-ttu-id="2f145-202">![Connexions](./media/active-directory-saas-zscaler-tutorial/ic769493.png "Connexions")</span><span class="sxs-lookup"><span data-stu-id="2f145-202">![Connections](./media/active-directory-saas-zscaler-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="2f145-203">Cliquez sur **Paramètres réseau** pour ouvrir la boîte de dialogue **Paramètres réseau**.</span><span class="sxs-lookup"><span data-stu-id="2f145-203">Click **LAN settings** to open the **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="2f145-204">Dans la section Serveur proxy, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2f145-204">In the Proxy server section, perform the following steps:</span></span>   
   
    <span data-ttu-id="2f145-205">![Serveur proxy](./media/active-directory-saas-zscaler-tutorial/ic769494.png "Serveur proxy")</span><span class="sxs-lookup"><span data-stu-id="2f145-205">![Proxy server](./media/active-directory-saas-zscaler-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="2f145-206">a.</span><span class="sxs-lookup"><span data-stu-id="2f145-206">a.</span></span> <span data-ttu-id="2f145-207">Sélectionnez **Utiliser un serveur proxy pour le réseau local**.</span><span class="sxs-lookup"><span data-stu-id="2f145-207">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="2f145-208">b.</span><span class="sxs-lookup"><span data-stu-id="2f145-208">b.</span></span> <span data-ttu-id="2f145-209">Dans la zone de texte Adresse, tapez **gateway.zscaler.net**.</span><span class="sxs-lookup"><span data-stu-id="2f145-209">In the Address textbox, type **gateway.zscaler.net**.</span></span>

    <span data-ttu-id="2f145-210">c.</span><span class="sxs-lookup"><span data-stu-id="2f145-210">c.</span></span> <span data-ttu-id="2f145-211">Dans la zone de texte Port, tapez **80**.</span><span class="sxs-lookup"><span data-stu-id="2f145-211">In the Port textbox, type **80**.</span></span>

    <span data-ttu-id="2f145-212">d.</span><span class="sxs-lookup"><span data-stu-id="2f145-212">d.</span></span> <span data-ttu-id="2f145-213">Sélectionnez **Ne pas utiliser de serveur proxy pour les adresses locales**.</span><span class="sxs-lookup"><span data-stu-id="2f145-213">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="2f145-214">e.</span><span class="sxs-lookup"><span data-stu-id="2f145-214">e.</span></span> <span data-ttu-id="2f145-215">Cliquez sur **OK** pour fermer la boîte de dialogue **Paramètres du réseau local**.</span><span class="sxs-lookup"><span data-stu-id="2f145-215">Click **OK** to close the **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="2f145-216">Cliquez sur **OK** pour fermer la boîte de dialogue **Options Internet**.</span><span class="sxs-lookup"><span data-stu-id="2f145-216">Click **OK** to close the **Internet Options** dialog.</span></span>

> [!TIP]
> <span data-ttu-id="2f145-217">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="2f145-217">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2f145-218">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="2f145-218">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2f145-219">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2f145-219">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2f145-220">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f145-220">Creating an Azure AD test user</span></span>
<span data-ttu-id="2f145-221">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2f145-221">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="2f145-223">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2f145-223">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2f145-224">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2f145-224">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscaler-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2f145-226">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="2f145-226">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscaler-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2f145-228">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="2f145-228">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscaler-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2f145-230">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2f145-230">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscaler-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2f145-232">a.</span><span class="sxs-lookup"><span data-stu-id="2f145-232">a.</span></span> <span data-ttu-id="2f145-233">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2f145-233">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2f145-234">b.</span><span class="sxs-lookup"><span data-stu-id="2f145-234">b.</span></span> <span data-ttu-id="2f145-235">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2f145-235">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2f145-236">c.</span><span class="sxs-lookup"><span data-stu-id="2f145-236">c.</span></span> <span data-ttu-id="2f145-237">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="2f145-237">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2f145-238">d.</span><span class="sxs-lookup"><span data-stu-id="2f145-238">d.</span></span> <span data-ttu-id="2f145-239">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="2f145-239">Click **Create**.</span></span>
 
### <a name="creating-a-zscaler-test-user"></a><span data-ttu-id="2f145-240">Création d’un utilisateur de test Zscaler</span><span class="sxs-lookup"><span data-stu-id="2f145-240">Creating a Zscaler test user</span></span>

<span data-ttu-id="2f145-241">Pour se connecter à Zscaler, les utilisateurs d’Azure AD doivent être attribués dans Zscaler.</span><span class="sxs-lookup"><span data-stu-id="2f145-241">To enable Azure AD users to log in to ZScaler, they must be provisioned to ZScaler.</span></span>  
<span data-ttu-id="2f145-242">Dans le cas de Zscaler, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="2f145-242">In the case of ZScaler, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="2f145-243">Pour configurer l'approvisionnement des utilisateurs, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2f145-243">To configure user provisioning, perform the following steps:</span></span>

1. <span data-ttu-id="2f145-244">Connectez-vous au locataire **Zscaler** .</span><span class="sxs-lookup"><span data-stu-id="2f145-244">Log in to your **Zscaler** tenant.</span></span>

2. <span data-ttu-id="2f145-245">Cliquez sur **Administration**.</span><span class="sxs-lookup"><span data-stu-id="2f145-245">Click **Administration**.</span></span>   
   
    <span data-ttu-id="2f145-246">![Administration](./media/active-directory-saas-zscaler-tutorial/ic781035.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="2f145-246">![Administration](./media/active-directory-saas-zscaler-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="2f145-247">Cliquez sur **User Management**.</span><span class="sxs-lookup"><span data-stu-id="2f145-247">Click **User Management**.</span></span>   
        
     <span data-ttu-id="2f145-248">![Ajouter](./media/active-directory-saas-zscaler-tutorial/ic781036.png "Ajouter")</span><span class="sxs-lookup"><span data-stu-id="2f145-248">![Add](./media/active-directory-saas-zscaler-tutorial/ic781036.png "Add")</span></span>

4. <span data-ttu-id="2f145-249">Sous l’onglet **Utilisateurs**, cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="2f145-249">In the **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="2f145-250">![Ajouter](./media/active-directory-saas-zscaler-tutorial/ic781037.png "Ajouter")</span><span class="sxs-lookup"><span data-stu-id="2f145-250">![Add](./media/active-directory-saas-zscaler-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="2f145-251">Dans la section Add User, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2f145-251">In the Add User section, perform the following steps:</span></span>
        
    <span data-ttu-id="2f145-252">![Ajouter un utilisateur](./media/active-directory-saas-zscaler-tutorial/ic781038.png "Ajouter un utilisateur")</span><span class="sxs-lookup"><span data-stu-id="2f145-252">![Add User](./media/active-directory-saas-zscaler-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="2f145-253">a.</span><span class="sxs-lookup"><span data-stu-id="2f145-253">a.</span></span> <span data-ttu-id="2f145-254">Renseignez les zones de texte **UserID**, **Nom d’affichage de l’utilisateur**, **Mot de passe** et **Confirmer le mot de passe**, puis sélectionnez **Groupes** ainsi que l’attribut **Département** du compte AAD valide que vous souhaitez approvisionner.</span><span class="sxs-lookup"><span data-stu-id="2f145-254">Type the **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and the **Department** of a valid AAD account you want to provision.</span></span>

    <span data-ttu-id="2f145-255">b.</span><span class="sxs-lookup"><span data-stu-id="2f145-255">b.</span></span> <span data-ttu-id="2f145-256">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="2f145-256">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="2f145-257">Vous pouvez utiliser tout autre outil ou n’importe quelle API de création de compte d’utilisateur fournis par Zscaler pour approvisionner des comptes d’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f145-257">You can use any other ZScaler user account creation tools or APIs provided by ZScaler to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2f145-258">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f145-258">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2f145-259">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Zscaler.</span><span class="sxs-lookup"><span data-stu-id="2f145-259">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zscaler.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="2f145-261">**Pour attribuer Britta Simon à Zscaler, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="2f145-261">**To assign Britta Simon to Zscaler, perform the following steps:**</span></span>

1. <span data-ttu-id="2f145-262">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="2f145-262">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="2f145-264">Dans la liste des applications, sélectionnez **Zscaler**.</span><span class="sxs-lookup"><span data-stu-id="2f145-264">In the applications list, select **Zscaler**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_app.png) 

3. <span data-ttu-id="2f145-266">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="2f145-266">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="2f145-268">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="2f145-268">Click **Add** button.</span></span> <span data-ttu-id="2f145-269">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="2f145-269">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="2f145-271">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="2f145-271">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2f145-272">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="2f145-272">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2f145-273">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="2f145-273">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2f145-274">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="2f145-274">Testing single sign-on</span></span>

<span data-ttu-id="2f145-275">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="2f145-275">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2f145-276">En cliquant sur la vignette Zscaler dans le Panneau d’accès, vous allez en principe être connecté automatiquement à votre application Zscaler.</span><span class="sxs-lookup"><span data-stu-id="2f145-276">When you click the Zscaler tile in the Access Panel, you should get automatically signed-on to your Zscaler application.</span></span>
<span data-ttu-id="2f145-277">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2f145-277">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2f145-278">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="2f145-278">Additional resources</span></span>

* [<span data-ttu-id="2f145-279">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2f145-279">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2f145-280">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="2f145-280">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_203.png

