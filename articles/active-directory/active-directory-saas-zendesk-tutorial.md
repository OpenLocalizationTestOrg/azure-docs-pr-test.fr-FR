---
title: "Didacticiel : Intégration d’Azure Active Directory à Zendesk | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Zendesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9d7c91e5-78f5-4016-862f-0f3242b00680
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 51c06d838c5ed6286dfb99ea25faaaf33bad5f3c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zendesk"></a><span data-ttu-id="0d0b8-103">Didacticiel : Intégration d’Azure Active Directory à Zendesk</span><span class="sxs-lookup"><span data-stu-id="0d0b8-103">Tutorial: Azure Active Directory integration with Zendesk</span></span>

<span data-ttu-id="0d0b8-104">Dans ce didacticiel, vous allez apprendre à intégrer Zendesk à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0d0b8-104">In this tutorial, you learn how to integrate Zendesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0d0b8-105">L’intégration de Zendesk à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="0d0b8-105">Integrating Zendesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0d0b8-106">Dans Azure AD, vous pouvez contrôler qui a accès à Zendesk</span><span class="sxs-lookup"><span data-stu-id="0d0b8-106">You can control in Azure AD who has access to Zendesk</span></span>
- <span data-ttu-id="0d0b8-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Zendesk (via l’authentification unique) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d0b8-107">You can enable your users to automatically get signed-on to Zendesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0d0b8-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="0d0b8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0d0b8-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0d0b8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0d0b8-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0d0b8-110">Prerequisites</span></span>

<span data-ttu-id="0d0b8-111">Pour configurer l’intégration d’Azure AD à Zendesk, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="0d0b8-111">To configure Azure AD integration with Zendesk, you need the following items:</span></span>

- <span data-ttu-id="0d0b8-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d0b8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0d0b8-113">Un abonnement pour lequel l’authentification unique à Zendesk est activée</span><span class="sxs-lookup"><span data-stu-id="0d0b8-113">A Zendesk single sign-on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="0d0b8-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="0d0b8-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="0d0b8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0d0b8-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0d0b8-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0d0b8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="0d0b8-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="0d0b8-118">Scenario description</span></span>
<span data-ttu-id="0d0b8-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0d0b8-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="0d0b8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0d0b8-121">Ajout de Zendesk depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="0d0b8-121">Adding Zendesk from the gallery</span></span>
2. <span data-ttu-id="0d0b8-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d0b8-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-zendesk-from-the-gallery"></a><span data-ttu-id="0d0b8-123">Ajout de Zendesk depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="0d0b8-123">Adding Zendesk from the gallery</span></span>
<span data-ttu-id="0d0b8-124">Pour configurer l’intégration de Zendesk à Azure AD, vous devez ajouter Zendesk, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-124">To configure the integration of Zendesk into Azure AD, you need to add Zendesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0d0b8-125">**Pour ajouter Zendesk à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0d0b8-125">**To add Zendesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0d0b8-126">Dans le volet de navigation gauche du **[Portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0d0b8-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0d0b8-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="0d0b8-131">Cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-131">Click **New application** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="0d0b8-133">Dans la zone de recherche, tapez **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-133">In the search box, type **Zendesk**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_search.png)

5. <span data-ttu-id="0d0b8-135">Dans le panneau de résultats, sélectionnez **Zendesk**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-135">In the results panel, select **Zendesk**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0d0b8-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d0b8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0d0b8-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Zendesk, sur un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="0d0b8-138">In this section, you configure and test Azure AD single sign-on with Zendesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0d0b8-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Zendesk correspondant dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zendesk is to a user in Azure AD.</span></span> <span data-ttu-id="0d0b8-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur dans Zendesk associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-140">In other words, a link relationship between an Azure AD user and the related user in Zendesk needs to be established.</span></span>

<span data-ttu-id="0d0b8-141">Pour cela, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur **Nom d’utilisateur** dans Zendesk.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Zendesk.</span></span>

