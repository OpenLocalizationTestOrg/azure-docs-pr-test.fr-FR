---
title: "Didacticiel : intégration d’Azure Active Directory à Panopto | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Panopto."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 89c88e23-93ce-4970-9baa-1104c4e8fe4a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 725fba1227cfc9c4850f9e2d6fd0b13e88eafa20
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-panopto"></a><span data-ttu-id="0b850-103">Didacticiel : Intégration d’Azure Active Directory à Panopto</span><span class="sxs-lookup"><span data-stu-id="0b850-103">Tutorial: Azure Active Directory integration with Panopto</span></span>

<span data-ttu-id="0b850-104">Dans ce didacticiel, vous allez apprendre à intégrer Panopto à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0b850-104">In this tutorial, you learn how to integrate Panopto with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0b850-105">L’intégration de Panopto à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="0b850-105">Integrating Panopto with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0b850-106">Dans Azure AD, vous pouvez contrôler qui a accès à Panopto.</span><span class="sxs-lookup"><span data-stu-id="0b850-106">You can control in Azure AD who has access to Panopto</span></span>
- <span data-ttu-id="0b850-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Panopto (par authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0b850-107">You can enable your users to automatically get signed-on to Panopto (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0b850-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="0b850-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0b850-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0b850-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b850-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0b850-110">Prerequisites</span></span>

<span data-ttu-id="0b850-111">Pour configurer l’intégration d’Azure AD à Panopto, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="0b850-111">To configure Azure AD integration with Panopto, you need the following items:</span></span>

- <span data-ttu-id="0b850-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b850-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0b850-113">Un abonnement Panopto pour lequel l’authentification unique est activée.</span><span class="sxs-lookup"><span data-stu-id="0b850-113">A Panopto single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0b850-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="0b850-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0b850-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="0b850-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0b850-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="0b850-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0b850-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0b850-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0b850-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="0b850-118">Scenario description</span></span>
<span data-ttu-id="0b850-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="0b850-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0b850-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="0b850-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0b850-121">Ajout de Panopto à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="0b850-121">Adding Panopto from the gallery</span></span>
2. <span data-ttu-id="0b850-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b850-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-panopto-from-the-gallery"></a><span data-ttu-id="0b850-123">Ajout de Panopto à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="0b850-123">Adding Panopto from the gallery</span></span>
<span data-ttu-id="0b850-124">Pour configurer l’intégration de Panopto à Azure AD, vous devez ajouter Panopto à votre liste d’applications SaaS gérées, à partir de la galerie.</span><span class="sxs-lookup"><span data-stu-id="0b850-124">To configure the integration of Panopto into Azure AD, you need to add Panopto from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0b850-125">**Pour ajouter Panopto à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0b850-125">**To add Panopto from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0b850-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0b850-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0b850-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="0b850-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0b850-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="0b850-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="0b850-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="0b850-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="0b850-133">Dans la zone de recherche, entrez **Panopto**.</span><span class="sxs-lookup"><span data-stu-id="0b850-133">In the search box, type **Panopto**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_search.png)

5. <span data-ttu-id="0b850-135">Dans le panneau des résultats, sélectionnez **Panopto**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="0b850-135">In the results panel, select **Panopto**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0b850-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b850-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="0b850-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Panopto avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="0b850-138">In this section, you configure and test Azure AD single sign-on with Panopto based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0b850-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Panopto équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0b850-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Panopto is to a user in Azure AD.</span></span> <span data-ttu-id="0b850-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Panopto associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="0b850-140">In other words, a link relationship between an Azure AD user and the related user in Panopto needs to be established.</span></span>

<span data-ttu-id="0b850-141">Dans Panopto, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="0b850-141">In Panopto, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0b850-142">Pour configurer et tester l’authentification unique Azure AD avec Panopto, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="0b850-142">To configure and test Azure AD single sign-on with Panopto, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0b850-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="0b850-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0b850-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0b850-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0b850-145">**[Création d’un utilisateur de test Panopto](#creating-a-panopto-test-user)** pour obtenir un équivalent de Britta Simon dans Panopto lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0b850-145">**[Creating a Panopto test user](#creating-a-panopto-test-user)** - to have a counterpart of Britta Simon in Panopto that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0b850-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0b850-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0b850-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="0b850-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0b850-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b850-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0b850-149">Dans cette section, vous activez l’authentification unique Azure AD dans le portail Azure et configurez l’authentification unique dans votre application Panopto.</span><span class="sxs-lookup"><span data-stu-id="0b850-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Panopto application.</span></span>

<span data-ttu-id="0b850-150">**Pour configurer l’authentification unique Azure AD avec Panopto, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0b850-150">**To configure Azure AD single sign-on with Panopto, perform the following steps:**</span></span>

1. <span data-ttu-id="0b850-151">Dans le portail Azure, sur la page d’intégration de l’application **Panopto**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="0b850-151">In the Azure portal, on the **Panopto** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="0b850-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="0b850-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_samlbase.png)

