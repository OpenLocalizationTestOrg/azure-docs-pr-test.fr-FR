---
title: "Didacticiel : intégration d’Azure Active Directory à Humanity | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Humanity."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6aa771e9-31c6-48d1-8dde-024bebc06943
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 327cc1e3d0836e79376e0a3cd5a4422a967f5943
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-humanity"></a><span data-ttu-id="2fce3-103">Didacticiel : intégration d’Azure Active Directory à Humanity</span><span class="sxs-lookup"><span data-stu-id="2fce3-103">Tutorial: Azure Active Directory integration with Humanity</span></span>

<span data-ttu-id="2fce3-104">L’objectif de ce didacticiel est de vous apprendre à intégrer Humanity à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2fce3-104">In this tutorial, you learn how to integrate Humanity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2fce3-105">Intégrer Humanity à Azure AD offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="2fce3-105">Integrating Humanity with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2fce3-106">Dans Azure AD, vous pouvez contrôler l’accès à Humanity</span><span class="sxs-lookup"><span data-stu-id="2fce3-106">You can control in Azure AD who has access to Humanity</span></span>
- <span data-ttu-id="2fce3-107">Vous pouvez autoriser vos utilisateurs à être automatiquement connectés à Humanity (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="2fce3-107">You can enable your users to automatically get signed-on to Humanity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2fce3-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="2fce3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2fce3-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2fce3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2fce3-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="2fce3-110">Prerequisites</span></span>

<span data-ttu-id="2fce3-111">Pour configurer l’intégration d’Azure AD avec Humanity, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2fce3-111">To configure Azure AD integration with Humanity, you need the following items:</span></span>

- <span data-ttu-id="2fce3-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="2fce3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2fce3-113">Un abonnement Humanity pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="2fce3-113">A Humanity single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2fce3-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="2fce3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2fce3-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="2fce3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2fce3-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="2fce3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2fce3-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2fce3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2fce3-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="2fce3-118">Scenario description</span></span>
<span data-ttu-id="2fce3-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="2fce3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2fce3-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="2fce3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2fce3-121">Ajouter Humanity à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="2fce3-121">Adding Humanity from the gallery</span></span>
2. <span data-ttu-id="2fce3-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2fce3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-humanity-from-the-gallery"></a><span data-ttu-id="2fce3-123">Ajouter Humanity à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="2fce3-123">Adding Humanity from the gallery</span></span>
<span data-ttu-id="2fce3-124">Pour configurer l’intégration de Humanity à Azure AD, vous devez ajouter Humanity, disponible à partir de la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="2fce3-124">To configure the integration of Humanity into Azure AD, you need to add Humanity from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2fce3-125">**Pour ajouter Humanity à partir de la galerie, réalisez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="2fce3-125">**To add Humanity from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2fce3-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2fce3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2fce3-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="2fce3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2fce3-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="2fce3-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="2fce3-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="2fce3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="2fce3-133">Dans la zone de recherche, tapez **Humanity**.</span><span class="sxs-lookup"><span data-stu-id="2fce3-133">In the search box, type **Humanity**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_search.png)

5. <span data-ttu-id="2fce3-135">Dans le panneau de résultats, sélectionnez **Humanity**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="2fce3-135">In the results panel, select **Humanity**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2fce3-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2fce3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2fce3-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Humanity, grâce à un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="2fce3-138">In this section, you configure and test Azure AD single sign-on with Humanity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2fce3-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Humanity correspondant dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2fce3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Humanity is to a user in Azure AD.</span></span> <span data-ttu-id="2fce3-140">En d’autres termes, il faut établir une relation entre l’utilisateur Azure AD et l’utilisateur Humanity associé.</span><span class="sxs-lookup"><span data-stu-id="2fce3-140">In other words, a link relationship between an Azure AD user and the related user in Humanity needs to be established.</span></span>

<span data-ttu-id="2fce3-141">Dans Humanity, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **Nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="2fce3-141">In Humanity, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2fce3-142">Pour configurer et tester l’authentification unique Azure AD avec Humanity, vous devez compléter les instructions des blocs de construction suivants :</span><span class="sxs-lookup"><span data-stu-id="2fce3-142">To configure and test Azure AD single sign-on with Humanity, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2fce3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="2fce3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2fce3-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2fce3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2fce3-145">**[Création d’un utilisateur de test Humanity](#creating-a-humanity-test-user)** pour avoir un équivalent de Britta Simon dans Humanity qui est lié à la représentation d’un utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2fce3-145">**[Creating a Humanity test user](#creating-a-humanity-test-user)** - to have a counterpart of Britta Simon in Humanity that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2fce3-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2fce3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2fce3-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="2fce3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2fce3-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2fce3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2fce3-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Humanity.</span><span class="sxs-lookup"><span data-stu-id="2fce3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Humanity application.</span></span>

<span data-ttu-id="2fce3-150">**Pour configurer l’authentification unique Azure AD avec Humanity, réalisez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="2fce3-150">**To configure Azure AD single sign-on with Humanity, perform the following steps:**</span></span>

1. <span data-ttu-id="2fce3-151">Dans le portail Azure, sur la page d’intégration de l’application **Humanity**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="2fce3-151">In the Azure portal, on the **Humanity** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="2fce3-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="2fce3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_samlbase.png)

3. <span data-ttu-id="2fce3-155">Sur la section **Domaine et URL Humanity**, réalisez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="2fce3-155">On the **Humanity Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_url.png)

    <span data-ttu-id="2fce3-157">a.</span><span class="sxs-lookup"><span data-stu-id="2fce3-157">a.</span></span> <span data-ttu-id="2fce3-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://company.humanity.com/includes/saml/`</span><span class="sxs-lookup"><span data-stu-id="2fce3-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://company.humanity.com/includes/saml/`</span></span>

    <span data-ttu-id="2fce3-159">b.</span><span class="sxs-lookup"><span data-stu-id="2fce3-159">b.</span></span> <span data-ttu-id="2fce3-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://company.humanity.com/app/`</span><span class="sxs-lookup"><span data-stu-id="2fce3-160">In the **Identifier** textbox, type a URL using the following pattern: `https://company.humanity.com/app/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2fce3-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="2fce3-161">These values are not real.</span></span> <span data-ttu-id="2fce3-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="2fce3-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="2fce3-163">Pour obtenir ces valeurs, contactez l’[équipe de support aux clients Humanity](https://www.humanity.com/support/).</span><span class="sxs-lookup"><span data-stu-id="2fce3-163">Contact [Humanity Client support team](https://www.humanity.com/support/) to get these values.</span></span> 
 
