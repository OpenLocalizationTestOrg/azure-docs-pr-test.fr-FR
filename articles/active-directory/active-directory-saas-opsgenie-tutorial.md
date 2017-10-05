---
title: "Didacticiel : Intégration d’Azure Active Directory à OpsGenie | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et OpsGenie."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 41b59b22-a61d-4fe6-ab0d-6c3991d1375f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: ce63726d2406d2f1415d29786f0ef92ca95b9b90
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-opsgenie"></a><span data-ttu-id="40d02-103">Didacticiel : Intégration d’Azure Active Directory à OpsGenie</span><span class="sxs-lookup"><span data-stu-id="40d02-103">Tutorial: Azure Active Directory integration with OpsGenie</span></span>

<span data-ttu-id="40d02-104">Dans ce didacticiel, vous allez apprendre à intégrer OpsGenie à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="40d02-104">In this tutorial, you learn how to integrate OpsGenie with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="40d02-105">L’intégration d’OpsGenie dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="40d02-105">Integrating OpsGenie with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="40d02-106">Dans Azure AD, vous pouvez contrôler qui a accès à OpsGenie.</span><span class="sxs-lookup"><span data-stu-id="40d02-106">You can control in Azure AD who has access to OpsGenie</span></span>
- <span data-ttu-id="40d02-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à OpsGenie (par le biais de l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="40d02-107">You can enable your users to automatically get signed-on to OpsGenie (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="40d02-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="40d02-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="40d02-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="40d02-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40d02-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="40d02-110">Prerequisites</span></span>

<span data-ttu-id="40d02-111">Pour configurer l’intégration d’Azure AD à OpsGenie, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="40d02-111">To configure Azure AD integration with OpsGenie, you need the following items:</span></span>

- <span data-ttu-id="40d02-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="40d02-112">An Azure AD subscription</span></span>
- <span data-ttu-id="40d02-113">Un abonnement OpsGenie pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="40d02-113">A OpsGenie single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="40d02-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="40d02-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="40d02-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="40d02-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="40d02-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="40d02-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="40d02-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="40d02-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="40d02-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="40d02-118">Scenario description</span></span>
<span data-ttu-id="40d02-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="40d02-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="40d02-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="40d02-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="40d02-121">Ajout de OpsGenie à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="40d02-121">Adding OpsGenie from the gallery</span></span>
2. <span data-ttu-id="40d02-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="40d02-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-opsgenie-from-the-gallery"></a><span data-ttu-id="40d02-123">Ajout de OpsGenie à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="40d02-123">Adding OpsGenie from the gallery</span></span>
<span data-ttu-id="40d02-124">Pour configurer l’intégration de OpsGenie à Azure AD, vous devez ajouter OpsGenie à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="40d02-124">To configure the integration of OpsGenie into Azure AD, you need to add OpsGenie from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="40d02-125">**Pour ajouter OpsGenie à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="40d02-125">**To add OpsGenie from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="40d02-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="40d02-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="40d02-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="40d02-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="40d02-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="40d02-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="40d02-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="40d02-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="40d02-133">Dans la zone de recherche, entrez **OpsGenie**.</span><span class="sxs-lookup"><span data-stu-id="40d02-133">In the search box, type **OpsGenie**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_search.png)

5. <span data-ttu-id="40d02-135">Dans le panneau des résultats, sélectionnez **OpsGenie**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="40d02-135">In the results panel, select **OpsGenie**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="40d02-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="40d02-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="40d02-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec OpsGenie, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="40d02-138">In this section, you configure and test Azure AD single sign-on with OpsGenie based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="40d02-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur OpsGenie correspondant dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="40d02-139">For single sign-on to work, Azure AD needs to know what the counterpart user in OpsGenie is to a user in Azure AD.</span></span> <span data-ttu-id="40d02-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur OpsGenie associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="40d02-140">In other words, a link relationship between an Azure AD user and the related user in OpsGenie needs to be established.</span></span>

<span data-ttu-id="40d02-141">Dans OpsGenie, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="40d02-141">In OpsGenie, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="40d02-142">Pour configurer et tester l’authentification unique Azure AD avec OpsGenie, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="40d02-142">To configure and test Azure AD single sign-on with OpsGenie, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="40d02-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="40d02-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="40d02-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="40d02-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="40d02-145">**[Création d’un utilisateur de test OpsGenie](#creating-a-opsgenie-test-user)** pour obtenir un équivalent de Britta Simon dans OpsGenie lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="40d02-145">**[Creating a OpsGenie test user](#creating-a-opsgenie-test-user)** - to have a counterpart of Britta Simon in OpsGenie that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="40d02-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="40d02-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="40d02-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="40d02-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="40d02-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="40d02-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="40d02-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application OpsGenie.</span><span class="sxs-lookup"><span data-stu-id="40d02-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your OpsGenie application.</span></span>

<span data-ttu-id="40d02-150">**Pour configurer l’authentification unique Azure AD avec OpsGenie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="40d02-150">**To configure Azure AD single sign-on with OpsGenie, perform the following steps:**</span></span>

1. <span data-ttu-id="40d02-151">Dans le portail Azure, sur la page d’intégration de l’application **OpsGenie**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="40d02-151">In the Azure portal, on the **OpsGenie** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="40d02-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="40d02-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_samlbase.png)

