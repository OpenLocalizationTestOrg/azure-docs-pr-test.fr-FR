---
title: "Didacticiel : intégration d’Azure Active Directory à Tableau Server | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Tableau Server."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c1917375-08aa-445c-a444-e22e23fa19e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 6b35609d88fbbf649e15863901d521886db2a4d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-server"></a><span data-ttu-id="865a5-103">Didacticiel : Intégration d’Azure Active Directory à Tableau Server</span><span class="sxs-lookup"><span data-stu-id="865a5-103">Tutorial: Azure Active Directory integration with Tableau Server</span></span>

<span data-ttu-id="865a5-104">Dans ce didacticiel, vous allez apprendre à intégrer Tableau Server avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="865a5-104">In this tutorial, you learn how to integrate Tableau Server with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="865a5-105">L’intégration de Tableau Server à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="865a5-105">Integrating Tableau Server with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="865a5-106">Dans Azure AD, vous pouvez contrôler qui a accès à Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="865a5-106">You can control in Azure AD who has access to Tableau Server</span></span>
- <span data-ttu-id="865a5-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Tableau Server (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="865a5-107">You can enable your users to automatically get signed-on to Tableau Server (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="865a5-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="865a5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="865a5-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="865a5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="865a5-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="865a5-110">Prerequisites</span></span>

<span data-ttu-id="865a5-111">Pour configurer l’intégration d’Azure AD à Tableau Server, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="865a5-111">To configure Azure AD integration with Tableau Server, you need the following items:</span></span>

- <span data-ttu-id="865a5-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="865a5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="865a5-113">Un abonnement Tableau Server pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="865a5-113">A Tableau Server single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="865a5-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="865a5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="865a5-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="865a5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="865a5-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="865a5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="865a5-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="865a5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="865a5-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="865a5-118">Scenario description</span></span>
<span data-ttu-id="865a5-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="865a5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="865a5-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="865a5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="865a5-121">Ajout de Tableau Server à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="865a5-121">Adding Tableau Server from the gallery</span></span>
2. <span data-ttu-id="865a5-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="865a5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tableau-server-from-the-gallery"></a><span data-ttu-id="865a5-123">Ajout de Tableau Server à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="865a5-123">Adding Tableau Server from the gallery</span></span>
<span data-ttu-id="865a5-124">Pour configurer l’intégration de Tableau Server à Azure AD, vous devez ajouter Tableau Server, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="865a5-124">To configure the integration of Tableau Server into Azure AD, you need to add Tableau Server from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="865a5-125">**Pour ajouter Tableau Server à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="865a5-125">**To add Tableau Server from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="865a5-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="865a5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="865a5-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="865a5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="865a5-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="865a5-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="865a5-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="865a5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="865a5-133">Dans la zone de recherche, tapez **Tableau Server**.</span><span class="sxs-lookup"><span data-stu-id="865a5-133">In the search box, type **Tableau Server**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_search.png)

5. <span data-ttu-id="865a5-135">Dans le panneau de résultats, sélectionnez **Tableau Server**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="865a5-135">In the results panel, select **Tableau Server**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="865a5-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="865a5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="865a5-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Tableau Server grâce à un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="865a5-138">In this section, you configure and test Azure AD single sign-on with Tableau Server based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="865a5-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Tableau Server équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="865a5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Tableau Server is to a user in Azure AD.</span></span> <span data-ttu-id="865a5-140">En d’autres termes, une relation entre un utilisateur Azure AD et l’utilisateur Tableau Server associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="865a5-140">In other words, a link relationship between an Azure AD user and the related user in Tableau Server needs to be established.</span></span>

