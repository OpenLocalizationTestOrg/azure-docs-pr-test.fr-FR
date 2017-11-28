---
title: "Didacticiel : intégration d’Azure Active Directory à Projectplace | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Projectplace."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 298059ca-b652-4577-916a-c31393d53d7a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: bb9dd10c887cb0e42e544066d9b0dcfa554e10ce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-projectplace"></a><span data-ttu-id="ccf3c-103">Didacticiel : Intégration d’Azure Active Directory à Projectplace</span><span class="sxs-lookup"><span data-stu-id="ccf3c-103">Tutorial: Azure Active Directory integration with Projectplace</span></span>

<span data-ttu-id="ccf3c-104">Dans ce didacticiel, vous allez apprendre à intégrer Projectplace à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ccf3c-104">In this tutorial, you learn how to integrate Projectplace with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ccf3c-105">L’intégration de Projectplace dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="ccf3c-105">Integrating Projectplace with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ccf3c-106">Dans Azure AD, vous pouvez contrôler qui a accès à Projectplace.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-106">You can control in Azure AD who has access to Projectplace</span></span>
- <span data-ttu-id="ccf3c-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Projectplace (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-107">You can enable your users to automatically get signed-on to Projectplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ccf3c-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="ccf3c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ccf3c-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ccf3c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ccf3c-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ccf3c-110">Prerequisites</span></span>

<span data-ttu-id="ccf3c-111">Pour configurer l’intégration d’Azure AD à Projectplace, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ccf3c-111">To configure Azure AD integration with Projectplace, you need the following items:</span></span>

- <span data-ttu-id="ccf3c-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="ccf3c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ccf3c-113">Un abonnement Projectplace pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="ccf3c-113">A Projectplace single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ccf3c-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ccf3c-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ccf3c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ccf3c-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ccf3c-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ccf3c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ccf3c-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="ccf3c-118">Scenario description</span></span>
<span data-ttu-id="ccf3c-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ccf3c-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="ccf3c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ccf3c-121">Ajout de Projectplace à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="ccf3c-121">Adding Projectplace from the gallery</span></span>
2. <span data-ttu-id="ccf3c-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ccf3c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-projectplace-from-the-gallery"></a><span data-ttu-id="ccf3c-123">Ajout de Projectplace à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="ccf3c-123">Adding Projectplace from the gallery</span></span>
<span data-ttu-id="ccf3c-124">Pour configurer l’intégration de Projectplace avec Azure AD, vous devez ajouter Projectplace à votre liste d’applications SaaS gérées, à partir de la galerie.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-124">To configure the integration of Projectplace into Azure AD, you need to add Projectplace from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ccf3c-125">**Pour ajouter Projectplace à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ccf3c-125">**To add Projectplace from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ccf3c-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ccf3c-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ccf3c-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="ccf3c-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="ccf3c-133">Dans la zone de recherche, saisissez **Projectplace**.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-133">In the search box, type **Projectplace**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_search.png)

5. <span data-ttu-id="ccf3c-135">Dans le panneau des résultats, sélectionnez **Projectplace**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-135">In the results panel, select **Projectplace**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ccf3c-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ccf3c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ccf3c-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Projectplace, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="ccf3c-138">In this section, you configure and test Azure AD single sign-on with Projectplace based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ccf3c-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Projectplace correspondant dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Projectplace is to a user in Azure AD.</span></span> <span data-ttu-id="ccf3c-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Projectplace associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-140">In other words, a link relationship between an Azure AD user and the related user in Projectplace needs to be established.</span></span>

<span data-ttu-id="ccf3c-141">Dans Projectplace, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-141">In Projectplace, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ccf3c-142">Pour configurer et tester l’authentification unique Azure AD avec Projectplace, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="ccf3c-142">To configure and test Azure AD single sign-on with Projectplace, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ccf3c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ccf3c-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ccf3c-145">**[Création d’un utilisateur de test Projectplace](#creating-a-projectplace-test-user)** pour obtenir un équivalent de Britta Simon dans Projectplace lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-145">**[Creating a Projectplace test user](#creating-a-projectplace-test-user)** - to have a counterpart of Britta Simon in Projectplace that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ccf3c-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ccf3c-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ccf3c-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ccf3c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ccf3c-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Projectplace.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Projectplace application.</span></span>

<span data-ttu-id="ccf3c-150">**Pour configurer l’authentification unique Azure AD avec Projectplace, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ccf3c-150">**To configure Azure AD single sign-on with Projectplace, perform the following steps:**</span></span>

1. <span data-ttu-id="ccf3c-151">Dans le portail Azure, sur la page d’intégration de l’application **Projectplace**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-151">In the Azure portal, on the **Projectplace** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="ccf3c-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_samlbase.png)

