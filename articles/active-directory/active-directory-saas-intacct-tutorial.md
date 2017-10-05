---
title: "Didacticiel : Intégration d’Azure Active Directory avec Intacct | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Intacct."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 92518e02-a62c-4b1b-a8e9-2803eb2b49ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: c203b192b9da0d280cbd7f6c123219242ee4a3d1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intacct"></a><span data-ttu-id="0b918-103">Didacticiel : Intégration d’Azure Active Directory à Intacct</span><span class="sxs-lookup"><span data-stu-id="0b918-103">Tutorial: Azure Active Directory integration with Intacct</span></span>

<span data-ttu-id="0b918-104">Dans ce didacticiel, vous allez apprendre à intégrer Intacct à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0b918-104">In this tutorial, you learn how to integrate Intacct with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0b918-105">L’intégration d’Intacct à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="0b918-105">Integrating Intacct with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0b918-106">Dans Azure AD, vous pouvez contrôler qui a accès à Intacct</span><span class="sxs-lookup"><span data-stu-id="0b918-106">You can control in Azure AD who has access to Intacct</span></span>
- <span data-ttu-id="0b918-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Intacct (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b918-107">You can enable your users to automatically get signed-on to Intacct (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0b918-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="0b918-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0b918-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0b918-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b918-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0b918-110">Prerequisites</span></span>

<span data-ttu-id="0b918-111">Pour configurer l’intégration d’Azure AD à Intacct, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="0b918-111">To configure Azure AD integration with Intacct, you need the following items:</span></span>

- <span data-ttu-id="0b918-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b918-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0b918-113">Un abonnement Intacct pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="0b918-113">An Intacct single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0b918-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="0b918-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0b918-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="0b918-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0b918-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="0b918-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0b918-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0b918-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0b918-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="0b918-118">Scenario description</span></span>
<span data-ttu-id="0b918-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="0b918-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0b918-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="0b918-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0b918-121">Ajout d’Intacct à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="0b918-121">Adding Intacct from the gallery</span></span>
2. <span data-ttu-id="0b918-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b918-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intacct-from-the-gallery"></a><span data-ttu-id="0b918-123">Ajout d’Intacct à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="0b918-123">Adding Intacct from the gallery</span></span>
<span data-ttu-id="0b918-124">Pour configurer l’intégration d’Intacct avec Azure AD, vous devez ajouter Intacct à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="0b918-124">To configure the integration of Intacct into Azure AD, you need to add Intacct from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0b918-125">**Pour ajouter Intacct à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0b918-125">**To add Intacct from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0b918-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0b918-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0b918-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="0b918-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0b918-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="0b918-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="0b918-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="0b918-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="0b918-133">Dans la zone de recherche, entrez **Intacct**.</span><span class="sxs-lookup"><span data-stu-id="0b918-133">In the search box, type **Intacct**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_search.png)

5. <span data-ttu-id="0b918-135">Dans le volet de résultats, sélectionnez **Intacct**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="0b918-135">In the results panel, select **Intacct**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0b918-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b918-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0b918-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Intacct avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="0b918-138">In this section, you configure and test Azure AD single sign-on with Intacct based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0b918-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Intacct équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0b918-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Intacct is to a user in Azure AD.</span></span> <span data-ttu-id="0b918-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Intacct associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="0b918-140">In other words, a link relationship between an Azure AD user and the related user in Intacct needs to be established.</span></span>

<span data-ttu-id="0b918-141">Dans Intacct, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur **Nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="0b918-141">In Intacct, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0b918-142">Pour configurer et tester l’authentification unique Azure AD avec Intacct, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="0b918-142">To configure and test Azure AD single sign-on with Intacct, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0b918-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="0b918-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0b918-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0b918-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0b918-145">**[Création d’un utilisateur de test Intacct](#creating-an-intacct-test-user)** : pour avoir un équivalent de l’utilisateur Britta Simon dans Intacct, qui soit lié à la représentation de l’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0b918-145">**[Creating an Intacct test user](#creating-an-intacct-test-user)** - to have a counterpart of Britta Simon in Intacct that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0b918-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0b918-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0b918-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="0b918-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0b918-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b918-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0b918-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Intacct.</span><span class="sxs-lookup"><span data-stu-id="0b918-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Intacct application.</span></span>

<span data-ttu-id="0b918-150">**Pour configurer l’authentification unique Azure AD avec Intacct, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0b918-150">**To configure Azure AD single sign-on with Intacct, perform the following steps:**</span></span>

1. <span data-ttu-id="0b918-151">Dans le portail Azure, sur la page d’intégration de l’application **Intacct**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="0b918-151">In the Azure portal, on the **Intacct** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="0b918-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="0b918-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_samlbase.png)

