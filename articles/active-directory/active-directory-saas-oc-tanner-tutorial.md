---
title: "Didacticiel : Intégration d’Azure Active Directory à O.C. Tanner - AppreciateHub | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et O.C. Tanner - AppreciateHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dee8fbca-0b60-4a21-8917-1fb6919de5a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: 9af12372b30d9ee1575e46be3b4144fc3b73ec69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-oc-tanner---appreciatehub"></a><span data-ttu-id="8282a-105">Didacticiel : Intégration d’Azure Active Directory à O.C.</span><span class="sxs-lookup"><span data-stu-id="8282a-105">Tutorial: Azure Active Directory integration with O.C.</span></span> <span data-ttu-id="8282a-106">Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="8282a-106">Tanner - AppreciateHub</span></span>

<span data-ttu-id="8282a-107">Dans ce didacticiel, vous allez apprendre à intégrer O.C.</span><span class="sxs-lookup"><span data-stu-id="8282a-107">In this tutorial, you learn how to integrate O.C.</span></span> <span data-ttu-id="8282a-108">Tanner - AppreciateHub à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8282a-108">Tanner - AppreciateHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8282a-109">L’intégration d’O.C.</span><span class="sxs-lookup"><span data-stu-id="8282a-109">Integrating O.C.</span></span> <span data-ttu-id="8282a-110">Tanner - AppreciateHub à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="8282a-110">Tanner - AppreciateHub with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8282a-111">Dans Azure AD, vous pouvez contrôler qui a accès à O.C.</span><span class="sxs-lookup"><span data-stu-id="8282a-111">You can control in Azure AD who has access to O.C.</span></span> <span data-ttu-id="8282a-112">Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="8282a-112">Tanner - AppreciateHub</span></span>
- <span data-ttu-id="8282a-113">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à O.C.</span><span class="sxs-lookup"><span data-stu-id="8282a-113">You can enable your users to automatically get signed-on to O.C.</span></span> <span data-ttu-id="8282a-114">Tanner - AppreciateHub (par le biais de l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8282a-114">Tanner - AppreciateHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8282a-115">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="8282a-115">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8282a-116">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8282a-116">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8282a-117">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8282a-117">Prerequisites</span></span>

<span data-ttu-id="8282a-118">Pour configurer l’intégration d’Azure AD à O.C.</span><span class="sxs-lookup"><span data-stu-id="8282a-118">To configure Azure AD integration with O.C.</span></span> <span data-ttu-id="8282a-119">Tanner - AppreciateHub, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="8282a-119">Tanner - AppreciateHub, you need the following items:</span></span>

- <span data-ttu-id="8282a-120">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="8282a-120">An Azure AD subscription</span></span>
- <span data-ttu-id="8282a-121">Un abonnement O.C.</span><span class="sxs-lookup"><span data-stu-id="8282a-121">A O.C.</span></span> <span data-ttu-id="8282a-122">Un abonnement Tanner - AppreciateHub pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="8282a-122">Tanner - AppreciateHub single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8282a-123">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="8282a-123">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8282a-124">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="8282a-124">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8282a-125">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="8282a-125">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8282a-126">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8282a-126">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8282a-127">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="8282a-127">Scenario description</span></span>
<span data-ttu-id="8282a-128">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="8282a-128">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8282a-129">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="8282a-129">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8282a-130">Ajout d’O.C.</span><span class="sxs-lookup"><span data-stu-id="8282a-130">Adding O.C.</span></span> <span data-ttu-id="8282a-131">Tanner - AppreciateHub à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="8282a-131">Tanner - AppreciateHub from the gallery</span></span>
2. <span data-ttu-id="8282a-132">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8282a-132">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-oc-tanner---appreciatehub-from-the-gallery"></a><span data-ttu-id="8282a-133">Ajout d’O.C.</span><span class="sxs-lookup"><span data-stu-id="8282a-133">Adding O.C.</span></span> <span data-ttu-id="8282a-134">Tanner - AppreciateHub à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="8282a-134">Tanner - AppreciateHub from the gallery</span></span>
<span data-ttu-id="8282a-135">Pour configurer l’intégration d’O.C.</span><span class="sxs-lookup"><span data-stu-id="8282a-135">To configure the integration of O.C.</span></span> <span data-ttu-id="8282a-136">Tanner - AppreciateHub à Azure AD, vous devez ajouter O.C.</span><span class="sxs-lookup"><span data-stu-id="8282a-136">Tanner - AppreciateHub into Azure AD, you need to add O.C.</span></span> <span data-ttu-id="8282a-137">Tanner - AppreciateHub à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="8282a-137">Tanner - AppreciateHub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8282a-138">**Pour ajouter O.C. Tanner - AppreciateHub à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8282a-138">**To add O.C. Tanner - AppreciateHub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8282a-139">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8282a-139">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8282a-141">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="8282a-141">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8282a-142">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8282a-142">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="8282a-144">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8282a-144">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="8282a-146">Dans la zone de recherche, tapez **O.C. Tanner - AppreciateHub**.</span><span class="sxs-lookup"><span data-stu-id="8282a-146">In the search box, type **O.C. Tanner - AppreciateHub**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_search.png)