3. <span data-ttu-id="40d02-155">Dans la section **Domaine et URL OpsGenie**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="40d02-155">On the **OpsGenie Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_url.png)

    <span data-ttu-id="40d02-157">Dans la zone de texte **URL de connexion**, entrez l’URL : `https://app.opsgenie.com/auth/login`</span><span class="sxs-lookup"><span data-stu-id="40d02-157">In the **Sign-on URL** textbox, type the URL: `https://app.opsgenie.com/auth/login`</span></span>

4. <span data-ttu-id="40d02-158">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="40d02-158">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_certificate.png) 

5. <span data-ttu-id="40d02-160">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="40d02-160">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-opsgenie-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="40d02-162">Dans la section **Configuration d’OpsGenie**, cliquez sur **Configurer OpsGenie** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="40d02-162">On the **OpsGenie Configuration** section, click **Configure OpsGenie** to open **Configure sign-on** window.</span></span> <span data-ttu-id="40d02-163">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="40d02-163">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_configure.png) 

7. <span data-ttu-id="40d02-165">Ouvrez une autre instance de navigateur, puis connectez-vous à OpsGenie en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="40d02-165">Open another browser instance, and then log-in to OpsGenie as an administrator.</span></span>

8. <span data-ttu-id="40d02-166">Cliquez sur **Paramètres**, puis cliquez sur l’onglet **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="40d02-166">Click **Settings**, and then click the **Single Sign On** tab.</span></span>
   
    ![Authentification unique OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_06.png)

9. <span data-ttu-id="40d02-168">Pour activer l’authentification unique, sélectionnez **Activé**.</span><span class="sxs-lookup"><span data-stu-id="40d02-168">To enable SSO, select **Enabled**.</span></span>
   
    ![Paramètres OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_07.png) 

10. <span data-ttu-id="40d02-170">Dans la section **Fournisseur** cliquez sur l’onglet **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="40d02-170">In the **Provider** section, click the **Azure Active Directory** tab.</span></span>
   
    ![Paramètres OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_08.png) 

11. <span data-ttu-id="40d02-172">Sur la page de boîte de dialogue Azure Active Directory, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="40d02-172">On the Azure Active Directory dialog page, perform the following steps:</span></span>
   
    ![Paramètres OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_09.png)
    
    <span data-ttu-id="40d02-174">a.</span><span class="sxs-lookup"><span data-stu-id="40d02-174">a.</span></span> <span data-ttu-id="40d02-175">Collez l’**URL du service d’authentification unique** que vous avez copiée sur le portail Azure dans la zone de texte **Point de terminaison SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="40d02-175">Paste **Single Sign On Service URL**, which you have copied from the Azure portal into the **SAML 2.0 Endpoint** textbox.</span></span>
    
    <span data-ttu-id="40d02-176">b.</span><span class="sxs-lookup"><span data-stu-id="40d02-176">b.</span></span> <span data-ttu-id="40d02-177">Dans le bloc-notes, ouvrez votre certificat codé en base 64 téléchargé, copiez son contenu dans le Presse-papiers et collez-le dans la zone de texte **Certificat X 500**.</span><span class="sxs-lookup"><span data-stu-id="40d02-177">Open your downloaded base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it into the **X.500 Certificate** textbox.</span></span>
    
    <span data-ttu-id="40d02-178">c.</span><span class="sxs-lookup"><span data-stu-id="40d02-178">c.</span></span> <span data-ttu-id="40d02-179">Cliquez sur **Enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="40d02-179">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="40d02-180">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="40d02-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="40d02-181">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="40d02-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="40d02-182">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="40d02-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="40d02-183">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="40d02-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="40d02-184">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="40d02-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="40d02-186">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="40d02-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="40d02-187">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="40d02-187">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="40d02-189">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="40d02-189">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="40d02-191">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="40d02-191">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="40d02-193">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="40d02-193">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="40d02-195">a.</span><span class="sxs-lookup"><span data-stu-id="40d02-195">a.</span></span> <span data-ttu-id="40d02-196">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="40d02-196">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="40d02-197">b.</span><span class="sxs-lookup"><span data-stu-id="40d02-197">b.</span></span> <span data-ttu-id="40d02-198">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="40d02-198">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="40d02-199">c.</span><span class="sxs-lookup"><span data-stu-id="40d02-199">c.</span></span> <span data-ttu-id="40d02-200">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="40d02-200">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="40d02-201">d.</span><span class="sxs-lookup"><span data-stu-id="40d02-201">d.</span></span> <span data-ttu-id="40d02-202">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="40d02-202">Click **Create**.</span></span>
 
