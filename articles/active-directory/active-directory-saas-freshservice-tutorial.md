---
title: "Didacticiel : intégration d’Azure Active Directory à Freshservice | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Freshservice."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3dd22b1f-445d-45c6-8eda-30207eb9a1a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: d32775fa91d3a49da1ef55e57d1d38990fa09346
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshservice"></a><span data-ttu-id="25c4b-103">Didacticiel : intégration d’Azure Active Directory à Freshservice</span><span class="sxs-lookup"><span data-stu-id="25c4b-103">Tutorial: Azure Active Directory integration with Freshservice</span></span>

<span data-ttu-id="25c4b-104">Dans ce didacticiel, vous allez apprendre à intégrer Freshservice à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="25c4b-104">In this tutorial, you learn how to integrate Freshservice with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="25c4b-105">L’intégration de Freshservice à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="25c4b-105">Integrating Freshservice with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="25c4b-106">Dans Azure AD, vous pouvez contrôler qui a accès à Freshservice.</span><span class="sxs-lookup"><span data-stu-id="25c4b-106">You can control in Azure AD who has access to Freshservice</span></span>
- <span data-ttu-id="25c4b-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Freshservice (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25c4b-107">You can enable your users to automatically get signed-on to Freshservice (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="25c4b-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="25c4b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="25c4b-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="25c4b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="25c4b-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="25c4b-110">Prerequisites</span></span>

<span data-ttu-id="25c4b-111">Pour configurer l’intégration d’Azure AD à Freshservice, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="25c4b-111">To configure Azure AD integration with Freshservice, you need the following items:</span></span>

- <span data-ttu-id="25c4b-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="25c4b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="25c4b-113">Un abonnement Freshservice pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="25c4b-113">A Freshservice single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="25c4b-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="25c4b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="25c4b-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="25c4b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="25c4b-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="25c4b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="25c4b-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="25c4b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="25c4b-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="25c4b-118">Scenario description</span></span>
<span data-ttu-id="25c4b-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="25c4b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="25c4b-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="25c4b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="25c4b-121">Ajout de Freshservice à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="25c4b-121">Adding Freshservice from the gallery</span></span>
2. <span data-ttu-id="25c4b-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="25c4b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshservice-from-the-gallery"></a><span data-ttu-id="25c4b-123">Ajout de Freshservice à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="25c4b-123">Adding Freshservice from the gallery</span></span>
<span data-ttu-id="25c4b-124">Pour configurer l’intégration de Freshservice à Azure AD, vous devez ajouter Freshservice disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="25c4b-124">To configure the integration of Freshservice into Azure AD, you need to add Freshservice from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="25c4b-125">**Pour ajouter Freshservice à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="25c4b-125">**To add Freshservice from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="25c4b-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="25c4b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="25c4b-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="25c4b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="25c4b-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="25c4b-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="25c4b-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="25c4b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="25c4b-133">Dans la zone de recherche, entrez **Freshservice**.</span><span class="sxs-lookup"><span data-stu-id="25c4b-133">In the search box, type **Freshservice**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_search.png)

5. <span data-ttu-id="25c4b-135">Dans le volet de résultats, sélectionnez **Freshservice**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="25c4b-135">In the results panel, select **Freshservice**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="25c4b-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="25c4b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="25c4b-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Freshservice, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="25c4b-138">In this section, you configure and test Azure AD single sign-on with Freshservice based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="25c4b-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Freshservice équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25c4b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Freshservice is to a user in Azure AD.</span></span> <span data-ttu-id="25c4b-140">En d’autres termes, une relation entre un utilisateur Azure AD et l’utilisateur Freshservice associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="25c4b-140">In other words, a link relationship between an Azure AD user and the related user in Freshservice needs to be established.</span></span>

<span data-ttu-id="25c4b-141">Dans Freshservice, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="25c4b-141">In Freshservice, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="25c4b-142">Pour configurer et tester l’authentification unique Azure AD avec Freshservice, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="25c4b-142">To configure and test Azure AD single sign-on with Freshservice, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="25c4b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="25c4b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="25c4b-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="25c4b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="25c4b-145">**[Création d’un utilisateur de test Freshservice](#creating-a-freshservice-test-user)** pour avoir un équivalent de Britta Simon dans Freshservice lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="25c4b-145">**[Creating a Freshservice test user](#creating-a-freshservice-test-user)** - to have a counterpart of Britta Simon in Freshservice that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="25c4b-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25c4b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="25c4b-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="25c4b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="25c4b-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="25c4b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="25c4b-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Freshservice.</span><span class="sxs-lookup"><span data-stu-id="25c4b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Freshservice application.</span></span>

<span data-ttu-id="25c4b-150">**Pour configurer l’authentification unique Azure AD avec Freshservice, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="25c4b-150">**To configure Azure AD single sign-on with Freshservice, perform the following steps:**</span></span>

1. <span data-ttu-id="25c4b-151">Dans le portail Azure, dans la page d’intégration de l’application **Freshservice**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="25c4b-151">In the Azure portal, on the **Freshservice** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="25c4b-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="25c4b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_samlbase.png)