<span data-ttu-id="0d0b8-142">Pour configurer et tester l’authentification unique Azure AD avec Zendesk, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="0d0b8-142">To configure and test Azure AD single sign-on with Zendesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0d0b8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0d0b8-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0d0b8-145">**[Création d’un utilisateur de test Zendesk](#creating-a-zendesk-test-user)** : pour avoir un équivalent de Britta Simon dans Zendesk lié à la représentation de l’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-145">**[Creating a Zendesk test user](#creating-a-zendesk-test-user)** - to have a counterpart of Britta Simon in Zendesk that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0d0b8-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0d0b8-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0d0b8-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d0b8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0d0b8-149">Dans cette section, vous activez l’authentification unique Azure AD dans le portail Azure et configurez l’authentification unique dans votre application Zendesk.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zendesk application.</span></span>

<span data-ttu-id="0d0b8-150">**Pour configurer l’authentification unique Azure AD avec Zendesk, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0d0b8-150">**To configure Azure AD single sign-on with Zendesk, perform the following steps:**</span></span>

1. <span data-ttu-id="0d0b8-151">Dans le portail Azure, sur la page d’intégration de l’application **Zendesk**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-151">In the Azure portal, on the **Zendesk** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="0d0b8-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_samlbase.png)

3. <span data-ttu-id="0d0b8-155">Dans la section **Domaine et URL Zendesk**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0d0b8-155">On the **Zendesk Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_url.png)

    <span data-ttu-id="0d0b8-157">a.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-157">a.</span></span> <span data-ttu-id="0d0b8-158">Dans la zone de texte **URL de connexion**, tapez la valeur au format suivant : `https://<subdomain>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="0d0b8-158">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<subdomain>.zendesk.com`</span></span>

    <span data-ttu-id="0d0b8-159">b.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-159">b.</span></span> <span data-ttu-id="0d0b8-160">Dans la zone de texte **Identificateur**, tapez la valeur au format suivant : `https://<subdomain>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="0d0b8-160">In the **Identifier** textbox, type the value using the following pattern: `https://<subdomain>.zendesk.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0d0b8-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-161">These values are not real.</span></span> <span data-ttu-id="0d0b8-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur URL réels.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-162">Update these values with the actual Sign-on URL and Identifier URL.</span></span> <span data-ttu-id="0d0b8-163">Pour obtenir ces valeurs, contactez [l’équipe de support technique Zendesk](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise).</span><span class="sxs-lookup"><span data-stu-id="0d0b8-163">Contact [Zendesk support team](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) to get these values.</span></span> 

4. <span data-ttu-id="0d0b8-164">Zendesk attend les assertions SAML dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-164">Zendesk expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="0d0b8-165">Il n’y a aucun attribut SAML obligatoire, mais si vous le souhaitez, vous pouvez ajouter un attribut à partir de la section **Attributs utilisateur** en suivant les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="0d0b8-165">There are no mandatory SAML attributes but optionally you can add an attribute from **User Attributes** section by following the below steps:</span></span> 

     ![Configurer l’authentification unique](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes1.png)

    <span data-ttu-id="0d0b8-167">a.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-167">a.</span></span> <span data-ttu-id="0d0b8-168">Cochez la case **Afficher et modifier tous les autres attributs**.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-168">Click the **View and edit all the other attributes** check box.</span></span>
     
    ![Configurer l’authentification unique](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes2.png)
   
    <span data-ttu-id="0d0b8-170">b.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-170">b.</span></span> <span data-ttu-id="0d0b8-171">Cliquez sur **Ajouter un attribut** pour ouvrir la boîte de dialogue **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-171">Click the **Add Attribute** to open **Add attribute** dialog.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-zendesk-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="0d0b8-173">c.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-173">c.</span></span> <span data-ttu-id="0d0b8-174">Dans la zone de texte **Nom**, saisissez le nom de l’attribut (par exemple **adresse e-mail**).</span><span class="sxs-lookup"><span data-stu-id="0d0b8-174">In the **Name** textbox, type the attribute name (for example **emailaddress**).</span></span>
    
    <span data-ttu-id="0d0b8-175">d.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-175">d.</span></span> <span data-ttu-id="0d0b8-176">Dans la liste **Valeur**, sélectionnez la valeur de l’attribut (comme **user.mail**).</span><span class="sxs-lookup"><span data-stu-id="0d0b8-176">From the **Value** list, select the attribute value (as **user.mail**).</span></span>
    
    <span data-ttu-id="0d0b8-177">e.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-177">e.</span></span> <span data-ttu-id="0d0b8-178">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-178">Click **Ok**</span></span>
 
    > [!NOTE] 
    > <span data-ttu-id="0d0b8-179">Utilisez des attributs d’extension pour ajouter des attributs qui ne sont pas dans Azure AD par défaut.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-179">You use extension attributes to add attributes that are not in Azure AD by default.</span></span> <span data-ttu-id="0d0b8-180">Cliquez sur [les attributs d’utilisateur qui peuvent être définis dans SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) pour obtenir la liste complète des attributs SAML que **Zendesk** accepte.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-180">Click [User attributes that can be set in SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) to get the complete list of SAML attributes that **Zendesk** accepts.</span></span> 

