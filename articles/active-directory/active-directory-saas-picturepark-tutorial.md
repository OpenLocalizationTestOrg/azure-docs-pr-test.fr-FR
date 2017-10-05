---
title: "Didacticiel : Intégration d’Azure Active Directory avec Picturepark | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Picturepark."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 31c21cd4-9c00-4cad-9538-a13996dc872f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: jeedes
ms.openlocfilehash: 1c009aa1fdd3140a4466cf762b6c9687e74ce4c7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-picturepark"></a><span data-ttu-id="79053-103">Didacticiel : Intégration d’Azure Active Directory avec Picturepark</span><span class="sxs-lookup"><span data-stu-id="79053-103">Tutorial: Azure Active Directory integration with Picturepark</span></span>

<span data-ttu-id="79053-104">Ce didacticiel explique comment intégrer Picturepark avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="79053-104">In this tutorial, you learn how to integrate Picturepark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="79053-105">L’intégration de Picturepark avec Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="79053-105">Integrating Picturepark with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="79053-106">Dans Azure AD, vous pouvez contrôler qui a accès à Picturepark.</span><span class="sxs-lookup"><span data-stu-id="79053-106">You can control in Azure AD who has access to Picturepark</span></span>
- <span data-ttu-id="79053-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Picturepark (authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="79053-107">You can enable your users to automatically get signed-on to Picturepark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="79053-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="79053-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="79053-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="79053-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79053-110">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="79053-110">Prerequisites</span></span>

<span data-ttu-id="79053-111">Pour configurer l’intégration d’Azure AD avec Picturepark, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="79053-111">To configure Azure AD integration with Picturepark, you need the following items:</span></span>

- <span data-ttu-id="79053-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="79053-112">An Azure AD subscription</span></span>
- <span data-ttu-id="79053-113">Un abonnement Picturepark pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="79053-113">A Picturepark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="79053-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="79053-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="79053-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="79053-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="79053-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="79053-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="79053-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="79053-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="79053-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="79053-118">Scenario description</span></span>
<span data-ttu-id="79053-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="79053-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="79053-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="79053-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="79053-121">Ajout de Picturepark à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="79053-121">Adding Picturepark from the gallery</span></span>
2. <span data-ttu-id="79053-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="79053-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-picturepark-from-the-gallery"></a><span data-ttu-id="79053-123">Ajout de Picturepark à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="79053-123">Adding Picturepark from the gallery</span></span>
<span data-ttu-id="79053-124">Pour configurer l’intégration de Picturepark à Azure AD, vous devez ajouter Picturepark à partir de la galerie à votre liste d’applications SaaS managées.</span><span class="sxs-lookup"><span data-stu-id="79053-124">To configure the integration of Picturepark into Azure AD, you need to add Picturepark from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="79053-125">**Pour ajouter Picturepark à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="79053-125">**To add Picturepark from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="79053-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="79053-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="79053-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="79053-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="79053-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="79053-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="79053-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="79053-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="79053-133">Dans la zone de recherche, tapez **Picturepark**.</span><span class="sxs-lookup"><span data-stu-id="79053-133">In the search box, type **Picturepark**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_search.png)

5. <span data-ttu-id="79053-135">Dans le volet de résultats, sélectionnez **Picturepark**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="79053-135">In the results panel, select **Picturepark**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="79053-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="79053-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="79053-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Picturepark sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="79053-138">In this section, you configure and test Azure AD single sign-on with Picturepark based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="79053-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Picturepark équivalent à l’utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="79053-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Picturepark is to a user in Azure AD.</span></span> <span data-ttu-id="79053-140">En d’autres termes, une relation doit être établie entre un utilisateur Azure AD et l’utilisateur associé dans Picturepark.</span><span class="sxs-lookup"><span data-stu-id="79053-140">In other words, a link relationship between an Azure AD user and the related user in Picturepark needs to be established.</span></span>