<span data-ttu-id="865a5-141">Dans Tableau Server, assignez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **Nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="865a5-141">In Tableau Server, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="865a5-142">Pour configurer et tester l’authentification unique Azure AD avec Tableau Server, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="865a5-142">To configure and test Azure AD single sign-on with Tableau Server, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="865a5-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="865a5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="865a5-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="865a5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="865a5-145">**[Création d’un utilisateur de test Tableau Server](#creating-a-tableau-server-test-user)** pour avoir un équivalent de Britta Simon dans Tableau Server qui est lié à la représentation d’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="865a5-145">**[Creating a Tableau Server test user](#creating-a-tableau-server-test-user)** - to have a counterpart of Britta Simon in Tableau Server that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="865a5-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="865a5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="865a5-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="865a5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="865a5-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="865a5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="865a5-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurez l’authentification unique dans votre application Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="865a5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tableau Server application.</span></span>

<span data-ttu-id="865a5-150">**Pour configurer l’authentification unique Azure AD avec Tableau Server, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="865a5-150">**To configure Azure AD single sign-on with Tableau Server, perform the following steps:**</span></span>

1. <span data-ttu-id="865a5-151">Dans le portail Azure, sur la page d’intégration de l’application **Tableau Server**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="865a5-151">In the Azure portal, on the **Tableau Server** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="865a5-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="865a5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_samlbase.png)

3. <span data-ttu-id="865a5-155">Dans la section **Domaine et URL Tableau Server**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="865a5-155">On the **Tableau Server Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_url.png)

    <span data-ttu-id="865a5-157">a.</span><span class="sxs-lookup"><span data-stu-id="865a5-157">a.</span></span> <span data-ttu-id="865a5-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://azure.<domain name>.link`</span><span class="sxs-lookup"><span data-stu-id="865a5-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://azure.<domain name>.link`</span></span>
    
    <span data-ttu-id="865a5-159">b.</span><span class="sxs-lookup"><span data-stu-id="865a5-159">b.</span></span> <span data-ttu-id="865a5-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://azure.<domain name>.link`</span><span class="sxs-lookup"><span data-stu-id="865a5-160">In the **Identifier** textbox, type a URL using the following pattern: `https://azure.<domain name>.link`</span></span>

    <span data-ttu-id="865a5-161">c.</span><span class="sxs-lookup"><span data-stu-id="865a5-161">c.</span></span> <span data-ttu-id="865a5-162">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://azure.<domain name>.link/wg/saml/SSO/index.html`</span><span class="sxs-lookup"><span data-stu-id="865a5-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://azure.<domain name>.link/wg/saml/SSO/index.html`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="865a5-163">Les valeurs ci-dessus ne sont pas des valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="865a5-163">The preceding values are not real values.</span></span> <span data-ttu-id="865a5-164">Plus tard, vous pourrez mettre à jour les valeurs avec l’URL et l’identificateur réels à partir de la page de configuration de Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="865a5-164">Later, you update the values with the actual URL and identifier from the Tableau Server configuration page.</span></span> 

4. <span data-ttu-id="865a5-165">L’application Tableau Server attend les assertions SAML dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="865a5-165">Tableau Server application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="865a5-166">Configurez les revendications suivantes pour cette application.</span><span class="sxs-lookup"><span data-stu-id="865a5-166">Configure the following claims for this application.</span></span> <span data-ttu-id="865a5-167">Vous pouvez gérer les valeurs de ces attributs à partir de la section **« Attributs utilisateur »** sur la page d’intégration de l’application.</span><span class="sxs-lookup"><span data-stu-id="865a5-167">You can manage the values of these attributes from the **"User Attributes"** section on application integration page.</span></span> <span data-ttu-id="865a5-168">La capture d’écran suivante montre un exemple identique.</span><span class="sxs-lookup"><span data-stu-id="865a5-168">The following screenshot shows an example for the same.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-tableauserver-tutorial/3.png)
    
