---
title: "Didacticiel : Intégration d’Azure Active Directory à ArcGIS Online | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et ArcGIS Online."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9e132a4-29e7-48bf-beb9-4148e617c8a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: df72270ca6443b456c079b22425f1660aa522389
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-arcgis-online"></a><span data-ttu-id="77b48-103">Didacticiel : Intégration d’Azure Active Directory à ArcGIS Online</span><span class="sxs-lookup"><span data-stu-id="77b48-103">Tutorial: Azure Active Directory integration with ArcGIS Online</span></span>

<span data-ttu-id="77b48-104">Dans ce didacticiel, vous allez apprendre à intégrer ArcGIS Online à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="77b48-104">In this tutorial, you learn how to integrate ArcGIS Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="77b48-105">L’intégration d’ArcGIS Online à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="77b48-105">Integrating ArcGIS Online with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="77b48-106">Dans Azure AD, vous pouvez contrôler qui a accès à ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="77b48-106">You can control in Azure AD who has access to ArcGIS Online</span></span>
- <span data-ttu-id="77b48-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à ArcGIS Online (authentification unique) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="77b48-107">You can enable your users to automatically get signed-on to ArcGIS Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="77b48-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="77b48-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="77b48-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="77b48-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with ArcGIS Online, it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in ArcGIS Online.

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="77b48-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="77b48-110">Prerequisites</span></span>

<span data-ttu-id="77b48-111">Pour configurer l’intégration d’Azure AD à ArcGIS Online, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="77b48-111">To configure Azure AD integration with ArcGIS Online, you need the following items:</span></span>

- <span data-ttu-id="77b48-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="77b48-112">An Azure AD subscription</span></span>
- <span data-ttu-id="77b48-113">Un abonnement ArcGIS Online pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="77b48-113">A ArcGIS Online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="77b48-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="77b48-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="77b48-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="77b48-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="77b48-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="77b48-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="77b48-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="77b48-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="77b48-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="77b48-118">Scenario description</span></span>
<span data-ttu-id="77b48-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="77b48-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="77b48-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="77b48-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="77b48-121">Ajout d’ArcGIS Online à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="77b48-121">Adding ArcGIS Online from the gallery</span></span>
2. <span data-ttu-id="77b48-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="77b48-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-arcgis-online-from-the-gallery"></a><span data-ttu-id="77b48-123">Ajout d’ArcGIS Online à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="77b48-123">Adding ArcGIS Online from the gallery</span></span>
<span data-ttu-id="77b48-124">Pour configurer l’intégration d’ArcGIS Online à Azure AD, vous devez ajouter ArcGIS Online à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="77b48-124">To configure the integration of ArcGIS Online into Azure AD, you need to add ArcGIS Online from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="77b48-125">**Pour ajouter ArcGIS Online à partir de la galerie, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="77b48-125">**To add ArcGIS Online from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="77b48-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="77b48-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="77b48-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="77b48-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="77b48-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="77b48-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="77b48-131">Pour ajouter la nouvelle application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="77b48-131">Click **New application** button on the top of the dialog to add new application.</span></span>

    ![Applications][3]

4. <span data-ttu-id="77b48-133">Dans la zone de recherche, tapez **ArcGIS Online**.</span><span class="sxs-lookup"><span data-stu-id="77b48-133">In the search box, type **ArcGIS Online**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_search.png)

5. <span data-ttu-id="77b48-135">Dans le volet de résultats, sélectionnez **ArcGIS Online**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="77b48-135">In the results panel, select **ArcGIS Online**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="77b48-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="77b48-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="77b48-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec ArcGIS Online sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="77b48-138">In this section, you configure and test Azure AD single sign-on with ArcGIS Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="77b48-139">Pour que l’authentification unique fonctionne, Azure AD doit connaître l’utilisateur ArcGIS Online correspondant à l’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="77b48-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ArcGIS Online is to a user in Azure AD.</span></span> <span data-ttu-id="77b48-140">En d’autres termes, une relation doit être établie entre l’utilisateur Azure AD et l’utilisateur ArcGIS Online associé.</span><span class="sxs-lookup"><span data-stu-id="77b48-140">In other words, a link relationship between an Azure AD user and the related user in ArcGIS Online needs to be established.</span></span>

<span data-ttu-id="77b48-141">Pour cela, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** dans ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="77b48-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ArcGIS Online.</span></span>