<span data-ttu-id="79053-141">Dans Picturepark, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **Username** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="79053-141">In Picturepark, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="79053-142">Pour configurer et tester l’authentification unique Azure AD avec Picturepark, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="79053-142">To configure and test Azure AD single sign-on with Picturepark, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="79053-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="79053-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="79053-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="79053-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="79053-145">**[Création d’un utilisateur de test Picturepark](#creating-a-picturepark-test-user)** pour avoir un équivalent de Britta Simon dans Picturepark, lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="79053-145">**[Creating a Picturepark test user](#creating-a-picturepark-test-user)** - to have a counterpart of Britta Simon in Picturepark that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="79053-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="79053-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="79053-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="79053-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="79053-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="79053-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="79053-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Picturepark.</span><span class="sxs-lookup"><span data-stu-id="79053-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Picturepark application.</span></span>

<span data-ttu-id="79053-150">**Pour configurer l’authentification unique Azure AD avec Picturepark, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="79053-150">**To configure Azure AD single sign-on with Picturepark, perform the following steps:**</span></span>

1. <span data-ttu-id="79053-151">Dans le portail Azure, sur la page d’intégration de l’application **Picturepark**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="79053-151">In the Azure portal, on the **Picturepark** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="79053-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="79053-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_samlbase.png)

3. <span data-ttu-id="79053-155">Dans la section **Domaine et URL Picturepark**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="79053-155">On the **Picturepark Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_url.png)

    <span data-ttu-id="79053-157">a.</span><span class="sxs-lookup"><span data-stu-id="79053-157">a.</span></span> <span data-ttu-id="79053-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<companyname>.picturepark.com`</span><span class="sxs-lookup"><span data-stu-id="79053-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.picturepark.com`</span></span>

    <span data-ttu-id="79053-159">b.</span><span class="sxs-lookup"><span data-stu-id="79053-159">b.</span></span> <span data-ttu-id="79053-160">Dans la zone de texte **Identificateur**, entrez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="79053-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span> 
    
    |  |
    |--|
    | `https://<companyname>.current-picturepark.com`|
    | `https://<companyname>.picturepark.com`|
    | `https://<companyname>.next-picturepark.com`|
    | |

    > [!NOTE] 
    > <span data-ttu-id="79053-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="79053-161">These values are not real.</span></span> <span data-ttu-id="79053-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="79053-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="79053-163">Pour obtenir ces valeurs, contactez l’[équipe de support technique Picturepark](https://picturepark.com/about/contact/).</span><span class="sxs-lookup"><span data-stu-id="79053-163">Contact [Picturepark Client support team](https://picturepark.com/about/contact/) to get these values.</span></span> 
 
4. <span data-ttu-id="79053-164">Dans la section **Certificat de signature SAML**, copiez la valeur **THUMBPRINT** du certificat.</span><span class="sxs-lookup"><span data-stu-id="79053-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_certificate.png) 

5. <span data-ttu-id="79053-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="79053-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-picturepark-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="79053-168">Dans la section **Configuration de Picturepark**, cliquez sur **Configurer Picturepark** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="79053-168">On the **Picturepark Configuration** section, click **Configure Picturepark** to open **Configure sign-on** window.</span></span> <span data-ttu-id="79053-169">Copiez l**’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="79053-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_configure.png) 

7. <span data-ttu-id="79053-171">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Picturepark en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="79053-171">In a different web browser window, log into your Picturepark company site as an administrator.</span></span>

8. <span data-ttu-id="79053-172">Dans la barre d’outils située en haut, cliquez sur **Administrative tools**, puis sur **Management Console**.</span><span class="sxs-lookup"><span data-stu-id="79053-172">In the toolbar on the top, click **Administrative tools**, and then click **Management Console**.</span></span>
   
    <span data-ttu-id="79053-173">![Console de gestion](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Console de gestion")</span><span class="sxs-lookup"><span data-stu-id="79053-173">![Management Console](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Management Console")</span></span>

9. <span data-ttu-id="79053-174">Cliquez sur **Authentication**, puis sur **Identity providers**.</span><span class="sxs-lookup"><span data-stu-id="79053-174">Click **Authentication**, and then click **Identity providers**.</span></span>
   
    <span data-ttu-id="79053-175">![Authentication](./media/active-directory-saas-picturepark-tutorial/ic795063.png "Authentication")</span><span class="sxs-lookup"><span data-stu-id="79053-175">![Authentication](./media/active-directory-saas-picturepark-tutorial/ic795063.png "Authentication")</span></span>

