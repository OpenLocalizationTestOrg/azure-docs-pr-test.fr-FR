---
title: "Didacticiel : Intégration d’Azure Active Directory dans M-Files | Documentation Microsoft"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et M-Files."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4536fd49-3a65-4cff-9620-860904f726d0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 0f2682cf7cd3e11a5a7156938fbe9d4c7f541312
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-m-files"></a><span data-ttu-id="bd93c-103">Didacticiel : Intégration d’Azure AD à M-Files</span><span class="sxs-lookup"><span data-stu-id="bd93c-103">Tutorial: Azure Active Directory integration with M-Files</span></span>

<span data-ttu-id="bd93c-104">Dans ce didacticiel, vous allez apprendre à intégrer M-Files à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bd93c-104">In this tutorial, you learn how to integrate M-Files with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bd93c-105">L’intégration de M-Files dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="bd93c-105">Integrating M-Files with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bd93c-106">Dans Azure AD, vous pouvez contrôler qui a accès à M-Files</span><span class="sxs-lookup"><span data-stu-id="bd93c-106">You can control in Azure AD who has access to M-Files</span></span>
- <span data-ttu-id="bd93c-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à M-Files (via l'authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd93c-107">You can enable your users to automatically get signed-on to M-Files (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bd93c-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="bd93c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="bd93c-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bd93c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd93c-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="bd93c-110">Prerequisites</span></span>

<span data-ttu-id="bd93c-111">Pour configurer l'intégration d'Azure AD avec M-Files, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="bd93c-111">To configure Azure AD integration with M-Files, you need the following items:</span></span>

- <span data-ttu-id="bd93c-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd93c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bd93c-113">Un abonnement à M-Files pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="bd93c-113">A M-Files single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bd93c-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="bd93c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bd93c-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="bd93c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bd93c-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="bd93c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bd93c-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bd93c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bd93c-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="bd93c-118">Scenario description</span></span>
<span data-ttu-id="bd93c-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="bd93c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bd93c-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="bd93c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bd93c-121">Ajout de M-Files à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="bd93c-121">Adding M-Files from the gallery</span></span>
2. <span data-ttu-id="bd93c-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd93c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-m-files-from-the-gallery"></a><span data-ttu-id="bd93c-123">Ajout de M-Files à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="bd93c-123">Adding M-Files from the gallery</span></span>
<span data-ttu-id="bd93c-124">Pour configurer l’intégration de M-Files avec Azure AD, vous devez ajouter M-Files à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="bd93c-124">To configure the integration of M-Files into Azure AD, you need to add M-Files from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bd93c-125">**Pour ajouter M-Files à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bd93c-125">**To add M-Files from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bd93c-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bd93c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bd93c-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="bd93c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bd93c-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="bd93c-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="bd93c-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="bd93c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="bd93c-133">Dans la zone de recherche, entrez **M-Files**.</span><span class="sxs-lookup"><span data-stu-id="bd93c-133">In the search box, type **M-Files**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_search.png)

5. <span data-ttu-id="bd93c-135">Dans le volet de résultats, sélectionnez **M-Files**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="bd93c-135">In the results panel, select **M-Files**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bd93c-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd93c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bd93c-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec M-Files avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="bd93c-138">In this section, you configure and test Azure AD single sign-on with M-Files based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bd93c-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur M-Files équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd93c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in M-Files is to a user in Azure AD.</span></span> <span data-ttu-id="bd93c-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur M-Files associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="bd93c-140">In other words, a link relationship between an Azure AD user and the related user in M-Files needs to be established.</span></span>

<span data-ttu-id="bd93c-141">Dans M-Files, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur **Nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="bd93c-141">In M-Files, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="bd93c-142">Pour configurer et tester l’authentification unique Azure AD avec M-Files, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="bd93c-142">To configure and test Azure AD single sign-on with M-Files, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bd93c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="bd93c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bd93c-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bd93c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bd93c-145">**[Création d’un utilisateur de test M-Files](#creating-a-m-files-test-user)** : pour avoir un équivalent de Britta Simon dans M-Files lié à la représentation de l’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd93c-145">**[Creating a M-Files test user](#creating-a-m-files-test-user)** - to have a counterpart of Britta Simon in M-Files that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="bd93c-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd93c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bd93c-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="bd93c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bd93c-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd93c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bd93c-149">Dans cette section, vous activez l’authentification unique Azure AD dans le portail Azure et configurez l’authentification unique dans votre application M-Files.</span><span class="sxs-lookup"><span data-stu-id="bd93c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your M-Files application.</span></span>

<span data-ttu-id="bd93c-150">**Pour configurer l’authentification unique Azure AD avec M-Files, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bd93c-150">**To configure Azure AD single sign-on with M-Files, perform the following steps:**</span></span>

1. <span data-ttu-id="bd93c-151">Dans le portail Azure, sur la page d’intégration de l’application **M-Files**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="bd93c-151">In the Azure portal, on the **M-Files** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="bd93c-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="bd93c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_samlbase.png)