3. <span data-ttu-id="0b918-155">Dans la section **Domaine et URL Intacct**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0b918-155">On the **Intacct Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_url.png)

    <span data-ttu-id="0b918-157">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="0b918-157">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.intacct.com/ia/acct/sso_response.phtml`|
    | `https://www.intacct.com/ia/acct/sso_response.phtml` |

    > [!NOTE] 
    > <span data-ttu-id="0b918-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="0b918-158">This value is not real.</span></span> <span data-ttu-id="0b918-159">Mettez à jour la valeur avec l’URL de réponse réelle.</span><span class="sxs-lookup"><span data-stu-id="0b918-159">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="0b918-160">Pour obtenir ces valeurs, contactez [l’équipe de support technique Intacct](https://us.intacct.com/support).</span><span class="sxs-lookup"><span data-stu-id="0b918-160">Contact [Intacct support team](https://us.intacct.com/support) to get this value.</span></span>

4. <span data-ttu-id="0b918-161">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="0b918-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_certificate.png) 

5. <span data-ttu-id="0b918-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="0b918-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-intacct-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0b918-165">Dans la section **Configuration de Intacct**, cliquez sur **Configurer Intacct** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="0b918-165">On the **Intacct Configuration** section, click **Configure Intacct** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0b918-166">Copiez l’**ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="0b918-166">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_configure.png) 

7. <span data-ttu-id="0b918-168">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Intacct en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="0b918-168">In a different web browser window, sign in to your Intacct company site as an administrator.</span></span>

8. <span data-ttu-id="0b918-169">Cliquez sur l’onglet **Company**, puis sur **Company Info**.</span><span class="sxs-lookup"><span data-stu-id="0b918-169">Click the **Company** tab, and then click **Company Info**.</span></span>

    <span data-ttu-id="0b918-170">![Company](./media/active-directory-saas-intacct-tutorial/ic790037.png "Company")</span><span class="sxs-lookup"><span data-stu-id="0b918-170">![Company](./media/active-directory-saas-intacct-tutorial/ic790037.png "Company")</span></span>

9. <span data-ttu-id="0b918-171">Cliquez sur l’onglet **Security**, puis sur **Edit**.</span><span class="sxs-lookup"><span data-stu-id="0b918-171">Click the **Security** tab, and then click **Edit**.</span></span>

    <span data-ttu-id="0b918-172">![Sécurité](./media/active-directory-saas-intacct-tutorial/ic790038.png "Sécurité")</span><span class="sxs-lookup"><span data-stu-id="0b918-172">![Security](./media/active-directory-saas-intacct-tutorial/ic790038.png "Security")</span></span>