<span data-ttu-id="77b48-142">Pour configurer et tester l’authentification unique Azure AD avec ArcGIS Online, vous devez suivre les instructions des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="77b48-142">To configure and test Azure AD single sign-on with ArcGIS Online, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="77b48-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="77b48-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="77b48-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="77b48-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="77b48-145">**[Création d’un utilisateur de test ArcGIS Online](#creating-an-arcgis-online-test-user)** pour avoir dans ArcGIS Online un équivalent de Britta Simon lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="77b48-145">**[Creating an ArcGIS Online test user](#creating-an-arcgis-online-test-user)** - to have a counterpart of Britta Simon in ArcGIS Online that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="77b48-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="77b48-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="77b48-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="77b48-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="77b48-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="77b48-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="77b48-149">Dans cette section, vous activez l’authentification unique Azure AD dans le portail Azure et configurez l’authentification unique dans votre application ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="77b48-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ArcGIS Online application.</span></span>

<span data-ttu-id="77b48-150">**Pour configurer l’authentification unique Azure AD avec ArcGIS Online, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="77b48-150">**To configure Azure AD single sign-on with ArcGIS Online, perform the following steps:**</span></span>

1. <span data-ttu-id="77b48-151">Dans le portail Azure, dans la page d’intégration de l’application **ArcGIS Online**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="77b48-151">In the Azure portal, on the **ArcGIS Online** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="77b48-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="77b48-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_samlbase.png)