4. <span data-ttu-id="2fce3-164">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="2fce3-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_certificate.png) 

5. <span data-ttu-id="2fce3-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="2fce3-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2fce3-168">Pour ouvrir la fenêtre **Configurer l’authentification**, sur la section **Configuration Humanity**, cliquez sur **Configurer Humanity**.</span><span class="sxs-lookup"><span data-stu-id="2fce3-168">On the **Humanity Configuration** section, click **Configure Humanity** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2fce3-169">Copiez l’**URL du service d’authentification unique SAML et l’URL de déconnexion** à partir de la section **Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="2fce3-169">Copy the **SAML Single Sign-On Service URL, and Sign-Out URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_configure.png) 

7. <span data-ttu-id="2fce3-171">Dans une autre fenêtre de navigateur web, ouvrez une session sur votre site d’entreprise **Humanity** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="2fce3-171">In a different web browser window, log in to your **Humanity** company site as an administrator.</span></span>

8. <span data-ttu-id="2fce3-172">Dans le menu situé en haut, cliquez sur **Admin**.</span><span class="sxs-lookup"><span data-stu-id="2fce3-172">In the menu on the top, click **Admin**.</span></span>
   
    <span data-ttu-id="2fce3-173">![Administrateur](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Administrateur")</span><span class="sxs-lookup"><span data-stu-id="2fce3-173">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span></span>

9. <span data-ttu-id="2fce3-174">Sous **Integration**, cliquez sur **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="2fce3-174">Under **Integration**, click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="2fce3-175">![Authentification unique](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "Authentification unique")</span><span class="sxs-lookup"><span data-stu-id="2fce3-175">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "Single Sign-On")</span></span>