3. <span data-ttu-id="25c4b-155">Dans la section **Domaine et URL Freshservice**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="25c4b-155">On the **Freshservice Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_url.png)

    <span data-ttu-id="25c4b-157">a.</span><span class="sxs-lookup"><span data-stu-id="25c4b-157">a.</span></span> <span data-ttu-id="25c4b-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<democompany>.freshservice.com`</span><span class="sxs-lookup"><span data-stu-id="25c4b-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<democompany>.freshservice.com`</span></span>

    <span data-ttu-id="25c4b-159">b.</span><span class="sxs-lookup"><span data-stu-id="25c4b-159">b.</span></span> <span data-ttu-id="25c4b-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<democompany>.freshservice.com`</span><span class="sxs-lookup"><span data-stu-id="25c4b-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<democompany>.freshservice.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="25c4b-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="25c4b-161">These values are not real.</span></span> <span data-ttu-id="25c4b-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="25c4b-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="25c4b-163">Pour obtenir ces valeurs, contactez [l’équipe du support client Freshservice](https://support.freshservice.com/).</span><span class="sxs-lookup"><span data-stu-id="25c4b-163">Contact [Freshservice Client support team](https://support.freshservice.com/) to get these values.</span></span> 
 
4. <span data-ttu-id="25c4b-164">Dans la section **Certificat de signature SAML**, copiez la valeur **THUMBPRINT** du certificat.</span><span class="sxs-lookup"><span data-stu-id="25c4b-164">On the **SAML Signing Certificate** section, copy **THUMBPRINT** value of certificate.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_certificate.png) 

5. <span data-ttu-id="25c4b-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="25c4b-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-freshservice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="25c4b-168">Dans la section **Configuration de Freshservice**, cliquez sur **Configurer Freshservice** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="25c4b-168">On the **Freshservice Configuration** section, click **Configure Freshservice** to open **Configure sign-on** window.</span></span> <span data-ttu-id="25c4b-169">Copiez **l’URL de déconnexion et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="25c4b-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_configure.png) 

7. <span data-ttu-id="25c4b-171">Dans une autre fenêtre de navigateur web, connectez-vous au site de votre entreprise Freshservice en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="25c4b-171">In a different web browser window, log in to your Freshservice company site as an administrator.</span></span>

