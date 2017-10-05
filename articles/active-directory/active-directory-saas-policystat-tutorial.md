---
title: "Didacticiel : Intégration d’Azure Active Directory avec PolicyStat | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et PolicyStat."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: af5eb0f1-1c8e-4809-b0c4-8ccfb915ca42
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 704afd5515b02ce2a4fbf35da65fad74dc506271
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-policystat"></a><span data-ttu-id="1142c-103">Didacticiel : Intégration d’Azure Active Directory avec PolicyStat</span><span class="sxs-lookup"><span data-stu-id="1142c-103">Tutorial: Azure Active Directory integration with PolicyStat</span></span>

<span data-ttu-id="1142c-104">Dans ce didacticiel, vous allez apprendre à intégrer PolicyStat avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1142c-104">In this tutorial, you learn how to integrate PolicyStat with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1142c-105">L’intégration de PolicyStat avec Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="1142c-105">Integrating PolicyStat with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1142c-106">Vous pouvez contrôler dans Azure AD qui a accès à PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="1142c-106">You can control in Azure AD who has access to PolicyStat</span></span>
- <span data-ttu-id="1142c-107">Vous pouvez permettre à vos utilisateurs d’être automatiquement connectés à PolicyStat (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1142c-107">You can enable your users to automatically get signed-on to PolicyStat (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1142c-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1142c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1142c-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1142c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1142c-110">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="1142c-110">Prerequisites</span></span>

<span data-ttu-id="1142c-111">Pour configurer l’intégration d’Azure AD avec PolicyStat, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1142c-111">To configure Azure AD integration with PolicyStat, you need the following items:</span></span>

- <span data-ttu-id="1142c-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="1142c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1142c-113">Un abonnement PolicyStat pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="1142c-113">A PolicyStat single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1142c-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="1142c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1142c-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1142c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1142c-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="1142c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1142c-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1142c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1142c-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="1142c-118">Scenario description</span></span>
<span data-ttu-id="1142c-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="1142c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1142c-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="1142c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1142c-121">Ajout de PolicyStat à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="1142c-121">Adding PolicyStat from the gallery</span></span>
2. <span data-ttu-id="1142c-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1142c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-policystat-from-the-gallery"></a><span data-ttu-id="1142c-123">Ajout de PolicyStat à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="1142c-123">Adding PolicyStat from the gallery</span></span>
<span data-ttu-id="1142c-124">Pour configurer l’intégration de PolicyStat à Azure AD, vous devez ajouter PolicyStat à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="1142c-124">To configure the integration of PolicyStat into Azure AD, you need to add PolicyStat from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1142c-125">**Pour ajouter PolicyStat à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1142c-125">**To add PolicyStat from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1142c-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1142c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1142c-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="1142c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1142c-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1142c-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="1142c-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1142c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="1142c-133">Dans la zone de recherche, tapez **PolicyStat**.</span><span class="sxs-lookup"><span data-stu-id="1142c-133">In the search box, type **PolicyStat**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_search.png)

5. <span data-ttu-id="1142c-135">Dans le volet de résultats, sélectionnez **PolicyStat**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="1142c-135">In the results panel, select **PolicyStat**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1142c-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1142c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1142c-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec PolicyStat sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="1142c-138">In this section, you configure and test Azure AD single sign-on with PolicyStat based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1142c-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur PolicyStat équivalent à l’utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1142c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PolicyStat is to a user in Azure AD.</span></span> <span data-ttu-id="1142c-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur PolicyStat associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="1142c-140">In other words, a link relationship between an Azure AD user and the related user in PolicyStat needs to be established.</span></span>

<span data-ttu-id="1142c-141">Dans PolicyStat, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur **Nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="1142c-141">In PolicyStat, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1142c-142">Pour configurer et tester l’authentification unique Azure AD avec PolicyStat, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="1142c-142">To configure and test Azure AD single sign-on with PolicyStat, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1142c-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="1142c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1142c-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1142c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1142c-145">**[Création d’un utilisateur de test PolicyStat](#creating-a-policystat-test-user)** pour obtenir un équivalent de Britta Simon dans PolicyStat lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="1142c-145">**[Creating a PolicyStat test user](#creating-a-policystat-test-user)** - to have a counterpart of Britta Simon in PolicyStat that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1142c-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1142c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1142c-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="1142c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1142c-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1142c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1142c-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="1142c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PolicyStat application.</span></span>

<span data-ttu-id="1142c-150">**Pour configurer l’authentification unique Azure AD avec PolicyStat, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1142c-150">**To configure Azure AD single sign-on with PolicyStat, perform the following steps:**</span></span>

