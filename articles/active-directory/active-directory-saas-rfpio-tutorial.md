---
title: "Didacticiel : Intégration d’Azure Active Directory à RFPIO | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et RFPIO."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 87187076-7b50-4247-814f-f217b052703f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 26a8bb17dad5a01b401ce7f9b484f09822825cbf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rfpio"></a><span data-ttu-id="ae0d3-103">Didacticiel : Intégration d’Azure Active Directory à RFPIO</span><span class="sxs-lookup"><span data-stu-id="ae0d3-103">Tutorial: Azure Active Directory integration with RFPIO</span></span>

<span data-ttu-id="ae0d3-104">Dans ce didacticiel, vous allez apprendre à intégrer RFPIO à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ae0d3-104">In this tutorial, you learn how to integrate RFPIO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ae0d3-105">L’intégration de RFPIO dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="ae0d3-105">Integrating RFPIO with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ae0d3-106">Dans Azure AD, vous pouvez contrôler qui a accès à RFPIO.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-106">You can control who in Azure AD who has access to RFPIO.</span></span>
- <span data-ttu-id="ae0d3-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à RFPIO (par authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-107">You can enable your users to automatically get signed-on to RFPIO (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="ae0d3-108">Vous pouvez gérer vos comptes à un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-108">You can manage your accounts in one central location--the Azure portal.</span></span>

<span data-ttu-id="ae0d3-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ae0d3-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae0d3-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ae0d3-110">Prerequisites</span></span>

<span data-ttu-id="ae0d3-111">Pour configurer l’intégration d’Azure AD avec RFPIO, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ae0d3-111">To configure Azure AD integration with RFPIO, you need the following items:</span></span>

- <span data-ttu-id="ae0d3-112">Un abonnement Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-112">An Azure AD subscription.</span></span>
- <span data-ttu-id="ae0d3-113">Un abonnement RFPIO pour lequel l’authentification unique est activée.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-113">A RFPIO single sign-on-enabled subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="ae0d3-114">Nous déconseillons l’utilisation d’un environnement de production pour tester les étapes de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-114">We don't recommend that you use a production environment to test the steps in this tutorial.</span></span>

<span data-ttu-id="ae0d3-115">Pour tester la procédure de ce didacticiel, suivez les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ae0d3-115">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="ae0d3-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-116">Do not use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="ae0d3-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ae0d3-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ae0d3-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="ae0d3-118">Scenario description</span></span>
<span data-ttu-id="ae0d3-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ae0d3-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="ae0d3-120">The scenario that's outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ae0d3-121">Ajout de RFPIO depuis la galerie.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-121">Adding RFPIO from the gallery.</span></span>
2. <span data-ttu-id="ae0d3-122">Configuration et test de l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-122">Configuring and testing Azure AD single sign-on.</span></span>

## <a name="add-rfpio-from-the-gallery"></a><span data-ttu-id="ae0d3-123">Ajout de RFPIO depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="ae0d3-123">Add RFPIO from the gallery</span></span>
<span data-ttu-id="ae0d3-124">Pour configurer l’intégration de RFPIO avec Azure AD, vous devez ajouter RFPIO à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-124">To configure the integration of RFPIO into Azure AD, you need to add RFPIO from the gallery to your list of managed SaaS apps.</span></span>

### <a name="to-add-rfpio-from-the-gallery"></a><span data-ttu-id="ae0d3-125">Pour ajouter RFPIO depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="ae0d3-125">To add RFPIO from the gallery</span></span>

1. <span data-ttu-id="ae0d3-126">Dans le panneau de navigation de gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation pane, select the **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ae0d3-128">Sélectionnez **Applications d’entreprise**, puis **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="ae0d3-130">Pour ajouter une nouvelle application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-130">To add a new application, select the **New application** button on the top of dialog box.</span></span>

    ![Applications][3]

4. <span data-ttu-id="ae0d3-132">Dans la zone de recherche, saisissez **RFPIO**.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-132">In the search box, type **RFPIO**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_search.png)

5. <span data-ttu-id="ae0d3-134">Dans le panneau de résultats, sélectionnez **RFPIO**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-134">In the results panel, select **RFPIO**, and then select the **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ae0d3-136">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae0d3-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="ae0d3-137">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec RFPIO, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="ae0d3-137">In this section, you configure and test Azure AD single sign-on with RFPIO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ae0d3-138">Pour que l’authentification unique fonctionne, Azure AD doit définir la relation entre l’utilisateur équivalent dans RFPIO et un utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-138">For single sign-on to work, Azure AD needs to know what the relationship is between counterpart user in RFPIO and a user in Azure AD.</span></span> <span data-ttu-id="ae0d3-139">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur RFPIO associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-139">In other words, a link relationship between an Azure AD user and the related user in RFPIO needs to be established.</span></span>

<span data-ttu-id="ae0d3-140">Dans RFPIO, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-140">In RFPIO, assign the value of **user name** in Azure AD as the value of  **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ae0d3-141">Pour configurer et tester l’authentification unique Azure AD avec RFPIO, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="ae0d3-141">To configure and test Azure AD single sign-on with RFPIO, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ae0d3-142">**[Configurer l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-142">**[Configure Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**--to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ae0d3-143">**[Créer un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-143">**[Create an Azure AD test user](#creating-an-azure-ad-test-user)**-- to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ae0d3-144">**[Créer un utilisateur de test RFPIO](#creating-a-rfpio-test-user)** pour avoir un équivalent de Britta Simon dans RFPIO lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-144">**[Create a RFPIO test user](#creating-a-rfpio-test-user)** --to have a counterpart of Britta Simon in RFPIO that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ae0d3-145">**[Affecter l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-145">**[Assign the Azure AD test user](#assigning-the-azure-ad-test-user)**--to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ae0d3-146">**[Tester l’authentification unique](#testing-single-sign-on)** pour vérifier que la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-146">**[Test Single Sign-On](#testing-single-sign-on)** --to verify if the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ae0d3-147">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae0d3-147">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ae0d3-148">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application RFPIO.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RFPIO application.</span></span>

<span data-ttu-id="ae0d3-149">**Pour configurer l’authentification unique Azure AD avec RFPIO, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ae0d3-149">**To configure Azure AD single sign-on with RFPIO, perform the following steps:**</span></span>

1. <span data-ttu-id="ae0d3-150">Dans le portail Azure, sur la page d’intégration de l’application **RFPIO**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-150">In the Azure portal, on the **RFPIO** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="ae0d3-152">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_samlbase.png)

3. <span data-ttu-id="ae0d3-154">Dans la section **Domaines et URL RFPIO**, si vous souhaitez configurer l’application en mode initié par **IDP**, suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ae0d3-154">On the **RFPIO Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url.png)

    <span data-ttu-id="ae0d3-156">a.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-156">a.</span></span> <span data-ttu-id="ae0d3-157">Dans la zone de texte **Identificateur**, saisissez l’URL : `https://www.rfpio.com`</span><span class="sxs-lookup"><span data-stu-id="ae0d3-157">In the **Identifier** textbox, type the URL: `https://www.rfpio.com`</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url1.png)

    <span data-ttu-id="ae0d3-159">b.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-159">b.</span></span> <span data-ttu-id="ae0d3-160">Cliquez sur **Afficher les paramètres d’URL avancés**.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-160">Check **Show advanced URL settings**.</span></span>

    <span data-ttu-id="ae0d3-161">c.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-161">c.</span></span> <span data-ttu-id="ae0d3-162">Dans la zone de texte **État de relais**, entrez une valeur de chaîne.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-162">In the **Relay State** textbox enter a string value.</span></span> <span data-ttu-id="ae0d3-163">Contactez l’[équipe de support technique de RFPIO](https://www.rfpio.com/contact/) pour obtenir cette valeur.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-163">Contact [RFPIO support team](https://www.rfpio.com/contact/) to get this value.</span></span> 

4. <span data-ttu-id="ae0d3-164">Cliquez sur **Afficher les paramètres d’URL avancés**.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-164">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="ae0d3-165">Si vous souhaitez configurer l’application en mode initié par le **fournisseur de service** :</span><span class="sxs-lookup"><span data-stu-id="ae0d3-165">If you wish to configure the application in **SP** initiated mode:</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url2.png)

    <span data-ttu-id="ae0d3-167">Dans la zone de texte **URL d’authentification**, saisissez l’URL : `https://www.app.rfpio.com`</span><span class="sxs-lookup"><span data-stu-id="ae0d3-167">In the **Sign on URL** textbox, type the URL: `https://www.app.rfpio.com`</span></span>

5. <span data-ttu-id="ae0d3-168">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_certificate.png) 

6. <span data-ttu-id="ae0d3-170">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="ae0d3-170">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="ae0d3-172">Dans une autre fenêtre de navigateur web, connectez-vous au site web **RFPIO** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-172">In a different web browser window, login to the **RFPIO** website as an administrator.</span></span>

8. <span data-ttu-id="ae0d3-173">Cliquez sur la liste déroulante située en bas à gauche.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-173">Click on the bottom left corner dropdown.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/app1.png)

9. <span data-ttu-id="ae0d3-175">Cliquez sur **Paramètres de l’organisation**.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-175">Click on the **Organization Settings**.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/app2.png)

10. <span data-ttu-id="ae0d3-177">Cliquez sur **FONCTIONNALITÉS ET INTÉGRATION**.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-177">Click on the **FEATURES & INTEGRATION**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/app4.png)

11. <span data-ttu-id="ae0d3-179">Dans **Configuration SAML SSO**, cliquez sur **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-179">In the **SAML SSO Configuration** Click **Edit**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/app3.png)

12. <span data-ttu-id="ae0d3-181">Dans cette section, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ae0d3-181">In this Section perform following actions:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/app5.png)
    
    <span data-ttu-id="ae0d3-183">a.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-183">a.</span></span> <span data-ttu-id="ae0d3-184">Copiez le contenu du **fichier XML de métadonnées téléchargé** et collez-le dans le champ **Configuration de l’identité**.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-184">Copy the content of the **Downloaded Metadata XML** and paste it into the **identity configuration** field.</span></span>

    > [!NOTE]
    ><span data-ttu-id="ae0d3-185">Pour copier le contenu du fichier **XML de métadonnées** téléchargé, utilisez **Notepad++** ou **XML Editor**.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-185">To copy the content of downloaded **Metadata XML** Use **Notepad++** or proper **XML Editor**.</span></span> 

    <span data-ttu-id="ae0d3-186">b.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-186">b.</span></span> <span data-ttu-id="ae0d3-187">Cliquez sur **Valider**.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-187">Click **Validate**.</span></span>

    <span data-ttu-id="ae0d3-188">c.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-188">c.</span></span> <span data-ttu-id="ae0d3-189">Après avoir cliqué sur **Valider**, activez **SAML(Enabled)**.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-189">After Clicking **Validate**, Flip **SAML(Enabled)** to on.</span></span>

    <span data-ttu-id="ae0d3-190">d.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-190">d.</span></span> <span data-ttu-id="ae0d3-191">Cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-191">Click **Submit**.</span></span>

> [!TIP]
> <span data-ttu-id="ae0d3-192">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ae0d3-193">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ae0d3-194">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ae0d3-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ae0d3-195">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae0d3-195">Create an Azure AD test user</span></span>
<span data-ttu-id="ae0d3-196">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="ae0d3-198">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ae0d3-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ae0d3-199">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ae0d3-201">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ae0d3-203">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-203">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ae0d3-205">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ae0d3-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ae0d3-207">a.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-207">a.</span></span> <span data-ttu-id="ae0d3-208">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ae0d3-209">b.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-209">b.</span></span> <span data-ttu-id="ae0d3-210">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ae0d3-211">c.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-211">c.</span></span> <span data-ttu-id="ae0d3-212">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ae0d3-213">d.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-213">d.</span></span> <span data-ttu-id="ae0d3-214">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-214">Click **Create**.</span></span>
 
### <a name="create-a-rfpio-test-user"></a><span data-ttu-id="ae0d3-215">Créer un utilisateur de test RFPIO</span><span class="sxs-lookup"><span data-stu-id="ae0d3-215">Create a RFPIO test user</span></span>

<span data-ttu-id="ae0d3-216">Pour se connecter à RFPIO, les utilisateurs d’Azure AD doivent être configurés dans RFPIO.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-216">To enable Azure AD users to log in to RFPIO, they must be provisioned into RFPIO.</span></span>  
<span data-ttu-id="ae0d3-217">Dans le cas de RFPIO, l’approvisionnement se fait manuellement.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-217">In the case of RFPIO, provisioning is a manual task.</span></span>

<span data-ttu-id="ae0d3-218">**Pour approvisionner un compte d’utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ae0d3-218">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="ae0d3-219">Connectez-vous à votre site d’entreprise RFPIO en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-219">Log in to your RFPIO company site as an administrator.</span></span>

2. <span data-ttu-id="ae0d3-220">Cliquez sur la liste déroulante située en bas à gauche.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-220">Click on the bottom left corner dropdown.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/app1.png)

3. <span data-ttu-id="ae0d3-222">Cliquez sur **Paramètres de l’organisation**.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-222">Click on the **Organization Settings**.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/app2.png)

4. <span data-ttu-id="ae0d3-224">Cliquez sur **MEMBRES DE L’ÉQUIPE**.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-224">Click **TEAM MEMBERS**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/app6.png)

5. <span data-ttu-id="ae0d3-226">Cliquez sur **AJOUTER DES MEMBRES**.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-226">Click on **ADD MEMBERS**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/app7.png)

6. <span data-ttu-id="ae0d3-228">Dans la section **Ajouter de nouveaux membres**.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-228">In the **Add New Members** section.</span></span> <span data-ttu-id="ae0d3-229">Procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ae0d3-229">Perform following actions:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/app8.png)

    <span data-ttu-id="ae0d3-231">a.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-231">a.</span></span> <span data-ttu-id="ae0d3-232">Entrez l’**adresse e-mail** dans le champ **Entrer une adresse e-mail par ligne**.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-232">Enter **Email address** in the **Enter one email per line** field.</span></span>

    <span data-ttu-id="ae0d3-233">b.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-233">b.</span></span> <span data-ttu-id="ae0d3-234">Sélectionnez le **Rôle** selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-234">Plese select **Role** according your requirements.</span></span>

    <span data-ttu-id="ae0d3-235">c.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-235">c.</span></span> <span data-ttu-id="ae0d3-236">Cliquez sur **AJOUTER DES MEMBRES**.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-236">Click **ADD MEMBERS**.</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="ae0d3-237">Le titulaire du compte Azure Active Directory reçoit un e-mail contenant un lien à suivre pour confirmer son compte et l’activer.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-237">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="ae0d3-238">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae0d3-238">Assign the Azure AD test user</span></span>

<span data-ttu-id="ae0d3-239">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à RFPIO.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-239">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RFPIO.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="ae0d3-241">**Pour affecter Britta Simon à RFPIO, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ae0d3-241">**To assign Britta Simon to RFPIO, perform the following steps:**</span></span>

1. <span data-ttu-id="ae0d3-242">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="ae0d3-244">Dans la liste des applications, sélectionnez **RFPIO**.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-244">In the applications list, select **RFPIO**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_app.png) 

3. <span data-ttu-id="ae0d3-246">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-246">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="ae0d3-248">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-248">Click **Add** button.</span></span> <span data-ttu-id="ae0d3-249">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="ae0d3-251">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ae0d3-252">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ae0d3-253">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ae0d3-254">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="ae0d3-254">Test single sign-on</span></span>

<span data-ttu-id="ae0d3-255">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-255">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="ae0d3-256">Lorsque vous cliquez sur la vignette RFPIO dans le panneau d’accès, vous devez être connecté automatiquement à votre application RFPIO.</span><span class="sxs-lookup"><span data-stu-id="ae0d3-256">When you click the RFPIO tile in the Access Panel, you should get automatically signed-on to your RFPIO application.</span></span>
<span data-ttu-id="ae0d3-257">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ae0d3-257">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ae0d3-258">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="ae0d3-258">Additional resources</span></span>

* [<span data-ttu-id="ae0d3-259">Liste de didacticiels sur les procédures d’intégration des applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ae0d3-259">List of tutorials about how to integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ae0d3-260">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="ae0d3-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_203.png