10. <span data-ttu-id="79053-176">Dans la section **Identity provider configuration** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="79053-176">In the **Identity provider configuration** section, perform the following steps:</span></span>
   
    <span data-ttu-id="79053-177">![Configuration du fournisseur d’identité](./media/active-directory-saas-picturepark-tutorial/ic795064.png "Configuration du fournisseur d’identité")</span><span class="sxs-lookup"><span data-stu-id="79053-177">![Identity provider configuration](./media/active-directory-saas-picturepark-tutorial/ic795064.png "Identity provider configuration")</span></span>
   
    <span data-ttu-id="79053-178">a.</span><span class="sxs-lookup"><span data-stu-id="79053-178">a.</span></span> <span data-ttu-id="79053-179">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="79053-179">Click **Add**.</span></span>
  
    <span data-ttu-id="79053-180">b.</span><span class="sxs-lookup"><span data-stu-id="79053-180">b.</span></span> <span data-ttu-id="79053-181">Entrez un nom pour votre configuration.</span><span class="sxs-lookup"><span data-stu-id="79053-181">Type a name for your configuration.</span></span>
   
    <span data-ttu-id="79053-182">c.</span><span class="sxs-lookup"><span data-stu-id="79053-182">c.</span></span> <span data-ttu-id="79053-183">Sélectionnez **Set as default**.</span><span class="sxs-lookup"><span data-stu-id="79053-183">Select **Set as default**.</span></span>
   
    <span data-ttu-id="79053-184">d.</span><span class="sxs-lookup"><span data-stu-id="79053-184">d.</span></span> <span data-ttu-id="79053-185">Dans la zone de texte **Issuer URI (URI de l’émetteur)**, collez la valeur **URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="79053-185">In **Issuer URI** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="79053-186">e.</span><span class="sxs-lookup"><span data-stu-id="79053-186">e.</span></span> <span data-ttu-id="79053-187">Dans la zone de texte **Trusted Issuer Thumb Print** (Empreinte numérique de l’émetteur approuvé), collez la valeur de l’**empreinte** que vous avez copiée à partir de la section **Certificat de signature SAML**.</span><span class="sxs-lookup"><span data-stu-id="79053-187">In **Trusted Issuer Thumb Print** textbox, paste the value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span></span> 

11. <span data-ttu-id="79053-188">Cliquez sur **JoinDefaultUsersGroup**.</span><span class="sxs-lookup"><span data-stu-id="79053-188">Click **JoinDefaultUsersGroup**.</span></span>

12. <span data-ttu-id="79053-189">Pour définir l’attribut **Emailaddress** dans la zone de texte **Revendication**, tapez `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="79053-189">To set the **Emailaddress** attribute in the **Claim** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` and click **Save**.</span></span>

      <span data-ttu-id="79053-190">![Configuration](./media/active-directory-saas-picturepark-tutorial/ic795065.png "Configuration")</span><span class="sxs-lookup"><span data-stu-id="79053-190">![Configuration](./media/active-directory-saas-picturepark-tutorial/ic795065.png "Configuration")</span></span>

> [!TIP]
> <span data-ttu-id="79053-191">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="79053-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="79053-192">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="79053-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="79053-193">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="79053-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="79053-194">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="79053-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="79053-195">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="79053-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="79053-197">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="79053-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="79053-198">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="79053-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="79053-200">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="79053-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="79053-202">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="79053-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="79053-204">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="79053-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="79053-206">a.</span><span class="sxs-lookup"><span data-stu-id="79053-206">a.</span></span> <span data-ttu-id="79053-207">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="79053-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="79053-208">b.</span><span class="sxs-lookup"><span data-stu-id="79053-208">b.</span></span> <span data-ttu-id="79053-209">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="79053-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="79053-210">c.</span><span class="sxs-lookup"><span data-stu-id="79053-210">c.</span></span> <span data-ttu-id="79053-211">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="79053-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="79053-212">d.</span><span class="sxs-lookup"><span data-stu-id="79053-212">d.</span></span> <span data-ttu-id="79053-213">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="79053-213">Click **Create**.</span></span>
 
