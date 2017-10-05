---
title: "Didacticiel : Intégration d’Azure Active Directory à Clarizen | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Clarizen."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 574c6877bddac8be7d6d541bfabbdc10f6be3101
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clarizen"></a><span data-ttu-id="66e63-103">Didacticiel : Intégration d’Azure Active Directory à Clarizen</span><span class="sxs-lookup"><span data-stu-id="66e63-103">Tutorial: Azure Active Directory integration with Clarizen</span></span>

<span data-ttu-id="66e63-104">Dans ce didacticiel, vous allez apprendre à intégrer Azure Active Directory (Azure AD) à Clarizen.</span><span class="sxs-lookup"><span data-stu-id="66e63-104">In this tutorial, you learn how to integrate Azure Active Directory (Azure AD) with Clarizen.</span></span> <span data-ttu-id="66e63-105">Cette intégration vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="66e63-105">This integration gives you the following benefits:</span></span>

- <span data-ttu-id="66e63-106">Dans Azure AD, vous pouvez contrôler qui a accès à Clarizen.</span><span class="sxs-lookup"><span data-stu-id="66e63-106">You can control, in Azure AD, who has access to Clarizen.</span></span>
- <span data-ttu-id="66e63-107">Vous pouvez permettre aux utilisateurs de se connecter automatiquement à Clarizen (par le biais de l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="66e63-107">You can enable your users to be automatically signed in to Clarizen (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="66e63-108">Vous pouvez centraliser la gestion de vos comptes à un seul emplacement : le Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="66e63-108">You can manage your accounts in one central location, the Azure portal.</span></span>

<span data-ttu-id="66e63-109">Selon le scénario considéré dans ce didacticiel, vous allez exécuter deux tâches principales :</span><span class="sxs-lookup"><span data-stu-id="66e63-109">The scenario in this tutorial consists of two main tasks:</span></span>

1. <span data-ttu-id="66e63-110">Ajoutez Clarizen à partir de la galerie.</span><span class="sxs-lookup"><span data-stu-id="66e63-110">Add Clarizen from the gallery.</span></span>
2. <span data-ttu-id="66e63-111">Configurez et testez l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="66e63-111">Configure and test Azure AD single sign-on.</span></span>

<span data-ttu-id="66e63-112">Pour plus d’informations sur l’intégration d’applications SaaS (software as a service) à Azure AD, consultez l’article [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="66e63-112">If you want more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66e63-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="66e63-113">Prerequisites</span></span>
<span data-ttu-id="66e63-114">Pour configurer l’intégration d’Azure AD à Clarizen, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="66e63-114">To configure Azure AD integration with Clarizen, you need the following items:</span></span>

- <span data-ttu-id="66e63-115">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="66e63-115">An Azure AD subscription</span></span>
- <span data-ttu-id="66e63-116">Un abonnement Clarizen activé pour l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="66e63-116">A Clarizen subscription that's enabled for single sign-on</span></span>

<span data-ttu-id="66e63-117">Pour tester la procédure de ce didacticiel, suivez les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="66e63-117">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="66e63-118">Testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="66e63-118">Test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="66e63-119">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="66e63-119">Don't use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="66e63-120">Si vous ne disposez pas d’un environnement de test Azure AD, vous pouvez [vous inscrire pour un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="66e63-120">If you don't have an Azure AD test environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="add-clarizen-from-the-gallery"></a><span data-ttu-id="66e63-121">Ajouter Clarizen à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="66e63-121">Add Clarizen from the gallery</span></span>
<span data-ttu-id="66e63-122">Pour configurer l’intégration de Clarizen à Azure AD, ajoutez Clarizen à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="66e63-122">To configure the integration of Clarizen into Azure AD, add Clarizen from the gallery to your list of managed SaaS apps.</span></span>

1. <span data-ttu-id="66e63-123">Dans le volet gauche du [Portail Azure](https://portal.azure.com), cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="66e63-123">In the [Azure portal](https://portal.azure.com), in the left pane, click the **Azure Active Directory** icon.</span></span>

    ![Icône Azure Active Directory][1]

2. <span data-ttu-id="66e63-125">Cliquez sur **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="66e63-125">Click **Enterprise applications**.</span></span> <span data-ttu-id="66e63-126">Puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="66e63-126">Then click **All applications**.</span></span>

    ![Sélection des options « Applications d’entreprise » et « Toutes les applications »][2]

3. <span data-ttu-id="66e63-128">Cliquez sur le bouton **Ajouter** au bas de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="66e63-128">Click the **Add** button at the top of the dialog box.</span></span>

    ![Bouton « Ajouter »][3]

4. <span data-ttu-id="66e63-130">Dans la zone de recherche, tapez **Clarizen**.</span><span class="sxs-lookup"><span data-stu-id="66e63-130">In the search box, type **Clarizen**.</span></span>

    ![Saisie de « Clarizen » dans la zone de recherche](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_000.png)

5. <span data-ttu-id="66e63-132">Dans le volet de résultats, sélectionnez **Clarizen**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="66e63-132">In the results pane, select **Clarizen**, and then click **Add** to add the application.</span></span>

    ![Sélection de Clarizen dans le volet de résultats](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_0001.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="66e63-134">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="66e63-134">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="66e63-135">Dans les sections suivantes, vous allez configurer et tester l’authentification unique Azure AD avec Clarizen pour l’utilisateur de test nommé Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="66e63-135">In the following sections, you configure and test Azure AD single sign-on with Clarizen based on the test user Britta Simon.</span></span>

<span data-ttu-id="66e63-136">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Clarizen équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="66e63-136">For single sign-on to work, Azure AD needs to know what the counterpart user in Clarizen is to a user in Azure AD.</span></span> <span data-ttu-id="66e63-137">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Clarizen associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="66e63-137">In other words, a link relationship between an Azure AD user and the related user in Clarizen needs to be established.</span></span> <span data-ttu-id="66e63-138">Pour cela, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du champ **Username** (Nom d’utilisateur) dans Clarizen.</span><span class="sxs-lookup"><span data-stu-id="66e63-138">You establish this link relationship by assigning the value of **user name** in Azure AD as the value of **Username** in Clarizen.</span></span>

<span data-ttu-id="66e63-139">Pour configurer et tester l’authentification unique Azure AD avec Clarizen, suivez les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="66e63-139">To configure and test Azure AD single sign-on with Clarizen, complete the following building blocks:</span></span>

1. <span data-ttu-id="66e63-140">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="66e63-140">**[Configure Azure AD single sign-on](#configure-azure-ad-single-sign-on)** to enable your users to use this feature.</span></span>
2. <span data-ttu-id="66e63-141">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="66e63-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="66e63-142">**[Créer un utilisateur de test Clarizen](#create-a-clarizen-test-user)** pour disposer d’un équivalent de Britta Simon dans Clarizen lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="66e63-142">**[Create a Clarizen test user](#create-a-clarizen-test-user)** to have a counterpart of Britta Simon in Clarizen that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="66e63-143">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="66e63-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="66e63-144">**[Tester l’authentification unique](#test-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="66e63-144">**[Test single sign-on](#test-single-sign-on)** to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="66e63-145">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="66e63-145">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="66e63-146">Activez l’authentification unique Azure AD dans le Portail Azure et configurez l’authentification unique dans votre application Clarizen.</span><span class="sxs-lookup"><span data-stu-id="66e63-146">Enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Clarizen application.</span></span>

1. <span data-ttu-id="66e63-147">Dans le Portail Azure, sur la page d’intégration de l’application **Clarizen**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="66e63-147">In the Azure portal, on the **Clarizen** application integration page, click **Single sign-on**.</span></span>

    ![Sélection de l’option « Authentification unique »][4]

2. <span data-ttu-id="66e63-149">Dans la boîte de dialogue **Authentification unique**, au niveau de la zone **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="66e63-149">In the **Single sign-on** dialog box, for **Mode**, select **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Sélection de l’option « Authentification basée sur SAML »](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_01.png)

3. <span data-ttu-id="66e63-151">Dans la section **Domaine et URL Clarizen**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="66e63-151">In the **Clarizen Domain and URLs** section, perform the following steps:</span></span>

    ![Zones d’identificateur et d’URL de réponse](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_02.png)

    <span data-ttu-id="66e63-153">a.</span><span class="sxs-lookup"><span data-stu-id="66e63-153">a.</span></span> <span data-ttu-id="66e63-154">Dans la zone **Identificateur**, tapez la valeur **Clarizen**.</span><span class="sxs-lookup"><span data-stu-id="66e63-154">In the **Identifier** box, type the value as: **Clarizen**</span></span>

    <span data-ttu-id="66e63-155">b.</span><span class="sxs-lookup"><span data-stu-id="66e63-155">b.</span></span> <span data-ttu-id="66e63-156">Dans la zone **URL de réponse**, tapez une URL en utilisant le modèle suivant : **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span><span class="sxs-lookup"><span data-stu-id="66e63-156">In the **Reply URL** box, type a URL by using the following pattern: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span></span>

    > [!NOTE]
    > <span data-ttu-id="66e63-157">Il ne s’agit pas des valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="66e63-157">These are not the real values.</span></span> <span data-ttu-id="66e63-158">Vous devrez utiliser les véritables valeurs d’identificateur et d’URL de réponse.</span><span class="sxs-lookup"><span data-stu-id="66e63-158">You have to use the actual identifier and reply URL.</span></span> <span data-ttu-id="66e63-159">Nous vous suggérons d’utiliser ici la valeur unique d’une chaîne en guise d’identificateur.</span><span class="sxs-lookup"><span data-stu-id="66e63-159">Here we suggest that you use the unique value of a string as the identifier.</span></span> <span data-ttu-id="66e63-160">Pour obtenir les valeurs réelles, contactez [l’équipe de support technique Clarizen](https://success.clarizen.com/hc/en-us/requests/new).</span><span class="sxs-lookup"><span data-stu-id="66e63-160">To get the actual values, contact the [Clarizen support team](https://success.clarizen.com/hc/en-us/requests/new).</span></span>

4. <span data-ttu-id="66e63-161">Dans la section **Certificat de signature SAML**, cliquez sur **Créer un certificat**.</span><span class="sxs-lookup"><span data-stu-id="66e63-161">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Sélection de l’option « Créer un certificat »](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_03.png)  

5. <span data-ttu-id="66e63-163">Dans la boîte de dialogue **Créer un certificat**, cliquez sur l’icône de calendrier et sélectionnez une date d’expiration.</span><span class="sxs-lookup"><span data-stu-id="66e63-163">In the **Create New Certificate** dialog box, click the calendar icon and select an expiry date.</span></span> <span data-ttu-id="66e63-164">Cliquez ensuite sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="66e63-164">Then click **Save**.</span></span>

    ![Sélection et enregistrement d’une date d’expiration](./media/active-directory-saas-clarizen-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="66e63-166">Dans la section **Certificat de signature SAML**, sélectionnez **Activer le nouveau certificat**, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="66e63-166">In the **SAML Signing Certificate** section, select **Make new certificate active**, and then click **Save**.</span></span>

    ![Sélection de la case à cocher pour activer le nouveau certificat](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_04.png)

7. <span data-ttu-id="66e63-168">Dans la boîte de dialogue **Certificat de substitution**, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="66e63-168">In the **Rollover certificate** dialog box, click **OK**.</span></span>

    ![Sélection du bouton « OK » pour confirmer l’activation du certificat](./media/active-directory-saas-clarizen-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="66e63-170">Dans la section **Certificat de signature SAML**, cliquez sur **Certificat (Base64)**, puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="66e63-170">In the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Sélection de l’option « Certificat (Base64) » pour démarrer le téléchargement](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_05.png)

9. <span data-ttu-id="66e63-172">Dans la section **Configuration de Clarizen** , cliquez sur **Configurer Clarizen** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="66e63-172">In the **Clarizen Configuration** section, click **Configure Clarizen** to open the **Configure sign-on** window.</span></span>

    ![Sélection de l’option « Configurer Clarizen »](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_06.png)

    ![Fenêtre « Configurer l’authentification », incluant les URL et les fichiers](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_07.png)

10. <span data-ttu-id="66e63-175">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Clarizen en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="66e63-175">In a different web browser window, sign in to your Clarizen company site as an administrator.</span></span>

11. <span data-ttu-id="66e63-176">Cliquez sur votre nom d’utilisateur, puis sur **Settings** (Paramètres).</span><span class="sxs-lookup"><span data-stu-id="66e63-176">Click your username, and then click **Settings**.</span></span>

    <span data-ttu-id="66e63-177">![Sélection de l’option « Settings » (Paramètres) sous votre nom d’utilisateur](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "Settings") (Paramètres)</span><span class="sxs-lookup"><span data-stu-id="66e63-177">![Clicking "Settings" under your username](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "Settings")</span></span>

12. <span data-ttu-id="66e63-178">Cliquez sur l’onglet **Global Settings** (Paramètres globaux).</span><span class="sxs-lookup"><span data-stu-id="66e63-178">Click the **Global Settings** tab.</span></span> <span data-ttu-id="66e63-179">En regard de la zone **Federated Authentication** (Authentification fédérée), cliquez sur **edit** (modifier).</span><span class="sxs-lookup"><span data-stu-id="66e63-179">Then, next to **Federated Authentication**, click **edit**.</span></span>

    <span data-ttu-id="66e63-180">![Onglet « Global Settings » (Paramètres globaux)](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "Global Settings") (Paramètres globaux)</span><span class="sxs-lookup"><span data-stu-id="66e63-180">!["Global Settings" tab](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "Global Settings")</span></span>

13. <span data-ttu-id="66e63-181">Dans la boîte de dialogue **Federated Authentication** (Authentification fédérée), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="66e63-181">In the **Federated Authentication** dialog box, perform the following steps:</span></span>

    <span data-ttu-id="66e63-182">![Boîte de dialogue « Federated Authentication » (Authentification fédérée)](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Federated Authentication") (Authentification fédérée)</span><span class="sxs-lookup"><span data-stu-id="66e63-182">!["Federated Authentication" dialog box](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Federated Authentication")</span></span>

    <span data-ttu-id="66e63-183">a.</span><span class="sxs-lookup"><span data-stu-id="66e63-183">a.</span></span> <span data-ttu-id="66e63-184">Sélectionnez **Activer l'authentification fédérée**.</span><span class="sxs-lookup"><span data-stu-id="66e63-184">Select **Enable Federated Authentication**.</span></span>

    <span data-ttu-id="66e63-185">b.</span><span class="sxs-lookup"><span data-stu-id="66e63-185">b.</span></span> <span data-ttu-id="66e63-186">Cliquez sur **Upload** pour charger votre certificat téléchargé.</span><span class="sxs-lookup"><span data-stu-id="66e63-186">Click **Upload** to upload your downloaded certificate.</span></span>

    <span data-ttu-id="66e63-187">c.</span><span class="sxs-lookup"><span data-stu-id="66e63-187">c.</span></span> <span data-ttu-id="66e63-188">Dans la zone **Sign-in URL** (URL de connexion), entrez la valeur de la zone **URL du service d’authentification unique SAML** indiquée dans la fenêtre Configuration de l’application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="66e63-188">In the **Sign-in URL** box, enter the value of **SAML Single Sign-On Service URL** from the Azure AD application configuration window.</span></span>

    <span data-ttu-id="66e63-189">d.</span><span class="sxs-lookup"><span data-stu-id="66e63-189">d.</span></span> <span data-ttu-id="66e63-190">Dans la zone **Sign-in URL** (URL de connexion), entrez la valeur de la zone **URL de déconnexion** indiquée dans la fenêtre Configuration de l’application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="66e63-190">In the **Sign-out URL** box, enter the value of **Sign-Out URL** from the Azure AD application configuration window.</span></span>

    <span data-ttu-id="66e63-191">e.</span><span class="sxs-lookup"><span data-stu-id="66e63-191">e.</span></span> <span data-ttu-id="66e63-192">Sélectionnez **Use POST**.</span><span class="sxs-lookup"><span data-stu-id="66e63-192">Select **Use POST**.</span></span>

    <span data-ttu-id="66e63-193">f.</span><span class="sxs-lookup"><span data-stu-id="66e63-193">f.</span></span> <span data-ttu-id="66e63-194">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="66e63-194">Click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="66e63-195">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="66e63-195">Create an Azure AD test user</span></span>
<span data-ttu-id="66e63-196">Dans le Portail Azure, créez un utilisateur de test appelé Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="66e63-196">In the Azure portal, create a test user called Britta Simon.</span></span>

![Nom et adresse e-mail de l’utilisateur de test Azure AD][100]

1. <span data-ttu-id="66e63-198">Dans le volet gauche du Portail Azure, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="66e63-198">In the Azure portal, in the left pane, click the **Azure Active Directory** icon.</span></span>

    ![Icône Azure Active Directory](./media/active-directory-saas-clarizen-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="66e63-200">Cliquez sur **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs** pour afficher la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="66e63-200">Click **Users and groups**, and then click **All users** to display the list of users.</span></span>

    ![Sélection des options « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-clarizen-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="66e63-202">En haut de la boîte de dialogue, cliquez sur **Ajouter** pour ouvrir la boîte de dialogue **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="66e63-202">At the top of the dialog box, click **Add** to open the **User** dialog box.</span></span>

    ![Bouton « Ajouter »](./media/active-directory-saas-clarizen-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="66e63-204">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="66e63-204">In the **User** dialog box, perform the following steps:</span></span>

    ![Boîte de dialogue « Utilisateur » renseignée avec le nom, l’adresse e-mail et le mot de passe](./media/active-directory-saas-clarizen-tutorial/create_aaduser_04.png)

    <span data-ttu-id="66e63-206">a.</span><span class="sxs-lookup"><span data-stu-id="66e63-206">a.</span></span> <span data-ttu-id="66e63-207">Dans la zone **Nom**, tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="66e63-207">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="66e63-208">b.</span><span class="sxs-lookup"><span data-stu-id="66e63-208">b.</span></span> <span data-ttu-id="66e63-209">Dans la zone **Nom d’utilisateur** , tapez l’adresse e-mail du compte de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="66e63-209">In the **User name** box, type the email address of the Britta Simon account.</span></span>

    <span data-ttu-id="66e63-210">c.</span><span class="sxs-lookup"><span data-stu-id="66e63-210">c.</span></span> <span data-ttu-id="66e63-211">Sélectionnez **Afficher le mot de passe** et notez la valeur de la zone **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="66e63-211">Select **Show Password** and write down the value of **Password**.</span></span>

    <span data-ttu-id="66e63-212">d.</span><span class="sxs-lookup"><span data-stu-id="66e63-212">d.</span></span> <span data-ttu-id="66e63-213">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="66e63-213">Click **Create**.</span></span>

### <a name="create-a-clarizen-test-user"></a><span data-ttu-id="66e63-214">Créer un utilisateur de test Clarizen</span><span class="sxs-lookup"><span data-stu-id="66e63-214">Create a Clarizen test user</span></span>
<span data-ttu-id="66e63-215">Pour permettre aux utilisateurs Azure AD de se connecter à Clarizen, vous devez approvisionner des comptes d’utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="66e63-215">To enable Azure AD users to sign in to Clarizen, you must provision user accounts.</span></span> <span data-ttu-id="66e63-216">Dans le cas de Clarizen, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="66e63-216">In the case of Clarizen, provisioning is a manual task.</span></span>

1. <span data-ttu-id="66e63-217">Connectez-vous à votre site d’entreprise Clarizen en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="66e63-217">Sign in to your Clarizen company site as an administrator.</span></span>

2. <span data-ttu-id="66e63-218">Cliquez sur **People**.</span><span class="sxs-lookup"><span data-stu-id="66e63-218">Click **People**.</span></span>

    <span data-ttu-id="66e63-219">![Sélection de l’option « People » (Contacts)](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "People") (Contacts)</span><span class="sxs-lookup"><span data-stu-id="66e63-219">![Clicking "People"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="66e63-220">Cliquez sur **Invite User**.</span><span class="sxs-lookup"><span data-stu-id="66e63-220">Click **Invite User**.</span></span>

    <span data-ttu-id="66e63-221">![Bouton « Invite User » (Inviter un utilisateur)](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "Invite Users") (Inviter un utilisateur)</span><span class="sxs-lookup"><span data-stu-id="66e63-221">!["Invite User" button](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="66e63-222">Dans la boîte de dialogue **Invite People** (Inviter un contact), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="66e63-222">In the **Invite People** dialog box, perform the following steps:</span></span>

    <span data-ttu-id="66e63-223">![Boîte de dialogue « Invite People » (Inviter un contact)](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "Invite People") (Inviter un contact)</span><span class="sxs-lookup"><span data-stu-id="66e63-223">!["Invite People" dialog box](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="66e63-224">a.</span><span class="sxs-lookup"><span data-stu-id="66e63-224">a.</span></span> <span data-ttu-id="66e63-225">Dans la zone **Email** (E-mail), tapez l’adresse e-mail du compte de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="66e63-225">In the **Email** box, type the email address of the Britta Simon account.</span></span>

    <span data-ttu-id="66e63-226">b.</span><span class="sxs-lookup"><span data-stu-id="66e63-226">b.</span></span> <span data-ttu-id="66e63-227">Cliquez sur **Inviter**.</span><span class="sxs-lookup"><span data-stu-id="66e63-227">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="66e63-228">Le titulaire du compte Azure Active Directory reçoit un message électronique contenant un lien à suivre pour confirmer son compte et l’activer.</span><span class="sxs-lookup"><span data-stu-id="66e63-228">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="66e63-229">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="66e63-229">Assign the Azure AD test user</span></span>
<span data-ttu-id="66e63-230">Autorisez Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Clarizen.</span><span class="sxs-lookup"><span data-stu-id="66e63-230">Enable Britta Simon to use Azure single sign-on by granting her access to Clarizen.</span></span>

![Utilisateur de test affecté][200]

1. <span data-ttu-id="66e63-232">Dans le Portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, cliquez sur **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="66e63-232">In the Azure portal, open the applications view, browse to the directory view, click **Enterprise applications**, and then click **All applications**.</span></span>

    ![Sélection des options « Applications d’entreprise » et « Toutes les applications »][201]

2. <span data-ttu-id="66e63-234">Dans la liste des applications, sélectionnez **Clarizen**.</span><span class="sxs-lookup"><span data-stu-id="66e63-234">In the applications list, select **Clarizen**.</span></span>

    ![Sélection de Clarizen dans la liste](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_50.png)

3. <span data-ttu-id="66e63-236">Dans le volet gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="66e63-236">In the left pane, click **Users and groups**.</span></span>

    ![Sélection de l’option « Utilisateurs et groupes »][202]

4. <span data-ttu-id="66e63-238">Cliquez sur le bouton **Add** .</span><span class="sxs-lookup"><span data-stu-id="66e63-238">Click the **Add** button.</span></span> <span data-ttu-id="66e63-239">Ensuite, dans la boîte de dialogue **Ajouter une attribution**, sélectionnez **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="66e63-239">Then, in the **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![Bouton « Ajouter » et boîte de dialogue « Ajouter une attribution »][203]

5. <span data-ttu-id="66e63-241">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="66e63-241">In the **Users and groups** dialog box, select **Britta Simon** in the list of users.</span></span>

6. <span data-ttu-id="66e63-242">Dans la boîte de dialogue **Utilisateurs et groupes**, cliquez sur le bouton **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="66e63-242">In the **Users and groups** dialog box, click the **Select** button.</span></span>

7. <span data-ttu-id="66e63-243">Dans la boîte de dialogue **Ajouter une attribution**, cliquez sur le bouton **Attribuer**.</span><span class="sxs-lookup"><span data-stu-id="66e63-243">In the **Add Assignment** dialog box, click the **Assign** button.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="66e63-244">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="66e63-244">Test single sign-on</span></span>
<span data-ttu-id="66e63-245">Testez la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="66e63-245">Test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="66e63-246">Lorsque vous cliquez sur la vignette Clarizen dans le volet d’accès, vous devez être automatiquement connecté à votre application Clarizen.</span><span class="sxs-lookup"><span data-stu-id="66e63-246">When you click the Clarizen tile in the Access Panel, you should be automatically signed in to your Clarizen application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="66e63-247">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="66e63-247">Additional resources</span></span>

* [<span data-ttu-id="66e63-248">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="66e63-248">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="66e63-249">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="66e63-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_203.png