5. <span data-ttu-id="0d0b8-181">Dans la section **Certificat de signature SAML**, copiez la valeur **THUMBPRINT** du certificat.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-181">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_certificate.png) 

6. <span data-ttu-id="0d0b8-183">Dans la section **Configuration de Zendesk**, cliquez sur **Configurer Zendesk** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-183">On the **Zendesk Configuration** section, click **Configure Zendesk** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0d0b8-184">Copiez **l’URL de déconnexion et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-184">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_configure.png) 

7. <span data-ttu-id="0d0b8-186">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Zendesk en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-186">In a different web browser window, log into your Zendesk company site as an administrator.</span></span>

8. <span data-ttu-id="0d0b8-187">Cliquez sur **Admin**.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-187">Click **Admin**.</span></span>

9. <span data-ttu-id="0d0b8-188">Dans le volet de navigation gauche, cliquez sur **Settings**, puis sur **Security**.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-188">In the left navigation pane, click **Settings**, and then click **Security**.</span></span>

10. <span data-ttu-id="0d0b8-189">Sur la page **Sécurité**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0d0b8-189">On the **Security** page, perform the following steps:</span></span> 
   
     <span data-ttu-id="0d0b8-190">![Sécurité](./media/active-directory-saas-zendesk-tutorial/ic773089.png "Sécurité")</span><span class="sxs-lookup"><span data-stu-id="0d0b8-190">![Security](./media/active-directory-saas-zendesk-tutorial/ic773089.png "Security")</span></span>

    <span data-ttu-id="0d0b8-191">![Authentification unique](./media/active-directory-saas-zendesk-tutorial/ic773090.png "Authentification unique")</span><span class="sxs-lookup"><span data-stu-id="0d0b8-191">![Single sign-on](./media/active-directory-saas-zendesk-tutorial/ic773090.png "Single sign-on")</span></span>

     <span data-ttu-id="0d0b8-192">a.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-192">a.</span></span> <span data-ttu-id="0d0b8-193">Cliquez sur l’onglet **Administrateurs et Agents**.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-193">Click the **Admin & Agents** tab.</span></span>

     <span data-ttu-id="0d0b8-194">b.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-194">b.</span></span> <span data-ttu-id="0d0b8-195">Sélectionnez **Single sign-on (SSO) and SAML**, puis **SAML**.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-195">Select **Single sign-on (SSO) and SAML**, and then select **SAML**.</span></span>

     <span data-ttu-id="0d0b8-196">c.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-196">c.</span></span> <span data-ttu-id="0d0b8-197">Dans la zone de texte **URL SAML SSO**, collez la valeur de **l’URL du service d’authentification unique SAML** que vous avez copiée sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-197">In **SAML SSO URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

     <span data-ttu-id="0d0b8-198">d.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-198">d.</span></span> <span data-ttu-id="0d0b8-199">Dans la zone de texte **URL de déconnexion à distance**, collez la valeur de **l’URL de déconnexion** que vous avez copiée sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-199">In **Remote Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
        
     <span data-ttu-id="0d0b8-200">e.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-200">e.</span></span> <span data-ttu-id="0d0b8-201">Dans la zone de texte **Empreinte du certificat**, collez la valeur du certificat **Empreinte** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-201">In **Certificate Fingerprint** textbox, paste the **Thumbprint** value of certificate which you have copied from Azure portal.</span></span>
     
     <span data-ttu-id="0d0b8-202">f.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-202">f.</span></span> <span data-ttu-id="0d0b8-203">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-203">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0d0b8-204">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d0b8-204">Creating an Azure AD test user</span></span>
<span data-ttu-id="0d0b8-205">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-205">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="0d0b8-207">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0d0b8-207">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0d0b8-208">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-208">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0d0b8-210">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-210">To display the list of users go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0d0b8-212">En haut de la boîte de dialogue, cliquez sur **Ajouter** pour ouvrir la boîte de dialogue **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-212">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0d0b8-214">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0d0b8-214">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0d0b8-216">a.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-216">a.</span></span> <span data-ttu-id="0d0b8-217">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-217">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0d0b8-218">b.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-218">b.</span></span> <span data-ttu-id="0d0b8-219">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-219">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0d0b8-220">c.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-220">c.</span></span> <span data-ttu-id="0d0b8-221">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-221">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0d0b8-222">d.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-222">d.</span></span> <span data-ttu-id="0d0b8-223">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-223">Click **Create**.</span></span> 