3. <span data-ttu-id="bd93c-155">Dans la section **Domaine et URL M-Files**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="bd93c-155">On the **M-Files Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_url.png)

    <span data-ttu-id="bd93c-157">a.</span><span class="sxs-lookup"><span data-stu-id="bd93c-157">a.</span></span> <span data-ttu-id="bd93c-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span><span class="sxs-lookup"><span data-stu-id="bd93c-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span></span>

    <span data-ttu-id="bd93c-159">b.</span><span class="sxs-lookup"><span data-stu-id="bd93c-159">b.</span></span> <span data-ttu-id="bd93c-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<tenantname>.cloudvault.m-files.com`</span><span class="sxs-lookup"><span data-stu-id="bd93c-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.cloudvault.m-files.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bd93c-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="bd93c-161">These values are not real.</span></span> <span data-ttu-id="bd93c-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="bd93c-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="bd93c-163">Pour obtenir ces valeurs, contactez [l’équipe de support technique M-Files](mailto:support@m-files.com).</span><span class="sxs-lookup"><span data-stu-id="bd93c-163">Contact [M-Files Client support team](mailto:support@m-files.com) to get these values.</span></span> 
 
4. <span data-ttu-id="bd93c-164">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="bd93c-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_certificate.png) 

5. <span data-ttu-id="bd93c-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="bd93c-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-m-files-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bd93c-168">Pour obtenir la configuration de l’authentification unique pour votre application, contactez [l’équipe de support technique M-Files](mailto:support@m-files.com), en lui fournissant les métadonnées téléchargées.</span><span class="sxs-lookup"><span data-stu-id="bd93c-168">To get SSO configured for your application, contact [M-Files support team](mailto:support@m-files.com) and provide them the downloaded Metadata.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="bd93c-169">Suivez les étapes suivantes si vous souhaitez configurer l’authentification unique pour votre application de bureau M-Files.</span><span class="sxs-lookup"><span data-stu-id="bd93c-169">Follow the next steps if you want to configure SSO for you M-File desktop application.</span></span> <span data-ttu-id="bd93c-170">Aucune étape supplémentaire n’est nécessaire si vous souhaitez configurer l’authentification unique pour la version web de M-Files uniquement.</span><span class="sxs-lookup"><span data-stu-id="bd93c-170">No extra steps are required if you only want to configure SSO for M-Files web version.</span></span>  

7. <span data-ttu-id="bd93c-171">Suivez la procédure suivante pour configurer l’application de bureau M-Files de sorte à activer l’authentification unique avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd93c-171">Follow the next steps to configure the M-File desktop application to enable SSO with Azure AD.</span></span> <span data-ttu-id="bd93c-172">Pour télécharger M-Files, accédez à la page [Téléchargement de M-Files](https://www.m-files.com/en/download-latest-version).</span><span class="sxs-lookup"><span data-stu-id="bd93c-172">To download M-Files, go to [M-Files download](https://www.m-files.com/en/download-latest-version) page.</span></span>

8. <span data-ttu-id="bd93c-173">Ouvrez la fenêtre **Paramètres de bureau M-Files**.</span><span class="sxs-lookup"><span data-stu-id="bd93c-173">Open the **M-Files Desktop Settings** window.</span></span> <span data-ttu-id="bd93c-174">Cliquez ensuite sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="bd93c-174">Then, click **Add**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_10.png)