### <a name="creating-a-opsgenie-test-user"></a><span data-ttu-id="40d02-203">Création d’un utilisateur de test OpsGenie</span><span class="sxs-lookup"><span data-stu-id="40d02-203">Creating a OpsGenie test user</span></span>

<span data-ttu-id="40d02-204">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans OpsGenie.</span><span class="sxs-lookup"><span data-stu-id="40d02-204">The objective of this section is to create a user called Britta Simon in OpsGenie.</span></span> 

1. <span data-ttu-id="40d02-205">Dans une fenêtre de navigateur web, connectez-vous à votre client OpsGenie en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="40d02-205">In a web browser window, log into your OpsGenie tenant as an administrator.</span></span>

2. <span data-ttu-id="40d02-206">Accédez à la liste Utilisateurs en cliquant sur **Utilisateur** dans le volet gauche.</span><span class="sxs-lookup"><span data-stu-id="40d02-206">Navigate to Users list by clicking **User** in left panel.</span></span>
   
   ![Paramètres OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_10.png) 

3. <span data-ttu-id="40d02-208">Cliquez sur **Add User**.</span><span class="sxs-lookup"><span data-stu-id="40d02-208">Click **Add User**.</span></span>

4. <span data-ttu-id="40d02-209">Dans la boîte de dialogue **Ajouter un utilisateur** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="40d02-209">On the **Add User** dialog, perform the following steps:</span></span>
   
   ![Paramètres OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_11.png)
   
   <span data-ttu-id="40d02-211">a.</span><span class="sxs-lookup"><span data-stu-id="40d02-211">a.</span></span> <span data-ttu-id="40d02-212">Dans la zone de texte **E-mail**, saisissez l’adresse e-mail de BrittaSimon utilisée dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="40d02-212">In the **Email** textbox, type the email address of BrittaSimon addressed in Azure Active Directory.</span></span>
   
   <span data-ttu-id="40d02-213">b.</span><span class="sxs-lookup"><span data-stu-id="40d02-213">b.</span></span> <span data-ttu-id="40d02-214">Dans la zone de texte **Nom complet**, tapez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="40d02-214">In the **Full Name** textbox, type **Britta Simon**.</span></span>
   
   <span data-ttu-id="40d02-215">c.</span><span class="sxs-lookup"><span data-stu-id="40d02-215">c.</span></span> <span data-ttu-id="40d02-216">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="40d02-216">Click **Save**.</span></span> 

>[!NOTE]
><span data-ttu-id="40d02-217">Britta reçoit un e-mail contenant des instructions pour configurer son profil.</span><span class="sxs-lookup"><span data-stu-id="40d02-217">Britta gets an email with instructions for setting up her profile.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="40d02-218">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="40d02-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="40d02-219">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à OpsGenie.</span><span class="sxs-lookup"><span data-stu-id="40d02-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to OpsGenie.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="40d02-221">**Pour affecter Britta Simon à OpsGenie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="40d02-221">**To assign Britta Simon to OpsGenie, perform the following steps:**</span></span>

1. <span data-ttu-id="40d02-222">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="40d02-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="40d02-224">Dans la liste des applications, sélectionnez **OpsGenie**.</span><span class="sxs-lookup"><span data-stu-id="40d02-224">In the applications list, select **OpsGenie**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_app.png) 

3. <span data-ttu-id="40d02-226">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="40d02-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="40d02-228">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="40d02-228">Click **Add** button.</span></span> <span data-ttu-id="40d02-229">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="40d02-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="40d02-231">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="40d02-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="40d02-232">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="40d02-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="40d02-233">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="40d02-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="40d02-234">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="40d02-234">Testing single sign-on</span></span>

<span data-ttu-id="40d02-235">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="40d02-235">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="40d02-236">Quand vous cliquez sur la vignette OpsGenie dans le volet d’accès, vous devez être connecté automatiquement à votre application OpsGenie.</span><span class="sxs-lookup"><span data-stu-id="40d02-236">When you click the OpsGenie tile in the Access Panel, you should get automatically signed-on to your OpsGenie application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="40d02-237">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="40d02-237">Additional resources</span></span>

* [<span data-ttu-id="40d02-238">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="40d02-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="40d02-239">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="40d02-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_203.png