3. <span data-ttu-id="ccf3c-155">Dans la section **Domaine et URL Projectplace**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ccf3c-155">On the **Projectplace Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_url.png)

    <span data-ttu-id="ccf3c-157">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<company>.projectplace.com`</span><span class="sxs-lookup"><span data-stu-id="ccf3c-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.projectplace.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ccf3c-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-158">This value is not real.</span></span> <span data-ttu-id="ccf3c-159">Mettez à jour cette valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="ccf3c-160">Contactez [l’équipe de support technique Projectplace](https://success.planview.com/Projectplace/Support) pour obtenir cette valeur.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-160">Contact [Projectplace Client support team](https://success.planview.com/Projectplace/Support) to get this value.</span></span> 
 
4. <span data-ttu-id="ccf3c-161">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_certificate.png) 

5. <span data-ttu-id="ccf3c-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="ccf3c-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-projectplace-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="ccf3c-165">Pour configurer l’authentification unique côté **Projectplace**, vous devez envoyer le fichier **XML de métadonnées** téléchargé à l’[équipe de support technique Projectplace](https://success.planview.com/Projectplace/Support).</span><span class="sxs-lookup"><span data-stu-id="ccf3c-165">To configure single sign-on on **Projectplace** side, you need to send the downloaded **Metadata XML** to [Projectplace support team](https://success.planview.com/Projectplace/Support).</span></span> <span data-ttu-id="ccf3c-166">Celle-ci configure ensuite ce paramètre pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

>[!NOTE]
><span data-ttu-id="ccf3c-167">La configuration de l’authentification unique doit être effectuée par [l’équipe du support technique Projectplace](https://success.planview.com/Projectplace/Support).</span><span class="sxs-lookup"><span data-stu-id="ccf3c-167">The single sign-on configuration has to be performed by the [Projectplace support team](https://success.planview.com/Projectplace/Support).</span></span> <span data-ttu-id="ccf3c-168">Vous recevez une notification dès qu’elle est terminée.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-168">You will get a notification as soon as the configuration has been completed.</span></span>

> [!TIP]
> <span data-ttu-id="ccf3c-169">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ccf3c-170">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ccf3c-171">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ccf3c-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ccf3c-172">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="ccf3c-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="ccf3c-173">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="ccf3c-175">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ccf3c-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ccf3c-176">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-projectplace-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ccf3c-178">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-projectplace-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ccf3c-180">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-projectplace-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ccf3c-182">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ccf3c-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-projectplace-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ccf3c-184">a.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-184">a.</span></span> <span data-ttu-id="ccf3c-185">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ccf3c-186">b.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-186">b.</span></span> <span data-ttu-id="ccf3c-187">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ccf3c-188">c.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-188">c.</span></span> <span data-ttu-id="ccf3c-189">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ccf3c-190">d.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-190">d.</span></span> <span data-ttu-id="ccf3c-191">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-191">Click **Create**.</span></span>
 
### <a name="creating-a-projectplace-test-user"></a><span data-ttu-id="ccf3c-192">Création d’un utilisateur de test Projectplace</span><span class="sxs-lookup"><span data-stu-id="ccf3c-192">Creating a Projectplace test user</span></span>

<span data-ttu-id="ccf3c-193">Pour permettre aux utilisateurs Azure AD de se connecter à Projectplace, vous devez les approvisionner dans Projectplace.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-193">In order to enable Azure AD users to log into Projectplace, they must be provisioned into Projectplace.</span></span> <span data-ttu-id="ccf3c-194">Dans le cas de Projectplace, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-194">In the case of Projectplace, provisioning is a manual task.</span></span>

<span data-ttu-id="ccf3c-195">**Pour approvisionner un compte d’utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ccf3c-195">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="ccf3c-196">Connectez-vous au site d’entreprise **Projectplace** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-196">Log in to your **Projectplace** company site as an administrator.</span></span>

2. <span data-ttu-id="ccf3c-197">Accédez à **People**, puis cliquez sur **Members**.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-197">Go to **People**, and then click **Members**.</span></span>
   
    <span data-ttu-id="ccf3c-198">![Personnes](./media/active-directory-saas-projectplace-tutorial/ic790228.png "Personnes")</span><span class="sxs-lookup"><span data-stu-id="ccf3c-198">![People](./media/active-directory-saas-projectplace-tutorial/ic790228.png "People")</span></span>

3. <span data-ttu-id="ccf3c-199">Cliquez sur **Add Member**.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-199">Click **Add Member**.</span></span>
   
    <span data-ttu-id="ccf3c-200">![Ajouter des membres](./media/active-directory-saas-projectplace-tutorial/ic790232.png "ajouter des membres")</span><span class="sxs-lookup"><span data-stu-id="ccf3c-200">![Add Members](./media/active-directory-saas-projectplace-tutorial/ic790232.png "Add Members")</span></span>

4. <span data-ttu-id="ccf3c-201">Dans la section **Add Member** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ccf3c-201">In the **Add Member** section, perform the following steps:</span></span>
   
    <span data-ttu-id="ccf3c-202">![Nouveaux membres](./media/active-directory-saas-projectplace-tutorial/ic790233.png "nouveaux membres")</span><span class="sxs-lookup"><span data-stu-id="ccf3c-202">![New Members](./media/active-directory-saas-projectplace-tutorial/ic790233.png "New Members")</span></span>
   
    <span data-ttu-id="ccf3c-203">a.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-203">a.</span></span> <span data-ttu-id="ccf3c-204">Dans la zone de texte **New Members** , entrez l’adresse de messagerie d’un compte Azure Active Directory valide que vous souhaitez approvisionner dans les zones de texte correspondantes.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-204">In the **New Members** textbox, type the email address of a valid AAD account you want to provision into the related textboxes.</span></span>
   
    <span data-ttu-id="ccf3c-205">b.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-205">b.</span></span> <span data-ttu-id="ccf3c-206">Cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-206">Click **Send**.</span></span>

   <span data-ttu-id="ccf3c-207">Un message électronique contenant un lien pour confirmer le compte avant qu’il ne soit activé est envoyé au titulaire du compte Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-207">An email including a link to confirm the account before it becomes active is sent to the Azure Active Directory account holder.</span></span>

>[!NOTE]
><span data-ttu-id="ccf3c-208">Vous pouvez utiliser tout autre outil ou n’importe quelle API de création de compte d’utilisateur fournis par Projectplace pour approvisionner des comptes d’utilisateur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-208">You can use any other Projectplace user account creation tools or APIs provided by Projectplace to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ccf3c-209">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="ccf3c-209">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ccf3c-210">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Projectplace.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-210">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Projectplace.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="ccf3c-212">**Pour affecter Britta Simon à Projectplace, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ccf3c-212">**To assign Britta Simon to Projectplace, perform the following steps:**</span></span>

1. <span data-ttu-id="ccf3c-213">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-213">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="ccf3c-215">Dans la liste des applications, sélectionnez **Projectplace**.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-215">In the applications list, select **Projectplace**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_app.png) 

3. <span data-ttu-id="ccf3c-217">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-217">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="ccf3c-219">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-219">Click **Add** button.</span></span> <span data-ttu-id="ccf3c-220">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="ccf3c-222">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-222">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ccf3c-223">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ccf3c-224">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ccf3c-225">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="ccf3c-225">Testing single sign-on</span></span>

<span data-ttu-id="ccf3c-226">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ccf3c-227">Lorsque vous cliquez sur la vignette Projectplace dans le panneau d’accès, vous êtes automatiquement connecté à votre application Projectplace.</span><span class="sxs-lookup"><span data-stu-id="ccf3c-227">When you click the Projectplace tile in the Access Panel, you should get automatically signed-on to your Projectplace application.</span></span>
<span data-ttu-id="ccf3c-228">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ccf3c-228">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ccf3c-229">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="ccf3c-229">Additional resources</span></span>

* [<span data-ttu-id="ccf3c-230">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ccf3c-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ccf3c-231">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="ccf3c-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_203.png