5. <span data-ttu-id="8282a-148">Dans le panneau des résultats, sélectionnez **O.C. Tanner - AppreciateHub**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="8282a-148">In the results panel, select **O.C. Tanner - AppreciateHub**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8282a-150">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8282a-150">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8282a-151">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec O.C.</span><span class="sxs-lookup"><span data-stu-id="8282a-151">In this section, you configure and test Azure AD single sign-on with O.C.</span></span> <span data-ttu-id="8282a-152">Tanner - AppreciateHub au moyen d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="8282a-152">Tanner - AppreciateHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8282a-153">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur O.C.</span><span class="sxs-lookup"><span data-stu-id="8282a-153">For single sign-on to work, Azure AD needs to know what the counterpart user in O.C.</span></span> <span data-ttu-id="8282a-154">Tanner - AppreciateHub équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8282a-154">Tanner - AppreciateHub is to a user in Azure AD.</span></span> <span data-ttu-id="8282a-155">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur O.C.</span><span class="sxs-lookup"><span data-stu-id="8282a-155">In other words, a link relationship between an Azure AD user and the related user in O.C.</span></span> <span data-ttu-id="8282a-156">Tanner - AppreciateHub associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="8282a-156">Tanner - AppreciateHub needs to be established.</span></span>

<span data-ttu-id="8282a-157">Dans O.C.</span><span class="sxs-lookup"><span data-stu-id="8282a-157">In O.C.</span></span> <span data-ttu-id="8282a-158">Tanner - AppreciateHub, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="8282a-158">Tanner - AppreciateHub, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8282a-159">Pour configurer et tester l’authentification unique Azure AD avec O.C.</span><span class="sxs-lookup"><span data-stu-id="8282a-159">To configure and test Azure AD single sign-on with O.C.</span></span> <span data-ttu-id="8282a-160">Tanner - AppreciateHub, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="8282a-160">Tanner - AppreciateHub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8282a-161">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="8282a-161">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8282a-162">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8282a-162">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8282a-163">**[Création d’un utilisateur de test O.C. Tanner - AppreciateHub](#creating-a-oc-tanner---appreciatehub-test-user)** pour avoir un équivalent de Britta Simon dans O.C.</span><span class="sxs-lookup"><span data-stu-id="8282a-163">**[Creating a O.C. Tanner - AppreciateHub test user](#creating-a-oc-tanner---appreciatehub-test-user)** - to have a counterpart of Britta Simon in O.C.</span></span> <span data-ttu-id="8282a-164">Tanner - AppreciateHub lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="8282a-164">Tanner - AppreciateHub that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8282a-165">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8282a-165">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8282a-166">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="8282a-166">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8282a-167">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8282a-167">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8282a-168">Dans cette section, vous activez l’authentification unique Azure AD dans le portail Azure et configurez l’authentification unique dans votre application O.C.</span><span class="sxs-lookup"><span data-stu-id="8282a-168">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your O.C.</span></span> <span data-ttu-id="8282a-169">Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="8282a-169">Tanner - AppreciateHub application.</span></span>