5. <span data-ttu-id="865a5-170">Dans la section **Attributs utilisateur** de la boîte de dialogue **Authentification unique**, configurez le jeton SAML comme sur l’image ci-dessus et procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="865a5-170">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="865a5-171">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="865a5-171">Attribute Name</span></span> | <span data-ttu-id="865a5-172">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="865a5-172">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="865a5-173">username</span><span class="sxs-lookup"><span data-stu-id="865a5-173">username</span></span> | <span data-ttu-id="865a5-174">*user.displayname*</span><span class="sxs-lookup"><span data-stu-id="865a5-174">*user.displayname*</span></span> |

    <span data-ttu-id="865a5-175">a.</span><span class="sxs-lookup"><span data-stu-id="865a5-175">a.</span></span> <span data-ttu-id="865a5-176">Cliquez sur **Ajouter un attribut** pour ouvrir la boîte de dialogue **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="865a5-176">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_05.png)
    
    <span data-ttu-id="865a5-179">b.</span><span class="sxs-lookup"><span data-stu-id="865a5-179">b.</span></span> <span data-ttu-id="865a5-180">Dans la zone de texte **Attribut**, indiquez le nom d’attribut pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="865a5-180">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="865a5-181">c.</span><span class="sxs-lookup"><span data-stu-id="865a5-181">c.</span></span> <span data-ttu-id="865a5-182">Dans la liste **Valeur** , saisissez la valeur d’attribut affichée pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="865a5-182">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="865a5-183">d.</span><span class="sxs-lookup"><span data-stu-id="865a5-183">d.</span></span> <span data-ttu-id="865a5-184">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="865a5-184">Click **Ok**</span></span>


6. <span data-ttu-id="865a5-185">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="865a5-185">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_certificate.png) 

