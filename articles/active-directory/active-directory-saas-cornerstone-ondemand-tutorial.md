---
title: "Didacticiel : Intégration d’Azure Active Directory à Cornerstone OnDemand | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Cornerstone OnDemand."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f57c5fef-49b0-4591-91ef-fc0de6d654ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 8bb32588579a0d40b9ae7e0f823c6daab21c856e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cornerstone-ondemand"></a><span data-ttu-id="e7c2a-103">Didacticiel : Intégration d’Azure Active Directory à Cornerstone OnDemand</span><span class="sxs-lookup"><span data-stu-id="e7c2a-103">Tutorial: Azure Active Directory integration with Cornerstone OnDemand</span></span>

<span data-ttu-id="e7c2a-104">Dans ce didacticiel, vous allez découvrir comment intégrer Cornerstone OnDemand à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e7c2a-104">In this tutorial, you learn how to integrate Cornerstone OnDemand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e7c2a-105">L’intégration de Cornerstone OnDemand à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="e7c2a-105">Integrating Cornerstone OnDemand with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e7c2a-106">Dans Azure AD, vous pouvez contrôler qui a accès à Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-106">You can control in Azure AD who has access to Cornerstone OnDemand</span></span>
- <span data-ttu-id="e7c2a-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Cornerstone OnDemand (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-107">You can enable your users to automatically get signed-on to Cornerstone OnDemand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e7c2a-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="e7c2a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e7c2a-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e7c2a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e7c2a-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e7c2a-110">Prerequisites</span></span>

<span data-ttu-id="e7c2a-111">Pour configurer l’intégration d’Azure AD à Cornerstone OnDemand, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="e7c2a-111">To configure Azure AD integration with Cornerstone OnDemand, you need the following items:</span></span>

- <span data-ttu-id="e7c2a-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7c2a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e7c2a-113">Un abonnement Cornerstone OnDemand pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="e7c2a-113">A Cornerstone OnDemand single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e7c2a-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e7c2a-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="e7c2a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e7c2a-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e7c2a-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e7c2a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e7c2a-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="e7c2a-118">Scenario description</span></span>
<span data-ttu-id="e7c2a-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e7c2a-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="e7c2a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e7c2a-121">Ajout de Cornerstone OnDemand à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="e7c2a-121">Adding Cornerstone OnDemand from the gallery</span></span>
2. <span data-ttu-id="e7c2a-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7c2a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cornerstone-ondemand-from-the-gallery"></a><span data-ttu-id="e7c2a-123">Ajout de Cornerstone OnDemand à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="e7c2a-123">Adding Cornerstone OnDemand from the gallery</span></span>
<span data-ttu-id="e7c2a-124">Pour configurer l’intégration de Cornerstone OnDemand à Azure AD, vous devez ajouter Cornerstone OnDemand disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-124">To configure the integration of Cornerstone OnDemand into Azure AD, you need to add Cornerstone OnDemand from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e7c2a-125">**Pour ajouter Cornerstone OnDemand à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e7c2a-125">**To add Cornerstone OnDemand from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e7c2a-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e7c2a-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e7c2a-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="e7c2a-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="e7c2a-133">Dans la zone de recherche, tapez **Cornerstone OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-133">In the search box, type **Cornerstone OnDemand**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_search.png)

5. <span data-ttu-id="e7c2a-135">Dans le volet de résultats, sélectionnez **Cornerstone OnDemand**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-135">In the results panel, select **Cornerstone OnDemand**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e7c2a-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7c2a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e7c2a-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Cornerstone OnDemand avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="e7c2a-138">In this section, you configure and test Azure AD single sign-on with Cornerstone OnDemand based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e7c2a-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Cornerstone OnDemand équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cornerstone OnDemand is to a user in Azure AD.</span></span> <span data-ttu-id="e7c2a-140">En d’autres termes, une relation entre un utilisateur Azure AD et l’utilisateur Cornerstone OnDemand associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-140">In other words, a link relationship between an Azure AD user and the related user in Cornerstone OnDemand needs to be established.</span></span>