8. <span data-ttu-id="25c4b-172">Dans le menu situé en haut, cliquez sur **Admin**.</span><span class="sxs-lookup"><span data-stu-id="25c4b-172">In the menu on the top, click **Admin**.</span></span>
   
    <span data-ttu-id="25c4b-173">![Administrateur](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Administrateur")</span><span class="sxs-lookup"><span data-stu-id="25c4b-173">![Admin](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span></span>

9. <span data-ttu-id="25c4b-174">Dans le **Customer Portal**, cliquez sur **Security**.</span><span class="sxs-lookup"><span data-stu-id="25c4b-174">In the **Customer Portal**, click **Security**.</span></span>
   
    <span data-ttu-id="25c4b-175">![Sécurité](./media/active-directory-saas-freshservice-tutorial/ic790815.png "Sécurité")</span><span class="sxs-lookup"><span data-stu-id="25c4b-175">![Security](./media/active-directory-saas-freshservice-tutorial/ic790815.png "Security")</span></span>

10. <span data-ttu-id="25c4b-176">Dans la section **Security** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="25c4b-176">In the **Security** section, perform the following steps:</span></span>
   
    <span data-ttu-id="25c4b-177">![Single Sign On](./media/active-directory-saas-freshservice-tutorial/ic790816.png "Single Sign On")</span><span class="sxs-lookup"><span data-stu-id="25c4b-177">![Single Sign On](./media/active-directory-saas-freshservice-tutorial/ic790816.png "Single Sign On")</span></span>
   
    <span data-ttu-id="25c4b-178">a.</span><span class="sxs-lookup"><span data-stu-id="25c4b-178">a.</span></span> <span data-ttu-id="25c4b-179">Activez **Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="25c4b-179">Switch **Single Sign On**.</span></span>

    <span data-ttu-id="25c4b-180">b.</span><span class="sxs-lookup"><span data-stu-id="25c4b-180">b.</span></span> <span data-ttu-id="25c4b-181">Sélectionnez **SAML SSO**.</span><span class="sxs-lookup"><span data-stu-id="25c4b-181">Select **SAML SSO**.</span></span>

    <span data-ttu-id="25c4b-182">c.</span><span class="sxs-lookup"><span data-stu-id="25c4b-182">c.</span></span> <span data-ttu-id="25c4b-183">Dans la zone de texte **URL de connexion SAML**, collez la valeur de **l’URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="25c4b-183">In the **SAML Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="25c4b-184">d.</span><span class="sxs-lookup"><span data-stu-id="25c4b-184">d.</span></span> <span data-ttu-id="25c4b-185">Dans la zone de texte **URL de déconnexion**, collez la valeur de **l’URL de déconnexion** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="25c4b-185">In the **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="25c4b-186">e.</span><span class="sxs-lookup"><span data-stu-id="25c4b-186">e.</span></span> <span data-ttu-id="25c4b-187">Dans la zone de texte **Security Certificate Fingerprint** (Empreinte du certificat de sécurité), collez la valeur **THUMBPRINT** du certificat que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="25c4b-187">In **Security Certificate Fingerprint** textbox, paste the **THUMBPRINT** value of certificate which you have copied from Azure portal.</span></span>

    <span data-ttu-id="25c4b-188">f.</span><span class="sxs-lookup"><span data-stu-id="25c4b-188">f.</span></span> <span data-ttu-id="25c4b-189">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="25c4b-189">Click **Save**</span></span>
   
> [!TIP]
> <span data-ttu-id="25c4b-190">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="25c4b-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="25c4b-191">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="25c4b-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="25c4b-192">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="25c4b-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="25c4b-193">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="25c4b-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="25c4b-194">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="25c4b-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="25c4b-196">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="25c4b-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="25c4b-197">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="25c4b-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="25c4b-199">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="25c4b-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="25c4b-201">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="25c4b-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="25c4b-203">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="25c4b-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="25c4b-205">a.</span><span class="sxs-lookup"><span data-stu-id="25c4b-205">a.</span></span> <span data-ttu-id="25c4b-206">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="25c4b-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="25c4b-207">b.</span><span class="sxs-lookup"><span data-stu-id="25c4b-207">b.</span></span> <span data-ttu-id="25c4b-208">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="25c4b-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="25c4b-209">c.</span><span class="sxs-lookup"><span data-stu-id="25c4b-209">c.</span></span> <span data-ttu-id="25c4b-210">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="25c4b-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="25c4b-211">d.</span><span class="sxs-lookup"><span data-stu-id="25c4b-211">d.</span></span> <span data-ttu-id="25c4b-212">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="25c4b-212">Click **Create**.</span></span>
 
### <a name="creating-a-freshservice-test-user"></a><span data-ttu-id="25c4b-213">Création d’un utilisateur de test Freshservice</span><span class="sxs-lookup"><span data-stu-id="25c4b-213">Creating a Freshservice test user</span></span>

<span data-ttu-id="25c4b-214">Pour permettre aux utilisateurs Azure AD de se connecter à Freshservice, vous devez les approvisionner dans Freshservice.</span><span class="sxs-lookup"><span data-stu-id="25c4b-214">To enable Azure AD users to log in to FreshService, they must be provisioned into FreshService.</span></span> <span data-ttu-id="25c4b-215">Dans le cas de FreshService, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="25c4b-215">In the case of FreshService, provisioning is a manual task.</span></span>

<span data-ttu-id="25c4b-216">**Pour approvisionner un compte d’utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="25c4b-216">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="25c4b-217">Connectez-vous au site d’entreprise **FreshService** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="25c4b-217">Log in to your **FreshService** company site as an administrator.</span></span>

2. <span data-ttu-id="25c4b-218">Dans le menu situé en haut, cliquez sur **Admin**.</span><span class="sxs-lookup"><span data-stu-id="25c4b-218">In the menu on the top, click **Admin**.</span></span>
   
    <span data-ttu-id="25c4b-219">![Administrateur](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Administrateur")</span><span class="sxs-lookup"><span data-stu-id="25c4b-219">![Admin](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span></span>

3. <span data-ttu-id="25c4b-220">Dans la section **User Management**, cliquez sur **Requesters**.</span><span class="sxs-lookup"><span data-stu-id="25c4b-220">In the **User Management** section, click **Requesters**.</span></span>
   
    <span data-ttu-id="25c4b-221">![Requesters](./media/active-directory-saas-freshservice-tutorial/ic790818.png "Requesters")</span><span class="sxs-lookup"><span data-stu-id="25c4b-221">![Requesters](./media/active-directory-saas-freshservice-tutorial/ic790818.png "Requesters")</span></span>

4. <span data-ttu-id="25c4b-222">Cliquez sur **New Requester**.</span><span class="sxs-lookup"><span data-stu-id="25c4b-222">Click **New Requester**.</span></span>
   
    <span data-ttu-id="25c4b-223">![New Requesters](./media/active-directory-saas-freshservice-tutorial/ic790819.png "New Requesters")</span><span class="sxs-lookup"><span data-stu-id="25c4b-223">![New Requesters](./media/active-directory-saas-freshservice-tutorial/ic790819.png "New Requesters")</span></span>

5. <span data-ttu-id="25c4b-224">Dans la section **New Requester** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="25c4b-224">In the **New Requester** section, perform the following steps:</span></span>
   
    <span data-ttu-id="25c4b-225">![New Requester](./media/active-directory-saas-freshservice-tutorial/ic790820.png "New Requester")</span><span class="sxs-lookup"><span data-stu-id="25c4b-225">![New Requester](./media/active-directory-saas-freshservice-tutorial/ic790820.png "New Requester")</span></span>   

    <span data-ttu-id="25c4b-226">a.</span><span class="sxs-lookup"><span data-stu-id="25c4b-226">a.</span></span> <span data-ttu-id="25c4b-227">Entrez le prénom et l’adresse de messagerie d’un compte Azure Active Directory valide que vous souhaitez approvisionner dans les zones de texte **Prénom** et **Email**.</span><span class="sxs-lookup"><span data-stu-id="25c4b-227">Enter the **First Name** and **Email** attributes of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>

    <span data-ttu-id="25c4b-228">b.</span><span class="sxs-lookup"><span data-stu-id="25c4b-228">b.</span></span> <span data-ttu-id="25c4b-229">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="25c4b-229">Click **Save**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="25c4b-230">Le titulaire du compte Azure Active Directory reçoit un e-mail contenant un lien pour confirmer le compte avant qu’il ne soit activé.</span><span class="sxs-lookup"><span data-stu-id="25c4b-230">The Azure Active Directory account holder gets an email including a link to confirm the account before it becomes active</span></span>
    >  

>[!NOTE]
><span data-ttu-id="25c4b-231">Vous pouvez utiliser n’importe quel outil ou API de création de compte utilisateur, fourni par FreshService, pour approvisionner des comptes utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="25c4b-231">You can use any other FreshService user account creation tools or APIs provided by FreshService to provision AAD user accounts.</span></span>
>  

![Affecter des utilisateurs][200] 

<span data-ttu-id="25c4b-233">**Pour affecter Britta Simon à Freshservice, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="25c4b-233">**To assign Britta Simon to Freshservice, perform the following steps:**</span></span>

1. <span data-ttu-id="25c4b-234">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="25c4b-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="25c4b-236">Dans la liste des applications, sélectionnez **Freshservice**.</span><span class="sxs-lookup"><span data-stu-id="25c4b-236">In the applications list, select **Freshservice**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_app.png) 

3. <span data-ttu-id="25c4b-238">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="25c4b-238">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="25c4b-240">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="25c4b-240">Click **Add** button.</span></span> <span data-ttu-id="25c4b-241">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="25c4b-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="25c4b-243">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="25c4b-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="25c4b-244">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="25c4b-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="25c4b-245">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="25c4b-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="25c4b-246">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="25c4b-246">Testing single sign-on</span></span>

<span data-ttu-id="25c4b-247">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="25c4b-247">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="25c4b-248">Lorsque vous cliquez sur la vignette Freshservice dans le volet d’accès, vous devez être connecté automatiquement à votre application Freshservice.</span><span class="sxs-lookup"><span data-stu-id="25c4b-248">When you click the Freshservice tile in the Access Panel, you should get automatically signed-on to your Freshservice application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="25c4b-249">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="25c4b-249">Additional resources</span></span>

* [<span data-ttu-id="25c4b-250">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="25c4b-250">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="25c4b-251">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="25c4b-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_203.png

