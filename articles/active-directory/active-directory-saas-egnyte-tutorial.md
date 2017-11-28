---
title: "Didacticiel : Intégration d’Azure Active Directory avec Egnyte | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Egnyte."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8c2101d4-1779-4b36-8464-5c1ff780da18
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 62d01333b61e73c83588d2d1701c0c300df4ab1c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-egnyte"></a><span data-ttu-id="1ddd1-103">Didacticiel : Intégration d’Azure Active Directory à Egnyte</span><span class="sxs-lookup"><span data-stu-id="1ddd1-103">Tutorial: Azure Active Directory integration with Egnyte</span></span>

<span data-ttu-id="1ddd1-104">Dans ce didacticiel, vous allez apprendre à intégrer Egnyte à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1ddd1-104">In this tutorial, you learn how to integrate Egnyte with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1ddd1-105">L’intégration d’Egnyte dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="1ddd1-105">Integrating Egnyte with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1ddd1-106">Dans Azure AD, vous pouvez contrôler qui a accès à Egnyte.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-106">You can control in Azure AD who has access to Egnyte</span></span>
- <span data-ttu-id="1ddd1-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Egnyte (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-107">You can enable your users to automatically get signed-on to Egnyte (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1ddd1-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="1ddd1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1ddd1-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1ddd1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ddd1-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1ddd1-110">Prerequisites</span></span>

<span data-ttu-id="1ddd1-111">Pour configurer l’intégration d’Azure AD avec Egnyte, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1ddd1-111">To configure Azure AD integration with Egnyte, you need the following items:</span></span>

- <span data-ttu-id="1ddd1-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ddd1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1ddd1-113">Un abonnement Egnyte pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="1ddd1-113">An Egnyte single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1ddd1-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1ddd1-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1ddd1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1ddd1-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1ddd1-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1ddd1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1ddd1-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="1ddd1-118">Scenario description</span></span>
<span data-ttu-id="1ddd1-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1ddd1-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="1ddd1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1ddd1-121">Ajout d’Egnyte à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="1ddd1-121">Adding Egnyte from the gallery</span></span>
2. <span data-ttu-id="1ddd1-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ddd1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-egnyte-from-the-gallery"></a><span data-ttu-id="1ddd1-123">Ajout d’Egnyte à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="1ddd1-123">Adding Egnyte from the gallery</span></span>
<span data-ttu-id="1ddd1-124">Pour configurer l’intégration d’Egnyte avec Azure AD, vous devez ajouter Egnyte à votre liste d’applications SaaS gérées à partir de la galerie.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-124">To configure the integration of Egnyte into Azure AD, you need to add Egnyte from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1ddd1-125">**Pour ajouter Egnyte à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1ddd1-125">**To add Egnyte from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1ddd1-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1ddd1-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1ddd1-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="1ddd1-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="1ddd1-133">Dans la zone de recherche, entrez **Egnyte**.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-133">In the search box, type **Egnyte**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_search.png)

5. <span data-ttu-id="1ddd1-135">Dans le volet de résultats, sélectionnez **Egnyte**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-135">In the results panel, select **Egnyte**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1ddd1-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ddd1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1ddd1-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Egnyte, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="1ddd1-138">In this section, you configure and test Azure AD single sign-on with Egnyte based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1ddd1-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Egnyte correspondant dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Egnyte is to a user in Azure AD.</span></span> <span data-ttu-id="1ddd1-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Egnyte associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-140">In other words, a link relationship between an Azure AD user and the related user in Egnyte needs to be established.</span></span>

<span data-ttu-id="1ddd1-141">Dans Egnyte, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-141">In Egnyte, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1ddd1-142">Pour configurer et tester l’authentification unique Azure AD avec Egnyte, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="1ddd1-142">To configure and test Azure AD single sign-on with Egnyte, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1ddd1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1ddd1-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1ddd1-145">**[Création d’un utilisateur de test Egnyte](#creating-an-egnyte-test-user)** pour obtenir un équivalent de Britta Simon dans Egnyte lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-145">**[Creating an Egnyte test user](#creating-an-egnyte-test-user)** - to have a counterpart of Britta Simon in Egnyte that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1ddd1-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1ddd1-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1ddd1-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ddd1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1ddd1-149">Dans cette section, vous activez l’authentification unique Azure AD dans le portail Azure et configurez l’authentification unique dans votre application Egnyte.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Egnyte application.</span></span>

<span data-ttu-id="1ddd1-150">**Pour configurer l’authentification unique Azure AD avec Egnyte, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1ddd1-150">**To configure Azure AD single sign-on with Egnyte, perform the following steps:**</span></span>

1. <span data-ttu-id="1ddd1-151">Dans le portail Azure, sur la page d’intégration de l’application **Egnyte**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-151">In the Azure portal, on the **Egnyte** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="1ddd1-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_samlbase.png)

3. <span data-ttu-id="1ddd1-155">Dans la section **Domaine et URL Egnyte**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1ddd1-155">On the **Egnyte Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_url.png)

    <span data-ttu-id="1ddd1-157">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<companyname>.egnyte.com`</span><span class="sxs-lookup"><span data-stu-id="1ddd1-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.egnyte.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1ddd1-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-158">This value is not real.</span></span> <span data-ttu-id="1ddd1-159">Mettez à jour cette valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="1ddd1-160">Contactez [l’équipe de support technique Egnyte](https://www.egnyte.com/corp/contact_egnyte.html) pour obtenir cette valeur.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-160">Contact [Egnyte Client support team](https://www.egnyte.com/corp/contact_egnyte.html) to get this value.</span></span> 
 
4. <span data-ttu-id="1ddd1-161">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_certificate.png) 

5. <span data-ttu-id="1ddd1-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="1ddd1-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-egnyte-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1ddd1-165">Dans la section **Configuration d’Egnyte**, cliquez sur **Configurer Egnyte** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-165">On the **Egnyte Configuration** section, click **Configure Egnyte** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1ddd1-166">Copiez **l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_configure.png) 

7. <span data-ttu-id="1ddd1-168">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Egnyte en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-168">In a different web browser window, log in to your Egnyte company site as an administrator.</span></span>

8. <span data-ttu-id="1ddd1-169">Cliquez sur **Settings**.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-169">Click **Settings**.</span></span>
   
   <span data-ttu-id="1ddd1-170">![Paramètres](./media/active-directory-saas-egnyte-tutorial/ic787819.png "Paramètres")</span><span class="sxs-lookup"><span data-stu-id="1ddd1-170">![Settings](./media/active-directory-saas-egnyte-tutorial/ic787819.png "Settings")</span></span>

9. <span data-ttu-id="1ddd1-171">Dans le menu, cliquez sur **Settings**.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-171">In the menu, click **Settings**.</span></span>

   <span data-ttu-id="1ddd1-172">![Paramètres](./media/active-directory-saas-egnyte-tutorial/ic787820.png "Paramètres")</span><span class="sxs-lookup"><span data-stu-id="1ddd1-172">![Settings](./media/active-directory-saas-egnyte-tutorial/ic787820.png "Settings")</span></span>

10. <span data-ttu-id="1ddd1-173">Cliquez sur l’onglet **Configuration** puis sur **Security**.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-173">Click the **Configuration** tab, and then click **Security**.</span></span>

    <span data-ttu-id="1ddd1-174">![Sécurité](./media/active-directory-saas-egnyte-tutorial/ic787821.png "Sécurité")</span><span class="sxs-lookup"><span data-stu-id="1ddd1-174">![Security](./media/active-directory-saas-egnyte-tutorial/ic787821.png "Security")</span></span>

11. <span data-ttu-id="1ddd1-175">Dans la section **Single Sign-On Authentication** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1ddd1-175">In the **Single Sign-On Authentication** section, perform the following steps:</span></span>

    <span data-ttu-id="1ddd1-176">![Single Sign On Authentication](./media/active-directory-saas-egnyte-tutorial/ic787822.png "Single Sign On Authentication")</span><span class="sxs-lookup"><span data-stu-id="1ddd1-176">![Single Sign On Authentication](./media/active-directory-saas-egnyte-tutorial/ic787822.png "Single Sign On Authentication")</span></span>   
    
    <span data-ttu-id="1ddd1-177">a.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-177">a.</span></span> <span data-ttu-id="1ddd1-178">Pour **Single sign-on authentication**, sélectionnez **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-178">As **Single sign-on authentication**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="1ddd1-179">b.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-179">b.</span></span> <span data-ttu-id="1ddd1-180">Pour **Identity provider**, sélectionnez **AzureAD**.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-180">As **Identity provider**, select **AzureAD**.</span></span>
   
    <span data-ttu-id="1ddd1-181">c.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-181">c.</span></span> <span data-ttu-id="1ddd1-182">Collez **l’URL du service d’authentification unique SAML** copiée à partir du portail Azure dans la zone de texte **URL de connexion du fournisseur d’identité**.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-182">Paste **SAML Single Sign-On Service URL** copied from Azure portal into the **Identity provider login URL** textbox.</span></span>
   
    <span data-ttu-id="1ddd1-183">d.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-183">d.</span></span> <span data-ttu-id="1ddd1-184">Dans la zone de texte **ID d’entité du fournisseur d’identité**, collez l’**ID d’entité SAML** que vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-184">Paste **SAML Entity ID** which you have copied from Azure portal into the **Identity provider entity ID** textbox.</span></span>
      
    <span data-ttu-id="1ddd1-185">e.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-185">e.</span></span> <span data-ttu-id="1ddd1-186">Ouvrez dans le Bloc-notes votre certificat codé en base 64 téléchargé à partir du portail Azure, copiez son contenu dans le Presse-papiers, puis collez-le dans la zone de texte **Certificat de fournisseur d’identité**.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-186">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **Identity provider certificate** textbox.</span></span>
   
    <span data-ttu-id="1ddd1-187">f.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-187">f.</span></span> <span data-ttu-id="1ddd1-188">Pour **Default user mapping**, sélectionnez **Email address**.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-188">As **Default user mapping**, select **Email address**.</span></span>
   
    <span data-ttu-id="1ddd1-189">g.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-189">g.</span></span> <span data-ttu-id="1ddd1-190">Pour **Use domain-specific issuer value**, sélectionnez **disabled**.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-190">As **Use domain-specific issuer value**, select **disabled**.</span></span>
   
    <span data-ttu-id="1ddd1-191">h.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-191">h.</span></span> <span data-ttu-id="1ddd1-192">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-192">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="1ddd1-193">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1ddd1-194">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1ddd1-195">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1ddd1-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1ddd1-196">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ddd1-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="1ddd1-197">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="1ddd1-199">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1ddd1-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1ddd1-200">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1ddd1-202">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-202">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1ddd1-204">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-204">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1ddd1-206">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1ddd1-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1ddd1-208">a.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-208">a.</span></span> <span data-ttu-id="1ddd1-209">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1ddd1-210">b.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-210">b.</span></span> <span data-ttu-id="1ddd1-211">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1ddd1-212">c.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-212">c.</span></span> <span data-ttu-id="1ddd1-213">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1ddd1-214">d.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-214">d.</span></span> <span data-ttu-id="1ddd1-215">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-215">Click **Create**.</span></span>
 
### <a name="creating-an-egnyte-test-user"></a><span data-ttu-id="1ddd1-216">Création d’un utilisateur de test Egnyte</span><span class="sxs-lookup"><span data-stu-id="1ddd1-216">Creating an Egnyte test user</span></span>

<span data-ttu-id="1ddd1-217">Pour se connecter à Egnyte, les utilisateurs d’Azure AD doivent être approvisionnés dans Egnyte.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-217">To enable Azure AD users to log in to Egnyte, they must be provisioned into Egnyte.</span></span> <span data-ttu-id="1ddd1-218">Dans le cas de Egnyte, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-218">In the case of Egnyte, provisioning is a manual task.</span></span>

<span data-ttu-id="1ddd1-219">**Pour approvisionner un compte d’utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1ddd1-219">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="1ddd1-220">Connectez-vous à votre site d’entreprise **Egnyte** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-220">Log in to your **Egnyte** company site as administrator.</span></span>

2. <span data-ttu-id="1ddd1-221">Accédez à **Settings \> Users & Groups**.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-221">Go to **Settings \> Users & Groups**.</span></span>

3. <span data-ttu-id="1ddd1-222">Cliquez sur **Add New User**, puis sélectionnez le type d’utilisateur à ajouter.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-222">Click **Add New User**, and then select the type of user you want to add.</span></span>
   
   <span data-ttu-id="1ddd1-223">![Utilisateurs](./media/active-directory-saas-egnyte-tutorial/ic787824.png "Utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="1ddd1-223">![Users](./media/active-directory-saas-egnyte-tutorial/ic787824.png "Users")</span></span>

4. <span data-ttu-id="1ddd1-224">Dans la section **New Standard User** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1ddd1-224">In the **New Standard User** section, perform the following steps:</span></span>
   
   <span data-ttu-id="1ddd1-225">![New Standard User](./media/active-directory-saas-egnyte-tutorial/ic787825.png "New Standard User")</span><span class="sxs-lookup"><span data-stu-id="1ddd1-225">![New Standard User](./media/active-directory-saas-egnyte-tutorial/ic787825.png "New Standard User")</span></span>   

   <span data-ttu-id="1ddd1-226">a.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-226">a.</span></span> <span data-ttu-id="1ddd1-227">Tapez **l’adresse de messagerie**, le **nom d’utilisateur** et les autres informations d’un compte Azure Active Directory valide à approvisionner.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-227">Type the **Email**, **Username**, and other details of a valid Azure Active Directory account you want to provision.</span></span>
   
   <span data-ttu-id="1ddd1-228">b.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-228">b.</span></span> <span data-ttu-id="1ddd1-229">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-229">Click **Save**.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="1ddd1-230">Le titulaire du compte Azure Active Directory recevra une notification par courrier électronique.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-230">The Azure Active Directory account holder will receive a notification email.</span></span>
    >

>[!NOTE]
><span data-ttu-id="1ddd1-231">Vous pouvez utiliser n’importe quel autre outil ou API de création de compte d’utilisateur Egnyte fourni par ce site pour approvisionner des comptes d’utilisateurs AAD.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-231">You can use any other Egnyte user account creation tools or APIs provided by Egnyte to provision AAD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1ddd1-232">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ddd1-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1ddd1-233">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Egnyte.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Egnyte.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="1ddd1-235">**Pour affecter Britta Simon à Egnyte, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1ddd1-235">**To assign Britta Simon to Egnyte, perform the following steps:**</span></span>

1. <span data-ttu-id="1ddd1-236">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="1ddd1-238">Dans la liste des applications, sélectionnez **Egnyte**.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-238">In the applications list, select **Egnyte**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_app.png) 

3. <span data-ttu-id="1ddd1-240">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="1ddd1-242">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-242">Click **Add** button.</span></span> <span data-ttu-id="1ddd1-243">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="1ddd1-245">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1ddd1-246">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1ddd1-247">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1ddd1-248">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="1ddd1-248">Testing single sign-on</span></span>

<span data-ttu-id="1ddd1-249">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-249">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1ddd1-250">Si vous cliquez sur la vignette Egnyte dans le volet d’accès, vous devez vous connecter automatiquement à votre application Egnyte.</span><span class="sxs-lookup"><span data-stu-id="1ddd1-250">When you click the Egnyte tile in the Access Panel, you should get automatically signed-on to your Egnyte application.</span></span>
<span data-ttu-id="1ddd1-251">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1ddd1-251">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1ddd1-252">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="1ddd1-252">Additional resources</span></span>

* [<span data-ttu-id="1ddd1-253">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1ddd1-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1ddd1-254">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="1ddd1-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_203.png