<span data-ttu-id="e7c2a-141">Dans Cornerstone OnDemand, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-141">In Cornerstone OnDemand, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e7c2a-142">Pour configurer et tester l’authentification unique Azure AD avec Cornerstone OnDemand, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="e7c2a-142">To configure and test Azure AD single sign-on with Cornerstone OnDemand, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e7c2a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e7c2a-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e7c2a-145">**[Création d’un utilisateur de test Cornerstone OnDemand](#creating-a-cornerstone-ondemand-test-user)** pour avoir un équivalent de Britta Simon dans Cornerstone OnDemand lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-145">**[Creating a Cornerstone OnDemand test user](#creating-a-cornerstone-ondemand-test-user)** - to have a counterpart of Britta Simon in Cornerstone OnDemand that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e7c2a-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e7c2a-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e7c2a-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7c2a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e7c2a-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cornerstone OnDemand application.</span></span>

<span data-ttu-id="e7c2a-150">**Pour configurer l’authentification unique Azure AD avec Cornerstone OnDemand, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e7c2a-150">**To configure Azure AD single sign-on with Cornerstone OnDemand, perform the following steps:**</span></span>

1. <span data-ttu-id="e7c2a-151">Dans le portail Azure, dans la page d’intégration de l’application **Cornerstone OnDemand**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-151">In the Azure portal, on the **Cornerstone OnDemand** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="e7c2a-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_samlbase.png)

3. <span data-ttu-id="e7c2a-155">Dans la section **Domaine et URL Cornerstone OnDemand**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="e7c2a-155">On the **Cornerstone OnDemand Domain and URLs** section, perform the following step:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_url.png)

    <span data-ttu-id="e7c2a-157">a.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-157">a.</span></span> <span data-ttu-id="e7c2a-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<company>.csod.com`</span><span class="sxs-lookup"><span data-stu-id="e7c2a-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.csod.com`</span></span>

    <span data-ttu-id="e7c2a-159">b.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-159">b.</span></span> <span data-ttu-id="e7c2a-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<company>.csod.com`</span><span class="sxs-lookup"><span data-stu-id="e7c2a-160">In **Identifier** textbox, type a URL using the following pattern: `https://<company>.csod.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e7c2a-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-161">These values are not real.</span></span> <span data-ttu-id="e7c2a-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e7c2a-163">Pour obtenir ces valeurs, contactez [l’équipe du support client Cornerstone OnDemand](mailTo:moreinfo@csod.com).</span><span class="sxs-lookup"><span data-stu-id="e7c2a-163">Contact [Cornerstone OnDemand Client support team](mailTo:moreinfo@csod.com) to get these values.</span></span> 
 
4. <span data-ttu-id="e7c2a-164">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_certificate.png) 

5. <span data-ttu-id="e7c2a-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="e7c2a-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e7c2a-168">Dans la section **Configuration de Cornerstone OnDemand**, cliquez sur **Configurer Cornerstone OnDemand** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-168">On the **Cornerstone OnDemand Configuration** section, click **Configure Cornerstone OnDemand** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e7c2a-169">Copiez **l’URL de déconnexion et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-169">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_configure.png) 

7. <span data-ttu-id="e7c2a-171">Pour configurer l’authentification unique côté **Cornerstone OnDemand**, vous devez envoyer le **Certificat** téléchargé, **l’URL de déconnexion** et **l’URL du service d’authentification unique SAML** à [l’équipe de support Cornerstone OnDemand](mailTo:moreinfo@csod.com).</span><span class="sxs-lookup"><span data-stu-id="e7c2a-171">To configure single sign-on on **Cornerstone OnDemand** side, you need to send the downloaded **Certificate**, **Sign-Out URL** and **SAML Single Sign-On Service URL**  to [Cornerstone OnDemand support team](mailTo:moreinfo@csod.com).</span></span> <span data-ttu-id="e7c2a-172">Elle configure ce paramètre pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="e7c2a-173">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e7c2a-174">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e7c2a-175">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e7c2a-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e7c2a-176">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7c2a-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="e7c2a-177">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="e7c2a-179">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e7c2a-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e7c2a-180">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e7c2a-182">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e7c2a-184">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e7c2a-186">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="e7c2a-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e7c2a-188">a.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-188">a.</span></span> <span data-ttu-id="e7c2a-189">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e7c2a-190">b.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-190">b.</span></span> <span data-ttu-id="e7c2a-191">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e7c2a-192">c.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-192">c.</span></span> <span data-ttu-id="e7c2a-193">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e7c2a-194">d.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-194">d.</span></span> <span data-ttu-id="e7c2a-195">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-195">Click **Create**.</span></span>
 