10. <span data-ttu-id="2fce3-176">Dans la section **Single Sign-On** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2fce3-176">In the **Single Sign-On** section, perform the following steps:</span></span>
   
    <span data-ttu-id="2fce3-177">![Authentification unique](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "Authentification unique")</span><span class="sxs-lookup"><span data-stu-id="2fce3-177">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "Single Sign-On")</span></span>
   
    <span data-ttu-id="2fce3-178">a.</span><span class="sxs-lookup"><span data-stu-id="2fce3-178">a.</span></span> <span data-ttu-id="2fce3-179">Sélectionnez **SAML Enabled**.</span><span class="sxs-lookup"><span data-stu-id="2fce3-179">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="2fce3-180">b.</span><span class="sxs-lookup"><span data-stu-id="2fce3-180">b.</span></span> <span data-ttu-id="2fce3-181">Sélectionnez **Allow Password Login**.</span><span class="sxs-lookup"><span data-stu-id="2fce3-181">Select **Allow Password Login**.</span></span>

    <span data-ttu-id="2fce3-182">c.</span><span class="sxs-lookup"><span data-stu-id="2fce3-182">c.</span></span> <span data-ttu-id="2fce3-183">Collez la valeur de l’**URL du service d’authentification unique SAML** dans la zone de texte **URL de l’émetteur SAML**.</span><span class="sxs-lookup"><span data-stu-id="2fce3-183">Paste the **SAML Single Sign-On Service URL** value into the **SAML Issuer URL** textbox.</span></span>

    <span data-ttu-id="2fce3-184">d.</span><span class="sxs-lookup"><span data-stu-id="2fce3-184">d.</span></span> <span data-ttu-id="2fce3-185">Collez la valeur de l’**URL de déconnexion** dans la zone de texte **URL de déconnexion distante**.</span><span class="sxs-lookup"><span data-stu-id="2fce3-185">Paste the **Sign-Out URL** value into the **Remote Logout URL** textbox.</span></span>
   
    <span data-ttu-id="2fce3-186">e.</span><span class="sxs-lookup"><span data-stu-id="2fce3-186">e.</span></span> <span data-ttu-id="2fce3-187">Ouvrez votre certificat codé en base 64 dans le Bloc-notes, copiez son contenu dans le Presse-papiers, puis collez-le dans la zone de texte **X.509 Certificate** .</span><span class="sxs-lookup"><span data-stu-id="2fce3-187">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.</span></span>

11. <span data-ttu-id="2fce3-188">Cliquez sur **Save Settings**.</span><span class="sxs-lookup"><span data-stu-id="2fce3-188">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="2fce3-189">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="2fce3-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2fce3-190">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="2fce3-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2fce3-191">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2fce3-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2fce3-192">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="2fce3-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="2fce3-193">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2fce3-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="2fce3-195">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2fce3-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2fce3-196">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2fce3-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2fce3-198">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="2fce3-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2fce3-200">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="2fce3-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2fce3-202">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2fce3-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2fce3-204">a.</span><span class="sxs-lookup"><span data-stu-id="2fce3-204">a.</span></span> <span data-ttu-id="2fce3-205">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2fce3-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2fce3-206">b.</span><span class="sxs-lookup"><span data-stu-id="2fce3-206">b.</span></span> <span data-ttu-id="2fce3-207">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2fce3-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2fce3-208">c.</span><span class="sxs-lookup"><span data-stu-id="2fce3-208">c.</span></span> <span data-ttu-id="2fce3-209">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="2fce3-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2fce3-210">d.</span><span class="sxs-lookup"><span data-stu-id="2fce3-210">d.</span></span> <span data-ttu-id="2fce3-211">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="2fce3-211">Click **Create**.</span></span>
 
### <a name="creating-a-humanity-test-user"></a><span data-ttu-id="2fce3-212">Créer un utilisateur de test Humanity</span><span class="sxs-lookup"><span data-stu-id="2fce3-212">Creating a Humanity test user</span></span>

<span data-ttu-id="2fce3-213">Pour permettre aux utilisateurs Azure AD de se connecter à Humanity, vous devez les approvisionner dans Humanity.</span><span class="sxs-lookup"><span data-stu-id="2fce3-213">In order to enable Azure AD users to log in to Humanity, they must be provisioned into Humanity.</span></span> <span data-ttu-id="2fce3-214">Dans le cas de Humanity, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="2fce3-214">In the case of Humanity, provisioning is a manual task.</span></span>

<span data-ttu-id="2fce3-215">**Pour approvisionner un compte d’utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2fce3-215">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="2fce3-216">Ouvrez une session en tant qu’administrateur sur votre site d’entreprise **Humanity**.</span><span class="sxs-lookup"><span data-stu-id="2fce3-216">Log in to your **Humanity** company site as an administrator.</span></span>