3. <span data-ttu-id="0b850-155">Dans la section **Domaine et URL Panopto**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="0b850-155">On the **Panopto Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_url.png)

    <span data-ttu-id="0b850-157">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<tenant-name>.panopto.com`</span><span class="sxs-lookup"><span data-stu-id="0b850-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.panopto.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0b850-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="0b850-158">This value is not real.</span></span> <span data-ttu-id="0b850-159">Mettez à jour cette valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="0b850-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="0b850-160">Contactez [l’équipe de support technique Panopto](mailto:support@panopto.com‎) pour obtenir cette valeur.</span><span class="sxs-lookup"><span data-stu-id="0b850-160">Contact [Panopto Client support team](mailto:support@panopto.com‎) to get this value.</span></span> 
 
4. <span data-ttu-id="0b850-161">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="0b850-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_certificate.png) 

5. <span data-ttu-id="0b850-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="0b850-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-panopto-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0b850-165">Dans la section **Configuration de Panopto**, cliquez sur **Configurer Panopto** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="0b850-165">On the **Panopto Configuration** section, click **Configure Panopto** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0b850-166">Copiez l’**ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="0b850-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_configure.png) 

7. <span data-ttu-id="0b850-168">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Panopto en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="0b850-168">In a different web browser window, log in to your Panopto company site as an administrator.</span></span>

8. <span data-ttu-id="0b850-169">Dans la barre d’outils située sur la gauche, cliquez sur **System (Système)**, puis sur **Identity Providers (Fournisseurs d’identité)**.</span><span class="sxs-lookup"><span data-stu-id="0b850-169">In the toolbar on the left, click **System**, and then click **Identity Providers**.</span></span>
   
   <span data-ttu-id="0b850-170">![Système](./media/active-directory-saas-panopto-tutorial/ic777670.png "système")</span><span class="sxs-lookup"><span data-stu-id="0b850-170">![System](./media/active-directory-saas-panopto-tutorial/ic777670.png "System")</span></span>
9. <span data-ttu-id="0b850-171">Cliquez sur **Add Provider**.</span><span class="sxs-lookup"><span data-stu-id="0b850-171">Click **Add Provider**.</span></span>
   
   <span data-ttu-id="0b850-172">![Fournisseurs d’identité](./media/active-directory-saas-panopto-tutorial/ic777671.png "fournisseurs d’identité")</span><span class="sxs-lookup"><span data-stu-id="0b850-172">![Identity Providers](./media/active-directory-saas-panopto-tutorial/ic777671.png "Identity Providers")</span></span>
   
10. <span data-ttu-id="0b850-173">Dans la section du fournisseur SAML, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0b850-173">In the SAML provider section, perform the following steps:</span></span>
   
    <span data-ttu-id="0b850-174">![Configuration SaaS](./media/active-directory-saas-panopto-tutorial/ic777672.png "configuration SaaS")</span><span class="sxs-lookup"><span data-stu-id="0b850-174">![SaaS configuration](./media/active-directory-saas-panopto-tutorial/ic777672.png "SaaS configuration")</span></span>
    
    <span data-ttu-id="0b850-175">a.</span><span class="sxs-lookup"><span data-stu-id="0b850-175">a.</span></span> <span data-ttu-id="0b850-176">Dans la liste **Provider Type (Type de fournisseur)**, sélectionnez **SAML20**.</span><span class="sxs-lookup"><span data-stu-id="0b850-176">From the **Provider Type** list, select **SAML20**.</span></span>    
    
    <span data-ttu-id="0b850-177">b.</span><span class="sxs-lookup"><span data-stu-id="0b850-177">b.</span></span> <span data-ttu-id="0b850-178">Dans la zone de texte **Instance Name** , attribuez un nom à votre instance.</span><span class="sxs-lookup"><span data-stu-id="0b850-178">In the **Instance Name** textbox, type a name for the instance.</span></span>

    <span data-ttu-id="0b850-179">c.</span><span class="sxs-lookup"><span data-stu-id="0b850-179">c.</span></span> <span data-ttu-id="0b850-180">Dans la zone de texte **Friendly Description** , entrez une description conviviale.</span><span class="sxs-lookup"><span data-stu-id="0b850-180">In the **Friendly Description** textbox, type a friendly description.</span></span>
    
    <span data-ttu-id="0b850-181">d.</span><span class="sxs-lookup"><span data-stu-id="0b850-181">d.</span></span> <span data-ttu-id="0b850-182">Dans la zone de texte **URL de la page de rebond**, collez la valeur de l’**URL du service d’authentification unique SAML** que vous avez copiée sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0b850-182">In **Bounce Page Url** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0b850-183">e.</span><span class="sxs-lookup"><span data-stu-id="0b850-183">e.</span></span> <span data-ttu-id="0b850-184">Dans la zone de texte **Émetteur**, collez la valeur de **ID d’entité SAML** que vous avez copiée depuis le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0b850-184">In the **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0b850-185">f.</span><span class="sxs-lookup"><span data-stu-id="0b850-185">f.</span></span> <span data-ttu-id="0b850-186">Ouvrez votre certificat codé en base 64, téléchargé à partir du portail Azure, copiez son contenu dans le Presse-papiers, puis collez-le dans la zone de texte **Clé publique**.</span><span class="sxs-lookup"><span data-stu-id="0b850-186">Open your base-64 encoded certificate, which you have downloaded from Azure portal, copy the content of it in to your clipboard, and then paste it to the **Public Key**  textbox.</span></span>

11. <span data-ttu-id="0b850-187">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="0b850-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="0b850-188">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="0b850-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0b850-189">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="0b850-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0b850-190">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0b850-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0b850-191">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b850-191">Creating an Azure AD test user</span></span>

<span data-ttu-id="0b850-192">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0b850-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="0b850-194">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0b850-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0b850-195">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0b850-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0b850-197">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="0b850-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0b850-199">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="0b850-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0b850-201">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0b850-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0b850-203">a.</span><span class="sxs-lookup"><span data-stu-id="0b850-203">a.</span></span> <span data-ttu-id="0b850-204">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0b850-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0b850-205">b.</span><span class="sxs-lookup"><span data-stu-id="0b850-205">b.</span></span> <span data-ttu-id="0b850-206">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0b850-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0b850-207">c.</span><span class="sxs-lookup"><span data-stu-id="0b850-207">c.</span></span> <span data-ttu-id="0b850-208">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="0b850-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0b850-209">d.</span><span class="sxs-lookup"><span data-stu-id="0b850-209">d.</span></span> <span data-ttu-id="0b850-210">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="0b850-210">Click **Create**.</span></span>
 
### <a name="creating-a-panopto-test-user"></a><span data-ttu-id="0b850-211">Création d’un utilisateur de test Panopto</span><span class="sxs-lookup"><span data-stu-id="0b850-211">Creating a Panopto test user</span></span>

<span data-ttu-id="0b850-212">Aucun élément d’action ne vous permet de configurer l’approvisionnement des utilisateurs dans Panopto.</span><span class="sxs-lookup"><span data-stu-id="0b850-212">There is no action item for you to configure user provisioning to Panopto.</span></span>  
<span data-ttu-id="0b850-213">Lorsqu’un utilisateur affecté tente de se connecter à Panopto à l’aide du panneau d’accès, Panopto vérifie si cet utilisateur existe.</span><span class="sxs-lookup"><span data-stu-id="0b850-213">When an assigned user tries to log in to Panopto using the access panel, Panopto checks whether the user exists.</span></span>  

<span data-ttu-id="0b850-214">Si aucun compte d’utilisateur n’est disponible, Panopto le crée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="0b850-214">If there is no user account available yet, it is automatically created by Panopto.</span></span>

>[!NOTE]
><span data-ttu-id="0b850-215">Vous pouvez utiliser n’importe quel outil ou API de création de compte d’utilisateur, fourni par Panopto, pour approvisionner des comptes utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="0b850-215">You can use any other Panopto user account creation tools or APIs provided by Panopto to provision Azure AD user accounts.</span></span>
>
>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0b850-216">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b850-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0b850-217">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Panopto.</span><span class="sxs-lookup"><span data-stu-id="0b850-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Panopto.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="0b850-219">**Pour affecter Britta Simon à Panopto, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0b850-219">**To assign Britta Simon to Panopto, perform the following steps:**</span></span>

1. <span data-ttu-id="0b850-220">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="0b850-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="0b850-222">Dans la liste des applications, sélectionnez **Panopto**.</span><span class="sxs-lookup"><span data-stu-id="0b850-222">In the applications list, select **Panopto**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_app.png) 

3. <span data-ttu-id="0b850-224">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="0b850-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="0b850-226">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="0b850-226">Click **Add** button.</span></span> <span data-ttu-id="0b850-227">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="0b850-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="0b850-229">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="0b850-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0b850-230">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="0b850-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0b850-231">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="0b850-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0b850-232">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="0b850-232">Testing single sign-on</span></span>

<span data-ttu-id="0b850-233">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="0b850-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0b850-234">Lorsque vous cliquez sur la vignette Panopto dans le panneau d’accès, vous accédez automatiquement à la page de connexion Panopto.</span><span class="sxs-lookup"><span data-stu-id="0b850-234">When you click the Panopto tile in the Access Panel, you should get automatically login page of Panopto application.</span></span>
<span data-ttu-id="0b850-235">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0b850-235">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0b850-236">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="0b850-236">Additional resources</span></span>

* [<span data-ttu-id="0b850-237">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0b850-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0b850-238">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="0b850-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_203.png