9. <span data-ttu-id="bd93c-176">Dans la fenêtre **Propriétés de connexion au coffre de documents**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="bd93c-176">On the **Document Vault Connection Properties** window, perform the following steps:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_11.png)  

    <span data-ttu-id="bd93c-178">Sous la section Serveur, saisissez les valeurs comme suit :</span><span class="sxs-lookup"><span data-stu-id="bd93c-178">Under the Server section type, the values as follows:</span></span>  

    <span data-ttu-id="bd93c-179">a.</span><span class="sxs-lookup"><span data-stu-id="bd93c-179">a.</span></span> <span data-ttu-id="bd93c-180">Pour **Nom**, saisissez `<tenant-name>.cloudvault.m-files.com`.</span><span class="sxs-lookup"><span data-stu-id="bd93c-180">For **Name**, type `<tenant-name>.cloudvault.m-files.com`.</span></span> 
 
    <span data-ttu-id="bd93c-181">b.</span><span class="sxs-lookup"><span data-stu-id="bd93c-181">b.</span></span> <span data-ttu-id="bd93c-182">Pour **Numéro de port**, saisissez **4466**.</span><span class="sxs-lookup"><span data-stu-id="bd93c-182">For **Port Number**, type **4466**.</span></span> 

    <span data-ttu-id="bd93c-183">c.</span><span class="sxs-lookup"><span data-stu-id="bd93c-183">c.</span></span> <span data-ttu-id="bd93c-184">Pour **Protocole**, sélectionnez **HTTPS**.</span><span class="sxs-lookup"><span data-stu-id="bd93c-184">For **Protocol**, select **HTTPS**.</span></span> 

    <span data-ttu-id="bd93c-185">d.</span><span class="sxs-lookup"><span data-stu-id="bd93c-185">d.</span></span> <span data-ttu-id="bd93c-186">Dans le champ **Authentification**, sélectionnez **Utilisateur Windows spécifique**.</span><span class="sxs-lookup"><span data-stu-id="bd93c-186">In the **Authentication** field, select **Specific Windows user**.</span></span> <span data-ttu-id="bd93c-187">Ensuite, une page de signature s’affiche.</span><span class="sxs-lookup"><span data-stu-id="bd93c-187">Then, you are prompted with a signing page.</span></span> <span data-ttu-id="bd93c-188">Entrez vos informations d’identification Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd93c-188">Insert your Azure AD credentials.</span></span> 

    <span data-ttu-id="bd93c-189">e.</span><span class="sxs-lookup"><span data-stu-id="bd93c-189">e.</span></span> <span data-ttu-id="bd93c-190">Pour **Coffre sur le serveur**,  sélectionnez le coffre correspondant sur le serveur.</span><span class="sxs-lookup"><span data-stu-id="bd93c-190">For the **Vault on Server**,  select the corresponding vault on server.</span></span>
 
    <span data-ttu-id="bd93c-191">f.</span><span class="sxs-lookup"><span data-stu-id="bd93c-191">f.</span></span> <span data-ttu-id="bd93c-192">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="bd93c-192">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="bd93c-193">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="bd93c-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bd93c-194">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="bd93c-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bd93c-195">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bd93c-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bd93c-196">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd93c-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="bd93c-197">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="bd93c-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="bd93c-199">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bd93c-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bd93c-200">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bd93c-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bd93c-202">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="bd93c-202">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bd93c-204">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="bd93c-204">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bd93c-206">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="bd93c-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bd93c-208">a.</span><span class="sxs-lookup"><span data-stu-id="bd93c-208">a.</span></span> <span data-ttu-id="bd93c-209">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bd93c-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bd93c-210">b.</span><span class="sxs-lookup"><span data-stu-id="bd93c-210">b.</span></span> <span data-ttu-id="bd93c-211">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bd93c-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bd93c-212">c.</span><span class="sxs-lookup"><span data-stu-id="bd93c-212">c.</span></span> <span data-ttu-id="bd93c-213">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="bd93c-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="bd93c-214">d.</span><span class="sxs-lookup"><span data-stu-id="bd93c-214">d.</span></span> <span data-ttu-id="bd93c-215">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="bd93c-215">Click **Create**.</span></span>
 
### <a name="creating-a-m-files-test-user"></a><span data-ttu-id="bd93c-216">Création d’un utilisateur de test M-Files</span><span class="sxs-lookup"><span data-stu-id="bd93c-216">Creating a M-Files test user</span></span>

<span data-ttu-id="bd93c-217">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans M-Files.</span><span class="sxs-lookup"><span data-stu-id="bd93c-217">The objective of this section is to create a user called Britta Simon in M-Files.</span></span> <span data-ttu-id="bd93c-218">Travailler avec [l’équipe de support technique M-Files](mailto:support@m-files.com) pour ajouter des utilisateurs dans les M-Files.</span><span class="sxs-lookup"><span data-stu-id="bd93c-218">Work with  [M-Files support team](mailto:support@m-files.com) to add the users in the M-Files.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="bd93c-219">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd93c-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="bd93c-220">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à M-Files.</span><span class="sxs-lookup"><span data-stu-id="bd93c-220">In this section, you enable Britta Simon to use Azure single sign-on by granting access to M-Files.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="bd93c-222">**Pour affecter Britta Simon à M-Files, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bd93c-222">**To assign Britta Simon to M-Files, perform the following steps:**</span></span>

1. <span data-ttu-id="bd93c-223">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="bd93c-223">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="bd93c-225">Dans la liste des applications, sélectionnez **M-Files**.</span><span class="sxs-lookup"><span data-stu-id="bd93c-225">In the applications list, select **M-Files**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_app.png) 

3. <span data-ttu-id="bd93c-227">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="bd93c-227">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="bd93c-229">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="bd93c-229">Click **Add** button.</span></span> <span data-ttu-id="bd93c-230">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="bd93c-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="bd93c-232">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="bd93c-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="bd93c-233">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="bd93c-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bd93c-234">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="bd93c-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bd93c-235">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="bd93c-235">Testing single sign-on</span></span>

<span data-ttu-id="bd93c-236">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="bd93c-236">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="bd93c-237">Lorsque vous cliquez sur la mosaïque M-Files dans le volet d'accès, vous êtes connecté automatiquement à votre application M-Files.</span><span class="sxs-lookup"><span data-stu-id="bd93c-237">When you click the M-Files tile in the Access Panel, you should get automatically signed-on to your M-Files application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bd93c-238">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="bd93c-238">Additional resources</span></span>

* [<span data-ttu-id="bd93c-239">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bd93c-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bd93c-240">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="bd93c-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_203.png