### <a name="creating-a-picturepark-test-user"></a><span data-ttu-id="79053-214">Création d’un utilisateur de test Picturepark</span><span class="sxs-lookup"><span data-stu-id="79053-214">Creating a Picturepark test user</span></span>

<span data-ttu-id="79053-215">Pour permettre aux utilisateurs Azure AD de se connecter à Picturepark, vous devez les approvisionner dans Picturepark.</span><span class="sxs-lookup"><span data-stu-id="79053-215">In order to enable Azure AD users to log into Picturepark, they must be provisioned into Picturepark.</span></span> <span data-ttu-id="79053-216">Dans le cas de Picturepark, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="79053-216">In the case of Picturepark, provisioning is a manual task.</span></span>

<span data-ttu-id="79053-217">**Pour approvisionner un compte d’utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="79053-217">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="79053-218">Connectez-vous à votre locataire **Picturepark** .</span><span class="sxs-lookup"><span data-stu-id="79053-218">Log in to your **Picturepark** tenant.</span></span>

2. <span data-ttu-id="79053-219">Dans la barre d’outils située en haut, cliquez sur **Administrative tools**, puis sur **Users**.</span><span class="sxs-lookup"><span data-stu-id="79053-219">In the toolbar on the top, click **Administrative tools**, and then click **Users**.</span></span>
   
    <span data-ttu-id="79053-220">![Utilisateurs](./media/active-directory-saas-picturepark-tutorial/ic795067.png "Utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="79053-220">![Users](./media/active-directory-saas-picturepark-tutorial/ic795067.png "Users")</span></span>

3. <span data-ttu-id="79053-221">Dans l’onglet **Users overview**, cliquez sur **New**.</span><span class="sxs-lookup"><span data-stu-id="79053-221">In the **Users overview** tab, click **New**.</span></span>
   
    <span data-ttu-id="79053-222">![Gestion des utilisateurs](./media/active-directory-saas-picturepark-tutorial/ic795068.png "gestion des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="79053-222">![User management](./media/active-directory-saas-picturepark-tutorial/ic795068.png "User management")</span></span>

4. <span data-ttu-id="79053-223">Dans la boîte de dialogue **Créer un utilisateur**, procédez comme suit pour un utilisateur Azure Active Directory valide que vous souhaitez approvisionner :</span><span class="sxs-lookup"><span data-stu-id="79053-223">On the **Create User** dialog, perform the following steps of a valid Azure Active Directory User you want to provision:</span></span>
   
    <span data-ttu-id="79053-224">![Create User](./media/active-directory-saas-picturepark-tutorial/ic795069.png "Create User")</span><span class="sxs-lookup"><span data-stu-id="79053-224">![Create User](./media/active-directory-saas-picturepark-tutorial/ic795069.png "Create User")</span></span>
   
    <span data-ttu-id="79053-225">a.</span><span class="sxs-lookup"><span data-stu-id="79053-225">a.</span></span> <span data-ttu-id="79053-226">Dans la zone de texte **Email Address** (Adresse e-mail), entrez l’**adresse e-mail** de l’utilisateur **BrittaSimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="79053-226">In the **Email Address** textbox, type the **email address** of the user **BrittaSimon@contoso.com**.</span></span>  
   
    <span data-ttu-id="79053-227">b.</span><span class="sxs-lookup"><span data-stu-id="79053-227">b.</span></span> <span data-ttu-id="79053-228">Dans les zones de texte **Password** (Mot de passe) et **Confirm Password** (Confirmer le mot de passe), entrez le **mot de passe** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="79053-228">In the **Password** and **Confirm Password** textboxes, type the **password** of BrittaSimon.</span></span> 
   
    <span data-ttu-id="79053-229">c.</span><span class="sxs-lookup"><span data-stu-id="79053-229">c.</span></span> <span data-ttu-id="79053-230">Dans la zone de texte **First Name** (Prénom), entrez le **prénom** de l’utilisateur **Britta**.</span><span class="sxs-lookup"><span data-stu-id="79053-230">In the **First Name** textbox, type the **First Name** of the user **Britta**.</span></span> 
   
    <span data-ttu-id="79053-231">d.</span><span class="sxs-lookup"><span data-stu-id="79053-231">d.</span></span> <span data-ttu-id="79053-232">Dans la zone de texte **Last Name** (Nom), entrez le **nom** de l’utilisateur **Simon**.</span><span class="sxs-lookup"><span data-stu-id="79053-232">In the **Last Name** textbox, type the **Last Name** of the user **Simon**.</span></span>
   
    <span data-ttu-id="79053-233">e.</span><span class="sxs-lookup"><span data-stu-id="79053-233">e.</span></span> <span data-ttu-id="79053-234">Dans la zone de texte **Company** (Société), entrez le **nom de la société** de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="79053-234">In the **Company** textbox, type the **Company name** of the user.</span></span> 
   
    <span data-ttu-id="79053-235">f.</span><span class="sxs-lookup"><span data-stu-id="79053-235">f.</span></span> <span data-ttu-id="79053-236">Dans la zone de texte **Country** (Pays), sélectionnez le **pays** de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="79053-236">In the **Country** textbox, select the **Country** of the user.</span></span>
  
    <span data-ttu-id="79053-237">g.</span><span class="sxs-lookup"><span data-stu-id="79053-237">g.</span></span> <span data-ttu-id="79053-238">Dans la zone de texte **ZIP** (Code postal), entrez le **code postal** de la ville.</span><span class="sxs-lookup"><span data-stu-id="79053-238">In the **ZIP** textbox, type the **ZIP code** of the city.</span></span>
   
    <span data-ttu-id="79053-239">h.</span><span class="sxs-lookup"><span data-stu-id="79053-239">h.</span></span> <span data-ttu-id="79053-240">Dans la zone de texte **City** (Ville), entrez le **nom de la ville** de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="79053-240">In the **City** textbox, type the **City name** of the user.</span></span>

    <span data-ttu-id="79053-241">i.</span><span class="sxs-lookup"><span data-stu-id="79053-241">i.</span></span> <span data-ttu-id="79053-242">Sélectionnez une langue dans **Language**.</span><span class="sxs-lookup"><span data-stu-id="79053-242">Select a **Language**.</span></span>
   
    <span data-ttu-id="79053-243">j.</span><span class="sxs-lookup"><span data-stu-id="79053-243">j.</span></span> <span data-ttu-id="79053-244">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="79053-244">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="79053-245">Vous pouvez utiliser n’importe quel outil ou API de création de compte utilisateur fournis par Picturepark pour approvisionner des comptes utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="79053-245">You can use any other Picturepark user account creation tools or APIs provided by Picturepark to provision Azure AD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="79053-246">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="79053-246">Assigning the Azure AD test user</span></span>

<span data-ttu-id="79053-247">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Picturepark.</span><span class="sxs-lookup"><span data-stu-id="79053-247">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Picturepark.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="79053-249">**Pour affecter Britta Simon à Picturepark, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="79053-249">**To assign Britta Simon to Picturepark, perform the following steps:**</span></span>

1. <span data-ttu-id="79053-250">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="79053-250">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="79053-252">Dans la liste des applications, sélectionnez **Picturepark**.</span><span class="sxs-lookup"><span data-stu-id="79053-252">In the applications list, select **Picturepark**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_app.png) 

3. <span data-ttu-id="79053-254">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="79053-254">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="79053-256">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="79053-256">Click **Add** button.</span></span> <span data-ttu-id="79053-257">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="79053-257">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="79053-259">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="79053-259">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="79053-260">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="79053-260">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="79053-261">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="79053-261">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="79053-262">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="79053-262">Testing single sign-on</span></span>

<span data-ttu-id="79053-263">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="79053-263">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="79053-264">Lorsque vous cliquez sur la vignette Picturepark dans le volet d’accès, vous devez être connecté automatiquement à votre application Picturepark.</span><span class="sxs-lookup"><span data-stu-id="79053-264">When you click the Picturepark tile in the Access Panel, you should get automatically signed-on to your Picturepark application.</span></span> <span data-ttu-id="79053-265">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="79053-265">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="79053-266">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="79053-266">Additional resources</span></span>

* [<span data-ttu-id="79053-267">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="79053-267">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="79053-268">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="79053-268">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_203.png

