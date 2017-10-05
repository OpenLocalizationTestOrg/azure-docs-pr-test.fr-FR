---
title: "Didacticiel : Intégration de Pluralsight à Azure Active Directory | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Pluralsight."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4c3f07d2-4e1f-4ea3-9025-c663f1f2b7b4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 62429643a108665544e42001d264046b5db1ec97
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pluralsight"></a><span data-ttu-id="92d72-103">Didacticiel : Intégration de Pluralsight à Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="92d72-103">Tutorial: Azure Active Directory integration with Pluralsight</span></span>

<span data-ttu-id="92d72-104">Dans ce didacticiel, vous allez apprendre à intégrer Pluralsight à Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="92d72-104">In this tutorial, you learn how to integrate Pluralsight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="92d72-105">L’intégration de Pluralsight à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="92d72-105">Integrating Pluralsight with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="92d72-106">Dans Azure AD, vous pouvez contrôler qui a accès à Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="92d72-106">You can control in Azure AD who has access to Pluralsight</span></span>
- <span data-ttu-id="92d72-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Pluralsight (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92d72-107">You can enable your users to automatically get signed-on to Pluralsight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="92d72-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="92d72-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="92d72-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="92d72-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92d72-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="92d72-110">Prerequisites</span></span>

<span data-ttu-id="92d72-111">Pour configurer l’intégration de Pluralsight à Azure AD, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="92d72-111">To configure Azure AD integration with Pluralsight, you need the following items:</span></span>

- <span data-ttu-id="92d72-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="92d72-112">An Azure AD subscription</span></span>
- <span data-ttu-id="92d72-113">Un abonnement Pluralsight pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="92d72-113">A Pluralsight single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="92d72-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="92d72-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="92d72-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="92d72-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="92d72-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="92d72-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="92d72-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="92d72-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="92d72-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="92d72-118">Scenario description</span></span>
<span data-ttu-id="92d72-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="92d72-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="92d72-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="92d72-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="92d72-121">Ajout de Pluralsight à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="92d72-121">Adding Pluralsight from the gallery</span></span>
2. <span data-ttu-id="92d72-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="92d72-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pluralsight-from-the-gallery"></a><span data-ttu-id="92d72-123">Ajout de Pluralsight à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="92d72-123">Adding Pluralsight from the gallery</span></span>
<span data-ttu-id="92d72-124">Pour configurer l’intégration de Pluralsight à Azure AD, vous devez ajouter Pluralsight depuis la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="92d72-124">To configure the integration of Pluralsight into Azure AD, you need to add Pluralsight from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="92d72-125">**Pour ajouter Pluralsight à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="92d72-125">**To add Pluralsight from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="92d72-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="92d72-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="92d72-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="92d72-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="92d72-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="92d72-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="92d72-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="92d72-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="92d72-133">Dans la zone de recherche, tapez **Pluralsight**.</span><span class="sxs-lookup"><span data-stu-id="92d72-133">In the search box, type **Pluralsight**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_search.png)

5. <span data-ttu-id="92d72-135">Dans le panneau des résultats, sélectionnez **Pluralsight**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="92d72-135">In the results panel, select **Pluralsight**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="92d72-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="92d72-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="92d72-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Pluralsight avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="92d72-138">In this section, you configure and test Azure AD single sign-on with Pluralsight based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="92d72-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Pluralsight équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92d72-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Pluralsight is to a user in Azure AD.</span></span> <span data-ttu-id="92d72-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Pluralsight associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="92d72-140">In other words, a link relationship between an Azure AD user and the related user in Pluralsight needs to be established.</span></span>

<span data-ttu-id="92d72-141">Dans Pluralsight, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="92d72-141">In Pluralsight, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="92d72-142">Pour configurer et tester l’authentification unique Azure AD avec Pluralsight, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="92d72-142">To configure and test Azure AD single sign-on with Pluralsight, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="92d72-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="92d72-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="92d72-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="92d72-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="92d72-145">**[Création d’un utilisateur de test Pluralsight](#creating-a-pluralsight-test-user)** pour obtenir un équivalent de Britta Simon dans Pluralsight lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="92d72-145">**[Creating a Pluralsight test user](#creating-a-pluralsight-test-user)** - to have a counterpart of Britta Simon in Pluralsight that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="92d72-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92d72-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="92d72-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="92d72-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="92d72-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="92d72-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="92d72-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="92d72-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Pluralsight application.</span></span>

<span data-ttu-id="92d72-150">**Pour configurer l’authentification unique Azure AD avec Pluralsight, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="92d72-150">**To configure Azure AD single sign-on with Pluralsight, perform the following steps:**</span></span>

1. <span data-ttu-id="92d72-151">Dans le Portail Azure, sur la page d’intégration de l’application **Pluralsight**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="92d72-151">In the Azure portal, on the **Pluralsight** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="92d72-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="92d72-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_samlbase.png)