2. <span data-ttu-id="2fce3-217">Cliquez sur **Admin**.</span><span class="sxs-lookup"><span data-stu-id="2fce3-217">Click **Admin**.</span></span>
   
    <span data-ttu-id="2fce3-218">![Administrateur](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Administrateur")</span><span class="sxs-lookup"><span data-stu-id="2fce3-218">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span></span>

3. <span data-ttu-id="2fce3-219">Cliquez sur **Staff**.</span><span class="sxs-lookup"><span data-stu-id="2fce3-219">Click **Staff**.</span></span>
   
    <span data-ttu-id="2fce3-220">![Staff](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "Staff")</span><span class="sxs-lookup"><span data-stu-id="2fce3-220">![Staff](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "Staff")</span></span>

4. <span data-ttu-id="2fce3-221">Sous **Actions**, cliquez sur **Ajouter des employés**.</span><span class="sxs-lookup"><span data-stu-id="2fce3-221">Under **Actions**, click **Add Employees**.</span></span>
   
    <span data-ttu-id="2fce3-222">![Add Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "Add Employees")</span><span class="sxs-lookup"><span data-stu-id="2fce3-222">![Add Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "Add Employees")</span></span>

5. <span data-ttu-id="2fce3-223">Dans la section **Add employees** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2fce3-223">In the **Add Employees** section, perform the following steps:</span></span>
   
    <span data-ttu-id="2fce3-224">![Save Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "Save Employees")</span><span class="sxs-lookup"><span data-stu-id="2fce3-224">![Save Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "Save Employees")</span></span>
   
    <span data-ttu-id="2fce3-225">a.</span><span class="sxs-lookup"><span data-stu-id="2fce3-225">a.</span></span> <span data-ttu-id="2fce3-226">Indiquez dans les zones de texte correspondantes le **prénom**, le **nom** et **l’e-mail** du compte AAD valide que vous souhaitez approvisionner.</span><span class="sxs-lookup"><span data-stu-id="2fce3-226">Type the **First Name**, **Last Name**, and **Email** of a valid AAD account you want to provision into the related textboxes.</span></span>

    <span data-ttu-id="2fce3-227">b.</span><span class="sxs-lookup"><span data-stu-id="2fce3-227">b.</span></span> <span data-ttu-id="2fce3-228">Cliquez sur **Save Employees**.</span><span class="sxs-lookup"><span data-stu-id="2fce3-228">Click **Save Employees**.</span></span>

>[!NOTE]
><span data-ttu-id="2fce3-229">Vous pouvez utiliser n’importe quel autre outil ou API de création de compte d’utilisateur Humanity fourni par ce site pour approvisionner des comptes d’utilisateurs AAD.</span><span class="sxs-lookup"><span data-stu-id="2fce3-229">You can use any other Humanity user account creation tools or APIs provided by Humanity to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2fce3-230">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="2fce3-230">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2fce3-231">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Humanity.</span><span class="sxs-lookup"><span data-stu-id="2fce3-231">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Humanity.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="2fce3-233">**Pour assigner Britta Simon à Humanity, réalisez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="2fce3-233">**To assign Britta Simon to Humanity, perform the following steps:**</span></span>

1. <span data-ttu-id="2fce3-234">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="2fce3-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="2fce3-236">Dans la liste des applications, sélectionnez **Humanity**.</span><span class="sxs-lookup"><span data-stu-id="2fce3-236">In the applications list, select **Humanity**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_app.png) 

3. <span data-ttu-id="2fce3-238">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="2fce3-238">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="2fce3-240">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="2fce3-240">Click **Add** button.</span></span> <span data-ttu-id="2fce3-241">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="2fce3-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="2fce3-243">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="2fce3-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2fce3-244">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="2fce3-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2fce3-245">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="2fce3-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2fce3-246">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="2fce3-246">Testing single sign-on</span></span>

<span data-ttu-id="2fce3-247">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="2fce3-247">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2fce3-248">En cliquant sur la vignette Humanity dans le Panneau d’accès, vous allez en principe être connecté automatiquement à votre application Humanity.</span><span class="sxs-lookup"><span data-stu-id="2fce3-248">When you click the Humanity tile in the Access Panel, you should get automatically signed-on to your Humanity application.</span></span>
<span data-ttu-id="2fce3-249">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2fce3-249">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2fce3-250">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="2fce3-250">Additional resources</span></span>

* [<span data-ttu-id="2fce3-251">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2fce3-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2fce3-252">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="2fce3-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_203.png