### <a name="creating-a-zendesk-test-user"></a><span data-ttu-id="0d0b8-224">Création d’un utilisateur de test Zendesk</span><span class="sxs-lookup"><span data-stu-id="0d0b8-224">Creating a Zendesk test user</span></span>

<span data-ttu-id="0d0b8-225">Pour pouvoir se connecter à **Zendesk**, les utilisateurs d’Azure AD doivent être approvisionnés dans **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-225">To enable Azure AD users to log into **Zendesk**, they must be provisioned into **Zendesk**.</span></span>  
<span data-ttu-id="0d0b8-226">En fonction du rôle assigné dans les applications, ce comportement est attendu :</span><span class="sxs-lookup"><span data-stu-id="0d0b8-226">Depending on the role assigned in the apps, it's the expected behavior:</span></span>

 1. <span data-ttu-id="0d0b8-227">Les comptes de **l’utilisateur final** sont automatiquement approvisionnés lors de la connexion.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-227">**End-user** accounts are automatically provisioned when signing in.</span></span>
 2. <span data-ttu-id="0d0b8-228">Les comptes **Agent** et **Admin** doivent être approvisionnés manuellement dans **Zendesk** avant de vous connecter.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-228">**Agent** and **Admin** accounts need to be manually provisioned in **Zendesk** before signing in.</span></span>
 
<span data-ttu-id="0d0b8-229">**Pour approvisionner un compte d’utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0d0b8-229">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="0d0b8-230">Connectez-vous à votre client **Zendesk** .</span><span class="sxs-lookup"><span data-stu-id="0d0b8-230">Log in to your **Zendesk** tenant.</span></span>

2. <span data-ttu-id="0d0b8-231">Sélectionnez l’onglet **Customer List** .</span><span class="sxs-lookup"><span data-stu-id="0d0b8-231">Select the **Customer List** tab.</span></span>

3. <span data-ttu-id="0d0b8-232">Sélectionnez l’onglet **User**, puis cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-232">Select the **User** tab, and click **Add**.</span></span>
   
    <span data-ttu-id="0d0b8-233">![Ajouter un utilisateur](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Ajouter un utilisateur")</span><span class="sxs-lookup"><span data-stu-id="0d0b8-233">![Add user](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Add user")</span></span>
4. <span data-ttu-id="0d0b8-234">Tapez l’adresse de messagerie du compte Azure AD que vous souhaitez approvisionner, puis cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-234">Type the email address of an existing Azure AD account you want to provision, and then click **Save**.</span></span>
   
    <span data-ttu-id="0d0b8-235">![Nouvel utilisateur](./media/active-directory-saas-zendesk-tutorial/ic773633.png "Nouvel utilisateur")</span><span class="sxs-lookup"><span data-stu-id="0d0b8-235">![New user](./media/active-directory-saas-zendesk-tutorial/ic773633.png "New user")</span></span>

> [!NOTE]
> <span data-ttu-id="0d0b8-236">Vous pouvez utiliser tout autre outil ou n’importe quelle API de création de compte d’utilisateur fournis par Zendesk pour approvisionner des comptes d’utilisateurs Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-236">You can use any other Zendesk user account creation tools or APIs provided by Zendesk to provision AAD user accounts.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0d0b8-237">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d0b8-237">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0d0b8-238">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Zendesk.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zendesk.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="0d0b8-240">**Pour affecter Britta Simon à Zendesk, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0d0b8-240">**To assign Britta Simon to Zendesk, perform the following steps:**</span></span>

1. <span data-ttu-id="0d0b8-241">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="0d0b8-243">Dans la liste des applications, sélectionnez **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-243">In the applications list, select **Zendesk**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_app.png) 

3. <span data-ttu-id="0d0b8-245">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-245">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="0d0b8-247">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-247">Click **Add** button.</span></span> <span data-ttu-id="0d0b8-248">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="0d0b8-250">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0d0b8-251">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0d0b8-252">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0d0b8-253">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="0d0b8-253">Testing single sign-on</span></span>

<span data-ttu-id="0d0b8-254">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-254">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0d0b8-255">Lorsque vous cliquez sur la vignette Zendesk dans le volet d’accès, vous devez être connecté automatiquement à votre application Zendesk.</span><span class="sxs-lookup"><span data-stu-id="0d0b8-255">When you click the Zendesk tile in the Access Panel, you should get automatically signed-on to your Zendesk application.</span></span>
<span data-ttu-id="0d0b8-256">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0d0b8-256">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0d0b8-257">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="0d0b8-257">Additional resources</span></span>

* [<span data-ttu-id="0d0b8-258">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0d0b8-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0d0b8-259">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="0d0b8-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_203.png