1. <span data-ttu-id="1142c-151">Dans le portail Azure, sur la page d’intégration de l’application **PolicyStat**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="1142c-151">In the Azure portal, on the **PolicyStat** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="1142c-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="1142c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_samlbase.png)

3. <span data-ttu-id="1142c-155">Dans la section **Domaine et URL PolicyStat**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1142c-155">On the **PolicyStat Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_url.png)

    <span data-ttu-id="1142c-157">a.</span><span class="sxs-lookup"><span data-stu-id="1142c-157">a.</span></span> <span data-ttu-id="1142c-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<companyname>.policystat.com`</span><span class="sxs-lookup"><span data-stu-id="1142c-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.policystat.com`</span></span>

    <span data-ttu-id="1142c-159">b.</span><span class="sxs-lookup"><span data-stu-id="1142c-159">b.</span></span> <span data-ttu-id="1142c-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<companyname>.policystat.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="1142c-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.policystat.com/saml2/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1142c-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="1142c-161">These values are not real.</span></span> <span data-ttu-id="1142c-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="1142c-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1142c-163">Pour obtenir ces valeurs, contactez l’[équipe de support technique PolicyStat](http://www.policystat.com/support/).</span><span class="sxs-lookup"><span data-stu-id="1142c-163">Contact [PolicyStat Client support team](http://www.policystat.com/support/) to get these values.</span></span> 
 
4. <span data-ttu-id="1142c-164">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1142c-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_certificate.png) 

5. <span data-ttu-id="1142c-166">Cette section explique comment permettre aux utilisateurs de s’authentifier sur PolicyStat avec leur compte Azure AD en utilisant la fédération basée sur le protocole SAML.</span><span class="sxs-lookup"><span data-stu-id="1142c-166">The objective of this section is to outline how to enable users to authenticate to PolicyStat with their account in Azure AD using federation based on the SAML protocol.</span></span>

    <span data-ttu-id="1142c-167">L’application PolicyStat s’attend à recevoir les assertions SAML dans un format spécifique, ce qui vous oblige à ajouter des mappages d’attributs personnalisés à votre configuration **Attributs du jeton SAML**.</span><span class="sxs-lookup"><span data-stu-id="1142c-167">The PolicyStat application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **SAML Token Attributes** configuration.</span></span>  

     <span data-ttu-id="1142c-168">La capture d’écran suivante présente un exemple de cette opération.</span><span class="sxs-lookup"><span data-stu-id="1142c-168">The following screenshot shows an example of this.</span></span>

     <span data-ttu-id="1142c-169">![Attributs](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "Attributs")</span><span class="sxs-lookup"><span data-stu-id="1142c-169">![Attributes](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "Attributes")</span></span>

6. <span data-ttu-id="1142c-170">Pour ajouter les mappages d’attribut requis, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1142c-170">To add the required attribute mappings, perform the following steps:</span></span>

    | <span data-ttu-id="1142c-171">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="1142c-171">Attribute Name</span></span>    |   <span data-ttu-id="1142c-172">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="1142c-172">Attribute Value</span></span> |
    |------------------- | -------------------- |
    | <span data-ttu-id="1142c-173">uid</span><span class="sxs-lookup"><span data-stu-id="1142c-173">uid</span></span> | <span data-ttu-id="1142c-174">ExtractMailPrefix([mail])</span><span class="sxs-lookup"><span data-stu-id="1142c-174">ExtractMailPrefix([mail])</span></span> |
    
    <span data-ttu-id="1142c-175">a.</span><span class="sxs-lookup"><span data-stu-id="1142c-175">a.</span></span> <span data-ttu-id="1142c-176">Cliquez sur **Ajouter un attribut** pour ouvrir la boîte de dialogue **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="1142c-176">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addatribute.png)
    
    <span data-ttu-id="1142c-179">b.</span><span class="sxs-lookup"><span data-stu-id="1142c-179">b.</span></span> <span data-ttu-id="1142c-180">Dans la zone de texte **Nom de l’attribut**, entrez **uid**.</span><span class="sxs-lookup"><span data-stu-id="1142c-180">In the **Attribute Name** textbox, type **uid**.</span></span>

    <span data-ttu-id="1142c-181">c.</span><span class="sxs-lookup"><span data-stu-id="1142c-181">c.</span></span> <span data-ttu-id="1142c-182">Dans la zone de texte **Valeur de l’attribut**, sélectionnez **ExtractMailPrefix()**.</span><span class="sxs-lookup"><span data-stu-id="1142c-182">In the **Attribute Value** textbox, select **ExtractMailPrefix()**.</span></span>    
   
    <span data-ttu-id="1142c-183">d.</span><span class="sxs-lookup"><span data-stu-id="1142c-183">d.</span></span> <span data-ttu-id="1142c-184">Dans la liste **Mail**, sélectionnez **User.mail**.</span><span class="sxs-lookup"><span data-stu-id="1142c-184">From the **Mail** list, select **User.mail**.</span></span>
    
    <span data-ttu-id="1142c-185">e.</span><span class="sxs-lookup"><span data-stu-id="1142c-185">e.</span></span> <span data-ttu-id="1142c-186">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="1142c-186">Click **Ok**</span></span>

7. <span data-ttu-id="1142c-187">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="1142c-187">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-policystat-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="1142c-189">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise PolicyStat en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="1142c-189">In a different web browser window, log into your PolicyStat company site as an administrator.</span></span>

9. <span data-ttu-id="1142c-190">Cliquez sur l’onglet **Admin**, puis sur **Single Sign-On Configuration** dans le volet de navigation de gauche.</span><span class="sxs-lookup"><span data-stu-id="1142c-190">Click the **Admin** tab, and then click **Single Sign-On Configuration** in left navigation pane.</span></span>
   
    <span data-ttu-id="1142c-191">![Menu administrateur](./media/active-directory-saas-policystat-tutorial/ic808633.png "Menu administrateur")</span><span class="sxs-lookup"><span data-stu-id="1142c-191">![Administrator Menu](./media/active-directory-saas-policystat-tutorial/ic808633.png "Administrator Menu")</span></span>

10. <span data-ttu-id="1142c-192">Dans la section **Setup**, sélectionnez **Enable Single Sign-on Integration**.</span><span class="sxs-lookup"><span data-stu-id="1142c-192">In the **Setup** section, select **Enable Single Sign-on Integration**.</span></span>
   
    <span data-ttu-id="1142c-193">![Configuration de l’authentification unique](./media/active-directory-saas-policystat-tutorial/ic808634.png "Configuration de l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="1142c-193">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808634.png "Single Sign-On Configuration")</span></span>

11. <span data-ttu-id="1142c-194">Cliquez sur **Configure Attributes**, puis, dans la section **Configure Attributes**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1142c-194">Click **Configure Attributes**, and then, in the **Configure Attributes** section, perform the following steps:</span></span>
   
    <span data-ttu-id="1142c-195">![Configuration de l’authentification unique](./media/active-directory-saas-policystat-tutorial/ic808635.png "Configuration de l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="1142c-195">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808635.png "Single Sign-On Configuration")</span></span>
   
    <span data-ttu-id="1142c-196">a.</span><span class="sxs-lookup"><span data-stu-id="1142c-196">a.</span></span> <span data-ttu-id="1142c-197">Dans la zone de texte **Username Attribute**, entrez **uid**.</span><span class="sxs-lookup"><span data-stu-id="1142c-197">In the **Username Attribute** textbox, type **uid**.</span></span>

    <span data-ttu-id="1142c-198">b.</span><span class="sxs-lookup"><span data-stu-id="1142c-198">b.</span></span> <span data-ttu-id="1142c-199">Dans la zone de texte **First Name Attribute**, entrez la valeur **firstname** de l’utilisateur **Britta**.</span><span class="sxs-lookup"><span data-stu-id="1142c-199">In the **First Name Attribute** textbox, type **firstname** of user **Britta**.</span></span>

    <span data-ttu-id="1142c-200">c.</span><span class="sxs-lookup"><span data-stu-id="1142c-200">c.</span></span> <span data-ttu-id="1142c-201">Dans la zone de texte **Last Name Attribute**, entrez la valeur **lastname** de l’utilisateur **Simon**.</span><span class="sxs-lookup"><span data-stu-id="1142c-201">In the **Last Name Attribute** textbox, type **lastname** of user **Simon**.</span></span>

    <span data-ttu-id="1142c-202">d.</span><span class="sxs-lookup"><span data-stu-id="1142c-202">d.</span></span> <span data-ttu-id="1142c-203">Dans la zone de texte **Email Attribute**, entrez la valeur **emailaddress** de l’utilisateur **BrittaSimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="1142c-203">In the **Email Attribute** textbox, type **emailaddress** of user **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="1142c-204">e.</span><span class="sxs-lookup"><span data-stu-id="1142c-204">e.</span></span> <span data-ttu-id="1142c-205">Cliquez sur **Enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="1142c-205">Click **Save Changes**.</span></span>

12. <span data-ttu-id="1142c-206">Cliquez sur **Your IDP Metadata**, puis, dans la section **Your IDP Metadata**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1142c-206">Click **Your IDP Metadata**, and then, in the **Your IDP Metadata** section, perform the following steps:</span></span>
   
    <span data-ttu-id="1142c-207">![Configuration de l’authentification unique](./media/active-directory-saas-policystat-tutorial/ic808636.png "Configuration de l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="1142c-207">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808636.png "Single Sign-On Configuration")</span></span>
   
    <span data-ttu-id="1142c-208">a.</span><span class="sxs-lookup"><span data-stu-id="1142c-208">a.</span></span> <span data-ttu-id="1142c-209">Ouvrez votre fichier de métadonnées téléchargé, copiez son contenu, puis collez-le dans la zone de texte **Your Identity Provider Metadata**.</span><span class="sxs-lookup"><span data-stu-id="1142c-209">Open your downloaded metadata file, copy the content, and  then paste it into the **Your Identity Provider Metadata** textbox.</span></span>

    <span data-ttu-id="1142c-210">b.</span><span class="sxs-lookup"><span data-stu-id="1142c-210">b.</span></span> <span data-ttu-id="1142c-211">Cliquez sur **Enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="1142c-211">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="1142c-212">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="1142c-212">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1142c-213">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="1142c-213">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1142c-214">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1142c-214">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1142c-215">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1142c-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="1142c-216">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1142c-216">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="1142c-218">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1142c-218">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1142c-219">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1142c-219">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1142c-221">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="1142c-221">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1142c-223">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1142c-223">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1142c-225">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1142c-225">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1142c-227">a.</span><span class="sxs-lookup"><span data-stu-id="1142c-227">a.</span></span> <span data-ttu-id="1142c-228">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1142c-228">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1142c-229">b.</span><span class="sxs-lookup"><span data-stu-id="1142c-229">b.</span></span> <span data-ttu-id="1142c-230">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1142c-230">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1142c-231">c.</span><span class="sxs-lookup"><span data-stu-id="1142c-231">c.</span></span> <span data-ttu-id="1142c-232">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="1142c-232">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1142c-233">d.</span><span class="sxs-lookup"><span data-stu-id="1142c-233">d.</span></span> <span data-ttu-id="1142c-234">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="1142c-234">Click **Create**.</span></span>
 
### <a name="creating-a-policystat-test-user"></a><span data-ttu-id="1142c-235">Création d’un utilisateur de test PolicyStat</span><span class="sxs-lookup"><span data-stu-id="1142c-235">Creating a PolicyStat test user</span></span>

<span data-ttu-id="1142c-236">Pour permettre aux utilisateurs Azure AD de se connecter à PolicyStat, vous devez les approvisionner dans PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="1142c-236">In order to enable Azure AD users to log into PolicyStat, they must be provisioned into PolicyStat.</span></span>  

<span data-ttu-id="1142c-237">PolicyStat prend en charge l’approvisionnement juste-à-temps des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="1142c-237">PolicyStat supports just in time user provisioning.</span></span> <span data-ttu-id="1142c-238">Il est donc inutile d’ajouter les utilisateurs manuellement à PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="1142c-238">This means, you do not need to add the users manually to PolicyStat.</span></span> <span data-ttu-id="1142c-239">Les utilisateurs seront ajoutés automatiquement à leur première connexion à l’aide de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="1142c-239">The users will get added automatically on their first login through SSO.</span></span>

>[!NOTE]
><span data-ttu-id="1142c-240">Vous pouvez utiliser n’importe quel outil ou API de création de compte utilisateur, fourni par PolicyStat, pour approvisionner des comptes utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1142c-240">You can use any other PolicyStat user account creation tools or APIs provided by PolicyStat to provision Azure AD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1142c-241">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1142c-241">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1142c-242">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="1142c-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PolicyStat.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="1142c-244">**Pour affecter Britta Simon à PolicyStat, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1142c-244">**To assign Britta Simon to PolicyStat, perform the following steps:**</span></span>

1. <span data-ttu-id="1142c-245">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1142c-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="1142c-247">Dans la liste des applications, sélectionnez **PolicyStat**.</span><span class="sxs-lookup"><span data-stu-id="1142c-247">In the applications list, select **PolicyStat**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_app.png) 

3. <span data-ttu-id="1142c-249">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1142c-249">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="1142c-251">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="1142c-251">Click **Add** button.</span></span> <span data-ttu-id="1142c-252">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1142c-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="1142c-254">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="1142c-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1142c-255">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1142c-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1142c-256">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1142c-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1142c-257">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="1142c-257">Testing single sign-on</span></span>

<span data-ttu-id="1142c-258">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="1142c-258">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1142c-259">Quand vous cliquez sur la vignette PolicyStat dans le volet d’accès, vous êtes connecté automatiquement à votre application PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="1142c-259">When you click the PolicyStat tile in the Access Panel, you should get automatically signed-on to your PolicyStat application.</span></span>
<span data-ttu-id="1142c-260">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1142c-260">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1142c-261">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="1142c-261">Additional resources</span></span>

* [<span data-ttu-id="1142c-262">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1142c-262">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1142c-263">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="1142c-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_203.png