7. <span data-ttu-id="865a5-187">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="865a5-187">Click **Save** button.</span></span>

    <span data-ttu-id="865a5-188">![Configurer l’authentification unique](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="865a5-188">![Configure Single Sign-On](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS></span></span>
8. <span data-ttu-id="865a5-189">Pour que l’authentification unique soit configurée pour votre application, vous devez vous connecter à votre locataire Tableau Server en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="865a5-189">To get SSO configured for your application, you need to sign-on to your Tableau Server tenant as an administrator.</span></span>
   
   <span data-ttu-id="865a5-190">a.</span><span class="sxs-lookup"><span data-stu-id="865a5-190">a.</span></span> <span data-ttu-id="865a5-191">Dans Tableau Server configuration (Configuration de Tableau Server), cliquez sur l’onglet **SAML** .</span><span class="sxs-lookup"><span data-stu-id="865a5-191">In the Tableau Server configuration, click the **SAML** tab.</span></span>
  
    ![Configurer l’authentification unique](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_001.png) 
  
   <span data-ttu-id="865a5-193">b.</span><span class="sxs-lookup"><span data-stu-id="865a5-193">b.</span></span> <span data-ttu-id="865a5-194">Cochez la case **Use SAML for single sign-on**(Utiliser SAML pour l’authentification unique).</span><span class="sxs-lookup"><span data-stu-id="865a5-194">Select the checkbox of **Use SAML for single sign-on**.</span></span>
   
   <span data-ttu-id="865a5-195">c.</span><span class="sxs-lookup"><span data-stu-id="865a5-195">c.</span></span> <span data-ttu-id="865a5-196">Tableau Server return URL (URL de retour Tableau Server) : URL à laquelle accèdent les utilisateurs Tableau Server, telle que http://tableau_server.</span><span class="sxs-lookup"><span data-stu-id="865a5-196">Tableau Server return URL—The URL that Tableau Server users will be accessing, such as http://tableau_server.</span></span> <span data-ttu-id="865a5-197">L’utilisation de l’URL http://localhost n’est pas recommandée.</span><span class="sxs-lookup"><span data-stu-id="865a5-197">Using http://localhost is not recommended.</span></span> <span data-ttu-id="865a5-198">L’utilisation d’une URL avec une barre oblique finale (par exemple, http://tableau_server/) n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="865a5-198">Using a URL with a trailing slash (for example, http://tableau_server/) is not supported.</span></span> <span data-ttu-id="865a5-199">Copiez l’**URL de renvoi Tableau Server** et collez-la dans la zone de texte **URL de connexion** d’Azure AD, dans la section **Domaine et URL Tableau Server**.</span><span class="sxs-lookup"><span data-stu-id="865a5-199">Copy **Tableau Server return URL** and paste it to Azure AD **Sign On URL** textbox in **Tableau Server Domain and URLs** section.</span></span>
   
   <span data-ttu-id="865a5-200">d.</span><span class="sxs-lookup"><span data-stu-id="865a5-200">d.</span></span> <span data-ttu-id="865a5-201">SAML entity ID (ID d’entité SAML) : l’ID d’entité identifie de façon unique votre installation Tableau Server auprès du fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="865a5-201">SAML entity ID—The entity ID uniquely identifies your Tableau Server installation to the IdP.</span></span> <span data-ttu-id="865a5-202">Vous pouvez à nouveau entrer l’URL Tableau Server ici, si vous le souhaitez, mais ce n’est pas obligatoire.</span><span class="sxs-lookup"><span data-stu-id="865a5-202">You can enter your Tableau Server URL again here, if you like, but it does not have to be your Tableau Server URL.</span></span> <span data-ttu-id="865a5-203">Copiez l’**ID d’entité SAML** et collez-la dans la zone de texte **Identificateur** d’Azure AD, dans la section **Domaine et URL Tableau Server**.</span><span class="sxs-lookup"><span data-stu-id="865a5-203">Copy **SAML entity ID** and paste it to Azure AD **Identifier** textbox in **Tableau Server Domain and URLs** section.</span></span>
     
   <span data-ttu-id="865a5-204">e.</span><span class="sxs-lookup"><span data-stu-id="865a5-204">e.</span></span> <span data-ttu-id="865a5-205">Cliquez sur **Exporter le fichier de métadonnées** et ouvrez-le dans l’application de l’éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="865a5-205">Click the **Export Metadata File** and open it in the text editor application.</span></span> <span data-ttu-id="865a5-206">Recherchez l’URL Assertion Consumer Service avec HTTP POST et Index 0, puis copiez l’URL.</span><span class="sxs-lookup"><span data-stu-id="865a5-206">Locate Assertion Consumer Service URL with Http Post and Index 0 and copy the URL.</span></span> <span data-ttu-id="865a5-207">Collez maintenant cette URL dans la zone de texte **URL de réponse** d’Azure AD, dans la section **Domaine et URL Tableau Server**.</span><span class="sxs-lookup"><span data-stu-id="865a5-207">Now paste it to Azure AD **Reply URL** textbox in **Tableau Server Domain and URLs** section.</span></span>
   
   <span data-ttu-id="865a5-208">f.</span><span class="sxs-lookup"><span data-stu-id="865a5-208">f.</span></span> <span data-ttu-id="865a5-209">Localisez votre fichier de métadonnées de fédération téléchargé à partir du portail Azure, puis chargez-le dans le **fichier de métadonnées du fournisseur d’identité SAML**.</span><span class="sxs-lookup"><span data-stu-id="865a5-209">Locate your Federation Metadata file downloaded from Azure portal, and then upload it in the **SAML Idp metadata file**.</span></span>
   
   <span data-ttu-id="865a5-210">g.</span><span class="sxs-lookup"><span data-stu-id="865a5-210">g.</span></span> <span data-ttu-id="865a5-211">Sur la page Configuration de Tableau Server, cliquez sur le bouton **OK**.</span><span class="sxs-lookup"><span data-stu-id="865a5-211">Click the **OK** button in the Tableau Server Configuration page.</span></span>
   
    >[!NOTE] 
    ><span data-ttu-id="865a5-212">Le client doit charger l’ensemble des certificats dans la configuration SAML SSO de Tableau Server. Les certificats seront ignorés dans le flux SSO.</span><span class="sxs-lookup"><span data-stu-id="865a5-212">Customer have to upload any certificate in the Tableau Server SAML SSO configuration and it will get ignored in the SSO flow.</span></span>
    ><span data-ttu-id="865a5-213">Si vous avez besoin d’aide pour la configuration de SAML dans Tableau Server, consultez l’article [Configurer SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).</span><span class="sxs-lookup"><span data-stu-id="865a5-213">If you need help configuring SAML on Tableau Server then please refer to this article [Configure SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).</span></span>
    >
<CE>

> [!TIP]
> <span data-ttu-id="865a5-214">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="865a5-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="865a5-215">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="865a5-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="865a5-216">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="865a5-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="865a5-217">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="865a5-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="865a5-218">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="865a5-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="865a5-220">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="865a5-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="865a5-221">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="865a5-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="865a5-223">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="865a5-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="865a5-225">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="865a5-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="865a5-227">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="865a5-227">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="865a5-229">a.</span><span class="sxs-lookup"><span data-stu-id="865a5-229">a.</span></span> <span data-ttu-id="865a5-230">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="865a5-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="865a5-231">b.</span><span class="sxs-lookup"><span data-stu-id="865a5-231">b.</span></span> <span data-ttu-id="865a5-232">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="865a5-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="865a5-233">c.</span><span class="sxs-lookup"><span data-stu-id="865a5-233">c.</span></span> <span data-ttu-id="865a5-234">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="865a5-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="865a5-235">d.</span><span class="sxs-lookup"><span data-stu-id="865a5-235">d.</span></span> <span data-ttu-id="865a5-236">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="865a5-236">Click **Create**.</span></span>
 
### <a name="creating-a-tableau-server-test-user"></a><span data-ttu-id="865a5-237">Création d’un utilisateur de test Tableau Server</span><span class="sxs-lookup"><span data-stu-id="865a5-237">Creating a Tableau Server test user</span></span>

<span data-ttu-id="865a5-238">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="865a5-238">The objective of this section is to create a user called Britta Simon in Tableau Server.</span></span> <span data-ttu-id="865a5-239">Vous devez approvisionner tous les utilisateurs dans Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="865a5-239">You need to provision all the users in the Tableau server.</span></span> 

<span data-ttu-id="865a5-240">Le nom de l’utilisateur doit correspondre à la valeur que vous avez configurée dans l’attribut personnalisé Azure AD **username**.</span><span class="sxs-lookup"><span data-stu-id="865a5-240">That username of the user should match the value which you have configured in the Azure AD custom attribute of **username**.</span></span> <span data-ttu-id="865a5-241">Avec le mappage correct, l’intégration doit fonctionner. [Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="865a5-241">With the correct mapping the integration should work [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="865a5-242">Si vous avez besoin de créer un utilisateur manuellement, vous devez contacter l’administrateur Tableau Server de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="865a5-242">If you need to create a user manually, you need to contact the Tableau Server administrator in your organization.</span></span>
> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="865a5-243">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="865a5-243">Assigning the Azure AD test user</span></span>

<span data-ttu-id="865a5-244">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="865a5-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tableau Server.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="865a5-246">**Pour affecter Britta Simon à Tableau Server, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="865a5-246">**To assign Britta Simon to Tableau Server, perform the following steps:**</span></span>

1. <span data-ttu-id="865a5-247">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="865a5-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="865a5-249">Dans la liste des applications, sélectionnez **Tableau Server**.</span><span class="sxs-lookup"><span data-stu-id="865a5-249">In the applications list, select **Tableau Server**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_app.png) 

3. <span data-ttu-id="865a5-251">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="865a5-251">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="865a5-253">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="865a5-253">Click **Add** button.</span></span> <span data-ttu-id="865a5-254">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="865a5-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="865a5-256">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="865a5-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="865a5-257">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="865a5-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="865a5-258">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="865a5-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="865a5-259">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="865a5-259">Testing single sign-on</span></span>

<span data-ttu-id="865a5-260">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="865a5-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="865a5-261">Quand vous cliquez sur la vignette Tableau Server dans le volet d’accès, vous devez être connecté automatiquement à votre application Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="865a5-261">When you click the Tableau Server tile in the Access Panel, you should get automatically signed-on to your Tableau Server application.</span></span>
<span data-ttu-id="865a5-262">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="865a5-262">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="865a5-263">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="865a5-263">Additional resources</span></span>

* [<span data-ttu-id="865a5-264">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="865a5-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="865a5-265">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="865a5-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_203.png