<span data-ttu-id="8282a-170">**Pour configurer l’authentification unique Azure AD avec O.C. Tanner - AppreciateHub, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8282a-170">**To configure Azure AD single sign-on with O.C. Tanner - AppreciateHub, perform the following steps:**</span></span>

1. <span data-ttu-id="8282a-171">Dans le portail Azure, sur la page d’intégration de l’application **O.C. Tanner - AppreciateHub** cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="8282a-171">In the Azure portal, on the **O.C. Tanner - AppreciateHub** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="8282a-173">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="8282a-173">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_samlbase.png)

3. <span data-ttu-id="8282a-175">Dans la section **Domaine et URL O.C. Tanner - AppreciateHub**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="8282a-175">On the **O.C. Tanner - AppreciateHub Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_url.png)

    <span data-ttu-id="8282a-177">a.</span><span class="sxs-lookup"><span data-stu-id="8282a-177">a.</span></span> <span data-ttu-id="8282a-178">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<companyname>.appreciatehub.com/fed/sp/authnResponse20`</span><span class="sxs-lookup"><span data-stu-id="8282a-178">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.appreciatehub.com/fed/sp/authnResponse20`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8282a-179">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="8282a-179">This value is not real.</span></span> <span data-ttu-id="8282a-180">Mettez à jour la valeur avec l’URL de réponse réelle.</span><span class="sxs-lookup"><span data-stu-id="8282a-180">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="8282a-181">Pour obtenir cette valeur, contactez [l’équipe du support technique O.C. Tanner - AppreciateHub](mailto:sso@octanner.com).</span><span class="sxs-lookup"><span data-stu-id="8282a-181">Contact [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com) to get this value.</span></span>

    <span data-ttu-id="8282a-182">b.</span><span class="sxs-lookup"><span data-stu-id="8282a-182">b.</span></span> <span data-ttu-id="8282a-183">Ouvrez le fichier de métadonnées à l’aide du lien suivant : [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).</span><span class="sxs-lookup"><span data-stu-id="8282a-183">Open the metadata file using the following link: [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).</span></span>
   
    <span data-ttu-id="8282a-184">c.</span><span class="sxs-lookup"><span data-stu-id="8282a-184">c.</span></span> <span data-ttu-id="8282a-185">Recherchez le nœud **md:AssertionConsumerService** .</span><span class="sxs-lookup"><span data-stu-id="8282a-185">Locate the **md:AssertionConsumerService** node.</span></span> 
   
    <span data-ttu-id="8282a-186">d.</span><span class="sxs-lookup"><span data-stu-id="8282a-186">d.</span></span> <span data-ttu-id="8282a-187">Copiez la valeur de l’attribut **Location** .</span><span class="sxs-lookup"><span data-stu-id="8282a-187">Copy the value of the **Location** attribute.</span></span> 
   
    ![Configurer les paramètres d’application][12]
   
    <span data-ttu-id="8282a-189">e.</span><span class="sxs-lookup"><span data-stu-id="8282a-189">e.</span></span> <span data-ttu-id="8282a-190">Dans la zone de texte **URL de connexion** , collez la valeur que vous avez obtenue à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="8282a-190">In the **Sign On URL** textbox, past the value you have obtained in the previous step.</span></span>

4. <span data-ttu-id="8282a-191">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="8282a-191">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_certificate.png) 

5. <span data-ttu-id="8282a-193">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="8282a-193">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8282a-195">Pour configurer l’authentification unique côté **O.C. Tanner - AppreciateHub**, vous devez envoyer le fichier **XML de métadonnées** téléchargé à [l’équipe du support technique O.C. Tanner - AppreciateHub](mailto:sso@octanner.com).</span><span class="sxs-lookup"><span data-stu-id="8282a-195">To configure single sign-on on **O.C. Tanner - AppreciateHub** side, you need to send the downloaded **Metadata XML** to [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com).</span></span>