3. <span data-ttu-id="77b48-155">Dans la section **Domaine et URL ArcGIS Online**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="77b48-155">On the **ArcGIS Online Domain and URLs** section, perform the following step:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_url.png)

    <span data-ttu-id="77b48-157">Dans la zone de texte **URL de connexion**, tapez la valeur au format suivant : `https://<company>.maps.arcgis.com`</span><span class="sxs-lookup"><span data-stu-id="77b48-157">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<company>.maps.arcgis.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="77b48-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="77b48-158">This value is not the real.</span></span> <span data-ttu-id="77b48-159">Mettez à jour cette valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="77b48-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="77b48-160">Pour obtenir cette valeur, contactez [l’équipe du support ArcGIS Online](http://support.esri.com/).</span><span class="sxs-lookup"><span data-stu-id="77b48-160">Contact [ArcGIS Online Client support team](http://support.esri.com/) to get this value.</span></span> 

4. <span data-ttu-id="77b48-161">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier XML sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="77b48-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_certificate.png) 

5. <span data-ttu-id="77b48-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="77b48-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-arcgis-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="77b48-165">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise ArcGIS en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="77b48-165">In a different web browser window, log into your ArcGIS company site as an administrator.</span></span>

7. <span data-ttu-id="77b48-166">Cliquez sur **Edit Settings** (Modifier les paramètres).</span><span class="sxs-lookup"><span data-stu-id="77b48-166">Click **EDIT SETTINGS**.</span></span>

    <span data-ttu-id="77b48-167">![Modifier les paramètres](./media/active-directory-saas-arcgis-tutorial/ic784742.png "Modifier les paramètres")</span><span class="sxs-lookup"><span data-stu-id="77b48-167">![Edit Settings](./media/active-directory-saas-arcgis-tutorial/ic784742.png "Edit Settings")</span></span>

8. <span data-ttu-id="77b48-168">Cliquez sur **Sécurité**.</span><span class="sxs-lookup"><span data-stu-id="77b48-168">Click **Security**.</span></span>

    <span data-ttu-id="77b48-169">![Sécurité](./media/active-directory-saas-arcgis-tutorial/ic784743.png "Sécurité")</span><span class="sxs-lookup"><span data-stu-id="77b48-169">![Security](./media/active-directory-saas-arcgis-tutorial/ic784743.png "Security")</span></span>

9. <span data-ttu-id="77b48-170">Sous **Enterprise Logins** (Informations de connexion entreprise), cliquez sur **Set Identity Provider** (Définir un fournisseur d’identité).</span><span class="sxs-lookup"><span data-stu-id="77b48-170">Under **Enterprise Logins**, click **SET IDENTITY PROVIDER**.</span></span>

    <span data-ttu-id="77b48-171">![Connexions de l’entreprise](./media/active-directory-saas-arcgis-tutorial/ic784744.png "Connexions de l’entreprise")</span><span class="sxs-lookup"><span data-stu-id="77b48-171">![Enterprise Logins](./media/active-directory-saas-arcgis-tutorial/ic784744.png "Enterprise Logins")</span></span>

10. <span data-ttu-id="77b48-172">Dans la page de configuration **Set Identity Provider** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="77b48-172">On the **Set Identity Provider** configuration page, perform the following steps:</span></span>
   
    <span data-ttu-id="77b48-173">![Définir le fournisseur d’identité](./media/active-directory-saas-arcgis-tutorial/ic784745.png "Définir le fournisseur d’identité")</span><span class="sxs-lookup"><span data-stu-id="77b48-173">![Set Identity Provider](./media/active-directory-saas-arcgis-tutorial/ic784745.png "Set Identity Provider")</span></span>
   
    <span data-ttu-id="77b48-174">a.</span><span class="sxs-lookup"><span data-stu-id="77b48-174">a.</span></span> <span data-ttu-id="77b48-175">Dans la zone de texte **Name** (Nom), tapez le nom de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="77b48-175">In the **Name** textbox, type your organization’s name.</span></span>

    <span data-ttu-id="77b48-176">b.</span><span class="sxs-lookup"><span data-stu-id="77b48-176">b.</span></span> <span data-ttu-id="77b48-177">Pour **Metadata for the Enterprise Identity Provider will be supplied using**, sélectionnez **A File**.</span><span class="sxs-lookup"><span data-stu-id="77b48-177">For **Metadata for the Enterprise Identity Provider will be supplied using**, select **A File**.</span></span>

    <span data-ttu-id="77b48-178">c.</span><span class="sxs-lookup"><span data-stu-id="77b48-178">c.</span></span> <span data-ttu-id="77b48-179">Pour télécharger votre fichier de métadonnées, cliquez sur **Choose file**.</span><span class="sxs-lookup"><span data-stu-id="77b48-179">To upload your downloaded metadata file, click **Choose file**.</span></span>

    <span data-ttu-id="77b48-180">d.</span><span class="sxs-lookup"><span data-stu-id="77b48-180">d.</span></span> <span data-ttu-id="77b48-181">Cliquez sur **Set Identity Provider** (Définir un fournisseur d’identité).</span><span class="sxs-lookup"><span data-stu-id="77b48-181">Click **SET IDENTITY PROVIDER**.</span></span>

> [!TIP]
> <span data-ttu-id="77b48-182">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="77b48-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="77b48-183">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="77b48-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="77b48-184">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="77b48-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="77b48-185">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="77b48-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="77b48-186">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="77b48-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="77b48-188">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="77b48-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="77b48-189">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="77b48-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="77b48-191">Accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs** pour afficher la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="77b48-191">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="77b48-193">En haut de la boîte de dialogue, cliquez sur **Ajouter** pour ouvrir la boîte de dialogue **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="77b48-193">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="77b48-195">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="77b48-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="77b48-197">a.</span><span class="sxs-lookup"><span data-stu-id="77b48-197">a.</span></span> <span data-ttu-id="77b48-198">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="77b48-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="77b48-199">b.</span><span class="sxs-lookup"><span data-stu-id="77b48-199">b.</span></span> <span data-ttu-id="77b48-200">Dans la zone de texte **Nom d’utilisateur** , tapez l’**adresse de messagerie** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="77b48-200">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="77b48-201">c.</span><span class="sxs-lookup"><span data-stu-id="77b48-201">c.</span></span> <span data-ttu-id="77b48-202">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="77b48-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="77b48-203">d.</span><span class="sxs-lookup"><span data-stu-id="77b48-203">d.</span></span> <span data-ttu-id="77b48-204">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="77b48-204">Click **Create**.</span></span>
 
### <a name="creating-an-arcgis-online-test-user"></a><span data-ttu-id="77b48-205">Création d’un utilisateur de test ArcGIS Online</span><span class="sxs-lookup"><span data-stu-id="77b48-205">Creating an ArcGIS Online test user</span></span>

<span data-ttu-id="77b48-206">Pour permettre aux utilisateurs Azure AD de se connecter à ArcGIS Online, vous devez les attribuer dans ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="77b48-206">In order to enable Azure AD users to log into ArcGIS Online, they must be provisioned into ArcGIS Online.</span></span>  
<span data-ttu-id="77b48-207">Pour ArcGIS Online, cette attribution s’effectue manuellement.</span><span class="sxs-lookup"><span data-stu-id="77b48-207">In the case of ArcGIS Online, provisioning is a manual task.</span></span>

<span data-ttu-id="77b48-208">**Pour approvisionner un compte d’utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="77b48-208">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="77b48-209">Connectez-vous à votre locataire **ArcGIS** .</span><span class="sxs-lookup"><span data-stu-id="77b48-209">Log in to your **ArcGIS** tenant.</span></span>

2. <span data-ttu-id="77b48-210">Cliquez sur **Invite Members** (Inviter des membres).</span><span class="sxs-lookup"><span data-stu-id="77b48-210">Click **INVITE MEMBERS**.</span></span>
   
    <span data-ttu-id="77b48-211">![Inviter des membres](./media/active-directory-saas-arcgis-tutorial/ic784747.png "Inviter des membres")</span><span class="sxs-lookup"><span data-stu-id="77b48-211">![Invite Members](./media/active-directory-saas-arcgis-tutorial/ic784747.png "Invite Members")</span></span>

3. <span data-ttu-id="77b48-212">Sélectionnez **Add members automatically without sending an email** (Ajouter des membres automatiquement sans envoyer d’e-mail), puis cliquez sur **Next** (Suivant).</span><span class="sxs-lookup"><span data-stu-id="77b48-212">Select **Add members automatically without sending an email**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="77b48-213">![Ajouter des membres automatiquement](./media/active-directory-saas-arcgis-tutorial/ic784748.png "Ajouter des membres automatiquement")</span><span class="sxs-lookup"><span data-stu-id="77b48-213">![Add Members Automatically](./media/active-directory-saas-arcgis-tutorial/ic784748.png "Add Members Automatically")</span></span>

4. <span data-ttu-id="77b48-214">Dans la page de boîte de dialogue **Members** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="77b48-214">On the **Members** dialog page, perform the following steps:</span></span>
   
     <span data-ttu-id="77b48-215">![Ajouter et vérifier](./media/active-directory-saas-arcgis-tutorial/ic784749.png "Ajouter et vérifier")</span><span class="sxs-lookup"><span data-stu-id="77b48-215">![Add and review](./media/active-directory-saas-arcgis-tutorial/ic784749.png "Add and review")</span></span>
    
     <span data-ttu-id="77b48-216">a.</span><span class="sxs-lookup"><span data-stu-id="77b48-216">a.</span></span> <span data-ttu-id="77b48-217">Entrez **l’adresse e-mail**, le **prénom** et le **nom** d’un compte Azure AD valide que vous voulez attribuer.</span><span class="sxs-lookup"><span data-stu-id="77b48-217">Enter the **Email**, **First Name**, and **Last Name** of a valid AAD account you want to provision.</span></span>
  
     <span data-ttu-id="77b48-218">b.</span><span class="sxs-lookup"><span data-stu-id="77b48-218">b.</span></span> <span data-ttu-id="77b48-219">Cliquez sur **Add And Review** (Ajouter et vérifier).</span><span class="sxs-lookup"><span data-stu-id="77b48-219">Click **ADD AND REVIEW**.</span></span>
5. <span data-ttu-id="77b48-220">Passez en revue les données que vous avez entrées, puis cliquez sur **Add Members** (Ajouter des membres).</span><span class="sxs-lookup"><span data-stu-id="77b48-220">Review the data you have entered, and then click **ADD MEMBERS**.</span></span>
   
    <span data-ttu-id="77b48-221">![Ajouter un membre](./media/active-directory-saas-arcgis-tutorial/ic784750.png "Ajouter un membre")</span><span class="sxs-lookup"><span data-stu-id="77b48-221">![Add member](./media/active-directory-saas-arcgis-tutorial/ic784750.png "Add member")</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="77b48-222">Le titulaire du compte Azure Active Directory reçoit un message électronique contenant un lien à suivre pour confirmer son compte et l’activer.</span><span class="sxs-lookup"><span data-stu-id="77b48-222">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="77b48-223">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="77b48-223">Assigning the Azure AD test user</span></span>

<span data-ttu-id="77b48-224">Dans cette section, vous autorisez Britta Simon à utiliser l’authentification unique Azure en accordant l’accès à ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="77b48-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ArcGIS Online.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="77b48-226">**Pour attribuer Britta Simon à ArcGIS Online, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="77b48-226">**To assign Britta Simon to ArcGIS Online, perform the following steps:**</span></span>

1. <span data-ttu-id="77b48-227">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="77b48-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="77b48-229">Dans la liste des applications, sélectionnez **ArcGIS Online**.</span><span class="sxs-lookup"><span data-stu-id="77b48-229">In the applications list, select **ArcGIS Online**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_app.png) 

3. <span data-ttu-id="77b48-231">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="77b48-231">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="77b48-233">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="77b48-233">Click **Add** button.</span></span> <span data-ttu-id="77b48-234">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="77b48-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="77b48-236">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="77b48-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="77b48-237">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="77b48-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="77b48-238">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="77b48-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="77b48-239">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="77b48-239">Testing single sign-on</span></span>

<span data-ttu-id="77b48-240">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="77b48-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="77b48-241">Quand vous cliquez sur la vignette ArcGIS Online dans le volet d’accès, vous devez être authentifié automatiquement auprès de votre application ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="77b48-241">When you click the ArcGIS Online tile in the Access Panel, you should get automatically signed-on to your ArcGIS Online application.</span></span>
<span data-ttu-id="77b48-242">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="77b48-242">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="77b48-243">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="77b48-243">Additional resources</span></span>

* [<span data-ttu-id="77b48-244">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="77b48-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="77b48-245">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="77b48-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_203.png