3. <span data-ttu-id="92d72-155">Dans la section **Domaine et URL Pluralsight**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="92d72-155">On the **Pluralsight Domain and URLs** section, perform the following:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_url.png)

    <span data-ttu-id="92d72-157">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<instance name>.pluralsight.com/sso/<company name>`</span><span class="sxs-lookup"><span data-stu-id="92d72-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instance name>.pluralsight.com/sso/<company name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="92d72-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="92d72-158">This value is not real.</span></span> <span data-ttu-id="92d72-159">Mettez à jour cette valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="92d72-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="92d72-160">Contactez l’[équipe de support technique Pluralsight](mailto:support@pluralsight.com) pour obtenir cette valeur.</span><span class="sxs-lookup"><span data-stu-id="92d72-160">Contact [Pluralsight Client support team](mailto:support@pluralsight.com) to get this value.</span></span> 
 


4. <span data-ttu-id="92d72-161">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="92d72-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_certificate.png) 

5. <span data-ttu-id="92d72-163">L’objectif de cette section est d’activer l’authentification unique Azure AD dans le portail Azure et de la configurer dans l’application Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="92d72-163">The objective of this section is to enable Azure AD single sign-on in the Azure portal and to configure SSO in the Pluralsight application.</span></span>

    <span data-ttu-id="92d72-164">L’application Pluralsight s’attend à recevoir les assertions SAML dans un format spécifique, ce qui vous oblige à ajouter des mappages d’attributs personnalisés à votre configuration d’attributs de jeton SAML.</span><span class="sxs-lookup"><span data-stu-id="92d72-164">The Pluralsight application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="92d72-165">La capture d’écran suivante montre un exemple :</span><span class="sxs-lookup"><span data-stu-id="92d72-165">The following screenshot shows an example for this.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_attribute.png)

    >[!NOTE]
    ><span data-ttu-id="92d72-167">Vous pouvez également ajouter l’attribut **« Unique ID »** avec la valeur appropriée, comme EmployeeID ou autre valeur convenant à votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="92d72-167">You can also add the **"Unique ID"** attribute with the appropriate value like EmployeeID or something else which suits for your organization.</span></span> <span data-ttu-id="92d72-168">Notez qu’il ne s’agit pas de l’attribut nécessaire, mais qu’il peut être ajouté pour l’identification de l’utilisateur unique.</span><span class="sxs-lookup"><span data-stu-id="92d72-168">Also note that this is not the required attribute; however, you can add it to  identify the unique user.</span></span> 

6. <span data-ttu-id="92d72-169">Pour ajouter les **Attributs du jeton SAML**requis, pour chaque ligne indiquée dans le tableau ci-dessous, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="92d72-169">To add the required **SAML token attributes**, for each row shown in the table below, perform the following steps:</span></span>
   
   | <span data-ttu-id="92d72-170">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="92d72-170">Attribute Name</span></span> | <span data-ttu-id="92d72-171">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="92d72-171">Attribute Value</span></span> |
   | ---| --- |
   | <span data-ttu-id="92d72-172">Prénom</span><span class="sxs-lookup"><span data-stu-id="92d72-172">First Name</span></span> |<span data-ttu-id="92d72-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="92d72-173">user.givenname</span></span> |
   | <span data-ttu-id="92d72-174">Nom</span><span class="sxs-lookup"><span data-stu-id="92d72-174">Last Name</span></span> |<span data-ttu-id="92d72-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="92d72-175">user.surname</span></span> |
   | <span data-ttu-id="92d72-176">Email</span><span class="sxs-lookup"><span data-stu-id="92d72-176">Email</span></span> |<span data-ttu-id="92d72-177">user.mail</span><span class="sxs-lookup"><span data-stu-id="92d72-177">user.mail</span></span> |
   
   <span data-ttu-id="92d72-178">a.</span><span class="sxs-lookup"><span data-stu-id="92d72-178">a.</span></span> <span data-ttu-id="92d72-179">Cliquez sur **ajouter un attribut utilisateur** pour ouvrir la boîte de dialogue **Ajouter un attribut utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="92d72-179">Click **add user attribute** to open the **Add User Attribure** dialog.</span></span>
    
     ![Configurer l’authentification unique](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_addattribute.png)
  
   <span data-ttu-id="92d72-181">b.</span><span class="sxs-lookup"><span data-stu-id="92d72-181">b.</span></span> <span data-ttu-id="92d72-182">Dans la zone de texte **Nom de l’attribut** , indiquez le nom d’attribut pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="92d72-182">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
  
   <span data-ttu-id="92d72-183">c.</span><span class="sxs-lookup"><span data-stu-id="92d72-183">c.</span></span> <span data-ttu-id="92d72-184">Dans la liste **Valeur de l’attribut** , sélectionnez la valeur d’attribut pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="92d72-184">From the **Attribute Value** list, select the attribute value shown for that row.</span></span>
  
   <span data-ttu-id="92d72-185">d.</span><span class="sxs-lookup"><span data-stu-id="92d72-185">d.</span></span> <span data-ttu-id="92d72-186">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="92d72-186">Click **Ok**.</span></span>    

7. <span data-ttu-id="92d72-187">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="92d72-187">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pluralsight-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="92d72-189">Pour obtenir la configuration de l’authentification unique pour votre application, contactez l’équipe [Services professionnels de Pluralsight](mailTo:professionalservices@pluralsight.com) et envoyez-lui le fichier de métadonnées téléchargé.</span><span class="sxs-lookup"><span data-stu-id="92d72-189">To get SSO configured for your application, contact [Pluralsight Professional Services](mailTo:professionalservices@pluralsight.com) team and provide the downloaded metadata file.</span></span>

> [!TIP]
> <span data-ttu-id="92d72-190">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="92d72-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="92d72-191">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="92d72-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="92d72-192">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="92d72-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="92d72-193">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="92d72-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="92d72-194">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="92d72-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="92d72-196">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="92d72-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="92d72-197">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="92d72-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="92d72-199">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="92d72-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="92d72-201">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="92d72-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="92d72-203">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="92d72-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="92d72-205">a.</span><span class="sxs-lookup"><span data-stu-id="92d72-205">a.</span></span> <span data-ttu-id="92d72-206">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="92d72-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="92d72-207">b.</span><span class="sxs-lookup"><span data-stu-id="92d72-207">b.</span></span> <span data-ttu-id="92d72-208">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="92d72-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="92d72-209">c.</span><span class="sxs-lookup"><span data-stu-id="92d72-209">c.</span></span> <span data-ttu-id="92d72-210">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="92d72-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="92d72-211">d.</span><span class="sxs-lookup"><span data-stu-id="92d72-211">d.</span></span> <span data-ttu-id="92d72-212">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="92d72-212">Click **Create**.</span></span>
 
### <a name="creating-a-pluralsight-test-user"></a><span data-ttu-id="92d72-213">Création d’un utilisateur de test Pluralsight</span><span class="sxs-lookup"><span data-stu-id="92d72-213">Creating a Pluralsight test user</span></span>

<span data-ttu-id="92d72-214">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="92d72-214">The objective of this section is to create a user called Britta Simon in Pluralsight.</span></span> <span data-ttu-id="92d72-215">Contactez l’équipe du [support technique Pluralsight](mailto:support@pluralsight.com) pour ajouter des utilisateurs au compte Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="92d72-215">Please work with [Pluralsight Client support team](mailto:support@pluralsight.com) to add the users in the Pluralsight account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="92d72-216">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="92d72-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="92d72-217">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="92d72-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Pluralsight.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="92d72-219">**Pour affecter Britta Simon à Pluralsight, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="92d72-219">**To assign Britta Simon to Pluralsight, perform the following steps:**</span></span>

1. <span data-ttu-id="92d72-220">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="92d72-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="92d72-222">Dans la liste des applications, sélectionnez **Pluralsight**.</span><span class="sxs-lookup"><span data-stu-id="92d72-222">In the applications list, select **Pluralsight**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_app.png) 

3. <span data-ttu-id="92d72-224">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="92d72-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="92d72-226">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="92d72-226">Click **Add** button.</span></span> <span data-ttu-id="92d72-227">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="92d72-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="92d72-229">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="92d72-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="92d72-230">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="92d72-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="92d72-231">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="92d72-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="92d72-232">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="92d72-232">Testing single sign-on</span></span>

<span data-ttu-id="92d72-233">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="92d72-233">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="92d72-234">Quand vous cliquez sur la vignette Pluralsight dans le volet d’accès, vous êtes connecté automatiquement à votre application Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="92d72-234">When you click the Pluralsight tile in the Access Panel, you should get automatically signed-on to your Pluralsight application.</span></span> <span data-ttu-id="92d72-235">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="92d72-235">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="92d72-236">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="92d72-236">Additional resources</span></span>

* [<span data-ttu-id="92d72-237">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="92d72-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="92d72-238">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="92d72-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_203.png