> [!TIP]
> <span data-ttu-id="8282a-196">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="8282a-196">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8282a-197">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="8282a-197">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8282a-198">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8282a-198">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8282a-199">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="8282a-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="8282a-200">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8282a-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="8282a-202">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8282a-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8282a-203">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8282a-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8282a-205">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="8282a-205">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8282a-207">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8282a-207">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8282a-209">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="8282a-209">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8282a-211">a.</span><span class="sxs-lookup"><span data-stu-id="8282a-211">a.</span></span> <span data-ttu-id="8282a-212">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8282a-212">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8282a-213">b.</span><span class="sxs-lookup"><span data-stu-id="8282a-213">b.</span></span> <span data-ttu-id="8282a-214">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8282a-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8282a-215">c.</span><span class="sxs-lookup"><span data-stu-id="8282a-215">c.</span></span> <span data-ttu-id="8282a-216">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="8282a-216">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8282a-217">d.</span><span class="sxs-lookup"><span data-stu-id="8282a-217">d.</span></span> <span data-ttu-id="8282a-218">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="8282a-218">Click **Create**.</span></span>
 
### <a name="creating-a-oc-tanner---appreciatehub-test-user"></a><span data-ttu-id="8282a-219">Création d’un utilisateur de test O.C.</span><span class="sxs-lookup"><span data-stu-id="8282a-219">Creating a O.C.</span></span> <span data-ttu-id="8282a-220">Tanner - AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="8282a-220">Tanner - AppreciateHub test user</span></span>

<span data-ttu-id="8282a-221">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans O.C.</span><span class="sxs-lookup"><span data-stu-id="8282a-221">The objective of this section is to create a user called Britta Simon in O.C.</span></span> <span data-ttu-id="8282a-222">Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="8282a-222">Tanner - AppreciateHub.</span></span>

<span data-ttu-id="8282a-223">**Pour créer un utilisateur nommé Britta Simon dans O.C. Tanner - AppreciateHub, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8282a-223">**To create a user called Britta Simon in O.C. Tanner - AppreciateHub, perform the following steps:**</span></span>

<span data-ttu-id="8282a-224">Demandez à [l’équipe du support technique O.C. Tanner - AppreciateHub](mailto:sso@octanner.com) de créer un utilisateur dont l’attribut nameID est identique au nom d’utilisateur de Britta Simon dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8282a-224">Ask your [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com) to create a user that has as nameID attribute the same value as the user name of Britta Simon in Azure AD.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8282a-225">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="8282a-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8282a-226">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à O.C.</span><span class="sxs-lookup"><span data-stu-id="8282a-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to O.C.</span></span> <span data-ttu-id="8282a-227">Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="8282a-227">Tanner - AppreciateHub.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="8282a-229">**Pour affecter Britta Simon à O.C. Tanner - AppreciateHub, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8282a-229">**To assign Britta Simon to O.C. Tanner - AppreciateHub, perform the following steps:**</span></span>

1. <span data-ttu-id="8282a-230">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8282a-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="8282a-232">Dans la liste des applications, sélectionnez **O.C. Tanner - AppreciateHub**.</span><span class="sxs-lookup"><span data-stu-id="8282a-232">In the applications list, select **O.C. Tanner - AppreciateHub**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_app.png) 

3. <span data-ttu-id="8282a-234">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8282a-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="8282a-236">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="8282a-236">Click **Add** button.</span></span> <span data-ttu-id="8282a-237">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="8282a-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="8282a-239">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="8282a-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8282a-240">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8282a-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8282a-241">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="8282a-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8282a-242">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="8282a-242">Testing single sign-on</span></span>

<span data-ttu-id="8282a-243">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="8282a-243">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="8282a-244">Quand vous cliquez sur la vignette O.C.</span><span class="sxs-lookup"><span data-stu-id="8282a-244">When you click the O.C.</span></span> <span data-ttu-id="8282a-245">Tanner - AppreciateHub dans le volet d’accès, vous devez être connecté automatiquement à votre application O.C.</span><span class="sxs-lookup"><span data-stu-id="8282a-245">Tanner - AppreciateHub tile in the Access Panel, you should get automatically signed-on to your O.C.</span></span> <span data-ttu-id="8282a-246">Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="8282a-246">Tanner - AppreciateHub application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8282a-247">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="8282a-247">Additional resources</span></span>

* [<span data-ttu-id="8282a-248">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8282a-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8282a-249">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="8282a-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_08.png

[100]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_203.png