10. <span data-ttu-id="0b918-173">Dans la section **Single sign on (SSO)** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0b918-173">In the **Single sign on (SSO)** section, perform the following steps:</span></span>

    <span data-ttu-id="0b918-174">![Single sign On](./media/active-directory-saas-intacct-tutorial/ic790039.png "Single sign On")</span><span class="sxs-lookup"><span data-stu-id="0b918-174">![Single sign on](./media/active-directory-saas-intacct-tutorial/ic790039.png "single sign on")</span></span>

    <span data-ttu-id="0b918-175">a.</span><span class="sxs-lookup"><span data-stu-id="0b918-175">a.</span></span> <span data-ttu-id="0b918-176">Sélectionnez **Enable Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="0b918-176">Select **Enable single sign on**.</span></span>

    <span data-ttu-id="0b918-177">b.</span><span class="sxs-lookup"><span data-stu-id="0b918-177">b.</span></span> <span data-ttu-id="0b918-178">Pour **Identity provider type**, sélectionnez **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="0b918-178">As **Identity provider type**, select **SAML 2.0**.</span></span>

    <span data-ttu-id="0b918-179">c.</span><span class="sxs-lookup"><span data-stu-id="0b918-179">c.</span></span> <span data-ttu-id="0b918-180">Dans la zone de texte **URL émettrice**, collez la valeur **ID d’entité SAML** que vous avez copiée dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0b918-180">In **Issuer URL** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="0b918-181">d.</span><span class="sxs-lookup"><span data-stu-id="0b918-181">d.</span></span> <span data-ttu-id="0b918-182">Dans la zone de texte **URL de connexion**, collez la valeur **URL du service d’authentification unique SAML** que vous avez copiée dans portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0b918-182">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0b918-183">e.</span><span class="sxs-lookup"><span data-stu-id="0b918-183">e.</span></span> <span data-ttu-id="0b918-184">Ouvrez votre certificat codé en**base-64** dans le bloc-notes, copiez son contenu dans le presse-papiers, puis collez-le dans la zone **Certificat**.</span><span class="sxs-lookup"><span data-stu-id="0b918-184">Open your **base-64** encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Certificate** box.</span></span>
   
    <span data-ttu-id="0b918-185">f.</span><span class="sxs-lookup"><span data-stu-id="0b918-185">f.</span></span> <span data-ttu-id="0b918-186">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="0b918-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="0b918-187">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="0b918-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0b918-188">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="0b918-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0b918-189">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0b918-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0b918-190">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b918-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="0b918-191">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0b918-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="0b918-193">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0b918-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0b918-194">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0b918-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0b918-196">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="0b918-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0b918-198">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="0b918-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0b918-200">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0b918-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0b918-202">a.</span><span class="sxs-lookup"><span data-stu-id="0b918-202">a.</span></span> <span data-ttu-id="0b918-203">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0b918-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0b918-204">b.</span><span class="sxs-lookup"><span data-stu-id="0b918-204">b.</span></span> <span data-ttu-id="0b918-205">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0b918-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0b918-206">c.</span><span class="sxs-lookup"><span data-stu-id="0b918-206">c.</span></span> <span data-ttu-id="0b918-207">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="0b918-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0b918-208">d.</span><span class="sxs-lookup"><span data-stu-id="0b918-208">d.</span></span> <span data-ttu-id="0b918-209">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="0b918-209">Click **Create**.</span></span>
 
### <a name="creating-an-intacct-test-user"></a><span data-ttu-id="0b918-210">Création d’un utilisateur de test Intacct</span><span class="sxs-lookup"><span data-stu-id="0b918-210">Creating an Intacct test user</span></span>

<span data-ttu-id="0b918-211">Pour configurer les utilisateurs Azure AD afin qu’ils puissent se connecter à Intacct, ils doivent être approvisionnés dans Intacct.</span><span class="sxs-lookup"><span data-stu-id="0b918-211">To set up Azure AD users so they can sign in to Intacct, they must be provisioned into Intacct.</span></span> <span data-ttu-id="0b918-212">Pour Intacct, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="0b918-212">For Intacct, provisioning is a manual task.</span></span>

<span data-ttu-id="0b918-213">**Pour approvisionner un compte d’utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0b918-213">**To provision user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="0b918-214">Connectez-vous à votre locataire **Intacct**.</span><span class="sxs-lookup"><span data-stu-id="0b918-214">Sign in to your **Intacct** tenant.</span></span>