### <a name="creating-a-cornerstone-ondemand-test-user"></a><span data-ttu-id="e7c2a-196">Création d’un utilisateur de test Cornerstone OnDemand</span><span class="sxs-lookup"><span data-stu-id="e7c2a-196">Creating a Cornerstone OnDemand test user</span></span>

<span data-ttu-id="e7c2a-197">Pour se connecter à Cornerstone OnDemand, les utilisateurs d’Azure AD doivent être approvisionnés dans Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-197">In order to enable Azure AD users to log into Cornerstone OnDemand, they must be provisioned into Cornerstone OnDemand.</span></span> <span data-ttu-id="e7c2a-198">Dans le cas de Cornerstone OnDemand, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-198">In the case of Cornerstone OnDemand, provisioning is a manual task.</span></span>

<span data-ttu-id="e7c2a-199">Pour configurer l’attribution d’utilisateurs, envoyez les informations sur l’utilisateur Azure AD que vous souhaitez approvisionner (par exemple le nom, l’adresse e-mail) à [l’équipe du support technique Cornerstone OnDemand](mailTo:moreinfo@csod.com).</span><span class="sxs-lookup"><span data-stu-id="e7c2a-199">To configure user provisioning, send the information (e.g.: Name, Email) about the Azure AD user you want to provision to the [Cornerstone OnDemand support team](mailTo:moreinfo@csod.com).</span></span>

>[!NOTE]
><span data-ttu-id="e7c2a-200">Vous pouvez utiliser tout autre outil ou API de création de compte d’utilisateur fourni par Cornerstone OnDemand pour approvisionner des comptes d’utilisateurs AAD.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-200">You can use any other Cornerstone OnDemand user account creation tools or APIs provided by Cornerstone OnDemand to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e7c2a-201">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7c2a-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e7c2a-202">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cornerstone OnDemand.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="e7c2a-204">**Pour affecter Britta Simon à Cornerstone OnDemand, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e7c2a-204">**To assign Britta Simon to Cornerstone OnDemand, perform the following steps:**</span></span>

1. <span data-ttu-id="e7c2a-205">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="e7c2a-207">Dans la liste des applications, sélectionnez **Cornerstone OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-207">In the applications list, select **Cornerstone OnDemand**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_app.png) 

3. <span data-ttu-id="e7c2a-209">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="e7c2a-211">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-211">Click **Add** button.</span></span> <span data-ttu-id="e7c2a-212">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="e7c2a-214">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e7c2a-215">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e7c2a-216">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e7c2a-217">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="e7c2a-217">Testing single sign-on</span></span>

<span data-ttu-id="e7c2a-218">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-218">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e7c2a-219">Lorsque vous cliquez sur la vignette Cornerstone OnDemand dans le volet d’accès, vous devez être connecté automatiquement à votre application Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="e7c2a-219">When you click the Cornerstone OnDemand tile in the Access Panel, you should get automatically signed-on to your Cornerstone OnDemand application.</span></span>
<span data-ttu-id="e7c2a-220">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e7c2a-220">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e7c2a-221">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="e7c2a-221">Additional resources</span></span>

* [<span data-ttu-id="e7c2a-222">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e7c2a-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e7c2a-223">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="e7c2a-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_203.png