2. <span data-ttu-id="0b918-215">Cliquez sur l’onglet **Company**, puis sur **Users**.</span><span class="sxs-lookup"><span data-stu-id="0b918-215">Click the **Company** tab, and then click **Users**.</span></span>

    <span data-ttu-id="0b918-216">![Utilisateurs](./media/active-directory-saas-intacct-tutorial/ic790041.png "Utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="0b918-216">![Users](./media/active-directory-saas-intacct-tutorial/ic790041.png "Users")</span></span>
3. <span data-ttu-id="0b918-217">Cliquez sur l’onglet **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="0b918-217">Click the **Add** tab.</span></span>

    <span data-ttu-id="0b918-218">![Add](./media/active-directory-saas-intacct-tutorial/ic790042.png "Add")</span><span class="sxs-lookup"><span data-stu-id="0b918-218">![Add](./media/active-directory-saas-intacct-tutorial/ic790042.png "Add")</span></span>
4. <span data-ttu-id="0b918-219">Dans la section **User Information** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0b918-219">In the **User Information** section, perform the following steps:</span></span>

    <span data-ttu-id="0b918-220">![User Information](./media/active-directory-saas-intacct-tutorial/ic790043.png "User Information")</span><span class="sxs-lookup"><span data-stu-id="0b918-220">![User Information](./media/active-directory-saas-intacct-tutorial/ic790043.png "User Information")</span></span>

    <span data-ttu-id="0b918-221">a.</span><span class="sxs-lookup"><span data-stu-id="0b918-221">a.</span></span> <span data-ttu-id="0b918-222">Tapez **l’ID utilisateur**, le **nom**, le **prénom**, **l’adresse de messagerie**, le **titre** et le **numéro de téléphone** d’un compte Azure AD que vous souhaitez approvisionner dans la section **Informations utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="0b918-222">Enter the **User ID**, the **Last name**, **First name**, the **Email address**, the **Title**, and the **Phone** of an Azure AD account that you want to provision into the **User Information** section.</span></span>

    <span data-ttu-id="0b918-223">b.</span><span class="sxs-lookup"><span data-stu-id="0b918-223">b.</span></span> <span data-ttu-id="0b918-224">Sélectionnez les **privilèges d’administrateur** d’un compte Azure AD que vous voulez approvisionner.</span><span class="sxs-lookup"><span data-stu-id="0b918-224">Select the **Admin privileges** of an Azure AD account that you want to provision.</span></span>
   
    <span data-ttu-id="0b918-225">c.</span><span class="sxs-lookup"><span data-stu-id="0b918-225">c.</span></span> <span data-ttu-id="0b918-226">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="0b918-226">Click **Save**.</span></span> <span data-ttu-id="0b918-227">Le détenteur du compte Azure AD reçoit un message électronique et suit un lien pour confirmer le compte avant qu’il ne soit activé.</span><span class="sxs-lookup"><span data-stu-id="0b918-227">The Azure AD account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

>[!NOTE]
><span data-ttu-id="0b918-228">Pour approvisionner des comptes utilisateur Azure AD, vous pouvez utiliser d’autres outils de création de compte utilisateur Intacct ou des API fournies par Intacct.</span><span class="sxs-lookup"><span data-stu-id="0b918-228">To provision Azure AD user accounts, you can use other Intacct user account creation tools or APIs that are provided by Intacct.</span></span>
        
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0b918-229">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b918-229">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0b918-230">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Intacct.</span><span class="sxs-lookup"><span data-stu-id="0b918-230">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Intacct.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="0b918-232">**Pour affecter Britta Simon à Intacct, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0b918-232">**To assign Britta Simon to Intacct, perform the following steps:**</span></span>

1. <span data-ttu-id="0b918-233">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="0b918-233">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="0b918-235">Dans la liste des applications, sélectionnez **Intacct**.</span><span class="sxs-lookup"><span data-stu-id="0b918-235">In the applications list, select **Intacct**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_app.png) 

3. <span data-ttu-id="0b918-237">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="0b918-237">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="0b918-239">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="0b918-239">Click **Add** button.</span></span> <span data-ttu-id="0b918-240">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="0b918-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="0b918-242">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="0b918-242">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0b918-243">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="0b918-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0b918-244">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="0b918-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0b918-245">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="0b918-245">Testing single sign-on</span></span>

<span data-ttu-id="0b918-246">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="0b918-246">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="0b918-247">Lorsque vous cliquez sur la vignette Intacct dans le volet d’accès, vous devez être connecté automatiquement à votre application Intacct.</span><span class="sxs-lookup"><span data-stu-id="0b918-247">When you click the Intacct tile in the Access Panel, you should be automatically signed in to your Intacct application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0b918-248">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="0b918-248">Additional resources</span></span>

* [<span data-ttu-id="0b918-249">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0b918-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0b918-250">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="0b918-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_203.png

